---
title: Twitter へのパブリッシュの設定
seo-title: Twitter へのパブリッシュの設定
description: Twitter へのパブリッシュの設定
seo-description: null
page-status-flag: never-activated
uuid: 88867881-fb59-4f0d-862e-537d498e9aef
contentOwner: sauviat
products: SG_CAMPAIGN/CLASSIC
audience: social
content-type: reference
topic-tags: configuration
discoiquuid: 9d74ed9c-0055-4556-a205-6e5fea11816b
translation-type: ht
source-git-commit: 70b143445b2e77128b9404e35d96b39694d55335
workflow-type: ht
source-wordcount: '798'
ht-degree: 100%

---


# Twitter へのパブリッシュの設定{#configuring-publishing-on-twitter}

Adobe Campaign で Twitter アカウントに対してツイートを送信できるようにするには、これらのアカウントの Adobe Campaign への書き込みアクセス権をデリゲートする必要があります。それには、次の設定手順に従います。

* Twitter アカウントを作成します。
* 配達確認を送信するためのテスト用 Twitter アカウントを作成します。
* Twitter アカウントごとに 1 つの Twitter アプリケーションを作成します。
* 各 Twitter アプリケーションに対して、新しい **[!UICONTROL Twitter]** タイプのサービスを作成します。

![](assets/social_diagram_twitter_service.png)

## 前提条件 {#prerequisites}

まず、ツイートの送信先となる 1 つ以上の Twitter アカウントを作成します。

