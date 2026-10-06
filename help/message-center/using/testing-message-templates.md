---
product: campaign
title: トランザクションメッセージテンプレートのテスト
description: トランザクションメッセージ内のシードアドレスを管理して、Adobe Campaign Classic でプレビューおよびテストする方法について説明します
feature: Transactional Messaging, Message Center, Templates
audience: message-center
content-type: reference
topic-tags: message-templates
exl-id: 417004c9-ed96-4b98-a518-a3aa6123ee7b
TQID: 'https://experienceleague.adobe.com/jcmXX4aMPaTBatt4m3s-IAaAeoXnjmPaEE4oqIDoIOI'
product_v2:
  - id: dfc56824-e8b9-499e-85d4-21aedb507314
    internal-label: Campaign
  - id: fd6e6e36-54e4-4f1a-96fc-1a750e400d50
    internal-label: Campaign Classic v7
feature_v2:
  - id: 6d358f27-4f3c-5ddf-9159-05192e672ba7
    internal-label: Message Center
  - id: baf8e746-117b-5e73-b179-0a83edc0295f
    internal-label: Templates
  - id: a4671286-a59f-47e3-b97b-90627a1977d5
    internal-label: Communication channels
subfeature_v2:
  - id: d3b34fea-a110-482f-adb2-aae8d686bac8
    internal-label: Transactional messaging
topic_v2:
  - id: e0eb8757-182f-49f3-94a4-1587d16f5094
    internal-label: Personalization
source-git-commit: a43e591a565a18d79f583d975e3e812c5435b0c0
workflow-type: tm+mt
source-wordcount: '607'
ht-degree: 100%
---
# トランザクションメッセージテンプレートのテスト {#testing-message-templates}



[メッセージテンプレート](../../message-center/using/creating-the-message-template.md)の準備が整ったら、次の手順に従ってプレビューしテストします。

## トランザクションメッセージでのシードアドレスの管理 {#managing-seed-addresses-in-transactional-messages}

シードアドレスを使用すると、メールまたは SMS 配信の前に、メッセージのプレビューを表示したり、配達確認を送信したり、メッセージのパーソナライゼーションを検証したりすることができます。 シードアドレスは配信に関連付けられ、その他の配信に利用することはできません。

トランザクションメッセージでシードアドレスを作成するには、次の手順に従います。

1. トランザクションメッセージテンプレートで、「**[!UICONTROL シードアドレス]**」タブをクリックします。

   ![](assets/messagecenter_create_seedaddr_001.png)

1. 後で容易に選択できるよう、ラベルを割り当てます。

   ![](assets/messagecenter_create_seedaddr_002.png)

1. シードアドレス（通信チャネルによりメールまたは携帯電話）を入力します。

   ![](assets/messagecenter_create_seedaddr_003.png)

1. 外部識別子を入力します。このオプションのフィールドには、web サイト上のすべてのアプリケーションに共通し、プロファイルを識別するのに利用できるビジネスキー（一意の識別子、名前 + メールなど） を入力することができます。 Adobe Campaign マーケティングデータベースにもこのフィールドが存在する場合、データベース内のプロファイルとイベントを紐付けることができます。

   ![](assets/messagecenter_create_seedaddr_003bis.png)

