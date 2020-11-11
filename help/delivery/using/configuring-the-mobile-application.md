---
title: Adobe Campaign での iOS モバイルアプリケーションの設定
description: iOS 用モバイルアプリケーションの設定方法を説明します。
page-status-flag: never-activated
uuid: aff1a4a0-34e7-4ce0-9eb3-30a8de1380f2
contentOwner: sauviat
products: SG_CAMPAIGN/CLASSIC
audience: delivery
content-type: reference
topic-tags: sending-push-notifications
discoiquuid: 7b5a1ad6-da5a-4cbd-be51-984c07c8d0b3
translation-type: ht
source-git-commit: 16985c1ddcd380cfc1ca4960b35bb5e78628f464
workflow-type: ht
source-wordcount: '944'
ht-degree: 100%

---


# iOS の設定手順 {#configuring-the-mobile-application-in-adobe-campaign-ios}

パッケージがインストールされたら、Adobe Campaign Classic で iOS アプリの設定を定義できます。

>[!NOTE]
>
>Android 用のアプリの設定方法と Android 用の配信の作成方法については、[この節](../../delivery/using/configuring-the-mobile-application-android.md)を参照してください。

## iOS 外部アカウントの設定 {#configuring-external-account-ios}

iOS では、iOS HTTP/2 コネクタが HTTP/2 APNs に通知を送信します。

このコネクタを設定するには、次の手順に従います。

1. **[!UICONTROL 管理／プラットフォーム／外部アカウント]**&#x200B;に移動します。
1. **[!UICONTROL iOS ルーティング]**&#x200B;外部アカウントを選択します。
1. 「**[!UICONTROL コネクタ]**」タブで、「**[!UICONTROL コネクタのアクセス URL]**」フィールドに「```http://localhost:8080/nms/jsp/iosHTTP2.jsp```」を入力します。

   >[!NOTE]
   >
   > Campaign 20.3 リリース以降、iOS レガシーバイナリコネクタは非推奨となりました。このコネクタを使用する場合は、それに応じて実装を適応させる必要があります。[詳細情報](https://helpx.adobe.com/jp/campaign/kb/migrate-to-http2.html)

   ![](assets/nmac_connectors.png)

1. 「**[!UICONTROL 保存]**」をクリックします。

これで、iOS コネクタが設定されました。サービスの作成を開始できます。

## iOS サービスの設定 {#configuring-ios-service}

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

1. iOS の開発用アプリケーションおよび本番用アプリケーションを作成します。詳しくは、[この節](../../delivery/using/configuring-the-mobile-application.md#creating-ios-app)を参照してください。

## iOS モバイルアプリケーションの作成 {#creating-ios-app}

サービスの作成後に、iOS アプリケーションを作成する必要があります。

1. 新しく作成したサービスで、「**[!UICONTROL 追加]**」ボタンをクリックしてアプリケーションタイプを選択します。

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

1. 「**[!UICONTROL アプリケーションアイコン]**」フィールドからあらかじめ用意されているアイコンの 1 つを選択して、サービス内のモバイルアプリケーションをパーソナライズします。

1. 「**[!UICONTROL 認証モード]**」を選択します。認証モードは、後でモバイルアプリケーションの「**[!UICONTROL 証明書]**」タブで変更することができます。
   * **[!UICONTROL 証明書ベースの認証]**：「**[!UICONTROL 証明書を入力...]**」をクリックし、p12 キーを選択して、モバイルアプリケーション開発者から提供されたパスワードを入力します。
   * **[!UICONTROL トークンベースの認証]**：接続設定の&#x200B;**[!UICONTROL キー ID]**、**[!UICONTROL チーム ID]**、**[!UICONTROL バンドル ID]** を入力し、「**[!UICONTROL 秘密鍵を入力]**」をクリックして p8 証明書を選択します。**[!UICONTROL トークンベースの認証]**&#x200B;について詳しくは、[Apple のドキュメント](https://developer.apple.com/documentation/usernotifications/setting_up_a_remote_notification_server/establishing_a_token-based_connection_to_apnsToken-based)を参照してください。

   >[!NOTE]
   >
   > iOS 設定には&#x200B;**[!UICONTROL トークンベースの認証]**&#x200B;を使用することをお勧めします。これは、この認証モードの方がセキュリティが強化され、証明書の有効期限に縛られないためです。

   ![](assets/nmac_ios_4.png)

1. 「**[!UICONTROL 接続をテスト]**」をクリックすると、接続が成功したことを確認できます。

1. 「**[!UICONTROL 次へ]**」をクリックして本番アプリケーションの設定をおこない、上記と同じ手順に従います。

   ![](assets/nmac_ios_5.png)

1. 「**[!UICONTROL 完了]**」をクリックします。

これで、Campaign Classic で iOS アプリケーションを使用する準備が整いました。

## iOS のリッチ通知の作成 {#creating-ios-delivery}

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

プッシュ通知が購読者のモバイル iOS デバイスで受信されると、画像と web ページが表示されます。

![](assets/nmac_ios_8.png)
