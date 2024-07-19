---
product: campaign
title: レポートの管理
description: レポートの管理
feature: Reporting, Configuration
role: Data Engineer, Developer
badge-v8: label="v8 にも適用されます" type="Positive" tooltip="Campaign v8 にも適用されます"
exl-id: 68908664-3cf6-4a6c-a327-c7f059c27aa3
source-git-commit: e34718caefdf5db4ddd61db601420274be77054e
workflow-type: tm+mt
source-wordcount: '173'
ht-degree: 8%

---

# レポートの管理{#managing-reports}



カスタムテーブルおよびターゲットマッピングを使用してリンクされたテーブルのデータが考慮されるように、デフォルトのAdobe Campaign受信者（nm：受信者またはリンクされたスキーマ）に固有のスキーマに基づくレポートを再開発する必要があります（「ターゲットマッピング [ の節を参照 ](../../configuration/using/target-mapping.md)。

新しいレポートを作成するには、[ この節 ](../../reporting/using/about-reports-creation-in-campaign.md) を参照してください。

場合によっては、これらのテーブル固有の新しいキューブも配置する必要があります。 キューブについて詳しくは、[ この節 ](../../reporting/using/ac-cubes.md) を参照してください。

以下のレポートが関係しています。

* **[!UICONTROL 最近の提案トラッキング]** （recentPropositions）：リアルタイムの提案トラッキング。
* **[!UICONTROL 開封数の分類]** （opensByUserAgent）：ユーザーソフトウェアに応じて分類された開封数。
* **[!UICONTROL 共有アクティビティの統計]** （forwardActivities）：期間ごとの共有アクティビティ、開封数および購読数の分析。
* **[!UICONTROL トラッキング指標]** （mobileAppDeliveryFeedback）：モバイルアプリケーションにおける配信のトラッキング指標。
* **[!UICONTROL オファー分析]** （offerAnalysis）：日付およびチャネルごとのオファー分析。
* **[!UICONTROL 反応率]** （mobileAppDistribution）：最新の配信の反応率。
* **[!UICONTROL 購読の分類]** （mobileAppDistribution）：モバイルアプリケーションごとのアクティブな購読の分類。
