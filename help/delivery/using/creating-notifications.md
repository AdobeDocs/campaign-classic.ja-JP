---
title: 通知の作成
seo-title: 通知の作成
description: 通知の作成
seo-description: null
page-status-flag: never-activated
uuid: fb1862df-e616-4147-a642-dc867bc983b5
contentOwner: sauviat
products: SG_CAMPAIGN/CLASSIC
audience: delivery
content-type: reference
topic-tags: sending-push-notifications
discoiquuid: 345af5c2-c852-4086-8ed0-ff3e7e402e04
index: y
internal: n
snippet: y
translation-type: ht
source-git-commit: b78db689958c9b240da9a0315060fe63bcb48e0a

---


# 通知の作成{#creating-notifications}

ここでは、iOS および Android の通知の配信に固有な設定について説明します。配信の作成に関するグローバルな概念については、[この節](../../delivery/using/steps-about-delivery-creation-steps.md)で説明しています。

新しい配信を作成して開始します。

![](assets/nmac_delivery_1.png)

## iOS で通知を送信する {#sending-notifications-on-ios}

1. 「**[!UICONTROL iOS 配信]**」配信テンプレートを選択します。

   ![](assets/nmac_delivery_ios_1.png)

1. 通知のターゲットを定義するには、**[!UICONTROL 宛先]**&#x200B;リンク／**[!UICONTROL 追加]**&#x200B;をクリックします。

   ![](assets/nmac_delivery_ios_2.png)

   >[!NOTE]
   >
   >配信のターゲット母集団を選択する際の詳細なプロセスについては、[この節](../../delivery/using/steps-defining-the-target-population.md)を参照してください。
   >
   >パーソナライゼーションフィールドの使用について詳しくは、[パーソナライゼーションについて](../../delivery/using/about-personalization.md)を参照してください。
   >
   >シードリストの追加について詳しくは、[シードアドレスについて](../../delivery/using/about-seed-addresses.md)を参照してください。

1. 「**[!UICONTROL iOS モバイルアプリケーション (iPhone、iPad) の購読者]**」を選択してモバイルアプリケーション（この場合は Neotrips）に関連するサービスを選択し、アプリケーションの iOS バージョンを選択します。

   ![](assets/nmac_delivery_ios_3.png)

1. **[!UICONTROL アラート]**、**[!UICONTROL バッジ]**、**[!UICONTROL アラートおよびバッジ]**&#x200B;または&#x200B;**[!UICONTROL サイレントプッシュ]**&#x200B;から通知の種類を選択します。

   ![](assets/nmac_delivery_ios_4.png)

   >[!NOTE]
   >
   >「**サイレントプッシュ**」モードは、iOS 7 以降で利用できます。このモードでは、モバイルアプリケーションに「無音の」通知を送信します。ユーザーは、通知が到着したことを知らされません。通知は、アプリケーションに直接転送されます。

