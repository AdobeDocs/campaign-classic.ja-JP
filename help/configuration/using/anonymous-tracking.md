---
title: 匿名トラッキング
seo-title: 匿名トラッキング
description: 匿名トラッキング
seo-description: null
page-status-flag: never-activated
uuid: 21ba3657-eabf-4228-9fc0-e72712bf8fe7
contentOwner: sauviat
products: SG_CAMPAIGN/CLASSIC
audience: configuration
content-type: reference
topic-tags: setting-up-web-tracking
discoiquuid: 2d2c6ae9-4dba-4b82-a25e-eda65a49572d
translation-type: tm+mt
source-git-commit: 70b143445b2e77128b9404e35d96b39694d55335
workflow-type: tm+mt
source-wordcount: '211'
ht-degree: 7%

---


# 匿名トラッキング{#anonymous-tracking}

Adobe Campaignを使用すると、収集したWeb トラッキング情報を受信者がサイトを匿名で閲覧する際に、ユーザーにリンクできます。 ユーザがWebサイトのタグ付きページを閲覧すると、この閲覧情報が収集されるので、Adobe Campaignから送信される電子メールをクリックすると、ユーザが識別され、情報が自動的にWebサイトにリンクされます。

>[!IMPORTANT]
>
>Webサイトで匿名トラッキングを設定すると、大量のトラッキングログの収集がトリガーされ、データベースの操作に影響を与える可能性があります。 注意して設定します。\
>トラッキングログは、追跡データが削除されるまでデータベースに保存されます。 展開ウィザードを使用して、削除の頻度を設定します。 詳しくは、[この節](../../installation/using/deploying-an-instance.md#purging-data)を参照してください。

インスタンスで匿名Web トラッキングを有効にするには、次の要素を設定する必要があります。

* トラッキングサーバーの **リダイレクト** 要素のtrackWebVisitors **** パラメーターは、インターネット訪問者不明のブラウザーに恒久的なcookieを置くように、 ************ trueCookieを設定する必要があります。
* デプロイメントウィザードの追跡設定画面で **匿名Web トラッキング** (Anonymous Mode)を選択する必要があります。

   ![](assets/webtracking_anonymous_set.png)

* Web フォームと調査は、トラッキングサーバー上で公開し、実行する必要があります。 配置ウィザードで、一致するオプションを選択する必要があります。

   ![](assets/webtracking_publication_set_for_webapps.png)