1. テストデータを挿入します（[パーソナライゼーションデータ](#personalization-data)を参照）。

   ![](assets/messagecenter_create_custo_001.png)

   <!--## Creating several seed addresses {#creating-several-seed-addresses}-->
1. 「**[!UICONTROL 他のシードアドレスを追加]**」リンクをクリックし、「**[!UICONTROL 追加]**」ボタンをクリックします。

   ![](assets/messagecenter_create_seedaddr_004.png)

   <!--1. Follow the configuration steps for a seed address detailed in the [Creating a seed address](#creating-a-seed-address) section.-->
1. この手順を繰り返して、必要な数のアドレスを作成します。

   ![](assets/messagecenter_create_seedaddr_008.png)

アドレスを作成したら、プレビューとパーソナライゼーションを表示することができます。 [トランザクションメッセージのプレビュー](#transactional-message-preview)を参照してください。

## パーソナライゼーションデータ {#personalization-data}

メッセージテンプレート内のデータを使い、トランザクションメッセージのパーソナライゼーションをテストできます。 この機能は、プレビューを生成したり、配達確認を送信するために使用されます。 さまざまなインターネットアクセスプロバイダーに向けたメッセージのレンダリングを表示することもできます。 詳しくは、[受信ボックスのレンダリング](../../delivery/using/inbox-rendering.md)を参照してください。

このデータの目的は、最終的に配信する前にメッセージをテストすることです。 このメッセージは、処理される実際のデータと同一のものではありません。 ただし以下に示すように、XML 構造は実行インスタンスに保存されているイベントの構造と同一です。

![](assets/messagecenter_create_custo_006.png)

この情報を使用して、パーソナライズ機能のタグを使用してメッセージコンテンツをパーソナライズできます。詳しくは、[メッセージコンテンツの作成](../../message-center/using/creating-the-message-template.md#creating-message-content)を参照してください。

1. トランザクションメッセージテンプレートを選択します。

1. テンプレートで、「**[!UICONTROL シードアドレス]**」タブをクリックします。

1. イベントコンテンツに、XML フォーマットでテスト情報を入力します。

   ![](assets/messagecenter_create_custo_001.png)

1. 「**[!UICONTROL 保存]**」をクリックします。

## トランザクションメッセージのプレビュー {#transactional-message-preview}

1 つまたは複数のシードアドレスとメッセージ本文を作成したら、メッセージをプレビューして、パーソナライゼーションを確認することができます。

1. メッセージテンプレートで、「**[!UICONTROL プレビュー]**」タブをクリックします。

   ![](assets/messagecenter_preview_001.png)

1. ドロップダウンリストから「**[!UICONTROL シードアドレス]**」を選択します。

   ![](assets/messagecenter_preview_002.png)

1. 作成済みのシードアドレスを選択してパーソナライズされたメッセージを表示します。

   ![](assets/messagecenter_create_seedaddr_009.png)

シードアドレスを使用して、さまざまなインターネットアクセスプロバイダーに向けたメッセージのレンダリングを表示することもできます。 詳しくは、[受信ボックスのレンダリング](../../delivery/using/inbox-rendering.md)を参照してください。

## 配達確認の送信 {#sending-a-proof}

作成済みのシードアドレスへ配達確認を送信することで、メッセージ配信をテストできます。

配達確認の送信は、通常の配信の場合と同じプロセスで行います。 [Campaign v8 ドキュメント](https://experienceleague.adobe.com/docs/campaign/campaign-v8/send/validate/preview-and-proof.html?lang=ja){target="_blank"}を参照してください。 ただし、トランザクションメッセージでは、事前に次の操作を実行する必要があります。

* [パーソナライズ機能のデータ](#personalization-data)を使用して、1 つまたは複数の[シードアドレス](#managing-seed-addresses-in-transactional-messages)を作成します。
* [メッセージコンテンツを作成](../../message-center/using/creating-the-message-template.md#creating-message-content)します。

配達確認を送信するには：

1. 配信ウィンドウで、「**[!UICONTROL 配達確認を送信]**」ボタンをクリックします。
1. 配信を分析します。
1. エラーを修正し、配信を確認します。

   ![](assets/messagecenter_send_proof_001.png)

1. シードアドレスにメッセージが配信されたこと、およびそのコンテンツが設定どおりであることを確認します。

   ![](assets/messagecenter_send_proof_002.png)

配達確認は、各テンプレートの「**[!UICONTROL 監査]**」タブからアクセスできます。 詳しくは、[Campaign v8 ドキュメント](https://experienceleague.adobe.com/docs/campaign/campaign-v8/send/validate/preview-and-proof.html?lang=ja){target="_blank"}を参照してください。

![](assets/messagecenter_send_proof_003.png)

これで、メッセージテンプレートを[パブリッシュ](../../message-center/using/publishing-message-templates.md)する準備が整いました。