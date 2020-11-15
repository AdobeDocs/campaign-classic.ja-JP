---
title: 外部データベースへのアクセス権
description: 外部データベースのアクセス権限
page-status-flag: never-activated
uuid: b84359b9-c584-431d-80d5-71146d9b6854
contentOwner: sauviat
products: SG_CAMPAIGN/CLASSIC
audience: platform
content-type: reference
topic-tags: connectors
discoiquuid: dd3d14cc-5153-428d-a98a-32b46f0fe811
translation-type: tm+mt
source-git-commit: 9bbde65aea6735e30e95e75c2b6ae5445d4a2bdd
workflow-type: tm+mt
source-wordcount: '1029'
ht-degree: 99%

---


# リモートデータベースのアクセス権 {#remote-database-access-rights}

まず、ユーザーが FDA で外部データベースの操作を実行できるように、Adobe Campaign で特定のネームド権限を設定する必要があります。

1. Adobe Campaign エクスプローラーで、**[!UICONTROL 管理／アクセス管理／ネームド権限]**&#x200B;ノードを選択します。
1. 任意のラベルを指定して新しい権限を作成します。
1. 「**[!UICONTROL 名前]**」フィールドを指定します。**user:base@server** の形式で指定する必要があります。

   * **user** は、外部データベースのユーザーの名前に対応します。
   * **base** は、外部データベースの名前に対応します。
   * **server** は、外部データベースサーバーの名前に対応します。

      >[!NOTE]
      >
      >**:base** の部分は、Oracle では省略可能です。

1. ネームド権限を保存し、Adobe Campaign エクスプローラーの&#x200B;**[!UICONTROL 管理／アクセス管理／オペレーター]**&#x200B;ノードで目的のユーザーにリンクします。

次に、外部データベースに格納されているデータを処理できるように、Adobe Campaign ユーザーに少なくともデータベースに対する「書き込み」権限を付与して、作業用テーブルの作成を許可する必要があります。作業用テーブルは Adobe Campaign で自動的に削除されます。

一般に必要となる権限には次のものがあります。

* **CONNECT**：リモートデータベースへの接続
* **READ Data**：顧客データが格納されたテーブルへの読み取り専用アクセス
* **READ &#39;MetaData&#39;**：テーブル構造を取得するためのサーバーデータカタログへのアクセス
* **LOAD**：作業用テーブルへの一括読み込み（収集や結合の作業で必要）
* **TABLE/INDEX/PROCEDURE/FUNCTION** に対する **CREATE/DROP**（Adobe Campaign によって生成されるワークテーブルの場合のみ）
* **EXPLAIN**（推奨）：問題が発生した場合にパフォーマンスの監視に使用
* **WRITE Data**（統合シナリオに応じて）

データベース管理者は、これらの権限を各データベースエンジン特有の権限に対応付ける必要があります。詳しくは、以下の節を参照してください。

## FDA 権限 {#fda-rights}

|   | Snowflake | Redshift | Oracle | SQLServer | PostgreSQL | MySQL |
|:-:|:-:|:-:|:-:|:-:|:-:|:-:|
| **リモートデータベースへの接続** | ウェアハウスでの使用、データベースでの使用、スキーマ特権での使用 | AWS アカウントにリンクされたユーザーの作成 | CREATE SESSION 権限 | CONNECT 権限 | CONNECT 権限 | ALL PRIVILEGES を持つリモートホストに関連付けられたユーザーの作成 |
| **テーブルの作成** | CREATE TABLE ON SCHEMA 権限 | CREATE 権限 | CREATE TABLE 権限 | CREATE TABLE 権限 | CREATE 権限 | CREATE 権限 |
| **インデックスの作成** | 該当なし | CREATE 権限 | INDEX または CREATE ANY INDEX 権限 | ALTER 権限 | CREATE 権限 | INDEX 特権 |
| **関数の作成** | CREATE FUNCTION ON SCHEMA 権限 | 外部の Python スクリプトを呼び出せる USAGE ON LANGUAGE plpythonu 権限 | CREATE PROCEDURE または CREATE ANY PROCEDURE 権限 | CREATE FUNCTION 権限 | USAGE 権限 | CREATE ROUTINE 権限 |
| **プロシージャの作成** | 該当なし | 外部の Python スクリプトを呼び出せる USAGE ON LANGUAGE plpythonu 権限 | CREATE PROCEDURE または CREATE ANY PROCEDURE 権限 | CREATE PROCEDURE 権限 | USAGE 権限（プロシージャは関数） | CREATE ROUTINE 権限 |
| **オブジェクト（テーブル、インデックス、関数、プロシージャ）の削除** | オブジェクトの所有者 | オブジェクトの所有者またはスーパーユーザー | DROP ANY &lt; object > 権限 | ALTER 権限 | テーブル：テーブルの所有者。インデックス：インデックスの所有者。関数：関数の所有者。 | DROP 権限 |
| **実行の監視** | 必要なオブジェクトに対する MONITOR 権限 | EXPLAIN コマンドの使用に権限は不要 | EXPLAIN PLAN の基となる文を実行するための INSERT 権限、SELECT 権限および必要な権限 | SHOWPLAN 権限 | EXPLAIN 文の使用に権限は不要 | SELECT 権限 |
| **データの書き込み** | INSERT / UPDATE 権限（書き込み操作に応じて異なる） | INSERT および UPDATE 権限 | INSERT および UPDATE 権限または INSERT および UPDATE ANY TABLE 権限 | INSERT および UPDATE パーミッション | INSERT および UPDATE 権限 | INSERT および UPDATE 権限 |
| **テーブルへのデータの読み込み** | CREATE STAGE ON SCHEMA およびターゲットテーブルでの SELECT および INSERT 権限 | SELECT および INSERT 権限 | SELECT および INSERT 権限 | INSERT、ADMINISTER BULK OPERATIONS および ALTER TABLE 権限 | SELECT および INSERT 権限 | FILE 権限 |
| **クライアントデータへのアクセス** | SELECT on (FUTURE) TABLE または VIEW 権限 | SELECT 権限 | SELECT または SELECT ANY TABLE 権限 | SELECT パーミッション | SELECT 権限 | SELECT 権限 |
| **メタデータへのアクセス** | SELECT on INFORMATION_SCHEMA SCHEMA 権限 | SELECT 権限 | DESCRIBE 文の使用に権限は不要 | VIEW DEFINITION 権限 | 「\d table」コマンドの使用に権限は不要 | SELECT 権限 |

