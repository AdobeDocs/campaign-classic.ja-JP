---
title: Adobe CampaignでのiOSモバイルアプリケーションの設定
description: iOS用のモバイルアプリケーションの設定方法を説明します。
page-status-flag: never-activated
uuid: aff1a4a0-34e7-4ce0-9eb3-30a8de1380f2
contentOwner: sauviat
products: SG_CAMPAIGN/CLASSIC
audience: delivery
content-type: reference
topic-tags: sending-push-notifications
discoiquuid: 7b5a1ad6-da5a-4cbd-be51-984c07c8d0b3
translation-type: tm+mt
source-git-commit: 16985c1ddcd380cfc1ca4960b35bb5e78628f464
workflow-type: tm+mt
source-wordcount: '944'
ht-degree: 67%

---


# iOSの設定手順 {#configuring-the-mobile-application-in-adobe-campaign-ios}

パッケージがインストールされたら、Adobe Campaign ClassicでiOSアプリの設定を定義できます。

>[!NOTE]
>
>Android用のアプリの設定方法とAndroid用の配信の作成方法については、この [節を参照してください](../../delivery/using/configuring-the-mobile-application-android.md)。

## Configuring iOS external account {#configuring-external-account-ios}

iOSの場合、iOS HTTP/2コネクタはHTTP/2 APNに通知を送信します。

このコネクタを設定するには、次の手順に従います。

