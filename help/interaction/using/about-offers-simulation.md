---
title: オファーのシミュレーションについて
seo-title: オファーのシミュレーションについて
description: オファーのシミュレーションについて
seo-description: null
page-status-flag: never-activated
uuid: 3c6783a0-6bab-4c41-8101-1d926c1ac6ac
contentOwner: sauviat
products: SG_CAMPAIGN/CLASSIC
audience: interaction
content-type: reference
topic-tags: simulating-offers
discoiquuid: 0af021af-2686-4a37-97d9-6d13a851b5dd
index: y
internal: n
snippet: y
translation-type: ht
source-git-commit: 5489e09303920bf5bd3dcd08263dc3c945d151c1

---


# オファーのシミュレーションについて{#about-offers-simulation}

**シミュレーション**&#x200B;モジュールを使用すると、提案を受信者に送信する前に、1 つのカテゴリまたは環境に属するオファーの配分をテストできます。

シミュレーションには、オファーにあらかじめ適用されているコンテキストおよび実施要件ルール（[オファーカタログの概要](../../interaction/using/offer-catalog-overview.md)を参照）と、オファーのプレゼンテーションルール（[オファー表示域の管理](../../interaction/using/managing-offer-presentation.md)を参照）が考慮されます。ターゲットの受信者はシミュレーションの影響を受けないので、これにより、実際にオファーを使用したり、ターゲットを拡大または縮小したりしなくても、オファーの提案の様々なバージョンをテストして調整できます。

オファーをシミュレートする方法については、以下の手順を参照してください。この[ビデオ](https://helpx.adobe.com/jp/campaign/classic/how-to/simulate-offer-in-acv6.html?playlist=/ccx/v1/collection/product/campaign/classic/segment/digital-marketers/explevel/intermediate/applaunch/introduction/collection.ccx.js&amp;ref=helpx.adobe.com)もご覧ください。

## シミュレーション作成の主な手順 {#main-steps-for-creating-a-simulation}

オファーのシミュレーションを実行するには、次の手順に従います。

1. **[!UICONTROL プロファイルとターゲット]**&#x200B;ウィンドウで、「**[!UICONTROL シミュレーション]**」リンクをクリックし、「**[!UICONTROL 作成]**」ボタンをクリックします。

   ![](assets/offer_simulation_001.png)

1. 作成したシミュレーションを保存し、編集します。
1. 「**[!UICONTROL 編集]**」タブに移動し、実行設定を指定します。

   詳しくは、[実行設定](../../interaction/using/execution-settings.md)を参照してください。

   ![](assets/offer_simulation_003.png)

   >[!NOTE]
   >
   >実行設定は、Campaign でインタラクションを使用する場合にのみ使用できます。

1. シミュレーションのスコープを指定します。

   詳しくは、[スコープの定義](../../interaction/using/simulation-scope.md#definition-of-the-scope)を参照してください。

   ![](assets/offer_simulation_004.png)

1. レポートの軸を追加して、**[!UICONTROL オファーの配分（ランク別）]**&#x200B;レポートの内容をより充実させます（オプション）。

   詳しくは、[レポートの軸の追加](../../interaction/using/simulation-scope.md#adding-reporting-axes)を参照してください。

   ![](assets/offer_simulation_005.png)

1. 「**[!UICONTROL 保存]**」をクリックして、シミュレーションの設定を保存します。
1. ダッシュボードからシミュレーションを開始します。

   ![](assets/offer_simulation_006.png)

1. シミュレーション結果をチェックし、分析レポートを表示します。

   詳しくは、[シミュレーショントラッキング](../../interaction/using/simulation-tracking.md)を参照してください。

   ![](assets/offer_simulation_007.png)
