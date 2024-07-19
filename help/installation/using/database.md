---
product: campaign
title: Campaign Classicデータベースの推奨事項
description: データベースの推奨事項
feature: Installation, Instance Settings
badge-v7-prem: label="オンプレミス／ハイブリッドのみ" type="Caution" url="https://experienceleague.adobe.com/docs/campaign-classic/using/installing-campaign-classic/architecture-and-hosting-models/hosting-models-lp/hosting-models.html?lang=ja" tooltip="オンプレミスデプロイメントとハイブリッドデプロイメントにのみ適用されます"
audience: installation
content-type: reference
topic-tags: prerequisites-and-recommendations-
exl-id: 8a0426c1-9e8d-4053-bc2b-6a550e2eed2f
source-git-commit: 14ba450ebff9bba6a36c0df07d715b7279604222
workflow-type: tm+mt
source-wordcount: '282'
ht-degree: 6%

---

# データベース{#database}



データベース・サーバは、アプリケーション・サーバまたはサーバが使用するオペレーティング・システムに関係なく、それらの間にネットワーク接続がある限り、特定のオペレーティング・システム上で実行できます。

データベースサーバーのオペレーティングシステムは、Adobe Campaignの様々なコンポーネントとの接続が可能であれば重要ではありません。

また、「[ データベースアクセスレイヤー ](../../installation/using/prerequisites-of-campaign-installation-in-linux.md#database-access-layers) セクションも確認してください。

## Microsoft SQL Server {#microsoft-sql-server}

ネイティブクライアントをAdobe Campaign アプリケーションサーバーにインストールする必要があります。

サーバー上のネイティブ クライアントは、ODBC ドライバー構成パネルの **SQL Server Native Client 11.0** で確認できます。

アクセス DLL **sqlncli11.dll** が必要です。

アクセス DLL はMicrosoftの Web サイトにあります。

>[!NOTE]
>
>Linux で動作しているアプリケーションサーバーからMicrosoft SQL Server へのアクセスはサポートされていません。

## Oracle {#oracle}

>[!NOTE]
>
>マルチバイト文字を含む列名はサポートされていません。

**NLS_NCHAR_CHARACTERSET** および **NLS_CHARACTERSET** パラメータは、データベースが Unicode または ANSI で動作するように正しく設定されている必要があります。

Adobe Campaignでは、デフォルトのOracleエンコーディングが使用されます。 他のエンコーディングを使用すると、トリガーの互換性の問題が発生する場合があります。この場合は、テクニカルサポートにお問い合わせください。

エンコーディングを確認するには、次の **sqlplus** コマンドを使用します。

```
SELECT * FROM nls_database_parameters ;
```

* Unicode インストールの場合、サポートされているエンコードは次のとおりです。

  ```
  NLS_NCHAR_CHARACTERSET         AL16UTF16
  NLS_CHARACTERSET         AL32UTF8
  ```

* ANSI インストール （非 Unicode）の場合、次のエンコードのみがサポートされます。

```
  NLS_CHARACTERSET WE8MSWIN1252
```

**sqlplus** にログオンするには、Oracleユーザープロファイルを使用します。

```
su - oracle 
sqlplus 
[login] [password]
```

また、[Linux のOracleクライアント ](../../installation/using/installing-packages-with-linux.md#oracle-client-in-linux) も参照してください。

## PostgresSQL {#postgressql}

データベースエンジンをインストールする際は、UTF-8 サポートをインストールすることをお勧めします。 これにより、Unicode データベースを作成できるようになります。

**関連トピック**

* [Adobe Campaign Classic テーブルの未ログオプション ](https://helpx.adobe.com/campaign/kb/unlogged-tables-classic.html)
