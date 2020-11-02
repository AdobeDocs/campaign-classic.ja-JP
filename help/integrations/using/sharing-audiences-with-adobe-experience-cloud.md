---
title: オーディエンスを Adobe Experience Cloud と共有する
seo-title: オーディエンスを Adobe Experience Cloud と共有する
description: オーディエンスを Adobe Experience Cloud と共有する
seo-description: null
page-status-flag: never-activated
uuid: 24ac3463-69ab-48b4-85e0-4fe1948bf5ed
contentOwner: sauviat
products: SG_CAMPAIGN/CLASSIC
audience: integrations
content-type: reference
topic-tags: audience-sharing
discoiquuid: 8f295058-5a78-4512-9bdf-d5f022457e10
translation-type: tm+mt
source-git-commit: 4b98c23f4120cbea6dd54cd68b61202e74bee3e1
workflow-type: tm+mt
source-wordcount: '248'
ht-degree: 62%

---


# オーディエンスを Adobe Experience Cloud と共有する{#sharing-audiences-with-adobe-experience-cloud}

>[!CAUTION]
>
>Adobe Experience Cloudのソリューションとオーディエンスを共有するには、AdobeIdentity Managementシステムを導入する必要があります。 [IMSの詳細を表示します](../../integrations/using/about-adobe-id.md)。

Adobe Campaignを使用すると、オーディエンスやセグメントをAdobe Experience Cloudのソリューションやコアサービスと共有できます。 次の2つのオプションを使用できます。

1. Adobe Experience PlatformセグメントデータをAdobe Campaignに送信します。 この統合を実装するには、Real-Time Customer Data Platformをキャンペーン(RTCDP)に接続する必要があります。 [詳しくは、この節](https://docs.adobe.com/content/help/ja-JP/experience-platform/rtcdp/destinations/destinations-cat/adobe-destinations/adobe-campaign-destination.html)を参照してください。


1. **Adobe Campaignを** Peopleコアサービス **(** プロファイル&amp;オーディエンスコアサービス ****)またはAdobe Audience Managerと統合します。 統合すると、次のことが可能になります。

   * 共有されたオーディエンスまたはセグメントを、他の Adobe Experience Cloud ソリューションから Adobe Campaign にインポートします。オーディエンスは Adobe Campaign のリストを使用してインポートできます。

   * Adobe Experience Cloud 共有オーディエンスのフォームでリストをエクスポートします。これらのオーディエンスは、お使いの他の Adobe Experience Cloud ソリューションで使用できます。オーディエンスは、ワークフローでターゲティングした後、専用の&#x200B;**[!UICONTROL 共有オーディエンスの更新]**&#x200B;アクティビティを使用してエクスポートできます。

この統合では、2種類のAdobe Experience CloudIDがサポートされます。

* **訪問者 ID**：このタイプの識別子は、Adobe Experience Cloud の訪問者を Adobe Campaign 受信者に紐付けします。
* **宣言済み ID**：このタイプの識別子は、すべてのタイプのデータを Adobe Campaign データベースからの要素に紐付けします。Adobe Campaign では、事前定義された紐付けキーとして示されます。
