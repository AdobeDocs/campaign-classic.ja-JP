---
product: campaign
title: RDBMS 固有のレコメンデーション
description: RDBMS 固有のレコメンデーション
feature: Monitoring
badge-v7-prem: label="オンプレミス／ハイブリッドのみ" type="Caution" url="https://experienceleague.adobe.com/docs/campaign-classic/using/installing-campaign-classic/architecture-and-hosting-models/hosting-models-lp/hosting-models.html?lang=ja" tooltip="オンプレミスデプロイメントとハイブリッドデプロイメントにのみ適用されます"
audience: production
content-type: reference
topic-tags: database-maintenance
exl-id: a586d70b-1b7f-47c2-a821-635098a70e45
TQID: https://experienceleague.adobe.com/WmadkiwNNUMeQSnm8O4NJjnv1GQHvO6hZ9kqtoGBySA
product_v2: id: dfc56824-e8b9-499e-85d4-21aedb507314
topic_v2: id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
source-git-commit: 4c295c0dabae8aba298390a3da2422a3fa1219f9
workflow-type: tm+mt
source-wordcount: 1305
ht-degree: 4%

---

# RDBMS 固有のレコメンデーション{#rdbms-specific-recommendations}



この節では、メンテナンスプランの設定に役立つように、Adobe Campaignがサポートする様々なRDBMS エンジンに適応した推奨事項とベストプラクティスを示します。 ただし、これらは推奨事項に過ぎません。 あなたのニーズに合わせて、あなたの内部手順と制約に合わせてそれらを適応させるのは、あなた次第です。 データベース管理者には、これらのプランを構築して実行する責任があります。

## PostgreSQL {#postgresql}

### 大きなテーブルの検出 {#detecting-large-tables}

1. 次のビューをデータベースに追加できます。

   ```
   create or replace view uvSpace
    as
    SELECT c1.relname AS tablename, c2.relname AS indexname, c2.relpages * 8  / 1024 AS size_mbytes, c2.relfilenode AS filename, cast(0 AS bigint) AS row_count
    FROM pg_class c1, pg_class c2, pg_index i
    WHERE c1.oid = i.indrelid AND i.indexrelid = c2.oid
    UNION
    SELECT pg_class.relname AS tablename, NULL::"unknown" AS indexname, pg_class.relpages * 8  /1024  AS size_mbytes, pg_class.relfilenode AS filename, cast(pg_class.reltuples as bigint) AS row_count
    FROM pg_class
    WHERE pg_class.relkind = 'r'::"char"
    ORDER BY 3 DESC, 1, 2 DESC;
   ```

1. このクエリを実行して、大きなテーブルとインデックスを見つけることができます。

   ```
   SELECT * FROM uvSpace;
   ```

   または、このクエリを実行して、すべてのインデックスサイズをまとめて表示することもできます。

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
>Adobeは、Campaign Adobeでホストされているデータベース設定でVACUUM FULLを実行しないことを強くお勧めします。推奨されるメンテナンスは、オンプレミスでのインストールに関するガイドです。 カスタムテーブル実装とスキーマの場合は、VACUUM FULLを監視せずに使用すると、テーブルを排他的にロックしてクエリが停止する可能性があり、場合によってはデータベース全体をロックする可能性があります。

PostgreSQLでは、次の一般的なキーワードを使用できます。

* VACUUM （FULL, ANALYZE, VERBOSE）

VACUUM操作を実行し、分析して時間を計るには、次の構文を使用できます。

```
\timing on
VACUUM (FULL, ANALYZE, VERBOSE) <table>;
```

ANALYZE ステートメントを省略しないことを強くお勧めします。 それ以外の場合、バキュームされたテーブルは統計情報なしで残されます。 その理由は、新しいテーブルが作成され、古いテーブルが削除されるためです。 その結果、テーブルのオブジェクト ID （OID）は変更されますが、統計情報は計算されません。 その結果、パフォーマンスの問題が即座に発生します。

