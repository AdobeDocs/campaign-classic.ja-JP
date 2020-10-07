---
title: データベース
seo-title: データベース
description: データベース
seo-description: null
page-status-flag: never-activated
uuid: b318365c-8846-4c1d-b5f7-ece55fb8c4af
contentOwner: sauviat
products: SG_CAMPAIGN/CLASSIC
audience: installation
content-type: reference
topic-tags: prerequisites-and-recommendations-
discoiquuid: 1dcf01af-c2f3-4975-ba05-628d52952064
translation-type: tm+mt
source-git-commit: 70b143445b2e77128b9404e35d96b39694d55335
workflow-type: tm+mt
source-wordcount: '307'
ht-degree: 3%

---


# データベース{#database}

データベース・サーバは、アプリケーション・サーバが使用するオペレーティング・システムに関係なく、任意のオペレーティング・システム上で実行できます。ただし、サーバ間にネットワーク接続が存在する場合に限ります。

データベース・サーバのオペレーティング・システムは、Adobe Campaignの異なるコンポーネントとの接続が可能な限り重要ではありません。

また、「 [Database access layers](../../installation/using/prerequisites-of-campaign-installation-in-linux.md#database-access-layers) 」セクションも確認します。

## Microsoft SQL Server {#microsoft-sql-server}

ネイティブクライアントは、Adobe Campaignアプリケーションサーバーにインストールする必要があります。

SQL Server Native Client 10.0 **（Microsoft SQL Server 2008および2008 R2クライアントの場合）または** SQL Server Native Client 11.0 **** （Microsoft SQL Server 20クライアントの場合）の下のODBCドライバ設定パネルを使用して、サーバー上のネイティブクライアントを確認できます。（2014年、2016年、2017年の各クライアント）。

次のアクセスDLLが必要です：

* **sqlncli10.dll** for Microsoft SQL Server 2008 and 2008 R2 clients,
* **sqlncli11.dll** （Microsoft SQL Server 2012、2014、2016、2017の各クライアント用）。

   アクセスDLLは、MicrosoftのWebサイトにあります。

>[!NOTE]
>
>Linuxで実行しているアプリケーションサーバーからのMicrosoft SQL Serverへのアクセスはサポートされていません。

## Oracle {#oracle}

>[!NOTE]
>
>マルチバイト文字を含む列名はサポートされていません。

データベースがUnicodeまたはANSIで動作するためには、 **NLS_NCHAR_CHARACTERSET****パラメータと** NLS_CHARACTERSETパラメータを正しく設定する必要があります。

Adobe Campaignでは、デフォルトのOracleエンコーディングが使用されます。 他のエンコーディングを使用すると、互換性の問題が発生する可能性があります。この場合は、テクニカルサポートにお問い合わせください。

エンコーディングを確認するには、次の **sqlplus** コマンドを使用します。

```
SELECT * FROM nls_database_parameters ;
```

* Unicodeのインストールの場合、次のエンコーディングがサポートされます。

   ```
   NLS_NCHAR_CHARACTERSET         AL16UTF16
   NLS_CHARACTERSET         AL32UTF8
   ```

* ANSIインストール（非Unicode）の場合、次のエンコーディングのみがサポートされます。

```
  NLS_CHARACTERSET WE8MSWIN1252
```

sqlplusにログオンするには、Oracleユーザー **プロファイルを使用します**。

```
su - oracle 
sqlplus 
[login] [password]
```

また、Linuxでは [Oracle Clientを参照できます](../../installation/using/installing-packages-with-linux.md#oracle-client-in-linux)。

## PostgresSQL {#postgressql}

データベースエンジンをインストールする場合は、UTF-8サポートをインストールすることをお勧めします。 これにより、Unicodeデータベースを作成できます。

**関連トピック**

* [Adobe Campaign Classicテーブルのログなしオプション](https://helpx.adobe.com/campaign/kb/unlogged-tables-classic.html)