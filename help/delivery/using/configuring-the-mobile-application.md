---
product: campaign
title: Adobe CampaignでのiOSモバイルアプリケーションの設定
description: iOS 用モバイルアプリケーションの設定方法を説明します。
feature: Push
exl-id: 67eee1c5-a918-46b9-875d-7c3c71c00635
source-git-commit: 9839dbacda475c2a586811e3c4f686b1b1baab05
workflow-type: tm+mt
source-wordcount: '739'
ht-degree: 98%

---

# iOS 向けの設定手順 {#configuring-the-mobile-application-in-adobe-campaign-ios}

![](../../assets/common.svg)

パッケージがインストールされたら、Adobe Campaign Classic で iOS アプリの設定を定義できます。

>[!NOTE]
>
>Android 用のアプリの設定方法と Android 用の配信の作成方法については、[この節](configuring-the-mobile-application-android.md)を参照してください。

主な手順は次のとおりです。

1. [iOS 外部アカウントの設定](#configuring-external-account-ios)
1. [iOS サービスの設定](#configuring-ios-service)
1. [Campaign での iOS モバイルアプリの統合](#creating-ios-app)

これで、[iOS デバイス用のプッシュ通知を作成](create-notifications-ios.md)できます。


## iOS 外部アカウントの設定 {#configuring-external-account-ios}

iOS では、iOS HTTP/2 コネクタが HTTP/2 APNs に通知を送信します。

このコネクタを設定するには、次の手順に従います。

1. **[!UICONTROL 管理／プラットフォーム／外部アカウント]**&#x200B;に移動します。
1. **[!UICONTROL iOS ルーティング]**&#x200B;外部アカウントを選択します。
1. 「**[!UICONTROL コネクタ]**」タブで、「**[!UICONTROL コネクタのアクセス URL]**」フィールドに「```http://localhost:8080/nms/jsp/iosHTTP2.jsp```」を入力します。

   ![](assets/nmac_connectors.png)

1. 「**[!UICONTROL 保存]**」をクリックします。

これで、iOS コネクタが設定されました。サービスの作成を開始できます。

## iOS サービスの設定 {#configuring-ios-service}

>[!CAUTION]
>
>Adobe Campaign SDK に統合する前に、アプリケーションにプッシュアクションを設定する必要があります。
>
>該当しない場合は、[このページ](https://developer.apple.com/documentation/usernotifications)を参照してください。

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

1. iOS の開発用アプリケーションおよび本番用アプリケーションを作成します。詳しくは、[この節](configuring-the-mobile-application.md#creating-ios-app)を参照してください。

## iOS モバイルアプリの作成 {#creating-ios-app}

サービスを作成したら、Campaign で iOS アプリケーションを作成します。以下の手順に従います。

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

1. Adobe Campaign と、アプリケーションコード（SDK 経由）で同じ「**[!UICONTROL 統合キー]**」が定義されていることを確認します。詳しくは、[このページ](integrating-campaign-sdk-into-the-mobile-application.md)を参照してください。この統合キーは各アプリケーションに対して固有のもので、これを使用すると、モバイルアプリケーションを Adobe Campaign プラットフォームにリンクできます。

   >[!NOTE]
   >
   > **[!UICONTROL 統合キー]**&#x200B;は、文字列値を使用して完全にカスタマイズできますが、SDK で指定されたものと完全に同じにする必要があります。

1. 「**[!UICONTROL アプリケーションアイコン]**」フィールドからあらかじめ用意されているアイコンの 1 つを選択して、サービス内のモバイルアプリケーションをパーソナライズします。

1. 「**[!UICONTROL 認証モード]**」を選択します。認証モードは、後でモバイルアプリケーションの「**[!UICONTROL 証明書]**」タブで変更することができます。
   * **[!UICONTROL 証明書ベースの認証]**：「**[!UICONTROL 証明書を入力...]**」をクリックし、p12 キーを選択して、モバイルアプリケーション開発者から提供されたパスワードを入力します。
   * **[!UICONTROL トークンベースの認証]**：接続設定の&#x200B;**[!UICONTROL キー ID]**、**[!UICONTROL チーム ID]**、**[!UICONTROL バンドル ID]** を入力し、「**[!UICONTROL 秘密鍵を入力]**」をクリックして p8 証明書を選択します。**[!UICONTROL トークンベースの認証]**&#x200B;について詳しくは、[Apple のドキュメント](https://developer.apple.com/documentation/usernotifications/setting_up_a_remote_notification_server/establishing_a_token-based_connection_to_apns)を参照してください。

   >[!NOTE]
   >
   > iOS 設定には&#x200B;**[!UICONTROL トークンベースの認証]**&#x200B;を使用することをお勧めします。これは、この認証モードの方がセキュリティが強化され、証明書の有効期限に縛られないためです。

   ![](assets/nmac_ios_4.png)

1. 「**[!UICONTROL 接続をテスト]**」をクリックすると、接続が成功したことを確認できます。

1. 「**[!UICONTROL 次へ]**」をクリックして本番アプリケーションの設定をおこない、上記と同じ手順に従います。

   ![](assets/nmac_ios_5.png)

1. 「**[!UICONTROL 完了]**」をクリックします。

これで、Campaign Classic で iOS アプリケーションを使用する準備が整いました。
