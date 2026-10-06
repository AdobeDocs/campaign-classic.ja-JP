---
product: campaign
title: 配信コントロール
description: 配信コントロールワークフローアクティビティの詳細を説明します
feature: Workflows
hide: true
exl-id: c7cface2-0837-4e6a-91dc-b8353010a7a4
TQID: 'https://experienceleague.adobe.com/WVXqtjcGQQOQJfVi58BqtLPqgG7AkgslAzQk4Vjbl9k'
product_v2:
  - id: dfc56824-e8b9-499e-85d4-21aedb507314
    internal-label: Campaign
  - id: fd6e6e36-54e4-4f1a-96fc-1a750e400d50
    internal-label: Campaign Classic v7
feature_v2:
  - id: a658c786-869b-4194-a780-2594d663adda
    internal-label: Data management
subfeature_v2:
  - id: ee25c34b-ea50-427b-9369-ba0a160f7d70
    internal-label: HeatMap
  - id: b5f0aaf4-1e48-400d-95ac-6eb3078cf22f
    internal-label: Execution activities
  - id: d1110311-2ca4-442b-be37-088a6db845ee
    internal-label: Data Management activities
  - id: fcb46c0f-76e1-48bc-9dd0-fcf9d97526cf
    internal-label: Workflows
source-git-commit: a43e591a565a18d79f583d975e3e812c5435b0c0
workflow-type: tm+mt
source-wordcount: '180'
ht-degree: 100%
---
# 配信コントロール{#delivery-control}



「**配信コントロール**」タイプアクションでは、配信を開始、一時停止、または中止できます。

これは、トランジション内で指定された配信、明示的に選択された配信、またはスクリプトで自動生成された配信です。 詳しくは、[配信](delivery.md)を参照してください。

![](assets/edit_diffusion_act.png)

「**[!UICONTROL 開始]**」を選択した場合、アクティビティは配信の開始に必要なすべての手順を実行します（ターゲットの計算、コンテンツの準備、配信）。 これらの手順の一部が、先行のワークフローアクティビティによって実行されている場合、再度実行されることはありません。 例えば、ターゲットの推定が「**[!UICONTROL 配信]**」タイプアクティビティによって既に実行されている場合（[配信](delivery.md)を参照）、「**[!UICONTROL 配信に基づくアクション]**」アクティビティが残りの手順を開始します（コンテンツの準備と配信）。

次のオプションを使用できます。

* **[!UICONTROL アウトバウンドトランジションを生成]**

  実行の終了時に有効化される出力トランジションを生成します。 アウトバウンド配信のターゲットを取得するかどうかを選択できます。

* **[!UICONTROL エラーを処理]**

  [エラーを処理](monitoring-workflow-execution.md#processing-errors)を参照してください。

## 入力パラメーター {#input-parameters}

* deliveryId

「**[!UICONTROL トランジション内で指定]**」アクションが選択されている場合の配信 ID。
