---
product: campaign
title: マーケティングキャンペーンについて
description: マーケティングキャンペーンを定義、最適化、実行、分析します。
role: User
feature: Campaigns
exl-id: 07cfa2b3-4e70-437a-ad5f-15fbfe717d5c
source-git-commit: dd6bcb16fe41b6a3f1e3f5aaf2f753b29ad4bc1d
workflow-type: tm+mt
source-wordcount: '296'
ht-degree: 42%

---

# マーケティングキャンペーンの調整{#designing-marketing-campaigns}

Adobe Campaign が提供する一連のソリューションを使用すると、オンラインとオフラインのすべてのチャネルで、キャンペーンをパーソナライズして配信することができます。マーケティングキャンペーンの作成、設定、実施、分析などを行うことができます。すべてのマーケティングキャンペーンを統合コントロールセンターから管理できます。

キャンペーンには、アクション（配信）とプロセス（ファイルのインポートまたは抽出）だけでなく、マーケティングドキュメントや配信の概要といったリソースも含まれます。これらはマーケティングキャンペーンで使用されます。キャンペーンはプログラムの一部で、プログラムは 1 つのキャンペーンプランに含まれます。

キャンペーン管理について詳しくは、[Campaign v8 ドキュメント](https://experienceleague.adobe.com/docs/campaign/campaign-v8/campaigns/campaigns.html?lang=ja){target=_blank}を参照してください。

![](assets/do-not-localize/campaign.jpg){width="40%"}

キャンペーン管理に関連する主な手順を説明します。

* [ 基本を学ぶ ](https://experienceleague.adobe.com/docs/campaign/automation/campaign-orchestration/set-up-campaigns.html?lang=ja){target=_blank}:Adobe Campaignでマーケティングキャンペーンを作成および実行する方法を手順を追って説明します。

* [ 最初のキャンペーンの作成 ](https://experienceleague.adobe.com/docs/campaign/automation/campaign-orchestration/marketing-campaign-create.html?lang=ja){target=_blank}：キャンペーンを調整するロジックをスケジュールおよび設定する方法について説明します。 キャンペーンは、配信、ターゲティングルール、費用、出力ファイル、関連ドキュメントなど、マーケティングキャンペーンに関連するすべての要素を 1 つにまとめたものです。

* [ キャンペーンでのメッセージの送信 ](https://experienceleague.adobe.com/docs/campaign/automation/campaign-orchestration/marketing-campaign-deliveries.html?lang=ja){target=_blank}：キャンペーンでクロスチャネル配信を調整します。パーソナライズされたメール、SMS、プッシュ通知およびアプリ内メッセージを通じて、Adobe Campaignとのコミュニケーションを効率化します。

![](assets/do-not-localize/add-on.jpg){width="40%"}

キャンペーン管理には、次の 3 つのアドオンを使用できます。

* [ キャンペーンの最適化 ](https://experienceleague.adobe.com/docs/campaign/automation/campaign-optimization/campaign-typologies.html?lang=ja){target=_blank}：このモジュールでは、配信の送信を制御、フィルタリングおよび監視できます。 このテストにより、企業のコミュニケーションポリシーに準拠し、顧客のニーズと期待に応える最適なメッセージを送信できます。

* [ マーケティングリソース管理 ](https://experienceleague.adobe.com/docs/campaign/automation/mrm/about-marketing-resource-management.html?lang=ja){target=_blank}：このモジュールを使用すると、関係するタスク、予算およびマーケティングリソースの完全な管理とリアルタイムトラッキングにより、マーケティングアクションを協調的に制御できます。

* [ 分散型マーケティング ](https://experienceleague.adobe.com/docs/campaign/automation/distributed-marketing/about-distributed-marketing.html?lang=ja){target=_blank}：このモジュールでは、関係するタスク、予算およびマーケティングリソースの完全な管理とリアルタイムトラッキングにより、マーケティングアクションを協調的に制御できます。

<!--

Adobe Campaign lets you define, optimize, execute and analyze communications and marketing campaigns. Adobe Campaign acts like a unified order and execution center for marketing strategies. For more on this, refer to [Access campaigns](../../distributed/using/accessing-campaigns.md) and [Create marketing campaigns](../../campaign/using/setting-up-marketing-campaigns.md).

In addition, the **Marketing Resource Management (MRM)** module lets you control marketing actions in a collaborative mode by providing complete management and real-time tracking of the tasks, budgets and marketing resources involved. The Marketing Resource Management lets you optimize and regulate the management of internal and external processes, resources and marketing campaigns, as well as third party relations (agencies, printers, etc.). For more on this, refer to [this section](../../mrm/using/about-marketing-resource-management.md).

>[!NOTE]
>
>For more on the Adobe Campaign core functionalities, refer t [this section](../../platform/using/about-adobe-campaign-classic.md) section.  
>Capabilities related to population targeting, message personalization and message delivery on the various channels are detailed in [this section](../../delivery/using/steps-about-delivery-creation-steps.md).

![](assets/do-not-localize/how-to-video.png) [Discover marketing campaigns keys concepts in video](#video)

## Core concepts {#core-concepts}

The following concepts need to be known in the context of Campaign:

* **Campaign**

  A campaign centralizes all the elements related to a marketing campaign: deliveries, targeting rules, costs, export files, related documents, etc. Each campaign is attached to a program.

  For more on this, refer to [Adding a campaign](../../campaign/using/setting-up-marketing-campaigns.md#adding-a-campaign).

* **Program**

  A program lets you define marketing actions for a calendar period: launch, canvassing, loyalty, etc. Each program contains campaigns linked to a calendar, which provides an overall view.

* **Plan**

  The marketing plan can contain multiple programs. It is linked to a calendar period, has an allocated budget and can also be linked up to documents and objectives.

  For more on this, refer to [Campaign calendar](../../campaign/using/accessing-marketing-campaigns.md#campaign-calendar).

* **Workflow**

  A campaign workflow contains the same activities as for all workflows but is specific to the campaign. It enables you to create and configure deliveries for all available channels.

  For more on this, refer to [this section](../../campaign/using/marketing-campaign-deliveries.md#building-the-main-target-in-a-workflow).

* **Objectives**

  Within the campaign, program or plan, you can state a list of objectives. These are quantified values to be reached. At the end of the campaign, program or plan, the MRM module lets you compare the objectives and results in dedicated reports.

* **Delivery outline**

  A delivery outline is a structured description of a delivery. Every delivery can refer to a delivery outline which contains, for example, the related offers, documents to be attached, or a link to stores. An offer can be referenced in the delivery according to the delivery outline selected.

  For more on this, refer to [this section](../../campaign/using/marketing-campaign-deliveries.md#associating-and-structuring-resources-linked-via-a-delivery-outline).

## Tutorial {#video}

This video presents the key concepts of marketing campaigns.

>[!VIDEO](https://video.tv.adobe.com/v/35131?quality=12)

Additional Campaign Classic how-to videos are available [here](https://experienceleague.adobe.com/docs/campaign-classic-learn/tutorials/overview.html).

-->