---
product: campaign
title: SMS チャネルの基本を学ぶ
description: SMS チャネルの基本を学ぶ
feature: SMS
role: User
exl-id: 6fc2ab09-8ea7-4865-88ad-bd45eee68958
source-git-commit: 42cec0e9bede94a2995a5ad442822512bda14f2b
workflow-type: tm+mt
source-wordcount: '256'
ht-degree: 21%

---

# SMS チャネルの基本を学ぶ{#sms-channel}

Adobe Campaign を使用して、顧客のモバイルデバイスにテキストメッセージを送信します。SMS エディターからテキスト形式で、メッセージの作成、パーソナライズ、プレビューを行うことができます。

SMS 配信の作成に関連する主な手順については、Campaign v8 ドキュメントを参照してください。

* [SMS チャネルの概要 ](https://experienceleague.adobe.com/docs/campaign/campaign-v8/send/sms/sms.html?lang=ja){target="_blank"}：顧客のモバイルデバイスにテキストメッセージを送信する方法について説明します。
* [SMS 配信の作成 ](https://experienceleague.adobe.com/docs/campaign/campaign-v8/send/sms/create-sms/create-sms.html?lang=ja){target="_blank"}：新しい SMS 配信の作成に必要な様々な手順を確認します。
* [ コンテンツの定義 ](https://experienceleague.adobe.com/docs/campaign/campaign-v8/send/sms/create-sms/sms-content.html?lang=ja){target="_blank"}:SMS メッセージのコンテンツをパーソナライズする方法を説明します。
* [ オーディエンスを選択 ](https://experienceleague.adobe.com/docs/campaign/campaign-v8/send/sms/create-sms/sms-audience.html?lang=ja){target="_blank"}：メインターゲットはAdobe Campaign データベースから抽出され、外部ファイルに保存することもできます。
* [SMS 配達確認の送信 ](https://experienceleague.adobe.com/docs/campaign/campaign-v8/send/sms/validate-sms/sms-proofs.html?lang=ja)：配信の検証サイクルの設定が不可欠です。 コンテンツをオーディエンスに送信する前に、必ず承認するようにしてください。
* [ オーディエンスに送信 ](https://experienceleague.adobe.com/docs/campaign/campaign-v8/send/sms/validate-sms/sms-send.html?lang=ja):SMS が検証されると、その SMS をオーディエンスに送信できるようになりました。
* [SMS の監視と追跡 ](https://experienceleague.adobe.com/docs/campaign/campaign-v8/send/sms/sms-monitor.html?lang=ja)：マーケティングキャンペーンが効率的であることを確認するために、SMS 配信を監視します。

設定について詳しくは、次のページを参照してください。

* [ スタンドアロン設定 ](sms-set-up.md)：スタンドアロンインスタンスで SMS チャネルを設定する方法を説明します。
* [ ミッドソーシング設定 ](sms-set-up-mid.md)：ミッドサーバーを使用して携帯電話に送信する方法を説明します。
* [SMS コネクタ ](sms-protocol.md):SMS コネクタのプロトコルと設定について説明します。
* [ 追加設定 ](sms-send.md)：詳細設定パラメーターやその他の追加設定について説明します。
* [ トラブルシューティング ](troubleshooting-sms.md)：一連の潜在的な問題とその解決策をリストしました。

<!--
Use Adobe Campaign to send personalized SMS messages.

Before starting sending SMS:

* Make sure recipient profiles contain at least a mobile phone in their profile.
* Learn more about the Adobe Campaign [Delivery best practices](delivery-best-practices.md).

The key steps to send a SMS are as follows:

* [Configure the SMS channel](sms-set-up.md)
* [Create a SMS delivery](sms-create.md)
* [Define the audience](sms-create.md#selecting-the-target-population)
* [Define the SMS content](sms-create.md#defining-the-sms-content)
* [Send, monitor and track SMS](sms-send.md)
* [Troubleshoot](troubleshooting-sms.md)

In addition, you need to be familiar with SMS protocol and settings. Walk through the connection set up between Adobe Campaign and a SMPP provider in [this document](sms-protocol.md)

For global information on how to create a delivery, refer to [this section](steps-about-delivery-creation-steps.md).

>[!NOTE]
>
>Adobe Campaign also lets you submit notifications on mobile terminals, via its **Adobe Campaign Mobile App Channel (NMAC)** option. 
> 
>For more on this, refer to the [Get started with mobile app channel](about-mobile-app-channel.md) section.
-->