Twitter アカウントを作成するには、[https://twitter.com](https://twitter.com) にアクセスします。

## Twitter でのテストアカウントの作成 {#creating-a-test-account-on-twitter}

ツイートの配達確認を送信するために使用できる非公開の Twitter アカウントを作成することもお勧めします（詳しくは、[配達確認の送信](../../social/using/publishing-on-twitter.md#sending-the-proof)を参照）。

* 新しい Twitter アカウントを作成します。
* 右上隅のメニューをクリックし、「**[!UICONTROL 設定]**」を選択します。
* 「**[!UICONTROL セキュリティとプライバシー]**」タブを選択し、「**[!UICONTROL ツイートを保護]**」チェックボックスをオンにします。
* ページ下部の「**[!UICONTROL 変更を保存]**」ボタンをクリックします。

![](assets/social_twitter_test_page.png)

## Twitter でのアプリケーションの作成 {#creating-an-application-on-twitter}

Adobe Campaign で Twitter アカウントに対してツイートを送信できるようにするには、Twitter アカウントごとに 1 つの Twitter アプリケーションを作成する必要があります。それには、次の手順に従います。

1. Twitter アカウントにログオンします。
1. インターネットブラウザーにアドレス [https://apps.twitter.com/](https://apps.twitter.com/) を入力します。
1. 次に、右側の「**[!UICONTROL Create New App]**」ボタンをクリックします。

   ![](assets/social_create_twitter_app_001.png)

1. ウィザードの指示に従ってプロセスを進めます。

   このアプリケーションで Adobe Campaign が自分のアカウントにツイートを送信できるようにするには、アプリケーションの「**[!UICONTROL Permissions]**」タブに移動し、「**[!UICONTROL Access]**」セクションで「**[!UICONTROL Read and Write]**」を選択します。また、「**[!UICONTROL Settings]**」タブで、「**[!UICONTROL Callback URL]**」フィールドを空のままにしておく必要があります。

   ![](assets/social_create_twitter_app_002.png)

## Adobe Campaign への書き込みアクセス権のデリゲート {#delegating-write-access-to-adobe-campaign}

Twitter アプリケーションごとに、アプリケーション設定を含む異なる **[!UICONTROL Twitter]** タイプのサービスを作成する必要があります。

この手順では、Adobe Campaign コンソールと、Twitter アカウントにログオンしているインターネットブラウザーに同時にアクセスする必要があります。

* **Twitter**：以前に作成したアプリケーション（[https://dev.twitter.com/apps](https://dev.twitter.com/apps)）を選択し、「**[!UICONTROL Keys and Access Tokens]**」タブをクリックします。

   ![](assets/social_twitter_service_002.png)

* **Adobe Campaign**：「**[!UICONTROL プロファイルとターゲット]**」領域に移動し、「**[!UICONTROL サービスと購読]**」リンクをクリックして、「**[!UICONTROL 作成]**」ボタンをクリックします。

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
   * サービスの概要で、作成した Twitter タイプのサービスをクリックします。
   * 「**[!UICONTROL Twitter ページ]**」タブを選択します。Twitter アカウントが表示されます。

      ![](assets/social_twitter_service_010.png)

1. 「**[!UICONTROL 訪問者フォルダー]**」フィールドで、フォロワーを作成する訪問者フォルダーを選択します。詳しくは、[動作の仕組み](../../social/using/publishing-on-twitter.md#operating-principle)を参照してください。デフォルトでは、フォロワーは&#x200B;**[!UICONTROL 訪問者]**&#x200B;フォルダーのルートに作成されます。

   ![](assets/social_twitter_service_010_b.png)

1. Twitter で、「**[!UICONTROL Consumer Key（API キー）]**」および「**[!UICONTROL Consumer Secret（API 秘密鍵）]**」フィールドの内容をコピーし、コンソールの「**[!UICONTROL Consumer key]**」および「**[!UICONTROL Consumer secret]**」フィールドに貼り付けます。

   ![](assets/social_twitter_service_012.png)

1. Twitter で、「**[!UICONTROL アクセストークン]**」および「**[!UICONTROL アクセストークン秘密鍵]**」フィールドの内容をコピーし、「**[!UICONTROL アクセストークン]**」および「**[!UICONTROL アクセストークン秘密鍵]**」フィールドに貼り付けます。

   ![](assets/social_twitter_service_013.png)

1. Adobe Campaign コンソールで、「**[!UICONTROL 保存]**」をクリックします。これで、書き込みアクセス権の Adobe Campaign へのデリゲートが完了しました。

   ![](assets/social_twitter_service_014.png)

>[!NOTE]
>
>Twitter アプリケーションごとに 1 つの **[!UICONTROL Twitter]** タイプのサービスを作成する必要があります。

**[!UICONTROL Twitter アカウントの同期]**&#x200B;ワークフローは、Adobe Campaign で Twitter アカウントを同期します。詳しくは、[Facebook ページの同期](../../social/using/publishing-on-facebook-walls.md#synchronizing-facebook-pages)を参照してください。

## Twitter アカウントの同期 {#synchronizing-twitter-accounts}

>[!IMPORTANT]
>
>ワークフローで Twitter 購読者のリストを復元するには、アカウントにリンクされたサービスの編集セクションで「**[!UICONTROL Twitter アカウントの同期]**」チェックボックスをオンにする必要があります。詳しくは、[Adobe Campaign への書き込みアクセス権のデリゲート](#delegating-write-access-to-adobe-campaign)を参照してください。

**[!UICONTROL Twitter アカウントの同期]**&#x200B;ワークフロー（**[!UICONTROL 管理／プロダクション／テクニカルワークフロー／ソーシャルネットワーク管理]**&#x200B;ノードからアクセス）を使用すると、Adobe Campaign で以前に設定した Twitter アカウントを同期できます。デフォルトでは、このワークフローは毎週木曜日の午前 7 時 30 分にトリガーされます。

>[!NOTE]
>
>予想されるタスク処理を実行することで、ワークフローをいつでも開始できます。スケジューラーを編集して、ワークフローのトリガー頻度を変更することもできます。スケジューラーについて詳しくは、[この節](../../workflow/using/scheduler.md)を参照してください。

これで、Twitter アカウントにツイートを送信したり、フォロワーにダイレクトメッセージを送信したりできるようになりました。詳しくは、[Twitter へのパブリッシュ](../../social/using/publishing-on-twitter.md)を参照してください。
