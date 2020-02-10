---
title: RDBMS固有の推奨事項
seo-title: RDBMS固有の推奨事項
description: RDBMS固有の推奨事項
seo-description: null
page-status-flag: never-activated
uuid: 637c1b5a-0484-4734-a012-eb4ba8036263
contentOwner: sauviat
products: SG_CAMPAIGN/CLASSIC
audience: production
content-type: reference
topic-tags: database-maintenance
discoiquuid: b2219912-5570-45d2-8b52-52486e29d008
index: y
internal: n
snippet: y
translation-type: tm+mt
source-git-commit: 9662e88578747a519df2e68e5a7d7987cc3ffdd4

---


# RDBMS固有の推奨事項{#rdbms-specific-recommendations}

メンテナンスプランの設定に役立つように、この節では、Adobe Campaignがサポートする様々なRDBMSエンジンに適した推奨事項とベストプラクティスを示します。 ただし、これらは単なる推奨事項です。 内部の手順や制約に従って、ニーズに合わせて適応するのは、お客様次第です。 データベース管理者は、これらのプランを作成して実行する権限を持っています。

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

1. 次のコマンドを実行すると、大きなテーブルとインデックスを検出できます。

   ```
   select * from uvSpace;
   ```

### 簡単なメンテナンス {#simple-maintenance}

PostgreSQLでは、使用できる一般的なコマンドは真空フル **と再インデックス****です**。

