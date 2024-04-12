---
product: campaign
title: RDBMS 固有のレコメンデーション
description: RDBMS 固有のレコメンデーション
feature: Monitoring
badge-v7-prem: label="オンプレミスおよびハイブリッド" type="Caution" url="https://experienceleague.adobe.com/docs/campaign-classic/using/installing-campaign-classic/architecture-and-hosting-models/hosting-models-lp/hosting-models.html?lang=ja" tooltip="オンプレミスデプロイメントとハイブリッドデプロイメントにのみ適用されます"
audience: production
content-type: reference
topic-tags: database-maintenance
exl-id: a586d70b-1b7f-47c2-a821-635098a70e45
source-git-commit: b666535f7f82d1b8c2da4fbce1bc25cf8d39d187
workflow-type: tm+mt
source-wordcount: '1280'
ht-degree: 4%

---

# RDBMS 固有のレコメンデーション{#rdbms-specific-recommendations}



メンテナンスプランを設定しやすくするために、Adobe Campaignがサポートする様々な RDBMS エンジンに適合する推奨事項とベストプラクティスをいくつか示します。 ただし、これらは推奨事項にすぎません。 社内の手順や制約に合わせて、ニーズに合わせて調整するかどうかはユーザー次第です。 データベース管理者は、これらの計画を作成および実行する責任を負います。

## PostgreSQL {#postgresql}

### 大きいテーブルの検出 {#detecting-large-tables}

1. データベースに次のビューを追加できます。

   ```
   create or replace view uvSpace
    as
    SELECT c1.relname AS tablename, c2.relname AS indexname, c2.relpages * 8 / 1024 AS size_mbytes, c2.relfilenode AS filename, 0 AS row_count
    FROM pg_class c1, pg_class c2, pg_index i
    WHERE c1.oid = i.indrelid AND i.indexrelid = c2.oid
    UNION 
    SELECT pg_class.relname AS tablename, NULL::"unknown" AS indexname, pg_class.relpages * 8 / 1024 AS size_mbytes, pg_class.relfilenode AS filename, cast(pg_class.reltuples as integer) AS row_count
    FROM pg_class
    WHERE pg_class.relkind = 'r'::"char"
    ORDER BY 3 DESC, 1, 2 DESC;
   ```

1. このクエリを実行すると、大きなテーブルとインデックスを検出できます。

   ```
   SELECT * FROM uvSpace;
   ```

   または、例えばこのクエリを実行して、すべてのインデックスサイズをまとめて確認することもできます。

   ```
   SELECT
      tablename,
      sum(size_mbytes) AS "sizeMB_all",
      (
         SELECT sum(size_mbytes)
         FROM uvspace
         AS uv2
         WHERE
            INDEXNAME IS NULL
            AND uv1.tablename = uv2.tablename
      ) AS "sizeMB_data",
      (
         SELECT sum(size_mbytes)
         FROM uvspace 
         AS uv2 
         WHERE
            INDEXNAME IS NOT NULL
            AND uv1.tablename = uv2.tablename
      ) AS "sizeMB_index",
      (
         SELECT ROW_COUNT
         FROM uvspace
         AS uv2
         WHERE
            INDEXNAME IS NULL
            AND uv1.tablename = uv2.tablename
      ) AS ROWS FROM uvspace AS uv1
      GROUP BY tablename
      ORDER BY 2 DESC
   ```

### シンプルなメンテナンス {#simple-maintenance}

>[!IMPORTANT]
>
>Adobeでは、Campaign Adobeがホストするデータベース設定で VACUUM FULL を実行しないことを強くお勧めします。推奨されるメンテナンスは、オンプレミスインストール専用のガイドです。 カスタムテーブルの実装やスキーマの場合、VACUUM FULL はご自身のリスクで使用してください。VACUUM は、監視なしで、クエリの停止を引き起こすテーブルのみをロックし、場合によってはデータベース全体をロックすることができます。

PostgreSQL では、次の一般的なキーワードを使用できます。

* 真空（完全、分析、詳細）

VACUUM 操作を実行し、分析し、時間を計算するには、次の構文を使用します。

```
\timing on
VACUUM (FULL, ANALYZE, VERBOSE) <table>;
```

ANALYZE ステートメントを省略しないことを強くお勧めします。 それ以外の場合は、バキュームされたテーブルは統計なしで残されます。 理由は、新しいテーブルが作成され、古いテーブルが削除されるためです。 その結果、テーブルのオブジェクト ID （OID）が変更されますが、統計は計算されません。 その結果、パフォーマンスの問題が直ちに発生します。

