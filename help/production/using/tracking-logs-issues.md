---
product: campaign
title: トラッキングログの問題
description: トラッキングログの問題
feature: Monitoring
badge-v7-only: label="v7" type="Informative" tooltip="Campaign Classicv7 にのみ適用"
audience: production
content-type: reference
topic-tags: troubleshooting
exl-id: 58656aa1-aa95-451f-80b8-9e2d28223056
source-git-commit: 3a9b21d626b60754789c3f594ba798309f62a553
workflow-type: tm+mt
source-wordcount: '76'
ht-degree: 13%

---

# トラッキングログの問題{#tracking-logs-issues}



トラッキングログが転送されない複数の理由が考えられます。 次の情報を確認することをお勧めします。

* **を実行します。**&#x200B;トラッキング&#x200B;**エラーが発生した場合は、**

  参照： [テクニカルワークフローの監視](../../workflow/using/monitoring-technical-workflows.md).

  ![](assets/tracking_scheduled_task.png)

* **モジュールですか** trackinglogd **サーバ上で実行しているか**

  参照： [ログファイル](../../production/using/log-files.md).

* **変更が加えられたか。**

  トラッキングエイリアスを使用して、トリガーとサーバーとの接続が失われる可能性があります。
