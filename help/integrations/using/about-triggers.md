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
translation-type: ht
source-git-commit: 70b143445b2e77128b9404e35d96b39694d55335
workflow-type: ht
source-wordcount: '479'
ht-degree: 100%

---


# Adobe Experience Cloud Triggers について{#about-adobe-experience-triggers}

[!DNL Triggers] は、パイプラインを使用して Adobe Campaign と Adobe Analytics を統合します。パイプラインは、Web サイトからユーザーのアクションまたはトリガーを取得します。買い物かごの放棄は、トリガーの一例です。トリガーが Adobe Campaign で処理されて、ほぼリアルタイムで E メールが送信されます。

[!DNL Triggers] は、ユーザーのアクションの後、短時間のうちにマーケティングアクションを実行します。通常の応答時間は 1 時間未満です。

設定は最小限で、サードパーティが関与しないので、より機敏な統合処理が可能です。
また、マーケティングアクティビティのパフォーマンスに影響を与えることなく、大量のトラフィックをサポートします。例えば、この統合機能では 1 時間に 100 万個のトリガーを処理できます。

## [!DNL Triggers] アーキテクチャ {#triggers-architecture}

### パイプラインとは {#pipeline-explanation}

>[!CAUTION]
>
>アドビのパイプラインサービスのイベントを生成し利用できるのは、アドビのクラウドソリューションだけです。アドビ以外のシステムではできません。

パイプラインは Experience Cloud でホストされるメッセージングシステムで、[Apache Kafka](http://kafka.apache.org/) を使用します。これは、ソリューション間で簡単にデータを渡す方法です。さらに、パイプラインはデータベースではなくメッセージキューです。プロデューサーはパイプラインにイベントをプッシュし、コンシューマーはフローをリッスンして、プロデューサーの希望どおりにイベントを処理します。イベントは数日間保持されますが、それ以上は保持されません。その目的は、24 時間 365 日リッスンし、イベントを即座に処理することです。

![](assets/triggers_1.png)

### パイプラインの仕組み {#how-pipeline-work}

[!DNL pipelined] プロセスは、Adobe Campaign マーケティングサーバーで常に動作しています。パイプラインに接続し、イベントを取得して直ちに処理します。

![](assets/triggers_2.png)

[!DNL pipelined] プロセスは、認証サービスを使用して Experience Cloud にログインし、秘密鍵を送信します。認証サービスがトークンを返します。トークンは、イベントの取得時に認証に使用されます。[!DNL Triggers] は、シンプルな GET リクエストを使用して REST Web サービスから取得されます。応答は JSON 形式です。リクエストのパラメーターには、トリガーの名前と、最後に取得されたメッセージを示すポインターが含まれます。[!DNL pipelined] プロセスは、それを自動的に処理します。

## Adobe Campaign Classic での Adobe Experience Cloud Triggers 統合機能の使用

以下に、[!DNL Triggers] のベストプラクティスをいくつか示します。

* [!DNL Trigger] データは Campaign での受信時に保存する必要があります。遅延が発生する可能性があるので、直接処理しないでください。
* タイムスタンプは、データベースではなく、メッセージから確認してください。
* 重複を削除する場合は、TriggerTimestamp とトリガー ID を使用します。

>[!CAUTION]
>
>次の例は、標準では提供されていません。これは、考えられる様々な実装から得られる具体的な例です。

パイプラインイベントが自動的にダウンロードされます。これらのイベントは、フォームを使用して監視できます。

![](assets/triggers_3.png)

パイプラインイベントノードは組み込まれておらず、追加する必要があります。また、関連フォームも Campaign で作成する必要があります。これらの操作は、エキスパートユーザーのみに制限されます。この点について詳しくは、[ナビゲーション階層](../../configuration/using/about-navigation-hierarchy.md)および[フォームの編集](../../configuration/using/editing-forms.md)の節を参照してください。

反復的なキャンペーンワークフローでトリガーに対するクエリが実行されます。トリガーがマーケティング条件に一致する場合は、配信が開始されます。

![](assets/triggers_4.png)
