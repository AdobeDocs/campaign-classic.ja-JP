---
product: campaign
title: 通信チャネル
description: 様々なチャネルでパーソナライズされたメッセージを送信するための配信を作成します。
feature: Cross Channel Orchestration, Email, SMS, In App, Direct Mail, Push
role: User
exl-id: 92b5e013-b619-4f0b-b0b1-1fc2e653ceac
source-git-commit: ad6f3f2cf242d28de9e6da5cec100e096c5cbec2
workflow-type: tm+mt
source-wordcount: '998'
ht-degree: 91%

---

# 通信チャネル{#communication-channels}

Adobe Campaign を使用すると、メール、SMS、プッシュ通知、ダイレクトメールなどのクロスチャネルキャンペーンを送信し、各種の専用レポートを使用してキャンペーンの有効性を評価できます。これらのメッセージは、デザインし、配信を介して送信します。また、受信者ごとにパーソナライズできます。

コア機能には、ターゲティング、メッセージの定義とパーソナライゼーション、通信の実行、関連する運用可能なレポートなどがあります。

Campaign v7 から v8 への移行の一環として、Campaign Classic ドキュメントセットを合理化し、再編成しました。 共通機能は、Campaign v8 ドキュメントセットでのみ使用できるようになりました。

>[!BEGINTABS]

>[!TAB 通信チャネルドキュメント]

