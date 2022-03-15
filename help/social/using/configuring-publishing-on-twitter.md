---
product: campaign
title: Twitter へのパブリッシュの設定
description: Twitter へのパブリッシュの設定
audience: social
content-type: reference
topic-tags: configuration
exl-id: 2d2a6e32-587d-4a7b-ba1c-d9140da53f64
source-git-commit: d891a235002d465f3b00fafa375d87d42ebafaa6
workflow-type: tm+mt
source-wordcount: '776'
ht-degree: 100%

---

# Twitter に公開するための設定手順{#configuring-publishing-on-twitter}

![](../../assets/v7-only.svg)

Adobe Campaign で Twitter アカウントに対してツイートを送信できるようにするには、これらのアカウントの Adobe Campaign への書き込みアクセス権をデリゲートする必要があります。それには、次の設定手順に従います。

* Twitter アカウントを作成します。
* 配達確認を送信するためのテスト用 Twitter アカウントを作成します。
* Twitter アカウントごとに 1 つの Twitter アプリケーションを作成します。
* 各 Twitter アプリケーションに対して、新しい **[!UICONTROL Twitter]** タイプのサービスを作成します。

![](assets/social_diagram_twitter_service.png)

## 前提条件 {#prerequisites}

まず、ツイートの送信先となる 1 つまたは複数の Twitter アカウントを作成します。

