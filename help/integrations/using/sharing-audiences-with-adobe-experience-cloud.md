---
product: campaign
title: オーディエンスを Adobe Experience Cloud と共有する
description: オーディエンスを Adobe Experience Cloud と共有する
badge-v7: label="v7" type="Informative" tooltip="Applies to Campaign Classic v7"
badge-v8: label="v8" type="Positive" tooltip="Also applies to Campaign v8"
audience: integrations
content-type: reference
topic-tags: audience-sharing
exl-id: 1c90e913-3375-476c-ab60-89f20239eb0d
source-git-commit: 6dc6aeb5adeb82d527b39a05ee70a9926205ea0b
workflow-type: tm+mt
source-wordcount: '305'
ht-degree: 100%

---

# オーディエンスを Adobe Experience Cloud と共有する{#sharing-audiences-with-adobe-experience-cloud}



>[!CAUTION]
>
>オーディエンスを Adobe Experience Cloud ソリューションと共有するには、Adobe Identity Management システムを実装する必要があります。[IMS の詳細を説明します](../../integrations/using/about-adobe-id.md)。

Adobe Campaign を使用すると、オーディエンスやセグメントを Adobe Experience Cloud のソリューションやコアサービスと共有できます。次の 2 つのオプションを使用できます。

1. Adobe Experience Platform セグメントデータを Adobe Campaign に送信します。この統合を実装するには、リアルタイム顧客データプラットフォーム（RTCDP）を Campaign に接続する必要があります。[詳しくは、この節を参照してください](https://experienceleague.adobe.com/docs/experience-platform/destinations/catalog/email-marketing/adobe-campaign.html?lang=ja)。

1. **Adobe Campaign** を **People コアサービス**（**Profiles &amp; Audiences コアサービス**&#x200B;とも呼ばれます）または Adobe Audience Manager と統合します。統合すると、次のことが可能になります。

   * 共有されたオーディエンスまたはセグメントを、他の Adobe Experience Cloud ソリューションから Adobe Campaign にインポートします。オーディエンスは Adobe Campaign のリストを使用してインポートできます。

   * Adobe Experience Cloud 共有オーディエンスのフォームでリストをエクスポートします。これらのオーディエンスは、お使いの他の Adobe Experience Cloud ソリューションで使用できます。オーディエンスは、ワークフローでターゲティングした後、専用の&#x200B;**[!UICONTROL 共有オーディエンスの更新]**&#x200B;アクティビティを使用してエクスポートできます。

この統合では、2 つのタイプの Adobe Experience Cloud ID をサポートしています。

* **訪問者 ID**：このタイプの識別子は、Adobe Experience Cloud の訪問者を Adobe Campaign 受信者に紐付けします。
* **宣言済み ID**：このタイプの識別子は、すべてのタイプのデータを Adobe Campaign データベース内の要素に紐付けします。Adobe Campaign では、事前定義された紐付けキーとして示されます。

  >[!NOTE]
  >
  > 宣言済み ID データソースも People コアサービス統合で使用できるようになりました。 
  >
  >People コアサービス統合を使用していて、Audience Manager 統合を追加する場合は、Adobe Audience Manager コンテキストでこの宣言済み ID データソースに移行する際に収集された ID 同期がすべて失われないように、Adobe Audience Manager コンサルタントの支援が必要です。
