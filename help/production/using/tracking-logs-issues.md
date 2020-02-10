---
title: ログの問題の追跡
seo-title: ログの問題の追跡
description: ログの問題の追跡
seo-description: null
page-status-flag: never-activated
uuid: 996869c4-7ffe-4fcc-9555-1d8b65e93e87
contentOwner: sauviat
products: SG_CAMPAIGN/CLASSIC
audience: production
content-type: reference
topic-tags: troubleshooting
discoiquuid: 1b9ff479-4847-408d-a5c2-9a164805081f
index: y
internal: n
snippet: y
translation-type: tm+mt
source-git-commit: e1937c1ddcbde092a22f4fe8c50d3d72b02cfeed

---


# ログの問題の追跡{#tracking-logs-issues}

トラッキングログが転送されない理由は複数考えられます。 次の情報を確認することをお勧めします。

* 追跡ワークフ **ローに** 、エラーがあるか。

   「技術ワークフロー [の監視」を参照してください](../../workflow/using/monitoring-technical-workflows.md)。

   ![](assets/tracking_scheduled_task.png)

* モジュール **trackinglogdは** 、サーバー上で実行されていますか。

   ログファイル [を参照](../../production/using/log-files.md)。

* 変更は行われましたか。 トラッキングエイリアスを使用して、サーバーへの接続が失われる可能性があります。

