---
title: RDBMS に関する推奨事項
seo-title: RDBMS に関する推奨事項
description: RDBMS に関する推奨事項
seo-description: null
page-status-flag: never-activated
uuid: 637c1b5a-0484-4734-a012-eb4ba8036263
contentOwner: sauviat
products: SG_CAMPAIGN/CLASSIC
audience: production
content-type: reference
topic-tags: database-maintenance
discoiquuid: b2219912-5570-45d2-8b52-52486e29d008
translation-type: tm+mt
source-git-commit: 70b143445b2e77128b9404e35d96b39694d55335
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---


# RDBMS に関する推奨事項{#rdbms-specific-recommendations}

メンテナンス計画の設定に役立つように、この節では、Adobe Campaignがサポートする様々なRDBMSエンジンに適合した推奨事項/ベストプラクティスをリストします。 ただし、これらは単なる推奨事項です。 内部の手順や制約に合わせて、ニーズに合わせて変更を行うのは、お客様次第です。 データベース管理者は、これらのプランを作成して実行する能力を持っています。

## PostgreSQL {#postgresql}

### 大きいテーブルの検出 {#detecting-large-tables}

1. データベースに次の表示を追加できます。

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

1. 次のコマンドを実行すると、大きなテーブルとインデックスを指定できます。

   ```
   select * from uvSpace;
   ```

### 簡単なメンテナンス {#simple-maintenance}

PostgreSQLでは、 **真空フル** 、 **再インデックスの一般的なコマンドが使用できます**。

次の2つのコマンドを使用して、定期的に実行するSQL保守計画の典型的な例を示します。

```
vacuum full nmsdelivery;
 reindex table nmsdelivery;
 
 vacuum full nmsdeliverystat;
 reindex table nmsdeliverystat;
 
 vacuum full xtkworkflow;
 reindex table xtkworkflow;
 
 vacuum full xtkworkflowevent;
 reindex table xtkworkflowevent;
 
 vacuum full xtkworkflowjob;
 reindex table xtkworkflowjob;
 
 vacuum full xtkworkflowlog;
 reindex table xtkworkflowlog;
 
 vacuum full xtkworkflowtask;
 reindex table xtkworkflowtask;
 
 vacuum full xtkjoblog;
 reindex table xtkjoblog;
 
 vacuum full xtkjob;
 reindex table xtkjob;
 
 vacuum full nmsaddress;
 reindex table nmsaddress;

 vacuum full nmsdeliverypart;
 reindex table nmsdeliverypart;
 
 vacuum full nmsmirrorpageinfo;
 reindex table nmsmirrorpageinfo;
```

>[!NOTE]
>
>* Adobeでは、最初に小さなテーブルを使用することをお勧めします。大きなテーブル（失敗のリスクが最も高いテーブル）でプロセスが失敗した場合、メンテナンスの少なくとも一部が完了しています。
>* Adobeは、重要な更新を受ける可能性のある、データモデル固有のテーブルを追加するコマンドを再実行します。 これは、 **NmsRecipient** （日別データレプリケーションフローが大きい場合）に発生する可能性があります。
>* vacuum **コマンドと** re-index **** コマンドはテーブルをロックし、メンテナンスの実行中に一部のプロセスを一時停止します。
>* 非常に大きなテーブル（通常5 Gbを超える）の場合、 **真空が完全になると非効率になり** 、非常に長い時間がかかります。 Adobeでは、YyyNmsBroadLogXxx **テーブルに対して使用することはお勧めしません** 。
>* このメンテナンス操作は、 **[!UICONTROL SQL]** アクティビティを使用してAdobe Campaignワークフローによって実装できます(詳しくは、 [この節を参照](../../workflow/using/architecture.md))。 バックアップウィンドウに衝突しないアクティビティが低い時間にメンテナンスをスケジュールしてください。

>



### データベースの再構築 {#rebuilding-a-database}

PostgreSQLは、 **真空フルロックによりテーブルをロックするので、オンラインテーブルの再構築を容易に実行する方法を提供しません** 。したがって、通常の実稼働を防ぐことができます。 つまり、テーブルを使用しない場合はメンテナンスを行う必要があります。 次のいずれかが可能です。

* adobe campaignプラットフォームが停止した場合にメンテナンスを実行し、
* 再構築中のテーブルに書き込みが行われる可能性の高い様々なAdobe Campaignサブサービスを停止します(**nlserver stop wfserver instance_name** )。ワークフロープロセスを停止します。

必要なDDLを生成するための特定の関数を使用した表の最適化の例を次に示します。 次のSQLでは、2つの新しい関数を作成できます。 **GenRebuildTablePart1** とGenRebuildTablePart2 ****。これは、テーブルを再作成するために必要なDDLを生成するのに使用できます。

* 最初の関数では、元のテーブルのコピーである作業テーブル（ここでは** _tmp**）を作成できます。
* 次に、2番目の関数は、元のテーブルを削除し、作業テーブルとそのインデックスの名前を変更します。
* 1つではなく2つの関数を使用すると、最初の関数が失敗した場合に、元のテーブルを削除するリスクがなくなります。

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

次の例は、 **vacuum/rebuild** コマンドを使用する代わりに、ワークフローで使用して必要なテーブルを再構築する場合に使用できます。

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

お使いのOracleバージョンに最も適した手順については、データベース管理者にお問い合わせください。

## Microsoft SQL Server {#microsoft-sql-server}

