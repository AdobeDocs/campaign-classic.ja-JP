---
product: campaign
title: マーケティングキャンペーンの設計と実行
description: マーケティングキャンペーンを定義、最適化、実行、分析します
role: User
feature: Campaigns
hide: true
exl-id: 4e0df18f-3623-4dfb-a2f8-ad293dbc4dd5
TQID: https://experienceleague.adobe.com/IafzeMWF-WfGa3h70HsX6OXZIUeu47PJlqsliA8T5EM
product_v2:
  - id: dfc56824-e8b9-499e-85d4-21aedb507314
feature_v2:
  - id: a075b2c1-7748-4328-b7f6-343aa314616a
  - id: afa4204e-6d08-4e29-bc35-26aafb656d48
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
topic_v2:
  - id: e0eb8757-182f-49f3-94a4-1587d16f5094
subfeature_v2:
  - id: f863efa9-030c-4466-a2b8-a52aea6b722c
source-git-commit: c35995a47788db080636c66827a4bd6dc98806cf
workflow-type: tm+mt
source-wordcount: 453
ht-degree: 100%

---

# マーケティングキャンペーンの設計と実行{#designing-marketing-campaigns}

[!DNL Adobe Campaign] では、コミュニケーションおよびマーケティングキャンペーンを定義、最適化、実行および分析できます。 [!DNL Adobe Campaign] により、マーケティング戦略の指示や実行を一元的に行うことができます。 詳細については、[キャンペーンへのアクセス](../../distributed/using/accessing-campaigns.md)および[マーケティングキャンペーンの作成](../../campaign/using/setting-up-marketing-campaigns.md)を参照してください。

また、**マーケティングリソース管理（MRM）**&#x200B;モジュールでは、関連するタスク、予算およびマーケティングリソースの完全な管理とリアルタイムトラッキングにより、マーケティングアクションを協調モードで制御できます。 マーケティングリソース管理では、社内および社外のプロセス、リソース、マーケティングキャンペーンの管理を最適化および調整できます。 また、サードパーティ（エージェントや印刷業者など）との関係性もサポートしています。 詳しくは、[この節](../../mrm/using/about-marketing-resource-management.md)を参照してください。

>[!NOTE]
>
>[!DNL Adobe Campaign] コア機能について詳しくは、[この節](../../platform/using/about-adobe-campaign-classic.md)を参照してください。
>
>様々なチャネルでの母集団のターゲティング、メッセージパーソナライゼーションおよびメッセージ配信に関連する機能について詳しくは、[Campaign v8 ドキュメント](https://experienceleague.adobe.com/docs/campaign/campaign-v8/send/create-message.html?lang=ja){target="_blank"}を参照してください。


![チュートリアルビデオのサムネイル](assets/do-not-localize/how-to-video.png) [マーケティングキャンペーンの主要概念について詳しくは、ビデオを参照してください](#video)

## 主要コンセプト {#core-concepts}

キャンペーンのコンテキストにおける以下の概念を理解しておく必要があります。

* **キャンペーン**

  キャンペーンは、配信、ターゲティングルール、コスト、エクスポートファイル、関連ドキュメントなど、マーケティングキャンペーンに関連するすべての要素を集中管理します。各キャンペーンは 1 つのプログラムに関連付けられます。

  詳しくは、[キャンペーンの追加](../../campaign/using/setting-up-marketing-campaigns.md#adding-a-campaign)を参照してください。

* **プログラム**

  プログラムでは、特定のカレンダー期間におけるローンチ、勧誘、ロイヤルティなどのマーケティングアクションを定義します。各プログラムには 1 つ以上のキャンペーンが含まれ、各キャンペーンにリンクされているカレンダーに概要が表示されます。

* **プラン**

  マーケティングプランには複数のプログラムを含めることができます。 マーケティングプランは 1 つのカレンダー期間にリンクされ、予算が割り当てられています。また、ドキュメントや目標にリンクすることもできます。

  詳しくは、[キャンペーンカレンダー](../../campaign/using/accessing-marketing-campaigns.md#campaign-calendar)を参照してください。

* **ワークフロー**

  キャンペーンワークフローにはすべてのワークフローと同じアクティビティが含まれますが、ワークフローはキャンペーンに固有です。 ワークフローにより、使用可能なすべてのチャネル用の配信を作成して設定できます。

  詳しくは、[この節](../../campaign/using/marketing-campaign-deliveries.md#building-the-main-target-in-a-workflow)を参照してください。

* **目標**

  キャンペーン、プログラムまたはプラン内に一連の目標を記述することができます。 目標は、到達すべき定量値です。 キャンペーン、プログラムまたはプランの終了時に MRM モジュールを使用して、目標と結果を専用レポートで比較することができます。

* **配信の概要**

  配信の概要は、配信の内容を構造的に記述したものです。 すべての配信は、関連するオファー、添付するドキュメント、店舗へのリンクなどを含む配信の概要を参照できます。 選択した配信の概要に従って、配信内でオファーを参照できます。

  詳しくは、[この節](../../campaign/using/marketing-campaign-deliveries.md#associating-and-structuring-resources-linked-via-a-delivery-outline)を参照してください。

## チュートリアル {#video}

このビデオでは、マーケティングキャンペーンの主要概念を紹介します。

>[!VIDEO](https://video.tv.adobe.com/v/326573?captions=jpn&quality=12)

[!DNL Campaign Classic] に関するその他のチュートリアルビデオは[こちら](https://experienceleague.adobe.com/docs/campaign-classic-learn/tutorials/overview.html?lang=ja)で参照できます。

