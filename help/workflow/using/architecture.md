---
product: campaign
title: アーキテクチャ
description: ワークフローは特定のモジュールによって処理され、複数のサーバーから起動し、処理の負荷を分散することができます。
audience: workflow
content-type: reference
topic-tags: -general-operation
exl-id: 46801f78-706c-4dfa-bce7-3d15f569f222
source-git-commit: 20509f44c5b8e0827a09f44dffdf2ec9d11652a1
workflow-type: tm+mt
source-wordcount: '116'
ht-degree: 100%

---

# アーキテクチャ {#architecture}

![](../../assets/common.svg)

ワークフローは特定のモジュールによって処理されます。このモジュールは、複数のサーバーから起動し、処理の負荷を分散することができます。

![](assets/architecture.png)

* 「ワークフローインスタンスランナー」（runwf）プロセスは、所定のワークフローインスタンスのすべてのタスクを実行します。一定期間、実行されるタスクがない場合、プロセスは「passive」になります。つまり、データベース内でステータスを保存し、停止します。
* 「ワークフローサーバー」（wfserver）モジュールは、現在のワークフローインスタンスを監視します。実行するタスクがある場合、このモジュールは対応するインスタンスを有効化（または再有効化）するプロセスを作成します。
