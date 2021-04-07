---
solution: Campaign Classic
product: campaign
title: イベントの収集
description: イベントの収集
audience: message-center
content-type: reference
topic-tags: event-processing
translation-type: ht
source-git-commit: 693e38477b318ee44e0373a04d8524ddf128fe36
workflow-type: ht
source-wordcount: '143'
ht-degree: 100%

---


# イベントの収集{#event-collection}

情報システムによって生成されたイベントは、次の 2 つのモードを使用して収集できます。

* SOAP メソッドの呼び出しでは Adobe Campaign 内でイベントをプッシュすることができます。PushEvent メソッドはイベントを 1 つずつ送信し、PushEvents メソッドは複数のイベントを一度に送信します。[イベントの説明](../../message-center/using/event-description.md)を参照してください。
* ワークフローを作成すると、ファイルのインポートまたは SQL ゲートウェイ経由（「**Federated Data Access**」オプションを使用）でイベントを復元することができます。

回収されたイベントは、テクニカルワークフローによって実行インスタンスのリアルタイムキューとバッチキューに分別され、メッセージテンプレートにリンクされるのを待つことになります。

![](assets/messagecenter_events_queues_001.png)

>[!NOTE]
>
>実行インスタンス上では、**[!UICONTROL リアルタイムイベント]**&#x200B;フォルダーまたは&#x200B;**[!UICONTROL バッチイベント]**&#x200B;フォルダーをビューとして設定しないでください。アクセス権の問題が発生するおそれがあるからです。 フォルダーをビューとして設定する方法について詳しくは、[この節](../../platform/using/access-management-folders.md)を参照してください。
