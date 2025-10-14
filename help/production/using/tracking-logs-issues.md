---
product: campaign
title: トラッキングログの問題
description: トラッキングログの問題
feature: Monitoring
audience: production
content-type: reference
topic-tags: troubleshooting
exl-id: 58656aa1-aa95-451f-80b8-9e2d28223056
source-git-commit: ad6f3f2cf242d28de9e6da5cec100e096c5cbec2
workflow-type: tm+mt
source-wordcount: '71'
ht-degree: 14%

---

# トラッキングログの問題{#tracking-logs-issues}



トラッキングログが転送されない理由は複数ある可能性があります。 次の情報を確認することをお勧めします。

* **** トラッキング **ワークフローにエラーはありますか？**

[Campaign v8 ドキュメント ](https://experienceleague.adobe.com/docs/campaign/automation/workflows/monitoring-workflows/monitor-technical-workflows.html?lang=ja){target="_blank"} を参照してください。

![](assets/tracking_scheduled_task.png)

* **モジュール** trackinglogd **はサーバーで実行されていますか？**

  [ ログファイル ](../../production/using/log-files.md) を参照してください。

* **変更が加えられましたか？**

  トラッキングエイリアスを使用すると、サーバーへの接続損失のトリガーになる可能性があります。
