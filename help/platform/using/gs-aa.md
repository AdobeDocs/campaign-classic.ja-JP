---
product: campaign
title: Adobe CampaignとAdobe分析の操作
description: Adobe CampaignとAdobe Analyticsの使用
badge-v7-only: label="v7" type="Informative" tooltip="Campaign Classic v7 にのみ適用されます"
feature: Analytics Integration
role: User, Admin
level: Beginner
source-git-commit: 59156851156338c9462781d31ce81a651362f2da
workflow-type: tm+mt
source-wordcount: '191'
ht-degree: 51%

---

# Adobe CampaignとAdobe Analyticsの使用 {#adobe-analytics-connector-gs}

Adobe Analytics Connectorを使用すると、Adobe Campaign と Adobe Analytics が **[!UICONTROL Web 分析コネクタ]**&#x200B;パッケージを介してやり取りできます。 キャンペーン後のユーザー行動に関するデータをセグメントの形式で Adobe Campaign に送信します。逆に、Adobe Campaign から配信されたキャンペーンの指標と属性を Adobe Analytics に送信します。

## ガードレールと前提条件 {#adobe-analytics-connector-guardrails}

Adobe Campaign-Adobe Analyticsコネクタの使用を開始する前に、次のガードレールと前提条件を考慮します。

* この統合では、AdobeIdentity Management System(IMS) を使用して Campaign に接続する必要があります。 [詳細情報](../../integrations/using/about-adobe-id.md)。

* Adobe Analytics Connector は、トランザクションメッセージ（Message Center）との互換性はありません。

* 専用パッケージを使用して、Web 分析コネクタアドオンをお使いの環境にインストールする必要があります。

   * ハイブリッド実装およびオンプレミス実装の場合は、[このページ](../../platform/using/adobe-analytics-provisioning.md)で説明されているプロビジョニング手順に必ず従ってください。
   * ホスターまたは管理Cloud Serviceのユーザーが Campaign をAdobe Experience Cloudのサービスおよびソリューションに接続するには、Adobeにお問い合わせください。


## 設定と使用方法 {#adobe-analytics-connector-usage}

でAdobe CampaignとAdobe Analyticsを使用する方法を学ぶ [Adobe Campaign v8 ドキュメント](https://experienceleague.adobe.com/en/docs/campaign/campaign-v8/connect/ac-aa){target="_blank"}.

