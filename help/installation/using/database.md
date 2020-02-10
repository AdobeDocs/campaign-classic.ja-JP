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
index: y
internal: n
snippet: y
translation-type: tm+mt
source-git-commit: 28614a6b0c45deef17d9b3275a16e65bdff4538b

---


# データベース{#database}

データベース・サーバは、アプリケーション・サーバが使用するオペレーティング・システムに関係なく、任意のオペレーティング・システム上で実行できます。ただし、その間にネットワーク接続が存在する場合に限ります。

Adobe Campaignの様々なコンポーネントとの接続が可能な限り、データベースサーバーのオペレーティングシステムは重要ではありません。

また、「 [Database access layers」セクションも確認します](../../installation/using/prerequisites-of-campaign-installation-in-linux.md#database-access-layers) 。

## Microsoft SQL Server {#microsoft-sql-server}

ネイティブクライアントは、Adobe Campaignアプリケーションサーバーにインストールする必要があります。

ODBCドライバ設定パネルの **SQL Native Client** （Microsoft SQL Server 2005クライアントの場合）または **SQL Server Native Client 10.0** （Microsoft SQL Server 2008および2008 R2クライアントの場合）で、サーバ上のネイティブクライアントを確認できます。また **はSQL Server Native Client 11.0** （Microsoft SQL Server 2012クライアント用）。

次のアクセスDLLが必要です：

* **microsoft SQL Server 2005クライアント用のsqlncli.dll** 、
* **microsoft SQL Server 2008および** 2008 R2クライアントの場合はsqlncli10.dll、
* **microsoft SQL Server 2012クライアントの場合は** 、sqlncli11.dllを使用します。

   アクセスDLLは、MicrosoftのWebサイトで見つかります。

>[!NOTE]
>
>Linuxで実行されているアプリケーションサーバーからMicrosoft SQL serverへのアクセスはサポートされていません。

## Oracle {#oracle}

>[!NOTE]
>
>マルチバイト文字を含む列名はサポートされていません。

データベースがUnicodeまたはANSIで動作するためには、 **NLS_NCHAR_CHARACTERSET** と **** NLS_CHARACTERSETの各パラメータを正しく設定する必要があります。

Adobe Campaignでは、デフォルトのOracleエンコーディングを使用します。 他のエンコーディングを使用すると、互換性の問題が発生する可能性があります。この場合は、テクニカルサポートにお問い合わせください。

使用しているエンコードを確認するには、次の **sqlplusコマンドを使用します** 。

```
SELECT * FROM nls_database_parameters ;
```

* Unicodeの場合、次のエンコーディングがサポートされます。

   ```
   NLS_NCHAR_CHARACTERSET         AL16UTF16
   NLS_CHARACTERSET         AL32UTF8
   ```

* ANSIインストール（非Unicode）の場合、次のエンコードのみがサポートされます。

```
  NLS_CHARACTERSET WE8MSWIN1252
```

sqlplusにログオンするには、 **Oracleユーザー**・プロファイルを使用します。

```
su - oracle 
sqlplus 
[login] [password]
```

また、Linuxでは [Oracle clientを参照できます](../../installation/using/installing-packages-with-linux.md#oracle-client-in-linux)。

## PostgresSQL {#postgressql}

データベースエンジンをインストールする場合は、UTF-8サポートをインストールすることをお勧めします。 これにより、Unicodeデータベースを作成できます。

**関連トピック**

* [Adobe Campaign Classicの表のログなしオプション](https://helpx.adobe.com/campaign/kb/unlogged-tables-classic.html)