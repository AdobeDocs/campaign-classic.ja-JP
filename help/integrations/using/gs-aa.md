---
product: campaign
title: Adobe Campaign と Adobe Analytics の連携
description: Adobe Campaign と Adobe Analytics の連携
feature: Analytics Integration
role: User, Admin
level: Beginner
exl-id: 985cf088-7546-4875-8e11-cafe5bd3e323
source-git-commit: a38d53f4b37aadbc53446b5e399af2eae56c12af
workflow-type: tm+mt
source-wordcount: '200'
ht-degree: 84%

---

# Adobe Campaign と Adobe Analytics の連携 {#adobe-analytics-connector-gs}

Adobe Analytics Connector を使用すると、Adobe Campaign と Adobe Analytics が **[!UICONTROL Web 分析コネクタ]**&#x200B;パッケージを介してやり取りできます。キャンペーン後のユーザー行動に関するデータをセグメントの形式で Adobe Campaign に送信します。逆に、Adobe Campaign から配信されたキャンペーンの指標と属性を Adobe Analytics に送信します。

## ガードレールと前提条件 {#adobe-analytics-connector-guardrails}

Adobe Campaign-Adobe Analytics コネクタの使用を開始する前に、次のガードレールと前提条件を考慮してください。

* この統合には、Adobe Identity Management System（IMS）を使用して Campaign に接続する必要があります。[詳細情報](../../integrations/using/about-adobe-id.md)。

* Adobe Analytics Connector は、トランザクションメッセージ（Message Center）との互換性はありません。

* 専用パッケージを使用して、web 分析コネクタアドオンをお使いの環境にインストールする必要があります。

   * ハイブリッド実装およびオンプレミス実装の場合は、次に説明するプロビジョニング手順に必ず従ってください [ページ](adobe-analytics-provisioning.md).
   * Hoster ユーザーまたは Managed Cloud Services ユーザーとして、Campaign を Adobe Experience Cloud サービスおよびソリューションに接続するには、アドビにお問い合わせください。


## 設定と使用法 {#adobe-analytics-connector-usage}

この統合を有効にするには、に説明されているとおりにAdobeのテクニカルアカウントを作成する必要があります。 [このページ](oauth-technical-account.md).

Adobe Campaign と Adobe Analytics の連携について詳しくは、[Adobe Campaign v8 ドキュメント](https://experienceleague.adobe.com/ja/docs/campaign/campaign-v8/connect/ac-aa){target="_blank"}を参照してください。
