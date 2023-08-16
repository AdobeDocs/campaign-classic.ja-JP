---
product: campaign
title: 配信の実行
description: トランザクションメッセージ配信の実行と監視についての詳細情報
feature: Transactional Messaging, Message Center, Monitoring
badge-v7-only: label="v7" type="Informative" tooltip="Campaign Classic v7 にのみ適用されます"
audience: message-center
content-type: reference
topic-tags: event-processing
exl-id: 930c6395-0c00-40ee-a925-3e0cae67c55f
source-git-commit: 3a9b21d626b60754789c3f594ba798309f62a553
workflow-type: tm+mt
source-wordcount: '250'
ht-degree: 100%

---

# 配信の実行 {#delivery-execution}



## トランザクションメッセージの送信 {#transactional-message-send}

実行インスタンスは、エンリッチメントステージが完了し、イベントに配信テンプレートをリンクすると、配信を送信します。

>[!NOTE]
>
>MTA は、トランザクションメッセージの処理を他のどの配信よりも優先します。

すべての配信は、**[!UICONTROL 管理／プロダクション／Message Center／デフォルト／配信]**&#x200B;フォルダーにまとめられます。

![](assets/messagecenter_deliveries_execinstances_001.png)

デフォルトでは、配信は配信月ごとにサブフォルダーに並べ替えられます。この並べ替えは、以下に示されるように、メッセージテンプレートのプロパティで変更することができます。

![](assets/messagecenter_deliveries_properties_001.png)

>[!NOTE]
>
>ホストインストールまたはハイブリッドインストールでは、[Enhanced MTA](../../delivery/using/sending-with-enhanced-mta.md) にアップグレードしている場合、配信品質、スループットおよびバウンス処理を向上させるために、すべてのトランザクションメッセージも Adobe Campaign Enhanced MTA と共に送信される場合があります。この変更による影響はすべて、標準のマーケティングメッセージと同じです。

## トランザクションメッセージの監視 {#transactional-message-monitoring}

トランザクションメッセージを監視するには、[配信ログ](../../delivery/using/delivery-dashboard.md#delivery-logs-and-history)を確認します。

実行インスタンスから送信されるトランザクション配信は、1 時間ごとに実行されるテクニカルワークフロー（**[!UICONTROL Message Center 実行インスタンス]**）を通じてコントロールインスタンスに同期されます。

>[!NOTE]
>
>配信は、イベント作成日ではなく、最新のイベント更新に基づいて、毎週イベントを累積します。したがって、コントロールインスタンスからトランザクションメッセージング配信ログを抽出する場合、各配信ログ ID に関連付けられている配信 ID は、ログが更新されると、時間の経過と共に変わる場合があります（例えば、イベントに対して受信したバウンス）。

<!--The transactional deliveries sent from the execution instance are synchronized back to the control instance as follows.

Let's take a [delivery template](../../message-center/using/introduction.md) labelled *Template_1*.

1. An event corresponding to *Template_1* is received on the execution instance.
1. The **Processing real time events** (rtEventsProcessing) workflow processes the event and searches for an existing delivery for the current month.

    >[!NOTE]
    >
    >If not found, a new delivery is created and the event is assigned to the new delivery.

1. The transactional email is sent and the delivery status changes to **[!UICONTROL Sent]**.
1. The **Message Center execution instance** (mcSync_mcExec) workflow retrieves the delivery logs from the execution instance and updates the delivery logs on the control instance.
1. The control instance searches for an existing delivery for week 40 (2020-09-28_Template_1).

    >[!NOTE]
    >
    >If not found, a new delivery is created.

1. The week after, an inbound bounce is received for the event.
1. The status of the event changes to **[!UICONTROL Delivery failed]**.
1. The **Message Center execution instance** (mcSync_mcExec) workflow retrieves the delivery logs from the execution instance and searches for a delivery for week 41 (2020-10-05_Template_1) to update the delivery logs. The delivery logs are then linked to a new delivery for the current week.

To summarize, the deliveries weekly accumulate the events based on the latest event update, and not on the event creation date.

Therefore, when extracting transactional messaging delivery logs from the control instance, the delivery ID associated with each delivery log ID changes every week.-->

実行インスタンスのアクティビティと実行の監視については、[トランザクションメッセージレポート](../../message-center/using/about-transactional-messaging-reports.md)を参照してください。
