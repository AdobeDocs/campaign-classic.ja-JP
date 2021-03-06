---
product: campaign
title: 集計の更新
description: 「集計を更新」ワークフローアクティビティの詳細を説明します
feature: Workflows
exl-id: d2b26af0-30a1-4852-acd5-996795f198a1
source-git-commit: 381538fac319dfa075cac3db2252a9cc80b31e0f
workflow-type: ht
source-wordcount: '0'
ht-degree: 100%

---

# 集計の更新{#update-aggregate}

![](../../assets/v7-only.svg)

集計は、レポーティングの目的のためキューブレベルで定義できます。集計の設定は、「**[!UICONTROL ワークフロー]**」タブでおこないます。

キューブおよび Adobe Campaign での集計の使用方法について、詳しくはこの[節](../../reporting/using/concepts-and-methodology.md#calculating-and-using-aggregates)を参照してください。

「**[!UICONTROL 集計を更新]**」アクティビティで、適用する更新モード（完全または部分的）を選択できます。

デフォルトでは、各計算時に完全更新が実行されます。部分的更新を有効にするには、該当するオプションを選択し、更新の条件を定義します。

![](assets/s_advuser_cube_agregate_05.png)

**ベストプラクティス**：アクティビティを使用して、計算の更新頻度をスケジュール設定できる「**[!UICONTROL スケジューラー]**」アクティビティ。

![](assets/s_advuser_cube_agregate_04.png)