Twitter アカウントを作成するには、[https://twitter.com](https://twitter.com){target=&quot;_blank&quot;} にアクセスします。

## Twitter でのテストアカウントの作成 {#creating-a-test-account-on-twitter}

[ツイートの配達確認](../../social/using/publishing-on-twitter.md#sending-the-proof)の送信に使用できる非公開 Twitter アカウントを作成します。非公開 Twitter アカウントを作成するには、次の手順に従います。

1. 新しい Twitter アカウントを作成します。
1. そのアカウントの&#x200B;**[!UICONTROL 設定]**&#x200B;にアクセスします。
1. 「**[!UICONTROL プライバシーと安全性]**」および「**[!UICONTROL オーディエンスとタグ付け]**」を参照し、「**[!UICONTROL ツイートの保護]**」オプションをオンにします。ツイートやその他のアカウント情報は、フォロワーにのみ表示されます。

![](assets/social_twitter_test_page.png)

## Twitter でのアプリケーションの作成 {#creating-an-application-on-twitter}

Adobe Campaign で Twitter アカウントに対してツイートを送信できるようにするには、Twitter アカウントごとに 1 つの Twitter アプリケーションを作成する必要があります。それには、次の手順に従います。

1. Twitter アカウントにログオンします。
1. インターネットブラウザーに [https://developer.twitter.com/en/apps](https://developer.twitter.com/en/apps) のアドレスを入力します。
1. 次に、右側の「**[!UICONTROL アプリの作成]**」ボタンをクリックします。

   ![](assets/social_create_twitter_app_001.png)

1. ウィザードの指示に従ってプロセスを進めます。

   このアプリケーションで Adobe Campaign が自分のアカウントにツイートを送信できるようにするには、アプリケーションの「**[!UICONTROL Permissions]**」タブに移動し、「**[!UICONTROL Access]**」セクションで「**[!UICONTROL Read and Write]**」を選択します。また、「**[!UICONTROL Settings]**」タブで、「**[!UICONTROL Callback URL]**」フィールドを空のままにしておく必要があります。

   ![](assets/social_create_twitter_app_002.png)

## Adobe Campaign への書き込みアクセス権のデリゲート {#delegating-write-access-to-adobe-campaign}

Twitter アプリケーションごとに、アプリケーション設定を含む異なる **[!UICONTROL Twitter]** タイプのサービスを作成する必要があります。

この手順では、Adobe Campaign コンソールと、Twitter アカウントにログオンしているインターネットブラウザーに同時にアクセスする必要があります。

* **Twitter の場合**：[このページ](https://developer.twitter.com/en/portal/projects-and-apps)で、作成済みのアプリを選択し「**アプリの権限**」を編集します。

   ![](assets/social_twitter_service_002.png)

   「**キーとトークン**」タブを編集し、アプリの詳細にアクセスします。

* **Adobe Campaign の場合**：「**[!UICONTROL プロファイルとターゲット]**」タブに移動し、「**[!UICONTROL サービスと購読]**」リンクをクリックして、「**[!UICONTROL 作成]**」ボタンをクリックします。

   ![](assets/social_twitter_service_007.png)

1. **[!UICONTROL Twitter]** タイプを選択します。

   ![](assets/social_twitter_service_008.png)

   >[!NOTE]
   >
   >「**[!UICONTROL 購読を同期]**」オプションはデフォルトで有効になっています。このチェックボックスをオンにすると、Twitter アカウントの同期ワークフロー（[Twitter アカウントの同期](#synchronizing-twitter-accounts)を参照）で Twitter フォロワーのリストが復元され、ダイレクトメッセージを送信できるようになります（[購読者へのダイレクトメッセージの送信](../../social/using/publishing-on-twitter.md#sending-direct-messages-to-subscribers)を参照）。フォロワーのリストを復元しない場合は、このチェックボックスをオフにします。

1. サービスのラベルおよび内部名を入力します。

   ![](assets/social_twitter_service_009.png)

   >[!IMPORTANT]
   >
   >サービスの&#x200B;**[!UICONTROL 内部名]**&#x200B;は、Twitter アカウントの名前と同じである必要があります。入力エラーがないことを確認するには、次の手順に従います。

   * 「**[!UICONTROL 保存]**」ボタンをクリックします。
   * サービスの概要で、作成したばかりの Twitter サービスをクリックします。

   <!-- * Select the **[!UICONTROL Twitter page]** tab. The Twitter account should be displayed. 
    
      ![](assets/social_twitter_service_010.png)-->

1. 「**[!UICONTROL 訪問者フォルダー]**」フィールドで、フォロワーが作成されるフォルダーを選択します。詳しくは、[この節](../../social/using/publishing-on-twitter.md#operating-principle)を参照してください。デフォルトでは、フォロワーは&#x200B;**[!UICONTROL 訪問者]**&#x200B;フォルダーに保存されます。

   ![](assets/social_twitter_service_010_b.png)

1. Twitter で、「**[!UICONTROL Consumer Key (API Key)]**」フィールドと「**[!UICONTROL Consumer Secret (API Secret)]**」フィールドの内容をコピーして、Campaign クライアントコンソールの「**[!UICONTROL Consumer key]**」フィールドと「**[!UICONTROL Consumer secret]**」フィールドに貼り付けます。

   ![](assets/social_twitter_service_012.png)

1. Twitter で、「**[!UICONTROL Access Token]**」フィールドと「**[!UICONTROL Access Token Secret]**」フィールドの内容をコピーし、Campaign クライアントコンソールの「**[!UICONTROL アクセストークン]**」フィールドと「**[!UICONTROL アクセストークン秘密鍵]**」フィールドに貼り付けます。

   ![](assets/social_twitter_service_013.png)

1. Campaign クライアントコンソールで、「**[!UICONTROL 保存]**」をクリックします。これで、書き込みアクセス権が Adobe Campaign にデリゲートされました。

   ![](assets/social_twitter_service_014.png)

>[!NOTE]
>
>Twitter アプリケーションごとに 1 つの **[!UICONTROL Twitter]** サービスを作成する必要があります。

**[!UICONTROL Twitter アカウントの同期]**&#x200B;ワークフローは、Adobe Campaign で Twitter アカウントを同期させます。

## Twitter アカウントの同期 {#synchronizing-twitter-accounts}

>[!IMPORTANT]
>
>ワークフローで Twitter 購読者のリストを復元するには、アカウントにリンクされているサービスの編集セクションで「**[!UICONTROL Twitter アカウントの同期]**」ボックスをオンにする必要があります。詳しくは、[この節](#delegating-write-access-to-adobe-campaign)を参照してください。

**[!UICONTROL Twitter アカウントの同期]**&#x200B;ワークフロー（**[!UICONTROL 管理／プロダクション／テクニカルワークフロー／ソーシャルネットワーク管理]**&#x200B;ノードからアクセス）を使用すると、Adobe Campaign で以前に設定した Twitter アカウントを同期できます。デフォルトでは、このワークフローは毎週木曜日の午前 7 時 30 分にトリガーされます。

>[!NOTE]
>
>予想されるタスク処理を実行することにより、いつでもワークフローを開始できます。 スケジューラーを編集して、ワークフローのトリガー頻度を変更することもできます。スケジューラーについて詳しくは、[この節](../../workflow/using/scheduler.md)を参照してください。

これで、Twitter アカウントにツイートを送信したり、フォロワーにダイレクトメッセージを送信したりできるようになりました。詳しくは、[このページ](../../social/using/publishing-on-twitter.md)を参照してください。
