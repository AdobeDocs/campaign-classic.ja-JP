---
product: campaign
title: 外部データベースにアクセスするための権限
description: 外部データベースアクセス権限
feature: Installation, Instance Settings, Federated Data Access
audience: platform
content-type: reference
topic-tags: connectors
exl-id: 3d43010e-53f8-4aa2-a651-c422a02191fe
TQID: https://experienceleague.adobe.com/J55-McblpyrkaTwKk7d09Yv6sXereUGgjep-k-wNdA4
product_v2: id: dfc56824-e8b9-499e-85d4-21aedb507314
feature_v2: id: c5474392-5419-4296-9e41-f6f4ce4f6e9b
subfeature_v2: id: e3988c18-3cfa-4f16-b812-ac2d2b1056faid: efa38731-2723-4334-8d8b-a778af834835
topic_v2: id: a004cc84-67b9-4a33-a3a7-8ec7273ef4dcid: eddd9b14-83bd-4ff4-9072-54a4a484abb7
source-git-commit: 4c295c0dabae8aba298390a3da2422a3fa1219f9
workflow-type: tm+mt
source-wordcount: 933
ht-degree: 96%

---

# リモートデータベースのアクセス権 {#remote-database-access-rights}



まず、ユーザーが FDA で外部データベースの操作を実行できるように、Adobe Campaign で特定のネームド権限を設定する必要があります。

1. Adobe Campaign エクスプローラーで、**[!UICONTROL 管理／アクセス管理／ネームド権限]**&#x200B;ノードを選択します。
1. 任意のラベルを指定して新しい権限を作成します。
1. **[!UICONTROL 名前]** フィールドは、次の形式&#x200B;**ユーザー:base@server**&#x200B;にする必要があります。ここで、

   * **user** は、外部データベースのユーザーの名前に対応します。
   * **base** は、外部データベースの名前に対応します。
   * **server** は、外部データベースサーバーの名前に対応します。

     >[!NOTE]
     >
     >**:base**&#x200B;部分はOracleではオプションです。

1. ネームド権限を保存し、Adobe Campaign エクスプローラーの&#x200B;**[!UICONTROL 管理／アクセス管理／オペレーター]**&#x200B;ノードで目的のユーザーにリンクします。

次に、外部データベースに格納されているデータを処理できるように、Adobe Campaign ユーザーに少なくともデータベースに対する「書き込み」権限を付与して、ワークテーブルの作成を許可する必要があります。 作業用テーブルは Adobe Campaign で自動的に削除されます。

一般に必要となる権限には次のものがあります。

* **CONNECT**：リモートデータベースへの接続
* **READ Data**：顧客データが格納されたテーブルへの読み取り専用アクセス
* **READ &#39;MetaData&#39;**：テーブル構造を取得するためのサーバーデータカタログへのアクセス
* **LOAD**：ワークテーブルへの一括読み込み（収集や結合の作業で必要）
* **TABLE/INDEX/PROCEDURE/FUNCTION** に対する **CREATE/DROP**（Adobe Campaign によって生成されるワークテーブルの場合のみ）
* **EXPLAIN**（推奨）：問題が発生した場合にパフォーマンスの監視に使用
* **WRITE Data**（統合シナリオに応じて）

データベース管理者は、これらの権限を各データベースエンジン特有の権限に対応付ける必要があります。 詳しくは、以下の節を参照してください。

## FDAの権利 {#fda-rights}

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

|   | TeraData | InfiniDB | Sybase IQ / Sybase ASE | Netezza | AsterData |
|:-:|:-:|:-:|:-:|:-:|:-:|
| **リモートデータベースへの接続** | CONNECT 権限 | ALL PRIVILEGES を持つリモートホストに関連付けられたユーザーの作成 | CONNECT 文の使用にパーミッションは不要 | 権限は不要 | CONNECT 権限 |
| **テーブルの作成** | CREATE TABLE または TABLE キーワード | CREATE 権限 | RESOURCE 権限と CREATE パーミッション | TABLE 権限 | CREATE 権限 |
| **インデックスの作成** | CREATE INDEX または INDEX キーワード | INDEX 特権 | RESOURCE 権限と CREATE パーミッション | INDEX 特権 | CREATE 権限 |
| **関数の作成** | CREATE FUNCTION または FUNCTION キーワード | CREATE ROUTINE 権限 | RESOURCE 権限または Java 関数への DBA 権限 | FUNCTION 権限 | CREATE FUNCTION 権限 |
| **プロシージャの作成** | CREATE PROCEDURE または PROCEDURE キーワード | CREATE ROUTINE 権限 | RESOURCE 権限 | PROCEDURE 権限 | CREATE FUNCTION 権限 |
| **オブジェクト（テーブル、インデックス、関数、プロシージャ）の削除** | DROP &lt; object >またはオブジェクト関連のキーワード | DROP 権限 | オブジェクトの所有者または DBA 権限 | DROP 権限 | オブジェクトの所有者 |
| **実行の監視** | EXPLAIN 文の使用に権限は不要 | SELECT 権限 | sp_showplan を実行できるのはシステム管理者のみ | EXPLAIN 文の使用に権限は不要 | EXPLAIN 文の使用に権限は不要 |
| **データの書き込み** | INSERT および UPDATE 権限 | INSERT および UPDATE 権限 | INSERT および UPDATE パーミッション | INSERT および UPDATE 権限 | INSERT および UPDATE 権限 |
| **テーブルへのデータの読み込み** | COPY TO 文と COPY FROM 文をそれぞれ使用するには SELECT 権限と INSERT 権限 | FILE 権限 | テーブルの所有者または ALTER パーミッション。 -gl オプションによっては、LOAD TABLE は、ユーザーが DBA 権限を持っている場合にのみ実行されます | SELECT および INSERT 権限 | SELECT および INSERT 権限 |
| **クライアントデータへのアクセス** | SELECT 権限 | SELECT パーミッション | SELECT 権限 | SELECT 権限 |  |
| **メタデータへのアクセス** | SHOW 権限 | SELECT 権限 | DESCRIBE 文の使用にパーミッションは不要 | 「\d table」コマンドの使用に権限は不要 | SHOW コマンドの使用に権限は不要 |
