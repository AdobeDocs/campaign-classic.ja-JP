---
product: campaign
title: 匿名トラッキング
description: 匿名トラッキングの設定方法を説明します
feature: Configuration, Instance Settings
role: Data Engineer, Developer
exl-id: f251eb21-0f3c-4b46-927a-57a3291e705f
source-git-commit: b666535f7f82d1b8c2da4fbce1bc25cf8d39d187
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

* この **trackWebVisitors** のパラメーター **リダイレクト** の要素 **serverConf.xml** トラッキングサーバーのファイルは「」に設定する必要があります&#x200B;**true**&#39;。永続的な Cookie を配置します（**uuid230**）を選択します。
* この **匿名 Web トラッキング** デプロイメントウィザードのトラッキング設定画面でモードを選択する必要があります。

  ![](assets/webtracking_anonymous_set.png)

* Web フォームは、トラッキングサーバーで公開して実行する必要があります。 一致するオプションは、配置ウィザードで選択する必要があります。

  ![](assets/webtracking_publication_set_for_webapps.png)
