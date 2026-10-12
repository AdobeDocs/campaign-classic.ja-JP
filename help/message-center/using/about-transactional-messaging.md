---
product: campaign
title: トランザクションメッセージの基本を学ぶ
description: Adobe Campaign Classic におけるトランザクションメッセージの動作の仕組みと主な手順について説明します
feature: Transactional Messaging, Message Center
exl-id: dc52e789-d0bf-4e8f-b448-9d69a2762cc1
TQID: 'https://experienceleague.adobe.com/n4w2hZkuzHlD3Axc1tUCGfBQ13D28j3Xpmdh07tVr4g'
product_v2:
  - id: dfc56824-e8b9-499e-85d4-21aedb507314
    internal-label: Campaign
  - id: fd6e6e36-54e4-4f1a-96fc-1a750e400d50
    internal-label: Campaign Classic v7
feature_v2:
  - id: a4671286-a59f-47e3-b97b-90627a1977d5
    internal-label: Communication channels
  - id: 6d358f27-4f3c-5ddf-9159-05192e672ba7
    internal-label: Message Center
subfeature_v2:
  - id: d3b34fea-a110-482f-adb2-aae8d686bac8
    internal-label: Transactional messaging
source-git-commit: 617db6f51887118c965b8938b2b9f14335293875
workflow-type: tm+mt
source-wordcount: '610'
ht-degree: 72%
---
# トランザクションメッセージの基本を学ぶ {#about-transactional-messaging}



## 概要 {#overview}

**トランザクションメッセージ**（Message Center）は、カスタムトリガー通知を管理するためにデザインされたキャンペーンモジュールです。カスタムトリガー通知は、外部の情報システムが送信したイベントから生成されます。

Campaign v7 から v8 への移行の一環として、Campaign Classic のドキュメントセットを効率化および再編成しました。 共通機能は、Campaign v8 ドキュメントセットでのみ使用できるようになりました。 トランザクションメッセージについて詳しくは、[Campaign v8 ドキュメント &#x200B;](https://experienceleague.adobe.com/ja/docs/campaign/campaign-v8/send/real-time/transactional){target=_blank}を参照してください。

[![画像](../../assets/do-not-localize/learn-more-button.svg)](https://experienceleague.adobe.com/ja/docs/campaign/campaign-v8/send/real-time/transactional){target=_blank}

この節では、オンプレミスおよびハイブリッドのデプロイメントに固有の、トランザクションメッセージングアーキテクチャと、コントロールインスタンスおよび実行インスタンスの設定について説明します。

>[!IMPORTANT]
>
>トランザクションメッセージを利用するには特定のライセンスが必要です。 使用許諾契約書を確認してください。

<!--Before starting with transactional messaging, make sure you read the corresponding [best practices and limitations]().-->

## トランザクションメッセージの動作原理 {#transactional-messaging-operating-principle}

Adobe Campaign のトランザクションメッセージモジュールは情報システムに組み込まれ、システムはパーソナライズされたトランザクションメッセージに変換するイベントを返します。 これらのメッセージはメール、SMS、プッシュ通知などを介して、個別に送信することも、まとめて送信することもできます。

この機能は、独立した&#x200B;**実行インスタンス**&#x200B;と&#x200B;**コントロールインスタンス**&#x200B;から成る、特有のアーキテクチャで提供されます。 インスタンスを分けることにより、高い可用性と優れた負荷管理を実現します。 詳しくは、[トランザクションメッセージのアーキテクチャ](../../message-center/using/transactional-messaging-architecture.md)を参照してください。

>[!NOTE]
>
>Adobe Cloud が提供する Message Center の実行インスタンス用の新しいユーザーを作成する場合は、[アドビのカスタマーサポート](https://helpx.adobe.com/jp/enterprise/admin-guide.html/enterprise/using/support-for-experience-cloud.ug.html)に連絡してください。 Message Center のユーザーは、**[!UICONTROL リアルタイムイベント（nmsRtEvent）]**&#x200B;フォルダーにアクセスできる専用の権限が必要な特定のオペレーターです。

>[!NOTE]
>
>Adobe Campaign は、トランザクションメッセージの処理を他のどの配信よりも優先します。

## 主な手順 {#key-steps}

パーソナライズされたトランザクションメッセージを Adobe Campaign で作成し、管理する主な手順は以下の通りです。

### コントロールインスタンスで実行する手順

**コントロールインスタンス**&#x200B;で、次のアクションを実行する必要があります。

1. [&#x200B; イベントタイプを作成](https://experienceleague.adobe.com/ja/docs/campaign/campaign-v8/send/real-time/transactional){target="_blank"} （Campaign v8 ドキュメント）。
1. [&#x200B; メッセージテンプレートの作成とデザイン &#x200B;](https://experienceleague.adobe.com/en/docs/campaign/campaign-v8/send/real-time/transactional-template){target="_blank"} （Campaign v8 ドキュメント）。 この手順で、イベントをメッセージにリンクします。
1. [メッセージのテスト](../../message-center/using/testing-message-templates.md)。
1. [&#x200B; メッセージテンプレートを公開](https://experienceleague.adobe.com/en/docs/campaign/campaign-v8/send/real-time/transactional-template){target="_blank"} （Campaign v8 ドキュメント）。

>[!NOTE]
>
>上記の手順はすべて&#x200B;**コントロールインスタンス**&#x200B;で実行します。 コントロールインスタンスでテンプレートをパブリッシュすると、すべての&#x200B;**実行インスタンス**&#x200B;もパブリッシュされます。 トランザクションメッセージのインスタンスについては、[トランザクションメッセージのアーキテクチャ](../../message-center/using/transactional-messaging-architecture.md)を参照してください。

### 実行インスタンスでのイベント処理

トランザクションメッセージテンプレートを設計してパブリッシュして、対応するイベントがトリガーされた場合、以下の主な手順が&#x200B;**実行インスタンス**&#x200B;で実行されます。

1. 外部の情報システムでイベントが生成されると、**PushEvent** および **PushEvents** メソッドを介して関連データが Campaign に送信されます。 [&#x200B; イベントコレクション &#x200B;](https://experienceleague.adobe.com/en/docs/campaign/campaign-v8/send/real-time/event/event-processing#event-collection){target="_blank"} （Campaign v8 ドキュメント）を参照してください。
1. 適切なメッセージテンプレートにイベントがリンクされます。 テンプレートに向けた[&#x200B; ルーティング &#x200B;](https://experienceleague.adobe.com/en/docs/campaign/campaign-v8/send/real-time/event/event-processing#event-to-template){target="_blank"}を参照してください（Campaign v8 ドキュメント）。
1. エンリッチメントステージが完了すると、配信が送信されます。 [配信の実行](https://experienceleague.adobe.com/en/docs/campaign/campaign-v8/send/real-time/event/delivery-execution){target="_blank"} （Campaign v8 ドキュメント）を参照してください。 ターゲットの各受信者は、パーソナライズされたメッセージを受信します。

## 関連トピック {#related-topics}

* [コミュニケーションチャネルの概要](../../delivery/using/communication-channels.md)
* [配信の作成に関する主な手順](https://experienceleague.adobe.com/docs/campaign/campaign-v8/send/create-message.html?lang=ja){target="_blank"}
* [トランザクションメッセージのアーキテクチャ](../../message-center/using/transactional-messaging-architecture.md)
* [&#x200B; トランザクションメッセージングレポートへのアクセス &#x200B;](https://experienceleague.adobe.com/en/docs/campaign/campaign-v8/send/real-time/event/delivery-execution){target="_blank"} （Campaign v8 ドキュメント）
