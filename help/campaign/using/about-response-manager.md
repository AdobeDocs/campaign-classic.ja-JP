---
title: Response Manager について
seo-title: Response Manager について
description: Response Manager について
seo-description: null
page-status-flag: never-activated
uuid: 3087a96d-50fb-488a-9b76-70eb5c67deed
contentOwner: sauviat
products: SG_CAMPAIGN/CLASSIC
audience: campaign
content-type: reference
topic-tags: response-manager
discoiquuid: a4669fee-4512-455f-b495-ebd5a0746b76
translation-type: ht
source-git-commit: 70b143445b2e77128b9404e35d96b39694d55335
workflow-type: ht
source-wordcount: '442'
ht-degree: 100%

---


# Response Manager について{#about-response-manager}

## 目標 {#objectives}

Adobe Campaign には応答管理アプリケーション（Response Manager）が用意されています。これを使用すると、すべての通信チャネル（E メール、モバイル、電話、ダイレクトメール、FAX、代理店、その他）のマーケティングキャンペーンやオファー提案の成功および収益性を測定できます。

## 仮説の概念 {#hypothesis-concept}

配信受信後のターゲットの行動を推測するために、コンタクト日から指定の期間に仮説を設定できます。仮説は、購入と購入の詳細情報を保存する「**トランザクション**」テーブルに基づいて作成されます。

仮説は時間で制限されます。また、コントロール母集団に適用してターゲット母集団と比較することができます。仮説の結果は&#x200B;**指標**&#x200B;で表示されます。指標は、計算完了時に自動的に更新されます。キャンペーンレポートでは、仮説にリンクされた ROI が考慮されます。

また、Response Manager で提供される&#x200B;**レポート**&#x200B;により、売上増加率、利益計算、さらに配信またはオファーの ROI にリンクされた情報を集約できます。

加えて、購入の詳細ラインにより、例として 1 つの特定の製品のみに注目するように仮説を指定できます。

例えば、あるアイテムの宣伝の配信後に、発生する売上高を評価したいとします。配信の翌月にアイテムを少なくとも 1 つ購入したすべての受信者は、このアクションに反応したという仮説を適用します。この仮説に基づいて、どの購入リクエストラインを関連付けるべきかが決定されます。この後、関連付けられた購入リクエストラインを合計し、生じる売上高を計算できます。

>[!CAUTION]
>
>Response Manager は&#x200B;**[!UICONTROL キャンペーン]**&#x200B;のオプションです。使用許諾契約書を確認してください。

配信またはオファーを受け取った受信者全世帯のすべての反応を計算することもできます。

各仮説は単一のトランザクションテーブルにリンクされます。1 つの配信またはオファーを、複数の仮説にリンクすることができます。

## 方法 {#method}

Response Manager の使用を開始する前に、[設定](../../campaign/using/configuration.md)を参照して必要な設定を実行してください。

配信またはオファーで仮説を開始するには、作成する各仮説に使用するテンプレートでコンテキストを定義する必要があります。

測定の仮説を定義および作成するには、以下の手順に従います。

1. 仮説モデルを定義します。[仮説モデルの作成](../../campaign/using/hypothesis-templates.md#creating-a-hypothesis-model)を参照してください。
1. 既存の配信で 1 つまたは複数の仮説を作成します。[キャンペーン配信での仮説の参照](../../campaign/using/creating-hypotheses.md#referencing-a-hypothesis-in-a-campaign-delivery)を参照してください。

   または

   オファーで 1 つまたは複数の仮説を作成します。[オファーの仮説の作成](../../campaign/using/creating-hypotheses.md#creating-a-hypothesis-on-an-offer)を参照してください。

1. 仮説の結果を確認します。[仮説のトラッキング](../../campaign/using/hypothesis-tracking.md)を参照してください。
1. 必要に応じて仮説を再度開始します。[オンザフライでの配信の仮説の作成](../../campaign/using/creating-hypotheses.md#creating-a-hypothesis-on-the-fly-on-a-delivery)を参照してください。

