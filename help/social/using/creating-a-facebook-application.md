---
product: campaign
title: Facebook アプリケーションの作成
description: Facebook アプリケーションの作成
audience: social
content-type: reference
topic-tags: configuration
exl-id: 5c11bd0f-2df7-4c7f-b682-955fedf8e664
source-git-commit: b5334de18eca8fc1147ae0c42fe23a6932bf71d2
workflow-type: ht
source-wordcount: '996'
ht-degree: 100%

---

# Facebook アプリケーションの作成{#creating-a-facebook-application}

![](../../assets/v7-only.svg)

Campaign ソーシャルマーケティングモジュールでは、web アプリケーションを使用して、パーソナライズされたコンテンツを Facebook アプリケーションに表示することができるので、このソーシャルメディアを通じた見込み客の獲得が容易になります。Facebook タイプの web アプリケーションについては、その他に、[このページ](../../social/using/examples-of-facebook-apps.md)を参照してください。

>[!NOTE]
>
>また、パートナーが開発した Facebook アプリケーションと Adobe Campaign を統合することもできます。この場合、Facebook のプロファイルを取得するために Adobe Campaign の web アプリケーションを使用する必要はありません。[詳細情報](#configuring-external-accounts)。

![](assets/social_webapp_fb_000.png)

設定手順は次のとおりです。

1. 1 つまたは複数の Facebook アプリケーションを作成します。[詳細情報](../../social/using/publishing-on-facebook-walls.md#creating-a-facebook-application)
1. Facebook 権限リクエスト画面に表示される「**[!UICONTROL 利用規約]**」リンクと「**[!UICONTROL プライバシーポリシー]**」リンクを入力します。[詳細情報](#entering-the-terms-of-service-and-privacy-policy-links)
1. Facebook アプリケーションごとに、**[!UICONTROL Facebook Connect]** タイプの外部アカウントを作成します。[詳細情報](#configuring-external-accounts)
1. Facebook アプリケーションごとに、Adobe Campaign で Facebook タイプの web アプリケーションを作成します。[詳細情報](#creating-a-facebook-type-web-application)
1. Facebook ページにタブとして表示されるように Facebook アプリケーションを設定します。[詳細情報](#configuring-facebook-tabs)

## 外部アカウントの設定 {#configuring-external-accounts}

Facebook アプリケーションごとに、**[!UICONTROL Facebook Connect]** タイプの外部アカウントを作成する必要があります。

この手順では、Adobe Campaign コンソールと Facebook 管理者アカウントにアクセスする必要があります。

* **Facebook の場合**：以前に作成したアプリケーション（[https://developers.facebook.com/apps](https://developers.facebook.com/apps)）を選択し、**[!UICONTROL 設定]**／**[!UICONTROL 基本]**&#x200B;タブを選択します。

   ![](assets/social_webapp_fb_008.png)

   >[!NOTE]
   >
   >「**[!UICONTROL Facebook web ゲーム]**」セクションが表示されない場合は、ページの下部にある「**[!UICONTROL プラットフォームを追加]**」ボタンをクリックし、「**[!UICONTROL Facebook web ゲーム]**」を選択します。

* **Adobe Campaign の場合**：**[!UICONTROL 管理／プラットフォーム／外部アカウント]** を参照し、「**[!UICONTROL 新規]**」をクリックします。

   ![](assets/social_webapp_fb_005.png)

1. ラベルと内部名を入力し、「**[!UICONTROL Facebook Connect]**」タイプを選択します。

   ![](assets/social_webapp_fb_006.png)

1. アプリケーションのホスティングモード（「**[!UICONTROL パートナーがホストする]**」または「**[!UICONTROL このインスタンスでホストする]**」）を選択します。

   ![](assets/social_webapp_fb_012.png)

   **パートナーがホストするアプリケーション**

   パートナーが開発した Facebook アプリケーショを Adobe Campaign に統合することもできます。この場合、Facebook のプロフィールを取得するのに Adobe Campaign Web アプリケーションを使用する必要はありません。Facebook ユーザーがアプリケーションをインストールすると、キー（アクセストークン）が生成されます。パートナーは、Web サービスを呼び出して、このアクセストークンを Adobe Campaign に転送します。Adobe Campaign はこのトークンを使用して Facebook データベースにログオンし、アプリケーションを介してユーザーが共有するデータを収集します。

   >[!NOTE]
   >
   >Web サービスのパラメーターについて詳しくは、**`https://<Instance name>/nl/jsp/schemawsdl.jsp?schema=nms:visitor`** にある WSDL ファイルを参照してください。

   サードパーティのアプリケーションを Adobe Campaign に統合するには、Facebook の「**[!UICONTROL アプリID]**」および「**[!UICONTROL App Secret]**」フィールドの内容をコピーして、コンソールの「**[!UICONTROL アプリケーション ID]**」および「**[!UICONTROL アプリケーション秘密鍵]**」フィールドに貼り付ける必要があります。

   ![](assets/social_facebook_external_account_013.png)

   **このインスタンスでホストするアプリケーション**

   このインスタンスでアプリケーションをホストする場合（サードパーティのアプリケーションがない場合）、Adobe Campaign Web アプリケーションを使用して Facebook のプロフィールを取得する必要があります。詳しくは、[このページ](../../social/using/examples-of-facebook-apps.md)を参照してください。

   Adobe Campaign コンソールで、「**[!UICONTROL セキュアキャンバス URL]**」フィールドに含まれるアドレスをコピーし、Facebook の（「**[!UICONTROL Facebook web ゲーム]**」セクションにある）「**[!UICONTROL Facebook web ゲーム（https）]**」フィールドに貼り付けます。

   ![](assets/social_facebook_external_account_009.png)

   >[!CAUTION]
   >
   >安全でない URL は使用しないでください。

   Facebook で、「**[!UICONTROL アプリID]**」および「**[!UICONTROL App Secret]**」フィールドの内容をコピーし、コンソールの「**[!UICONTROL アプリケーション ID]**」および「**[!UICONTROL アプリケーション秘密鍵]**」フィールドに貼り付けます。

   ![](assets/social_facebook_external_account_008.png)

1. Facebook で、ページの下部にある「**[!UICONTROL 変更を保存]**」ボタンをクリックします。
1. Adobe Campaign コンソールで「**[!UICONTROL 購読]**」ボタンをクリックし、このアプリケーションを介してファンがチェックインするたびに Adobe Campaign がリアルタイムでデータを回復できるようにします。[詳細情報](../../social/using/examples-of-facebook-apps.md)

   ![](assets/social_webapp_fb_013.png)

## 「利用規約」リンクと「プライバシーポリシー」リンクの入力 {#entering-the-terms-of-service-and-privacy-policy-links}

Facebook の許可リクエスト画面に表示する&#x200B;**[!UICONTROL 利用規約]**&#x200B;および&#x200B;**[!UICONTROL プライバシーポリシー]**&#x200B;へのリンクを追加することを強くお勧めします。

![](assets/social_fb_terms_of_services_001.png)

設定手順は、以下のとおりです。

1. [https://developers.facebook.com/apps](https://developers.facebook.com/apps) のアドレスを開き、Facebook アプリケーションを選択します。
1. **[!UICONTROL 設定／「ベーシック」]**&#x200B;タブを選択し、「**[!UICONTROL プライバシーポリシーのURL]**」フィールドと「**[!UICONTROL 利用規約のURL]**」フィールドを入力します。

   ![](assets/social_fb_terms_of_services.png)

## Facebook タイプの web アプリケーションの作成 {#creating-a-facebook-type-web-application}

Adobe Campaign の Facebook アプリケーションを使用すると、パーソナライズされたコンテンツを Facebook アプリケーションに表示できます。Facebook アプリケーションごとに、Adobe Campaign で Web アプリケーションを作成する必要があります。Facebook Web アプリケーションの作成手順は、次のとおりです。

1. 「**[!UICONTROL ソーシャルネットワーク]**」タブに移動し、「**[!UICONTROL アプリケーション]**」リンクをクリックしてから、「**[!UICONTROL 作成]**」ボタンをクリックします。

   ![](assets/social_webapp_001.png)

1. リストから Facebook Web アプリケーションテンプレートを選択し、ラベルを入力します。

   ![](assets/social_webapp_002.png)

   >[!NOTE]
   >
   >デフォルトで提供される Facebook Web アプリケーションテンプレートは 4 つあります。
   >
   >* **[!UICONTROL 新規 Facebook アプリケーション]**：空のアプリケーションから開始したい場合は、このテンプレートを選択します。
   >* **[!UICONTROL 入力済みフォーム]**：フォームおよび「Facebook ログイン」ボタンを持つ Facebook アプリケーション。ユーザーは、プロフィールのデータを使用してフォームのフィールドに自動入力できます。これにより、ユーザーはすばやくフォームに記入でき、企業は高品質の情報を得ることができます。
   >* **[!UICONTROL 「キャンバスページ」の競合他社]**：画面の横幅いっぱいに表示される Facebook アプリケーション。より優れた視覚的効果をユーザーに提供します。
   >* **[!UICONTROL 「ページタブ」の競合他社]**：ブランドページのタブに完全に統合された Facebook アプリケーション。


1. 「**[!UICONTROL アプリケーション]**」フィールドに、Facebook アプリケーションにリンクされている外部アカウントを入力します。[詳細情報](#configuring-external-accounts)

   ![](assets/social_webapp_005.png)

1. 「**[!UICONTROL 編集]**」タブを選択し、web アプリケーションを編集します。[詳細情報](../../social/using/examples-of-facebook-apps.md)

   ![](assets/social_webapp_003.png)

1. Web アプリケーションが完成したら、「**[!UICONTROL ダッシュボード]**」タブを選択し、「**[!UICONTROL 公開]**」をクリックしてオンライン上に公開します。

   ![](assets/social_webapp_004.png)

## Facebook タブの設定 {#configuring-facebook-tabs}

Facebook ページにタブとして表示される Facebook アプリケーションを設定できます。それには、次の手順に従います。

1. Facebook アプリケーション（[https://developers.facebook.com/apps](https://developers.facebook.com/apps)）を選択し、**[!UICONTROL 設定／「ベーシック」]**&#x200B;タブを選択します。

   ![](assets/social_webapp_fb_008.png)

1. ページの下部にある「**[!UICONTROL プラットフォームを追加]**」ボタンをクリックし、「**[!UICONTROL ページタブ]**」を選択します。

   ![](assets/social_webapp_fb_008bis.png)

1. 「**[!UICONTROL ページタブ]**」セクションの「**[!UICONTROL ページタブ名]**」フィールドに、Facebook ページに表示するラベルを入力します。

   ![](assets/social_webapp_fb_001.png)

1. 「**[!UICONTROL セキュアページタブの URL]**」フィールドに、Web アプリケーションのパブリック URL を入力します。この URL は、Web アプリケーションの「**[!UICONTROL ダッシュボード]**」タブからアクセスできます。Facebook タイプの web アプリケーションの作成について詳しくは、[この節](#creating-a-facebook-type-web-application)を参照してください。

   ![](assets/social_webapp_fb_002.png)

1. Web アプリケーションの「**[!UICONTROL ダッシュボード]**」で、「**[!UICONTROL ページタブを追加]**」リンクをクリックします。

   ![](assets/social_webapp_fb_0010.png)

1. タブの追加先の Facebook ページを選択し、「**[!UICONTROL ページタブを追加]**」をクリックします。

   ![](assets/social_webapp_fb_0011.png)
