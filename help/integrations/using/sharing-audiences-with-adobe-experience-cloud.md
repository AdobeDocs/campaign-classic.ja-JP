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
index: y
internal: n
snippet: y
translation-type: ht
source-git-commit: 418a36cd51106dae2b4201c8b5abda9b05285a18

---


# オーディエンスを Adobe Experience Cloud と共有する{#sharing-audiences-with-adobe-experience-cloud}

>[!NOTE]
>
>この統合を使用するには、IMS を実装する必要があります。[IMS](../../integrations/using/about-adobe-id.md) についての節を参照してください。

Adobe Campaign では、Adobe Experience Cloud ソリューションやコアサービスとオーディエンスおよびセグメントの交換や共有をおこなうことができます。そのためには、**Adobe Campaign** を **People コアサービス**（**Profiles &amp; Audiences コアサービス**&#x200B;とも呼ばれます）または Adobe Audience Manager と統合する必要があります。統合すると、次のことが可能になります。

* 共有されたオーディエンスまたはセグメントを、他の Adobe Experience Cloud ソリューションから Adobe Campaign にインポートします。オーディエンスは Adobe Campaign のリストを使用してインポートできます。
* Adobe Experience Cloud 共有オーディエンスのフォームでリストをエクスポートします。これらのオーディエンスは、お使いの他の Adobe Experience Cloud ソリューションで使用できます。オーディエンスは、ワークフローでターゲティングした後、専用の&#x200B;**[!UICONTROL 共有オーディエンスの更新]**&#x200B;アクティビティを使用してエクスポートできます。

>[!CAUTION]
>
>データのタイプによっては、Adobe Campaign でのオーディエンスのインポートは法規制の対象となる場合があります。

この統合では、2 つのタイプの Adobe Experience Cloud ID をサポートしています。

* **訪問者 ID**：このタイプの識別子は、Adobe Experience Cloud の訪問者を Adobe Campaign 受信者に紐付けします。
* **宣言済み ID**：このタイプの識別子は、すべてのタイプのデータを Adobe Campaign データベースからの要素に紐付けします。Adobe Campaign では、事前定義された紐付けキーとして示されます。
