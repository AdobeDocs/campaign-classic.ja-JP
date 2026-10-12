---
product: campaign
title: ワークフローについて
description: ワークフローを使用すれば、データおよびオーディエンスの管理やメッセージの送信などのプロセスを自動化できます
feature: Workflows, Data Management
exl-id: 024a7344-9376-4ff3-926a-003148229f9f
product_v2:
  - id: dfc56824-e8b9-499e-85d4-21aedb507314
    internal-label: Campaign
  - id: fd6e6e36-54e4-4f1a-96fc-1a750e400d50
    internal-label: Campaign Classic v7
feature_v2:
  - id: a658c786-869b-4194-a780-2594d663adda
    internal-label: Data management
  - id: c5474392-5419-4296-9e41-f6f4ce4f6e9b
    internal-label: Administration
subfeature_v2:
  - id: ee25c34b-ea50-427b-9369-ba0a160f7d70
    internal-label: HeatMap
  - id: b5f0aaf4-1e48-400d-95ac-6eb3078cf22f
    internal-label: Execution activities
  - id: d1110311-2ca4-442b-be37-088a6db845ee
    internal-label: Data Management activities
  - id: fcb46c0f-76e1-48bc-9dd0-fcf9d97526cf
    internal-label: Workflows
source-git-commit: 9c678f353d367115bc188da80f07e018c44e2612
workflow-type: tm+mt
source-wordcount: '298'
ht-degree: 100%
---
# ワークフローを使用した自動化 {#gs-workflows}

Adobe Campaign のワークフローを使用すると、チームはプラットフォーム全体でエンドツーエンドのビジネスプロセスを合理化および自動化できます。 直感的なグラフィカルインターフェイスを使用すると、データのセグメント化、キャンペーンの実行、ファイル処理、ユーザーの承認などのタスクを調整するワークフローを、すべて 1 か所で設計および管理できます。

例えば、リモートサーバーからファイルを取得し、その内容を抽出し、Adobe Campaign サーバーにシームレスにデータを読み込むプロセスを自動化できます。これにより、手作業を減らし、運用効率を高めることができます。 ワークフローエンジンにより、すべての手順が確実に実行され、追跡されて可視性と制御性が確保されます。

>[!BEGINTABS]

>[!TAB ワークフロードキュメント]

