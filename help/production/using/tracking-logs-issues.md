---
product: campaign
title: トラッキングログの問題
description: トラッキングログの問題
feature: Monitoring
audience: production
content-type: reference
topic-tags: troubleshooting
exl-id: 58656aa1-aa95-451f-80b8-9e2d28223056
source-git-commit: b666535f7f82d1b8c2da4fbce1bc25cf8d39d187
workflow-type: tm+mt
source-wordcount: '69'
ht-degree: 13%

---

# トラッキングログの問題{#tracking-logs-issues}



トラッキングログが転送されない理由は複数ある可能性があります。 次の情報を確認することをお勧めします。

* **** トラッキング **ワークフローにエラーはありますか？**

  [ テクニカルワークフローの監視 ](../../workflow/using/monitoring-technical-workflows.md) を参照してください。

  ![](assets/tracking_scheduled_task.png)

* **モジュール** trackinglogd **はサーバーで実行されていますか？**

  [ ログファイル ](../../production/using/log-files.md) を参照してください。

* **変更が加えられましたか？**

  トラッキングエイリアスを使用すると、サーバーへの接続損失のトリガーになる可能性があります。
