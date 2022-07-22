---
product: campaign
title: Response Manager について
description: Response Manager について
exl-id: b5c0e960-2afe-4a98-b82c-d47a74659703
source-git-commit: 381538fac319dfa075cac3db2252a9cc80b31e0f
workflow-type: ht
source-wordcount: '0'
ht-degree: 100%

---

# Campaign Response Manager の基本を学ぶ{#about-response-manager}

![](../../assets/v7-only.svg)

Adobe Campaign では、マーケティングキャンペーンの成功や収益性を測定したり、メール、モバイル、ダイレクトメールなどのあらゆる通信チャネルでオファーを提案したりできる、応答管理アドオンを提供しています。

## 仮説 {#hypothesis-concept}

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

## 実装の手順 {#method}

Response Manager の使用を開始する前に、[設定](configuration.md)を参照して必要な設定を実行してください。

配信またはオファーで仮説を開始するには、作成する各仮説に使用するテンプレートでコンテキストを定義する必要があります。

測定の仮説を定義および作成するには、以下の手順に従います。

1. 仮説モデルを定義します。[詳細情報](hypothesis-templates.md#creating-a-hypothesis-model)
1. 既存の配信に 1 つまたは複数の仮説を作成します。[詳細情報](creating-hypotheses.md#referencing-a-hypothesis-in-a-campaign-delivery)

   または

   オファーで 1 つまたは複数の仮説を作成します。[詳細情報](creating-hypotheses.md#creating-a-hypothesis-on-an-offer)

1. 仮説の結果を確認します。[詳細情報](hypothesis-tracking.md)
1. 必要に応じて仮説を再度開始します。[詳細情報](creating-hypotheses.md#creating-a-hypothesis-on-the-fly-on-a-delivery)
