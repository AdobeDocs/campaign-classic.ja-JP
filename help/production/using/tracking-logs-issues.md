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

トラッキングログが転送されない理由は複数考えられます。 次の情報を確認することをお勧めします。

* **トラッキングワ****ークフローにエラーがあるか。**

   [ テクニカルワークフローの監視 ](../../workflow/using/monitoring-technical-workflows.md) を参照してください。

   ![](assets/tracking_scheduled_task.png)

* **モジュールがサーバー上****で酔っ払いを追跡しているか。**

   [ ログファイル ](../../production/using/log-files.md) を参照してください。

* **変更が加えられたか。**

   トラッキングエイリアスを使用して、トリガーとサーバーとの接続が失われる可能性があります。
