---
product: campaign
title: マーケティングキャンペーンの設計と実行
description: マーケティングキャンペーンを定義、最適化、実施、分析します。
role: User
feature: Campaigns
hide: true
hidefromtoc: true
exl-id: 4e0df18f-3623-4dfb-a2f8-ad293dbc4dd5
source-git-commit: 4a7ecd170bd27f43d515da71c212bbdaa306d602
workflow-type: tm+mt
source-wordcount: '431'
ht-degree: 76%

---

# マーケティングキャンペーンの設計と実行{#designing-marketing-campaigns}


[!DNL Adobe Campaign] を使用すると、コミュニケーションおよびマーケティングキャンペーンを定義、最適化、実行および分析できます。 [!DNL Adobe Campaign] は、マーケティング戦略の統一されたオーダーと実行センターのように機能します。 詳細については、[キャンペーンへのアクセス](../../distributed/using/accessing-campaigns.md)および[マーケティングキャンペーンの作成](../../campaign/using/setting-up-marketing-campaigns.md)を参照してください。

また、**マーケティングリソース管理（MRM）**&#x200B;モジュールでは、関連するタスク、予算およびマーケティングリソースの完全な管理とリアルタイムトラッキングにより、マーケティングアクションを協調モードで制御できます。マーケティングリソース管理を使用すると、内部および外部のプロセス、リソースおよびマーケティングキャンペーンの管理を最適化および規制できます。 また、サードパーティとの関係（代理店、プリンターなど）もサポートしています。 詳しくは、[この節](../../mrm/using/about-marketing-resource-management.md)を参照してください。

>[!NOTE]
>
>[!DNL Adobe Campaign] のコア機能について詳しくは、[&#x200B; この節 &#x200B;](../../platform/using/about-adobe-campaign-classic.md) を参照してください。\
>様々なチャネルにおける母集団のターゲティング、メッセージのパーソナライゼーションおよびメッセージ配信に関連する機能について詳しくは、[[!DNL Campaign v8 documentation]](https://experienceleague.adobe.com/docs/campaign/campaign-v8/send/create-message.html?lang=ja){target="_blank"} を参照してください。

![&#x200B; チュートリアルビデオのサムネール &#x200B;](assets/do-not-localize/how-to-video.png) [&#x200B; マーケティングキャンペーンの主要概念をビデオで確認 &#x200B;](#video)

## 主要コンセプト {#core-concepts}

キャンペーンのコンテキストにおける以下の概念を理解しておく必要があります。

* **キャンペーン**

  キャンペーンは、配信、ターゲティングルール、コスト、エクスポートファイル、関連ドキュメントなど、マーケティングキャンペーンに関連するすべての要素を集中管理します。各キャンペーンは 1 つのプログラムに関連付けられます。

  詳しくは、[キャンペーンの追加](../../campaign/using/setting-up-marketing-campaigns.md#adding-a-campaign)を参照してください。

* **プログラム**

  プログラムでは、特定のカレンダー期間におけるローンチ、勧誘、ロイヤルティなどのマーケティングアクションを定義します。各プログラムには 1 つ以上のキャンペーンが含まれ、各キャンペーンにリンクされているカレンダーに概要が表示されます。


* **プラン**

  マーケティングプランには複数のプログラムを含めることができます。マーケティングプランは 1 つのカレンダー期間にリンクされ、予算が割り当てられています。また、ドキュメントや目標にリンクすることもできます。

  詳しくは、[キャンペーンカレンダー](../../campaign/using/accessing-marketing-campaigns.md#campaign-calendar)を参照してください。

* **ワークフロー**

  キャンペーンワークフローにはすべてのワークフローと同じアクティビティが含まれますが、ワークフローはキャンペーンに固有です。ワークフローにより、使用可能なすべてのチャネル用の配信を作成して設定できます。

  詳しくは、[この節](../../campaign/using/marketing-campaign-deliveries.md#building-the-main-target-in-a-workflow)を参照してください。

* **目標**

  キャンペーン、プログラムまたはプラン内に一連の目標を記述することができます。目標は、到達すべき定量値です。キャンペーン、プログラムまたはプランの終了時に MRM モジュールを使用して、目標と結果を専用レポートで比較することができます。

* **配信の概要**

  配信の概要は、配信の内容を構造的に記述したものです。すべての配信は、関連するオファー、添付するドキュメント、店舗へのリンクなどを含む配信の概要を参照できます。選択した配信の概要に従って、配信内でオファーを参照できます。

  詳しくは、[この節](../../campaign/using/marketing-campaign-deliveries.md#associating-and-structuring-resources-linked-via-a-delivery-outline)を参照してください。

## チュートリアル {#video}

このビデオでは、マーケティングキャンペーンの主要概念を紹介します。

>[!VIDEO](https://video.tv.adobe.com/v/35131?quality=12)

その他の [!DNL Campaign Classic] チュートリアルビデオについては、[&#x200B; こちら &#x200B;](https://experienceleague.adobe.com/docs/campaign-classic-learn/tutorials/overview.html?lang=ja) を参照してください。
