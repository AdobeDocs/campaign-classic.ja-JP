---
title: テンプレートへのルーティング
seo-title: テンプレートへのルーティング
description: テンプレートへのルーティング
seo-description: null
page-status-flag: never-activated
uuid: 1f8252c4-7f96-4759-9544-39b8f854961f
contentOwner: sauviat
products: SG_CAMPAIGN/CLASSIC
audience: message-center
content-type: reference
topic-tags: event-processing
discoiquuid: 8fa464e6-3c88-441c-8179-0c54960469a7
index: y
internal: n
snippet: y
translation-type: ht
source-git-commit: 579329d9194115065dff2c192deb0376c75e67bd

---


# テンプレートへのルーティング{#routing-towards-a-template}

メッセージテンプレートが実行インスタンスにパブリッシュされると、リアルタイムイベントまたはバッチイベントにリンクされる 2 つのテンプレートが自動的に生成されます。ルーティングの手順では、イベントを適切なメッセージテンプレートにリンクします。リンクは、イベント自身のプロパティおよびテンプレートのプロパティで指定されているイベントタイプに基づいておこなわれます。

イベントプロパティ内のイベントタイプ定義：

![](assets/messagecenter_event_type_001.png)

メッセージテンプレートプロパティ内のイベントタイプの定義：

![](assets/messagecenter_event_type_002.png)

デフォルトでは、ルーティングは次の情報に基づいておこなわれます。

* イベントタイプ
* 使用するチャネル（デフォルトは E メール）
* パブリッシュ日に基づく最新の配信テンプレート

