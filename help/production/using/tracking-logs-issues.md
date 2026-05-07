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
source-wordcount: '81'
ht-degree: 32%

---

# トラッキングログの問題{#tracking-logs-issues}



トラッキングログが転送されない理由は複数あります。 次の情報を確認することをお勧めします。

* **&#x200B;**&#x200B;トラッキング **ワークフローにエラーがありますか？**

[Campaign v8 ドキュメント](https://experienceleague.adobe.com/docs/campaign/automation/workflows/monitoring-workflows/monitor-technical-workflows.html?lang=ja){target="_blank"}を参照してください。

![](assets/tracking_scheduled_task.png)

* **モジュール** trackinglogd **はサーバー上で実行されていますか？**

  [&#x200B; ログファイル &#x200B;](../../production/using/log-files.md)を参照してください。

* **変更が行われましたか？**

  トラッキングエイリアスを使用すると、サーバへの接続が失われることをトリガーできます。
