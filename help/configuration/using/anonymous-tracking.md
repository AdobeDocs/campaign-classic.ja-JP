---
product: campaign
title: 匿名トラッキング
description: 匿名トラッキングの設定方法を説明します
feature: Configuration, Instance Settings
role: Developer
exl-id: f251eb21-0f3c-4b46-927a-57a3291e705f
source-git-commit: 9f5205ced6b8d81639d4d0cb6a76905a753cddac
workflow-type: tm+mt
source-wordcount: '212'
ht-degree: 5%

---

# 匿名トラッキング{#anonymous-tracking}

Adobe Campaignを使用すると、受信者がサイトを匿名で参照した際に、収集した Web トラッキング情報を受信者にリンクできます。 ユーザーが web サイトのタグ付きページを閲覧すると、この閲覧情報が収集されます。これにより、Adobe Campaignから送信されたメールをクリックすると、ユーザーが識別され、情報が自動的にリンクされます。

>[!IMPORTANT]
>
>匿名トラッキングを web サイトに設定すると、大量のトラッキングログの収集がトリガーとなるので、データベースの処理に影響を与える可能性があります。 慎重に設定してください。\
>トラッキングログは、トラッキングデータがパージされるまでデータベースに保存されます。 デプロイメントウィザードを使用して、パージ頻度を設定します。 詳しくは、[この節](../../installation/using/deploying-an-instance.md#purging-data)を参照してください。

インスタンスで匿名 Web トラッキングを有効にするには、次の要素を設定する必要があります。

* トラッキングサーバーの **serverConf.xml** ファイルの **redirection** 要素の **trackWebVisitors** パラメーターを「**true**」に設定して、サイトを訪問した不明なインターネットユーザーのブラウザーに永続的な Cookie （**uuid230**）を配置する必要があります。
* デプロイメントウィザードのトラッキング設定画面で、「**匿名 Web トラッキング**」モードを選択する必要があります。

  ![](assets/webtracking_anonymous_set.png)

* Web フォームは、トラッキングサーバーで公開して実行する必要があります。 一致するオプションは、配置ウィザードで選択する必要があります。

  ![](assets/webtracking_publication_set_for_webapps.png)
