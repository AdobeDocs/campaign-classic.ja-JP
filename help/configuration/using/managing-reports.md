---
product: campaign
title: レポートの管理
description: レポートの管理
feature: Reporting, Configuration
badge-v7: label="v7" type="Informative" tooltip="Campaign Classicv7 に適用"
badge-v8: label="v8" type="Positive" tooltip="Campaign v8 にも適用されます"
exl-id: 68908664-3cf6-4a6c-a327-c7f059c27aa3
source-git-commit: 3a9b21d626b60754789c3f594ba798309f62a553
workflow-type: tm+mt
source-wordcount: '176'
ht-degree: 4%

---

# レポートの管理{#managing-reports}



カスタムテーブルと、ターゲットマッピングを介してリンクされたテーブルのデータを考慮するには、デフォルトのAdobe Campaign受信者（nm:recipient またはリンクされたスキーマ）に基づくレポートを再開発する必要があります ( [ターゲットマッピング](../../configuration/using/target-mapping.md) を参照 )。

新しいレポートを作成するには、 [この節](../../reporting/using/about-reports-creation-in-campaign.md).

場合によっては、これらのテーブルに固有の新しいキューブを配置する必要があります。 キューブについて詳しくは、 [この節](../../reporting/using/ac-cubes.md).

次のレポートが対象となります。

* **[!UICONTROL 最近の提案トラッキング]** (recentPropositions)：リアルタイム提案トラッキング。
* **[!UICONTROL 開封数の分類]** (opensByUserAgent)：が開き、ユーザーソフトウェアに応じて分類されます。
* **[!UICONTROL 共有アクティビティの統計]** (forwardActivities)：期間ごとの共有アクティビティ数、開封数および購読数の分析。
* **[!UICONTROL トラッキング指標]** (mobileAppDeliveryFeedback)：モバイルアプリケーションでの配信のトラッキング指標です。
* **[!UICONTROL オファー分析]** (offerAnalysis)：日付別およびチャネル別のオファー分析。
* **[!UICONTROL 反応率]** (mobileAppDistribution)：最新の配信の反応率。
* **[!UICONTROL 購読の分類]** (mobileAppDistribution)：モバイルアプリケーションごとのアクティブな購読の分類。