通信チャネルについて詳しくは、[Campaign v8 ドキュメント](https://experienceleague.adobe.com/docs/campaign/campaign-v8/send/gs-message.html?lang=ja){target=_blank}を参照してください。


[![画像](../../assets/do-not-localize/learn-more-button.svg)](https://experienceleague.adobe.com/docs/campaign/campaign-v8/send/gs-message.html?lang=ja){target=_blank}


>[!TAB 配信コンテンツとオーディエンス]

配信の作成、コンテンツ、オーディエンスに関連する主な手順については **Campaign v8 ドキュメント** を参照してください。

* [配信の作成](https://experienceleague.adobe.com/docs/campaign/campaign-v8/send/create-message.html?lang=ja#create-the-delivery){target="_blank"}：1 回限りの単一の配信を作成する方法について説明します。
* [コンテンツの定義](https://experienceleague.adobe.com/docs/campaign/campaign-v8/send/create-message.html?lang=ja#content-of-the-delivery){target="_blank"}：各チャネルに固有の配信コンテンツを設定します。
* [オーディエンスの指定](https://experienceleague.adobe.com/docs/campaign/campaign-v8/send/create-message.html?lang=ja#target-population){target="_blank"}：複数のタイプのターゲット（メインオーディエンス、配達確認ターゲット、シードアドレス、コントロール母集団）を定義します。
* [&#x200B; 配信テンプレートの操作 &#x200B;](https://experienceleague.adobe.com/docs/campaign/campaign-v8/send/create-templates.html?lang=ja){target="_blank"}：配信の作成を容易にするためにテンプレートを定義する方法について説明します。





>[!TAB 配信の検証と送信]

配信の検証、送信およびベストプラクティスについては、次のページ **Campaign v8 ドキュメント** を参照してください。

* [配信の検証](https://experienceleague.adobe.com/docs/campaign/campaign-v8/send/create-message.html?lang=ja#validate-the-delivery){target="_blank"}：配信をメインターゲットに送信する前に検証する方法について説明します。
* [配信の送信](https://experienceleague.adobe.com/docs/campaign/campaign-v8/send/create-message.html?lang=ja#configuring-and-sending-the-delivery){target="_blank"}：配信設定を指定し、メッセージの送信方法を定義します。
* [配信のベストプラクティス](https://experienceleague.adobe.com/docs/campaign/campaign-v8/send/delivery-best-practices.html?lang=ja){target="_blank"}：Campaign の配信機能に関連するベストプラクティスを参照してください。

>[!ENDTABS]

次の設定は、Campaign Classic に固有です。その他の配信設定について詳しくは、[Campaign v8 ドキュメント](https://experienceleague.adobe.com/docs/campaign/campaign-v8/send/gs-message.html?lang=ja){target="_blank"}を参照してください。

+++ **配信分析**

**配信分析パフォーマンスの向上**

配信準備にかかる時間を短縮するには、分析を開始する前に「**[!UICONTROL データベース内で配信部分を準備]**」オプションにチェックを入れます。

このオプションを有効にすると、配信準備がデータベース内で直接おこなわれ、分析時間が大幅に短縮されます。

現在、このオプションは、次の条件を満たす場合にのみ使用できます。

* 配信はメールである必要があります。現時点では、その他のチャネルはサポートされていません。
* ミッドソーシングや外部ルーティングは使用できません。一括配信ルーティングタイプのみ使用できます。**[!UICONTROL 配信プロパティ]**&#x200B;の「**[!UICONTROL 一般]**」タブで、使用するルーティングを確認できます。
* 外部ファイルからの母集団をターゲットに指定することはできません。単一の配信の場合、**[!UICONTROL メールパラメーター]**&#x200B;から&#x200B;**[!UICONTROL 宛先]**&#x200B;リンクをクリックし、「**[!UICONTROL データベースで定義]**」オプションが選択されていることを確認します。ワークフローで使用される配信の場合、「**[!UICONTROL 配信]**」タブにおいて受信者が&#x200B;**[!UICONTROL インバウンドイベントで指定]**&#x200B;されていることを確認します。
* PostgreSQL データベースを使用する必要があります。

**分析優先度の設定**

配信をキャンペーンの一環として使用する場合は、「**[!UICONTROL 詳細設定]**」タブに特別なオプションが 1 つ追加されます。このオプションを使用すると、同じキャンペーンに含まれる配信の処理順を調整できます。

各配信は、送信前に分析されます。分析の所要時間は配信の抽出ファイルによって異なります。ファイルサイズが大きいほど、分析にかかる時間は長くなり、後に続く配信が遅くなります。

「**[!UICONTROL スケジューラーによるメッセージの準備]**」のオプションで、キャンペーンワークフローの配信分析を優先順位付けできます。

![](assets/delivery_analysis_priority.png)

配信が非常に大きい場合、低い優先順位を設定することが、同じワークフローに含まれる他の配信の遅延を防ぐために有効と考えられます。

>[!NOTE]
>
>「**[!UICONTROL 低アクティビティ時の実行をスケジュール]**」オプションを選択すると、大きな配信分析によってワークフロー全体の進行が遅くなるのを防ぐことができます。

+++

+++ **配信の送信**

**再試行の設定**

**ソフト**&#x200B;または&#x200B;**無視**&#x200B;のエラーによって一時的に配信できなかったメッセージは、自動再試行の対象となります。配信エラーのタイプと理由については、[この節](understanding-delivery-failures.md#delivery-failure-types-and-reasons)を参照してください。

>[!IMPORTANT]
>
>ホストインストールまたはハイブリッドインストールで、[Enhanced MTA](sending-with-enhanced-mta.md) にアップグレードした場合、Campaign では配信の再試行設定が使用されなくなります。ソフトバウンスの再試行とその間隔は、メッセージの電子メールドメインから返されるバウンス応答のタイプと重大度に基づいて、Enhanced MTA が決定します。

従来の Campaign MTA を使用したオンプレミスインストールおよびホスト／ハイブリッドインストールの場合、配信パラメーターの「**[!UICONTROL 配信]**」タブの中央セクションは、配信の翌日に実行する再試行の数と再試行間の最小遅延を示します。

![](assets/s_ncs_user_wizard_retry_param.png)

デフォルトでは、配信後の最初の日に最低 1 時間の間隔をおいて、24 時間に 5 回の再試行がスケジュールされます。その後は、「**[!UICONTROL 有効性]**」タブで指定される配信期限が来るまで、1 日 1 回の再試行がスケジュールされます。以下の節を参照してください。

**有効期間の定義**

メッセージの送信（および再試行）が可能な期間は、配信が開始されたときから配信期限までです。配信期限は、配信プロパティの「**[!UICONTROL 有効性]**」タブに表示されます。

![](assets/s_ncs_user_email_del_valid_period.png)

* 「**[!UICONTROL 配信期間]**」フィールドには、グローバルでおこなう配信再試行の期限を入力できます。Adobe Campaign は、開始日にメッセージの送信を開始した後、エラーのみを返すメッセージについて、設定された定期的な再試行を、有効期限日に達するまで実行します。

  日付を指定することもできます。そのためには、「**[!UICONTROL 有効期限を明示的に設定]**」を選択します。この場合、配信および有効期限日に時刻を指定することもできます。デフォルト値は現在時刻ですが、入力フィールドを使用して直接変更できます。

  >[!IMPORTANT]
  >
  >ホストインストールまたはハイブリッドインストールで、[Enhanced MTA](sending-with-enhanced-mta.md) にアップグレードした場合、Campaign のメール配信の&#x200B;**[!UICONTROL 配信期間]**&#x200B;設定は、**3.5 日以下**&#x200B;に設定された場合にのみ使用されます。3.5 日を超える値を定義した場合、その値は考慮されません。

* **リソースの有効期限**：「**[!UICONTROL 有効期限]**」フィールドは、アップロードされたリソース（主にミラーページと画像）に関して使用されます。ディスクスペースを節約するために、このページ上のリソースが有効な期間は限られています。

  このフィールドの値は、[この節](../../platform/using/adobe-campaign-workspace.md#default-units)にリストされている単位で表示できます。

+++

<!--

   Learn how to create a one-shot single delivery. You can create other types of deliveries to build your use cases. 

For more information about the different types of deliveries and how to create them, refer to the [Campaign v8 documentation](https://experienceleague.adobe.com/docs/campaign/campaign-v8/send/create-message.html){target="_blank"}. 

>[!NOTE]
>
>Adobe Campaign offers a set of tools to monitor your deliverability and optimize email sending. Learn more in [this section](about-deliverability.md).

Delivery sending can be automated by preparing a delivery and/or sending it in the process of a workflow. For more on delivery-type activities in workflows, refer to [this section](../../workflow/using/about-action-activities.md).

Adobe Campaign offers the following delivery channels:

1. **Email channel**: email deliveries let you send personalized emails to the target population. Refer to [About email channel](about-email-channel.md).
1. **Direct mail channel**: direct mail deliveries let you generate an extraction file which contains data on the target population. Refer to [About direct mail channel](about-direct-mail-channel.md).
1. **Mobile channel**: deliveries on mobile channels let you send personalized SMS or LINE messages to the target population. Refer to [SMS channel](sms-channel.md).
1. **Mobile application channel**: mobile app deliveries let you send notifications to iOS and Android systems. Refer to the [Mobile app channel](about-mobile-app-channel.md) chapter.

   Other channels are described on [this section](#other-channels).

   >[!NOTE]
   >
   >The number of available channels depends on your contract. Please check your license agreement.

Deliveries can be carried out **online** (via email, one of the mobile channels and push notifications), and **offline** (direct mail channel).

Depending on the channel, delivery modes can be:

* Direct mass delivery via Adobe Campaign (default mode for email channel).
* External delivery via a specialist operator who is given the output file generated by the delivery assistant (default mode for direct mail channel).

External accounts are configured via the **[!UICONTROL Administration > Platform > External accounts]** node. This configuration should be performed by expert users only.

## Email deliveries {#email-deliveries}

The [Email channel](about-email-channel.md) is one of the core channels in Adobe Campaign, allowing you to schedule and send personalized emails to specific targets.

You can send different types of emails:

* Single-send emails: emails that you can send once to a defined target. They are usually used to promote a specific content that would be prepared and sent only once (newsletter, promotional email, etc.).
* Recurring emails: in a campaign, send the same email regularly and aggregate each send and its reports on a periodic basis. The same email is sent, but usually to a different target, based on the eligible target for the day of the send. A common example is a birthday email. For more on this, refer to [Recurring deliveries](../../workflow/using/recurring-delivery.md).
* Transactional emails: unitary emails that are triggered based on your customers' behavior. Refer to [Transactional messaging](../../message-center/using/about-transactional-messaging.md).

To learn about delivery usage and recommendations, consult Campaign [Delivery best practices](delivery-best-practices.md).

For more on the different types of deliveries, refer to [this section](#types-of-deliveries).

## Mobile deliveries {#mobile-deliveries}

Adobe Campaign allows you to deliver [SMS](sms-channel.md) and [LINE](line-channel.md) messages on mobiles.

For SMS messages, you can create, modify, and personalize messages in text format only. You can also preview your SMS messages before they are sent.

For LINE messages, you can send text or images and links.

To deliver SMS or LINE messages to a mobile phone you need:

* An external account configured on the **[!UICONTROL Mobile (SMS)]** channel or on the **[!UICONTROL LINE]** channel. 
* An SMS or LINE delivery template that is correctly linked to this external account.

## Push notifications {#push-notifications}

Adobe Campaign allows you to send personalized and segmented [push notifications](about-mobile-app-channel.md) on iOS and Android mobile devices, through dedicated apps. Once configuration and integration steps have been performed, iOS and Android deliveries can be created and sent. You can also design rich notifications with images or videos.

## Direct mail {#direct-mail}

[Direct mail](about-direct-mail-channel.md) is an offline channel that allows you to personalize and generate the file required by direct mail providers. It gives you the possibility to mix online and offline channels in your customer journeys.

Online channels allow you to create your messages (email, SMS, mobile app delivery, etc.) and send them to your audience directly from Adobe Campaign. With offline channels, it is different. When you prepare a direct mail delivery, Adobe Campaign generates a file including all the targeted profiles and the chosen contact information (postal address for example). You will then be able to send this file to your direct mail provider who will take care of the actual sending.

## Other channels {#other-channels}

Adobe Campaign offers Telephone delivery template, which is used to create external deliveries. Using this channel implies you set up dedicated methodologies to process output files. Configuration steps are the same as for [Direct mail channel](about-direct-mail-channel.md).

>[!NOTE]
>
>The Telephone channel is not available out-of-the-box. Its implementation requires Adobe Consulting or an Adobe Partner to be engaged. Please reach out to your Adobe representative for more information.

In addition, 'Other' type deliveries use a specific technical template which does not execute a process: this lets them manage marketing actions executed outside of the Adobe Campaign platform.

This channel has no specific mechanism. It is a generic channel that has its own external account routing option, delivery template type and campaign workflow activity, just like any other communication channel available in Adobe Campaign.

This channel is designed for descriptive purposes only, for example to define deliveries for which you want to keep a trace of the target of a campaign performed in a tool other than Adobe Campaign.

## Types of deliveries{#types-of-deliveries}

There are three types of delivery objects in Campaign:

### Single delivery {#single-delivery}

A **delivery** is a standalone delivery object that is executed once. It can be duplicated, prepared again, but as long as it is in its final state (canceled, stopped, finished), it cannot be reused.

Deliveries can be created either from the list of deliveries, or within a workflow via a [Delivery](../../workflow/using/delivery.md) activity.

Workflows also provide specific delivery activities according to the type of channel you want to use. For more on these activities, refer to [this section](../../workflow/using/cross-channel-deliveries.md).

### Recurring delivery {#recurring-delivery}

A **recurring delivery** lets you create a new delivery each time the activity is executed. This avoids you having to create a new delivery for recurring tasks.

As an example, if you run this type of activity once a month, you will end up with 12 deliveries after a year.

Recurring deliveries are created within workflows via the [Recurring delivery activity](../../workflow/using/recurring-delivery.md). An example of this activity being used is presented in this section: [Creating a recurring delivery in a targeting workflow](../../workflow/using/sending-a-birthday-email.md#creating-a-recurring-delivery-in-a-targeting-workflow).

### Continuous delivery {#continuous-delivery}

A **continuous delivery** lets you add new recipients to an existing delivery, which avoids having to create a new delivery each time it is executed.

If an information in the delivery changes (content, name, etc.), a new delivery object is created at the delivery execution. If no information was changed, the same delivery object is reused and the delivery and tracking logs are added in the same object.

As an example, if you run this type of activity once a month, you will end up with a single delivery after a year (provided you did not make any change to the delivery).

Continuous deliveries are created within workflows via the [Continuous delivery activity](../../workflow/using/continuous-delivery.md).-->
