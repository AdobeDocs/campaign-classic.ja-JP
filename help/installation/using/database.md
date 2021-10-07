---
product: campaign
title: Campaign Classicデータベースの推奨事項
description: データベースの推奨事項
audience: installation
content-type: reference
topic-tags: prerequisites-and-recommendations-
exl-id: 8a0426c1-9e8d-4053-bc2b-6a550e2eed2f
source-git-commit: 20509f44c5b8e0827a09f44dffdf2ec9d11652a1
workflow-type: tm+mt
source-wordcount: '277'
ht-degree: 2%

---

# データベース{#database}

![](../../assets/v7-only.svg)

データベース・サーバは、アプリケーション・サーバが使用するオペレーティング・システムに関係なく、任意のオペレーティング・システム上で実行できます。ただし、サーバ間にネットワーク接続がある場合は実行できます。

Adobe Campaignの様々なコンポーネントとの接続が可能である限り、データベースサーバーのオペレーティングシステムは重要ではありません。

[ データベースアクセス層 ](../../installation/using/prerequisites-of-campaign-installation-in-linux.md#database-access-layers) の節も確認してください。

## Microsoft SQL Server {#microsoft-sql-server}

ネイティブクライアントは、Adobe Campaignアプリケーションサーバーにインストールする必要があります。

**SQL Server Native Client 11.0** の下の ODBC ドライバー設定パネルで、サーバー上のネイティブクライアントを確認できます。

次のアクセス DLL が存在する必要があります：**sqlncli11.dll**。

アクセス DLL はMicrosoftの Web サイトにあります。

>[!NOTE]
>
>Linux で実行されているアプリケーションサーバーからのMicrosoft SQL Server へのアクセスはサポートされていません。

## Oracle {#oracle}

>[!NOTE]
>
>マルチバイト文字の列名はサポートされていません。

**NLS_NCHAR_CHARACTERSET** および **NLS_CHARACTERSET** パラメータは、データベースが Unicode または ANSI で動作するように正しく設定されている必要があります。

Adobe CampaignはデフォルトのOracleエンコーディングを使用します。 その他のエンコーディングを使用すると、トリガーの互換性の問題が発生する場合があります。この場合は、テクニカルサポートにお問い合わせください。

エンコードを調べるには、次の **sqlplus** コマンドを使用します。

```
SELECT * FROM nls_database_parameters ;
```

* Unicode インストールの場合、サポートされるエンコードは次のとおりです。

   ```
   NLS_NCHAR_CHARACTERSET         AL16UTF16
   NLS_CHARACTERSET         AL32UTF8
   ```

* ANSI インストール（非 Unicode）の場合、次のエンコードのみがサポートされます。

```
  NLS_CHARACTERSET WE8MSWIN1252
```

**sqlplus** にログオンするには、次のOracle・ユーザー・プロファイルを使用します。

```
su - oracle 
sqlplus 
[login] [password]
```

[Linux のOracle・クライアント ](../../installation/using/installing-packages-with-linux.md#oracle-client-in-linux) も参照できます。

## PostgresSQL {#postgressql}

データベースエンジンをインストールする場合は、UTF-8 サポートをインストールすることをお勧めします。 これにより、Unicode データベースを作成できます。

**関連トピック**

* [Adobe Campaign Classicテーブルのログなしオプション](https://helpx.adobe.com/campaign/kb/unlogged-tables-classic.html)
