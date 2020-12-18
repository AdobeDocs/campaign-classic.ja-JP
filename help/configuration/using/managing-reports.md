---
solution: Campaign Classic
product: campaign
title: レポートの管理
description: レポートの管理
audience: configuration
content-type: reference
topic-tags: use-a-custom-recipient-table
translation-type: tm+mt
source-git-commit: 972885c3a38bcd3a260574bacbb3f507e11ae05b
workflow-type: tm+mt
source-wordcount: '164'
ht-degree: 3%

---


# レポートの管理{#managing-reports}

カスタムテーブルと、ターゲットマッピングを介してリンクされたテーブルのデータを考慮するために、デフォルトのAdobe Campaign受信者(nm:受信者またはスキーマリンク)に固有のスキーマに基づくレポートを再開発する必要があります([ターゲットマッピング](../../configuration/using/target-mapping.md)の節を参照)。

新しいレポートを作成する方法については、[このセクション](../../reporting/using/about-reports-creation-in-campaign.md)を参照してください。

場合によっては、これらのテーブルに固有の新しいキューブも配置する必要があります。 キューブの詳細は[このセクション](../../reporting/using/about-cubes.md)に記載されています。

以下のレポートが対象となります。

* **[!UICONTROL 最近の提案の追跡]** (recentPropositions):リアルタイム提案トラッキング。
* **[!UICONTROL opens]** (opensByUserAgent)の分類：ユーザーソフトウェアに従って分類されて開きます。
* **[!UICONTROL 共有アクティビティ]** (forwardActivities)の統計：アクティビティ、開く、購読を期間ごとに共有する分析。
* **[!UICONTROL 追跡インジケーター]** (mobileAppDeliveryFeedback):モバイルアプリケーションの配信用の追跡インジケーター。
* **[!UICONTROL オファー分析]** (offerAnalysis):日付とチャネルごとのオファー分析。
* **[!UICONTROL 反応率]** (mobileAppDistribution):最新の配信の反応率。
* **[!UICONTROL 購読の分類]** (mobileAppDistribution):モバイルアプリケーションごとのアクティブな購読の分類。

