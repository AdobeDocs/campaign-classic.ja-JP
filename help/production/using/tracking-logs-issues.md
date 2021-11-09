---
product: campaign
title: トラッキングログの問題
description: トラッキングログの問題
audience: production
content-type: reference
topic-tags: troubleshooting
exl-id: 58656aa1-aa95-451f-80b8-9e2d28223056
source-git-commit: 20509f44c5b8e0827a09f44dffdf2ec9d11652a1
workflow-type: tm+mt
source-wordcount: '69'
ht-degree: 13%

---

# トラッキングログの問題{#tracking-logs-issues}

![](../../assets/v7-only.svg)

トラッキングログが転送されない複数の理由が考えられます。 次の情報を確認することをお勧めします。

* **を実行します。**&#x200B;トラッキング&#x200B;**エラーが発生した場合は、**

   参照： [テクニカルワークフローの監視](../../workflow/using/monitoring-technical-workflows.md).

   ![](assets/tracking_scheduled_task.png)

* **モジュールです** trackinglogd **サーバ上で実行しているか**

   参照： [ログファイル](../../production/using/log-files.md).

* **変更が加えられたか。**

   トラッキングエイリアスを使用して、トリガーとサーバーとの接続が失われる可能性があります。
