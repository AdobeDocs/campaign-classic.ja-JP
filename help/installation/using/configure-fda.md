---
product: campaign
title: FDA コネクタの設定
description: FDA の設定手順を説明します
badge-v7-only: label="v7" type="Informative" tooltip="Applies to Campaign Classic v7 only"
audience: platform
content-type: reference
topic-tags: connectors
exl-id: 0b53b165-a6d8-4604-b3f0-3fa6fce35146
source-git-commit: 8debcd3d8fb883b3316cf75187a86bebf15a1d31
workflow-type: tm+mt
source-wordcount: '342'
ht-degree: 59%

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

1. ドライバーをインストールし、Adobe Campaignサーバーにデータベースに対応する外部アカウントをセットアップします。 データベース固有のページを参照してください。 [次に示す](#fda-specific-configuration)
1. 外部アカウントをテストするか、Adobe Campaignと外部データベースの間に一時的な接続を作成します。 [詳細](../../installation/using/connecting-to-database.md)
1. Adobe Campaign で、外部データベースのスキーマを作成します。これにより、外部データベースのデータ構造を識別できるようになります。[詳細情報](../../installation/using/creating-data-schema.md)
1. 必要に応じて、以前に作成したスキーマから新しいターゲットマッピングを作成します。 これは、配信の受信者を外部データベースから取得している場合に必要です。 この実装には、メッセージのパーソナライゼーションに関する制限があります。 [詳細情報](../../installation/using/defining-data-mapping.md)

データスキーマを作成すると、Adobe Campaign ワークフローでデータを処理できるようになります。詳しくは、[この節](../../workflow/using/accessing-an-external-database--fda-.md)を参照してください。

## データベース固有の設定 {#fda-specific-configuration}

Adobe Campaign から外部データベースにアクセスできるようにするには、使用する外部データベースに応じて特定の設定をおこなう必要があります。これらの設定は、基本的に、ドライバーをインストールし、Adobe Campaignサーバー上の各 RDBMS に属する環境変数を宣言し、外部アカウントを設定することです。

詳しくは、以下のリンクを参照してください。

* Campaign との接続 [azure synapse](../../installation/using/configure-fda-synapse.md)
* Campaign との接続 [Google BigQuery](../../installation/using/configure-fda-google-big-query.md)
* Campaign との接続 [Hadoop](../../installation/using/configure-fda-hadoop.md)
* Campaign との接続 [Microsoft SQL Server](../../installation/using/configure-fda-sql.md)
* Campaign との接続 [Netezza](../../installation/using/configure-fda-netezza.md)
* Campaign との接続 [Oracle](../../installation/using/configure-fda-oracle.md)
* Campaign との接続 [PostgreSQL](../../installation/using/configure-fda-postgresql.md)
* Campaign との接続 [SAP HANA](../../installation/using/configure-fda-sap-hana.md)
* Campaign との接続 [Snowflake](../../installation/using/configure-fda-snowflake.md)
* Campaign との接続 [sybase IQ](../../installation/using/configure-fda-sybase.md)
* Campaign との接続 [Teradata](../../installation/using/configure-fda-teradata.md)
* Campaign との接続 [vertica analytics](../../installation/using/configure-fda-vertica.md)
