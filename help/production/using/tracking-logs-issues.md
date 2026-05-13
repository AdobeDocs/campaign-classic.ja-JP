---
product: campaign
title: トラッキングログの問題
description: トラッキングログの問題
feature: Monitoring
audience: production
content-type: reference
topic-tags: troubleshooting
exl-id: 58656aa1-aa95-451f-80b8-9e2d28223056
TQID: https://experienceleague.adobe.com/9u8xqAINLPKmeptZOZf94Ms-GiEciCL4nFBaw7SjRss
product_v2:
  - id: dfc56824-e8b9-499e-85d4-21aedb507314
topic_v2:
  - id: c1579802-ddd4-4214-8a91-97b2066abe11
source-git-commit: 4c295c0dabae8aba298390a3da2422a3fa1219f9
workflow-type: tm+mt
source-wordcount: 81
ht-degree: 32%

---

# トラッキングログの問題{#tracking-logs-issues}



トラッキングログが転送されない理由は複数あります。 次の情報を確認することをお勧めします。

* **&#x200B;**&#x200B;トラッキング **ワークフローにエラーがありますか？**

詳しくは、[Campaign v8 ドキュメント](https://experienceleague.adobe.com/docs/campaign/automation/workflows/monitoring-workflows/monitor-technical-workflows.html?lang=ja){target="_blank"}を参照してください。

![](assets/tracking_scheduled_task.png)

* **モジュール** trackinglogd **はサーバー上で実行されていますか？**

  [&#x200B; ログファイル &#x200B;](../../production/using/log-files.md)を参照してください。

* **変更が行われましたか？**

  トラッキングエイリアスを使用すると、サーバへの接続が失われることをトリガーできます。
