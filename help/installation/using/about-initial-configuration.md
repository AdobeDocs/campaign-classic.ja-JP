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
source-wordcount: '178'
ht-degree: 10%

---

# インスタンスを設定およびデプロイするための主な手順{#about-initial-configuration}



Adobe Campaignのインストールが完了したら、制約や技術的アーキテクチャに合わせて効率的に動作するように設定する必要があります。 この章では、Adobe Campaign インスタンスを次の順序で設定する手順について詳しく説明します。

1. インスタンスおよび関連する接続を作成します。[&#x200B; インスタンスの作成およびログオン &#x200B;](../../installation/using/creating-an-instance-and-logging-on.md) を参照してください。
1. データベースを作成および設定します。[&#x200B; データベースの作成および設定 &#x200B;](../../installation/using/creating-and-configuring-the-database.md) を参照してください。
1. Campaign サーバーを設定します。[Adobe Campaign サーバーの設定 &#x200B;](../../installation/using/configuring-campaign-server.md) を参照してください。
1. インスタンスをデプロイします。[&#x200B; インスタンスのデプロイ &#x200B;](../../installation/using/deploying-an-instance.md) を参照してください。

インスタンスを設定すると、プロセス（web、mta、wfserver など）が有効になります サーバーで起動し、メール送信やトラッキングなどのモジュールを設定します。 インスタンスごとに、サーバー上でAdobe Campaign プロセスがアクティブ化されます。 詳しくは、[この節](../../installation/using/configuring-campaign-server.md#enabling-processes)を参照してください。

Adobe Campaignの処理を最適化するために、各インスタンス（使用するモジュール、アーキテクチャおよびニーズに応じて）に追加の設定が必要になる場合があります。
