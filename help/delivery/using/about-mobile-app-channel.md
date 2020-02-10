---
title: Adobe Campaign Classicのモバイルアプリチャネルについて
description: ここでは、Adobe Campaign Classicのモバイルアプリチャネルに固有の一般情報を提供します。
page-status-flag: never-activated
uuid: e8d26b33-dc7c-4abd-956a-92f419a117e1
contentOwner: sauviat
products: SG_CAMPAIGN/CLASSIC
audience: delivery
content-type: reference
topic-tags: sending-push-notifications
discoiquuid: 6b3fe8b9-dae6-4f8e-83e1-3376c0fe72a5
index: y
internal: n
snippet: y
translation-type: tm+mt
source-git-commit: c581f22261af7e083f6bd47e603d17d2d71e7ce6

---


# モバイルアプリチャネルについて{#about-mobile-app-channel}

>[!CAUTION]
>
>このドキュメントは、モバイルアプリケーションを Adobe Campaign プラットフォームに統合するプロセスについて説明しています。モバイルアプリケーションの作成方法や、通知を管理するためのモバイルアプリケーションの設定方法については説明していません。詳しくは、Apple（[https://developer.apple.com/](https://developer.apple.com/)）および Android（[https://developer.android.com/index.html](https://developer.android.com/index.html)）の公式ドキュメントを参照してください。

以下の節では、モバイルアプリチャネルに固有の情報を示します。 For global information on how to create a delivery, refer to [this section](../../delivery/using/steps-about-delivery-creation-steps.md).

**モバイルアプリチャネル**&#x200B;では、Adobe Campaign プラットフォームを使用して iOS および Android の端末にパーソナライズされた通知をアプリ経由で送信できます。2 つの配信チャネルが使用可能です。

* Apple  のモバイルデバイスへの通知の送信を有効にする iOS チャネル：

   ![](assets/nmac_intro_2.png)

* Android のモバイルデバイスへのデータメッセージの送信を有効にする Android チャネル。

   ![](assets/nmac_intro_1.png)

これら 2 つのチャネルに対応して、キャンペーンワークフローには 2 つの配信アクティビティがあります。

![](assets/nmac_intro_3.png)

>[!NOTE]
>
>また、トランザクションメッセージに使用できるトランザクションメッセージテンプレートも 2 つあります。

ユーザーがアプリケーションのコンテキストに一致する画面を表示するための通知を有効化した場合のアプリケーションの動作を定義することもできます。次に例を示します。

* 荷物が倉庫から出荷されたことを顧客に知らせるために通知を送信します。顧客が通知を有効にすると、配信関連の情報が記載されたページが開きます。
* ユーザーがカートに商品を追加したものの、購入を完了することなくアプリケーションを終了した場合、カートの内容が破棄されたことを知らせる通知を送信します。ユーザーが通知を有効化すると、画面にその商品が表示されます。

>[!CAUTION]
>
>* モバイルアプリケーションに送信する通知が、Apple（Apple Push Notification Service）および Google（Google Cloud Messaging）によって指定されている条件を満たしていることを確認する必要があります。
>* 警告：国によっては、モバイルアプリケーションから収集するデータタイプとその処理の目的についてユーザーに知らせることが法律によって定められている場合があります。法律を確認する必要があります。


The **[!UICONTROL NMAC opt-out management]** (mobileAppOptOutMgt) workflow updates notification unsubscriptions on mobile devices. このワークフローについて詳しくは、[ワークフローガイド](../../workflow/using/mobile-app-channel.md)を参照してください。

Adobe Campaign はバイナリと HTTP/2 APNS の両方に対応しています。For more details on the configuration steps, refer to the [Connectors](../../delivery/using/setting-up-mobile-app-channel.md#connectors) section.