1. 「**[!UICONTROL タイトル]**」フィールドで、通知に表示するタイトルのラベルを入力します。このタイトルは、通知センターから使用可能な通知のリストにのみ表示されます。このフィールドを使用して、iOS 通知ペイロードの **title** パラメーターの値を定義できます。
1. HTTP/2 コネクタを使用する場合、サブタイトル（iOS 通知ペイロードの **subtitle** パラメーター）を追加できます。[Adobe Campaign でモバイルアプリケーションを設定する](../../delivery/using/configuring-the-mobile-application.md)の節を参照してください。
1. 選択した通知のタイプに基づいて「**[!UICONTROL メッセージ]**」と「**[!UICONTROL バッジの値]**」を入力します。

   ![](assets/nmac_delivery_ios_5.png)

   >[!NOTE]
   >
   >通知のコンテンツに絵文字を追加することができます。そのためには、絵文字のリストがある Web サイト（[例](https://www.utf8-chartable.de/unicode-utf8-table.pl?start=9728)）で絵文字をコピーし、コンテンツエディターに直接貼り付けます。Windows 7 では、一部の絵文字がエディターで正しく表示されない（四角形で表示される）ことがありますが、最終的な通知では正しく送信されます。絵文字を表示できるかどうかは、デバイスの OS によって異なります。配信を送信する前に、配信が正しく表示されることを示す証拠を送信することをお勧めします。

   >[!NOTE]
   >
   >「**[!UICONTROL バッジ]**」と「**[!UICONTROL アラートおよびバッジ]**」タイプの通知では、バッジの値（モバイルアプリケーションのロゴの上にある数字）を変更できます。バッジを更新するには、値として 0 を入力します。フィールドが空の場合、バッジの値は変更されません。

1. 「**[!UICONTROL アクションボタン]**」を使用すると、アラート通知に表示されるアクションボタンのラベルを定義できます（ペイロードの **action_loc_key** フィールド）。iOS アプリケーションでローカライズ可能文字列を管理する場合は（**Localizable.strings**）、対応するキーをこのフィールドに入力します。アプリケーションでローカライズ可能テキストを管理しない場合は、アクションボタンに表示するラベルを入力します。ローカライズ可能文字列について詳しくは、[Apple のドキュメント](https://developer.apple.com/library/archive/documentation/NetworkingInternet/Conceptual/RemoteNotificationsPG/CreatingtheNotificationPayload.html#//apple_ref/doc/uid/TP40008194-CH10-SW1)を参照してください。
1. 「**[!UICONTROL サウンドを再生]**」フィールドで、通知を受信したときにモバイル端末で再生されるサウンドを選択します。

   >[!NOTE]
   >
   >サウンドは、アプリケーションに含まれている必要があり、サービスが作成されたときに定義される必要があります。[iOS 外部アカウントの設定](../../delivery/using/configuring-the-mobile-application.md#configuring-external-account-ios)を参照してください。

1. 「**[!UICONTROL アプリケーション変数]**」フィールドで、それぞれの変数の値を入力します。アプリケーション変数によって、通知の動作を定義できます。例えば、ユーザーが通知を有効化したときに特定のアプリケーション画面が表示されるように設定できます。

   >[!NOTE]
   >
   >アプリケーション変数は、モバイルアプリケーションのコードで定義され、サービスの作成中に入力される必要があります。詳しくは、[Adobe Campaign でモバイルアプリケーションを設定する](../../delivery/using/configuring-the-mobile-application.md)を参照してください。

1. 通知を設定したら、「**[!UICONTROL プレビュー]**」タブをクリックして通知をプレビューします。

   ![](assets/nmac_intro_2.png)

   >[!NOTE]
   >
   >通知スタイル（バナーまたはアラート）は、Adobe Campaign では定義しません。スタイルは、iOS 設定でユーザーが選択した設定によって異なります。ただし、Adobe Campaign では、それぞれの通知スタイルをプレビューできます。右下の矢印をクリックすると、スタイルを切り替えることができます。
   >
   >プレビューでは iOS 10 と同様に表示されます。

配達確認や最終配信を送信するには、E メール配信と同じプロセスを使用します。

メッセージを送信した後は、配信を監視およびトラッキングできます。詳しくは、以下の節を参照してください。

* [プッシュ通知の強制隔離](../../delivery/using/understanding-quarantine-management.md#push-notification-quarantines)
* [配信の監視](../../delivery/using/monitoring-a-delivery.md)
* [配信エラーの理解](../../delivery/using/understanding-delivery-failures.md)

## Android で通知を送信する {#sending-notifications-on-android}

1. 「**[!UICONTROL Android に配信（android）]**」配信テンプレートを選択して開始します。

   ![](assets/nmac_delivery_android_1.png)

1. 通知のターゲットを定義するには、**[!UICONTROL 宛先]**&#x200B;リンク／**[!UICONTROL 追加]**&#x200B;をクリックします。

   ![](assets/nmac_delivery_android_2.png)

1. 「**[!UICONTROL Android モバイルアプリケーションの購読者]**」を選択してモバイルアプリケーション（この場合は Neotrips）に関連するサービスを選択し、アプリケーションの Android バージョンを選択します。

   ![](assets/nmac_delivery_android_3.png)

1. 次に通知の内容を入力します。

   ![](assets/nmac_delivery_android_4.png)

   >[!NOTE]
   >
   >通知のコンテンツに絵文字を追加することができます。そのためには、絵文字のリストがある Web サイト（[例](https://www.utf8-chartable.de/unicode-utf8-table.pl?start=9728)）で絵文字をコピーし、コンテンツエディターに直接貼り付けます。Windows 7 では、一部の絵文字がエディターで正しく表示されない（四角形で表示される）ことがありますが、最終的な E メールでは正しく送信されます。絵文字を表示できるかどうかは、デバイスの OS によって異なります。配信を送信する前に、配信が正しく表示されることを示す証拠を送信することをお勧めします。

1. 「**[!UICONTROL アプリケーション変数]**」フィールドで、それぞれの変数の値を入力します。アプリケーション変数によって、通知の動作を定義できます。例えば、ユーザーが通知を有効化したときに特定のアプリケーション画面が表示されるように設定できます。

   >[!NOTE]
   >
   >アプリケーション変数は、モバイルアプリケーションのコードで定義され、サービスの作成中に入力される必要があります。詳しくは、[Adobe Campaign でモバイルアプリケーションを設定する](../../delivery/using/configuring-the-mobile-application.md)を参照してください。

1. 通知を設定したら、「**[!UICONTROL プレビュー]**」タブをクリックして通知をプレビューします。

   ![](assets/nmac_intro_1.png)

配達確認や最終配信を送信するには、E メール配信と同じプロセスを使用します。

配信を検証および送信する際の詳細なプロセスについては、以下の節を参照してください。

* [配信の検証](../../delivery/using/steps-validating-the-delivery.md)
* [配信の送信](../../delivery/using/steps-sending-the-delivery.md)

メッセージを送信した後は、配信を監視およびトラッキングできます。詳しくは、以下の節を参照してください。

* [プッシュ通知の強制隔離](../../delivery/using/understanding-quarantine-management.md#push-notification-quarantines)
* [配信の監視](../../delivery/using/monitoring-a-delivery.md)
* [配信エラーの理解](../../delivery/using/understanding-delivery-failures.md)
