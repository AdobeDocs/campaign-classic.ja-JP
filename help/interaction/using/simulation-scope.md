---
product: campaign
title: シミュレーションのスコープ
description: シミュレーションのスコープ
badge-v7: label="v7" type="Informative" tooltip="Applies to Campaign Classic v7"
badge-v8: label="v8" type="Positive" tooltip="Also applies to Campaign v8"
audience: interaction
content-type: reference
topic-tags: simulating-offers
exl-id: 4f6b3de2-3fdf-441d-925d-476e20e75c6f
source-git-commit: 6dc6aeb5adeb82d527b39a05ee70a9926205ea0b
workflow-type: tm+mt
source-wordcount: '239'
ht-degree: 100%

---

# シミュレーションのスコープ{#simulation-scope}



## スコープの定義 {#definition-of-the-scope}

「**[!UICONTROL スコープ]**」タブを表示し、必要な設定を選択します。

次の項目は必須です。

* 環境またはオファーカテゴリ。
* オファースペース。
* コンタクト日.コンタクト日に実施要件を満たしていないオファーは、考慮されません。
* ターゲット母集団。

   ターゲットにフィルターを設定しない場合、受信者テーブル全体が考慮されます。

* ターゲットごとにシミュレーションされる提案数。

   受信者は、この多くの提案を受け取ります。例えば、5 と入力すると、各受信者が受け取るオファーの提案の数は最大 5 件になります。

   ![](assets/offer_simulation_009.png)

シミュレーションについて考慮に入れるようにオファーを調整するために、1 つまたは複数のテーマ（事前にカテゴリで指定されたもの）を追加できます。

また、シミュレーションをすべてのオファーについて実行するか、オンライン状態のオファーについてのみ実行するかを選択することもできます。一部のフィルターは、必要に応じて選択を変更できます。

>[!NOTE]
>
>コンタクト日の指定は必須です。これによって、インタラクションエンジンは選択した環境またはカテゴリのオファーを並べ替えることができます。日付を設定していない場合、シミュレーションを実行するとエラーが発生します。

## レポートの軸の追加 {#adding-reporting-axes}

「**[!UICONTROL 計算]**」タブで、ターゲットやオファー自体に対してレポートの軸を追加すると、シミュレーション分析をより充実させることができます。

それには、「**[!UICONTROL 追加]**」ボタンをクリックし、適切なフィールドを選択します。軸は、シミュレーションの計算に使用され、分析レポートに表示されます。詳しくは、[シミュレーションのトラッキング](../../interaction/using/simulation-tracking.md)を参照してください。

![](assets/offer_simulation_011.png)
