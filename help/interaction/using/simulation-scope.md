---
product: campaign
title: シミュレーションのスコープ
description: シミュレーションのスコープ
feature: Interaction, Offers
badge-v7: label="v7" type="Informative" tooltip="Campaign Classicv7 に適用"
badge-v8: label="v8" type="Positive" tooltip="Campaign v8 にも適用されます"
audience: interaction
content-type: reference
topic-tags: simulating-offers
exl-id: 4f6b3de2-3fdf-441d-925d-476e20e75c6f
source-git-commit: 3a9b21d626b60754789c3f594ba798309f62a553
workflow-type: tm+mt
source-wordcount: '251'
ht-degree: 96%

---

# シミュレーションのスコープ{#simulation-scope}



## スコープの定義 {#definition-of-the-scope}

「**[!UICONTROL スコープ]**」タブを表示し、必要な設定を選択します。

次の項目は必須です。

* 環境またはオファーカテゴリ。
* オファースペース。
* 連絡日。連絡日に実施要件を満たしていないオファーは、考慮されません。
* ターゲット母集団。

  ターゲットにフィルターを設定しない場合、受信者テーブル全体が考慮されます。

* ターゲットごとにシミュレーションされる提案数。

  受信者は、この多くの提案を受け取ります。例えば、5 と入力すると、各受信者が受け取るオファーの提案の数は最大 5 件になります。

  ![](assets/offer_simulation_009.png)

シミュレーションについて考慮に入れるようにオファーを調整するために、1 つまたは複数のテーマ（事前にカテゴリで指定されたもの）を追加できます。

また、シミュレーションをすべてのオファーについて実行するか、オンライン状態のオファーについてのみ実行するかを選択することもできます。一部のフィルターは、必要に応じて選択を変更できます。

>[!NOTE]
>
>連絡日の指定は必須です。これによって、インタラクションエンジンは選択した環境またはカテゴリのオファーを並べ替えることができます。日付を設定していない場合、シミュレーションを実行するとエラーが発生します。

## レポートの軸の追加 {#adding-reporting-axes}

「**[!UICONTROL 計算]**」タブで、ターゲットやオファー自体に対してレポートの軸を追加すると、シミュレーション分析をより充実させることができます。

それには、「**[!UICONTROL 追加]**」ボタンをクリックし、適切なフィールドを選択します。軸は、シミュレーションの計算に使用され、分析レポートに表示されます。詳しくは、[シミュレーションのトラッキング](../../interaction/using/simulation-tracking.md)を参照してください。

![](assets/offer_simulation_011.png)
