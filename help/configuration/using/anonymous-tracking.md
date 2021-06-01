---
product: campaign
title: 匿名トラッキング
description: 匿名トラッキング
audience: configuration
content-type: reference
topic-tags: setting-up-web-tracking
exl-id: f251eb21-0f3c-4b46-927a-57a3291e705f
source-git-commit: 98d646919fedc66ee9145522ad0c5f15b25dbf2e
workflow-type: tm+mt
source-wordcount: '209'
ht-degree: 6%

---

# 匿名トラッキング{#anonymous-tracking}

Adobe Campaignでは、収集したWebトラッキング情報を、受信者がサイトを匿名で閲覧する際に受信者とリンクできます。 ユーザーがWebサイトのタグ付きページを閲覧すると、この閲覧情報が収集され、Adobe Campaignから送信されるEメールをクリックすると、その情報が識別され、自動的にその情報にリンクされます。

>[!IMPORTANT]
>
>Webサイト上で匿名トラッキングを設定すると、大量のトラッキングログの収集をトリガー化できるので、データベースの操作に影響を与えます。 慎重に設定します。\
>トラッキングログは、トラッキングデータがパージされるまで、データベースに保存されます。 デプロイウィザードを使用して、パージの頻度を設定します。 詳細については、[このセクション](../../installation/using/deploying-an-instance.md#purging-data)を参照してください。

インスタンスで匿名Webトラッキングを有効にするには、次の要素を設定する必要があります。

* 永続的なCookie(**uuid230**)を配置するには、トラッキングサーバーの&#x200B;**serverConf.xml**&#x200B;ファイルの&#x200B;**redirection**&#x200B;要素の&#x200B;**trackWebVisitors**&#x200B;パラメーターを&#39;**true**&#39;に設定する必要があります。サイトにアクセスした不明なインターネットユーザーのブラウザー。
* デプロイウィザードのトラッキング設定画面で、**匿名Webトラッキング**&#x200B;モードを選択する必要があります。

   ![](assets/webtracking_anonymous_set.png)

* Webフォームと調査は、トラッキングサーバー上でパブリッシュおよび実行する必要があります。 デプロイウィザードで、一致するオプションを選択する必要があります。

   ![](assets/webtracking_publication_set_for_webapps.png)
