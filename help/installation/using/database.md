---
product: campaign
title: Campaign Classic Databaseの推奨事項
description: データベースの推奨事項
feature: Installation, Instance Settings
badge-v7-prem: label="On-premise/hybrid only" type="Caution" url="https://experienceleague.adobe.com/docs/campaign-classic/using/installing-campaign-classic/architecture-and-hosting-models/hosting-models-lp/hosting-models.html?lang=ja" tooltip="Applies to on-premise and hybrid deployments only"
audience: installation
content-type: reference
topic-tags: prerequisites-and-recommendations-
exl-id: 8a0426c1-9e8d-4053-bc2b-6a550e2eed2f
TQID: 'https://experienceleague.adobe.com/1rAC8pXCS8aKbzDrjv1HCa4W-Ieh3fx-nBzFbe8nMjg'
product_v2:
  - id: dfc56824-e8b9-499e-85d4-21aedb507314
    internal-label: Campaign
  - id: fd6e6e36-54e4-4f1a-96fc-1a750e400d50
    internal-label: Campaign Classic v7
feature_v2:
  - id: 7f0a1ee5-eeb8-5478-a9cd-b1896f033118
    internal-label: Instance Settings
  - id: c5474392-5419-4296-9e41-f6f4ce4f6e9b
    internal-label: Administration
subfeature_v2:
  - id: e656c701-3899-4db3-989c-de0980ddfffa
    internal-label: Installation
topic_v2:
  - id: d095671a-1355-40aa-8b5f-06c33c68080b
    internal-label: Security
  - id: f4e6943a-c91a-4134-a2c7-f4f20cfff2f0
    internal-label: Privacy
source-git-commit: a43e591a565a18d79f583d975e3e812c5435b0c0
workflow-type: tm+mt
source-wordcount: '298'
ht-degree: 8%
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
