---
product: campaign
title: 初期設定について
description: 初期設定について
feature: Installation, Configuration
badge-v7-prem: label="On-premise/hybrid only" type="Caution" url="https://experienceleague.adobe.com/docs/campaign-classic/using/installing-campaign-classic/architecture-and-hosting-models/hosting-models-lp/hosting-models.html?lang=ja" tooltip="Applies to on-premise and hybrid deployments only"
audience: installation
content-type: reference
topic-tags: initial-configuration
exl-id: f77ba178-0dfb-4a2e-b33b-971765d42298
TQID: 'https://experienceleague.adobe.com/rQT-wcpjGzyYfEV3thGlY0WD7Po-A08yD0pGMr13p7s'
product_v2:
  - id: dfc56824-e8b9-499e-85d4-21aedb507314
    internal-label: Campaign
  - id: fd6e6e36-54e4-4f1a-96fc-1a750e400d50
    internal-label: Campaign Classic v7
feature_v2:
  - id: c5474392-5419-4296-9e41-f6f4ce4f6e9b
    internal-label: Administration
subfeature_v2:
  - id: e656c701-3899-4db3-989c-de0980ddfffa
    internal-label: Installation
  - id: a14877cc-63b1-41d9-bf0b-5f97cadd0417
    internal-label: Configuration guidelines
source-git-commit: a43e591a565a18d79f583d975e3e812c5435b0c0
workflow-type: tm+mt
source-wordcount: '185'
ht-degree: 14%
---
# インスタンスを設定してデプロイするための主な手順{#about-initial-configuration}



Adobe Campaignのインストールが完了したら、制約や技術的なアーキテクチャを考慮して効率的に動作するように設定する必要があります。 Adobe Campaign インスタンスを設定する手順については、この章で次の順序で詳しく説明します。

1. インスタンスと関連する接続を作成します。[&#x200B; インスタンスの作成とログオン &#x200B;](../../installation/using/creating-an-instance-and-logging-on.md)を参照してください。
1. データベースの作成と設定については、[&#x200B; データベースの作成と設定](../../installation/using/creating-and-configuring-the-database.md)を参照してください。
1. Adobe Campaign サーバーを設定します。[Campaign サーバー設定](../../installation/using/configuring-campaign-server.md)を参照してください。
1. インスタンスをデプロイします。[&#x200B; インスタンスのデプロイ &#x200B;](../../installation/using/deploying-an-instance.md)を参照してください。

インスタンスを設定すると、プロセス（web、mta、wfserverなど）が有効になります。 サーバーで開始し、メール送信、トラッキングなどのモジュールを設定します。各インスタンスについて、Adobe Campaign プロセスはサーバー上でアクティブ化されます。 詳しくは、[この節](../../installation/using/configuring-campaign-server.md#enabling-processes)を参照してください。

Adobe Campaignの運用を最適化するには、各インスタンス（使用するモジュール、アーキテクチャ、ニーズに応じて）に追加の設定が必要になる場合があります。
