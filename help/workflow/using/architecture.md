---
product: campaign
title: アーキテクチャ
description: ワークフローは特定のモジュールによって処理され、複数のサーバーから起動し、処理の負荷を分散することができます
feature: Workflows
hide: true
hidefromtoc: true
exl-id: 46801f78-706c-4dfa-bce7-3d15f569f222
source-git-commit: 776c664a99721063dce5fa003cf40c81d94f8c78
workflow-type: tm+mt
source-wordcount: '116'
ht-degree: 100%

---

# アーキテクチャ {#architecture}



ワークフローは特定のモジュールによって処理されます。このモジュールは、複数のサーバーから起動し、処理の負荷を分散することができます。

![](assets/architecture.png)

* 「ワークフローインスタンスランナー」（runwf）プロセスは、所定のワークフローインスタンスのすべてのタスクを実行します。一定期間、実行されるタスクがない場合、プロセスは「passive」になります。つまり、データベース内でステータスを保存し、停止します。
* 「ワークフローサーバー」（wfserver）モジュールは、現在のワークフローインスタンスを監視します。実行するタスクがある場合、このモジュールは対応するインスタンスを有効化（または再有効化）するプロセスを作成します。