ワークフロー管理について詳しくは、[Campaign v8 ドキュメント](https://experienceleague.adobe.com/docs/campaign/automation/workflows/introduction/about-workflows.html?lang=ja){target=_blank}を参照してください。


[![画像](../../assets/do-not-localize/learn-more-button.svg)](https://experienceleague.adobe.com/docs/campaign/automation/workflows/introduction/about-workflows.html?lang=ja){target=_blank}


>[!TAB 便利なリンク]

ワークフロー管理に関連する主な手順について詳しくは、Campaign v8 ドキュメントを参照してください。

* [ワークフローアクティビティ](https://experienceleague.adobe.com/docs/campaign/automation/workflows/wf-activities/activities.html?lang=ja){target=_blank}：アクティビティは、タスクテンプレートです。 ワークフローには、ターゲティング、フロー制御、アクションおよびイベントアクティビティが含まれます。

* [ワークフローの作成](https://experienceleague.adobe.com/docs/campaign/automation/workflows/introduction/build-a-workflow.html?lang=ja){target=_blank}：ターゲティング、キャンペーン、テクニカルワークフローの作成および実行方法について説明します。

* [ベストプラクティス](https://experienceleague.adobe.com/docs/campaign/automation/workflows/introduction/workflow-best-practices.html?lang=ja){target=_blank}：Campaign ワークフローのパフォーマンスを最適化し、ワークフローのデザインを改善し、正しい設定を定義するためのガイドラインについて説明します。

* [ワークフローの監視](https://experienceleague.adobe.com/docs/campaign/automation/workflows/monitoring-workflows/monitor-workflow-execution.html?lang=ja){target=_blank}：ワークフローの実行を監視して、すべてが正しく実行されていることを確認する方法について説明します。

* [ワークフローのユースケース](https://experienceleague.adobe.com/docs/campaign/automation/workflows/use-cases/workflow-use-cases.html?lang=ja){target=_blank}：ワークフローを使用できるコンテキストと、エンドツーエンドのユースケースを通じてワークフローを実装する方法について説明します。


>[!ENDTABS]





<!--

Adobe Campaign uses workflows to:

* Carry out targeting campaigns. [Learn more](https://experienceleague.adobe.com/ja/docs/campaign/automation/workflows/introduction/build-a-workflow){target="_blank"} (Campaign v8 documentation)
* Build campaigns: for each campaign, the **[!UICONTROL Workflow]** tab lets you build the target and create the deliveries. [Learn more](https://experienceleague.adobe.com/ja/docs/campaign/automation/workflows/introduction/build-a-workflow){target="_blank"} (Campaign v8 documentation)
* Perform technical processes: cleanup, collecting tracking information or provisional calculations. [Learn more](https://experienceleague.adobe.com/ja/docs/campaign/automation/workflows/introduction/build-a-workflow){target="_blank"} (Campaign v8 documentation)

A workflow can mean both a process definition (the workflow model, which is a representation of what is supposed to happen) and an instance of this process (a workflow instance, which is a representation of what is actually happening).

The workflow template describes the various tasks to be performed and how they are linked together. The task templates are called activities and are represented by icons. They are linked together by transitions.

![](assets/example1.png)

Each workflow contains:

* **[!UICONTROL Activities]**

  An activity describes a task template. The various activities available are represented on the diagram by icons. Each type has common properties and specific properties. For example, while all activities have a name and label, only the **[!UICONTROL Approval]** activity has an assignment.

  In a workflow diagram, a given activity can produce multiple tasks, in particular when there is a loop or recurrent (periodic) actions.

  All workflow activities are listed in [this section](https://experienceleague.adobe.com/ja/docs/campaign/automation/workflows/wf-activities/activities){target="_blank"} (Campaign v8 documentation), including use cases and samples.

* **[!UICONTROL Transitions]**

  Transitions enable you to link activities and to define their sequence. A transition links a source activity to a destination activity. There are several sorts of transitions, which depend on the source activity. Some transitions have additional parameters such as a duration, a condition or a filter.

  A transition which is not linked to a destination activity is colored orange and the arrow head is shown as a diamond.

  >[!NOTE]
  >
  >A workflow containing unterminated transitions can still be executed: a warning message will be generated and the workflow will pause once it reaches the transition but it will not generate an error. It is thus possible to start a workflow without it being finished and to add to it as you go along.

  For more information about how to build a workflow, refer to [this section](https://experienceleague.adobe.com/ja/docs/campaign/automation/workflows/introduction/build-a-workflow){target="_blank"} (Campaign v8 documentation).

* **[!UICONTROL Worktables]**

  The worktable contains all the information carried by the transition. Each workflow uses several worktables. The data conveyed in these tables can be accelerated and used throughout the workflow's life cycle, as long as it is not purged. Indeed, unneeded tables are purged each time the workflow is passivated, and possibly during the execution of the largest workflows to avoid overloading the server.

  Learn more on workflow data and tables in [this section](https://experienceleague.adobe.com/ja/docs/campaign/automation/workflows/introduction/use-workflow-data){target="_blank"} (Campaign v8 documentation).

## Key principles and best practices{#principles-workflows}

Refer to these sections to find guidance and best practices to automate processes with workflows:

* Learn more about workflow activities in [this page](https://experienceleague.adobe.com/ja/docs/campaign/automation/workflows/introduction/use-workflow-data){target="_blank"} (Campaign v8 documentation).
* Learn how to build a workflow in [this section](https://experienceleague.adobe.com/ja/docs/campaign/automation/workflows/introduction/build-a-workflow){target="_blank"} (Campaign v8 documentation).
* Discover how to use workflows to import data in Campaign in [this section](../../platform/using/import-export-workflows.md).
* Workflow best practices are detailed in [this page](https://experienceleague.adobe.com/ja/docs/campaign/automation/workflows/introduction/workflow-best-practices){target="_blank"} (Campaign v8 documentation).
* Find guidance about workflow execution in [this section](https://experienceleague.adobe.com/ja/docs/campaign/automation/workflows/executing-a-workflow/start-a-workflow){target="_blank"} (Campaign v8 documentation).
* Learn how to monitor workflows in [this page](https://experienceleague.adobe.com/ja/docs/campaign/automation/workflows/monitoring-workflows/monitor-workflow-execution){target="_blank"} (Campaign v8 documentation).
* Learn how to grant access to users to use workflows in [this page](https://experienceleague.adobe.com/ja/docs/campaign/automation/workflows/advanced-management/managing-rights){target="_blank"} (Campaign v8 documentation).

-->