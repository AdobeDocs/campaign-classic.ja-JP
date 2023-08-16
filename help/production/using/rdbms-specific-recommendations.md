---
product: campaign
title: RDBMS 固有の推奨事項
description: RDBMS 固有の推奨事項
feature: Monitoring
badge-v7-only: label="v7" type="Informative" tooltip="Campaign Classic v7 にのみ適用されます"
badge-v7-prem: label="オンプレミスおよびハイブリッド" type="Caution" url="https://experienceleague.adobe.com/docs/campaign-classic/using/installing-campaign-classic/architecture-and-hosting-models/hosting-models-lp/hosting-models.html?lang=ja" tooltip="オンプレミスデプロイメントとハイブリッドデプロイメントにのみ適用されます"
audience: production
content-type: reference
topic-tags: database-maintenance
exl-id: a586d70b-1b7f-47c2-a821-635098a70e45
source-git-commit: 3a9b21d626b60754789c3f594ba798309f62a553
workflow-type: tm+mt
source-wordcount: '1239'
ht-degree: 5%

---

# RDBMS 固有の推奨事項{#rdbms-specific-recommendations}



メンテナンスプランの設定に役立つように、この節では、Adobe Campaignがサポートする様々な RDBMS エンジンに適した推奨事項とベストプラクティスを示します。 ただし、これらは単なる推奨事項です。 内部の手順や制約に従って、ニーズに合わせて変更を加えるかどうかは、お客様次第です。 データベース管理者は、これらのプランを作成して実行する責任を負います。

## PostgreSQL {#postgresql}

### 大きなテーブルの検出 {#detecting-large-tables}

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

1. このクエリを実行して、大きなテーブルやインデックスを見つけることができます。

   ```
   SELECT * FROM uvSpace;
   ```

   また、このクエリを実行して、例えば、すべてのインデックス・サイズを一括して表示することもできます。

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

### 簡単なメンテナンス {#simple-maintenance}

PostgreSQL では、次の一般的なキーワードを使用できます。

* 真空（完全、分析、詳細）

VACUUM 操作を実行し、分析して時間を計測するには、次の構文を使用します。

```
\timing on
VACUUM (FULL, ANALYZE, VERBOSE) <table>;
```

ANALYZE 文は省略しないことを強くお勧めします。 それ以外の場合、バキュームされたテーブルは統計情報を含まないままになります。 これは、新しいテーブルが作成され、古いテーブルが削除されるからです。 その結果、テーブルのオブジェクト ID(OID) は変更されますが、統計は計算されません。 その結果、パフォーマンスに関する問題が直ちに発生します。

定期的に実行される SQL メンテナンス計画の典型的な例を次に示します。

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
>* Adobeでは、小さいテーブルから始めることをお勧めします。この方法を使用すると、大きなテーブル（失敗のリスクが最も高い）でプロセスが失敗した場合、メンテナンスの少なくとも一部が完了しています。
>* Adobeでは、大幅な更新が必要となる、データモデルに固有のテーブルを追加することをお勧めします。 これは、次の場合に該当します。 **NmsRecipient** 日別のデータレプリケーションフローが大きい場合。
>* VACUUM 文はテーブルをロックし、メンテナンスの実行中に一部のプロセスを一時停止します。
>* 非常に大きなテーブル（通常は 5 Gb を超える）の場合、VACUUM FULL 文は非常に非効率になり、非常に長い時間がかかる可能性があります。 Adobeでは、 **YyyNmsBroadLogXxx** 表。
>* このメンテナンス操作は、Adobe Campaignワークフローで、 **[!UICONTROL SQL]** アクティビティ。 詳しくは、[この節](../../workflow/using/architecture.md)を参照してください。バックアップウィンドウに衝突しない低アクティビティ時間のメンテナンスをスケジュールしてください。
>

### データベースの再構築 {#rebuilding-a-database}

VACUUM FULL 文はテーブルをロックするので、通常の実稼動を防ぐので、PostgreSQL はオンラインテーブルの再構築を簡単に実行する方法を提供しません。 つまり、テーブルを使用しない場合はメンテナンスを実行する必要があります。 次のいずれかが可能です。

* Adobe Campaign platform が停止したら、メンテナンスを実行します。
* 再構築中のテーブルに書き込まれる可能性が高い様々なAdobe Campaignサブサービスを停止します (**nlserver stop wfserver instance_name** 」をクリックして、ワークフロープロセスを停止します )。

次に、必要な DDL を生成する特定の関数を使用したテーブルの最適化の例を示します。 次の SQL では、2 つの新しい関数を作成できます。 **GenRebuildTablePart1** および **GenRebuildTablePart2**：テーブルを再作成するために必要な DDL を生成するために使用できます。

* 1 つ目の関数では、元のテーブルのコピーである作業用テーブル ( ここでは** _tmp**) を作成できます。
* 次に、2 つ目の関数は、元のテーブルを削除し、作業用テーブルとそのインデックスの名前を変更します。
* 1 つではなく 2 つの関数を使用することは、最初の関数が失敗した場合に、元のテーブルを削除するリスクを回避することを意味します。

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

次の例は、ワークフローで、 **真空/再構築** コマンド：

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

お使いのデータベースのバージョンに最も適した手順については、Oracle管理者にお問い合わせください。

