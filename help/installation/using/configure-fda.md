---
product: campaign
title: FDA コネクタの設定
description: FDA の設定手順を学ぶ
feature: Installation, Federated Data Access
audience: platform
content-type: reference
topic-tags: connectors
exl-id: 0b53b165-a6d8-4604-b3f0-3fa6fce35146
source-git-commit: b666535f7f82d1b8c2da4fbce1bc25cf8d39d187
workflow-type: tm+mt
source-wordcount: '347'
ht-degree: 57%

---

# FDA コネクタの設定 {#specific-configurations-by-database-type}



Adobe Campaign から外部データベースにアクセスできるようにするには、使用する外部データベースに応じて特定の設定をおこなう必要があります。これらの設定は、基本的には、ドライバーをインストールし、Adobe Campaign サーバー上の各 RDBMS に属する環境変数を宣言することです。

原則として、外部データベースの対応するクライアントレイヤーを Adobe Campaign サーバーにインストールする必要があります。

>[!NOTE]
>
>互換性のあるバージョンは [Campaign 互換性マトリックス](../../rn/using/compatibility-matrix.md#FederatedDataAccessFDA)に記載されています。
>

## 設定の手順 {#fda-configuration-steps}

FDA を使用して外部データベースへのアクセスを設定するには、次の設定手順を実行します。

1. ドライバーをインストールし、Adobe Campaign サーバー上のデータベースに対応する外部アカウントを設定します。 データベース固有のページを参照してください。 [以下にリスト](#fda-specific-configuration)
1. 外部アカウントをテストするか、Adobe Campaignと外部データベースの間に一時的な接続を作成します。 [詳細](../../installation/using/connecting-to-database.md)
1. Adobe Campaign で、外部データベースのスキーマを作成します。これにより、外部データベースのデータ構造を識別できるようになります。[詳細情報](../../installation/using/creating-data-schema.md)
1. 必要に応じて、以前に作成したスキーマから新しいターゲットマッピングを作成します。 これは、配信の受信者を外部データベースから取得している場合に必要です。 この実装には、メッセージのパーソナライゼーションに関する制限があります。 [詳細情報](../../installation/using/defining-data-mapping.md)

データスキーマを作成すると、Adobe Campaign ワークフローでデータを処理できるようになります。詳しくは、[この節](../../workflow/using/accessing-an-external-database-fda.md)を参照してください。

## データベース固有の設定 {#fda-specific-configuration}

Adobe Campaign から外部データベースにアクセスできるようにするには、使用する外部データベースに応じて特定の設定をおこなう必要があります。これらの設定には基本的に、Adobe Campaign サーバー上の各 RDBMS に属するドライバーのインストールと環境変数の宣言および外部アカウントの設定が含まれます。

詳しくは、以下のリンクを参照してください。

* Campaign とを接続 [Amazon Redshift](../../installation/using/configure-fda-redshift.md)
* Campaign とを接続 [Azure synapse](../../installation/using/configure-fda-synapse.md)
* Campaign とを接続 [Google BigQuery](../../installation/using/configure-fda-google-big-query.md)
* Campaign とを接続 [Hadoop](../../installation/using/configure-fda-hadoop.md)
* Campaign とを接続 [Microsoft SQL Server](../../installation/using/configure-fda-sql.md)
* Campaign とを接続 [Netezza](../../installation/using/configure-fda-netezza.md)
* Campaign とを接続 [Oracle](../../installation/using/configure-fda-oracle.md)
* Campaign とを接続 [PostgreSQL](../../installation/using/configure-fda-postgresql.md)
* Campaign とを接続 [SAP HANA](../../installation/using/configure-fda-sap-hana.md)
* Campaign とを接続 [Snowflake](../../installation/using/configure-fda-snowflake.md)
* Campaign とを接続 [Sybase IQ](../../installation/using/configure-fda-sybase.md)
* Campaign とを接続 [Teradata](../../installation/using/configure-fda-teradata.md)
* Campaign とを接続 [Vertica analytics](../../installation/using/configure-fda-vertica.md)
