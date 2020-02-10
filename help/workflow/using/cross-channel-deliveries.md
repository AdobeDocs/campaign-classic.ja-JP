---
title: クロスチャネル配信
seo-title: クロスチャネル配信
description: クロスチャネル配信
seo-description: null
page-status-flag: never-activated
uuid: 191ff39e-f739-48b3-8865-ad1b641b7499
contentOwner: sauviat
products: SG_CAMPAIGN/CLASSIC
audience: workflow
content-type: reference
topic-tags: action-activities
discoiquuid: 8dda45b4-4b5d-4b4e-a8b4-45d9bc49aaf3
index: y
internal: n
snippet: y
translation-type: tm+mt
source-git-commit: 20f835c357d016643ea1f3209ee4dfb6d3239f90

---


# クロスチャネル配信{#cross-channel-deliveries}

Cross-channel deliveries are available in the **[!UICONTROL Deliveries]** tab of campaign workflow activities.

クロスチャネル配信を使用して、特定のチャネルに固有の配信を作成できます。従来の配信ウィザードと同じ方法で、配信およびコンテンツのベースとなるテンプレートを指定できます。

次に、使用可能な様々なチャネルを示します。

* [E メール](../../delivery/using/about-email-channel.md)
* [ダイレクトメール](../../delivery/using/about-direct-mail-channel.md)
* [モバイル](../../delivery/using/sms-channel.md)
* [Twitter](../../social/using/publishing-on-twitter.md)
* [Facebook](../../social/using/publishing-on-facebook.md)
* [iOS](../../delivery/using/creating-notifications.md#sending-notifications-on-ios)
* [Android](../../delivery/using/creating-notifications.md#sending-notifications-on-android)

各種ターゲティングアクティビティを使用して、ワークフローの配信アップストリームのターゲットを指定できます。

例えば、ここでは、プッシュ通知購読者に E メールまたは SMS を送信し、1 週間後にプッシュ通知を通知するワークフローを作成します。手順は次のとおりです。

1. キャンペーンを作成します。
1. キャンペーン **[!UICONTROL Targeting and workflows]** のタブで、ワークフローにを **[!UICONTROL Query]** 追加します。
1. クエリを設定します。例えば、ここでは、ターゲットディメンションとしてプッシュ通知を購読している受信者を選択します。

   >[!NOTE]
   >
   >プッシュ通知の場合、必ず&#x200B;**購読者のアプリケーション**&#x200B;ターゲットディメンションを使用するようにします。

   ![](assets/cross_channel_delivery_1.png)

1. クエリにフィルター条件を追加します。この場合、モバイル番号または E メールアドレスを持つ受信者を選択します。

   ![](assets/cross_channel_delivery_2.png)

1. Add a **[!UICONTROL Split]** activity to your workflow to divide recipients who have a mobile number and those who have an email address.
1. In the **[!UICONTROL Delivery]** tab, select a delivery for each of your targets.

   ワークフローの配信アクティビティをダブルクリックして、従来の配信ウィザードと同じ方法で配信を作成します。詳しくは、この[ページ](../../delivery/using/about-email-channel.md)を参照してください。

   ![](assets/cross_channel_delivery_3.png)

1. Add and configure a **[!UICONTROL Wait]** activity in order for the recipients not to receive too many deliveries at once.
1. Add a **[!UICONTROL Split]** activity to divide subscribers of an iOS or Android mobile applications.

   各オペレーティングシステム用のサービスを選択します。サービスの作成について詳しくは、この[ページ](../../delivery/using/setting-up-mobile-app-channel.md#creating-the-service-and-collecting-subscriptions)を参照してください。

   ![](assets/cross_channel_delivery_4.png)

1. 各オペレーティングシステム用のモバイルアプリケーション配信を選択および設定します。

   ![](assets/cross_channel_delivery_5.png)