1. **[!UICONTROL 管理／プラットフォーム／外部アカウント]**&#x200B;に移動します。
1. **[!UICONTROL iOS ルーティング]**&#x200B;外部アカウントを選択します。
1. In the **[!UICONTROL Connector]** tab, fill in the **[!UICONTROL Access URL of the connector]** field with the following URL: ```http://localhost:8080/nms/jsp/iosHTTP2.jsp```

   >[!NOTE]
   >
   > キャンペーン20.3リリース以降、iOSレガシバイナリコネクタは非推奨となりました。 このコネクタを使用する場合は、それに応じて実装を適応させる必要があります。 [詳細情報](https://helpx.adobe.com/campaign/kb/migrate-to-http2.html)

   ![](assets/nmac_connectors.png)

1. 「**[!UICONTROL 保存]**」をクリックします。

これで、iOS コネクタが設定されました。サービスの作成を開始できます。

## iOSサービスの設定 {#configuring-ios-service}

>[!CAUTION]
>
>Adobe Campaign SDK に統合する前に、アプリケーションにプッシュアクションを設定する必要があります。
>
>該当しない場合は、[このページ](https://developer.apple.com/library/archive/documentation/NetworkingInternet/Conceptual/RemoteNotificationsPG/)を参照してください。

1. **[!UICONTROL プロファイルとターゲット／サービスと購読]**&#x200B;ノードに移動して、「**[!UICONTROL 新規]**」をクリックします。

   ![](assets/nmac_service_1.png)

1. 「**[!UICONTROL ラベル]**」と「**[!UICONTROL 内部名]**」を定義します。
1. 「**[!UICONTROL タイプ]**」フィールドに移動して「**[!UICONTROL モバイルアプリケーション]**」を選択します。

   >[!NOTE]
   >
   >デフォルトの「**[!UICONTROL 購読者のアプリケーション（nms:appSubscriptionRcp）]**」ターゲットマッピングが受信者のテーブルにリンクされています。異なるターゲットマッピングを使用する場合は、新しいターゲットマッピングを作成し、サービスの「**[!UICONTROL ターゲットマッピング]**」フィールドに入力する必要があります。ターゲットマッピングの作成について詳しくは、[設定ガイド](../../configuration/using/about-custom-recipient-table.md)を参照してください。

   ![](assets/nmac_ios.png)

1. 次に、「**[!UICONTROL 追加]**」ボタンをクリックして、アプリケーションタイプを選択します。

   ![](assets/nmac_service_2.png)

1. iOS開発および実稼働環境用アプリケーションを作成します。 詳しくは、[この節](../../delivery/using/configuring-the-mobile-application.md#creating-ios-app)を参照してください。

## iOSモバイルアプリケーションの作成 {#creating-ios-app}

サービスを作成した後、iOSアプリケーションを作成する必要があります。

1. 新しく作成したサービスで、 **** 追加ボタンをクリックしてアプリケーションの種類を選択します。

   ![](assets/nmac_service_2.png)

1. 次のウィンドウが表示されます。「**[!UICONTROL iOS アプリケーションを作成]**」を選択し、**[!UICONTROL ラベル]**&#x200B;の入力を開始します。

   ![](assets/nmac_ios_2.png)

1. オプションとして、必要に応じ、**[!UICONTROL アプリケーション変数]**&#x200B;を使用してプッシュメッセージのコンテンツを強化できます。これらは完全にカスタマイズ可能で、モバイルデバイスに送信されるメッセージペイロードの一部です。次の例では、**mediaURl** および **mediaExt** を追加し、リッチなプッシュ通知を作成してさらに通知内に表示する画像をアプリケーションに提供します。

   ![](assets/nmac_ios_3.png)

1. 「**[!UICONTROL 購読パラメーター]**」タブを使用すると、**[!UICONTROL 購読者のアプリケーション（nms:appsubscriptionRcp）]**&#x200B;スキーマの拡張によりマッピングを定義できます。

   >[!NOTE]
   >
   >アプリケーションの開発バージョン（サンドボックス）と本番バージョンに同じ証明書を使用しないでください。

1. 「**[!UICONTROL サウンド]**」タブでは、再生するサウンドを指定できます。「**[!UICONTROL 追加]**」をクリックし、「**[!UICONTROL 内部名]**」フィールドに、アプリケーションに埋め込まれたファイル名またはシステムサウンドの名前を入力します。

1. 「**[!UICONTROL 次へ]**」をクリックし、開発アプリケーションの設定をおこないます。

1. Adobe Campaign と、アプリケーションコード（SDK 経由）で同じ「**[!UICONTROL 統合キー]**」が定義されていることを確認します。詳しくは、[Campaign SDK をモバイルアプリケーションに統合する](../../delivery/using/integrating-campaign-sdk-into-the-mobile-application.md)を参照してください。この統合キーは、各アプリケーションに対して固有で、モバイルアプリケーションを Adobe Campaign プラットフォームにリンクできます。

   >[!NOTE]
   >
   > **[!UICONTROL 統合キー]**&#x200B;は、文字列値を使用して完全にカスタマイズできますが、SDK で指定されたものと完全に同じにする必要があります。

1. Select one of the out-of-the-box icons from the **[!UICONTROL Application icon]** field to personalize mobile application in your service.

1. [ **[!UICONTROL 認証モード]**]を選択します。 認証モードは、後でモバイルアプリケーションの「 **[!UICONTROL 証明書]** 」タブで変更することができます。
   * **[!UICONTROL 証明書ベースの認証]**:「証明書を **[!UICONTROL 入力。.]** 」をクリックし、p12キーを選択して、モバイルアプリケーション開発者から提供されたパスワードを入力します。
   * **[!UICONTROL トークンベースの認証]**:接続設定の **[!UICONTROL キーID]**、 **[!UICONTROL チームID]** 、 **[!UICONTROL バンドルIDを入力し、「秘密鍵を]******&#x200B;入力」をクリックしてp8証明書を選択します。 トー **[!UICONTROL クンベースの認証について詳しくは、]** Appleのドキュメントを参照してください [](https://developer.apple.com/documentation/usernotifications/setting_up_a_remote_notification_server/establishing_a_token-based_connection_to_apnsToken-based)。

   >[!NOTE]
   >
   > Adobeでは、iOS設定に **[!UICONTROL トークンベースの認証]** （認証モード）を使用することをお勧めします。これは、この認証モードの方がセキュリティが強化され、証明書の有効期限に縛られないためです。

   ![](assets/nmac_ios_4.png)

1. 「**[!UICONTROL 接続をテスト]**」をクリックすると、接続が成功したことを確認できます。

1. 「**[!UICONTROL 次へ]**」をクリックして本番アプリケーションの設定をおこない、上記と同じ手順に従います。

   ![](assets/nmac_ios_5.png)

1. 「**[!UICONTROL 完了]**」をクリックします。

これで、Campaign Classic で iOS アプリケーションを使用する準備が整いました。

## Creating an iOS rich notification {#creating-ios-delivery}

iOS 10 以降では、リッチ通知を生成することができます。Adobe Campaign では、変数を使用して通知を送信し、デバイスでリッチ通知を表示できます。

次に、新しい配信を作成し、作成したモバイルアプリケーションにリンクする必要があります。

1. **[!UICONTROL キャンペーン管理]**／**[!UICONTROL 配信]**&#x200B;に移動します。

1. 「**[!UICONTROL 新規]**」をクリックします。

   ![](assets/nmac_android_3.png)

1. 「**[!UICONTROL 配信テンプレート]**」ドロップダウンで「**[!UICONTROL iOS 配信（ios）]**」を選択します。配信に&#x200B;**[!UICONTROL ラベル]**&#x200B;を追加します。

1. 「**[!UICONTROL 宛先]**」をクリックして、ターゲットにする母集団を定義します。デフォルトでは、**[!UICONTROL 購読者のアプリケーション]**&#x200B;ターゲットマッピングが適用されます。「**[!UICONTROL 追加]**」をクリックして、前の手順で作成したサービスを選択します。

   ![](assets/nmac_ios_9.png)

1. **[!UICONTROL ターゲットのタイプ]**&#x200B;ウィンドウで、「**[!UICONTROL iOS モバイルアプリケーション (iPhone、iPad) の購読者]**」を選択し、「**[!UICONTROL 次へ]**」をクリックします。

1. 「**[!UICONTROL サービス]**」ドロップダウンで、前の手順で作成したサービスを選択し、ターゲットするアプリケーションを選択して「**[!UICONTROL 完了]**」をクリックします。**[!UICONTROL アプリケーション変数]**&#x200B;は、設定手順で追加された内容に応じて自動的に追加されます。

   ![](assets/nmac_ios_6.png)

1. リッチ通知を編集します。

   ![](assets/nmac_ios_7.png)

1. 通知を編集ウィンドウの「**[!UICONTROL 可変コンテンツ]**」ボックスをオンにして、モバイルアプリケーションがメディアコンテンツをダウンロードできるようにします。

1. 「**[!UICONTROL 保存]**」をクリックし、配信を送信します。

プッシュ通知が購読者のモバイル iOS デバイスで受信されると、画像と Web ページが表示されます。

![](assets/nmac_ios_8.png)