|   | DB2 UDB | TeraData | InfiniDB | Sybase IQ / Sybase ASE | Netezza | Greenplum | AsterData |
|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|
| **リモートデータベースへの接続** | CONNECT 権限 | CONNECT 権限 | ALL PRIVILEGES を持つリモートホストに関連付けられたユーザーの作成 | CONNECT 文の使用にパーミッションは不要 | 権限は不要 | CONNECT 権限 | CONNECT 権限 |
| **テーブルの作成** | CREATETAB 権限 | CREATE TABLE または TABLE キーワード | CREATE 権限 | RESOURCE 権限と CREATE パーミッション | TABLE 権限 | CREATE 権限 | CREATE 権限 |
| **インデックスの作成** | INDEX 特権 | CREATE INDEX または INDEX キーワード | INDEX 特権 | RESOURCE 権限と CREATE パーミッション | INDEX 特権 | CREATE 権限 | CREATE 権限 |
| **関数の作成** | IMPLICIT_SCHEMA 権限または CREATEIN 特権 | CREATE FUNCTION または FUNCTION キーワード | CREATE ROUTINE 権限 | RESOURCE 権限または Java 関数への DBA 権限 | FUNCTION 権限 | USAGE 権限 | CREATE FUNCTION 権限 |
| **プロシージャの作成** | IMPLICIT_SCHEMA 権限または CREATEIN 特権 | CREATE PROCEDURE または PROCEDURE キーワード | CREATE ROUTINE 権限 | RESOURCE 権限 | PROCEDURE 権限 | USAGE 権限 | CREATE FUNCTION 権限 |
| **オブジェクト（テーブル、インデックス、関数、プロシージャ）の削除** | DROPIN 特権、CONTROL 特権またはオブジェクトの所有者 | DROP &lt; object >またはオブジェクト関連のキーワード | DROP 権限 | オブジェクトの所有者または DBA 権限 | DROP 権限 | オブジェクトの所有者 | オブジェクトの所有者 |
| **実行の監視** | EXPLAIN 権限 | EXPLAIN 文の使用に権限は不要 | SELECT 権限 | sp_showplan を実行できるのはシステム管理者のみ | EXPLAIN 文の使用に権限は不要 | EXPLAIN 文の使用に権限は不要 | EXPLAIN 文の使用に権限は不要 |
| **データの書き込み** | INSERT および UPDATE 特権または DATAACCESS 権限 | INSERT および UPDATE 権限 | INSERT および UPDATE 権限 | INSERT および UPDATE パーミッション | INSERT および UPDATE 権限 | INSERT および UPDATE 権限 | INSERT および UPDATE 権限 |
| **テーブルへのデータの読み込み** | LOAD 権限 | COPY TO 文と COPY FROM 文をそれぞれ使用するには SELECT 権限と INSERT 権限 | FILE 権限 | テーブルの所有者または ALTER パーミッション。-gl オプションによっては、LOAD TABLE は、ユーザーが DBA 権限を持っている場合にのみ実行されます | SELECT および INSERT 権限 | SELECT および INSERT 権限 | SELECT および INSERT 権限 |
| **クライアントデータへのアクセス** | INSERT/UPDATE 特権または DATAACCESS 権限 | SELECT 権限 | SELECT 権限 | SELECT パーミッション | SELECT 権限 | SELECT 権限 | SELECT 権限 |
| **メタデータへのアクセス** | DESCRIBE 文の使用に認証は不要 | SHOW 権限 | SELECT 権限 | DESCRIBE 文の使用にパーミッションは不要 | 「\d table」コマンドの使用に権限は不要 | 「\d table」コマンドの使用に権限は不要 | SHOW コマンドの使用に権限は不要 |