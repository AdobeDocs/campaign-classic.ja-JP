---
title: Adobe Campaign での Android モバイルアプリケーションの設定
description: Android 用のモバイルアプリケーションの設定方法を説明します。
page-status-flag: never-activated
uuid: aff1a4a0-34e7-4ce0-9eb3-30a8de1380f2
contentOwner: sauviat
products: SG_CAMPAIGN/CLASSIC
audience: delivery
content-type: reference
topic-tags: sending-push-notifications
discoiquuid: 7b5a1ad6-da5a-4cbd-be51-984c07c8d0b3
index: y
internal: n
snippet: y
translation-type: ht
source-git-commit: 9844616f417608051bbff2593d6124d8ff83008c
workflow-type: ht
source-wordcount: '1731'
ht-degree: 100%

---


# Android の設定手順

パッケージがインストールされたら、Adobe Campaign Classic で Android アプリの設定を定義できます。

>[!NOTE]
>
>iOS 用にアプリを設定する方法と iOS 用の配信を作成する方法については、[この節](../../delivery/using/configuring-the-mobile-application.md)を参照してください。


## Android 外部アカウントの設定 {#configuring-external-account-android}

Android の場合、2 種類のコネクタを使用できます。

* V1 コネクタでは、MTA の子 1 つにつき 1 つのコネクタを使用できます。
* V2 コネクタでは、スループット向上のために FCM サーバーへの同時接続が可能です。

使用するコネクタを選択するには、次の手順に従います。

1. **[!UICONTROL 管理／プラットフォーム／外部アカウント]**&#x200B;に移動します。
1. **[!UICONTROL Android ルーティング]**&#x200B;外部アカウントを選択します。
1. 「**[!UICONTROL コネクタ]**」タブで、「**[!UICONTROL コネクタで使用された JavaScript]**」フィールドに次のように入力します。

   Android V2 の場合：https://localhost:8080/nms/jsp/androidPushConnectorV2.js

   >[!NOTE]
   >
   > または、https://localhost:8080/nms/jsp/androidPushConnector.js に設定することもできますが、コネクタのバージョン 2 を使用することをお勧めします。

   ![](assets/nmac_connectors3.png)

1. Android V2 では、アドビサーバー設定ファイル（serverConf.xml）で次の追加パラメーターを使用できます。

   * **maxGCMConnectPerChild**：それぞれの子サーバーで開始できる、FCM に対する並列 HTTP リクエストの最大数（デフォルト値は 8）。

## Android サービスの設定 {#configuring-android-service}

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

