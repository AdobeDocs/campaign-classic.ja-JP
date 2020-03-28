---
title: イベントのパージ
seo-title: イベントのパージ
description: イベントのパージ
seo-description: null
page-status-flag: never-activated
uuid: bbce6813-dfa8-418c-9b52-06e814c15265
contentOwner: sauviat
products: SG_CAMPAIGN/CLASSIC
audience: message-center
content-type: reference
topic-tags: instance-configuration
discoiquuid: 2f643080-93b4-4c9f-80cf-b1770b149e6c
index: y
internal: n
snippet: y
translation-type: ht
source-git-commit: 20f835c357d016643ea1f3209ee4dfb6d3239f90

---


# イベントのパージ{#purging-events}

デプロイウィザードを使用し、データをデータベース上に保存する期間の設定をおこなうことができます。

イベントのパージは、**[!UICONTROL データベースクリーンアップ]**&#x200B;ワークフローによって自動的に実行されます。このワークフローは、実行インスタンスが受信し保存したイベントおよびコントロールインスタンスがアーカイブしたイベントをパージします。

矢印を使用し、必要に応じてパージの設定を変更します。

コントロールインスタンスのイベントパージ設定：

![](assets/messagecenter_delete_events_001.png)

実行インスタンスのイベントパージ設定：

![](assets/messagecenter_delete_events_002.png)

データベースクリーンアップワークフローについて詳しくは、[この節](../../production/using/database-cleanup-workflow.md)を参照してください。
