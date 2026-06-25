---
product: campaign
title: Adobe Campaign でのモバイルアプリケーションの設定
description: モバイルアプリケーション設定の開始方法を説明します。
feature: Push
role: User, Developer
level: Intermediate, Experienced
hide: true
exl-id: 95bc07cc-8837-4511-81bc-05fad28191c9
TQID: https://experienceleague.adobe.com/cJ0deoAKq2ac-04v87YFRvwx-mqhrHyzQYxGmkvgKiY
product_v2:
  - id: dfc56824-e8b9-499e-85d4-21aedb507314
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
level_v2:
  - id: b5a62a22-46f7-4f0d-b151-3fc640bef588
feature_v2:
  - id: b631758a-142d-425f-b9aa-f756d85cb979
  - id: c858a28b-ea19-49b0-8d48-828717fad89c
subfeature_v2:
  - id: e95a583b-fcfa-4524-8666-46a29c828119
  - id: c8da4fdd-eb94-4751-a43c-f82733fb2d6e
  - id: d5bbe3da-ba85-4242-817e-54f7c4b943e0
  - id: f4da0e76-df77-451e-ad61-21afb7bd8810
source-git-commit: 38eab6b8da73163e4476e91c0ef73f25c3f57546
workflow-type: ht
source-wordcount: 351
ht-degree: 100%

---

# アプリ設定の基本を学ぶ



この節は、オンラインホリデーパッケージを販売する会社を想定した設定例です。 同社のモバイルアプリケーション（Neotrips）は、Android 用 Neotrips と iOS 用 Neotrips の 2 つのバージョンで顧客に提供されています。

Adobe Campaign でプッシュ通知を送信するには、次の操作が必要です。

* Neotrips モバイルアプリケーション用に、**[!UICONTROL モバイルアプリケーション]**&#x200B;タイプの情報サービスを作成します。 iOS については、[この節](configuring-the-mobile-application.md#configuring-ios-service)を参照してください。 Android については、[この節](configuring-the-mobile-application-android.md#configuring-android-service)を参照してください。
* このサービスに、iOS バージョンと Android バージョンのアプリケーションを追加します。
* [iOS](create-notifications-ios.md) と [Android](create-notifications-android.md) 用の配信を作成します。

![](assets/nmac_service_diagram.png)

>[!NOTE]
>
>サービスの「**[!UICONTROL 購読]**」タブに移動して、サービスの購読者（モバイルデバイスにアプリケーションをインストールして、通知の受信に同意したすべてのユーザー）のリストを表示します。

## パッケージのインストール {#installing-package-ios}

[!BADGE オンプレミスおよびハイブリッド]{type=Caution url="https://experienceleague.adobe.com/docs/campaign-classic/using/installing-campaign-classic/architecture-and-hosting-models/hosting-models-lp/hosting-models.html?lang=ja" tooltip="オンプレミスデプロイメントとハイブリッドデプロイメントにのみ適用されます"}

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

この手順が完了したら、Android および iOS アプリを設定できます。
次の節を参照してください。

* [iOS の設定手順](configuring-the-mobile-application.md)

* [Android の設定手順](configuring-the-mobile-application-android.md)
