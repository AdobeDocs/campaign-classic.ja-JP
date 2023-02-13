---
product: campaign
title: Adobe Experience Cloud Triggers について
description: Adobe Experience Cloud Triggers の実装入門
audience: integrations
content-type: reference
exl-id: 0e337620-a49f-4e14-8c67-9279d74736f1
source-git-commit: 0a59b0dbdbe70cf8993ce7153b8f3c049c1f1108
workflow-type: tm+mt
source-wordcount: '235'
ht-degree: 100%

---

# Campaign と Experience Cloud トリガーの連携{#about-adobe-experience-triggers}

![](../../assets/common.svg)

[!DNL Triggers] は、パイプラインを使用して Adobe Campaign と Adobe Analytics を統合します。パイプラインは、web サイトからユーザーのアクションまたはトリガーを取得します。買い物かごの放棄は、トリガーの一例です。トリガーが Adobe Campaign で処理されて、ほぼリアルタイムで E メールが送信されます。

>[!CAUTION]
>
>この機能は、製品の一部として標準搭載はされていません。この実装では、最初にアドビのサポートでチケットを開く必要があります。すると、この[ページ](../../integrations/using/configuring-pipeline.md#prerequisites)で詳しく説明されている手順を実行できるようになります。

[!DNL Triggers] は、ユーザーのアクションの後、短時間のうちにマーケティングアクションを実行します。通常の応答時間は 1 時間未満です。

設定は最小限で、サードパーティが関与しないので、より機敏な統合処理が可能です。
また、マーケティングアクティビティのパフォーマンスに影響を与えることなく、大量のトラフィックをサポートします。例えば、この統合機能では 1 時間に 100 万個のトリガーを処理できます。

## [!DNL Triggers] アーキテクチャ {#triggers-architecture}

[!DNL pipelined] プロセスは、Adobe Campaign マーケティングサーバーで常に動作しています。パイプラインに接続し、イベントを取得してただちに処理します。

![](assets/triggers_2.png)

[!DNL pipelined] プロセスは、認証サービスを使用して Experience Cloud にログインし、秘密鍵を送信します。認証サービスがトークンを返します。トークンは、イベント取得時の認証に使用されます。

認証について詳しくは、[このページ](../../integrations/using/configuring-adobe-io.md)を参照してください。
