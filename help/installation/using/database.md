---
product: campaign
title: Campaign Classicデータベースの推奨
description: データベースの推奨事項
badge-v7-only: label="v7" type="Informative" tooltip="Applies to Campaign Classic v7 only"
badge-v7-prem: label="on-premise & hybrid" type="Caution" url="https://experienceleague.adobe.com/docs/campaign-classic/using/installing-campaign-classic/architecture-and-hosting-models/hosting-models-lp/hosting-models.html" tooltip="Applies to on-premise and hybrid deployments only"
audience: installation
content-type: reference
topic-tags: prerequisites-and-recommendations-
exl-id: 8a0426c1-9e8d-4053-bc2b-6a550e2eed2f
source-git-commit: 4661688a22bd1a82eaf9c72a739b5a5ecee168b1
workflow-type: tm+mt
source-wordcount: '277'
ht-degree: 2%

---

# データベース{#database}



データベース・サーバは、アプリケーション・サーバが使用するオペレーティング・システムに関係なく、任意のオペレーティング・システム上で実行できます。

Adobe Campaignの様々なコンポーネントとの接続が利用できる限り、データベースサーバーのオペレーティングシステムは重要ではありません。

また、 [データベースアクセスレイヤー](../../installation/using/prerequisites-of-campaign-installation-in-linux.md#database-access-layers) 」セクションに入力します。

## Microsoft SQL Server {#microsoft-sql-server}

ネイティブクライアントは、Adobe Campaignアプリケーションサーバーにインストールする必要があります。

サーバー上のネイティブクライアントを確認するには、[ODBC ドライバーの設定 ] パネルの [ **SQL Server Native Client 11.0**.

次のアクセス DLL が存在する必要があります： **sqlncli11.dll**.

アクセス DLL がMicrosoftの Web サイトに見つかりました。

>[!NOTE]
>
>Linux で実行されているアプリケーションサーバーからのMicrosoft SQL Server へのアクセスはサポートされていません。

## Oracle {#oracle}

>[!NOTE]
>
>2 バイト文字を含む列名はサポートされていません。

この **NLS_NCHAR_CHARACTERSET** および **NLS_CHARACTERSET** データベースが Unicode または ANSI で動作するように、パラメータを正しく設定する必要があります。

Adobe CampaignはデフォルトのOracleエンコーディングを使用します。 他のエンコーディングを使用すると、トリガーの互換性の問題が発生する場合があります。この場合は、テクニカルサポートにお問い合わせください。

エンコーディングを確認するには、次を使用します **sqlplus** コマンド：

```
SELECT * FROM nls_database_parameters ;
```

* Unicode インストールの場合、次のエンコードがサポートされます。

   ```
   NLS_NCHAR_CHARACTERSET         AL16UTF16
   NLS_CHARACTERSET         AL32UTF8
   ```

* ANSI インストール（非 Unicode）の場合、次のエンコーディングのみがサポートされます。

```
  NLS_CHARACTERSET WE8MSWIN1252
```

にログオンするには **sqlplus**&#x200B;を使用する場合は、次のOracleユーザープロファイルを使用します。

```
su - oracle 
sqlplus 
[login] [password]
```

また、 [Linux のoracleクライアント](../../installation/using/installing-packages-with-linux.md#oracle-client-in-linux).

## PostgresSQL {#postgressql}

データベースエンジンをインストールする際には、UTF-8 サポートをインストールすることをお勧めします。 これにより、Unicode データベースを作成できます。

**関連トピック**

* [Adobe Campaign Classicテーブルのログなしオプション](https://helpx.adobe.com/campaign/kb/unlogged-tables-classic.html)
