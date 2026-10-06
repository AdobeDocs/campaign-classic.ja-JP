---
product: campaign
title: レポートの管理
description: レポートの管理
feature: Reporting, Configuration
role: Developer
badge-v8: label="Also applies to v8" type="Positive" tooltip="Also applies to Campaign v8"
exl-id: 68908664-3cf6-4a6c-a327-c7f059c27aa3
TQID: 'https://experienceleague.adobe.com/LA4v5oODC9n5K2Ttox9SF7lwcGQOU7IDEvL1P4Sls-4'
product_v2:
  - id: dfc56824-e8b9-499e-85d4-21aedb507314
    internal-label: Campaign
  - id: fd6e6e36-54e4-4f1a-96fc-1a750e400d50
    internal-label: Campaign Classic v7
feature_v2:
  - id: c309ee4e-82e4-4f7e-b608-ef345678c34e
    internal-label: Dynamic reporting
  - id: c5474392-5419-4296-9e41-f6f4ce4f6e9b
    internal-label: Administration
subfeature_v2:
  - id: b3a4149f-2b3a-44d1-894e-e3ac4c77fb47
    internal-label: Reporting interface
  - id: a14877cc-63b1-41d9-bf0b-5f97cadd0417
    internal-label: Configuration guidelines
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
topic_v2:
  - id: aa2f3246-cb95-4b30-8899-fdf7d73550cc
    internal-label: Reporting
source-git-commit: a43e591a565a18d79f583d975e3e812c5435b0c0
workflow-type: tm+mt
source-wordcount: '165'
ht-degree: 3%
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
