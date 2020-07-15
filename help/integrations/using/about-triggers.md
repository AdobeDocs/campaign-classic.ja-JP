---
title: Adobe Experience Manager について
seo-title: Adobe Experience Manager について
description: Adobe Experience Manager について
seo-description: null
page-status-flag: never-activated
uuid: c523822f-8178-4989-bd88-ab402470e540
contentOwner: sauviat
products: SG_CAMPAIGN/CLASSIC
audience: integrations
content-type: reference
topic-tags: adobe-experience-manager
discoiquuid: 0d617f1c-0d0b-489f-9027-a92b1f1eee37
index: y
internal: n
snippet: y
translation-type: tm+mt
source-git-commit: 0112d5bd052ad66169225073276d1da4f3c245d8
workflow-type: tm+mt
source-wordcount: '479'
ht-degree: 3%

---


# Adobe Experience Cloud Triggers について{#about-adobe-experience-triggers}

[!DNL Triggers] は、パイプラインを使用してAdobe CampaignとアドビAnalyticsを統合します。 パイプラインは、Webサイトからユーザーのアクションまたはトリガーを取得します。 買い物かごの放棄は、トリガーの一例です。 トリガーは、ほぼリアルタイムで電子メールを送信するためにAdobe Campaignで処理されます。

[!DNL Triggers] ユーザーのアクションの後、短い範囲でマーケティングアクションを実行します。 通常の応答時間は1時間未満です。

設定は最小限で、サードパーティが関与しないため、より迅速な統合が可能です。
また、マーケティングアクティビティのパフォーマンスに影響を与えることなく、大量のトラフィックをサポートします。 例として、統合では1時間に100万個のトリガーを処理できます。

## [!DNL Triggers] 建築 {#triggers-architecture}

### パイプラインとは {#pipeline-explanation}

>[!CAUTION]
>
>アドビのパイプラインサービスのイベントを作成し、利用できるのは、Adobe Cloudソリューションのみです。 アドビの外部のシステムは使用できません。

パイプラインは、 [Apache Kafkaを使用するExperience Cloudでホストされるメッセージングシステム](http://kafka.apache.org/)です。 これは、ソリューション間で簡単にデータを渡す方法です。 さらに、パイプラインはデータベースではなくメッセージキューです。 生産者はイベントを動かし、消費者は流れを聞き、イベントで自分の好きなように行動する。 イベントは数日間保持されますが、それ以上は保持されません。 24時間365日リッスンし、イベントを即座に処理することを目的としています。

![](assets/triggers_1.png)

### パイプラインの動作 {#how-pipeline-work}

この [!DNL pipelined] プロセスは、常にAdobe Campaignマーケティングサーバーで実行されます。 パイプラインに接続し、イベントを取得して、直ちに処理します。

![](assets/triggers_2.png)

プロセスは、認証サービスを使用してExperience Cloudにログインし、秘密鍵を送信します。 [!DNL pipelined] 認証サービスはトークンを返します。 トークンは、イベントの取得時に認証に使用されます。 [!DNL Triggers] は、単純なGET要求を使用してREST Webサービスから取得されます。 応答はJSON形式です。 リクエストのパラメーターには、トリガーの名前と、最後に取得されたメッセージを示すポインターが含まれます。 プロセスは、 [!DNL pipelined] それを自動的に処理します。

## Adobe Experience Cloud Triggersを使用したAdobe Campaignクラシックとの統合

次に、いくつかのベストプラクティスを示 [!DNL Triggers] します。

* データはキャンペーン時に格納する必要があり [!DNL Trigger] ます。 遅延が発生するので、直接処理しないでください。
* タイムスタンプは、データベースではなく、メッセージから確認する必要があります。
* 重複を削除するには、TriggerTimestampとトリガーIDを使用します。

>[!CAUTION]
>
>次の例は、そのまま使用できる状態では提供されていません。 これは、様々な実装から得られる具体的な例です。

パイプラインイベントが自動的にダウンロードされます。 これらのイベントは、フォームを使用して監視できます。

![](assets/triggers_3.png)

パイプラインイベントノードは組み込まれておらず、追加する必要があります。また、関連するフォームをキャンペーンで作成する必要があります。 これらの操作は、エキスパートユーザーにのみ制限されます。 この点について詳しくは、次の節を参照してください。 [ナビゲーション階層](../../configuration/using/about-navigation-hierarchy.md) 、 [フォームの](../../configuration/using/editing-forms.md)編集。

トリガーに対する反復的なキャンペーンワークフロークエリです。トリガーがマーケティング条件に一致する場合は、配信を開始します。

![](assets/triggers_4.png)
