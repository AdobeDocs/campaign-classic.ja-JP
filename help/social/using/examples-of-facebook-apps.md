---
title: Facebook アプリの例
seo-title: Facebook アプリの例
description: Facebook アプリの例
seo-description: null
page-status-flag: never-activated
uuid: 336f4006-3545-4b04-959d-61cd0446af27
contentOwner: sauviat
products: SG_CAMPAIGN/CLASSIC
audience: social
content-type: reference
topic-tags: annexes
discoiquuid: 07be1d3c-b038-48ca-be37-a33adb8e0fc0
translation-type: ht
source-git-commit: a0ab8794bdbdfbe627bf33580dc8991793447336
workflow-type: ht
source-wordcount: '2129'
ht-degree: 100%

---


# Facebook アプリの例{#examples-of-facebook-apps}

ユーザーが Facebook アプリケーションのタブをクリックすると、幅が 810 ピクセルのスペースに表示されます。Adobe Campaign では、Facebook タイプの Web アプリケーションを使用して、Facebook アプリケーションに表示するコンテンツを定義およびパーソナライズできるので、プロフィールの取得が容易になります。

>[!NOTE]
>
>また、パートナーが開発した Facebook アプリケーションと Adobe Campaign を統合することもできます。この場合、Adobe Campaign Web アプリケーションを使用して Facebook のプロフィールを取得する必要はありません。詳しくは、[外部アカウントの設定](../../social/using/creating-a-facebook-application.md#configuring-external-accounts)を参照してください。

![](assets/social_webapp_fb_000.png)

>[!IMPORTANT]
>
>[Facebook アプリケーションの作成](../../social/using/creating-a-facebook-application.md)で説明されている設定手順に従ってください。

>[!NOTE]
>
>ここでは、Facebook タイプの Web アプリケーションに関連する要素について詳しく説明します。標準の Web アプリケーションと共有するすべての要素について詳しくは、[この節](../../web/using/about-web-applications.md)で説明しています。

ここで説明する Facebook タイプの Web アプリケーションの例を以下に示します。

* 7 ステップで Facebook アプリケーションを作成する方法。[クイックスタート：7 ステップで作成する Facebook アプリケーション](#quick-start--creating-a-facebook-application-in-7-steps)を参照してください。
* 設定を Facebook アプリケーションに転送する方法。[設定を Facebook アプリケーションに転送するには？](#how-to-forward-settings-to-a-facebook-application-)を参照してください。
* ファンデータの取得方法。[ファンデータを取得するには？](#how-to-acquire-fan-data-)を参照してください。

>[!IMPORTANT]
>
>Facebook タイプの Web アプリケーションの機能を説明する例として、シンプルな使用例が提供されています。

## 推奨事項 {#recommendations}

以下の制限は Facebook に直結しています。

* すべての Web アプリケーションは HTTPS で構築する必要があります。
* タブを介して表示される Facebook アプリケーションの幅は 810 ピクセルです。

## クイックスタート：7 ステップで作成する Facebook アプリケーション {#quick-start--creating-a-facebook-application-in-7-steps}

この例では、Adobe Campaign で作成したアプリケーションを Facebook に表示する方法について詳細な手順を説明します。ここでは、ユーザーがアプリケーションタブ（**App01**）をクリックすると&#x200B;**ようこそ**&#x200B;メッセージを表示できるアプリケーションを作成します。

このアプリケーションを作成するには、以下の手順に従います。

1. Facebook でアプリケーションを作成します（[https://developers.facebook.com/apps](https://developers.facebook.com/apps)）。詳しくは、[Facebook アプリケーションの作成](../../social/using/publishing-on-facebook-walls.md#creating-a-facebook-application)を参照してください。

   ![](assets/social_create_facebook_app_002.png)

1. **[!UICONTROL Facebook Connect]** タイプの外部アカウントを作成し、Facebook アプリケーションのパラメーターを入力します。詳しくは、[外部アカウントの設定](../../social/using/creating-a-facebook-application.md#configuring-external-accounts)を参照してください。

   ![](assets/social_quick_start_2.png)

1. Facebook 権限リクエスト画面に表示する&#x200B;**[!UICONTROL サービス利用条件]**&#x200B;および&#x200B;**[!UICONTROL プライバシーポリシー]**&#x200B;のリンクを入力します。詳しくは、[サービス利用条件およびプライバシーポリシーのリンクの入力](../../social/using/creating-a-facebook-application.md#entering-the-terms-of-service-and-privacy-policy-links)を参照してください。

   ![](assets/social_quick_start_1.png)

1. Adobe Campaign で Facebook タイプの Web アプリケーションを作成します。詳しくは、[Facebook タイプ の Web アプリケーションの作成](../../social/using/creating-a-facebook-application.md#creating-a-facebook-type-web-application)を参照してください。

   ![](assets/social_webapp_005.png)

1. Web アプリケーションを編集します。この例では、**[!UICONTROL ページ]**&#x200B;アクティビティを追加し、そのタイトルを定義しました。

   ![](assets/social_quick_start_4.png)

1. アプリケーションをデプロイします。

   ![](assets/social_webapp_004.png)

1. Facebook アプリケーションが Facebook ページのタブとして表示されるように設定します。詳しくは、[Facebook タブの設定](../../social/using/creating-a-facebook-application.md#configuring-facebook-tabs)を参照してください。

   ![](assets/social_quick_start_5.png)

![](assets/social_quick_start_6.png)

**App01** アプリケーションのタブが Facebook ページに表示されることを確認します。クリックすると、**ようこそ**&#x200B;メッセージが表示されます。

![](assets/social_webapp_042.png)

## 設定を Facebook アプリケーションに転送するには？{#how-to-forward-settings-to-a-facebook-application-}

>[!IMPORTANT]
>
>[Facebook アプリケーションの作成](../../social/using/creating-a-facebook-application.md)で説明されている設定手順に従います。

例 1 では、「**[!UICONTROL ページのファン]**」フィールドの値に応じて Facebook ページの表示をパーソナライズしました。また、「**[!UICONTROL アプリケーション設定]**」フィールドを処理することもできます。このフィールドを使用すると、Adobe Campaign で生成されたリンクに含まれていたデータを Facebook 経由で復元できます。

ここでは、E メールキャンペーンの送信を決定した会社の例を見てみましょう。配信では、リンクが Facebook アプリケーションを指しています。このリンクは、URL の末尾に追加されている **[!UICONTROL app_data]** パラメーターによってパーソナライズされます。このパラメーターの値は、顧客の重要性を反映する指標にすることができます。この例では、**[!UICONTROL app_data]** パラメーターの値は、**[!UICONTROL big]**（重要な顧客）と **[!UICONTROL small]**（あまり重要でない顧客）です。

パーソナライズされると、URL は以下のようになります。

* `http://<path of the Facebook application>&app_data=big`（重要な顧客の場合）
* `http://<path of the Facebook application>&app_data=small`（あまり重要でない顧客の場合）

Facebook によって Adobe Campaign に転送された匿名データの中で、「**[!UICONTROL アプリケーションパラメーター]**」フィールドの値が収集され、Adobe Campaign はこのパラメーターに基づいてアプリケーションの表示をパーソナライズできます。

ユーザーが重要な顧客（**[!UICONTROL app_data]** パラメーターの値が **[!UICONTROL big]**）の場合、以下の画像が表示されます。

![](assets/social_webapp_017.png)

ユーザーがあまり重要でない顧客（**[!UICONTROL app_data]** パラメーターの値が **[!UICONTROL small]**）の場合、以下の画像が表示されます。

![](assets/social_webapp_016.png)

この事例を再作成するために、以下の要素で構成された Web アプリケーションを作成しました。

* 「**[!UICONTROL アプリケーションパラメーター]**」フィールドに基づく&#x200B;**[!UICONTROL テスト]**&#x200B;アクティビティ。
* 「**[!UICONTROL アプリケーションパラメーター]**」フィールドの値に応じて表示する画像を含む 2 つのページ。

![](assets/social_webapp_018.png)

## ファンデータを取得するには？{#how-to-acquire-fan-data-}

>[!IMPORTANT]
>
>[Facebook アプリケーションの作成](../../social/using/creating-a-facebook-application.md)で説明されている設定手順に従います。

この例では、Facebook ユーザーと連絡を取り、ユーザーがプロフィール情報を共有できるようにする方法を示します。見込み客を獲得したいと思っている企業の例を見てみましょう。Facebook のページでコンテストを企画し、見込み客を惹きつけます。

ユーザーが「**[!UICONTROL App03]**」タブをクリックするたびに、コンテストに参加するかどうかを尋ねます。

![](assets/social_webapp_fb_000.png)

コンテストに参加すると決めたら、ユーザーにプロフィール情報を共有するよう提案します。

![](assets/social_webapp_021.png)

情報の共有に同意すると、以下の画面が表示されます。

![](assets/social_webapp_022.png)

この事例を作成するために、以下の要素を含む Web アプリケーションを作成しました。

* **[!UICONTROL テスト]**&#x200B;アクティビティ
* 3 つのページ
* **[!UICONTROL アクセス制御]**&#x200B;アクティビティ
* **[!UICONTROL プリロード]**&#x200B;アクティビティ
* **[!UICONTROL 保存]**&#x200B;アクティビティ
* **[!UICONTROL 終了]**&#x200B;アクティビティ

![](assets/social_webapp_019.png)

### テストアクティビティ {#test-activity}

**[!UICONTROL テスト]**&#x200B;アクティビティは、**[!UICONTROL ID]** および「**[!UICONTROL アプリケーションパラメーター]**」フィールドに基づきます。

![](assets/social_webapp_023.png)

3 つの分岐で構成されています。

* **[!UICONTROL 識別子（UID）が空]**：識別子は、ユーザーが既に情報の共有に同意している場合にのみ、Facebook によって転送されます。**[!UICONTROL テスト]**&#x200B;アクティビティの最初の分岐では、参加したことのないユーザー（つまり、空の ID を持つユーザー）にのみコンテストを利用できるようにします。
* **[!UICONTROL アプリケーションパラメーターが「thanks」に等しい]**：Facebook に関連する表示エラーを回避するために、Web アプリケーションのエンドページは、**[!UICONTROL thanks]** 値を使用する **[!UICONTROL app_data]** パラメーターが追加された Facebook アプリケーションの URL を指します（詳しくは、[終了アクティビティ](#end-activity)を参照）。2 つ目の分岐では、ユーザーが 1 つ目の分岐の&#x200B;**[!UICONTROL 終了]**&#x200B;アクティビティからアクセスしたか（およびコンテストに参加したか）どうかを調べて、「ありがとうございます」メッセージを表示できます。追加の URL パラメーターの使用について詳しくは、[設定を Facebook アプリケーションに転送するには？](#how-to-forward-settings-to-a-facebook-application-)を参照してください。
* **[!UICONTROL デフォルトの分岐]**：ユーザーが前日に既にコンテストに参加している（ID が既に入力されている）場合（アプリケーションパラメーターが **[!UICONTROL thanks]** とは異なる）は、既に参加済みであることを示すページが表示されます。

### コンテストページ {#competition-page}

Facebook に関連する表示エラーを回避するには、コンテストページの「**[!UICONTROL ウィンドウ]**」フィールドで「**[!UICONTROL メインウィンドウ]**」または「**[!UICONTROL 上部ウィンドウで]**」を選択する必要もあります。

![](assets/social_webapp_028.png)

### アクセス制御アクティビティ {#access-control-activity}

**[!UICONTROL アクセス制御]**&#x200B;アクティビティを使用すると、ユーザーがコンテストに参加する際に Facebook 権限リクエストページを表示できます。ユーザーが情報の共有に同意した場合、プリロード時に復元されます。詳しくは、[プリロードアクティビティ](#pre-loading-activity)を参照してください。

Web アプリケーションを作成する際に事前に外部アカウントを入力した場合（[Facebook タイプの Web アプリケーションの作成](../../social/using/creating-a-facebook-application.md#creating-a-facebook-type-web-application)を参照）は、アクティビティを編集する必要はありません。そうでない場合は、「**[!UICONTROL アプリケーション]**」フィールドに移動し、Facebook アプリケーションにリンクされた外部アカウントを選択します。

![](assets/social_webapp_024.png)

### プリロードアクティビティ {#pre-loading-activity}

プリロードに使用するデータソースを選択します。

* **[!UICONTROL マーケティングデータベース]**：このオプションを使用すると、Adobe Campaign データベースを介してデータをプリロードできます。
* **[!UICONTROL Facebook]**：このオプションを使用すると、Facebook を使用してデータをプリロードできます。

![](assets/social_webapp_029.png)

**マーケティングデータベース**

このオプションを使用すると、訪問者テーブルに存在するプロフィールのデータを復元できます。検証は、ユーザーが Facebook アプリケーションタブをクリックする際に復元された外部 Facebook ID に基づいて実行されます。**[!UICONTROL プリロード]**&#x200B;アクティビティの後にフォームを追加すると、データベース内の情報を含むフィールドがプリロードされます。

![](assets/social_webapp_030.png)

>[!NOTE]
>
>Adobe Campaign データベースを介したデータのプリロードについて詳しくは、[この節](../../web/using/publishing-a-web-form.md#pre-loading-the-form-data)を参照してください。

**Facebook**

このオプションを使用すると、保存を考慮して、ユーザーが共有に同意した Facebook のプロフィール情報を収集するように定義できます。

![](assets/social_webapp_025.png)

「**[!UICONTROL データベース情報]**」オプションを使用すると、以下のデータを収集できます。

* **[!UICONTROL 外部 ID]**：ユーザー ID
* **[!UICONTROL 性別]**：ユーザーの性別
* **[!UICONTROL 検証済み]**：このフィールドは、ユーザーが検証済み Facebook アカウントを持っているかどうかを指定します。
* **[!UICONTROL 姓名]**：ユーザーの姓名
* **[!UICONTROL 名]**：ユーザーの名
* **[!UICONTROL 姓]**：ユーザーの姓
* **[!UICONTROL 言語]**：ユーザーの言語

また、該当するボックスをオンにすることで、プロフィール写真、友達のリスト、E メールアドレス、誕生日、興味、場所を収集することもできます。

「**[!UICONTROL OK]**」をクリックする前に、「**[!UICONTROL Facebook 利用条件に同意します。]**」チェックボックスをオンにします。

>[!NOTE]
>
>「**[!UICONTROL 個人情報]**」セクションの 1 つ以上のチェックボックスをオンにすると、Facebook 権限リクエスト画面に、このデータのアクセスリクエストが自動的に表示されます。
>
>選択した情報を収集するには、ユーザーが情報を共有することに同意する必要があります。
>
>両方のタイプのプリロード（Adobe Campaign 経由および Facebook 経由）が必要な場合は、2 つのプリロードボックスを順々に追加します。

### 保存アクティビティ {#save-activity}

**[!UICONTROL 保存]**&#x200B;アクティビティでは、訪問者テーブルの以前のステージで収集した情報を保存できます。

訪問者テーブルに既にプロフィールが存在する場合、そのデータは収集された新しいデータで更新されます。

データベースにプロフィールが存在せず、Facebook ユーザーの E メールアドレスが収集されている場合、訪問者テーブルに訪問者が作成されます。

![](assets/social_webapp_026.png)

1. 「**[!UICONTROL 訪問者作成フォルダー]**」フィールドで、プロフィールを作成するフォルダーを選択します。Facebook タイプの Web アプリケーションの場合、デフォルトの作成フォルダーは **[!UICONTROL Visitors]** です。
1. 「**[!UICONTROL 紐付けモード]**」フィールドで、使用する紐付けモードを選択します。

   * **[!UICONTROL 自動]**：紐付けは、E メール、姓、名、誕生日に基づいておこなわれます。
   * **[!UICONTROL 手動]**：1 つ以上の紐付けキーを選択してください。
   * **[!UICONTROL なし]**：紐付けはおこなわれません。

1. 「**[!UICONTROL マッピング]**」フィールドで、紐付けを実行するスキーマを選択します。

   >[!IMPORTANT]
   >
   >配信マッピングで、「**[!UICONTROL ソーシャルネットワーク]**」タブのフィールドが正しく入力されていることを確認します。配信マッピングには、**[!UICONTROL 管理／キャンペーン管理／ターゲットマッピング]**&#x200B;ノードを使用してアクセスします。

1. 紐付けの検索フォルダーと、新しいプロフィールの作成フォルダーを選択できます。フィールドが空の場合、プロフィールが検索され、マッピングスキーマのデフォルトのフォルダーに作成されます。

### 終了アクティビティ {#end-activity}

Facebook に関連する表示エラーを回避するには、「**[!UICONTROL 外部 URL を使用]**」チェックボックスをオンにして、Facebook アプリケーションの URL を入力し、その後に **[!UICONTROL app_data]** パラメーターおよび値を入力する必要があります。この値は、**[!UICONTROL テスト]**&#x200B;アクティビティで使用され、ユーザーがコンテストに参加したかどうかを検出し、該当する場合は「ありがとうございます」メッセージを表示します。詳しくは、[テストアクティビティ](#test-activity)を参照してください。

この例では、使用する値は「**thanks**」です。

![](assets/social_webapp_027.png)

### 訪問者の詳細画面 {#details-screen-of-a-visitor}

Twitter のフォロワーと同様（[動作の仕組み](../../social/using/publishing-on-twitter.md#operating-principle)を参照）、復元した Facebook プロフィールは訪問者テーブルに保存されます。訪問者のリストを表示するには、**[!UICONTROL プロファイルとターゲット／訪問者]**&#x200B;ノードに移動します。

プロフィール情報の共有に同意する各 Facebook の見込み客が、訪問者のリストに追加されます。**[!UICONTROL プリロード]**&#x200B;アクティビティで「**[!UICONTROL 友達]**」チェックボックスがオンになっている場合（[プリロードアクティビティ](#pre-loading-activity)を参照）、友達も追加されます。

![](assets/social_webapp_037.png)

訪問者の詳細ウィンドウの「**[!UICONTROL 概要]**」セクションでは、**[!UICONTROL 新しい連絡先]**&#x200B;指標に対して 2 つの状態が考えられます。

![](assets/social_webapp_038.png)

緑色のチェックマークが表示されている場合、その訪問者は他の受信者と紐付けられていなかったことを意味します。この場合、受信者のリストに新しいプロフィールが作成されます。

![](assets/social_webapp_039.png)

赤色のバツ印は、その訪問者が受信者と紐付けられていることを意味します。「**[!UICONTROL 受信者]**」フィールドの右側の拡大鏡をクリックすると、一致する受信者が表示されます。

![](assets/social_webapp_040.png)

該当する場合は、受信者の詳細ウィンドウに移動して、一致する訪問者を表示します。「**[!UICONTROL その他]**」タブを選択し、「**[!UICONTROL Web ID]**」セクションで訪問者の名前をダブルクリックします。

![](assets/social_webapp_041.png)

訪問者の詳細ページの&#x200B;**[!UICONTROL アクティビティ]**&#x200B;画面には、以下の情報が含まれています。

* 「Open Graph」タイプのファンアクティビティ：再生した音楽、視聴済み動画、既読記事、インストールされたアプリケーションの推測（Deezer、Spotify、Dailymotion、Yahoo ニュースなど）

   ![](assets/social_facebook_activities.png)

* Adobe Campaign から送信された配信の後にファンによって追加された「いいね！」およびコメント
* ファンによって「いいね！」されたページ
* ファンによるチェックイン

   ![](assets/social_facebook_checkins.png)

   >[!NOTE]
   >
   >Adobe Campaign でファンのチェックインを収集するには、サービス設定画面の「**[!UICONTROL 購読]**」ボタンをクリックする必要があります。詳しくは、[外部アカウントの設定](../../social/using/creating-a-facebook-application.md#configuring-external-accounts)を参照してください。

## Facebook プロフィールデータを使用したフォームのフィールドのプリロード方法 {#how-to-pre-load-the-fields-of-a-form-using-facebook-profile-data}

**[!UICONTROL ソーシャルマーケティング]**&#x200B;アプリケーションを使用すると、Facebook のプロフィール情報を使用してフィールドをプリロードするためのボタンをフォームに追加できます。このオプション（すべての Web アプリケーションテンプレート（**[!UICONTROL ページ]**&#x200B;タイプのアクティビティ）で使用できます）について詳しくは、[この節](../../web/using/static-elements-in-a-web-form.md#inserting-html-content)を参照してください。

![](assets/social_webapp_035.png)

>[!NOTE]
>
>この機能を使用する前に、Facebook アプリケーションと **[!UICONTROL Facebook Connect]** タイプの外部アカウントを作成する必要があります。詳しくは、[外部アカウントの設定](../../social/using/creating-a-facebook-application.md#configuring-external-accounts)を参照してください。

