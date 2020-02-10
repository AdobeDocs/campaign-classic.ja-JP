---
title: ジャンプ（開始ポイントと終了ポイント）
seo-title: ジャンプ（開始ポイントと終了ポイント）
description: ジャンプ（開始ポイントと終了ポイント）
seo-description: null
page-status-flag: never-activated
uuid: 68e669eb-6c70-483e-afb7-7340225a6e1d
contentOwner: sauviat
products: SG_CAMPAIGN/CLASSIC
audience: workflow
content-type: reference
topic-tags: flow-control-activities
discoiquuid: f3cd5409-c301-4580-96e3-9349e18cf42a
index: y
internal: n
snippet: y
translation-type: tm+mt
source-git-commit: 20f835c357d016643ea1f3209ee4dfb6d3239f90

---


# ジャンプ（開始ポイントと終了ポイント）{#jump-start-point-and-end-point}

**[!UICONTROL Jump]** 複雑な図、特に交差遷移を持つ図の読みやすさを改善するために、 — タイプのグラフィカルオブジェクトを使用します。

ジャンプは矢印なしのトランジションです。次の例のように、あるアクティビティから別のアクティビティに移動します。

![](assets/s_user_segmentation_jump_sample.png)

「開始ポイント」タイプのトランジションごとに、それぞれ「終了ポイント」タイプのトランジションを配置する必要があります。

同じワークフロー内に、ジャンプする開始ポイントと終了ポイントを複数挿入できます。各ポイントは、パラメーターに必ず入力される番号によって識別されます。

![](assets/s_user_segmentation_jump_in.png)

ダイアグラムの可読性を向上させるには、ジャンプに関連付けけられた画像に、そのジャンプの番号が表示されるように変更します。アクティビティ [画像の管理を参照してください](../../workflow/using/managing-activity-images.md)。
