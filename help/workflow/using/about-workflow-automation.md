---
product: campaign
title: ワークフローについて
description: ワークフローを使用すれば、データおよびオーディエンスの管理やメッセージの送信などのプロセスを自動化できます
feature: Workflows, Data Management
exl-id: 024a7344-9376-4ff3-926a-003148229f9f
source-git-commit: dd6bcb16fe41b6a3f1e3f5aaf2f753b29ad4bc1d
workflow-type: ht
source-wordcount: '274'
ht-degree: 100%

---

# ワークフローを使用した自動化 {#gs-workflows}

Adobe Campaign に含まれているワークフローモジュールを使用すると、アプリケーションサーバーのさまざまなモジュールにわたり、すべての範囲のプロセスとタスクを調整できます。総合的なグラフィカル環境により、セグメント化、キャンペーン実行、ファイル処理、手作業での処理などのプロセスをデザインできます。これらのプロセスは、ワークフローエンジンが実行し、トラッキングします。

例えば、ワークフローを使用して、サーバーからファイルをダウンロードしたり、ファイルを解凍したり、ファイルに含まれるレコードを Adobe Campaign データベースにインポートしたりできます。

またワークフローには、1 人または複数のオペレーターを関連付けて、通知の対象とすることや、プロセスの選択や承認に関与させることもできます。この方法により、配信アクションを作成して 1 人または複数のオペレーターにタスクを割り当て、コンテンツに対して作業する、ターゲットを指定する、配信開始前に配達確認を承認する、などが可能になります。

ワークフローは、キャンペーン管理プロセスの様々なコンテキストおよびステージで発生します。

ワークフロー管理について詳しくは、[Campaign v8 ドキュメント](https://experienceleague.adobe.com/docs/campaign/automation/workflows/introduction/about-workflows.html?lang=ja){target=_blank}を参照してください。

![](assets/do-not-localize/workflow.jpg){width="40%"}

ワークフロー管理に関連する主な手順について説明します。

* [ワークフローアクティビティ](https://experienceleague.adobe.com/docs/campaign/automation/workflows/wf-activities/activities.html?lang=ja){target=_blank}：アクティビティは、タスクテンプレートを図示したものです。ワークフローには、ターゲティング、フロー制御、アクションおよびイベントアクティビティが含まれます。

* [ワークフローの作成](https://experienceleague.adobe.com/docs/campaign/automation/workflows/introduction/build-a-workflow.html?lang=ja){target=_blank}：ターゲティング、キャンペーン、テクニカルワークフローの作成および実行方法について説明します。

* [ベストプラクティス](https://experienceleague.adobe.com/docs/campaign/automation/workflows/introduction/workflow-best-practices.html?lang=ja){target=_blank}：Campaign ワークフローのパフォーマンスを最適化し、ワークフローのデザインを改善し、正しい設定を選択するためのガイドラインについて説明します。

* [ワークフローの監視](https://experienceleague.adobe.com/docs/campaign/automation/workflows/monitoring-workflows/monitor-workflow-execution.html?lang=ja){target=_blank}：ワークフローの実行を監視して、すべてが正しく実行されていることを確認する方法について説明します。

* [ワークフローのユースケース](https://experienceleague.adobe.com/docs/campaign/automation/workflows/use-cases/workflow-use-cases.html?lang=ja){target=_blank}：ワークフローを使用できる様々なコンテキストと、エンドツーエンドのユースケースを通じてワークフローを実装する方法について説明します。

<!--

Adobe Campaign uses workflows to:

* Carry out targeting campaigns. [Learn more](building-a-workflow.md#implementation-steps-)
* Build campaigns: for each campaign, the **[!UICONTROL Workflow]** tab lets you build the target and create the deliveries. [Learn more](building-a-workflow.md#campaign-workflows)
* Perform technical processes: cleanup, collecting tracking information or provisional calculations. [Learn more](building-a-workflow.md#technical-workflows)

A workflow can mean both a process definition (the workflow model, which is a representation of what is supposed to happen) and an instance of this process (a workflow instance, which is a representation of what is actually happening).

The workflow template describes the various tasks to be performed and how they are linked together. The task templates are called activities and are represented by icons. They are linked together by transitions.

![](assets/example1.png)

Each workflow contains:

* **[!UICONTROL Activities]**

  An activity describes a task template. The various activities available are represented on the diagram by icons. Each type has common properties and specific properties. For example, while all activities have a name and label, only the **[!UICONTROL Approval]** activity has an assignment.

  In a workflow diagram, a given activity can produce multiple tasks, in particular when there is a loop or recurrent (periodic) actions.

  All workflow activities are listed in [this section](about-activities.md), including use cases and samples.

* **[!UICONTROL Transitions]**

  Transitions enable you to link activities and to define their sequence. A transition links a source activity to a destination activity. There are several sorts of transitions, which depend on the source activity. Some transitions have additional parameters such as a duration, a condition or a filter.

  A transition which is not linked to a destination activity is colored orange and the arrow head is shown as a diamond.

  >[!NOTE]
  >
  >A workflow containing unterminated transitions can still be executed: a warning message will be generated and the workflow will pause once it reaches the transition but it will not generate an error. It is thus possible to start a workflow without it being finished and to add to it as you go along.

  For more information about how to build a workflow, refer to [this section](building-a-workflow.md).

* **[!UICONTROL Worktables]**

  The worktable contains all the information carried by the transition. Each workflow uses several worktables. The data conveyed in these tables can be accelerated and used throughout the workflow's life cycle, as long as it is not purged. Indeed, unneeded tables are purged each time the workflow is passivated, and possibly during the execution of the largest workflows to avoid overloading the server.

  Learn more on workflow data and tables in [this section](how-to-use-workflow-data.md).

## Key principles and best practices{#principles-workflows}

Refer to these sections to find guidance and best practices to automate processes with workflows:

* Learn more about workflow activities in [this page](how-to-use-workflow-data.md).
* Learn how to build a workflow in [this section](building-a-workflow.md).
* Discover how to use workflows to import data in Campaign in [this section](../../platform/using/import-export-workflows.md).
* Workflow best practices are detailed in [this page](workflow-best-practices.md).
* Find guidance about workflow execution in [this section](starting-a-workflow.md).
* Learn how to monitor workflows in [this page](monitoring-workflow-execution.md).
* Learn how to grant access to users to use workflows in [this page](managing-rights.md).

-->