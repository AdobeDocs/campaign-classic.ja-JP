---
title: 配信コントロール
seo-title: 配信コントロール
description: 配信コントロール
seo-description: null
page-status-flag: never-activated
uuid: f9cef2d9-a6a5-45bd-8c7a-fabc11879628
contentOwner: sauviat
products: SG_CAMPAIGN/CLASSIC
audience: workflow
content-type: reference
topic-tags: action-activities
discoiquuid: 0b5ee05c-4b96-425a-ab0f-60b930de21bd
index: y
internal: n
snippet: y
translation-type: tm+mt
source-git-commit: cfb1b02a6261c001392b5cc6430f00206e802bb8

---


# 配信コントロール{#delivery-control}

「**配信コントロール**」タイプアクションでは、配信を開始、一時停止、または中止できます。

これは、トランジション内で指定された配信、明示的に選択された配信、またはスクリプトで自動生成された配信です。詳しくは、[配信](../../workflow/using/delivery.md)を参照してください。

![](assets/edit_diffusion_act.png)

If you select **[!UICONTROL Start]**, the activity will perform all the steps required to start the delivery (target calculation, content preparation, delivery). これらの手順の一部が、先行のワークフローアクティビティによって実行されている場合、再度実行されることはありません。For instance, if the target estimation was already performed by a **[!UICONTROL Delivery]** type activity (refer to [Delivery](../../workflow/using/delivery.md)), the **[!UICONTROL Act on the delivery]** activity will launch the remaining steps (content preparation and delivery).

次のオプションを使用できます。

* **[!UICONTROL Generate an outbound transition]**

   実行の終了時に有効化される出力トランジションを生成します。アウトバウンド配信のターゲットを取得するかどうかを選択できます。

* **[!UICONTROL Processing errors]**

   詳しくは、処理エ [ラーを参照してくださ](../../workflow/using/monitoring-workflow-execution.md#processing-errors)い。

## 入力パラメーター {#input-parameters}

* deliveryId

配信識別子(選択したアクションが **[!UICONTROL Specified in the transition]**。
