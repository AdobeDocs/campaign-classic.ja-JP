---
product: campaign
title: RDBMS 固有の推奨事項
description: RDBMS 固有の推奨事項
audience: production
content-type: reference
topic-tags: database-maintenance
exl-id: a586d70b-1b7f-47c2-a821-635098a70e45
source-git-commit: 20509f44c5b8e0827a09f44dffdf2ec9d11652a1
workflow-type: tm+mt
source-wordcount: '1217'
ht-degree: 3%

---

# RDBMS 固有の推奨事項{#rdbms-specific-recommendations}

![](../../assets/v7-only.svg)

メンテナンス計画の設定に役立つように、この節では、Adobe Campaignがサポートする様々な RDBMS エンジンに適した推奨事項とベストプラクティスを示します。 ただし、これらは単なる推奨事項です。 内部の手順や制約に従って、ニーズに合わせて変更を加える必要があります。 データベース管理者は、これらのプランを作成して実行する責任を負います。

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

1. このクエリを実行して、大きなテーブルとインデックスを検索できます。

   ```
   SELECT * FROM uvSpace;
   ```

   また、このクエリを実行して、例えば、すべてのインデックス・サイズをまとめて表示することもできます。

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

PostgreSQL では、次の一般的なキーワードを使用できます。

* 真空（完全、分析、詳細）
* REINDEX

VACUUM 操作を実行し、分析して時間を計測するには、次の構文を使用します。

```
\timing on
VACUUM (FULL, ANALYZE, VERBOSE) <table>;
```

ANALYZE 文は省略しないことを強くお勧めします。 それ以外の場合は、バキュームされたテーブルに統計情報が残りません。 新しいテーブルが作成され、古いテーブルが削除されるのが理由です。 その結果、テーブルのオブジェクト ID(OID) は変更されますが、統計は計算されません。 その結果、パフォーマンスに関する問題が直ちに発生します。

定期的に実行される SQL メンテナンス計画の典型的な例を次に示します。

```
\timing on
VACUUM (FULL, ANALYZE, VERBOSE) nmsdelivery;
REINDEX TABLE nmsdelivery;

\timing on
VACUUM (FULL, ANALYZE, VERBOSE) nmsdeliverystat;
REINDEX TABLE nmsdeliverystat;

\timing on
VACUUM (FULL, ANALYZE, VERBOSE) xtkworkflow;
REINDEX TABLE xtkworkflow;

\timing on
VACUUM (FULL, ANALYZE, VERBOSE) xtkworkflowevent;
REINDEX TABLE xtkworkflowevent;

\timing on
VACUUM (FULL, ANALYZE, VERBOSE) xtkworkflowjob;
REINDEX TABLE xtkworkflowjob;

\timing on
VACUUM (FULL, ANALYZE, VERBOSE) xtkworkflowlog;
REINDEX TABLE xtkworkflowlog;

\timing on
VACUUM (FULL, ANALYZE, VERBOSE) xtkworkflowtask;
REINDEX TABLE xtkworkflowtask;

\timing on
VACUUM (FULL, ANALYZE, VERBOSE) xtkjoblog;
REINDEX TABLE xtkjoblog;

\timing on
VACUUM (FULL, ANALYZE, VERBOSE) xtkjob;
REINDEX TABLE xtkjob;

\timing on
VACUUM (FULL, ANALYZE, VERBOSE) nmsaddress;
REINDEX TABLE nmsaddress;

\timing on
VACUUM (FULL, ANALYZE, VERBOSE) nmsdeliverypart;
REINDEX TABLE nmsdeliverypart;

\timing on
VACUUM (FULL, ANALYZE, VERBOSE) nmsmirrorpageinfo;
REINDEX TABLE nmsmirrorpageinfo;
```

