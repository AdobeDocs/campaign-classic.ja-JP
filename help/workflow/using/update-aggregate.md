---
title: 集計を更新
seo-title: 集計を更新
description: 集計を更新
seo-description: null
page-status-flag: never-activated
uuid: 34ae42e1-da34-43be-b219-0b3b872177b3
contentOwner: sauviat
products: SG_CAMPAIGN/CLASSIC
audience: workflow
content-type: reference
topic-tags: action-activities
discoiquuid: 031f8d5d-940c-4a4c-97e7-ad4ef61983c1
index: y
internal: n
snippet: y
translation-type: tm+mt
source-git-commit: 20f835c357d016643ea1f3209ee4dfb6d3239f90

---


# 集計を更新{#update-aggregate}

集計は、レポーティングの目的のためキューブレベルで定義できます。A **[!UICONTROL Workflow]** tab is available when configuring an aggregate.

キューブおよび Adobe Campaign での集計の使用方法について、詳しくはこの[節](../../reporting/using/concepts-and-methodology.md#calculating-and-using-aggregates)を参照してください。

The **[!UICONTROL Update aggregate]** activity lets you select the update mode to apply: full or partial.

デフォルトでは、各計算時に完全更新が実行されます。部分的更新を有効にするには、該当するオプションを選択し、更新の条件を定義します。

![](assets/s_advuser_cube_agregate_05.png)

**ベストプラクティス**:アクティビテ **[!UICONTROL Scheduler]** ィを使用して、計算の更新の頻度を指定できます。

![](assets/s_advuser_cube_agregate_04.png)

