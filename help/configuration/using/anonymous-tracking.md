---
product: campaign
title: 匿名トラッキング
description: 匿名トラッキング
audience: configuration
content-type: reference
topic-tags: setting-up-web-tracking
exl-id: f251eb21-0f3c-4b46-927a-57a3291e705f
source-git-commit: 20509f44c5b8e0827a09f44dffdf2ec9d11652a1
workflow-type: tm+mt
source-wordcount: '207'
ht-degree: 6%

---

# 匿名トラッキング{#anonymous-tracking}

![](../../assets/v7-only.svg)

Adobe Campaignでは、収集した Web トラッキング情報を、サイトを匿名で閲覧する受信者にリンクできます。 ユーザーが Web サイトのタグ付きページを閲覧すると、この閲覧情報が収集され、Adobe Campaignから送信される E メールをクリックすると、ユーザーが識別され、情報が自動的にそのページにリンクされます。

>[!IMPORTANT]
>
>Web サイトで匿名トラッキングを設定すると、大量のトラッキングログの収集をトリガー化できるので、データベースの操作に影響を与えます。 慎重に設定します。\
>トラッキングログは、トラッキングデータがパージされるまで、データベースに保存されます。 デプロイウィザードを使用して、パージの頻度を設定します。 詳しくは、[この節](../../installation/using/deploying-an-instance.md#purging-data)を参照してください。

インスタンスで匿名 Web トラッキングを有効にするには、次の要素を設定する必要があります。

* 永続的な Cookie(**uuid230**) を配置するには、トラッキングサーバーの **serverConf.xml** ファイルの **redirection** 要素の **trackWebVisitors** パラメーターを&#39;**true**&#39;に設定する必要があります。サイトを訪問した不明なインターネットユーザーのブラウザー。
* デプロイウィザードのトラッキング設定画面で、**匿名 Web トラッキング** モードを選択する必要があります。

   ![](assets/webtracking_anonymous_set.png)

* Web フォームは、トラッキングサーバー上で発行および実行する必要があります。 デプロイウィザードで、一致するオプションを選択する必要があります。

   ![](assets/webtracking_publication_set_for_webapps.png)
