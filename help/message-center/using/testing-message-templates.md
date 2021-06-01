---
product: campaign
title: テストトランザクションメッセージテンプレート
description: Adobe Campaign Classicでプレビューおよびテストするために、トランザクションメッセージ内のシードアドレスを管理する方法について説明します。
audience: message-center
content-type: reference
topic-tags: message-templates
exl-id: 417004c9-ed96-4b98-a518-a3aa6123ee7b
source-git-commit: 98d646919fedc66ee9145522ad0c5f15b25dbf2e
workflow-type: tm+mt
source-wordcount: '578'
ht-degree: 62%

---

# テストトランザクションメッセージテンプレート{#testing-message-templates}

[メッセージテンプレート](../../message-center/using/creating-the-message-template.md)の準備が整ったら、次の手順に従ってプレビューし、テストします。

## トランザクションメッセージでのシードアドレスの管理 {#managing-seed-addresses-in-transactional-messages}

シードアドレスを使用すると、E メールまたは SMS 配信の前に、メッセージのプレビューを表示したり、配達確認を送信したり、メッセージのパーソナライゼーションを検証したりすることができます。シードアドレスは配信に関連付けられ、その他の配信に利用することはできません。

トランザクションメッセージでシードアドレスを作成するには、次の手順に従います。

1. トランザクションメッセージテンプレートで、「**[!UICONTROL シードアドレス]**」タブをクリックします。

   ![](assets/messagecenter_create_seedaddr_001.png)

1. 後で容易に選択できるよう、ラベルを割り当てます。

   ![](assets/messagecenter_create_seedaddr_002.png)

1. シードアドレス（通信チャネルにより E メールまたは携帯電話）を入力します。

   ![](assets/messagecenter_create_seedaddr_003.png)

1. 外部識別子を入力します。このオプションのフィールドには、web サイト上のすべてのアプリケーションに共通し、プロファイルを識別するのに利用できるビジネスキー（一意の識別子、名前 + E メールなど）を入力することができます。Adobe Campaign マーケティングデータベースにもこのフィールドが存在する場合、データベース内のプロファイルとイベントとを照合することができます。

   ![](assets/messagecenter_create_seedaddr_003bis.png)

1. テストデータを挿入します（[パーソナライゼーションデータ](#personalization-data)を参照）。

   ![](assets/messagecenter_create_custo_001.png)

   <!--## Creating several seed addresses {#creating-several-seed-addresses}-->
1. 「**[!UICONTROL 他のシードアドレスを追加]**」リンクをクリックし、「**[!UICONTROL 追加]**」ボタンをクリックします。

   ![](assets/messagecenter_create_seedaddr_004.png)

   <!--1. Follow the configuration steps for a seed address detailed in the [Creating a seed address](#creating-a-seed-address) section.-->
1. この手順を繰り返して、必要な数のアドレスを作成します。

   ![](assets/messagecenter_create_seedaddr_008.png)

アドレスを作成したら、プレビューとパーソナライゼーションを表示することができます。[トランザクションメッセージのプレビュー](#transactional-message-preview)を参照してください。

## パーソナライゼーションデータ {#personalization-data}

メッセージテンプレート内のデータを使い、トランザクションメッセージのパーソナライゼーションをテストできます。この機能は、プレビューを生成したり、配達確認を送信するために使用されます。様々なインターネットアクセスプロバイダー向けにメッセージのレンダリングを表示することもできます。 詳しくは、[受信ボックスレンダリング](../../delivery/using/inbox-rendering.md)を参照してください。

このデータの目的は、最終配信の前にメッセージを検証することです。これらのメッセージは、実際に処理するデータとは一致しません。 ただし、XML構造は、次に示すように、実行インスタンスに格納されるイベントの構造と同じである必要があります。

![](assets/messagecenter_create_custo_006.png)

この情報により、パーソナライゼーションタグを使用してメッセージコンテンツをパーソナライズできます（詳しくは、[メッセージコンテンツの作成](../../message-center/using/creating-the-message-template.md#creating-message-content)を参照）。

1. トランザクションメッセージテンプレートを選択します。

1. テンプレートで、「**[!UICONTROL シードアドレス]**」タブをクリックします。

1. イベントコンテンツに、XML フォーマットでテスト情報を入力します。

   ![](assets/messagecenter_create_custo_001.png)

1. 「**[!UICONTROL 保存]**」をクリックします。

## メッセージのプレビュー {#transactional-message-preview}

1 つまたは複数のシードアドレスとメッセージ本文を作成したら、メッセージをプレビューして、パーソナライゼーションを確認することができます。

1. メッセージテンプレートで、「**[!UICONTROL プレビュー]**」タブをクリックします。

   ![](assets/messagecenter_preview_001.png)

1. ドロップダウンリストから「**[!UICONTROL シードアドレス]**」を選択します。

   ![](assets/messagecenter_preview_002.png)

1. 作成済みのシードアドレスを選択してパーソナライズされたメッセージを表示します。

   ![](assets/messagecenter_create_seedaddr_009.png)

シードアドレスを使用して、様々なインターネットアクセスプロバイダー向けのメッセージのレンダリングを表示することもできます。 詳しくは、[受信ボックスレンダリング](../../delivery/using/inbox-rendering.md)を参照してください。

## 配達確認の送信 {#sending-a-proof}

作成済みのシードアドレスへ配達確認を送信することで、メッセージ配信をテストできます。

配達確認の送信は、[通常の配信](../../delivery/using/steps-validating-the-delivery.md#sending-a-proof)と同じ手順に従います。 ただし、トランザクションメッセージでは、事前に次の操作を実行する必要があります。

* [パーソナライゼーションデータ](#personalization-data)を使用して、1つ以上の[シードアドレス](#managing-seed-addresses-in-transactional-messages)を作成します。
* [メッセージコンテンツの作成](../../message-center/using/creating-the-message-template.md#creating-message-content).

配達確認を送信するには：

1. 配信ウィンドウで、「**[!UICONTROL 配達確認を送信]**」ボタンをクリックします。
1. 配信を分析します。
1. エラーを修正し、配信を確認します。

   ![](assets/messagecenter_send_proof_001.png)

1. シードアドレスにメッセージが配信されたこと、およびそのコンテンツが設定どおりであることを確認します。

   ![](assets/messagecenter_send_proof_002.png)

配達確認は、各テンプレートの「**[!UICONTROL 監査]**」タブからアクセスできます。詳しくは、[配達確認の送信](../../delivery/using/steps-validating-the-delivery.md#sending-a-proof)を参照してください。

![](assets/messagecenter_send_proof_003.png)

これで、メッセージテンプレートを[公開](../../message-center/using/publishing-message-templates.md)する準備が整いました。