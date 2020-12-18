---
solution: Campaign Classic
product: campaign
title: トラッキングログの問題
description: トラッキングログの問題
audience: production
content-type: reference
topic-tags: troubleshooting
translation-type: tm+mt
source-git-commit: 972885c3a38bcd3a260574bacbb3f507e11ae05b
workflow-type: tm+mt
source-wordcount: '69'
ht-degree: 13%

---


# トラッキングログの問題{#tracking-logs-issues}

トラッキングログが転送されない理由は複数考えられます。 次の情報を確認することをお勧めします。

* **追跡**&#x200B;ワークフローにエラーがあるかどうか

   [監視テクニカルワークフロー](../../workflow/using/monitoring-technical-workflows.md)を参照してください。

   ![](assets/tracking_scheduled_task.png)

* モジュール&#x200B;**trackinglogd**&#x200B;はサーバー上で実行されていますか？

   [ログファイル](../../production/using/log-files.md)を参照してください。

* 変更は行われたか。 トラッキングエイリアスを使用して、サーバーとの接続が失われる可能性があります。

