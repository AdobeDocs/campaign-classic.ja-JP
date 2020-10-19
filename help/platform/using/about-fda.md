---
title: 外部データベースへのアクセス
description: 外部データベースのデータにアクセスして処理する方法を学びます。
page-status-flag: never-activated
uuid: b84359b9-c584-431d-80d5-71146d9b6854
contentOwner: sauviat
products: SG_CAMPAIGN/CLASSIC
audience: platform
content-type: reference
topic-tags: connectors
discoiquuid: dd3d14cc-5153-428d-a98a-32b46f0fe811
translation-type: tm+mt
source-git-commit: b447e316bed8e0e87d608679c147e6bd7b0815eb
workflow-type: tm+mt
source-wordcount: '583'
ht-degree: 98%

---


# Federated Data Access について {#about-federated-data-access}

Adobe Campaign では、**Federated Data Access**（FDA）オプションを利用することができます。このオプションを使用すると、1 つ以上の外部データベースに格納されている情報を処理することが可能です。Adobe Campaign データの構造を変更しなくても、外部データにアクセスできます。

>[!CAUTION]
>
>FDA 経由での外部データベースへのアクセスは、Snowflake コネクタを除き、オンプレミスまたはハイブリッドインストールでのみ可能です。詳しくは、この[ページ](https://helpx.adobe.com/jp/campaign/kb/acc-on-prem-vs-hosted.html)を参照してください。

## 動作の仕組み {#operating-principle}

FDA オプションを使用すると、サードパーティのデータベースでデータモデルを拡張できます。ターゲットテーブルの構造を自動的に検出し、SQL ソースのデータを使用します。

この機能を使用するには、以下をおこなう必要があります。

1. Adobe Campaign の FDA モジュールと互換性がある外部データベースを用意します。各種データベースシステムの互換性があるバージョンのリストについては、[互換性マトリックス](https://helpx.adobe.com/jp/campaign/kb/compatibility-matrix.html)を参照してください。さらに、Adobe Campaign および外部データベースで[必要な権限](../../platform/using/remote-database-access-rights.md)をユーザーに割り当てる必要があります。
1. Adobe Campaign サーバーに、データベースに対応する[ドライバをインストール](../../platform/using/specific-configuration-database.md)します。
1. Adobe Campaign と外部データベースの間の接続を確立するための[外部アカウントを作成および設定](../../platform/using/connecting-to-database.md)します。使用可能な外部アカウントについて詳しくは、この[ページ](../../platform/using/external-accounts.md)を参照してください。
1. Adobe Campaign で、外部データベースの[スキーマを作成](../../platform/using/creating-data-schema.md)します。これにより、外部データベースのデータ構造を認識できるようになります。
1. 最後に、前の手順で作成したスキーマから[新しいターゲットマッピングを作成](../../platform/using/defining-data-mapping.md)します。これは、配信の受信者を外部データベースから取得する場合に必要です。これにより、特に配信のパーソナライズに関して一定の制限を適用することが可能です。

データスキーマを作成すると、Adobe Campaign ワークフローでデータを処理できるようになります。詳しくは、[この節](../../workflow/using/accessing-an-external-database--fda-.md)を参照してください。

## 使用可能な外部データベース {#external-database}

Adobe Campaign FDA モジュールと互換性のあるすべての外部データベースのリストは、次のとおりです。

* Microsoft Azure Synapse Analytics：詳しくは、[この節](../../platform/using/specific-configuration-database.md#azure-external)を参照してください。
* Snowflake：詳しくは、[この節](../../platform/using/specific-configuration-database.md#configure-access-to-snowflake)を参照してください。
* Hadoop：詳しくは、[この節](../../platform/using/specific-configuration-database.md#configure-access-to-hadoop-3)を参照してください。
* Oracle：詳しくは、[この節](../../platform/using/specific-configuration-database.md#configure-access-to-oracle)を参照してください。
* Netezza：詳しくは、[この節](../../platform/using/specific-configuration-database.md#configure-access-to-netezza)を参照してください。
* Sybase IQ：詳しくは、[この節](../../platform/using/specific-configuration-database.md#configure-access-to-sybase-iq)を参照してください。
* Teradata：詳しくは、[この節](../../platform/using/specific-configuration-database.md#configure-access-to-teradata)を参照してください。
* SAP HANA：詳しくは、[この節](../../platform/using/specific-configuration-database.md)を参照してください。

## ベストプラクティスと推奨事項 {#best-practices-and-recommendations}

FDA オプションは、ワークフローにおいて外部データベースのデータをバッチモードで操作するように設計されています。FDA を単一の操作（パーソナライゼーション、インタラクション、リアルタイム配信など）に使用するなど、別の状況で使用する場合は、実行に際していくつかの注意事項があります。

Adobe Campaign と外部データベースの両方を使用する必要がある操作は、できるだけおこなわないようにします。これは、次のような方法で回避できます。

* Adobe Campaign データベースを外部データベースにエクスポートし、外部データベースからのみ操作を実行して、その結果を Adobe Campaign に再インポートします。
* 外部の Adobe Campaign データベースからデータを収集し、ローカルで操作を実行します。

外部データベースのデータを使用する配信でパーソナライゼーションを実行する場合は、ワークフローで使用するデータを収集して一時テーブルに格納してから、一時テーブルのデータを使用して配信をパーソナライズします。

## 制限事項 {#limitations}

FDA オプションには、使用する外部データベースシステムの制限事項が適用されます。

パフォーマンス上の理由から、配信のパーソナライゼーション、インタラクションモジュール、リアルタイム配信などの単一の操作の実行においては、この機能を使用しないことをお勧めします。