次に、定期的に実行する SQL メンテナンスプランの典型的な例を示します。

```
\timing on
VACUUM (FULL, ANALYZE, VERBOSE) nmsdelivery;

\timing on
VACUUM (FULL, ANALYZE, VERBOSE) nmsdeliverystat;

\timing on
VACUUM (FULL, ANALYZE, VERBOSE) xtkworkflow;

\timing on
VACUUM (FULL, ANALYZE, VERBOSE) xtkworkflowevent;

\timing on
VACUUM (FULL, ANALYZE, VERBOSE) xtkworkflowjob;

\timing on
VACUUM (FULL, ANALYZE, VERBOSE) xtkworkflowlog;

\timing on
VACUUM (FULL, ANALYZE, VERBOSE) xtkworkflowtask;

\timing on
VACUUM (FULL, ANALYZE, VERBOSE) xtkjoblog;

\timing on
VACUUM (FULL, ANALYZE, VERBOSE) xtkjob;

\timing on
VACUUM (FULL, ANALYZE, VERBOSE) nmsaddress;

\timing on
VACUUM (FULL, ANALYZE, VERBOSE) nmsdeliverypart;

\timing on
VACUUM (FULL, ANALYZE, VERBOSE) nmsmirrorpageinfo;
```

>[!NOTE]
>
>* Adobeでは、まず小さいテーブルから始めることをお勧めします。こうすることで、大きいテーブル（エラーのリスクが最も高い）でプロセスが失敗した場合、少なくとも一部のメンテナンスが完了します。
>* Adobeでは、データモデルに固有のテーブルを追加することをお勧めします。テーブルは大幅に更新される場合があります。 以下の場合があります **NmsRecipient** 毎日のデータレプリケーションフローが大きい場合。
>* VACUUM 文はテーブルをロックし、メンテナンスの実行中に一部のプロセスを一時停止します。
>* 非常に大きなテーブル（通常は 5 Gb を超える）の場合、VACUUM FULL 文は非常に非効率的になり、非常に長い時間がかかる可能性があります。 Adobeでは、以下で使用することはお勧めしません **YyyNmsBroadLogXxx** テーブル。
>* Adobe Campaignこのメンテナンス操作は、 **[!UICONTROL SQL]** アクティビティ。 詳しくは、[この節](../../workflow/using/architecture.md)を参照してください。バックアップウィンドウと競合しない低アクティビティ時間のメンテナンスをスケジュールしてください。
>

### データベースの再構築 {#rebuilding-a-database}

VACUUM FULL 文はテーブルをロックするので、通常の生成を防ぐことができるので、PostgreSQL はオンラインテーブルの再構築を簡単に行う方法を提供していません。 つまり、テーブルが使用されていない場合は、メンテナンスを実行する必要があります。 次のいずれかが可能です。

* Adobe Campaign プラットフォームが停止したらメンテナンスを実行する。
* 再構築するテーブルに書き込む可能性のある様々なAdobe Campaign サブサービスを停止します（**nlserver wfserver instance_name の停止** （ワークフロープロセスを停止します）。

次に、特定の関数を使用して必要な DDL を生成するテーブルの最適化の例を示します。 次の SQL を使用すると、2 つの新しい関数を作成できます。 **GenRebuildTablePart1** および **GenRebuildTablePart2**：テーブルの再作成に必要な DDL の生成に使用できます。

* 最初の関数では、元のテーブルのコピーであるワークテーブル（ここでは_tmp**を**します）を作成できます。
* 2 番目の関数は、元のテーブルを削除し、ワークテーブルとそのインデックスの名前を変更します。
* 1 つではなく 2 つの関数を使用すると、最初の関数が失敗した場合でも、元のテーブルが削除されるリスクがなくなります。

