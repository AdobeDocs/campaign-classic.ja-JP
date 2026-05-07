---
product: campaign
title: レポートの管理
description: レポートの管理
feature: Reporting, Configuration
role: Developer
badge-v8: label="v8 にも適用されます" type="Positive" tooltip="Campaign v8 にも適用されます"
exl-id: 68908664-3cf6-4a6c-a327-c7f059c27aa3
source-git-commit: 9f5205ced6b8d81639d4d0cb6a76905a753cddac
workflow-type: tm+mt
source-wordcount: '174'
ht-degree: 8%

---

# レポートの管理{#managing-reports}



デフォルトのAdobe Campaign受信者（nm:recipientまたはスキーマリンク）に固有のスキーマに基づくレポートは、カスタムテーブルのデータと、ターゲットマッピングを介してリンクされたテーブルのデータを考慮するために再開発する必要があります（[ ターゲットマッピング ](../../configuration/using/target-mapping.md)節を参照）。

新しいレポートを作成するには、[このセクション ](../../reporting/using/about-reports-creation-in-campaign.md)を参照してください。

場合によっては、これらのテーブルに固有の新しいキューブも配置する必要があります。 キューブの詳細については、[このセクション ](../../reporting/using/ac-cubes.md)を参照してください。

次のレポートが関係しています：

* **[!UICONTROL 最近の提案の追跡]** （recentPropositions）: リアルタイムの提案の追跡。
* **[!UICONTROL 開封数の内訳]** （opensByUserAgent）: ユーザーソフトウェアに応じて開封数が分類されます。
* **[!UICONTROL 共有アクティビティの統計]** （forwardActivities）：共有アクティビティ、開封数、サブスクリプション数を期間ごとに分析します。
* **[!UICONTROL トラッキング指標]** （mobileAppDeliveryFeedback）: モバイルアプリケーションでの配信のトラッキング指標。
* **[!UICONTROL オファー分析]** （offerAnalysis）：日付とチャネルごとのオファー分析。
* **[!UICONTROL 反応率]** （mobileAppDistribution）：最新の配信の反応率。
* **[!UICONTROL サブスクリプションの内訳]** （mobileAppDistribution）: モバイルアプリケーションごとのアクティブなサブスクリプションの内訳。
