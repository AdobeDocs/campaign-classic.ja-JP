---
product: campaign
title: Adobe Campaign と Adobe Analytics の連携
description: Adobe Campaign と Adobe Analytics の連携
feature: Analytics Integration
role: User, Admin
level: Beginner
exl-id: 985cf088-7546-4875-8e11-cafe5bd3e323
TQID: https://experienceleague.adobe.com/YuvP0m31wL-WlocUXU3rWovOiwLiA5XrEsnBLlW3nY8
product_v2: id: dfc56824-e8b9-499e-85d4-21aedb507314
feature_v2: id: a075b2c1-7748-4328-b7f6-343aa314616aid: d5ef99fa-df0c-4153-bf94-105ad0724167
role_v2: id: b69b2659-1057-424e-8fc5-ed9e016dc554id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
level_v2: id: e8ccd51f-da0d-4e3b-939b-e30d5ebb1ea5
topic_v2: id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
source-git-commit: 4c295c0dabae8aba298390a3da2422a3fa1219f9
workflow-type: tm+mt
source-wordcount: 212
ht-degree: 100%

---

# Adobe Campaign と Adobe Analytics の連携 {#adobe-analytics-connector-gs}

Adobe Analytics Connector を使用すると、Adobe Campaign と Adobe Analytics が **[!UICONTROL Web 分析コネクタ]**&#x200B;パッケージを介してやり取りできます。 キャンペーン後のユーザー行動に関するデータをセグメントの形式で Adobe Campaign に送信します。 逆に、Adobe Campaign から配信されたキャンペーンの指標と属性を Adobe Analytics に送信します。

## ガードレールと前提条件 {#adobe-analytics-connector-guardrails}

Adobe Campaign-Adobe Analytics コネクタの使用を開始する前に、次のガードレールと前提条件を考慮してください。

* この統合には、Adobe Identity Management System（IMS）を使用して Campaign に接続する必要があります。 [詳細情報](../../integrations/using/about-adobe-id.md)。

* Adobe Analytics Connector は、トランザクションメッセージ（Message Center）との互換性はありません。

* 専用パッケージを使用して、web 分析コネクタアドオンをお使いの環境にインストールする必要があります。

   * ハイブリッド実装およびオンプレミス実装の場合は、この[ページ](adobe-analytics-provisioning.md)で説明されているプロビジョニング手順に必ず従ってください。
   * Hoster ユーザーまたは Managed Cloud Services ユーザーとして、Campaign を Adobe Experience Cloud サービスおよびソリューションに接続するには、アドビにお問い合わせください。


## 設定と使用法 {#adobe-analytics-connector-usage}

この統合を有効にするには、[このページ](oauth-technical-account.md)で説明されているように、アドビのテクニカルアカウントを作成する必要があります。

Adobe Campaign と Adobe Analytics の連携について詳しくは、[Adobe Campaign v8 ドキュメント](https://experienceleague.adobe.com/ja/docs/campaign/campaign-v8/connect/ac-aa){target="_blank"}を参照してください。
