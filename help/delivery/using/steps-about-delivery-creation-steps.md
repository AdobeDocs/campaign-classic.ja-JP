---
product: campaign
title: Adobe Campaign の配信作成手順について
description: Adobe Campaign の配信作成の主な手順を確認する
feature: Channel Configuration
role: User
hide: true
exl-id: 0188c3fe-8176-4904-8505-c47a72c20fcc
TQID: https://experienceleague.adobe.com/r1Fnouqf-4hqCJ9jYqWI4pzNhqP0-XZBUHoZQr65DGI
product_v2:
  - id: dfc56824-e8b9-499e-85d4-21aedb507314
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
feature_v2:
  - id: b631758a-142d-425f-b9aa-f756d85cb979
  - id: c858a28b-ea19-49b0-8d48-828717fad89c
subfeature_v2:
  - id: e95a583b-fcfa-4524-8666-46a29c828119
  - id: c8da4fdd-eb94-4751-a43c-f82733fb2d6e
  - id: d5bbe3da-ba85-4242-817e-54f7c4b943e0
  - id: f4da0e76-df77-451e-ad61-21afb7bd8810
source-git-commit: 38eab6b8da73163e4476e91c0ef73f25c3f57546
workflow-type: ht
source-wordcount: 186
ht-degree: 100%

---

# 配信作成手順について {#about-delivery-creation}

配信を作成する際の主な手順を次に示します。

1. **配信の作成と識別** 詳しくは、[Campaign v8 ドキュメント](https://experienceleague.adobe.com/docs/campaign/campaign-v8/send/create-message.html?lang=ja#create-the-delivery){target="_blank"}を参照してください。

1. **配信コンテンツの定義** 配信コンテンツ定義は、各チャネル専用です。 詳しくは、該当する節を参照してください。

   * [メールチャネル](defining-the-email-content.md)
   * [SMS チャネル](sms-create.md#defining-the-sms-content)
   * [ダイレクトメールチャネル](defining-the-direct-mail-content.md)
   * [モバイルアプリケーションチャネル](about-mobile-app-channel.md)

1. **ターゲット母集団の定義** 詳しくは、[Campaign v8 ドキュメント](https://experienceleague.adobe.com/docs/campaign/campaign-v8/send/create-message#target-population.html?lang=ja){target="_blank"}を参照してください。

1. **配信の送信** [詳細を表示](steps-sending-the-delivery.md)

1. **配信の監視**（トラッキング、強制隔離、レポートなど） 詳しくは、[配信の監視](about-delivery-monitoring.md)および[メッセージトラッキング](https://experienceleague.adobe.com/ja/docs/campaign/campaign-v8/analytics/tracking/tracking){target="_blank"}の節を参照してください。

>[!NOTE]
>
>この章で説明する手順では、外部配信の場合（[Campaign v8 ドキュメント](https://experienceleague.adobe.com/docs/campaign/campaign-v8/send/create-message.html?lang=ja#selecting-external-recipients){target="_blank"}を参照）を除き、すべてのターゲット受信者とそのプロファイルがデータベース内に格納されていることを想定しています。