## Microsoft SQL Server {#microsoft-sql-server}

>[!NOTE]
>
>Microsoft SQL Server の場合は、次に詳しく説明するメンテナンスプランを使用できます。 [このページ](https://ola.hallengren.com/sql-server-index-and-statistics-maintenance.html).

次の例は、Microsoft SQL Server 2005 に関するものです。 別のバージョンを使用している場合は、データベース管理者に連絡してメンテナンス手順を確認してください。

1. まず、管理者権限を持つログインを使用して、Microsoft SQL Server Management Studio に接続します。
1. 次に移動： **[!UICONTROL 管理/メンテナンスプラン]** フォルダーを右クリックし、「 」を選択します。 **[!UICONTROL メンテナンスプランウィザード]**.
1. クリック **[!UICONTROL 次へ]** 最初のページが表示されたとき。
1. 作成するメンテナンスプランのタイプ（タスクごとに個別のスケジュールを選択するか、プラン全体で 1 つのスケジュールを選択する）を選択し、 **[!UICONTROL 変更…]** 」ボタンをクリックします。
1. Adobe Analytics の **[!UICONTROL ジョブスケジュールのプロパティ]** ウィンドウで、目的の実行設定を選択し、 **[!UICONTROL OK]**&#x200B;を選択し、次に **[!UICONTROL 次へ]**.
1. 実行するメンテナンスタスクを選択し、「 **[!UICONTROL 次へ]**.

   >[!NOTE]
   >
   >以下に示すメンテナンスタスクを少なくとも実行することをお勧めします。 統計の更新タスクも選択できますが、このタスクはデータベースクリーンアップワークフローによって既に実行されています。

1. ドロップダウンリストで、 **[!UICONTROL データベースの整合性チェック]** タスク。
1. データベースを選択し、 **[!UICONTROL OK]**&#x200B;を選択し、次に **[!UICONTROL 次へ]**.
1. データベースに割り当てる最大サイズを設定し、「 **[!UICONTROL 次へ]**.

   >[!NOTE]
   >
   >データベースのサイズがこのしきい値を超える場合、メンテナンスプランは、領域を解放するために未使用のデータを削除しようとします。

1. インデックスを再編成または再構築します。

   * インデックスの断片化率が 10%～40%の場合は、再編成をお勧めします。

     再編成するデータベースとオブジェクト（テーブルまたはビュー）を選択し、[ ] をクリックします。 **[!UICONTROL 次へ]**.

     >[!NOTE]
     >
     >設定に応じて、以前に選択したテーブルまたはデータベース内のすべてのテーブルを選択できます。

   * インデックスの断片化率が 40%を超える場合は、再構築をお勧めします。

     インデックスの再構築タスクに適用するオプションを選択し、 **[!UICONTROL 次へ]**.

     >[!NOTE]
     >
     >再構築インデックスプロセスは、プロセッサーの使用に関してより制約が高く、データベースリソースをロックします。 を選択します。 **[!UICONTROL インデックスの再作成中にインデックスをオンラインに保つ]** オプションを使用します。

1. アクティビティレポートに表示するオプションを選択し、 **[!UICONTROL 次へ]**.
1. メンテナンスプラン用に設定されたタスクの一覧を確認し、 **[!UICONTROL 完了]**.

   メンテナンスプランの概要と、その様々なステップのステータスが表示されます。

1. メンテナンスプランが完了したら、「 **[!UICONTROL 閉じる]**.
1. Microsoft SQL Server エクスプローラーで、 **[!UICONTROL 管理/メンテナンスプラン]** フォルダー。
1. Adobe Campaignメンテナンスプランを選択します。ワークフローでは、様々な手順について詳しく説明します。

   なお、 **[!UICONTROL SQL Server エージェント/ジョブ]** フォルダー。 このオブジェクトを使用して、メンテナンスプランを開始できます。 この例では、すべてのメンテナンスタスクが同じプランに含まれているので、オブジェクトは 1 つだけです。

   >[!IMPORTANT]
   >
   >このオブジェクトを実行するには、Microsoft SQL Server エージェントを有効にする必要があります。

**作業用テーブルに対する別のデータベースの設定**

>[!NOTE]
>
>この設定はオプションです。

「**WdbcOptions_TempDbName**」オプションを使用すると、Microsoft SQL Server 上で、ワークテーブル向けに別のデータベースを構成できます。これにより、バックアップとレプリケーションを最適化できます。

このオプションは、作業用テーブル（ワークフローの実行中に作成されたテーブルなど）を別のデータベースで作成する場合に使用できます。

このオプションを「tempdb.dbo」に設定すると、作業用テーブルがMicrosoft SQL Server のデフォルトの一時データベースに作成されます。 データベース管理者は、tempdb データベースへの書き込みアクセスを許可する必要があります。

このオプションを設定すると、Adobe Campaignで設定されているすべてのMicrosoft SQL Server データベース（メインデータベースおよび外部アカウント）でこのオプションが使用されます。 2 つの外部アカウントが同じサーバーを共有している場合は、（tempdb が一意なので）競合が発生する可能性があることに注意してください。 同様に、2 つの Campaign インスタンスが同じ MSSQL サーバーを使用する場合、同じ tempdb を使用すると競合が発生する可能性があります。
