---
product: campaign
title: マーケティングキャンペーンの設計と実行
description: マーケティング施策を定義、最適化、実行、分析
role: User
feature: Campaigns
hide: true
exl-id: 4e0df18f-3623-4dfb-a2f8-ad293dbc4dd5
source-git-commit: 720a5f4edf534788f7fd143a476c25e58a6f1586
workflow-type: tm+mt
source-wordcount: '453'
ht-degree: 81%

---


# マーケティングキャンペーンの設計と実行{#designing-marketing-campaigns}

[!DNL Adobe Campaign]では、コミュニケーションおよびマーケティング キャンペーンを定義、最適化、実行および分析できます。 [!DNL Adobe Campaign]は、マーケティング戦略のための統一された注文と実行センターのような役割を果たします。 詳細については、[キャンペーンへのアクセス](../../distributed/using/accessing-campaigns.md)および[マーケティングキャンペーンの作成](../../campaign/using/setting-up-marketing-campaigns.md)を参照してください。

また、**マーケティングリソース管理（MRM）**&#x200B;モジュールでは、関連するタスク、予算およびマーケティングリソースの完全な管理とリアルタイムトラッキングにより、マーケティングアクションを協調モードで制御できます。 マーケティングリソース管理では、社内外のプロセス、リソース、マーケティング施策の管理を最適化および規制できます。 また、サードパーティの関係（代理店、プリンターなど）もサポートしています。 詳しくは、[この節](../../mrm/using/about-marketing-resource-management.md)を参照してください。

>[!NOTE]
>
>[!DNL Adobe Campaign]のコア機能について詳しくは、[この節](../../platform/using/about-adobe-campaign-classic.md)を参照してください。
>
>様々なチャネルでの母集団のターゲティング、メッセージパーソナライゼーションおよびメッセージ配信に関連する機能について詳しくは、[Campaign v8 ドキュメント](https://experienceleague.adobe.com/docs/campaign/campaign-v8/send/create-message.html?lang=ja){target="_blank"}を参照してください。


![&#x200B; ハウツー動画のサムネイル &#x200B;](assets/do-not-localize/how-to-video.png) [動画でマーケティングキャンペーンの主要な概念を見つける](#video)

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

追加の[!DNL Campaign Classic]のハウツー動画は[こちら](https://experienceleague.adobe.com/docs/campaign-classic-learn/tutorials/overview.html?lang=ja)から利用できます。
