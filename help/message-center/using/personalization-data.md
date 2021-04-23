---
solution: Campaign Classic
product: campaign
title: パーソナライゼーションデータ
description: パーソナライゼーションデータ
audience: message-center
content-type: reference
topic-tags: message-templates
exl-id: 587d48aa-43ae-41c5-a0e3-6805a0e9b6a4
translation-type: ht
source-git-commit: 6854d06f8dc445b56ddfde7777f02916a60f2b63
workflow-type: ht
source-wordcount: '153'
ht-degree: 100%

---

# パーソナライゼーションデータ{#personalization-data}

メッセージテンプレート内のデータを使い、トランザクションメッセージのパーソナライゼーションをテストできます。この機能は、プレビューを生成したり、配達確認を送信するために使用されます。**配信品質**&#x200B;モジュールをインストールすると、このデータを使用して様々なインターネットアクセスプロバイダー用メッセージのレンダリングを表示できます（**受信トレイのレンダリング**：詳しくは、[この節](../../delivery/using/inbox-rendering.md)を参照）。

このデータの目的は、最終配信の前にメッセージを検証することです。このメッセージは、Message Center が処理する実際のデータとは一致しません。ただし以下に示すように、XML 構造は、実行インスタンスに保存されているイベントの構造と同一でなければなりません。

![](assets/messagecenter_create_custo_006.png)

この情報により、パーソナライゼーションタグを使用してメッセージコンテンツをパーソナライズできます（詳しくは、[メッセージコンテンツの作成](../../message-center/using/creating-message-content.md)を参照）。

1. メッセージテンプレートで「**[!UICONTROL シードアドレス]**」タブをクリックします。
1. イベントコンテンツに、XML フォーマットでテスト情報を入力します。

   ![](assets/messagecenter_create_custo_001.png)
