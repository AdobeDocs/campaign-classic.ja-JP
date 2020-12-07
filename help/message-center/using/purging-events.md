---
solution: Campaign Classic
product: campaign
title: イベントのパージ
description: イベントのパージ
audience: message-center
content-type: reference
topic-tags: instance-configuration
translation-type: ht
source-git-commit: 972885c3a38bcd3a260574bacbb3f507e11ae05b
workflow-type: ht
source-wordcount: '90'
ht-degree: 100%

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
