---
product: campaign
title: インタラクションとオファー管理
description: 実施要件ルールに基づいて、連絡先に最適なオファーを送信する方法を学ぶ
feature: Interaction, Offers
exl-id: 62b8fdcd-8423-496c-8407-ab89a3a70721
TQID: 'https://experienceleague.adobe.com/yUoaaurDek0SyjlZXodUQw5iruwl4WN5zNYaMaAVTeA'
product_v2:
  - id: dfc56824-e8b9-499e-85d4-21aedb507314
    internal-label: Campaign
  - id: fd6e6e36-54e4-4f1a-96fc-1a750e400d50
    internal-label: Campaign Classic v7
feature_v2:
  - id: b6fcaf36-3bc4-4604-94f3-81b5d3f41ecf
    internal-label: Offer Management
  - id: 65702805-0026-5ca1-843a-144fa79f0883
    internal-label: Interaction
  - id: ea08db70-4682-59a2-9408-9aedd9548e07
    internal-label: Offers
topic_v2:
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
    internal-label: Implementation
  - id: bce87dde-a4ab-44c9-8a18-ad66e4ddb377
    internal-label: Customer experience
source-git-commit: 323ff901668895588a6e9587fa2a8b7804cf2fb4
workflow-type: tm+mt
source-wordcount: '439'
ht-degree: 70%
---
# インタラクションとオファー管理{#interaction-and-offer-management}



インタラクションを使用すると、特定の連絡先（顧客またはターゲット）とのインタラクション中に 1 つまたは複数の調整したオファーを提供して、リアルタイムで応答することができます。 オファーの例としては、簡単な連絡メッセージや、1 つまたは複数の製品やサービスに関する特別オファーなどがあります。

オファーはインバウンド（Web サイトまたはコールセンター）またはアウトバウンド（メール配信、ダイレクトメールまたはマーケティングキャンペーン内の SMS）で連絡先に送信されます。

インバウンドチャネルおよびアウトバウンドチャネルと連動するオファーカタログを作成すると、特定のコンテキストに最適なオファーを選択して連絡先に送信できます。 各受信者向けのオファーの関連度は実施要件ルールに基づいて定義されます。 関連するオファーの中からどのオファーを選択するかは優先度ルールに基づいて決定されます。 オファーのプレゼンテーションルールでは連絡先とのやり取りの履歴が考慮されるので、同じ連絡先に同じオファーが繰り返し送信されることはありません。

インタラクションではオファーのカタログを作成して管理することができ、カタログにリンクされた実施要件ルールとアプリケーションテーマを設定することもできます。 様々なレンダリング関数を活用することで、選択したチャネルに応じてオファーコンテンツをパーソナライズできます。 最後に、シミュレーションモジュールを使用してオファー表示域の影響を計算できます。

Campaign v7 から v8 への移行の一環として、Campaign Classic のドキュメントセットを効率化および再編成しました。 共通機能は、Campaign v8 ドキュメントセットでのみ使用できるようになりました。 インタラクションについて詳しくは、[Campaign v8 ドキュメント &#x200B;](https://experienceleague.adobe.com/ja/docs/campaign/campaign-v8/offers/interaction){target=_blank}を参照してください。

[![画像](../../assets/do-not-localize/learn-more-button.svg)](https://experienceleague.adobe.com/ja/docs/campaign/campaign-v8/offers/interaction){target=_blank}

この節では、Campaign v8 ドキュメントに記載されていないインタラクション機能のみを取り上げます。[&#x200B; オファーシミュレーション &#x200B;](about-offers-simulation.md)、[&#x200B; オファープレゼンテーション &#x200B;](managing-offer-presentation.md)、[&#x200B; オファー承認](approving-and-activating-an-offer.md)、[&#x200B; オファーテンプレート &#x200B;](managing-offer-templates.md)および[詳細設定](using-advanced-parameters.md)。

![](assets/Offermgt2.png)

![](assets/do-not-localize/how-to-video.png) Campaign のインタラクションの機能と用語について詳しくは、[こちらのビデオ](https://helpx.adobe.com/jp/campaign/classic/how-to/acs-overview.html?playlist=/ccx/v1/collection/product/campaign/classic/segment/digital-marketers/explevel/intermediate/applaunch/get-started/collection.ccx.js&ref=helpx.adobe.com)をご覧ください。

## 関連トピック

| 便利なページ | その他のリソース |
|---|---|
| [&#x200B; インタラクションの実装手順](https://experienceleague.adobe.com/ja/docs/campaign/campaign-v8/offers/interaction){target="_blank"} （Campaign v8 ドキュメント） | [オファー配分のテスト](../../interaction/using/about-offers-simulation.md) |
| [&#x200B; ライブ/デザイン環境](https://experienceleague.adobe.com/ja/docs/campaign/campaign-v8/offers/interaction-settings/interaction-env){target="_blank"} （Campaign v8 ドキュメント） | [電子メールにオファーを追加する](https://experienceleague.adobe.com/ja/docs/campaign/campaign-v8/offers/interaction-send-offers){target="_blank"} （Campaign v8 ドキュメント） |
| [&#x200B; オファースペースの作成](https://experienceleague.adobe.com/ja/docs/campaign/campaign-v8/offers/interaction-settings/interaction-offer-spaces){target="_blank"} （Campaign v8 ドキュメント） | [使用例：Web サイトにオファーを追加する](../../interaction/using/offers-on-an-inbound-channel.md) |