>[!NOTE]
>
>* Adobeでは、次の小さなテーブルから始めることをお勧めします。この方法では、大きなテーブル（障害のリスクが最も高いテーブル）でプロセスが失敗した場合、メンテナンスの少なくとも一部が完了しています。
>* Adobeでは、重要な更新がおこなわれる可能性のある、データモデルに固有のテーブルを追加することをお勧めします。 これは、毎日のデータレプリケーションフローが大きい場合、 **NmsRecipient** に該当します。
>* VACUUM 文と REINDEX 文はテーブルをロックし、メンテナンスの実行中に一部のプロセスを一時停止します。
>* 非常に大きなテーブル（通常は 5 Gb を超えるテーブル）の場合、VACUUM FULL 文は非常に非効率になり、非常に長い時間がかかる場合があります。 Adobeは、 **YyyNmsBroadLogXxx** テーブルには使用しないことをお勧めします。
>* このメンテナンス操作は、Adobe Campaignワークフローで、**[!UICONTROL SQL]** アクティビティを使用して実装できます。 詳しくは、[この節](../../workflow/using/architecture.md)を参照してください。バックアップウィンドウと衝突しない低アクティビティ時間でメンテナンスをスケジュールしてください。

>


### データベースの再構築 {#rebuilding-a-database}

PostgreSQL は、VACUUM FULL 文がテーブルをロックし、通常の生産を防ぐので、オンラインテーブルの再構築を簡単に実行する方法を提供しません。 つまり、テーブルを使用しない場合はメンテナンスを実行する必要があります。 次のいずれかが可能です。

* Adobe Campaignプラットフォームが停止した場合は、メンテナンスを実行します。
* 再構築中のテーブルに書き込む可能性が高い様々なAdobe Campaignサブサービスを停止します（**nlserver stop wfserver instance_name** は、ワークフロープロセスを停止します）。

必要な DDL を生成する特定の関数を使用した表の最適化の例を次に示します。 次の SQL では、2 つの新しい関数を作成できます。**GenRebuildTablePart1** と **GenRebuildTablePart2**。これは、テーブルを再作成するために必要な DDL を生成するのに使用できます。

* 1 つ目の関数は、元のテーブルのコピーである作業用テーブル (** _tmp**ここでは ) を作成します。
* 次に、2 番目の関数は元のテーブルを削除し、作業用テーブルとそのインデックスの名前を変更します。
* 1 つではなく 2 つの関数を使用すると、最初の関数が失敗した場合、元のテーブルを削除するリスクは発生しません。

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

次の例は、**vacuum/rebuild** コマンドを使用する代わりに、ワークフローで必要なテーブルを再構築する場合に使用できます。

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

お使いのバージョンのデータベースに最も適した手順については、Oracle管理者にお問い合わせください。

## Microsoft SQL Server {#microsoft-sql-server}

