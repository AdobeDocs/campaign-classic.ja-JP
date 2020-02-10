---
title: マーケティングキャンペーンの設計
seo-title: マーケティングキャンペーンの設計
description: マーケティングキャンペーンの設計
seo-description: null
page-status-flag: never-activated
uuid: e0fd5df6-7516-4ca6-bbdf-243a264d0283
contentOwner: sauviat
products: SG_CAMPAIGN/CLASSIC
audience: campaign
content-type: reference
topic-tags: about-marketing-campaigns
discoiquuid: a9eb6627-2e51-42d0-9b29-5b798bdf5b33
index: y
internal: n
snippet: y
translation-type: tm+mt
source-git-commit: b47dcfa0e4ee2e5e43e7aa14b94e12fd70ff9c2d

---


# マーケティングキャンペーンの設計{#designing-marketing-campaigns}

Adobe Campaign では、コミュニケーションおよびマーケティングキャンペーンを定義、最適化、実行および分析できます。Adobe Campaign により、マーケティング戦略の指示や実行を一元的におこなうことができます。詳しくは、[キャンペーンへのアクセス](../../campaign/using/accessing-campaigns.md)および[キャンペーンの設定](../../campaign/using/setting-up-marketing-campaigns.md)を参照してください。

In addition, the **Marketing Resource Management (MRM)** module lets you control marketing actions in a collaborative mode by providing complete management and real-time tracking of the tasks, budgets and marketing resources involved. マーケティングリソース管理では、社内および社外のプロセス、リソース、マーケティングキャンペーンの管理に加えて、サードパーティ（エージェントや印刷業者など）との関係性も最適化および調整できます。詳しくは、[この節](../../campaign/using/about-marketing-resource-management.md)を参照してください。

>[!NOTE]
>
>Adobe Campaign のコア機能について詳しくは、[はじめに](../../platform/using/about-adobe-campaign-classic.md)の節を参照してください。\
>様々なチャネルを使用した母集団のターゲティング、メッセージのパーソナライズおよびメッセージ配信に関連する機能について詳しくは、[この節](../../delivery/using/communication-channels.md)を参照してください。

## 主な概念 {#core-concepts}

キャンペーンのコンテキストにおける以下の概念を理解しておく必要があります。

* **キャンペーン**

   キャンペーンは、配信、ターゲット設定ルール、コスト、エクスポートファイル、関連ドキュメントなど、マーケティングキャンペーンに関連するすべての要素を集中管理します。各キャンペーンは 1 つのプログラムに関連付けられます。

   For more on this, refer to [Adding a campaign](../../campaign/using/setting-up-marketing-campaigns.md#adding-a-campaign).

* **プログラム**

   プログラムでは、特定のカレンダー期間における開始、勧誘、ロイヤリティなどのマーケティングアクションを定義します。各プログラムには 1 つ以上のキャンペーンが含まれ、各キャンペーンにリンクされているカレンダーに概要が表示されます。

* **プラン**

   マーケティングプランには複数のプログラムを含めることができます。マーケティングプランは 1 つのカレンダー期間にリンクされ、予算が割り当てられています。また、ドキュメントや目標にリンクすることもできます。

   For more on this, refer to [Campaign calendar](../../campaign/using/accessing-marketing-campaigns.md#campaign-calendar).

* **ワークフロー**

   キャンペーンワークフローにはすべてのワークフローと同じアクティビティが含まれますが、ワークフローはキャンペーンに固有です。ワークフローにより、使用可能なすべてのチャネル用の配信を作成して設定できます。

   詳しくは、[この節](../../campaign/using/marketing-campaign-deliveries.md#building-the-main-target-in-a-workflow)を参照してください。

* **目標**

   キャンペーン、プログラムまたはプラン内に一連の目標を記述することができます。目標は、到達すべき定量値です。キャンペーン、プログラムまたはプランの終了時に MRM モジュールを使用して、目標と結果を専用レポートで比較することができます。

* **配信の概要**

   配信の概要は、配信の内容を構造的に記述したものです。すべての配信は、関連するオファー、添付するドキュメント、店舗へのリンクなどを含む配信の概要を参照できます。選択した配信の概要に従って、配信内でオファーを参照できます。

   詳しくは、「配信の概要を介してリンクさ [れたリソースの関連付けと構造化」を参照してください](../../campaign/using/marketing-campaign-deliveries.md#associating-and-structuring-resources-linked-via-a-delivery-outline)。
