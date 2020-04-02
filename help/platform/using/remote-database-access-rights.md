---
title: 外部データベースへのアクセス
seo-title: 外部データベースへのアクセス
description: 外部データベースへのアクセス
seo-description: null
page-status-flag: never-activated
uuid: b84359b9-c584-431d-80d5-71146d9b6854
contentOwner: sauviat
products: SG_CAMPAIGN/CLASSIC
audience: platform
content-type: reference
topic-tags: connectors
discoiquuid: dd3d14cc-5153-428d-a98a-32b46f0fe811
index: y
internal: n
snippet: y
translation-type: tm+mt
source-git-commit: 17eed4f4ead8ce4f424d4fb2681269e888229692

---


# リモートデータベースのアクセス権 {#remote-database-access-rights}

まず、ユーザーが FDA で外部データベースの操作を実行できるように、Adobe Campaign で特定のネームド権限を設定する必要があります。

1. Adobe Campaignエクスプ **[!UICONTROL Administration > Access Management > Named Rights]** ローラーでノードを選択します。
1. 任意のラベルを指定して新しい権限を作成します。
1. The **[!UICONTROL Name]** field must take the following format **user:base@server**, where :

   * **user** は、外部データベースのユーザーの名前に対応します。
   * **base** は、外部データベースの名前に対応します。
   * **server** は、外部データベースサーバーの名前に対応します。

      >[!NOTE]
      >
      >**:base** の部分は、Oracle では省略可能です。

1. Save the named right then link it to your chosen user from the **[!UICONTROL Administration > Access Management > Operators]** node of the Adobe Campaign explorer.

次に、外部データベースに格納されているデータを処理できるように、Adobe Campaign ユーザーに少なくともデータベースに対する「書き込み」権限を付与して、作業用テーブルの作成を許可する必要があります。作業用テーブルは Adobe Campaign で自動的に削除されます。

一般に必要となる権限には次のものがあります。

* **CONNECT**：リモートデータベースへの接続
* **READ Data**：顧客データが格納されたテーブルへの読み取り専用アクセス
* **READ &#39;MetaData&#39;**：テーブル構造を取得するためのサーバーデータカタログへのアクセス
* **LOAD**：作業用テーブルへの一括読み込み（収集や結合の作業で必要）
* **TABLE/INDEX/PROCEDURE/FUNCTION** の&#x200B;**CREATE/DROP**
* **EXPLAIN**（推奨）：問題が発生した場合にパフォーマンスの監視に使用
* **WRITE Data**（統合シナリオに応じて）

データベース管理者は、これらの権限を各データベースエンジン特有の権限に対応付ける必要があります。詳しくは、以下の節を参照してください。

## FDA権 {#fda-rights}

|   | Snowflake | Redshift | Oracle | SQLServer | PostgreSQL | MySQL |
|:-:|:-:|:-:|:-:|:-:|:-:|:-:|
| **リモート・データベースへの接続** | WAREHOUSEの使用およびデータベース権限の使用 | AWSアカウントにリンクされたユーザーの作成 | CREATE SESSION権限 | CONNECT権限 | CONNECT権限 | すべての権限を持つリモート・ホストに関連付けられたユーザーの作成 |
| **テーブルの作成** | CREATE TABLE ONスキーマ権限 | CREATE権限 | CREATE TABLE権限 | CREATE TABLE権限 | CREATE権限 | CREATE権限 |
| **インデックスの作成** | なし | CREATE権限 | INDEXまたはCREATE ANY INDEX権限 | ALTER権限 | CREATE権限 | INDEX権限 |
| **関数の作成** | CREATE FUNCTION ONスキーマ権限 | USAGE ON LANGUAGE plpythonu権限で外部のPythonスクリプトを呼び出す | CREATE PROCEDUREまたはCREATE ANY PROCEDURE権限 | CREATE FUNCTION権限 | USAGE権限 | CREATE ROUTINE権限 |
| **手順の作成** | CREATE PROCEDURE ONスキーマ権限 | USAGE ON LANGUAGE plpythonu権限で外部のPythonスクリプトを呼び出す | CREATE PROCEDUREまたはCREATE ANY PROCEDURE権限 | CREATE PROCEDURE権限 | USAGE権限（プロシージャは関数） | CREATE ROUTINE権限 |
| **オブジェクト（テーブル、インデックス、関数、プロシージャ）の削除** | オブジェクトの所有 | オブジェクトの所有またはスーパーユーザ | DROP ANY &lt; object > privilege | ALTER権限 | 表：テーブルを所有しています。インデックス：インデックスを所有しています。関数：関数の所有 | DROP権限 |
| **実行の監視** | 必要なオブジェクトに対するMONITOR権限 | EXPLAINコマンドを使用する権限が不要 | EXPLAIN PLANが基づく文を実行するためのINSERTおよびSELECT権限と必要な権限 | SHOWPLAN権限 | EXPLAIN文を使用する権限が不要 | SELECT権限 |
| **データの書き込み** | INSERT/UPDATE権限（書き込み操作に応じて異なる） | INSERTおよびUPDATE権限 | INSERT AND UPDATEまたはINSERT AND UPDATE ANY TABLE権限 | INSERT and UPDATE permissions | INSERTおよびUPDATE権限 | INSERTおよびUPDATE権限 |
| **テーブルへのデータの読み込み** | CREATE STAGE ON SELECT ONスキーマ、SELECTおよびINSERT on theターゲット表権限 | 権限の選択と挿入 | 権限の選択と挿入 | バルク操作の挿入、管理、テーブルの変更の権限 | 権限の選択と挿入 | FILE権限 |
| **クライアントデータへのアクセス** | SELECT on (FUTURE) TABLE(S) OR表示(S) PRIVILEGE(s) PRIVILEGE(s) SELECT on (FUTURE) TABLE(S) OR特権 | SELECT権限 | SELECTまたはSELECT ANY TABLE権限 | 権限の選択 | SELECT権限 | SELECT権限 |
| **メタデータへのアクセス** | SELECT on INFORMATION_SELECTスキーマスキーマ権限 | SELECT権限 | DESCRIBE文を使用する権限は不要 | 表示定義権限 | 「\d table」コマンドを使用する権限が必要ではありません | SELECT権限 |