次の2つのコマンドを使用して、定期的に実行するSQLメンテナンス計画の典型的な例を示します。

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
>* 小さい表から始めることをお勧めします。大きなテーブル（障害のリスクが最も高いテーブル）でプロセスが失敗した場合、メンテナンスの少なくとも一部が完了しています。
>* アドビは、重要な更新を受ける可能性のある、データモデルに固有のテーブルを追加するコマンドを再実行します。 日別データレプリケーションフローが **大きい場合** 、NmsRecipientに該当する可能性があります。
>* vacuumコマ **ンドと** re-indexコマンドは **** 、テーブルをロックし、メンテナンス中に一部のプロセスを一時停止します。
>* 非常に大きなテーブル（通常5 gbを超える）の場合、真空 **容量が非常に** 非効率になり、非常に長い時間がかかります。 YyyNmsBroadLogXxxテーブルには使用しないことをお勧 **めします** 。
>* このメンテナンス操作は、アクティビティを使用してAdobe Campaignワークフ **[!UICONTROL SQL]** ローで実装できます(詳しくは、この節を [参照](../../workflow/using/executing-a-workflow.md#architecture))。 バックアップウィンドウに衝突しない低アクティビティ時間のメンテナンスをスケジュールしてください。
>



### データベースの再構築 {#rebuilding-a-database}

PostgreSQLは、真空でテーブルをフルロックし、通常の生産を防ぐので、オンラインでのテーブル **の再構築を** 、簡単に実行する方法を提供しません。 つまり、テーブルを使用しない場合はメンテナンスを実行する必要があります。 次のいずれかが可能です。

* adobe Campaignプラットフォームが停止した場合にメンテナンスを実行し、
* 再構築中のテーブルに書き込みが行われる可能性の高い様々なAdobe Campaignサブサービスを停止します(**nlserver stop wfserver instance_name** 、ワークフロープロセスを停止します)。

必要なDDLを生成するための特定の関数を使用した表の最適化の例を次に示します。 次のSQLでは、2つの新しい関数を作成できます。GenRebuildTablePart1 **と** GenRebuildTablePart2 ****。これは、テーブルを再作成するために必要なDDLを生成するために使用できます。

* 最初の関数を使用すると、元のテーブルのコピーである作業テーブル（ここでは** _tmp**）を作成できます。
* 次に、2番目の関数は元のテーブルを削除し、作業テーブルとそのインデックスの名前を変更します。
* 1つの関数の代わりに2つの関数を使用すると、最初の関数が失敗しても、元のテーブルを削除するリスクがなくなります。

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

次の例は、vacuum/rebuildコマンドを使用する代わりに、必要なテーブルを再構築するワークフローで **使用できます** 。

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

お使いのバージョンのOracleに最も適した手順については、データベース管理者にお問い合わせください。

## Microsoft SQL Server {#microsoft-sql-server}

>[!NOTE]
>
>Microsoft SQL serverの場合は、このページで詳しく説明するメンテナンスプラン [を使用できます](http://ola.hallengren.com/sql-server-index-and-statistics-maintenance.html)。

以下の例は、Microsoft SQL Server 2005に関するものです。 別のバージョンを使用している場合は、データベース管理者に問い合わせて、メンテナンス手順を確認してください。

1. まず、管理者権限を持つログインでMicrosoft SQL Server Management studioに接続します。
1. フォルダーに移 **[!UICONTROL Management > Maintenance Plans]** 動し、フォルダーを右クリックして、「 **[!UICONTROL Maintenance Plan Wizard]**
1. 最初のペ **[!UICONTROL Next]** ージが表示されたらクリックします。
1. 作成するメンテナンスプランのタイプ（タスクごとに別々のスケジュール、またはプラン全体に対して1つのスケジュール）を選択し、ボタンをクリック **[!UICONTROL Change...]** します。
1. ウィンドウ **[!UICONTROL Job schedule properties]** で、目的の実行設定を選択し、をクリックし **[!UICONTROL OK]** て、をクリックしま **[!UICONTROL Next]** す。
1. 実行するメンテナンスタスクを選択し、をクリックしま **[!UICONTROL Next]** す。

   >[!NOTE]
   >
   >以下に示すメンテナンス作業を少なくとも実行することをお勧めします。 また、統計の更新タスクを選択することもできますが、データベースのクリーンアップワークフローによって既に実行されています。

1. ドロップダウンリストで、タスクを実行するデータベースを選択 **[!UICONTROL Database Check Integrity]** します。
1. データベースを選択し、をクリック **[!UICONTROL OK]** して、をクリックしま **[!UICONTROL Next]** す。
1. データベースに割り当てる最大サイズを設定し、をクリックしま **[!UICONTROL Next]** す。

   >[!NOTE]
   >
   >データベースのサイズがこのしきい値を超える場合、メンテナンスプランでは未使用のデータを削除して領域を解放しようとします。

1. インデックスを再構成または再構築します。

   * インデックスの断片化率が10%から40%の場合は、再編成が推奨されます。

      再編成するデータベースとオブジェクト（テーブルまたはビュー）を選択し、をクリックしま **[!UICONTROL Next]** す。

      >[!NOTE]
      >
      >設定に応じて、以前に選択したテーブルまたはデータベース内のすべてのテーブルを選択できます。

   * インデックスの断片化率が40%を超える場合は、再構築を推奨します。

      インデックスの再構築タスクに適用するオプションを選択し、をクリックしま **[!UICONTROL Next]** す。

      >[!NOTE]
      >
      >再構築インデックス・プロセスは、プロセッサの使用に関してはより制約が高く、データベース・リソースをロックします。 再構築時に **[!UICONTROL Keep index online while reindexing]** インデックスを使用できるようにする場合は、このオプションをオンにします。

1. アクティビティレポートに表示するオプションを選択し、をクリックしま **[!UICONTROL Next]** す。
1. メンテナンスプランに設定されたタスクのリストを確認し、をクリックしま **[!UICONTROL Finish]** す。

   メンテナンスプランの概要と、その様々な手順のステータスが表示されます。

1. メンテナンスプランが完了したら、をクリックしま **[!UICONTROL Close]** す。
1. Microsoft SQL serverエクスプローラーで、フォルダーをダブルクリック **[!UICONTROL Management > Maintenance Plans]** します。
1. Adobe Campaignメンテナンスプランを選択します。様々な手順について、ワークフローで詳しく説明します。

   フォルダー内にオブジェクトが作成されていることに注意して **[!UICONTROL SQL Server Agent > Jobs]** ください。 このオブジェクトを使用すると、メンテナンスプランを開始できます。 この例では、すべてのメンテナンスタスクが同じ計画の一部なので、オブジェクトは1つだけです。

   >[!CAUTION]
   >
   >このオブジェクトを実行するには、Microsoft SQL serverエージェントを有効にする必要があります。

**作業テーブル用の別のデータベースの設定**

>[!NOTE]
>
>この設定はオプションです。

WdbcOptions_ **TempDbName** オプションを使用すると、Microsoft SQL server上でテーブルを作業するための別のデータベースを構成できます。 これにより、バックアップとレプリケーションが最適化されます。

このオプションは、作業テーブル（ワークフローの実行中に作成されたテーブルなど）を別のデータベースに作成する場合に使用できます。

このオプションを「tempdb.dbo.」に設定すると、Microsoft SQL serverのデフォルトの一時データベースに作業テーブルが作成されます。 データベース管理者は、tempdbデータベースへの書き込みアクセスを許可する必要があります。

このオプションが設定されている場合、Adobe Campaignで設定されるすべてのMicrosoft SQL Serverデータベース（メインデータベースおよび外部アカウント）でこのオプションが使用されます。 2つの外部アカウントが同じサーバを共有している場合は、競合が発生する可能性があります（tempdbは一意になります）。 同様に、2つのキャンペーンインスタンスが同じMSSQLサーバーを使用する場合、同じtempdbを使用すると競合が発生する可能性があります。
