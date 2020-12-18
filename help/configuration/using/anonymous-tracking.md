---
solution: Campaign Classic
product: campaign
title: 匿名トラッキング
description: 匿名トラッキング
audience: configuration
content-type: reference
topic-tags: setting-up-web-tracking
translation-type: tm+mt
source-git-commit: 972885c3a38bcd3a260574bacbb3f507e11ae05b
workflow-type: tm+mt
source-wordcount: '209'
ht-degree: 6%

---


# 匿名トラッキング{#anonymous-tracking}

Adobe Campaignを使用すると、収集したWeb トラッキング情報を受信者がサイトを匿名で閲覧する際に、ユーザーにリンクできます。 ユーザがWebサイトのタグ付きページを閲覧すると、この閲覧情報が収集されるので、Adobe Campaignから送信される電子メールをクリックすると、ユーザが識別され、情報が自動的にWebサイトにリンクされます。

>[!IMPORTANT]
>
>Webサイトで匿名トラッキングを設定すると、大量のトラッキングログの収集がトリガーされ、データベースの操作に影響を与える可能性があります。 注意して設定します。\
>トラッキングログは、追跡データが削除されるまでデータベースに保存されます。 展開ウィザードを使用して、削除の頻度を設定します。 詳しくは、[こちらの節](../../installation/using/deploying-an-instance.md#purging-data)を参照してください。

インスタンスで匿名Web トラッキングを有効にするには、次の要素を設定する必要があります。

* トラッキングサーバーの&#x200B;**serverConf.xml**&#x200B;ファイルの&#x200B;**redirection**&#x200B;要素の&#x200B;**trackWebVisitors**&#x200B;パラメーターは、永続的なcookie(**uuid230**)を配置するために&#39;**true**&#39;に設定する必要があります。サイトを訪問した未知のインターネットユーザーのブラウザー。
* デプロイメントウィザードの追跡設定画面で、**匿名Web トラッキング**&#x200B;モードを選択する必要があります。

   ![](assets/webtracking_anonymous_set.png)

* Web フォームと調査は、トラッキングサーバー上で公開し、実行する必要があります。 配置ウィザードで、一致するオプションを選択する必要があります。

   ![](assets/webtracking_publication_set_for_webapps.png)

