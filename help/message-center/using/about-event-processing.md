---
solution: Campaign Classic
product: campaign
title: イベントの処理
description: Adobe Campaign Classicでのトランザクションメッセージイベントの処理方法を説明します。
audience: message-center
content-type: reference
topic-tags: event-processing
exl-id: 3d85866a-6339-458c-807a-b267cce772b8
source-git-commit: c41ca3d518391a648629ebc3fcd4c916e92c3a79
workflow-type: tm+mt
source-wordcount: '711'
ht-degree: 43%

---

# イベントの処理 {#about-event-processing}

トランザクションメッセージのコンテキストでは、イベントは、外部の情報システムによって生成され、 **[!UICONTROL PushEvent]**&#x200B;および&#x200B;**[!UICONTROL PushEvents]**&#x200B;メソッドを介してAdobe Campaignに送信されます（ [イベントの説明](../../message-center/using/event-description.md)を参照）。

このイベントには、[type](../../message-center/using/creating-event-types.md)（注文確認、Webサイトでのアカウント作成など）、Eメールアドレスや携帯電話番号、および配信前にトランザクションメッセージ（顧客連絡先情報、メッセージの言語、Eメールフォーマットなど）をエンリッチメントおよびパーソナライズする情報が含まれます。

イベントデータの例：

![](assets/messagecenter_events_request_001.png)

## イベント処理手順{#event-processing}

トランザクションメッセージイベントを処理するには、次の手順を実行インスタンスに適用します。

1. [イベントの収集](#event-collection)
1. [メッセージテンプレートへのイベント転送](#routing-towards-a-template)
1. パーソナライゼーションデータを使用したイベントの強化
1. [配信の実行](../../message-center/using/delivery-execution.md)
1. [リンクされた配](#event-recycling) 信に失敗したイベントの再利用(Adobe Campaignワークフロー経由)

上記のすべての手順が実行インスタンスを通じて実行されると、各ターゲット受信者にパーソナライズされたメッセージが届きます。

>[!NOTE]
>
>トランザクションメッセージインスタンスについて詳しくは、[トランザクションメッセージのアーキテクチャ](../../message-center/using/transactional-messaging-architecture.md)を参照してください。


## イベントの収集 {#event-collection}

情報システムによって生成されたイベントは、次の 2 つのモードを使用して収集できます。

* SOAPメソッドの呼び出しにより、Adobe Campaignでイベントをプッシュできます。PushEventメソッドではイベントを1つずつ送信し、PushEventsメソッドでは複数のイベントを一度に送信します。 詳しくは、[イベントの説明](../../message-center/using/event-description.md)を参照してください。

* ワークフローを作成すると、ファイルのインポートまたは SQL ゲートウェイ経由（「[Federated Data Access](../../installation/using/about-fda.md)」オプションを使用）でイベントを復元することができます。

収集されたイベントは、実行インスタンスのリアルタイムキューとバッチキューの間のテクニカルワークフローによって分類され、メッセージテンプレートにリンクされるのを待ちます。

![](assets/messagecenter_events_queues_001.png)

>[!NOTE]
>
>実行インスタンス上では、**[!UICONTROL リアルタイムイベント]**&#x200B;フォルダーまたは&#x200B;**[!UICONTROL バッチイベント]**&#x200B;フォルダーをビューとして設定しないでください。アクセス権の問題が発生するおそれがあるからです。 フォルダーをビューとして設定する方法について詳しくは、[この節](../../platform/using/access-management-folders.md)を参照してください。

## テンプレートへのルーティング {#routing-towards-a-template}

メッセージテンプレートが実行インスタンスに公開されると、2つのテンプレートが自動的に生成されます。1つはリアルタイムイベントにリンクされ、もう1つはバッチイベントにリンクされます。

ルーティングの手順では、次の条件に基づいて、イベントを適切なメッセージテンプレートにリンクします。

* イベント自体のプロパティで指定されるイベントタイプ。

   ![](assets/messagecenter_event_type_001.png)

* メッセージテンプレートのプロパティで指定されたイベントタイプ：

   ![](assets/messagecenter_event_type_002.png)

デフォルトでは、ルーティングは次の情報に基づいています。

* イベントタイプ
* 使用するチャネル（デフォルトは E メール）
* 公開日に基づく最新の配信テンプレート

## イベントのステータス {#event-statuses}

**イベント履歴**（**[!UICONTROL Message Center]**／**[!UICONTROL イベント履歴]**）は、処理されたすべてのイベントを 1 つのビューにまとめます。イベントは、イベントタイプまたは&#x200B;**ステータス**&#x200B;ごとに分類することができます。イベントのステータスは以下のとおりです。

* **保留中**:イベントは次のいずれかになります。

   * 収集されたばかりで処理されていないイベント。**[!UICONTROL エラー数]**&#x200B;列に値0が表示されます。 E メールテンプレートはまだリンクされていません。
   * 処理されたが、確認でエラーになったイベント。 **[!UICONTROL エラー数]**&#x200B;列に 0 以外の値が表示されます。このイベントが再処理される日付については、**[!UICONTROL 処理リクエスト日]**&#x200B;の列を参照してください。

* **配信待ち**:イベントは処理され、配信テンプレートがリンクされます。E メールは配信待ちとなり、標準的な配信処理が適用されます。詳しくは、[配信](../../delivery/using/about-message-tracking.md)を開いてください。
* **送信済み**、 **** 無視および **配信エラー**:これらの配信ステータスは、 updateEventsStatusworkflowを使用して復 **** 元します。詳しい情報を見るには、該当する配信を開いてください。
* **対象外のイベント**:トランザクションメッセージルーティングフェーズが失敗しました。例えば、Adobe Campaign がこのイベントのテンプレートとなる E メールを見つけられなかった場合などです。
* **期限切れのイベント**:送信試行の最大数に達しました。このイベントは空とみなされます。

## イベントの再利用 {#event-recycling}

特定のチャネルでのメッセージ配信に失敗した場合、Adobe Campaign は別のチャネルでメッセージを再送信することができます。例えば、SMS チャネルでの配信に失敗した場合、E メールチャネルを利用してメッセージを再送信します。

これには、ステータスが **Delivery error** であるすべてのイベントを再度作成し、異なるチャネルを割り当てるワークフローを設定する必要があります。

>[!CAUTION]
>
>この手順の実行は、ワークフローを使用する必要があるので、エキスパートユーザー向けの操作となります。詳しくは、アドビのアカウント担当者にお問い合わせください。