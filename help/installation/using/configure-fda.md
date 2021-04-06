---
solution: Campaign Classic
product: campaign
title: FDAコネクタの設定
description: FDAの設定手順を学ぶ
audience: platform
content-type: reference
topic-tags: connectors
exl-id: 0b53b165-a6d8-4604-b3f0-3fa6fce35146
translation-type: tm+mt
source-git-commit: 7ce5a01b57092043b8d9b52761b243f771cf74f2
workflow-type: tm+mt
source-wordcount: '322'
ht-degree: 44%

---

# FDA コネクタの設定 {#specific-configurations-by-database-type}

Adobe Campaign から外部データベースにアクセスできるようにするには、使用する外部データベースに応じて特定の設定をおこなう必要があります。これらの設定は、基本的には、ドライバーをインストールし、Adobe Campaign サーバー上の各 RDBMS に属する環境変数を宣言することです。

原則として、外部データベースの対応するクライアントレイヤーを Adobe Campaign サーバーにインストールする必要があります。

>[!NOTE]
>
>互換性のあるバージョンは [Campaign 互換性マトリックス](../../rn/using/compatibility-matrix.md#FederatedDataAccessFDA)に記載されています。


## 設定の手順 {#fda-configuration-steps}

FDAを使用して外部データベースへのアクセスを設定するには、次の構成手順を実行します。

1. ドライバーをインストールし、Adobe Campaignサーバー上のデータベースに対応する外部アカウントを設定します。 ](#fda-specific-configuration)の下に示すデータベース固有のページ[を参照
1. 外部アカウントをテストするか、Adobe Campaignと外部データベースの間に一時的な接続を作成します。 [詳細情報](../../installation/using/connecting-to-database.md)
1. Adobe Campaign で、外部データベースのスキーマを作成します。これにより、外部データベースのデータ構造を識別できます。 [詳細情報](../../installation/using/creating-data-schema.md)
1. 必要に応じて、以前に作成したスキーマから新しいターゲットマッピングを作成します。 これは、配信の受信者が外部データベースから来ている場合に必要です。 この実装には、メッセージのパーソナライゼーションに関する制限があります。 [詳細情報](../../installation/using/defining-data-mapping.md)

データスキーマを作成すると、Adobe Campaign ワークフローでデータを処理できるようになります。詳しくは、[この節](../../workflow/using/accessing-an-external-database--fda-.md)を参照してください。

## データベース固有の構成{#fda-specific-configuration}

Adobe Campaign から外部データベースにアクセスできるようにするには、使用する外部データベースに応じて特定の設定をおこなう必要があります。これらの設定では、基本的に、ドライバのインストール、Adobe Campaignサーバ上の各RDBMSに属する環境変数の宣言、外部アカウントの設定が行われます。

詳細については、次のリンクを参照してください。

* キャンペーンと[Azure synapse](../../installation/using/configure-fda-synapse.md)を接続

* キャンペーンと[Snowflake](../../installation/using/configure-fda-snowflake.md)を接続

* キャンペーンと[Hadoop](../../installation/using/configure-fda-hadoop.md)を接続

* キャンペーンと[Oracle](../../installation/using/configure-fda-oracle.md)を接続

* キャンペーンと[Netezza](../../installation/using/configure-fda-netezza.md)を接続

* キャンペーンと[Sybase IQ](../../installation/using/configure-fda-sybase.md)を接続

* キャンペーンと[Teradata](../../installation/using/configure-fda-teradata.md)を接続

* キャンペーンと[SAP HANA](../../installation/using/configure-fda-sap-hana.md)を接続
