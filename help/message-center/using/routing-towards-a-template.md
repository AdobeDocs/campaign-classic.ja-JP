---
solution: Campaign Classic
product: campaign
title: テンプレートへのルーティング
description: テンプレートへのルーティング
audience: message-center
content-type: reference
topic-tags: event-processing
translation-type: tm+mt
source-git-commit: 972885c3a38bcd3a260574bacbb3f507e11ae05b
workflow-type: tm+mt
source-wordcount: '121'
ht-degree: 100%

---


# テンプレートへのルーティング{#routing-towards-a-template}

メッセージテンプレートが実行インスタンスに公開されると、リアルタイムイベントまたはバッチイベントにリンクされる 2 つのテンプレートが自動的に生成されます。ルーティングの手順では、イベントを適切なメッセージテンプレートにリンクします。リンクは、イベント自身のプロパティおよびテンプレートのプロパティで指定されているイベントタイプに基づいておこなわれます。

イベントプロパティ内のイベントタイプ定義：

![](assets/messagecenter_event_type_001.png)

メッセージテンプレートプロパティ内のイベントタイプの定義：

![](assets/messagecenter_event_type_002.png)

デフォルトでは、ルーティングは次の情報に基づいておこなわれます。

* イベントタイプ
* 使用するチャネル（デフォルトは E メール）
* 公開日に基づく最新の配信テンプレート