>[!NOTE]
>
>Microsoft SQL Serverの場合は、このページで詳しく説明している保守プラン [を使用できます](https://ola.hallengren.com/sql-server-index-and-statistics-maintenance.html)。

次の例は、Microsoft SQL Server 2005に関するものです。 別のバージョンを使用している場合は、データベース管理者に問い合わせて、メンテナンス手順を確認してください。

1. まず、Microsoft SQL Server Management Studioに接続し、管理者権限でログインします。
1. [ **[!UICONTROL 管理] > [メンテナンスプラン]** ]フォルダに移動し、右クリックして[ **[!UICONTROL メンテナンスプランウィザード]を選択します]**
1. 最初のページが表示されたら **[!UICONTROL 「次へ]** 」をクリックします。
1. 作成する保守計画のタイプ(タスクごとに別々のスケジュールを作成するか、計画全体で1つのスケジュールを作成する)を選択し、「 **[!UICONTROL 変更…]** 」ボタンをクリックします。
1. 「 **[!UICONTROL ジョブ・スケジュール・プロパティ]** 」ウィンドウで、目的の実行設定を選択し、「 **[!UICONTROL OK]** 」をクリックし、「 **[!UICONTROL 次へ」をクリックします]** 。
1. 実行するメンテナンスタスクを選択し、「 **[!UICONTROL 次へ]** 」をクリックします。

   >[!NOTE]
   >
   >以下に示すメンテナンスタスクを少なくとも実行することをお勧めします。 また、統計の更新タスクを選択することもできます。ただし、このオプションは、データベースのクリーンアップワークフローで既に実行されています。

1. ドロップダウンリストで、「 **[!UICONTROL Database Check Integrity]** 」タスクを実行するデータベースを選択します。
1. データベースを選択し、「 **[!UICONTROL OK]** 」をクリックし、「 **[!UICONTROL 次へ]** 」をクリックします。
1. データベースに割り当てる最大サイズを設定し、「 **[!UICONTROL 次へ]** 」をクリックします。

   >[!NOTE]
   >
   >データベースのサイズがこのしきい値を超える場合、メンテナンス計画では、未使用のデータを削除して領域を解放しようとします。

1. インデックスを再構成または再構築する：

   * インデックスの断片化率が10%～40%の場合は、再編成が推奨されます。

      再構成するデータベースとオブジェクト(テーブルまたは表示)を選択し、 **[!UICONTROL 「次へ]** 」をクリックします。

      >[!NOTE]
      >
      >設定に応じて、以前に選択したテーブルか、データベース内のすべてのテーブルのどちらかを選択できます。

   * インデックスの断片化率が40%を超える場合は、再構築を推奨します。

      インデックスの再構築タスクに適用するオプションを選択し、 **[!UICONTROL 「次へ]** 」をクリックします。

      >[!NOTE]
      >
      >再構築インデックス・プロセスは、プロセッサの使用に関してはより制約が高く、データベース・リソースをロックします。 再構築時にインデックスを使用可能にする場合は、 **[!UICONTROL [インデックスをオンラインにして再インデックスを作成]** ]オプションをオンにします。

1. アクティビティレポートに表示するオプションを選択し、「 **[!UICONTROL 次へ]** 」をクリックします。
1. メンテナンス計画に設定されているタスクのリストを確認し、 **[!UICONTROL 「Finish]** 」をクリックします。

   メンテナンス計画の概要と、各ステップのステータスが表示されます。

1. メンテナンス計画が完了したら、「 **[!UICONTROL 閉じる]** 」をクリックします。
1. Microsoft SQL Serverエクスプローラで、 **[!UICONTROL Management（管理）/Maintenance Plans(メンテナンスプラン]** )フォルダを重複クリックします。
1. Adobe Campaign保守計画を選択します。ワークフローでは、様々な手順について詳しく説明します。

   オブジェクトは、 **[!UICONTROL SQL Server Agent/Jobs]** フォルダーに作成されています。 このオブジェクトを使用すると、保守計画を開始できます。 この例では、すべてのメンテナンスタスクが同じプランの一部であるため、オブジェクトは1つだけです。

   >[!CAUTION]
   >
   >このオブジェクトを実行するには、Microsoft SQL Serverエージェントを有効にする必要があります。

**作業テーブル用の別のデータベースの設定**

>[!NOTE]
>
>この設定はオプションです。

「**WdbcOptions_TempDbName**」オプションを使用すると、Microsoft SQL Server 上で、作業用テーブル向けに別のデータベースを構成できます。これにより、バックアップとレプリケーションを最適化できます。

このオプションは、作業テーブル（ワークフローの実行中に作成されたテーブルなど）を別のデータベースに作成する場合に使用できます。

このオプションを「tempdb.dbo.」に設定すると、Microsoft SQL Serverのデフォルトの一時データベースに作業テーブルが作成されます。 データベース管理者は、tempdbデータベースへの書き込みアクセスを許可する必要があります。

このオプションが設定されている場合、Adobe Campaign(メインデータベースおよび外部アカウント)で構成されているすべてのMicrosoft SQL Serverデータベースでこのオプションが使用されます。 2つの外部アカウントが同じサーバを共有している場合は、（tempdbが一意になるので）競合が発生する可能性があることに注意してください。 同様に、2つのキャンペーンインスタンスが同じMSSQLサーバーを使用する場合、同じtempdbを使用すると競合が発生する可能性があります。
