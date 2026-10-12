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
source-git-commit: 617db6f51887118c965b8938b2b9f14335293875
workflow-type: tm+mt
source-wordcount: '301'
ht-degree: 60%
---
# トランザクションメッセージテンプレートのテスト {#testing-message-templates}

[ メッセージテンプレート ](https://experienceleague.adobe.com/en/docs/campaign/campaign-v8/send/real-time/transactional-template){target="_blank"} （Campaign v8 ドキュメント）の準備が整ったら、次の手順に従ってプレビューとテストを行います。

Campaign v7 から v8 への移行の一環として、Campaign Classic のドキュメントセットを効率化および再編成しました。 共通機能は、Campaign v8 ドキュメントセットでのみ使用できるようになりました。 シードアドレスの追加方法、トランザクションメッセージのプレビュー、プルーフの送信方法については、[Campaign v8 ドキュメント ](https://experienceleague.adobe.com/en/docs/campaign/campaign-v8/send/real-time/transactional-template#test-message-template){target=_blank}を参照してください。

[![画像](../../assets/do-not-localize/learn-more-button.svg)](https://experienceleague.adobe.com/en/docs/campaign/campaign-v8/send/real-time/transactional-template#test-message-template){target=_blank}

## パーソナライゼーションデータ {#personalization-data}

メッセージテンプレート内のデータを使い、トランザクションメッセージのパーソナライゼーションをテストできます。 この機能は、プレビューを生成したり、配達確認を送信するために使用されます。 さまざまなインターネットアクセスプロバイダーに向けたメッセージのレンダリングを表示することもできます。 詳しくは、[受信ボックスのレンダリング](../../delivery/using/inbox-rendering.md)を参照してください。

このデータの目的は、最終的に配信する前にメッセージをテストすることです。 このメッセージは、処理される実際のデータと同一のものではありません。 ただし以下に示すように、XML 構造は実行インスタンスに保存されているイベントの構造と同一です。

![](assets/messagecenter_create_custo_006.png)

この情報を使用すると、パーソナライゼーションタグを使用してメッセージコンテンツをパーソナライズできます（詳しくは、[ メッセージコンテンツの作成](https://experienceleague.adobe.com/en/docs/campaign/campaign-v8/send/real-time/transactional-template#create-message-content){target="_blank"} （Campaign v8 ドキュメント）を参照）。

1. トランザクションメッセージテンプレートを選択します。

1. テンプレートで、「**[!UICONTROL シードアドレス]**」タブをクリックします。

1. イベントコンテンツに、XML フォーマットでテスト情報を入力します。

   ![](assets/messagecenter_create_custo_001.png)

1. 「**[!UICONTROL 保存]**」をクリックします。
