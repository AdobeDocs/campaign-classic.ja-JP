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
translation-type: tm+mt
source-git-commit: d15e953740b0a4dd8073b36fd59b4c4e44906340
workflow-type: tm+mt
source-wordcount: '261'
ht-degree: 75%

---


# Adobe Experience Cloud Triggers について{#about-adobe-experience-triggers}

[!DNL Triggers] は、パイプラインを使用して Adobe Campaign と Adobe Analytics を統合します。パイプラインは、Web サイトからユーザーのアクションまたはトリガーを取得します。買い物かごの放棄は、トリガーの一例です。トリガーが Adobe Campaign で処理されて、ほぼリアルタイムで E メールが送信されます。

[!DNL Triggers] は、ユーザーのアクションの後、短時間のうちにマーケティングアクションを実行します。通常の応答時間は 1 時間未満です。

設定は最小限で、サードパーティが関与しないので、より機敏な統合処理が可能です。
また、マーケティングアクティビティのパフォーマンスに影響を与えることなく、大量のトラフィックをサポートします。例えば、この統合機能では 1 時間に 100 万個のトリガーを処理できます。

## [!DNL Triggers] アーキテクチャ {#triggers-architecture}

[!DNL pipelined] プロセスは、Adobe Campaign マーケティングサーバーで常に動作しています。パイプラインに接続し、イベントを取得して直ちに処理します。

![](assets/triggers_2.png)

[!DNL pipelined] プロセスは、認証サービスを使用して Experience Cloud にログインし、秘密鍵を送信します。認証サービスがトークンを返します。トークンは、イベントの取得時に認証に使用されます。

For more information on authentication, refer to this [page](../../integrations/using/configuring-adobe-io.md).

>[!NOTE]
>
>デフォルトの実装以外で提供されるACXパッケージの一部として、イベントのさらなる処理を行います。 受信したイベントは、JavaScriptコードを使用して即座に処理されます。 これ以上処理をおこなうことなく、リアルタイムにデータベーステーブルに保存されます。
トリガーは、電子メールを送信するキャンペーンワークフローでのターゲティングに使用されます。 キャンペーンは、イベントをトリガーした顧客が電子メールを受信するように設定されます。