定期的に実行されるSQL メンテナンス計画の一般的な例を次に示します。

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
>* Adobeでは、小さいテーブルから始めることをお勧めします。これにより、大きなテーブルでプロセスが失敗した場合（失敗のリスクが最も高い場合）、メンテナンスの少なくとも一部が完了しています。
>* Adobeでは、データモデルに固有のテーブルを追加することをお勧めします。これらのテーブルは、大幅に更新される可能性があります。 毎日の大規模なデータレプリケーションフローがある場合は、**NmsRecipient**&#x200B;の場合に該当します。
>* VACUUM ステートメントはテーブルをロックし、メンテナンスの実行中に一部のプロセスを一時停止します。
>* 非常に大きなテーブル（通常は5 Gb以上）の場合、VACUUM FULL ステートメントは非常に非効率的になり、非常に長い時間がかかります。 Adobeでは、**YyyNmsBroadLogXxx** テーブルに使用することはお勧めしません。
>* このメンテナンス操作は、**[!UICONTROL SQL]** アクティビティを使用して、Adobe Campaign ワークフローで実装できます。 バックアップウィンドウと競合しない低いアクティビティ時間のメンテナンスをスケジュールしてください。
>

### データベースの再構築 {#rebuilding-a-database}

PostgreSQLは、VACUUM FULL文がテーブルをロックするので、オンラインでのテーブル再構築を簡単に実行する方法を提供しません。 つまり、テーブルを使用しない場合はメンテナンスを実行する必要があります。 次のいずれかが可能です。

* Adobe Campaignプラットフォームが停止したら，
* 再構築されるテーブルに書き込む可能性のあるさまざまなAdobe Campaign サブサービスを停止します（**nlserver stop wfserver instance_name** to stop workflow process）。

次に、特定の関数を使用して必要なDDLを生成するテーブルのデフラグメント化の例を示します。 次のSQLでは、2つの新しい関数を作成できます。**GenRebuildTablePart1**&#x200B;と&#x200B;**GenRebuildTablePart2**。これは、テーブルを再作成するために必要なDDLを生成するために使用できます。

* 最初の関数を使用すると、元のテーブルのコピーである作業テーブル（ここ**_tmp**を作成できます。
* 次に、2つ目の関数は、元のテーブルを削除し、作業テーブルとそのインデックスの名前を変更します。
* 1つの関数ではなく2つの関数を使用すると、最初の関数が失敗した場合、元のテーブルを削除するリスクは発生しません。

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

次の例は、**vacuum/rebuild** コマンドを使用せずに、必要なテーブルを再構築するワークフローで使用できます。

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

お使いのバージョンのOracleに最適な手順については、データベース管理者にお問い合わせください。

## Microsoft SQL Server {#microsoft-sql-server}

