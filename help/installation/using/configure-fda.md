---
title: FDAコネクタの設定
description: FDAの設定手順を学ぶ
page-status-flag: never-activated
uuid: b84359b9-c584-431d-80d5-71146d9b6854
contentOwner: sauviat
products: SG_CAMPAIGN/CLASSIC
audience: platform
content-type: reference
topic-tags: connectors
discoiquuid: dd3d14cc-5153-428d-a98a-32b46f0fe811
translation-type: tm+mt
source-git-commit: 3d6515ca291715e5e02f9b5404803e9087555284
workflow-type: tm+mt
source-wordcount: '299'
ht-degree: 70%

---


# FDA コネクタの設定 {#specific-configurations-by-database-type}

Adobe Campaign から外部データベースにアクセスできるようにするには、使用する外部データベースに応じて特定の設定をおこなう必要があります。これらの設定は、基本的には、ドライバーをインストールし、Adobe Campaign サーバー上の各 RDBMS に属する環境変数を宣言することです。

原則として、外部データベースの対応するクライアントレイヤーを Adobe Campaign サーバーにインストールする必要があります。

>[!NOTE]
>
>互換性のあるバージョンは [Campaign 互換性マトリックス](../../rn/using/compatibility-matrix.md#FederatedDataAccessFDA)に記載されています。


## 設定の手順 {#fda-configuration-steps}

FDAを使用して外部データベースへのアクセスを設定するには、次の構成手順を実行します。

1. Adobe Campaign サーバーに、データベースに対応するドライバーをインストールします。ドライバは、次に示すデータベース固有のページ [に一覧表示されます](#fda-specific-configuration)。
1. Adobe Campaign と外部データベースの間の接続を確立するための[外部アカウントを作成および設定](../../installation/using/connecting-to-database.md)します。キャンペーンの外部アカウントの詳細については、 [このページを参照してください](../../installation/using/external-accounts.md)。
1. Adobe Campaign で、外部データベースの[スキーマを作成](../../installation/using/creating-data-schema.md)します。これにより、外部データベースのデータ構造を認識できるようになります。
1. 必要に応じて、以前に作成したスキーマーから新しいターゲットマッピング [を](../../installation/using/defining-data-mapping.md) 作成します。 これは、配信の受信者が外部データベースから来ている場合に必要です。 この実装には、メッセージのパーソナライゼーションに関する制限があります。

データスキーマを作成すると、Adobe Campaign ワークフローでデータを処理できるようになります。詳しくは、[この節](../../workflow/using/accessing-an-external-database--fda-.md)を参照してください。

## データベース固有の設定 {#fda-specific-configuration}

Adobe Campaign から外部データベースにアクセスできるようにするには、使用する外部データベースに応じて特定の設定をおこなう必要があります。これらの設定は、基本的には、ドライバーをインストールし、Adobe Campaign サーバー上の各 RDBMS に属する環境変数を宣言することです。

詳細については、次のリンクを参照してください。

* [Azure Snapse](../../installation/using/configure-fda-synapse.md)

* [Snowflake](../../installation/using/configure-fda-snowflake.md)

* [Hadoop](../../installation/using/configure-fda-hadoop.md)

* [Oracle](../../installation/using/configure-fda-oracle.md)

* [Netezza](../../installation/using/configure-fda-netezza.md)

* [Sybase IQ](../../installation/using/configure-fda-sybase.md)

* [Teradata](../../installation/using/configure-fda-teradata.md)

* [SAP HANA](../../installation/using/configure-fda-sap-hana.md)
