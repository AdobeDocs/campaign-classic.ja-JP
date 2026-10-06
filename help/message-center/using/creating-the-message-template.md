---
product: campaign
title: トランザクションメッセージテンプレートのデザイン
description: Adobe Campaign Classic でトランザクションメッセージテンプレートを作成およびデザインする方法について説明します
feature: Transactional Messaging, Message Center, Templates
exl-id: a52bc140-072e-4f81-b6da-f1b38662bce5
TQID: 'https://experienceleague.adobe.com/lVjiHCruVE2IpwsTkjcNtccmpoSF1aeZ-PFRjcIwf7g'
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
source-wordcount: '513'
ht-degree: 100%
---
# トランザクションメッセージテンプレートのデザイン {#creating-the-message-template}



各イベントをパーソナライズされたメッセージに変えるには、各イベントタイプに一致するメッセージテンプレートを作成する必要があります。

>[!IMPORTANT]
>
>イベントタイプは事前に作成しておく必要があります。 詳しくは、[イベントタイプの作成](../../message-center/using/creating-event-types.md)を参照してください。

テンプレートには、トランザクションメッセージをパーソナライズするために必要な情報が含まれています。 テンプレートを使用すると、メッセージのプレビューを検証したり、最終的なターゲットへ配信する前にシードアドレスを使用した配達確認を送信することもできます。 詳しくは、[トランザクションメッセージテンプレートのテスト](../../message-center/using/testing-message-templates.md)を参照してください。

## メッセージテンプレートの作成 {#creating-message-template}

1. Adobe Campaign のツリーにて、**[!UICONTROL Message Center／トランザクションメッセージテンプレート]**&#x200B;フォルダーに移動します。

1. トランザクションメッセージテンプレートのリスト内を右クリックし、ドロップダウンメニューで「**[!UICONTROL 新規]**」を選択するか、トランザクションメッセージテンプレートのリストの上部にある「**[!UICONTROL 新規]**」ボタンをクリックします。

   ![](assets/messagecenter_create_model_001.png)

1. 配信ウィンドウで、使用したいチャネルに適した配信テンプレートを選択します。

   ![](assets/messagecenter_create_model_002.png)

1. 必要に応じて、ラベルを変更します。

1. 送信したいメッセージに合うイベントのタイプを選択します。

   ![](assets/messagecenter_create_model_003.png)

   イベントタイプはコンソールで事前に作成しておく必要があります。 詳しくは、[イベントタイプの作成](../../message-center/using/creating-event-types.md)を参照してください。

   >[!IMPORTANT]
   >
   >イベントタイプを複数のテンプレートにリンクすることはできません。

1. 特性と説明を入力したら、「**[!UICONTROL 続行]**」をクリックしてメッセージ本文を作成します。[メッセージコンテンツの作成](#creating-message-content)を参照してください。

   ![](assets/messagecenter_create_model_004.png)

## メッセージコンテンツの作成 {#creating-message-content}

トランザクションメッセージコンテンツの定義は、Adobe Campaign の通常の配信と同様です。 例えば、メール配信では、HTML またはテキストフォーマットでコンテンツを作成したり、添付ファイルを追加したり、配信オブジェクトをパーソナライズすることができます。 詳しくは、[メール配信](../../delivery/using/about-email-channel.md)の章を参照してください。

>[!IMPORTANT]
>
>メッセージに含まれる画像は、公的にアクセス可能でなければなりません。 Adobe Campaign には、トランザクションメッセージ用の画像アップロードのメカニズムがありません。\
>JSSP や Web アプリとは異なり、`<%=` にはデフォルトのエスケープ機能がありません。
>
>こうした場合は、イベントから取得されるそれぞれのデータを適切にエスケープする必要があります。 このエスケープ方法は、このフィールドの使用方法によって異なります。 例えば、URL 内では、encodeURIComponent を使用します。 HTML に表示する場合は、escapeXMLString を使用できます。

メッセージのコンテンツを定義したら、メッセージ本文にイベントの情報を取り入れ、パーソナライズすることができます。 イベントの情報は、パーソナライゼーションタグを使用してテキスト本文に挿入します。

![](assets/messagecenter_create_content_001.png)

* すべてのパーソナライゼーションフィールドはペイロードから取得されます。
* トランザクションメッセージ内では、1 つまたは複数のパーソナライゼーションブロックを参照できます。 ブロックコンテンツは、実行インスタンスへのパブリッシュ中に配信コンテンツに追加されます。

パーソナライゼーションタグをメールメッセージの本文に挿入するには、次の手順に従います。

1. メッセージのテンプレートで、メールフォーマットに合うタブをクリックします（HTML またはテキスト）。

1. メッセージの本文を入力します。

1. **[!UICONTROL リアルタイムイベント／イベント XML]** メニューを使用して、テキスト本文にタグを挿入します。

   ![](assets/messagecenter_create_custo_002.png)

1. 下記に示すように、タグの入力には次の構文を利用します。**要素名**.@**属性名**

   ![](assets/messagecenter_create_custo_003.png)

1. コンテンツを保存します。

これで、メッセージを[テスト](../../message-center/using/testing-message-templates.md)する準備が整いました。