```
 -- --------------------------------------------------------------------------
 -- Generate the CREATE TABLE DDL for a table
 -- --------------------------------------------------------------------------
 create or replace function GenTableDDL(text) returns text as $$
 declare
 vstrTable text;
 vrecFld RECORD;
 vstrDDL text;
 vstrFields text;
 vstrNsTable text;
 vstrTableSpace text;
 begin
 vstrTable = lower($1);
 
 vstrDDL = ;
 
 SELECT
 pg_catalog.quote_ident(n.nspname) || '.' || pg_catalog.quote_ident(c.relname),
 pg_catalog.quote_ident(t.spcname)
 INTO
 vstrNsTable, vstrTableSpace
 FROM
 pg_namespace n, pg_class c left outer join pg_tablespace t on c.reltablespace = t.oid
 WHERE
 n.oid = c.relnamespace AND
 c.relname = vstrTable;
 
 vstrDDL = 'CREATE TABLE ' || vstrNsTable || '_tmp(';
 
 vstrFields = ;
 FOR vrecFld IN
 SELECT
 pg_catalog.quote_ident(a.attname) ||
 ' ' || t.typname ||
 case when t.typname='varchar' then '(' || cast(a.atttypmod-4 as text) || ')'
 when t.typname='numeric' then '(' || cast((a.atttypmod-4)/65536 as text) || ',' || cast((a.atttypmod-4)%65536 as text) || ')'
 else end ||
 case when a.attnotnull then ' not null' else end ||
 case when a.atthasdef then ' default '|| d.adsrc else end as DDL
 FROM
 pg_type t, pg_class c, pg_attribute a LEFT OUTER JOIN pg_attrdef d ON d.adrelid=a.attrelid and d.adnum=a.attnum
 WHERE 
 a.attnum > 0 AND
 a.attrelid = c.oid AND
 t.oid = a.atttypid AND
 c.relname = vstrTable
 ORDER BY
 a.attnum
 LOOP
 IF vstrFields <> THEN
 vstrFields = vstrFields || ',' || chr(10) || ' ';
 ELSE
 vstrFields = vstrFields || chr(10) || ' ';
 END IF;
 vstrFields = vstrFields || vrecFld.DDL;
 END LOOP;
 
 vstrDDL = vstrDDL || vstrFields || chr(10) || ')';
 if vstrTableSpace <> then
 vstrDDL = vstrDDL || ' TABLESPACE ' || vstrTableSpace;
 end if;
 vstrDDL = vstrDDL || ';' || chr(10);
 
 return vstrDDL;
 END;
 $$ LANGUAGE plpgsql;

 -- --------------------------------------------------------------------------
 -- Generate the CREATE INDEX DDL for a table
 -- --------------------------------------------------------------------------
 create or replace function GenIndexDDL(text) returns text as $$
 declare
 vstrTable text;
 vrecIndex RECORD;
 vstrDDL text;
 viFld integer;
 vstrFld text;
 begin
 vstrTable = lower($1);
 
 vstrDDL = ;
 
 FOR vrecIndex IN
 SELECT
 i.indkey, i.indisunique,
 pg_catalog.quote_ident(c.relname) as tablename,
 pg_catalog.quote_ident(ic.relname) as indexname,
 pg_catalog.quote_ident(t.spcname) as tablespace
 FROM
 pg_class c, pg_index i, pg_class ic left outer join pg_tablespace t on ic.reltablespace = t.oid
 WHERE
 i.indexrelid = ic.oid AND
 i.indrelid = c.oid AND
 c.relname = vstrTable
 LOOP
 
  vstrDDL = vstrDDL || 'CREATE ';
  if vrecIndex.indisunique then
  vstrDDL = vstrDDL || 'UNIQUE ';
  end if;
  vstrDDL = vstrDDL ||
   'INDEX ' ||vrecIndex.indexname || '_tmp ON ' ||
   vrecIndex.tablename || '_tmp(';
 
  FOR viFld IN array_lower(vrecIndex.indkey, 1) .. array_upper(vrecIndex.indkey, 1) LOOP
  SELECT pg_catalog.quote_ident(a.attname) INTO vstrFld 
  FROM 
   pg_attribute a, pg_class c
  WHERE 
   a.attnum = vrecIndex.indkey[viFld] AND
   a.attrelid = c.oid AND c.relname=vstrTable;
  
  vstrDDL = vstrDDL || vstrFld;
  if viFld <> array_upper(vrecIndex.indkey, 1) then
   vstrDDL = vstrDDL || ', ';
  end if;
  END LOOP;
  vstrDDL = vstrDDL || ')';
 
  if vrecIndex.tablespace <> then
  vstrDDL = vstrDDL || 'TABLESPACE ' || vrecIndex.tablespace;
  end if;
  vstrDDL = vstrDDL || ';' || chr(10);
 
 END LOOP;
 
 return vstrDDL;
 END;
 $$ LANGUAGE plpgsql;

 -- --------------------------------------------------------------------------
 -- Generate the ALTER INDEX RENAME for a table
 -- --------------------------------------------------------------------------
 create or replace function GenRenameIndexDDL(text) returns text as $$
 declare
 vstrTable text;
 vrecIndex RECORD;
 vstrDDL text;
 begin
 vstrTable = lower($1);
 
 vstrDDL = ;
 
 FOR vrecIndex IN
  SELECT
  pg_catalog.quote_ident(n.nspname) as namespace,
  pg_catalog.quote_ident(ic.relname) as indexname
  FROM
  pg_namespace n, pg_class c, pg_index i, pg_class ic
  WHERE
  i.indexrelid = ic.oid AND
  n.oid = ic.relnamespace AND
  i.indrelid = c.oid AND
  c.relname = vstrTable
 LOOP
 
  vstrDDL = vstrDDL || 'ALTER INDEX ' || vrecIndex.namespace || '.' || vrecIndex.indexname ||
    '_tmp RENAME TO ' || vrecIndex.indexname ||
    ';' || chr(10);
 END LOOP;
 
 return vstrDDL;
 END;
 $$ LANGUAGE plpgsql;

 -- --------------------------------------------------------------------------
 -- Build a copy of a table, with index
 -- --------------------------------------------------------------------------
 create or replace function GenRebuildTablePart1(text) returns text as $$
 declare
 vstrTable text;
 vstrTmp text;
 vstrDDL text;
 begin
 vstrTable = lower($1);
  
 vstrDDL = ;
 
 SELECT GenTableDDL(vstrTable) INTO vstrTmp;
 vstrDDL = vstrDDL|| vstrTmp || chr(10);
 
 vstrDDL = vstrDDL|| 'INSERT INTO ' || vstrTable || '_tmp SELECT * FROM ' || vstrTable || ';'||chr(10);
 SELECT GenIndexDDL(vstrTable) INTO vstrTmp;
 
 vstrDDL = vstrDDL|| vstrTmp || chr(10);
 vstrDDL = vstrDDL|| 'VACUUM ANALYSE '|| vstrTable || '_tmp;' ||chr(10);
 
 return vstrDDL;
 end;
 $$ LANGUAGE plpgsql;
 
 -- --------------------------------------------------------------------------
 -- Drop the original table and rename the copy
 -- --------------------------------------------------------------------------
 create or replace function GenRebuildTablePart2(text) returns text as $$
 declare
 vstrTable text;
 vstrTmp text;
 vstrDDL text;
 begin
 vstrTable = lower($1);
  
 vstrDDL = 'DROP TABLE ' || vstrTable||';'|| chr(10);
 vstrDDL = vstrDDL|| 'ALTER TABLE ' || vstrTable || '_tmp RENAME TO ' || vstrTable ||';'|| chr(10);
 
 SELECT GenRenameIndexDDL(vstrTable) INTO vstrTmp;
 vstrDDL = vstrDDL|| vstrTmp || chr(10);
 
 return vstrDDL;
 end;
 $$ LANGUAGE plpgsql;
```

