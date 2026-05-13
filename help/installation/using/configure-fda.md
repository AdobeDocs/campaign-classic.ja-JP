---
product: campaign
title: FDA コネクタの設定
description: FDAの設定手順について説明します
feature: Installation, Federated Data Access
audience: platform
content-type: reference
topic-tags: connectors
exl-id: 0b53b165-a6d8-4604-b3f0-3fa6fce35146
TQID: https://experienceleague.adobe.com/F1-F9k9cn7jFb-xmYCQUq5h1-3A6-bajr1cfxeHNPf0
product_v2: id: dfc56824-e8b9-499e-85d4-21aedb507314
topic_v2: id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87cid: cdd65e7e-8839-44a2-bc21-0e03623b5dd1id: e0eb8757-182f-49f3-94a4-1587d16f5094
source-git-commit: 4c295c0dabae8aba298390a3da2422a3fa1219f9
workflow-type: tm+mt
source-wordcount: 355
ht-degree: 58%

---

# FDA コネクタの設定 {#specific-configurations-by-database-type}



Adobe Campaign から外部データベースにアクセスできるようにするには、使用する外部データベースに応じて特定の設定をおこなう必要があります。 これらの設定は、基本的には、ドライバーをインストールし、Adobe Campaign サーバー上の各 RDBMS に属する環境変数を宣言することです。

原則として、外部データベースの対応するクライアントレイヤーを Adobe Campaign サーバーにインストールする必要があります。

>[!NOTE]
>
>互換性のあるバージョンは [Campaign 互換性マトリックス](../../rn/using/compatibility-matrix.md#FederatedDataAccessFDA)に記載されています。
>

## 設定の手順 {#fda-configuration-steps}

FDA を使用して外部データベースへのアクセスを設定するには、次の設定手順を実行します。

1. ドライバをインストールし、Adobe Campaign サーバ上のデータベースに対応する外部アカウントを設定します。 以下のデータベース固有のページ [を参照してください](#fda-specific-configuration)
1. 外部アカウントをテストするか、Adobe Campaignと外部データベースの間に一時的な接続を作成します。 [詳細情報](../../installation/using/connecting-to-database.md)
1. Adobe Campaign で、外部データベースのスキーマを作成します。 これにより、外部データベースのデータ構造を識別できるようになります。 [詳細情報](../../installation/using/creating-data-schema.md)
1. 必要に応じて、以前に作成したスキーマから新しいターゲットマッピングを作成します。 これは、配信の受信者を外部データベースから取得している場合に必要です。 この実装には、メッセージのパーソナライゼーションに関する制限があります。 [詳細情報](../../installation/using/defining-data-mapping.md)

データスキーマを作成すると、Adobe Campaign ワークフローでデータを処理できるようになります。 [Campaign v8 ドキュメント](https://experienceleague.adobe.com/docs/campaign/automation/campaign-optimization/campaign-typologies.html?lang=ja){target="_blank"}を参照してください。

## データベース固有の設定 {#fda-specific-configuration}

Adobe Campaign から外部データベースにアクセスできるようにするには、使用する外部データベースに応じて特定の設定をおこなう必要があります。 これらの設定には、基本的に、Adobe Campaign サーバー上の各RDBMSに属するドライバーのインストールと環境変数の宣言、および外部アカウントの設定が含まれます。

詳細については、以下のリンクを参照してください。

* Campaignと[Amazon Redshift](../../installation/using/configure-fda-redshift.md)を接続
* Campaignと[Azure Synapse](../../installation/using/configure-fda-synapse.md)を連携
* Campaignと[Google BigQuery](../../installation/using/configure-fda-google-big-query.md)を接続
* Campaignと[Hadoop](../../installation/using/configure-fda-hadoop.md)を連携
* Campaignと[Microsoft SQL Server](../../installation/using/configure-fda-sql.md)を接続
* Campaignと[Netezza](../../installation/using/configure-fda-netezza.md)を連携
* Campaignと[Oracle](../../installation/using/configure-fda-oracle.md)を連携
* Campaignと[PostgreSQL](../../installation/using/configure-fda-postgresql.md)を接続
* Campaignと[SAP HANA](../../installation/using/configure-fda-sap-hana.md)を連携
* Campaignと[Snowflake](../../installation/using/configure-fda-snowflake.md)を連携
* Campaignと[Sybase IQ](../../installation/using/configure-fda-sybase.md)を連携
* Campaignと[Teradata](../../installation/using/configure-fda-teradata.md)を連携
* Campaignと[Vertica Analytics](../../installation/using/configure-fda-vertica.md)を連携
