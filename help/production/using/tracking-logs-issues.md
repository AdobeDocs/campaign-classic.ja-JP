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

* **実行**&#x200B;トラッキング&#x200B;**ワークフローにエラーがありますか？**

  こちらを参照してください [テクニカルワークフローの監視](../../workflow/using/monitoring-technical-workflows.md).

  ![](assets/tracking_scheduled_task.png)

* **モジュールです** trackinglogd **サーバーで実行している場合**

  こちらを参照してください [ログファイル](../../production/using/log-files.md).

* **変更が加えられましたか。**

  トラッキングエイリアスを使用すると、サーバーへの接続損失のトリガーになる可能性があります。
