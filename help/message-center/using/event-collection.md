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
translation-type: tm+mt
source-git-commit: 95dff2f3704e316e9ec9e454a8f3fb9835508ccd
workflow-type: tm+mt
source-wordcount: '106'
ht-degree: 50%

---


# イベントの収集{#event-collection}

情報システムによって生成されたイベントは、次の 2 つのモードを使用して収集できます。

* SOAPメソッドの呼び出しを使用すると、Adobe Campaign内のイベントをプッシュできます。PushEventメソッドを使用すると、一度に1つのイベントを送信でき、PushEventsメソッドを使用すると複数のイベントを一度に送信できます。 [イベントの説明](../../message-center/using/event-description.md)を参照してください。
* Creating a workflow lets you recover events by importing files or via an SQL gateway (with the **Federated Data Access** option).

回収されたイベントは、テクニカルワークフローによって実行インスタンスのリアルタイムキューとバッチキューに分別され、メッセージテンプレートにリンクされるのを待つことになります。

![](assets/messagecenter_events_queues_001.png)
