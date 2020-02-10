---
title: サブワークフロー
seo-title: サブワークフロー
description: サブワークフロー
seo-description: null
page-status-flag: never-activated
uuid: c952633f-1aca-44cf-bb50-a67e9b086030
contentOwner: sauviat
products: SG_CAMPAIGN/CLASSIC
audience: workflow
content-type: reference
topic-tags: flow-control-activities
discoiquuid: a4441820-1b3d-4bac-a6e3-1c9c14466d19
index: y
internal: n
snippet: y
translation-type: tm+mt
source-git-commit: c10a0a11c6e9952aa47da1f7a15188c79c62508d

---


# サブワークフロー{#sub-workflow}

The **[!UICONTROL Sub-workflow]** activity lets you trigger the execution of another workflow and recover the result. このアクティビティにより、簡素化されたインターフェイス経由で、複雑なワークフローを使用できます。

1 つのワークフローで複数のサブワークフローを呼び出すことができます。サブワークフローは、同期して実行されます。

>[!NOTE]
>
>サブワークフローが正常に動作するよう、一番小さい数の「到着」タイプのジャンプを 1 つのみ、一番大きい数の「開始」タイプのジャンプを 1 つのみにする必要があります。例えば、優先度が 1、2、および 3 の「開始」ジャンプタイプがある場合、優先度 3 の「開始」ジャンプタイプを 1 つにする必要があります。

1. 別のワークフローでサブワークフローとして使用するワークフローを作成します。
1. Insert a **[!UICONTROL Jump (end point)]** activity with a priority of 1 at the beginning of the workflow. 「到着」タイプジャンプが複数ある場合、Adobe Campaign は一番小さい数の「到着」ジャンプを使用します。

   Insert a **[!UICONTROL Jump (start point)]** activity with a priority of 2 at the end of the workflow. 「開始」タイプジャンプが複数ある場合、Adobe Campaign は一番大きい数の「開始」ジャンプを使用します。

   ![](assets/subworkflow_jumps.png)

   >[!NOTE]
   >
   >If the sub-workflow activity references a workflow with several **[!UICONTROL Jump]** activities, the sub-workflow is executed between the &quot;arrival&quot; type jump with the lowest number and the &quot;start&quot; type jump with the highest number.

1. この「サブワークフロー」を完了して保存します。
1. 「マスター」ワークフローを作成します。
1. Insert a **[!UICONTROL Sub-workflow]** activity and open it.
1. Select the workflow that you want to use from the **[!UICONTROL Workflow template]** drop-down list.

   ![](assets/subworkflow_selection.png)

1. さらに、参照先ワークフローを変更するための設定スクリプトを追加することもできます。
1. クリック **[!UICONTROL Ok]**. It will automatically create an outbound transition with the label of the **[!UICONTROL Jump (start point)]** activity from the selected workflow.

   ![](assets/subworkflow_outbound.png)

1. ワークフローを実行します。

Once run, the workflow that was called as a sub-workflow is still in **[!UICONTROL Being edited]** status, which means the following:

* トランジションを右クリックしてターゲットを表示することはできません。
* 中間母集団の数は表示できません。
* ログは「マスター」ワークフローで集計され、「サブワークフロー」としてのみラベルが付けられます。

実際、このワークフローはテンプレートに過ぎません。「マスター」ワークフローから呼び出すと、このテンプレートに基づいて新しいサブワークフローが作成されます。

## Input parameters (optional) {#input-parameters--optional-}

* tableName
* schema

各インバウンドイベントは、これらのパラメーターによって定義されるターゲットを指定する必要があります。

## 出力パラメーター {#output-parameters}

* tableName
* schema
* recCount

この 3 つの値セットは、クエリのターゲットとなる母集団を識別します。**[!UICONTROL tableName]** はターゲットの識別子を記録するテーブル名、**[!UICONTROL schema]** は母集団のスキーマ（通常は nms:recipient）、**[!UICONTROL recCount]** はテーブル内の要素の数です。

* targetSchema

この値は、作業用テーブルのスキーマです。このパラメーターは、**[!UICONTROL tableName]** と **[!UICONTROL schema]** のすべてのトランジションで有効です。
