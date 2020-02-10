---
title: テクニカルワークフロー
seo-title: テクニカルワークフロー
description: テクニカルワークフロー
seo-description: null
page-status-flag: never-activated
uuid: dfd1b180-86b5-4740-9bad-a0e210f433c5
contentOwner: sauviat
products: SG_CAMPAIGN/CLASSIC
audience: message-center
content-type: reference
topic-tags: instance-configuration
discoiquuid: 2e648e63-06d2-4e8f-9934-066a41d18eac
index: y
internal: n
snippet: y
translation-type: tm+mt
source-git-commit: 579329d9194115065dff2c192deb0376c75e67bd

---


# テクニカルワークフロー{#technical-workflows}

トランザクションメッセージテンプレートをデプロイする前に、コントロールインスタンスおよびそれぞれの実行インスタンス上にてテクニカルワークフローが作成され、開始されていることを確認する必要があります。

トランザクションメッセージ（Message Center）に関連する様々なテクニカルワークフローは、コントロールインスタンスと実行インスタンスとに分類されます。

## コントロールインスタンスのワークフロー {#control-instance-workflows}

コントロールインスタンス上には、実行インスタンスにつき 1 つのアーカイブワークフローを作成する必要があります。作成したアーカイブワークフローは、**管理／プロダクション／Message Center** フォルダーからアクセスできます。アーカイブワークフローは作成されると自動的に開始されます。

**分散アーキテクチャ**

If you have one or several execution instances registered, on the control instance, you must create one archiving workflow for each **[!UICONTROL Message Center execution instance]** external account. このボタンをク **[!UICONTROL Create the archiving workflow]** リックして、ワークフローを作成し、開始します。

![](assets/messagecenter_archiving_002.png)

**最小アーキテクチャ**

同一インスタンス上にコントロールおよび実行インスタンスをインストールしたら、デプロイウィザードを使用してアーカイブワークフローを作成する必要があります。このボタンをク **[!UICONTROL Create the archiving workflow]** リックして、ワークフローを作成し、開始します。

![](assets/messagecenter_archiving_001.png)

## 実行インスタンスのワークフロー {#execution-instance-workflows}

実行インスタンスでは、**管理／プロダクション／Message Center** フォルダーからトランザクションメッセージのテクニカルワークフローにアクセスできます。必要な操作は、ワークフローを開始することだけです。リストに含まれるワークフローは以下のとおりです。

* **[!UICONTROL Processing batch events]** (内部名： **[!UICONTROL batchEventsProcessing]** ):このワークフローを使用すると、バッチイベントをメッセージテンプレートにリンクする前に、キュー内のバッチイベントを分類できます。
* **[!UICONTROL Processing real time events]** (内部名： **[!UICONTROL rtEventsProcessing]** ):このワークフローを使用すると、リアルタイムイベントをメッセージテンプレートにリンクする前に、キュー内のリアルタイムイベントを分類できます。
* **[!UICONTROL Update event status]** (内部名： **[!UICONTROL updateEventStatus]** ):このワークフローでは、イベントにステータスを関連付けることができます。

   イベントステータスには以下のものがあります。

   * **[!UICONTROL Pending]** :イベントがキューにある。 イベントにはまだメッセージテンプレートが割り当てられていません。
   * **[!UICONTROL Pending delivery]** :イベントがキューにある場合、メッセージテンプレートが割り当てられ、配信によって処理されています。
   * **[!UICONTROL Sent]** :このステータスは配信ログからコピーされます。 配信が送信されたことを示します。
   * **[!UICONTROL Ignored by the delivery]** :このステータスは配信ログからコピーされます。 配信が無視されたことを意味しています。
   * **[!UICONTROL Delivery failed]** :このステータスは配信ログからコピーされます。 配信が失敗したことを意味しています。
   * **[!UICONTROL Event not taken into account]** :イベントをメッセージテンプレートにリンクできませんでした。 イベントの処理はおこなわれません。

