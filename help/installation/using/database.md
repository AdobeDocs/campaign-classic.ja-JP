---
product: campaign
title: Campaign Classicデータベースの推奨事項
description: データベースの推奨事項
audience: installation
content-type: reference
topic-tags: prerequisites-and-recommendations-
exl-id: 8a0426c1-9e8d-4053-bc2b-6a550e2eed2f
source-git-commit: 98d646919fedc66ee9145522ad0c5f15b25dbf2e
workflow-type: tm+mt
source-wordcount: '277'
ht-degree: 2%

---

# データベース{#database}

データベース・サーバは、アプリケーション・サーバが使用するオペレーティング・システムに関係なく、任意のオペレーティング・システム上で実行できます。

Adobe Campaignの様々なコンポーネントとの接続が可能である限り、データベースサーバーのオペレーティングシステムは重要ではありません。

[データベースアクセスレイヤー](../../installation/using/prerequisites-of-campaign-installation-in-linux.md#database-access-layers)の節も確認してください。

## Microsoft SQL Server {#microsoft-sql-server}

ネイティブクライアントは、Adobe Campaignアプリケーションサーバーにインストールする必要があります。

**SQL Server Native Client 11.0**&#x200B;の下のODBCドライバー設定パネルで、サーバー上のネイティブクライアントを確認できます。

次のアクセスDLLが存在する必要があります：**sqlncli11.dll**&#x200B;を指定します。

アクセスDLLはMicrosoftのWebサイトにあります。

>[!NOTE]
>
>Linuxで実行されているアプリケーションサーバーからのMicrosoft SQL Serverへのアクセスはサポートされていません。

## Oracle {#oracle}

>[!NOTE]
>
>マルチバイト文字を含む列名はサポートされていません。

**NLS_NCHAR_CHARACTERSET**&#x200B;および&#x200B;**NLS_CHARACTERSET**&#x200B;パラメータは、データベースがUnicodeまたはANSIで動作するように正しく設定されている必要があります。

Adobe CampaignはデフォルトのOracleエンコーディングを使用します。 その他のエンコーディングを使用すると、トリガーの互換性に関する問題が発生する場合があります。この場合は、テクニカルサポートにお問い合わせください。

使用するエンコーディングを確認するには、次の&#x200B;**sqlplus**&#x200B;コマンドを使用します。

```
SELECT * FROM nls_database_parameters ;
```

* Unicodeをインストールする場合、次のエンコードがサポートされます。

   ```
   NLS_NCHAR_CHARACTERSET         AL16UTF16
   NLS_CHARACTERSET         AL32UTF8
   ```

* ANSIインストール（非Unicode）の場合、次のエンコーディングのみがサポートされます。

```
  NLS_CHARACTERSET WE8MSWIN1252
```

**sqlplus**&#x200B;にログオンするには、次のOracle・ユーザー・プロファイルを使用します。

```
su - oracle 
sqlplus 
[login] [password]
```

Linuxの[Oracleクライアントも参照できます。](../../installation/using/installing-packages-with-linux.md#oracle-client-in-linux)

## PostgresSQL {#postgressql}

データベースエンジンをインストールする際には、UTF-8サポートをインストールすることをお勧めします。 これにより、Unicodeデータベースを作成できます。

**関連トピック**

* [Adobe Campaign Classicテーブルのログなしオプション](https://helpx.adobe.com/campaign/kb/unlogged-tables-classic.html)
