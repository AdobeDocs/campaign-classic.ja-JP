---
product: campaign
title: 初期設定について
description: 初期設定について
feature: Installation, Configuration
badge-v7-only: label="v7" type="Informative" tooltip="Campaign Classicv7 にのみ適用"
badge-v7-prem: label="オンプレミスおよびハイブリッド" type="Caution" url="https://experienceleague.adobe.com/docs/campaign-classic/using/installing-campaign-classic/architecture-and-hosting-models/hosting-models-lp/hosting-models.html?lang=ja" tooltip="オンプレミスデプロイメントとハイブリッドデプロイメントにのみ適用されます"
audience: installation
content-type: reference
topic-tags: initial-configuration
exl-id: f77ba178-0dfb-4a2e-b33b-971765d42298
source-git-commit: 3a9b21d626b60754789c3f594ba798309f62a553
workflow-type: tm+mt
source-wordcount: '192'
ht-degree: 16%

---

# インスタンスを設定およびデプロイするための主な手順{#about-initial-configuration}



Adobe Campaignのインストールが完了したら、制約と技術的アーキテクチャで効率的に動作するように、インストールを設定する必要があります。 Adobe Campaignインスタンスを設定する手順については、この章で次の順に説明します。

1. インスタンスと関連する接続の作成 ( [インスタンスの作成とログオン](../../installation/using/creating-an-instance-and-logging-on.md).
1. データベースの作成と設定については、 [データベースの作成と設定](../../installation/using/creating-and-configuring-the-database.md).
1. Adobe Campaignサーバーを設定します。を参照してください。 [Campaign サーバーの設定](../../installation/using/configuring-campaign-server.md).
1. インスタンスをデプロイします（を参照）。 [インスタンスのデプロイ](../../installation/using/deploying-an-instance.md).

インスタンスの設定は、プロセス（Web、MTA、wfserver など）を をサーバー上で起動し、e メールを送信するモジュールやトラッキング用モジュールなどを設定します。 各インスタンスに対して、Adobe Campaignプロセスがサーバー上でアクティブ化されます。 詳しくは、[この節](../../installation/using/configuring-campaign-server.md#enabling-processes)を参照してください。

Adobe Campaignの操作を最適化するには、（使用するモジュール、アーキテクチャ、ニーズに応じて）各インスタンスに追加の設定が必要になる場合があります。