次の例は、必要なテーブルを再構築するワークフローで、 **真空/再構築** コマンド：

```
function sqlGetMemo(strSql)
 {
 var res = sqlSelect("s, m:memo", strSql);
 return res.s.m.toString();
 }

 function RebuildTable(strTable)
 {
 // Rebuild a table_tmp
 var strSql = sqlGetMemo("select GenRebuildTablePart1('"+strTable+"')");
 logInfo("Rebuilding table '"+strTable+"'...");
 // logInfo(strSql);
 sqlExec(strSql);
 
 // If fails, there is an exception thrown and so we do not delete the original table
 strSql = sqlGetMemo("select GenRebuildTablePart2('"+strTable+"')");
 logInfo("Swapping table '"+strTable+"'...");
 //logInfo(strSql);
 sqlExec(strSql);
 }
 
 RebuildTable('nmsrecipient');
 RebuildTable('nmsrcpgrlrel');
 // ... other tables here
```

## Oracle {#oracle}

ご使用のOracleのバージョンに最適な手順については、データベース管理者にお問い合わせください。

## Microsoft SQL Server {#microsoft-sql-server}

>[!NOTE]
>
>Microsoft SQL Server の場合は、に詳しく記載されているメンテナンスプランを使用できます。 [このページ](https://ola.hallengren.com/sql-server-index-and-statistics-maintenance.html).

次の例は、Microsoft SQL Server 2005 に関するものです。 別のバージョンを使用している場合は、データベース管理者に連絡してメンテナンス手順を確認してください。

1. まず、管理者権限を持つログインを使用して、Microsoft SQL Server Management Studio に接続します。
1. に移動します **[!UICONTROL 管理/メンテナンス・プラン]** フォルダーを右クリックし、以下を選択します **[!UICONTROL メンテナンス計画ウィザード]**.
1. クリック **[!UICONTROL 次]** 最初のページが表示されたとき。
1. 作成するメンテナンス・プランのタイプ（タスクごとに個別のスケジュール、またはプラン全体に対して単一のスケジュール）を選択し、 **[!UICONTROL 変更…]** ボタン。
1. が含まれる **[!UICONTROL ジョブスケジュールのプロパティ]** ウィンドウで目的の実行設定を選択し、 **[!UICONTROL OK]**&#x200B;を選択し、 **[!UICONTROL 次]**.
1. 実行するメンテナンスタスクを選択し、 **[!UICONTROL 次]**.

   >[!NOTE]
   >
   >少なくとも、以下に示すメンテナンスタスクを実行することをお勧めします。 統計の更新タスクは、データベースクリーンアップワークフローで既に実行されていますが、選択することもできます。

1. ドロップダウンリストで、を実行するデータベースを選択します **[!UICONTROL データベース チェックの整合性]** タスク。
1. データベースを選択し、 **[!UICONTROL OK]**&#x200B;を選択し、 **[!UICONTROL 次]**.
1. データベースに割り当てる最大サイズを設定し、 **[!UICONTROL 次]**.

   >[!NOTE]
   >
   >データベースのサイズがこのしきい値を超えると、メンテナンス プランは未使用のデータを削除して領域を解放しようとします。

1. インデックスを再構成または再構築します。

   * インデックスの断片化レートが 10%～40% の場合は、再編成を推奨します。

     再編成するデータベースおよびオブジェクト（テーブルまたはビュー）を選択し、 **[!UICONTROL 次]**.

     >[!NOTE]
     >
     >設定に応じて、以前に選択したテーブルまたはデータベース内のすべてのテーブルを選択できます。

   * インデックスの断片化の割合が 40% より大きい場合は、再構築を推奨します。

     インデックス再作成タスクに適用するオプションを選択し、 **[!UICONTROL 次]**.

     >[!NOTE]
     >
     >インデックスの再構築プロセスは、プロセッサの使用に関してさらに制約を受け、データベース・リソースをロックします。 「」を選択します **[!UICONTROL インデックス再作成中にインデックスをオンラインに維持]** 再構築時にインデックスを使用できるようにする場合は、「」オプションを選択します。

1. アクティビティレポートに表示するオプションを選択し、をクリックします **[!UICONTROL 次]**.
1. メンテナンス・プランに対して構成されているタスクのリストを確認し、 **[!UICONTROL 終了]**.

   保守プランのサマリーと、その様々なステップのステータスが表示されます。

1. メンテナンス計画が完了したら、 **[!UICONTROL 閉じる]**.
1. Microsoft SQL Server エクスプローラーで、 **[!UICONTROL 管理/メンテナンス・プラン]** フォルダー。
1. Adobe Campaign メンテナンスプランを選択します（様々な手順の詳細がワークフローに記載されています）。

   でオブジェクトが作成されています。 **[!UICONTROL SQL Server エージェント/ジョブ]** フォルダー。 このオブジェクトを使用すると、メンテナンスプランを開始できます。 この例では、すべてのメンテナンスタスクが同じプランの一部なので、オブジェクトは 1 つだけです。

   >[!IMPORTANT]
   >
   >このオブジェクトを実行するには、Microsoft SQL Server エージェントを有効にする必要があります。

**ワークテーブル用の個別のデータベースの設定**

>[!NOTE]
>
>この設定はオプションです。

「**WdbcOptions_TempDbName**」オプションを使用すると、Microsoft SQL Server 上で、ワークテーブル向けに別のデータベースを構成できます。これにより、バックアップとレプリケーションが最適化されます。

このオプションは、ワークテーブル（ワークフローの実行中に作成されたテーブルなど）を別のデータベースに作成する場合に使用できます。

オプションを「tempdb.dbo.」に設定すると、ワークテーブルはMicrosoft SQL Server のデフォルトの一時データベースに作成されます。 データベース管理者は、tempdb データベースへの書き込みアクセスを許可する必要があります。

このオプションが設定されている場合は、Adobe Campaign（メインデータベースと外部アカウント）に設定されているすべてのMicrosoft SQL Server データベースで使用されます。 2 つの外部アカウントが同じサーバーを共有している場合、（tempdb が一意なので）競合が発生する可能性があることに注意してください。 同様に、2 つの Campaign インスタンスが同じ MSSQL サーバーを使用している場合、同じ tempdb を使用すると競合が発生する可能性があります。
