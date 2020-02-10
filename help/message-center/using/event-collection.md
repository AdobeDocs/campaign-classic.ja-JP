---
title: イベントの収集
seo-title: イベントの収集
description: イベントの収集
seo-description: null
page-status-flag: never-activated
uuid: 8c373962-40d4-4982-9bd1-ce1cf8261dd5
contentOwner: sauviat
products: SG_CAMPAIGN/CLASSIC
audience: message-center
content-type: reference
topic-tags: event-processing
discoiquuid: cfff302a-6ac0-461a-a1e4-8e4b617fe134
index: y
internal: n
snippet: y
translation-type: tm+mt
source-git-commit: 20f835c357d016643ea1f3209ee4dfb6d3239f90

---


# イベントの収集{#event-collection}

情報システムによって生成されたイベントは、次の 2 つのモードを使用して収集できます。

* SOAP メソッドの呼び出しでは Adobe Campaign 内でイベントをプッシュすることができます。PushEvent メソッドはイベントを 1 つずつ送信し、PushEvents メソッドは複数のイベントを一度に送信します。イベントの説 [明を参照](../../message-center/using/event-description.md)。
* ワークフローを作成すると、ファイルのインポートまたは SQL ゲートウェイ経由（「**Federated Data Access**」オプションを使用）でイベントを復元することができます。

回収されたイベントは、テクニカルワークフローによって実行インスタンスのリアルタイムキューとバッチキューに分別され、メッセージテンプレートにリンクされるのを待つことになります。

![](assets/messagecenter_events_queues_001.png)