1. Android アプリケーションを作成します。詳しくは、[この節](../../delivery/using/configuring-the-mobile-application-android.md#creating-android-app)を参照してください。

## Android モバイルアプリケーションの作成 {#creating-android-app}

サービスの作成後に、Android アプリケーションを作成する必要があります。

1. 新しく作成したサービスで、「**[!UICONTROL 追加]**」ボタンをクリックしてアプリケーションタイプを選択します。

   ![](assets/nmac_service_2.png)

1. 「**[!UICONTROL Android アプリケーションを作成]**」を選択し、**[!UICONTROL ラベル]**&#x200B;を入力します。

   ![](assets/nmac_android.png)

1. Adobe Campaign と、アプリケーションコード（SDK 経由）で同じ「**[!UICONTROL 統合キー]**」が定義されていることを確認します。詳しくは、[Campaign SDK をモバイルアプリケーションに統合する](../../delivery/using/integrating-campaign-sdk-into-the-mobile-application.md)を参照してください。

   >[!NOTE]
   >
   > **[!UICONTROL 統合キー]**&#x200B;は、文字列値を使用して完全にカスタマイズできますが、SDK で指定されたものと完全に同じにする必要があります。

1. 次のいずれかの **[!UICONTROL API バージョン]**&#x200B;を選択します。
   * HTTP。詳しくは[この節](../../delivery/using/configuring-the-mobile-application-android.md#android-service-http)を参照してください。
   * HTTPV1。詳しくは[この節](../../delivery/using/configuring-the-mobile-application-android.md#android-service-httpv1)を参照してください。

1. **[!UICONTROL Firebase Cloud Messaging for Android の接続設定]**&#x200B;のフィールドに入力します。

1. 「**[!UICONTROL 完了]**」、「**[!UICONTROL 保存]**」の順にクリックします。これで、Campaign Classic で Android アプリケーションを使用する準備が整いました。

デフォルトでは、Adobe Campaign は&#x200B;**[!UICONTROL 購読者のアプリケーション（nms:appSubscriptionRcp）]**&#x200B;テーブルの「**[!UICONTROL ユーザー ID]**」（@userKey）フィールドにキーを保存します。このキーによって購読情報を受信者にリンクできます。追加データ（複雑な紐付けキーなど）を収集するには、次の設定を適用する必要があります。

1. 「**[!UICONTROL 購読者のアプリケーション（nms:appsubscriptionRcp）]**」スキーマの拡張を作成し、新しいフィールドを定義します。

1. 「**[!UICONTROL 購読パラメーター]**」タブでマッピングを定義します。

   >[!CAUTION]
   >
   >「**[!UICONTROL 購読パラメーター]**」タブの設定名が、モバイルアプリケーションコードの設定名と同じであることを確認します。[Campaign SDK をモバイルアプリケーションに統合する](../../delivery/using/integrating-campaign-sdk-into-the-mobile-application.md)の節を参照してください。

### API バージョンを選択します。{#select-api-version}

サービスと新しいモバイルアプリケーションを作成したら、選択された API バージョンに応じてモバイルアプリケーションを設定する必要があります。

サービスおよびモバイルアプリケーションの作成について詳しくは、[この節](../../delivery/using/configuring-the-mobile-application-android.md#configuring-android-service)を参照してください。

#### HTTP v1 API バージョンの使用{#android-service-httpv1}

HTTP v1 API バージョンを設定するには、次の手順に従います。

1. **[!UICONTROL モバイルアプリケーション作成ウィザード]**&#x200B;ウィンドウの「**[!UICONTROL API バージョン]**」ドロップダウンで「**[!UICONTROL HTTPV1]**」を選択します。

1. 「**[!UICONTROL プロジェクトの詳細を抽出するプロジェクトの json ファイルを読み込む...]**」をクリックして、JSON キーファイルを直接読み込みます。JSON ファイルの抽出方法については、[このページ](https://firebase.google.com/docs/admin/setup#initialize-sdk)を参照してください。

1. 次の詳細を手動で入力することもできます。
   * **[!UICONTROL プロジェクト ID]**
   * **[!UICONTROL 秘密鍵]**
   * **[!UICONTROL クライアント E メール]**

   ![](assets/nmac_android_10.png)

1. 「**[!UICONTROL 接続をテスト]**」をクリックして、設定が正しいこと、およびマーケティングサーバーが FCM にアクセスできることを確認します。

   >[!CAUTION]
   >
   >ミッドソーシングデプロイメントの場合、「**[!UICONTROL 接続をテスト]**」ボタンは、MID サーバーが FCM サーバーにアクセスできるかどうかを確認しません。

   ![](assets/nmac_android_11.png)

1. オプションとして、必要に応じ、**[!UICONTROL アプリケーション変数]**&#x200B;を使用してプッシュメッセージのコンテンツを強化できます。これらは完全にカスタマイズ可能で、モバイルデバイスに送信されるメッセージペイロードの一部です。

1. 「**[!UICONTROL 完了]**」、「**[!UICONTROL 保存]**」の順にクリックします。これで、Campaign Classic で Android アプリケーションを使用する準備が整いました。

以下に、プッシュ通知をさらにパーソナライズするための FCM ペイロード名を示します。

| メッセージタイプ | 設定可能なメッセージ要素（FCM ペイロード名） | 設定可能なオプション（FCM ペイロード名） |
|:-:|:-:|:-:|
| データメッセージ | 該当なし | validate_only |
| 通知メッセージ | title、body、android_channel_id、icon、sound、tag、color、click_action、image、ticker、sticky、visibility、notification_priority、notification_count <br> | validate_only |

<br>
<br>

#### HTTP API バージョン{#android-service-http}

HTTP（レガシー）API バージョンを設定するには、次の手順に従います。

1. **[!UICONTROL モバイルアプリケーションの作成ウィザード]**&#x200B;ウィンドウの「**[!UICONTROL API バージョン]**」ドロップダウンで「**[!UICONTROL HTTP (レガシー)]**」を選択します。

1. モバイルアプリケーションの開発者が提供した&#x200B;**[!UICONTROL プロジェクトキー]**&#x200B;を入力します。

1. オプションとして、必要に応じ、**[!UICONTROL アプリケーション変数]**&#x200B;を使用してプッシュメッセージのコンテンツを強化できます。これらは完全にカスタマイズ可能で、モバイルデバイスに送信されるメッセージペイロードの一部です。

   次の例では、**title**、**imageURL** および **iconURL** を追加し、リッチなプッシュ通知を作成してさらに通知内に表示する画像、タイトル、アイコンをアプリケーションに提供します。

   ![](assets/nmac_android_2.png)

1. 「**[!UICONTROL 完了]**」、「**[!UICONTROL 保存]**」の順にクリックします。これで、Campaign Classic で Android アプリケーションを使用する準備が整いました。

以下に、プッシュ通知をさらにパーソナライズするための FCM ペイロード名を示します。

| メッセージタイプ | 設定可能なメッセージ要素（FCM ペイロード名） | 設定可能なオプション（FCM ペイロード名） |
|:-:|:-:|:-:|
| データメッセージ | 該当なし | dryRun |
| 通知メッセージ | title、body、android_channel_id、icon、sound、tag、color、click_action <br> | dryRun |

<br>

## Android のリッチ通知の作成 {#creating-android-delivery}

Firebase Cloud Messaging では、次の 2 種類のメッセージの中から選択できます。

* **[!UICONTROL データメッセージ]**は、クライアントアプリで処理されます。
   <br>メッセージは、デバイスへの Android 通知を生成して表示するモバイルアプリケーションに直接送信されます。データメッセージには、カスタムアプリケーション変数のみが含まれます。

* **[!UICONTROL 通知メッセージ]**は、FCM SDK によって自動的に処理されます。
   <br> FCM は、クライアントアプリに代わって、ユーザーのデバイスにメッセージを自動的に表示します。通知メッセージには、事前に定義された一連のパラメーターとオプションが含まれていますが、カスタムアプリケーション変数を使用してさらにパーソナライズすることもできます。

Firebase Cloud Messaging のメッセージタイプについて詳しくは、[FCM ドキュメント](https://firebase.google.com/docs/cloud-messaging/concept-options#notifications_and_data_messages)を参照してください。

### データメッセージの作成　{#creating-data-message}

1. **[!UICONTROL キャンペーン管理]**／**[!UICONTROL 配信]**&#x200B;に移動します。

1. 「**[!UICONTROL 新規]**」をクリックします。

   ![](assets/nmac_android_3.png)

1. 「**[!UICONTROL 配信テンプレート]**」ドロップダウンで「**[!UICONTROL Android 配信（android）]**」を選択します。配信に&#x200B;**[!UICONTROL ラベル]**&#x200B;を追加します。

1. 「**[!UICONTROL 宛先]**」をクリックして、ターゲットにする母集団を定義します。デフォルトでは、**[!UICONTROL 購読者のアプリケーション]**&#x200B;ターゲットマッピングが適用されます。「**[!UICONTROL 追加]**」をクリックしてサービスを選択します。

   ![](assets/nmac_android_7.png)

1. **[!UICONTROL ターゲットのタイプ]******&#x200B;ウィンドウで、「Android モバイルアプリケーションの購読者」を選択し、「**[!UICONTROL 次へ]**」をクリックします。

1. 「**[!UICONTROL サービス]**」ドロップダウンで、以前に作成したサービスとアプリケーションを選択して「**[!UICONTROL 完了]**」をクリックします。**[!UICONTROL アプリケーション変数]**&#x200B;は、設定手順で追加された内容に応じて自動的に追加されます。

   ![](assets/nmac_android_6.png)

1. 「**[!UICONTROL メッセージタイプ]**」で「**[!UICONTROL データメッセージ]**」を選択します。

1. リッチ通知を編集します。

   ![](assets/nmac_android_5.png)

1. 必要に応じて、以前設定した&#x200B;**[!UICONTROL アプリケーション変数]**&#x200B;に情報を追加できます。**[!UICONTROL アプリケーション変数]**&#x200B;は、Android サービスで設定する必要があり、モバイルデバイスに送信されるメッセージペイロードの一部です。

1. 「**[!UICONTROL 保存]**」をクリックし、配信を送信します。

プッシュ通知が購読者のモバイル Android デバイスで受信されると、画像と web ページが表示されます。

![](assets/nmac_android_4.png)

### 通知メッセージの作成 {#creating-notification-message}

>[!NOTE]
>
>通知メッセージのその他のオプションは、HTTP v1 API 設定でのみ使用できます。詳しくは、[この節](../../delivery/using/configuring-the-mobile-application-android.md#android-service-httpv1)を参照してください。

1. **[!UICONTROL キャンペーン管理]**／**[!UICONTROL 配信]**&#x200B;に移動します。

1. 「**[!UICONTROL 新規]**」をクリックします。

   ![](assets/nmac_android_3.png)

1. 「**[!UICONTROL 配信テンプレート]**」ドロップダウンで「**[!UICONTROL Android 配信（android）]**」を選択します。配信に&#x200B;**[!UICONTROL ラベル]**&#x200B;を追加します。

1. 「**[!UICONTROL 宛先]**」をクリックして、ターゲットにする母集団を定義します。デフォルトでは、**[!UICONTROL 購読者のアプリケーション]**&#x200B;ターゲットマッピングが適用されます。「**[!UICONTROL 追加]**」をクリックしてサービスを選択します。

   ![](assets/nmac_android_7.png)

1. **[!UICONTROL ターゲットのタイプ]******&#x200B;ウィンドウで、「Android モバイルアプリケーションの購読者」を選択し、「**[!UICONTROL 次へ]**」をクリックします。

1. 「**[!UICONTROL サービス]**」ドロップダウンで、以前に作成したサービスとアプリケーションを選択して「**[!UICONTROL 完了]**」をクリックします。

   ![](assets/nmac_android_6.png)

1. 「**[!UICONTROL メッセージタイプ]**」で「**[!UICONTROL 通知メッセージ]**」を選択します。

1. タイトルを追加し、メッセージを編集します。「**[!UICONTROL 通知オプション]**」を使用して、プッシュ通知をパーソナライズします。

   * **[!UICONTROL チャネル ID]**：通知のチャネル ID を設定します。このチャネル ID を持つ通知を受信するには、このチャネル ID を持つチャネルをアプリで事前に作成しておく必要があります。
   * **[!UICONTROL サウンド]**：デバイスが通知を受け取るときに再生するサウンドを設定します。
   * **[!UICONTROL 色]**：通知アイコンの色を設定します。
   * **[!UICONTROL アイコン]**：プロファイルのデバイスに表示される通知アイコンを設定します。
   * **[!UICONTROL タグ]**：通知ドロワー内の既存の通知を置き換えるために使用する識別子を設定します。
   * **[!UICONTROL クリックアクション]**：通知のユーザークリックに関連付けられたアクションを設定します。

   **[!UICONTROL 通知オプション]**&#x200B;とこれらのフィールドに入力する方法について詳しくは、[FCM のドキュメント](https://firebase.google.com/docs/reference/fcm/rest/v1/projects.messages#androidnotification)を参照してください。

   ![](assets/nmac_android_8.png)

1. アプリケーションが HTTP v1 API プロトコルを使用して設定されている場合は、以下の **[!UICONTROL HTTPV1 その他のオプション]**&#x200B;を使用して、プッシュ通知をさらにパーソナライズできます。

   * **[!UICONTROL ティッカー]**：通知のティッカーテキストを設定します。Android 5.0 Lollipop に設定されたデバイスでのみ使用できます。
   * **[!UICONTROL 画像]**：通知に表示する画像の URL を設定します。
   * **[!UICONTROL 通知数]**：アプリケーションアイコンに直接表示する新しい未読情報の数を設定します。
   * **[!UICONTROL スティッキー]**：true または false に設定します。false に設定した場合、ユーザーがクリックすると通知が自動的に閉じます。true に設定した場合、ユーザーがクリックしても通知は表示されます。
   * **[!UICONTROL 通知優先度]**：通知の優先度レベルを、デフォルト、最小、低、高のいずれかに設定します。詳しくは、[FCM のドキュメント](https://firebase.google.com/docs/reference/fcm/rest/v1/projects.messages#NotificationPriority)を参照してください。
   * **[!UICONTROL 表示]**：通知の表示レベルをパブリック、プライベート、秘密のいずれかに設定します。詳しくは、[FCM のドキュメント](https://firebase.google.com/docs/reference/fcm/rest/v1/projects.messages#visibility)を参照してください。

   **[!UICONTROL HTTPV1 その他のオプション]**&#x200B;とこれらのフィールドを設定する方法について詳しくは、[FCM ドキュメント](https://firebase.google.com/docs/reference/fcm/rest/v1/projects.messages#androidnotification)を参照してください。

   ![](assets/nmac_android_9.png)

1. 必要に応じて、以前設定した&#x200B;**[!UICONTROL アプリケーション変数]**&#x200B;に情報を追加できます。**[!UICONTROL アプリケーション変数]**&#x200B;は、Android サービスで設定する必要があり、モバイルデバイスに送信されるメッセージペイロードの一部です。

1. 「**[!UICONTROL 保存]**」をクリックし、配信を送信します。

プッシュ通知が購読者のモバイル Android デバイスで受信されると、画像と web ページが表示されます。
