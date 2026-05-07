---
product: campaign
title: 初期設定について
description: 初期設定について
feature: Installation, Configuration
badge-v7-prem: label="オンプレミス／ハイブリッドのみ" type="Caution" url="https://experienceleague.adobe.com/docs/campaign-classic/using/installing-campaign-classic/architecture-and-hosting-models/hosting-models-lp/hosting-models.html?lang=ja" tooltip="オンプレミスデプロイメントとハイブリッドデプロイメントにのみ適用されます"
audience: installation
content-type: reference
topic-tags: initial-configuration
exl-id: f77ba178-0dfb-4a2e-b33b-971765d42298
source-git-commit: 14ba450ebff9bba6a36c0df07d715b7279604222
workflow-type: tm+mt
source-wordcount: '197'
ht-degree: 19%

---

# インスタンスを設定してデプロイするための主な手順{#about-initial-configuration}



Adobe Campaignのインストールが完了したら、制約や技術的なアーキテクチャを考慮して効率的に動作するように設定する必要があります。 Adobe Campaign インスタンスを設定する手順については、この章で次の順序で詳しく説明します。

1. インスタンスと関連する接続を作成します。[ インスタンスの作成とログオン ](../../installation/using/creating-an-instance-and-logging-on.md)を参照してください。
1. データベースの作成と設定については、[ データベースの作成と設定](../../installation/using/creating-and-configuring-the-database.md)を参照してください。
1. Adobe Campaign サーバーを設定します。[Campaign サーバー設定](../../installation/using/configuring-campaign-server.md)を参照してください。
1. インスタンスをデプロイします。[ インスタンスのデプロイ ](../../installation/using/deploying-an-instance.md)を参照してください。

インスタンスを設定すると、プロセス（web、mta、wfserverなど）が有効になります。 サーバーで開始し、メール送信、トラッキングなどのモジュールを設定します。各インスタンスについて、Adobe Campaign プロセスはサーバー上でアクティブ化されます。 詳しくは、[この節](../../installation/using/configuring-campaign-server.md#enabling-processes)を参照してください。

Adobe Campaignの運用を最適化するには、各インスタンス（使用するモジュール、アーキテクチャ、ニーズに応じて）に追加の設定が必要になる場合があります。
