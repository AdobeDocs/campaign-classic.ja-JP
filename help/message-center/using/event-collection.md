---
solution: Campaign Classic
product: campaign
title: イベントの収集
description: イベントの収集
audience: message-center
content-type: reference
topic-tags: event-processing
translation-type: ht
source-git-commit: 972885c3a38bcd3a260574bacbb3f507e11ae05b
workflow-type: ht
source-wordcount: '104'
ht-degree: 100%

---


# イベントの収集{#event-collection}

情報システムによって生成されたイベントは、次の 2 つのモードを使用して収集できます。

* SOAP メソッドの呼び出しでは Adobe Campaign 内でイベントをプッシュすることができます。PushEvent メソッドはイベントを 1 つずつ送信し、PushEvents メソッドは複数のイベントを一度に送信します。[イベントの説明](../../message-center/using/event-description.md)を参照してください。
* ワークフローを作成すると、ファイルのインポートまたは SQL ゲートウェイ経由（「**Federated Data Access**」オプションを使用）でイベントを復元することができます。

回収されたイベントは、テクニカルワークフローによって実行インスタンスのリアルタイムキューとバッチキューに分別され、メッセージテンプレートにリンクされるのを待つことになります。

![](assets/messagecenter_events_queues_001.png)
