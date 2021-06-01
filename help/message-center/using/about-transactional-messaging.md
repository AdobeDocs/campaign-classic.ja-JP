---
product: campaign
title: トランザクションメッセージの基本を学ぶ
description: 'Adobe Campaign Classicトランザクションメッセージの動作の仕組みと主な手順について詳しく説明します。 '
audience: message-center
content-type: reference
topic-tags: introduction
exl-id: dc52e789-d0bf-4e8f-b448-9d69a2762cc1
source-git-commit: e86350cf12db37e3f2c227563057b97922601729
workflow-type: tm+mt
source-wordcount: '648'
ht-degree: 12%

---


# トランザクションメッセージの基本を学ぶ {#about-transactional-messaging}

## 概要 {#overview}

**トランザクショントリガー** (Message Center)は、外部の情報システムから送信されるイベントから生成されるカスタムメッセージ通知を管理するために設計されたCampaignモジュールです。

トランザクションメッセージは、Webサイトなどのプロバイダーによってリアルタイムに送信される、個々に固有の通信です。 特に、受信者が確認したい重要な情報が含まれているので、期待されています。

トランザクションメッセージ機能は、拡張性をサポートし、24/7のサービスを提供するように設計されています。

* **いつになる？** このメッセージには重要な情報が含まれているので、ユーザーはリアルタイムでの送信を求めています。その結果、トリガーされるイベントとメッセージの到着間の遅延が非常に短くなる必要があります。

* **なぜ重要なのか？** 一般に、トランザクションメッセージの開封率は高くなります。顧客との関係を定義するので、顧客の行動に強い影響を与える可能性があるので、慎重に設計する必要があります。

* **例えば？** アカウント作成後のお知らせメッセージ、注文の発送確認メッセージ、請求書、パスワード変更確認メッセージ、顧客がWebサイトを閲覧した後の通知、製品の利用不可に関する連絡、取引明細などが考えられます。

>[!IMPORTANT]
>
>トランザクションメッセージを利用するには特定のライセンスが必要です。使用許諾契約書を確認してください。

<!--Before starting with transactional messaging, make sure you read the corresponding [best practices and limitations]().-->

## トランザクションメッセージの動作原則 {#transactional-messaging-operating-principle}

Adobe Campaignトランザクションメッセージモジュールは、情報システムに統合され、返されるイベントをパーソナライズされたトランザクションメッセージに変更します。 これらのメッセージは、個別に送信することも、E メール、SMS またはプッシュ通知を介してまとめて送信することもできます。

この機能は、特定のアーキテクチャに依存しています。ここで、**実行インスタンス**&#x200B;は&#x200B;**コントロールインスタンス**&#x200B;とは別になっています。 この配布により、可用性が高く、負荷管理が向上します。 詳しくは、[トランザクションメッセージのアーキテクチャ](../../message-center/using/transactional-messaging-architecture.md)を参照してください。

>[!NOTE]
>
>Adobe Cloud でホストされる Message Center 実行インスタンスの新しいユーザーを作成するには、[アドビカスタマーケア](https://helpx.adobe.com/jp/enterprise/admin-guide.html/enterprise/using/support-for-experience-cloud.ug.html)に連絡する必要があります。Message Centerユーザーは、**[!UICONTROL リアルタイムイベント(nmsRtEvent)]**&#x200B;フォルダーにアクセスするための専用の権限を必要とする特定のオペレーターです。

トランザクションメッセージの全体的なプロセスは、次のように記述できます。

![](assets/transactional-msg-overview.png)

例えば、顧客が製品を購入できるWebサイトを持つ会社の例を考えてみます。

Adobe Campaignでは、買い物かごに製品を追加した顧客に通知Eメールを送信できます。 訪問者の1人が購入を経ずにWebサイトを離れると(Campaignイベントをトリガーする外部イベント)、買い物かごの放棄に関するEメールが自動的に送信されます（トランザクションメッセージ配信）。

これを導入する主な手順は、[この節](#key-steps)で説明します。

>[!NOTE]
>
>Adobe Campaignは、トランザクションメッセージの処理を他のどの配信よりも優先します。

## 主な手順 {#key-steps}

Adobe Campaignでパーソナライズされたトランザクションメッセージを作成および管理する際の主な手順を以下にまとめます。

### コントロールインスタンスで実行する手順

**コントロールインスタンス**&#x200B;で、次の操作を実行する必要があります。

1. [イベントタイプの作成](../../message-center/using/creating-event-types.md)を参照してください。
1. [メッセージテンプレートの作成とデザイン](../../message-center/using/creating-the-message-template.md)この手順では、イベントをメッセージにリンクする必要があります。
1. [メッセージをテストします](../../message-center/using/testing-message-templates.md)。
1. [メッセージテンプレートをパブリッシュします](../../message-center/using/publishing-message-templates.md)。

>[!NOTE]
>
>上記の手順はすべて、**コントロールインスタンス**&#x200B;で実行されます。 コントロールインスタンスでテンプレートを公開すると、すべての&#x200B;**実行インスタンス**&#x200B;にも公開されます。 トランザクションメッセージインスタンスについて詳しくは、[トランザクションメッセージのアーキテクチャ](../../message-center/using/transactional-messaging-architecture.md)を参照してください。

### 実行インスタンスでのイベント処理

トランザクションメッセージテンプレートを設計して公開すると、対応するイベントがトリガーされた場合、以下の主な手順が&#x200B;**実行インスタンス**&#x200B;で実行されます。

1. 外部情報システムによってイベントが生成されると、関連データが&#x200B;**PushEvent**&#x200B;および&#x200B;**PushEvents**&#x200B;メソッドを介してCampaignに送信されます。 [イベントの収集](../../message-center/using/about-event-processing.md#event-collection)を参照してください。
1. イベントは、適切なメッセージテンプレートにリンクされています。 [テンプレート](../../message-center/using/about-event-processing.md#routing-towards-a-template)へのルーティングを参照してください。
1. エンリッチメントステージが完了すると、配信が送信されます。 [配信の実行](../../message-center/using/delivery-execution.md)を参照してください。 各ターゲット受信者は、パーソナライズされたメッセージを受信します。

## 関連トピック {#related-topics}

* [通信チャネルの概要](../../delivery/using/communication-channels.md)
* [配信の作成に関する主な手順](../../delivery/using/steps-about-delivery-creation-steps.md)
* [トランザクションメッセージのアーキテクチャ](../../message-center/using/transactional-messaging-architecture.md)
* [トランザクションメッセージレポートへのアクセス](../../message-center/using/about-transactional-messaging-reports.md)
