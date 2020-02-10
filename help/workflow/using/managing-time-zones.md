---
title: タイムゾーンの管理
seo-title: タイムゾーンの管理
description: タイムゾーンの管理
seo-description: null
page-status-flag: never-activated
uuid: a253861a-fc15-406d-969d-33cfb4169839
contentOwner: sauviat
products: SG_CAMPAIGN/CLASSIC
audience: workflow
content-type: reference
topic-tags: advanced-management
discoiquuid: 8bcbcd23-9251-412a-ae72-11f15db74112
index: y
internal: n
snippet: y
translation-type: tm+mt
source-git-commit: c10a0a11c6e9952aa47da1f7a15188c79c62508d

---


# タイムゾーンの管理{#managing-time-zones}

Adobe Campaign では、関係するさまざまな国の間のタイムラグを、同じインスタンスで管理できます。適用する設定は、インスタンスの作成中に設定できます。

Adobe Campaign でのタイムゾーンの設定について詳しくは、この[節](../../installation/using/time-zone-management.md)を参照してください。

ワークフローでは、アクティビティの実行スケジュールを変更したり、固有のタイムゾーンをアクティビティやワークフロー全体とリンクしたりすることができます。この設定は、ファイルをインポートするときや、配信のスケジュール設定のフレームワークで役立ちます。

## 実行スケジュールの設定 {#execution-scheduling}

You can schedule the execution of tasks using the scheduler (refer to [Scheduler](../../workflow/using/scheduler.md)). アクティビティのスケジュール設定オプションでも同じことができます。以下のアクティビティにはタブが **[!UICONTROL Schedule]** あります。 **[!UICONTROL File collector]**、 **[!UICONTROL File transfer]**、 **[!UICONTROL Web download]**、 **[!UICONTROL Email reception]** お **[!UICONTROL SMS]**&#x200B;よびなど

スケジュール対象のすべてのタスク、すなわち、スケジュール設定オプションのあるアクティビティすべてについて、適用するタイムゾーンが選択できます。The time zone is selected via the **[!UICONTROL Advanced]** tab of the concerned activity:

![](assets/wf-timezone-in-a-box.png)

次のような値を選択できます。

* サーバーのタイムゾーン

   Adobe Campaign アプリケーションサーバーのタイムゾーンを使用します。

* ユーザーのタイムゾーン

   ワークフローを実行する Adobe Campaign オペレーターのタイムゾーンを使用します。

* データベースのタイムゾーン

   使用するデータベースサーバーのタイムゾーンを使用します。

* 固有のタイムゾーン

   選択したタイムゾーンを使用します。

If the **[!UICONTROL By default]** value is selected, the time zone of the workflow is applied, or, otherwise, that of the application server.

## タイムゾーンとアクティビティとのリンク {#linking-a-time-zone-to-an-activity}

The **[!UICONTROL Advanced]** tab of the workflow activities lets you select its time zone. ほとんどの場合、ワークフローのタイムゾーンを用意するだけで十分ですが、データのインポートのような特定のアクティビティの場合、タイムゾーンを時々オーバーロードして、日付を正しいタイムゾーンとリンクさせることが必要になる場合があります。