>[!NOTE]
>
>Microsoft SQL Serverの場合は、[このページ ](https://ola.hallengren.com/sql-server-index-and-statistics-maintenance.html)で詳細に説明されているメンテナンスプランを使用できます。

次の例は、Microsoft SQL Server 2005に関するものです。 別のバージョンを使用している場合は、データベース管理者に連絡してメンテナンス手順について確認してください。

1. まず、管理者権限を持つログイン権限でMicrosoft SQL Server Management Studioに接続します。
1. **[!UICONTROL 管理/ メンテナンスプラン]** フォルダーに移動し、フォルダーを右クリックして、**[!UICONTROL メンテナンスプランアシスタント]**&#x200B;を選択します。
1. 最初のページが表示されたら、**[!UICONTROL 次へ]**&#x200B;をクリックします。
1. 作成するメンテナンスプランのタイプ（各タスクの個別のスケジュールまたはプラン全体の単一のスケジュール）を選択し、「**[!UICONTROL 変更…]**」ボタンをクリックします。
1. **[!UICONTROL ジョブスケジュールのプロパティ]** ウィンドウで、必要な実行設定を選択し、**[!UICONTROL OK]**&#x200B;をクリックしてから、**[!UICONTROL 次へ]**&#x200B;をクリックします。
1. 実行するメンテナンスタスクを選択し、**[!UICONTROL 次へ]**&#x200B;をクリックします。

   >[!NOTE]
   >
   >少なくとも以下に示すメンテナンスタスクを実行することをお勧めします。 統計更新タスクを選択することもできます。ただし、このタスクはデータベースのクリーンアップワークフローによって既に実行されています。

1. ドロップダウンリストで、**[!UICONTROL データベースチェック整合性]** タスクを実行するデータベースを選択します。
1. データベースを選択し、**[!UICONTROL OK]**&#x200B;をクリックしてから、**[!UICONTROL 次へ]**&#x200B;をクリックします。
1. データベースに割り当てられた最大サイズを設定し、**[!UICONTROL 次へ]**&#x200B;をクリックします。

   >[!NOTE]
   >
   >データベースのサイズがこの閾値を超える場合、メンテナンスプランは未使用データの削除を試みて空き容量を増やします。

1. インデックスの再編成または再構築：

   * インデックスの断片化率が10%から40%の場合は、再編をお勧めします。

     再整理するデータベースとオブジェクト （テーブルまたはビュー）を選択し、**[!UICONTROL 次へ]**&#x200B;をクリックします。

     >[!NOTE]
     >
     >設定に応じて、以前に選択したテーブルまたはデータベース内のすべてのテーブルを選択できます。

   * インデックスの断片化率が40%を超える場合は、再構築をお勧めします。

     インデックスの再構築タスクに適用するオプションを選択し、**[!UICONTROL 次へ]**&#x200B;をクリックします。

     >[!NOTE]
     >
     >インデックスの再構築プロセスは、プロセッサの使用に関してより制約が多く、データベース リソースがロックされます。 再構築の際にインデックスを利用できるようにするには、「**[!UICONTROL インデックスをオンラインで再インデックス化する]**」オプションを選択します。

1. アクティビティレポートに表示するオプションを選択し、**[!UICONTROL 次へ]**&#x200B;をクリックします。
1. メンテナンスプランに設定されているタスクのリストを確認し、**[!UICONTROL 終了]**&#x200B;をクリックします。

   メンテナンス計画の概要と、その様々な手順のステータスが表示されます。

1. メンテナンスプランが完了したら、**[!UICONTROL 閉じる]**&#x200B;をクリックします。
1. Microsoft SQL Server エクスプローラーで、**[!UICONTROL 管理/ メンテナンスプラン]** フォルダーをダブルクリックします。
1. Adobe Campaign メンテナンスプランを選択します。様々な手順についてワークフローで詳しく説明します。

   オブジェクトが&#x200B;**[!UICONTROL SQL Server エージェント > ジョブ]** フォルダーに作成されていることに注意してください。 このオブジェクトを使用すると、メンテナンス計画を開始できます。 この例では、すべてのメンテナンスタスクが同じプランの一部であるため、オブジェクトは1つだけです。

   >[!IMPORTANT]
   >
   >このオブジェクトを実行するには、Microsoft SQL Server エージェントを有効にする必要があります。

**作業テーブル用の別のデータベースの設定**

>[!NOTE]
>
>この設定はオプションです。

「**WdbcOptions_TempDbName**」オプションを使用すると、Microsoft SQL Server 上で、ワークテーブル向けに別のデータベースを構成できます。 これにより、バックアップとレプリケーションが最適化されます。

このオプションは、作業用テーブル（ワークフローの実行時に作成されたテーブルなど）を別のデータベースに作成する場合に使用できます。

オプションを「tempdb.dbo」に設定すると、作業テーブルはMicrosoft SQL Serverのデフォルトの一時データベースに作成されます。 データベース管理者は、tempdb データベースへの書き込みアクセスを許可する必要があります。

このオプションが設定されている場合は、Adobe Campaignで設定されているすべてのMicrosoft SQL Server データベース（メインデータベースと外部アカウント）で使用されます。 2つの外部アカウントが同じサーバーを共有している場合、（tempdbが一意であるため）競合が発生する可能性があることに注意してください。 同様に、2つのCampaign インスタンスが同じMSSQL サーバーを使用している場合、同じtempdbを使用している場合に競合が発生する可能性があります。
