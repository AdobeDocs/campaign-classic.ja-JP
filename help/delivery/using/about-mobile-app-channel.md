---
product: campaign
title: モバイルアプリチャネルの基本を学ぶ
description: Adobe Campaign でのモバイルアプリチャネルの基本を学ぶ
feature: Push
role: User
exl-id: c3b0406f-f652-42f4-ad0d-23fb719cd1b6
source-git-commit: a1e9fec0e9c85bf25b79e24a7432dfb45bd1a0cb
workflow-type: tm+mt
source-wordcount: '585'
ht-degree: 44%

---

# モバイルアプリチャネルの基本を学ぶ{#about-mobile-app-channel}

Adobe Campaignを使用すると、パーソナライズされたメッセージをモバイルアプリのユーザーに送信するプッシュ通知配信を作成できます。

プッシュ通知を使用すると、iOSとAndroidでリアルタイムにユーザーを引き付けることができます。 更新、お知らせ、プロモーションなどを送信する場合でも、コンテンツ、タイミング、ターゲティングを制御できます。 プッシュチャネルの設定と使用、サブスクリプションの管理、APN と FCM との統合、メッセージのパーソナライズの方法については、[Adobe Campaign v8 ドキュメント &#x200B;](https://experienceleague.adobe.com/ja/docs/campaign/campaign-v8/send/emails/email){target=_blank} を参照してください。

Campaign v8 のプロモーションイニシアチブの一環として、Campaign Classic のドキュメントを再編成しました。共通機能は、Campaign v8 ドキュメントセットでのみ使用できるようになりました。

>[!BEGINTABS]

>[!TAB  プッシュチャネルドキュメント ]

プッシュ通知チャネルの詳細については、[Campaign v8 ドキュメント &#x200B;](https://experienceleague.adobe.com/docs/campaign/campaign-v8/send/push/push.html?lang=ja){target=_blank} を参照してください。

[![画像](../../assets/do-not-localize/learn-more-button.svg)](https://experienceleague.adobe.com/docs/campaign/campaign-v8/send/push/push.html?lang=ja){target=_blank}


>[!TAB  プッシュ配信の作成 ]

プッシュ配信の作成に関連する主な手順については、Campaign v8 ドキュメントを参照してください。

* [&#x200B; プッシュ通知の作成 &#x200B;](https://experienceleague.adobe.com/docs/campaign/campaign-v8/send/push/push.html?lang=ja#push-create){target="_blank"}：プッシュ配信の作成に必要な様々な手順について説明します。
* [&#x200B; プッシュ通知の送信と監視 &#x200B;](https://experienceleague.adobe.com/docs/campaign/campaign-v8/send/push/push.html?lang=ja#push-test){target="_blank"}：配信を検証、送信、トラッキングする方法について説明します。
* [Androidのリッチなプッシュ配信のデザイン &#x200B;](https://experienceleague.adobe.com/docs/campaign/campaign-v8/send/push/rich-push/rich-push-android.html?lang=ja){target="_blank"}:Android デバイス向けのリッチなプッシュ通知を作成および設定する方法を説明します。
* [iOSのリッチなプッシュ配信のデザイン &#x200B;](https://experienceleague.adobe.com/docs/campaign/campaign-v8/send/push/rich-push/rich-push-ios.html?lang=ja){target="_blank"}:Adobe Campaign v8 でiOS デバイス用のリッチなプッシュ通知をデザインし、設定する方法を説明します。


>[!TAB  プッシュパラメーター ]

プッシュパラメーターについて詳しくは、Campaign v8 ドキュメントを参照してください。

* [&#x200B; 設定の前提条件 &#x200B;](https://experienceleague.adobe.com/docs/campaign/campaign-v8/send/push/push-settings.html?lang=ja#before-starting){target="_blank"}：権限を設定し、アプリを設定する方法について説明します。
* [launch プロパティの設定 &#x200B;](https://experienceleague.adobe.com/docs/campaign/campaign-v8/send/push/push-settings.html?lang=ja#launch-property){target="_blank"}:Adobe Experience Platform データ収集でモバイルタグプロパティを設定して、プッシュ通知を有効にする方法を説明します。
* [&#x200B; プッシュサービスのモバイルサービスを設定 &#x200B;](https://experienceleague.adobe.com/docs/campaign/campaign-v8/send/push/push-settings.html?lang=ja#push-service){target="_blank"}: AdobeでiOSおよびAndroidのプッシュサービスを設定して、モバイルアプリユーザーに対してターゲット設定のプッシュ通知を有効にします。
* [&#x200B; モバイルプロパティで拡張機能を設定 &#x200B;](https://experienceleague.adobe.com/docs/campaign/campaign-v8/send/push/push-settings.html?lang=ja#configure-extension){target="_blank"}：モバイルプロパティに Campaign 拡張機能を統合して、プッシュ通知を有効にし、ユーザーのインタラクションを効果的に管理します。

>[!ENDTABS]


次の情報は、Campaign Classicに固有の情報です。

+++ **パッケージのインストール**

![](assets/do-not-localize/how-to-video.png) [モバイルアプリパッケージのインストール方法をビデオで確認](https://experienceleague.adobe.com/docs/campaign-classic-learn/tutorials/sending-messages/push-channel/installing-the-mobile-app-channel.html?lang=ja#sending-messages)

ハイブリッド／ホスト型のお客様は、[アドビカスタマーケア](https://helpx.adobe.com/jp/enterprise/admin-guide.html/enterprise/using/support-for-experience-cloud.ug.html)チームに連絡して、Campaign のプッシュ通知チャネルにアクセスします。

オンプレミスのお客様は、ビルトインのパッケージをインストールする必要があります。

>[!CAUTION]
>
>Campaign のビルトインパッケージ、ベストプラクティス、レコメンデーションについて詳しくは、[このページ](../../installation/using/installing-campaign-standard-packages.md)を参照してください。


インストール手順は次のとおりです。

1. Adobe Campaign クライアントコンソールの&#x200B;**[!UICONTROL ツール／高度なツール／パッケージをインポート]**&#x200B;から、パッケージインポートアシスタントにアクセスします。

   ![](assets/package_ios.png)

1. 「**[!UICONTROL 標準パッケージをインストール]**」を選択します。

1. 表示されるリストで、「**[!UICONTROL モバイルアプリチャネル]**」をチェックします。

   ![](assets/package_ios_2.png)

1. 「**[!UICONTROL 次へ]**」、「**[!UICONTROL 開始]**」の順にクリックして、パッケージのインストールを開始します。

   パッケージがインストールされると、進行状況バーに **100%** と表示され、インストールログに、「**[!UICONTROL パッケージが正常にインストールされました]**」と表示されます。

   ![](assets/package_ios_3.png)

1. インストールウィンドウを&#x200B;**[!UICONTROL 閉じます]**。

この手順が完了したら、Android アプリとiOS アプリを設定できます。 Campaign v8 [&#x200B; ドキュメント &#x200B;](https://experienceleague.adobe.com/docs/campaign/campaign-v8/send/push/push.html?lang=ja){target="_blank"} を参照してください。

+++

+++ **トラブルシューティング**

モバイルデバイスが Wi-Fi に接続されているにも関わらず通知を受信できない場合は、FCM または APNs のポートがファイアウォールによってブロックされていないか確認してみてください。

**Android**：モバイルデバイスは、ポート 5228 ～ 5230 で FCM サーバーに接続します。したがって、FCM への接続を許可するようにファイアウォールを設定する必要があります。開くポートは、5228（最も使用頻度が高い）、5229 および 5230 です。

**iOS**：

HTTP/2 コネクタ：次のサーバーとの間での通信を許可する必要があります。

* api.push.apple.com：ポート 443
* api.development.push.apple.com：ポート 443

>[!NOTE]
>
>2 つのコネクタについて詳しくは、Campaign v8 [&#x200B; ドキュメント &#x200B;](https://experienceleague.adobe.com/docs/campaign/campaign-v8/send/push/push-settings.html?lang=ja){target="_blank"} を参照してください。

+++
