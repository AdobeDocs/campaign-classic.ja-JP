---
product: campaign
title: アーキテクチャ
description: ワークフローは特定のモジュールによって処理され、複数のサーバーで開始して、処理の負荷を分散することができます
badge-v7-only: label="v7" type="Informative" tooltip="Applies to Campaign Classic v7 only"
feature: Workflows
exl-id: 46801f78-706c-4dfa-bce7-3d15f569f222
source-git-commit: 8debcd3d8fb883b3316cf75187a86bebf15a1d31
workflow-type: tm+mt
source-wordcount: '116'
ht-degree: 81%

---

# アーキテクチャ {#architecture}



ワークフローは特定のモジュールによって処理されます。このモジュールは、複数のサーバーから起動し、処理の負荷を分散することができます。

![](assets/architecture.png)

* 「ワークフローインスタンスランナー」（runwf）プロセスは、所定のワークフローインスタンスのすべてのタスクを実行します。一定期間、実行されるタスクがない場合、プロセスは「passive」になります。つまり、データベース内でステータスを保存し、停止します。
* 「ワークフローサーバー」（wfserver）モジュールは、現在のワークフローインスタンスを監視します。実行するタスクがある場合、このモジュールは対応するインスタンスを有効化（または再有効化）するプロセスを作成します。
