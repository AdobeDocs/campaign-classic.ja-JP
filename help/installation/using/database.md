---
solution: Campaign Classic
product: campaign
title: Campaign Classicデータベースの推奨事項
description: データベースの推奨事項
audience: installation
content-type: reference
topic-tags: prerequisites-and-recommendations-
translation-type: tm+mt
source-git-commit: 972885c3a38bcd3a260574bacbb3f507e11ae05b
workflow-type: tm+mt
source-wordcount: '277'
ht-degree: 2%

---


# データベース{#database}

データベース・サーバは、アプリケーション・サーバが使用するオペレーティング・システムに関係なく、任意のオペレーティング・システム上で実行できます。ただし、サーバ間にネットワーク接続が存在する場合に限ります。

データベース・サーバのオペレーティング・システムは、Adobe Campaignの異なるコンポーネントとの接続が可能な限り重要ではありません。

また、「 [Database access layers](../../installation/using/prerequisites-of-campaign-installation-in-linux.md#database-access-layers) 」セクションも確認します。

## Microsoft SQL Server {#microsoft-sql-server}

ネイティブクライアントは、Adobe Campaignアプリケーションサーバーにインストールする必要があります。

SQL Server Native Client 11.0の[ODBCドライバの設定]パネルで、サーバ上のネイティブ・クライアントを確認でき **ます**。

次のアクセスDLLが必要です： **sqlncli11.dll**.

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

sqlplusにログオンするには、 **Oracleユーザープロファイルを使用します**。

```
su - oracle 
sqlplus 
[login] [password]
```

Linuxでは [Oracleクライアントも参照できます](../../installation/using/installing-packages-with-linux.md#oracle-client-in-linux)。

## PostgresSQL {#postgressql}

データベースエンジンをインストールする場合は、UTF-8サポートをインストールすることをお勧めします。 これにより、Unicodeデータベースを作成できます。

**関連トピック**

* [Adobe Campaign Classicテーブルのログなしオプション](https://helpx.adobe.com/campaign/kb/unlogged-tables-classic.html)
