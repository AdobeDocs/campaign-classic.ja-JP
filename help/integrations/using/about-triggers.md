---
title: Adobe Experience Cloud トリガーについて
description: Adobe Experience Cloudトリガーの実装を開始する
page-status-flag: never-activated
uuid: c523822f-8178-4989-bd88-ab402470e540
contentOwner: sauviat
products: SG_CAMPAIGN/CLASSIC
audience: integrations
content-type: reference
topic-tags: adobe-experience-manager
discoiquuid: 0d617f1c-0d0b-489f-9027-a92b1f1eee37
translation-type: tm+mt
source-git-commit: 48acf8cbc52a54a2dd08f0b8f29be57d4e5e006f
workflow-type: tm+mt
source-wordcount: '228'
ht-degree: 84%

---


# Adobe Experience Cloudトリガーの使い始めに{#about-adobe-experience-triggers}

[!DNL Triggers] は、パイプラインを使用して Adobe Campaign と Adobe Analytics を統合します。パイプラインは、Web サイトからユーザーのアクションまたはトリガーを取得します。買い物かごの放棄は、トリガーの一例です。トリガーが Adobe Campaign で処理されて、ほぼリアルタイムで E メールが送信されます。

>[!CAUTION]
>
>この機能は、製品の一部として初期状態では使用できません。実装するには、アドビのコンサルティングサービス部門に依頼する必要があります。詳細については、Adobeの担当者にお問い合わせください。

[!DNL Triggers] は、ユーザーのアクションの後、短時間のうちにマーケティングアクションを実行します。通常の応答時間は 1 時間未満です。

設定は最小限で、サードパーティが関与しないので、より機敏な統合処理が可能です。
また、マーケティングアクティビティのパフォーマンスに影響を与えることなく、大量のトラフィックをサポートします。例えば、この統合機能では 1 時間に 100 万個のトリガーを処理できます。

## [!DNL Triggers] アーキテクチャ {#triggers-architecture}

[!DNL pipelined] プロセスは、Adobe Campaign マーケティングサーバーで常に動作しています。パイプラインに接続し、イベントを取得して直ちに処理します。

![](assets/triggers_2.png)

[!DNL pipelined] プロセスは、認証サービスを使用して Experience Cloud にログインし、秘密鍵を送信します。認証サービスがトークンを返します。トークンは、イベントの取得時に認証に使用されます。

For more information on authentication, refer to this [page](../../integrations/using/configuring-adobe-io.md).
