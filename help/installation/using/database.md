---
product: campaign
title: Campaign Classic Databaseの推奨事項
description: データベースの推奨事項
feature: Installation, Instance Settings
badge-v7-prem: label="オンプレミス／ハイブリッドのみ" type="Caution" url="https://experienceleague.adobe.com/docs/campaign-classic/using/installing-campaign-classic/architecture-and-hosting-models/hosting-models-lp/hosting-models.html?lang=ja" tooltip="オンプレミスデプロイメントとハイブリッドデプロイメントにのみ適用されます"
audience: installation
content-type: reference
topic-tags: prerequisites-and-recommendations-
exl-id: 8a0426c1-9e8d-4053-bc2b-6a550e2eed2f
source-git-commit: 14ba450ebff9bba6a36c0df07d715b7279604222
workflow-type: tm+mt
source-wordcount: '310'
ht-degree: 11%

---

# データベース{#database}



データベース・サーバは、アプリケーション・サーバまたはサーバ間にネットワーク接続がある限り、アプリケーション・サーバまたはサーバが使用するオペレーティング・システムに関係なく、任意のオペレーティング・システム上で実行できます。

データベース・サーバのオペレーティング・システムは、Adobe Campaignの様々なコンポーネントとの接続性が可能である限り重要ではありません。

[ データベースアクセスレイヤー](../../installation/using/prerequisites-of-campaign-installation-in-linux.md#database-access-layers) セクションも確認してください。

## Microsoft SQL Server {#microsoft-sql-server}

ネイティブクライアントは、Adobe Campaign アプリケーションサーバーにインストールする必要があります。

ODBC ドライバー設定パネル（**SQL Server Native Client 11.0**）で、サーバー上のネイティブクライアントを確認できます。

次のアクセス DLLが存在する必要があります：**sqlncli11.dll**。

アクセス DLLは、Microsoftのweb サイトにあります。

>[!NOTE]
>
>Linuxで動作するアプリケーションサーバーからのMicrosoft SQL Serverへのアクセスはサポートされていません。

## Oracle {#oracle}

>[!NOTE]
>
>マルチバイト文字を含む列名はサポートされていません。

データベースをUnicodeまたはANSIで動作させるには、**NLS_NCHAR_CHARACTERSET**&#x200B;および&#x200B;**NLS_CHARACTERSET** パラメーターを正しく設定する必要があります。

Adobe Campaignでは、デフォルトのOracle エンコーディングが使用されます。 他のエンコーディングを使用すると、トリガーの互換性の問題が発生する場合があります。この場合は、テクニカルサポートにお問い合わせください。

エンコーディングについて確認するには、次の&#x200B;**sqlplus** コマンドを使用します。

```
SELECT * FROM nls_database_parameters ;
```

* Unicode インストールの場合、サポートされるエンコーディングは次のとおりです。

  ```
  NLS_NCHAR_CHARACTERSET         AL16UTF16
  NLS_CHARACTERSET         AL32UTF8
  ```

* ANSI インストール（非Unicode）の場合、次のエンコーディングのみがサポートされます。

```
  NLS_CHARACTERSET WE8MSWIN1252
```

**sqlplus**&#x200B;にログオンするには、Oracle ユーザープロファイルを使用します。

```
su - oracle 
sqlplus 
[login] [password]
```

Linux](../../installation/using/installing-packages-with-linux.md#oracle-client-in-linux)で[Oracle Clientを参照することもできます。

## PostgresSQL {#postgressql}

データベースエンジンのインストール時には、UTF-8 サポートをインストールすることをお勧めします。 これにより、Unicode データベースを作成できるようになります。

**関連トピック**

* [Adobe Campaign Classic テーブルのログなしオプション](https://helpx.adobe.com/campaign/kb/unlogged-tables-classic.html)
