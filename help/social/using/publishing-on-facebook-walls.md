---
title: Facebook のウォールへのパブリッシュ
seo-title: Facebook のウォールへのパブリッシュ
description: Facebook のウォールへのパブリッシュ
seo-description: null
page-status-flag: never-activated
uuid: 02288473-a0d7-42b5-9f86-3c96550ab1a8
contentOwner: sauviat
products: SG_CAMPAIGN/CLASSIC
audience: social
content-type: reference
topic-tags: configuration
discoiquuid: 8577db0b-f1fc-41af-aa0f-ec4d02dac376
index: y
internal: n
snippet: y
translation-type: ht
source-git-commit: 0386ae88a1b4d9ebda64283d874e01b14e9e5af4
workflow-type: ht
source-wordcount: '1067'
ht-degree: 100%

---


# Facebook のウォールへのパブリッシュ{#publishing-on-facebook-walls}

Adobe Campaign で Facebook のウォールにパブリケーションを送信するには、これらのページへの書き込みアクセス権を Adobe Campaign にデリゲートする必要があります。それには、次の設定手順に従います。

1. 1 つ以上のページを持つ Facebook アカウントを作成します。
1. 配達確認を送信するためのテスト用 Facebook ページを作成します。
1. Facebook アプリケーションを作成します。
1. Adobe Campaign の **[!UICONTROL Facebook ルーティング]**&#x200B;外部アカウントに、Facebook アプリケーションの設定を入力します。

## 前提条件 {#prerequisites}

まず、Facebook アカウントおよび複数のページを作成します。これらはパブリケーションを送信するのに利用します。

