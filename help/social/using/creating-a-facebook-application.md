---
title: Facebook アプリケーションの作成
seo-title: Facebook アプリケーションの作成
description: Facebook アプリケーションの作成
seo-description: null
page-status-flag: never-activated
uuid: f02129b9-6f64-41ee-8b56-d85211a58f69
contentOwner: sauviat
products: SG_CAMPAIGN/CLASSIC
audience: social
content-type: reference
topic-tags: configuration
discoiquuid: c1d880bb-256e-451c-8c52-198711907f8e
translation-type: ht
source-git-commit: 70b143445b2e77128b9404e35d96b39694d55335
workflow-type: ht
source-wordcount: '1107'
ht-degree: 100%

---


# Facebook アプリケーションの作成{#creating-a-facebook-application}

Web アプリケーションのおかげで、ソーシャルマーケティングでは Facebook アプリケーションにパーソナライズしたコンテンツを表示でき、このソーシャルネットワーク経由で見込み客を獲得しやすくなります。Facebook タイプ Web アプリケーションのその他の例については、[Facebook アプリケーションの例](../../social/using/examples-of-facebook-apps.md)を参照してください。

>[!NOTE]
>
>また、パートナーが開発した Facebook アプリケーションと Adobe Campaign を統合することもできます。この場合、Adobe Campaign Web アプリケーションを使用して Facebook のプロフィールを取得する必要はありません。詳しくは、[外部アカウントの設定](#configuring-external-accounts)を参照してください。

![](assets/social_webapp_fb_000.png)

次の設定手順を実行します。

1. 1 つまたは複数の Facebook アプリケーションを作成します。詳しくは、[Facebook アプリケーションの作成](../../social/using/publishing-on-facebook-walls.md#creating-a-facebook-application)を参照してください。
1. Facebook 権限リクエスト画面に表示する&#x200B;**[!UICONTROL サービス利用条件]**&#x200B;および&#x200B;**[!UICONTROL プライバシーポリシー]**&#x200B;のリンクを入力します。詳しくは、[サービス利用条件およびプライバシーポリシーのリンクの入力](#entering-the-terms-of-service-and-privacy-policy-links)を参照してください。
1. Facebook アプリケーションごとに、**[!UICONTROL Facebook Connect]** タイプの外部アカウントを作成します。詳しくは、[外部アカウントの設定](#configuring-external-accounts)を参照してください。
1. Facebook アプリケーションごとに、Adobe Campaign で Facebook タイプの Web アプリケーションを作成します。詳しくは、[Facebook タイプ の Web アプリケーションの作成](#creating-a-facebook-type-web-application)を参照してください。
1. 各 Facebook アプリケーションが Facebook ページのタブとして表示されるように設定します。詳しくは、[Facebook タブの設定](#configuring-facebook-tabs)を参照してください。

## 外部アカウントの設定 {#configuring-external-accounts}

Facebook アプリケーションごとに、**[!UICONTROL Facebook Connect]** タイプの外部アカウントを作成する必要があります。

この手順では、Adobe Campaign コンソールおよびページ管理に使用する Facebook アカウントにログオンしているインターネットブラウザーの両方にアクセスする必要があります。

* **Facebook**：先に作成したアプリケーション（[https://developers.facebook.com/apps](https://developers.facebook.com/apps)）を選択し、**[!UICONTROL 設定]**／「**[!UICONTROL ベーシック]**」タブを選択します。

   ![](assets/social_webapp_fb_008.png)

   >[!NOTE]
   >
   >「**[!UICONTROL Facebookウェブゲーム]**」セクションが表示されない場合は、ページの下部にある「**[!UICONTROL プラットフォームを追加]**」ボタンをクリックし、「**[!UICONTROL Facebookウェブゲーム]**」を選択します。

* **Adobe Campaign**：ツリーの&#x200B;**[!UICONTROL 管理／プラットフォーム／外部アカウント]**&#x200B;ノードに移動し、「**[!UICONTROL 新規]**」をクリックします。

   ![](assets/social_webapp_fb_005.png)

1. ラベルおよび内部名を入力し、**[!UICONTROL Facebook Connect]** タイプを選択します。

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

   このインスタンスでアプリケーションをホストする場合（サードパーティのアプリケーションがない場合）、Adobe Campaign Web アプリケーションを使用して Facebook のプロフィールを取得する必要があります。詳しくは、[Facebook アプリケーションの例](../../social/using/examples-of-facebook-apps.md)を参照してください。

   Adobe Campaign コンソールで、「**[!UICONTROL セキュアキャンバス URL]**」フィールドに含まれるアドレスをコピーし、Facebook の「**[!UICONTROL Facebookウェブゲーム]**」セクションにある「**[!UICONTROL FacebookウェブゲームのURL(https)]**」フィールドに貼り付けます。

   ![](assets/social_facebook_external_account_009.png)

   >[!IMPORTANT]
   >
   >どのような状況にあっても、保護されていない URL を使用してはいけません。

   Facebook で、「**[!UICONTROL アプリID]**」および「**[!UICONTROL App Secret]**」フィールドの内容をコピーし、コンソールの「**[!UICONTROL アプリケーション ID]**」および「**[!UICONTROL アプリケーション秘密鍵]**」フィールドに貼り付けます。

   ![](assets/social_facebook_external_account_008.png)

1. Facebook で、ページの下部にある「**[!UICONTROL 変更を保存]**」ボタンをクリックします。
1. Adobe Campaign コンソールで「**[!UICONTROL 購読]**」ボタンをクリックし、このアプリケーションを介してファンがチェックインするたびに Adobe Campaign がリアルタイムでデータを取得できるようにします。詳しくは、[Facebook アプリケーションの例](../../social/using/examples-of-facebook-apps.md)を参照してください。

   ![](assets/social_webapp_fb_013.png)

## 利用規約およびプライバシーポリシーのリンクの入力 {#entering-the-terms-of-service-and-privacy-policy-links}

Facebook の許可リクエスト画面に表示する&#x200B;**[!UICONTROL 利用規約]**&#x200B;および&#x200B;**[!UICONTROL プライバシーポリシー]**&#x200B;へのリンクを追加することを強くお勧めします。

![](assets/social_fb_terms_of_services_001.png)

設定手順は、以下のとおりです。

1. [https://developers.facebook.com/apps](https://developers.facebook.com/apps) のアドレスを開き、Facebook アプリケーションを選択します。
1. **[!UICONTROL 設定／「ベーシック」]**&#x200B;タブを選択し、「**[!UICONTROL プライバシーポリシーのURL]**」フィールドと「**[!UICONTROL 利用規約のURL]**」フィールドを入力します。

   ![](assets/social_fb_terms_of_services.png)

## Facebook タイプの Web アプリケーションの作成 {#creating-a-facebook-type-web-application}

Adobe Campaign の Facebook アプリケーションを使用すると、パーソナライズされたコンテンツを Facebook アプリケーションに表示できます。Facebook アプリケーションごとに、Adobe Campaign で Web アプリケーションを作成する必要があります。Facebook Web アプリケーションの作成手順は、次のとおりです。

1. **[!UICONTROL ソーシャルネットワーク]**&#x200B;ウィンドウに移動し、「**[!UICONTROL アプリケーション]**」リンク、「**[!UICONTROL 作成]**」ボタンの順にクリックします。

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


1. 「**[!UICONTROL アプリケーション]**」フィールドに、Facebook アプリケーションにリンクされている外部アカウントを入力します。詳しくは、[外部アカウントの設定](#configuring-external-accounts)を参照してください。

   ![](assets/social_webapp_005.png)

1. 「**[!UICONTROL 編集]**」タブを選択し、Web アプリケーションを編集します。詳しくは、[Facebook アプリケーションの例](../../social/using/examples-of-facebook-apps.md)を参照してください。

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

1. 「**[!UICONTROL セキュアページタブの URL]**」フィールドに、Web アプリケーションのパブリック URL を入力します。この URL は、Web アプリケーションの「**[!UICONTROL ダッシュボード]**」タブからアクセスできます。Facebook タイプの Web アプリケーションの作成について詳しくは、「[Facebook タイプの Web アプリケーションの作成](#creating-a-facebook-type-web-application)」を参照してください。

   ![](assets/social_webapp_fb_002.png)

1. Web アプリケーションの「**[!UICONTROL ダッシュボード]**」で、「**[!UICONTROL ページタブを追加]**」リンクをクリックします。

   ![](assets/social_webapp_fb_0010.png)

1. タブの追加先の Facebook ページを選択し、「**[!UICONTROL ページタブを追加]**」をクリックします。

   ![](assets/social_webapp_fb_0011.png)

