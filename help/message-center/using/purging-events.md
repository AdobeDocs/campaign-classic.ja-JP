---
solution: Campaign Classic
product: campaign
title: イベントのパージ
description: イベントのパージ
audience: message-center
content-type: reference
topic-tags: instance-configuration
exl-id: 275a333b-70cc-4549-ac52-ac8ce54c2805
translation-type: ht
source-git-commit: 6854d06f8dc445b56ddfde7777f02916a60f2b63
workflow-type: ht
source-wordcount: '90'
ht-degree: 100%

---

# イベントのパージ{#purging-events}

[デプロイメントウィザード](../../production/using/database-cleanup-workflow.md#deployment-wizard)を使用し、データをデータベース上に保存する期間を設定できます。

イベントのパージは、[データベースクリーンアップワークフロー](../../production/using/database-cleanup-workflow.md)によって自動的に実行されます。このワークフローは、実行インスタンスが受信し保存したイベントおよびコントロールインスタンスがアーカイブしたイベントをパージします。

矢印を使用し、必要に応じてパージの設定を変更します。

コントロールインスタンスのイベントパージ設定：

![](assets/messagecenter_delete_events_001.png)

実行インスタンスのイベントパージ設定：

![](assets/messagecenter_delete_events_002.png)

データベースクリーンアップワークフローについて詳しくは、[この節](../../production/using/database-cleanup-workflow.md)を参照してください。