* Facebook アカウントを作成するには、[https://www.facebook.com](https://www.facebook.com) リンクを使用します。
* Facebook ページを作成するには、[https://www.facebook.com/pages/create](https://www.facebook.com/pages/create) リンクを使用します。

   同じ Facebook アカウントを利用して、すべてのページを管理することを推奨します。こうすることで、アカウントのすべてのページに書き込むのに必要な Facebook アプリケーションおよび外部アカウントがそれぞれ 1 つだけになります。

   ![](assets/social_diagram_fb_external_account.png)

## テスト用 Facebook ページの作成 {#creating-a-test-facebook-page}

パブリケーションの配達確認を送信するための非公開 Facebook ページを作成することを推奨します（詳しくは、[配達確認の送信](../../social/using/publishing-on-facebook.md#sending-the-proof)を参照）。

1. ページの管理に使用する Facebook アカウントにログオンします。
1. 新しい Facebook ページを作成します。
1. 右上隅の「**[!UICONTROL 設定]**」ボタンをクリックします。
1. 「**[!UICONTROL 一般]**」タブで、ページの表示パラメーターを変更します。「**[!UICONTROL 未公開ページ]**」ボックスをオンにします。
1. 「**[!UICONTROL 変更を保存]**」ボタンをクリックします。

![](assets/social_facebook_test_page.png)

## Facebook アプリケーションの作成 {#creating-a-facebook-application}

Adobe Campaign がページのウォールにパブリッシュできるようにするには、Facebook アプリケーションを作成する必要があります。それには、次の手順に従います。

1. ページの管理に使用する Facebook アカウントにログオンします。
1. ブラウザーに次のアドレスを入力します。[https://developers.facebook.com/apps](https://developers.facebook.com/apps)

   >[!IMPORTANT]
   >
   >所有しているアカウントの種類に応じて、1 つ以上の認証が必要な場合があります。
   >
   >Facebook アプリケーションを作成するには、**認証済み** Facebook アカウントが必要です。

1. ページの右上隅にある「**[!UICONTROL 新しいアプリを追加]**」ボタンをクリックします。アプリケーションの名前と連絡先の E メールを入力し、セキュリティチェックを通過します。

   ![](assets/social_create_facebook_app_002.png)

1. **[!UICONTROL 設定／ベーシック]**&#x200B;の下にある「**[!UICONTROL プラットフォームを追加]**」をクリックし、**[!UICONTROL Facebookウェブゲーム]**&#x200B;というタイプを選択します。

   ![](assets/social_create_facebook_app_003.png)

1. 左側メニューの「**[!UICONTROL プロダクト]**」セクションで、**[!UICONTROL Facebook ログイン]**&#x200B;製品が表示されていることを確認します。そうでない場合は、新しい製品を追加し、「**[!UICONTROL Facebook ログイン]**」を選択します。

   ![](assets/social_create_facebook_app_003bis.png)

1. アプリケーションを作成したら、「**[!UICONTROL アプリレビュー]**」タブを選択し、アプリをパブリッシュします。

   ![](assets/social_create_facebook_app_004.png)

## Adobe Campaign への書き込みアクセス権のデリゲート {#delegating-write-access-to-adobe-campaign}

Adobe Campaign がページのウォールに投稿できるよう書き込みアクセス権をデリゲートするには、先に作成した Facebook アプリケーションのパラメーターを入力する必要があります。

この手順では、Adobe Campaign コンソールおよびページ管理に使用する Facebook アカウントにログオンしているインターネットブラウザーの両方にアクセスする必要があります。

>[!IMPORTANT]
>
>この設定をおこなうには、Adobe Campaign のオペレーターは管理権限が必要です。

* **Facebook**：先に作成したアプリケーション（[https://developers.facebook.com/apps](https://developers.facebook.com/apps)）を選択し、**[!UICONTROL 設定／ベーシック]**&#x200B;タブを選択します。

   ![](assets/social_facebook_external_account_002.png)

   >[!NOTE]
   >
   >「**[!UICONTROL Facebookウェブゲーム]**」セクションが表示されない場合は、ページの下部にある「**[!UICONTROL プラットフォームを追加]**」ボタンをクリックし、「**[!UICONTROL Facebookウェブゲーム]**」を選択します。

* **Adobe Campaign**：ツリーの&#x200B;**[!UICONTROL 管理／プラットフォーム／外部アカウント]**&#x200B;ノードに移動し、**[!UICONTROL Facebook ルーティング]**&#x200B;外部アカウントを選択して、「**[!UICONTROL コネクタ]**」タブをクリックします。

   ![](assets/social_facebook_external_account_001.png)

1. Adobe Campaign コンソールで、「**[!UICONTROL セキュアキャンバス URL]**」フィールドに含まれるアドレスをコピーし、Facebook の「**[!UICONTROL Facebookウェブゲーム]**」セクションにある「**[!UICONTROL FacebookウェブゲームのURL(https)]**」フィールドに貼り付けます。

   ![](assets/social_facebook_external_account_006.png)

   >[!IMPORTANT]
   >
   >どのような状況にあっても、保護されていない URL を使用してはいけません。

   この URL は、**[!UICONTROL プロダクト]**／**[!UICONTROL Facebookログイン]**／**[!UICONTROL 設定]**&#x200B;にある「**[!UICONTROL 有効なOAuthリダイレクトURI]**」にもコピーして貼り付けます。URL の有効性を確認するには、アプリケーションを保存し、URL をコピーして「**[!UICONTROL チェックするリダイレクトURI]**」フィールドに貼り付け、「**[!UICONTROL URIをチェック]**」をクリックします。

   ![](assets/social_facebook_external_account_007bis.png)

1. Facebook で、「**[!UICONTROL アプリID]**」および「**[!UICONTROL App Secret]**」フィールドの内容をコピーし、コンソールの一致するフィールドに貼り付けます。

   ![](assets/social_facebook_external_account_007.png)

1. Facebook で、ページの下部にある「**[!UICONTROL 変更を保存]**」ボタンをクリックします。
1. Adobe Campaign コンソールに移動し、外部アカウントを保存します。

   >[!NOTE]
   >
   >「**[!UICONTROL マーケティング URL]**」フィールドはオプションです。

1. Adobe Campaign コンソールで、「**[!UICONTROL コネクタ]**」タブの下部にある「**[!UICONTROL アプリケーションからの承認をリクエスト]**」リンクをクリックします。「**[!UICONTROL Facebook ページを同期]**」ワークフローが自動的にトリガーされ、管理者が管理するすべての Facebook ページが収集されます。詳しくは、[Facebook ページの同期](#synchronizing-facebook-pages)を参照してください。

   ![](assets/social_facebook_external_account_004.png)

   >[!NOTE]
   >
   >デフォルトでは、ページは **[!UICONTROL Facebook]** サービスフォルダーに追加され、**[!UICONTROL プロファイルとターゲット／サービスと購読]**&#x200B;ノードで確認できます。「**[!UICONTROL コネクタ]**」タブの「**[!UICONTROL フォルダー]**」フィールドでは、同期後に Facebook ページが作成されるサービスフォルダーを変更できます。また、「**[!UICONTROL フィルター]**」フィールドを使用すれば、Adobe Campaign で同期する Facebook ページを選択することも可能です。このフィールドを空のままにすると、管理者が管理するすべての Facebook ページが同期されます。

1. 様々な Facebook 権限設定が記されたダイアログボックスが表示されます。これにより、Adobe Campaign が Facebook アカウントのページにパブリケーションを送信できるようになります。

   様々な権限リクエストを受け入れます。

   ![](assets/social_facebook_external_account_003.png)

1. これで Adobe Campaign に Facebook アカウントのページのウォールにパブリッシュする権限が与えられます。

   ![](assets/social_facebook_external_account_011.png)

>[!NOTE]
>
>Facebook アカウントで複数のページを管理している場合は、Facebook アカウントの任意のページに書き込む 1 つの外部アカウントを設定します。新しい Facebook アカウントごとに、新しい&#x200B;**[!UICONTROL ルーティング]**&#x200B;タイプの外部アカウントを作成する必要があります。

「**[!UICONTROL Facebook ページを同期]**」ワークフローが Facebook アカウントが管理するすべてのページを同期するので、Adobe Campaign を介して直接ウォールに投稿できます。詳しくは、[Facebook ページの同期](#synchronizing-facebook-pages)を参照してください。

## Facebook ページの同期 {#synchronizing-facebook-pages}

**[!UICONTROL 管理／プロダクション／テクニカルワークフロー／ソーシャルネットワーク管理]**&#x200B;ノードでアクセスできる「**[!UICONTROL Facebook ページを同期]**」ワークフローを使用すると、先に設定した Facebook アカウントのページを（Adobe Campaign 内で）同期できます。デフォルトでは、このワークフローは、1 日に 1 回または管理者がサービス設定画面の「**[!UICONTROL アプリケーションからの承認をリクエスト]**」リンクをクリックするたびに（[Adobe Campaign への書き込みアクセス権のデリゲート](#delegating-write-access-to-adobe-campaign)を参照）実行されるよう、設定されています。

同期が完了すると、収集されたページは、外部アカウントに入力されたサービスフォルダーに表示されます（[Adobe Campaign への書き込みアクセス権のデリゲート](#delegating-write-access-to-adobe-campaign)を参照）。デフォルトでは、ページは **[!UICONTROL Facebook]** サービスフォルダーのルートに追加され、**[!UICONTROL プロファイルとターゲット／サービスと購読]**&#x200B;メニューで確認できます。

![](assets/social_facebook_service_002.png)

これで、Adobe Campaign を使用して Facebook ページのウォールに直接投稿できるようになりました。詳しくは、[Facebook へのパブリッシュ](#publishing-on-facebook-walls)を参照してください。
