---
product: campaign
title: Adobe Experience Cloud Triggers について
description: Adobe Experience Cloud Triggers の実装入門
feature: Triggers
badge-v7: label="v7" type="Informative" tooltip="Campaign Classicv7 に適用"
badge-v8: label="v8" type="Positive" tooltip="Campaign v8 にも適用されます"
audience: integrations
content-type: reference
exl-id: 0e337620-a49f-4e14-8c67-9279d74736f1
source-git-commit: 3a9b21d626b60754789c3f594ba798309f62a553
workflow-type: tm+mt
source-wordcount: '269'
ht-degree: 96%

---

# Campaign と Experience Cloud トリガーの連携{#about-adobe-experience-triggers}

[!DNL Triggers] は、パイプラインを使用して Adobe Campaign と Adobe Analytics を統合します。パイプラインは、web サイトからユーザーのアクションまたはトリガーを取得します。買い物かごの放棄は、トリガーの一例です。トリガーが Adobe Campaign で処理されて、ほぼリアルタイムで E メールが送信されます。

>[!CAUTION]
>
>この機能は、製品の一部として標準搭載はされていません。この実装では、最初にアドビのサポートでチケットを開く必要があります。すると、この[ページ](../../integrations/using/configuring-pipeline.md#prerequisites)で詳しく説明されている手順を実行できるようになります。

[!DNL Triggers] は、ユーザーのアクションの後、短時間のうちにマーケティングアクションを実行します。通常の応答時間は 1 時間未満です。

設定は最小限で、サードパーティが関与しないので、より機敏な統合処理が可能です。
また、マーケティングアクティビティのパフォーマンスに影響を与えることなく、大量のトラフィックをサポートします。例えば、この統合機能では 1 時間に 100 万個のトリガーを処理できます。

![](assets/do-not-localize/book.png) [Experience Cloud トリガー](https://experienceleague.adobe.com/docs/experience-cloud/triggers/create.html?lang=ja)を作成し、重要なコンシューマーの行動を特定、定義、監視する方法を説明します。

## [!DNL Triggers] アーキテクチャ {#triggers-architecture}

[!DNL pipelined] プロセスは、Adobe Campaign マーケティングサーバーで常に動作しています。パイプラインに接続し、イベントを取得してただちに処理します。

![](assets/triggers_2.png)

[!DNL pipelined] プロセスは、認証サービスを使用して Experience Cloud にログインし、秘密鍵を送信します。認証サービスがトークンを返します。トークンは、イベント取得時の認証に使用されます。

認証について詳しくは、[このページ](../../integrations/using/configuring-adobe-io.md)を参照してください。
