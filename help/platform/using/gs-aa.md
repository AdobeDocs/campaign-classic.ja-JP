---
product: campaign
title: Adobe CampaignとAdobe分析の使用
description: Adobe CampaignとAdobe Analyticsの操作
feature: Analytics Integration
role: User, Admin
level: Beginner
exl-id: 985cf088-7546-4875-8e11-cafe5bd3e323
source-git-commit: b666535f7f82d1b8c2da4fbce1bc25cf8d39d187
workflow-type: tm+mt
source-wordcount: '184'
ht-degree: 50%

---

# Adobe CampaignとAdobe Analyticsの操作 {#adobe-analytics-connector-gs}

Adobe Analytics Connectorを使用すると、Adobe Campaign と Adobe Analytics が **[!UICONTROL Web 分析コネクタ]**&#x200B;パッケージを介してやり取りできます。 キャンペーン後のユーザー行動に関するデータをセグメントの形式で Adobe Campaign に送信します。逆に、Adobe Campaign から配信されたキャンペーンの指標と属性を Adobe Analytics に送信します。

## ガードレールと前提条件 {#adobe-analytics-connector-guardrails}

Adobe CampaignとAdobe Analytics コネクタの使用を開始する前に、次のガードレールと前提条件を考慮してください。

* この統合には、AdobeIdentity Management System （IMS）を使用した Campaign への接続が必要です。 [詳細情報](../../integrations/using/about-adobe-id.md)。

* Adobe Analytics Connector は、トランザクションメッセージ（Message Center）との互換性はありません。

* 専用パッケージを使用して、Web 分析コネクタアドオンをお使いの環境にインストールする必要があります。

   * ハイブリッド実装およびオンプレミス実装の場合は、[このページ](../../platform/using/adobe-analytics-provisioning.md)で説明されているプロビジョニング手順に必ず従ってください。
   * ホステルまたは管理対象Cloud Serviceのユーザーは、Adobeに連絡して、Campaign をAdobe Experience Cloudのサービスやソリューションと統合してください。


## 設定と使用 {#adobe-analytics-connector-usage}

でAdobe CampaignとAdobe Analyticsを使用する方法を説明します [Adobe Campaign v8 ドキュメント](https://experienceleague.adobe.com/en/docs/campaign/campaign-v8/connect/ac-aa){target="_blank"}.
