---
solution: Campaign Classic
product: campaign
title: 'Adobe Campaign でのモバイルアプリケーションの設定 '
description: モバイルアプリケーション設定の開始方法を説明します。
audience: delivery
content-type: reference
topic-tags: sending-push-notifications
translation-type: ht
source-git-commit: 1d7d48f52f69e4902eafa6806c2cd9170c21fe5a
workflow-type: ht
source-wordcount: '294'
ht-degree: 100%

---


# アプリ設定の基本を学ぶ

この節は、オンラインホリデーパッケージを販売する会社を想定した設定例です。そのモバイルアプリケーション（Neotrips）は、Android 用 Neotrips と iOS 用 Neotrips の 2 つのバージョンで顧客に提供されています。

Adobe Campaign でプッシュ通知を送信するには、次の操作が必要です。

* Neotrips モバイルアプリケーション用に、**[!UICONTROL モバイルアプリケーション]**&#x200B;タイプの情報サービスを作成します。iOS については、[この節](../../delivery/using/configuring-the-mobile-application.md#configuring-ios-service)を参照してください。Android については、[この節](../../delivery/using/configuring-the-mobile-application-android.md#configuring-android-service)を参照してください。
* このサービスに、iOS バージョンと Android バージョンのアプリケーションを追加します。
* iOS と Android の両方用に配信を作成します。[このページ](../../delivery/using/creating-notifications.md)を参照してください。

![](assets/nmac_service_diagram.png)

>[!NOTE]
>
>サービスの「**[!UICONTROL 購読]**」タブに移動して、サービスの購読者（モバイルデバイスにアプリケーションをインストールして、通知の受信に同意したすべてのユーザー）のリストを表示します。

## パッケージのインストール {#installing-package-ios}

![](assets/do-not-localize/how-to-video.png) [モバイルアプリパッケージのインストール方法をビデオで説明します](https://experienceleague.adobe.com/docs/campaign-classic-learn/tutorials/sending-messages/push-channel/installing-the-mobile-app-channel.html?lang=ja#sending-messages)

ハイブリッド／ホスト型の顧客は、アドビのカスタマーサポートチームに連絡して、Campaign のプッシュ通知チャネルにアクセスします。

オンプレミス型の顧客は、次のインストール手順を実行する必要があります。

1. Adobe Campaign クライアントコンソールの&#x200B;**[!UICONTROL ツール／高度なツール／パッケージをインポート...]**&#x200B;からパッケージ読み込みウィザードにアクセスします。

   ![](assets/package_ios.png)

1. 「**[!UICONTROL 標準パッケージをインストール]**」を選択します。

1. 表示されるリストで、「**[!UICONTROL モバイルアプリチャネル]**」をチェックします。

   ![](assets/package_ios_2.png)

1. 「**[!UICONTROL 次へ]**」、「**[!UICONTROL 開始]**」の順にクリックして、パッケージのインストールを開始します。

   パッケージがインストールされると、進行状況バーに **100%** と表示され、インストールログに、「**[!UICONTROL パッケージが正常にインストールされました]**」と表示されます。

   ![](assets/package_ios_3.png)

1. インストールウィンドウを&#x200B;**[!UICONTROL 閉じます]**。

この手順が完了したら、Android および iOS アプリを設定できます。これらの節を参照してください。

* [iOS の設定手順](../../delivery/using/configuring-the-mobile-application.md)

* [Android の設定手順](../../delivery/using/configuring-the-mobile-application-android.md)
