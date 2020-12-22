---
solution: Campaign Classic
product: campaign
title: イベントのパージ
description: イベントのパージ
audience: message-center
content-type: reference
topic-tags: instance-configuration
translation-type: tm+mt
source-git-commit: 5bc6c8a824929c6a61cf562fc961e5bdd1867837
workflow-type: tm+mt
source-wordcount: '90'
ht-degree: 66%

---


# イベントのパージ{#purging-events}

[展開ウィザード](../../production/using/database-cleanup-workflow.md#deployment-wizard)を使用して、データをデータベースに格納する期間を設定できます。

イベントの削除は、[データベースのクリーンアップワークフロー](../../production/using/database-cleanup-workflow.md)によって自動的に行われます。 このワークフローは、実行インスタンスが受信し保存したイベントおよびコントロールインスタンスがアーカイブしたイベントをパージします。

矢印を使用し、必要に応じてパージの設定を変更します。

コントロールインスタンスのイベントパージ設定：

![](assets/messagecenter_delete_events_001.png)

実行インスタンスのイベントパージ設定：

![](assets/messagecenter_delete_events_002.png)

データベースクリーンアップワークフローについて詳しくは、[この節](../../production/using/database-cleanup-workflow.md)を参照してください。
