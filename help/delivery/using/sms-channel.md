---
product: campaign
title: SMS チャネルの基本を学ぶ
description: SMS チャネルの基本を学ぶ
feature: SMS
role: User
exl-id: 6fc2ab09-8ea7-4865-88ad-bd45eee68958
source-git-commit: d3d731c64cb5a430de6adac3aeb326f74134c436
workflow-type: tm+mt
source-wordcount: '370'
ht-degree: 68%

---

# SMS チャネルの基本を学ぶ{#sms-channel}

Adobe Campaign を使用して、顧客のモバイルデバイスにテキストメッセージを送信します。SMS エディターからテキスト形式で、メッセージの作成、パーソナライズ、プレビューを行うことができます。

SMS は、ユーザーがどこにいても到達するための直接的で非常に効果的なチャネルです。 開封率が高く、ほぼ瞬時に配信できる SMS は、時間依存のアラート、トランザクションの更新、簡潔なプロモーションメッセージに最適です。 SMS を使用してクロスチャネル戦略を補完し、効果的なリアルタイムのコミュニケーションを実現します。 SMS チャネルを設定して効果的に使用する方法については、[Adobe Campaign v8 ドキュメント ](https://experienceleague.adobe.com/docs/campaign/campaign-v8/send/sms/sms.html?lang=ja){target=_blank} を参照してください。

Campaign v8 のプロモーションイニシアチブの一環として、Campaign Classicのドキュメントを再編成しました。 共通機能は、Campaign v8 ドキュメントセットでのみ使用できるようになりました。

>[!BEGINTABS]

>[!TAB SMS チャネルドキュメント ]

SMS チャネルについて詳しくは、[Campaign v8 ドキュメント ](https://experienceleague.adobe.com/docs/campaign/campaign-v8/send/sms/sms.html?lang=ja){target=_blank} を参照してください。


[![画像](../../assets/do-not-localize/learn-more-button.svg)](https://experienceleague.adobe.com/docs/campaign/campaign-v8/send/sms/sms.html?lang=ja){target=_blank}


>[!TAB SMS 配信の作成 ]

SMS 配信の作成に関連する主な手順について詳しくは、次の Campaign v8 ドキュメントを参照してください。

* [SMS チャネルの概要](https://experienceleague.adobe.com/docs/campaign/campaign-v8/send/sms/sms.html?lang=ja){target="_blank"}：顧客のモバイルデバイスにテキストメッセージを送信する方法について説明します。
* [SMS 配信の作成](https://experienceleague.adobe.com/docs/campaign/campaign-v8/send/sms/create-sms/create-sms.html?lang=ja){target="_blank"}：新しい SMS 配信の作成に必要な様々な手順について説明します。
* [コンテンツの定義](https://experienceleague.adobe.com/docs/campaign/campaign-v8/send/sms/create-sms/sms-content.html?lang=ja){target="_blank"}：SMS メッセージのコンテンツをパーソナライズする方法について説明します。
* [オーディエンスの選択](https://experienceleague.adobe.com/docs/campaign/campaign-v8/send/sms/create-sms/sms-audience.html?lang=ja){target="_blank"}：メインターゲットは、Adobe Campaign データベースから抽出されるか、外部ファイルに保存することもできます。
* [SMS 配達確認の送信](https://experienceleague.adobe.com/docs/campaign/campaign-v8/send/sms/validate-sms/sms-proofs.html?lang=ja)：配信の検証サイクルの設定が不可欠です。コンテンツをオーディエンスに送信する前に、必ず承認するようにしてください。
* [オーディエンスへの送信](https://experienceleague.adobe.com/docs/campaign/campaign-v8/send/sms/validate-sms/sms-send.html?lang=ja)：SMS が検証されると、オーディエンスに送信できるようになります。
* [SMS の監視とトラッキング](https://experienceleague.adobe.com/docs/campaign/campaign-v8/send/sms/sms-monitor.html?lang=ja)：マーケティングキャンペーンが効率的であることを確認するために、SMS 配信を監視します。


>[!TAB SMS 設定 ]

SMS 設定については、次のページを参照してください。

* [スタンドアロン設定](sms-set-up.md)：スタンドアロンインスタンスで SMS チャネルを設定する方法について説明します。
* [ミッドソーシング設定](sms-set-up-mid.md)：ミッドサーバーを使用して携帯電話に送信する方法について説明します。
* [SMS コネクタ](sms-protocol.md)：SMS コネクタのプロトコルと設定について説明します。
* [その他の設定](sms-send.md)：詳細設定パラメーターやその他の追加設定について説明します。
* [トラブルシューティング](troubleshooting-sms.md)：一連の潜在的な問題とその解決策をリストしました。

>[!ENDTABS]



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