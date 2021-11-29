---
product: campaign
title: Twitter へのパブリッシュの設定
description: Twitter へのパブリッシュの設定
audience: social
content-type: reference
topic-tags: configuration
exl-id: 2d2a6e32-587d-4a7b-ba1c-d9140da53f64
source-git-commit: d11c918213e72fe4bf6adb464e516fac19b63d54
workflow-type: tm+mt
source-wordcount: '784'
ht-degree: 60%

---

# twitterに公開するための設定手順{#configuring-publishing-on-twitter}

![](../../assets/v7-only.svg)

Adobe Campaign で Twitter アカウントに対してツイートを送信できるようにするには、これらのアカウントの Adobe Campaign への書き込みアクセス権をデリゲートする必要があります。それには、次の設定手順に従います。

* Twitter アカウントを作成します。
* 配達確認を送信するためのテスト用 Twitter アカウントを作成します。
* Twitter アカウントごとに 1 つの Twitter アプリケーションを作成します。
* 各 Twitter アプリケーションに対して、新しい **[!UICONTROL Twitter]** タイプのサービスを作成します。

![](assets/social_diagram_twitter_service.png)

## 前提条件 {#prerequisites}

まず、ツイートの送信先となる 1 つまたは複数の Twitter アカウントを作成します。

twitterアカウントを作成するには、に移動します。 [https://twitter.com](https://twitter.com){target=&quot;_blank&quot;}。

## twitterでのテストアカウントの作成 {#creating-a-test-account-on-twitter}

送信に使用できるプライベートTwitterアカウントを作成します [配達確認をツイート](../../social/using/publishing-on-twitter.md#sending-the-proof). プライベートTwitterアカウントを作成するには、次の手順に従います。

1. 新しい Twitter アカウントを作成します。
1. アカウントにアクセス  **[!UICONTROL 設定]**.
1. 参照先 **[!UICONTROL プライバシーと安全]** および **[!UICONTROL オーディエンスとタグ付け]** そして、 **[!UICONTROL Protect]** オプション。 ツイートやその他のアカウント情報は、自分をフォローしている人にのみ表示されます。

![](assets/social_twitter_test_page.png)

## twitterでのアプリケーションの作成 {#creating-an-application-on-twitter}

Adobe Campaign で Twitter アカウントに対してツイートを送信できるようにするには、Twitter アカウントごとに 1 つの Twitter アプリケーションを作成する必要があります。それには、次の手順に従います。

1. Twitter アカウントにログオンします。
1. インターネットブラウザーに次のアドレスを入力します。 [https://developer.twitter.com/en/apps](https://developer.twitter.com/en/apps).
1. 次に、 **[!UICONTROL アプリの作成]** 」ボタンをクリックします。

   ![](assets/social_create_twitter_app_001.png)

1. ウィザードの指示に従ってプロセスを進めます。

   このアプリケーションで Adobe Campaign が自分のアカウントにツイートを送信できるようにするには、アプリケーションの「**[!UICONTROL Permissions]**」タブに移動し、「**[!UICONTROL Access]**」セクションで「**[!UICONTROL Read and Write]**」を選択します。また、「**[!UICONTROL Settings]**」タブで、「**[!UICONTROL Callback URL]**」フィールドを空のままにしておく必要があります。

   ![](assets/social_create_twitter_app_002.png)

## 書き込みアクセスをAdobe Campaignに委任 {#delegating-write-access-to-adobe-campaign}

Twitter アプリケーションごとに、アプリケーション設定を含む異なる **[!UICONTROL Twitter]** タイプのサービスを作成する必要があります。

この手順では、Adobe Campaign コンソールと、Twitter アカウントにログオンしているインターネットブラウザーに同時にアクセスする必要があります。

* in **Twitter**:から [このページ](https://developer.twitter.com/en/portal/projects-and-apps)、作成済みのアプリを選択し、 **アプリの権限**.

   ![](assets/social_twitter_service_002.png)

   を編集します。 **キーとトークン** タブをクリックして、アプリの詳細にアクセスします。

* in **Adobe Campaign**:に移動する **[!UICONTROL プロファイルとターゲット]** タブで、 **[!UICONTROL サービスと購読]** リンクをクリックし、 **[!UICONTROL 作成]** 」ボタンをクリックします。

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
   * サービスの概要で、先ほど作成したTwitterサービスをクリックします。

   <!-- * Select the **[!UICONTROL Twitter page]** tab. The Twitter account should be displayed. 
    
      ![](assets/social_twitter_service_010.png)-->

1. 内 **[!UICONTROL 訪問者フォルダー]** 「 」フィールドで、フォロワーを作成するフォルダーを選択します。 詳しくは、[この節](../../social/using/publishing-on-twitter.md#operating-principle)を参照してください。デフォルトでは、フォロワーは **[!UICONTROL 訪問者]** フォルダー。

   ![](assets/social_twitter_service_010_b.png)

1. twitterで、 **[!UICONTROL 消費者キー（API キー）]** および **[!UICONTROL 消費者の秘密鍵（API の秘密鍵）]** フィールドに **[!UICONTROL 消費者キー]** および **[!UICONTROL 消費者秘密鍵]** Campaign クライアントコンソールのフィールド。

   ![](assets/social_twitter_service_012.png)

1. twitterで、 **[!UICONTROL アクセストークン]** および **[!UICONTROL アクセストークン秘密鍵]** フィールドに **[!UICONTROL アクセストークン]** および **[!UICONTROL アクセストークン秘密鍵]** Campaign クライアントコンソールのフィールド。

   ![](assets/social_twitter_service_013.png)

1. Campaign クライアントコンソールで、 **[!UICONTROL 保存]**. これで、書き込みアクセス権がAdobe Campaignに委任されました。

   ![](assets/social_twitter_service_014.png)

>[!NOTE]
>
>作成する必要があります **[!UICONTROL Twitter]** twitterアプリケーションごとのサービス

**[!UICONTROL Twitter アカウントの同期]**&#x200B;ワークフローは、Adobe Campaign で Twitter アカウントを同期します。詳しくは、[このページ](../../social/using/publishing-on-facebook-walls.md#synchronizing-facebook-pages)を参照してください。

## twitterアカウントの同期 {#synchronizing-twitter-accounts}

>[!IMPORTANT]
>
>ワークフローで Twitter 購読者のリストを復元するには、アカウントにリンクされたサービスの編集セクションで「**[!UICONTROL Twitter アカウントの同期]**」チェックボックスをオンにする必要があります。詳しくは、[この節](#delegating-write-access-to-adobe-campaign)を参照してください。

**[!UICONTROL Twitter アカウントの同期]**&#x200B;ワークフロー（**[!UICONTROL 管理／プロダクション／テクニカルワークフロー／ソーシャルネットワーク管理]**&#x200B;ノードからアクセス）を使用すると、Adobe Campaign で以前に設定した Twitter アカウントを同期できます。デフォルトでは、このワークフローは毎週木曜日の午前 7 時 30 分にトリガーされます。

>[!NOTE]
>
>予想されるタスク処理を実行することで、いつでもワークフローを開始できます。 スケジューラーを編集して、ワークフローのトリガー頻度を変更することもできます。スケジューラーについて詳しくは、[この節](../../workflow/using/scheduler.md)を参照してください。

これで、Twitter アカウントにツイートを送信したり、フォロワーにダイレクトメッセージを送信したりできるようになりました。詳しくは、[このページ](../../social/using/publishing-on-twitter.md)を参照してください。
