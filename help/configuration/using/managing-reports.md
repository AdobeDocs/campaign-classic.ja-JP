---
product: campaign
title: レポートの管理
description: レポートの管理
audience: configuration
content-type: reference
topic-tags: use-a-custom-recipient-table
exl-id: 68908664-3cf6-4a6c-a327-c7f059c27aa3
source-git-commit: 20509f44c5b8e0827a09f44dffdf2ec9d11652a1
workflow-type: tm+mt
source-wordcount: '164'
ht-degree: 3%

---

# レポートの管理{#managing-reports}

![](../../assets/v7-only.svg)

カスタムテーブルと、ターゲットマッピングを介してリンクされたテーブルのデータを考慮するには、デフォルトのAdobe Campaign受信者（nm:recipient またはスキーマリンク）に固有のスキーマに基づくレポートを再開発する必要があります（[ ターゲットマッピング ](../../configuration/using/target-mapping.md) の節を参照）。

新しいレポートを作成するには、[ この節 ](../../reporting/using/about-reports-creation-in-campaign.md) を参照してください。

場合によっては、これらのテーブルに固有の新しいキューブを配置する必要があります。 キューブについて詳しくは、[ この節 ](../../reporting/using/about-cubes.md) を参照してください。

次のレポートが対象です。

* **[!UICONTROL 最近の提案トラッキング]** (recentPropositions):リアルタイム提案トラッキング。
* **[!UICONTROL 開封数の分類]** (opensByUserAgent):ユーザーソフトウェアに従って分類された開き。
* **[!UICONTROL 共有アクティビティの統計]** (forwardActivities):期間ごとの共有アクティビティ数、開封数および購読数の分析。
* **[!UICONTROL トラッキング指標]** (mobileAppDeliveryFeedback):モバイルアプリケーションでの配信のトラッキング指標。
* **[!UICONTROL オファー分析]** (offerAnalysis):日付別およびチャネル別のオファー分析。
* **[!UICONTROL 反応率]** (mobileAppDistribution):最新の配信の反応率。
* **[!UICONTROL 購読の分類]** (mobileAppDistribution):モバイルアプリケーションごとのアクティブな購読の分類。