>[!NOTE]
>
>Microsoft SQL Server の場合は、[ このページ ](https://ola.hallengren.com/sql-server-index-and-statistics-maintenance.html) で説明されているメンテナンス計画を使用できます。

次の例は、Microsoft SQL Server 2005 に関するものです。 別のバージョンを使用している場合は、データベース管理者に問い合わせて、メンテナンス手順を確認してください。

1. まず、管理者権限を持つログインを使用して、Microsoft SQL Server Management Studio に接続します。
1. **[!UICONTROL 管理/メンテナンスプラン]** フォルダーに移動し、右クリックして「**[!UICONTROL メンテナンスプランウィザード]**」を選択します。
1. 最初のページが表示されたら、「**[!UICONTROL 次へ]**」をクリックします。
1. 作成するメンテナンスプランのタイプ（タスクごとに個別のスケジュールを選択するか、プラン全体で 1 つのスケジュールを選択する）を選択し、「**[!UICONTROL 変更…」をクリックします。]** ボタン。
1. **[!UICONTROL ジョブスケジュールのプロパティ]** ウィンドウで、目的の実行設定を選択し、「**[!UICONTROL OK]**」をクリックしてから、「**[!UICONTROL 次へ]**」をクリックします。
1. 実行するメンテナンスタスクを選択し、[**[!UICONTROL 次へ]**] をクリックします。

   >[!NOTE]
   >
   >少なくとも以下に示すメンテナンスタスクを実行することをお勧めします。 統計の更新タスクは、データベースクリーンアップワークフローによって既に実行されている場合でも、選択することができます。

1. ドロップダウンリストで、**[!UICONTROL Database Check Integrity]** タスクを実行するデータベースを選択します。
1. データベースを選択し、「**[!UICONTROL OK]**」をクリックし、「**[!UICONTROL 次へ]**」をクリックします。
1. データベースに割り当てる最大サイズを設定し、「**[!UICONTROL 次へ]**」をクリックします。

   >[!NOTE]
   >
   >データベースのサイズがこのしきい値を超える場合、メンテナンス計画では、空き容量を増やすために、未使用のデータを削除しようとします。

1. インデックスを再構成または再構築します。

   * インデックスの断片化率が 10%～40%の場合は、再編成をお勧めします。

      再編成するデータベースとオブジェクト（テーブルまたはビュー）を選択し、[**[!UICONTROL 次へ]**] をクリックします。

      >[!NOTE]
      >
      >設定に応じて、以前に選択したテーブルまたはデータベース内のすべてのテーブルを選択できます。

   * インデックスの断片化率が 40%を超える場合は、再構築をお勧めします。

      インデックス再構築タスクに適用するオプションを選択し、[**[!UICONTROL 次へ]**] をクリックします。

      >[!NOTE]
      >
      >リビルドインデックスプロセスは、プロセッサの使用に関してより狭く、データベースリソースをロックします。 再構築中にインデックスを使用できるようにするには、「**[!UICONTROL インデックスを再インデックス中にオンラインに維持]**」オプションを選択します。

1. アクティビティレポートに表示するオプションを選択し、「**[!UICONTROL 次へ]**」をクリックします。
1. メンテナンスプラン用に設定されたタスクの一覧を確認し、[**[!UICONTROL 終了]**] をクリックします。

   メンテナンス計画の概要と、その様々なステップのステータスが表示されます。

1. メンテナンス計画が完了したら、[**[!UICONTROL 閉じる]**] をクリックします。
1. Microsoft SQL Server エクスプローラーで、**[!UICONTROL 管理/メンテナンスプラン]** フォルダーをダブルクリックします。
1. Adobe Campaignメンテナンスプランの選択：様々な手順について詳しくは、ワークフローを参照してください。

   **[!UICONTROL SQL Server エージェント/ジョブ]** フォルダーにオブジェクトが作成されていることに注意してください。 このオブジェクトを使用して、メンテナンス計画を開始できます。 この例では、すべてのメンテナンスタスクが同じプランの一部なので、オブジェクトは 1 つだけです。

   >[!IMPORTANT]
   >
   >このオブジェクトを実行するには、Microsoft SQL Server エージェントを有効にする必要があります。

**作業用テーブル用の別のデータベースの設定**

>[!NOTE]
>
>この設定はオプションです。

「**WdbcOptions_TempDbName**」オプションを使用すると、Microsoft SQL Server 上で、作業用テーブル向けに別のデータベースを構成できます。これにより、バックアップとレプリケーションを最適化できます。

このオプションは、作業用テーブル（ワークフローの実行中に作成されたテーブルなど）を別のデータベースで作成する場合に使用できます。

このオプションを「tempdb.dbo」に設定すると、作業用テーブルがMicrosoft SQL Server のデフォルトの一時データベースに作成されます。 データベース管理者は、tempdb データベースへの書き込みアクセスを許可する必要があります。

このオプションを設定すると、Adobe Campaignで設定されているすべてのMicrosoft SQL Server データベース（メインデータベースおよび外部アカウント）でこのオプションが使用されます。 2 つの外部アカウントが同じサーバーを共有している場合は、（tempdb が一意であるので）競合が発生する可能性があります。 同様に、2 つの Campaign インスタンスが同じ MSSQL サーバーを使用する場合、同じ tempdb を使用すると競合が発生する可能性があります。
