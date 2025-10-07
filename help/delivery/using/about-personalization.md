---
product: campaign
title: パーソナライゼーションの基本を学ぶ
description: Campaign でメッセージをパーソナライズし条件付きコンテンツを使用する方法を説明します。
badge-v8: label="v8 にも適用されます" type="Positive" tooltip="Campaign v8 にも適用されます"
feature: Personalization
role: User
exl-id: 555082a2-1b62-4aa4-b80c-77b1a1ef9491
source-git-commit: a1e9fec0e9c85bf25b79e24a7432dfb45bd1a0cb
workflow-type: tm+mt
source-wordcount: '438'
ht-degree: 81%

---

# パーソナライゼーションの基本を学ぶ{#about-personalization}

Adobe Campaign で配信されるメッセージは、コンテンツや外観をいくつかの方法でパーソナライズできます。さらに、受信者のプロファイルから取得した条件に基づいて、それらの方法を組み合わせることもできます。メール配信の場合は、配信の要素やパーソナライゼーション条件を、メッセージの「**[!UICONTROL ソース]**」タブに JavaScript を記述して直接定義できます。Adobe Campaign には、全体として次のようなパーソナライゼーション機能が備わっています。

* メッセージ形式のパーソナライズ：[メッセージコンテンツ](defining-the-email-content.md#message-content)を参照してください。
* パーソナライゼーションフィールドの動的な挿入：[パーソナライゼーションフィールド](personalization-fields.md)を参照してください。
* 定義済みパーソナライゼーションブロックの挿入：[パーソナライゼーションブロック](personalization-blocks.md)を参照してください。
* 条件付きコンテンツの作成：[条件付きコンテンツ](conditional-content.md)の節を参照してください。

>[!CAUTION]
>
>次に示す変数は内部変数です。これらをパーソナライゼーションに使用できますが、値の変更は絶対にしないでください。**delivery**、**message**、**dataSource**、**targetData**、**provider**、**coupon**、**couponValue**、**proposition**。


Adobe Campaignを使用して配信をパーソナライズし、各受信者のプロファイルや興味の対象に合わせてメッセージを送信します。

Personalizationは、メッセージをより関連性が高く、魅力的にするのに役立ちます。 受信者データを使用して、コンテンツの調整、動的フィールドの追加、条件に基づく様々な情報の表示を行うことができます。 配信でのパーソナライゼーション機能の設定および使用方法については、[Adobe Campaign v8 ドキュメント &#x200B;](https://experienceleague.adobe.com/docs/campaign/campaign-v8/send/personalize/personalize.html){target=_blank} を参照してください。

Campaign v8 のプロモーションイニシアチブの一環として、Campaign Classic のドキュメントを再編成しました。共通機能は、Campaign v8 ドキュメントセットでのみ使用できるようになりました。

>[!BEGINTABS]

>[!TAB  コンテンツのパーソナライゼーションドキュメント ]

コンテンツのパーソナライゼーションについて詳しくは、[Campaign v8 ドキュメント &#x200B;](https://experienceleague.adobe.com/docs/campaign/campaign-v8/send/personalize/personalize.html){target=_blank} を参照してください。


[![画像](../../assets/do-not-localize/learn-more-button.svg)](https://experienceleague.adobe.com/docs/campaign/campaign-v8/send/personalize/personalize.html){target=_blank}


>[!TAB メール配信作成]

メール配信の作成に関連する主な手順について詳しくは、次の Campaign v8 ドキュメントを参照してください。

* [メール配信の作成](https://experienceleague.adobe.com/docs/campaign/campaign-v8/send/emails/email.html?lang=ja){target="_blank"}：メール配信の作成に必要な様々な手順について説明します。
* [メールコンテンツの定義](https://experienceleague.adobe.com/docs/campaign/campaign-v8/send/emails/defining-the-email-content.html?lang=ja){target="_blank"}：メールに含める内容（送信者、件名、コンテンツ、画像）を定義します。
* [インタラクティブコンテンツの定義](https://experienceleague.adobe.com/docs/campaign/campaign-v8/send/emails/defining-interactive-content.html?lang=ja){target="_blank"}：動的なメールを送信するには、インタラクティブな AMP for Email 形式を使用します。
* [日本の携帯電話向けのメールの送信](https://experienceleague.adobe.com/docs/campaign/campaign-v8/send/emails/sending-emails-on-japanese-mobiles.html?lang=ja){target="_blank"}：携帯電話向けのメールには、3 種類ある日本固有の形式のいずれかを使用します。
* [メールへのファイルの添付](https://experienceleague.adobe.com/docs/campaign/campaign-v8/send/emails/attaching-files.html?lang=ja){target="_blank"}：メールに 1 つ以上のファイルを添付する様々な方法について説明します。


>[!TAB メールパラメーター]

Campaign v8 ドキュメントでのメールパラメーターについて詳しくは、次のページを参照してください。

* [ミラーページへのリンク](https://experienceleague.adobe.com/docs/campaign/campaign-v8/send/emails/mirror-page.html?lang=ja){target="_blank"}：ミラーページを設定して、クライアントが常に最高のレンダリングエクスペリエンスを得られるようにします。
* [BCC アドレスの追加](https://experienceleague.adobe.com/docs/campaign/campaign-v8/send/emails/email-bcc.html?lang=ja){target="_blank"}：プラットフォームから送信されたメールのコピーを保持するように Adobe Campaign を設定します。
* [追加のメールパラメーターの定義](https://experienceleague.adobe.com/docs/campaign/campaign-v8/send/emails/email-parameters.html?lang=ja){target="_blank"}：配信プロパティで使用できるオプションとパラメーターについて説明します。

また、Enhanced MTA について詳しくは、この[ページ](sending-with-enhanced-mta.md)を参照してください。

>[!ENDTABS]





<!--
Adobe Campaign lets you mass deliver personalized electronic messages to a target population.

Before starting sending emails:

* Make sure recipient profiles contain at least an email address.
* Learn more about the Adobe Campaign [Delivery best practices](delivery-best-practices.md).
* Read out these sections to learn more about Deliverability: [Deliverability management in Campaign](about-deliverability.md) and [Deliverability best practices guide](https://experienceleague.adobe.com/docs/deliverability-learn/deliverability-best-practice-guide/introduction.html).

The key steps to send an email are as follows:

* [Create an email delivery](creating-an-email-delivery.md)
* [Define the target population](steps-defining-the-target-population.md)
* [Define the email content](defining-the-email-content.md)
* [Send the email](sending-messages.md)
* [Monitor the delivery](about-delivery-monitoring.md)

The sections below provide information that is specific to the email channel. For global information on how to create a delivery, refer to [this section](steps-about-delivery-creation-steps.md).
-->