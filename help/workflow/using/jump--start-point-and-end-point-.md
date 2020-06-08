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
source-git-commit: 4994aff9f2db36a519a9c7af2864393713eb65e3
workflow-type: tm+mt
source-wordcount: '123'
ht-degree: 86%

---


# ジャンプ（開始ポイントと終了ポイント）{#jump-start-point-and-end-point}

「**[!UICONTROL ジャンプ]**」タイプのグラフィカルオブジェクトは、特に、交差するトランジションを持つ複雑なダイアグラムの可読性を向上させます。

ジャンプは、矢印のないトランジションです。

次の例のように、アクティビティ間を移動します。

![](assets/s_user_segmentation_jump_sample.png)

「開始ポイント」タイプのトランジションごとに、それぞれ「終了ポイント」タイプのトランジションを配置する必要があります。

同じワークフロー内に、ジャンプする開始ポイントと終了ポイントを複数挿入できます。各ポイントは、パラメーターに必ず入力される番号によって識別されます。

![](assets/s_user_segmentation_jump_in.png)

ダイアグラムの可読性を向上させるには、ジャンプに関連付けけられた画像に、そのジャンプの番号が表示されるように変更します。[アクティビティ画像の管理](../../workflow/using/managing-activity-images.md)を参照してください。
