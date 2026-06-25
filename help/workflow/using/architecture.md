---
product: campaign
title: アーキテクチャ
description: ワークフローは特定のモジュールによって処理され、複数のサーバーから起動し、処理の負荷を分散することができます
feature: Workflows
hide: true
exl-id: 46801f78-706c-4dfa-bce7-3d15f569f222
TQID: https://experienceleague.adobe.com/lQLXeSTFhKRCNhA9SdShd9Nyd1mbNt-KPa-XJw-6wAs
product_v2:
  - id: dfc56824-e8b9-499e-85d4-21aedb507314
feature_v2: []
subfeature_v2:
  - id: ee25c34b-ea50-427b-9369-ba0a160f7d70
  - id: b5f0aaf4-1e48-400d-95ac-6eb3078cf22f
  - id: d1110311-2ca4-442b-be37-088a6db845ee
source-git-commit: 38eab6b8da73163e4476e91c0ef73f25c3f57546
workflow-type: ht
source-wordcount: 116
ht-degree: 100%

---

# アーキテクチャ {#architecture}



ワークフローは特定のモジュールによって処理されます。 このモジュールは、複数のサーバーから起動し、処理の負荷を分散することができます。

![](assets/architecture.png)

* 「ワークフローインスタンスランナー」（runwf）プロセスは、所定のワークフローインスタンスのすべてのタスクを実行します。 一定期間、実行されるタスクがない場合、プロセスは「passive」になります。つまり、データベース内でステータスを保存し、停止します。
* 「ワークフローサーバー」（wfserver）モジュールは、現在のワークフローインスタンスを監視します。 実行するタスクがある場合、このモジュールは対応するインスタンスを有効化（または再有効化）するプロセスを作成します。