|   | DB2 UDB | TeraData | InfiniDB | Sybase IQ/Sybase ASE | Netezza | グリーンプラム | AsterData |
|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|
| **リモート・データベースへの接続** | CONNECT権限 | CONNECT権限 | すべての権限を持つリモート・ホストに関連付けられたユーザーの作成 | CONNECT文を使用する権限は不要 | 権限は不要 | CONNECT権限 | CONNECT権限 |
| **テーブルの作成** | CREATETAB権限 | 表または表のキーワードを作成 | CREATE権限 | RESOURCE AUTHORITYとCREATE権限 | TABLE権限 | CREATE権限 | CREATE権限 |
| **インデックスの作成** | INDEX権限 | 索引または索引キーワードの作成 | INDEX権限 | RESOURCE AUTHORITYとCREATE権限 | INDEX権限 | CREATE権限 | CREATE権限 |
| **関数の作成** | IMPLICIT_スキーマ権限またはCREATEIN権限 | CREATE FUNCTIONまたはFUNCTIONキーワード | CREATE ROUTINE権限 | Java関数のRESOURCE権限またはDBA権限 | FUNCTION権限 | USAGE権限 | CREATE FUNCTION権限 |
| **手順の作成** | IMPLICIT_スキーマ権限またはCREATEIN権限 | CREATE PROCEDUREまたはPROCEDUREキーワード | CREATE ROUTINE権限 | リソース権限 | PROCEDURE権限 | USAGE権限 | CREATE FUNCTION権限 |
| **オブジェクト（テーブル、インデックス、関数、プロシージャ）の削除** | DROPIN権限またはCONTROL権限、またはオブジェクトの所有 | DROP &lt; object >またはオブジェクト関連のキーワード | DROP権限 | オブジェクトの所有またはDBA権限 | DROP権限 | オブジェクトの所有 | オブジェクトの所有 |
| **実行の監視** | EXPLAIN権限 | EXPLAIN文を使用する権限が不要 | SELECT権限 | sp_showplanを実行できるのはシステム管理者のみです | EXPLAIN文を使用する権限が不要 | EXPLAIN文を使用する権限が不要 | EXPLAIN文を使用する権限が不要 |
| **データの書き込み** | INSERT and UPDATE権限またはDATAACCESS権限 | INSERTおよびUPDATE権限 | INSERTおよびUPDATE権限 | INSERT and UPDATE permissions | INSERTおよびUPDATE権限 | INSERTおよびUPDATE権限 | INSERTおよびUPDATE権限 |
| **テーブルへのデータの読み込み** | LOAD権限 | COPY TO文とCOPY FROM文をそれぞれ使用するSELECT権限とINSERT権限 | FILE権限 | テーブルの所有者またはALTERパーミッション。 -glオプションによっては、LOAD TABLEは、ユーザがDBA権限を持っている場合にのみ実行されます | 権限の選択と挿入 | 権限の選択と挿入 | 権限の選択と挿入 |
| **クライアントデータへのアクセス** | INSERT/UPDATE権限またはDATAACCESS権限 | SELECT権限 | SELECT権限 | 権限の選択 | SELECT権限 | SELECT権限 | SELECT権限 |
| **メタデータへのアクセス** | DESCRIBE文を使用するための認証は不要 | SHOW権限 | SELECT権限 | DESCRIBE文を使用する権限は不要 | 「\d table」コマンドを使用する権限が必要ではありません | 「\d table」コマンドを使用する権限が必要ではありません | SHOWコマンドを使用する権限が不要 |