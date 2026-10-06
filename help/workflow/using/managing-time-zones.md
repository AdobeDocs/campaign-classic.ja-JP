---
product: campaign
title: タイムゾーンの管理
description: タイムゾーンの管理
feature: Workflows
hide: true
exl-id: c2f6033c-30cd-4eb4-adf1-ab2de7510220
TQID: 'https://experienceleague.adobe.com/POlYZz1HCRqIp3TdBvIEsOu1grFmxVgqN1xQ1KnuQlQ'
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
source-wordcount: '297'
ht-degree: 100%
---
# タイムゾーンの管理{#managing-time-zones}



Adobe Campaign では、関係するさまざまな国の間のタイムラグを、同じインスタンスで管理できます。 適用する設定は、インスタンスの作成中に設定できます。

Adobe Campaign でのタイムゾーンの設定について詳しくは、[Campaign Classic v7 インストールガイド](../../installation/using/time-zone-management.md)を参照してください。

ワークフローでは、アクティビティの実行スケジュールを変更したり、固有のタイムゾーンをアクティビティやワークフロー全体とリンクしたりすることができます。 この設定は、ファイルをインポートするときや、配信のスケジュール設定のフレームワークで役立ちます。

## 実行スケジュールの設定 {#execution-scheduling}

スケジューラーを使用して、タスクの実行スケジュールを設定できます（[スケジューラー](scheduler.md)を参照）。 アクティビティのスケジュール設定オプションでも同じことができます。 以下に示すようなアクティビティの「**[!UICONTROL スケジュール]**」タブでこの機能を利用できます。**[!UICONTROL ファイルコレクター]**、**[!UICONTROL ファイル転送]**、**[!UICONTROL Web ダウンロード]**、**[!UICONTROL メール受信]**、**[!UICONTROL SMS]** などがあります。

スケジュール対象のすべてのタスク、すなわち、スケジュール設定オプションのあるアクティビティすべてについて、適用するタイムゾーンが選択できます。 タイムゾーンは、関係するアクティビティの「**[!UICONTROL 詳細設定]**」タブで選択します。

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

**[!UICONTROL デフォルト]**&#x200B;値を選択した場合、ワークフローのタイムゾーンが適用されるか、アプリケーションサーバーのタイムゾーンが適用されます。

## タイムゾーンとアクティビティとのリンク {#linking-a-time-zone-to-an-activity}

ワークフローアクティビティの「**[!UICONTROL 詳細設定]**」タブでは、そのアクティビティのタイムゾーンを選択できます。 ほとんどの場合、ワークフローのタイムゾーンを用意するだけで十分ですが、データのインポートのような特定のアクティビティの場合、タイムゾーンを時々オーバーロードして、日付を正しいタイムゾーンとリンクさせることが必要になる場合があります。
