---
product: campaign
title: 匿名トラッキング
description: 匿名トラッキングの設定方法を説明します
feature: Configuration, Instance Settings
badge-v7-only: label="v7" type="Informative" tooltip="Campaign Classicv7 にのみ適用"
exl-id: f251eb21-0f3c-4b46-927a-57a3291e705f
source-git-commit: 3a9b21d626b60754789c3f594ba798309f62a553
workflow-type: tm+mt
source-wordcount: '219'
ht-degree: 5%

---

# 匿名トラッキング{#anonymous-tracking}

Adobe Campaignでは、収集した Web トラッキング情報を、サイトを匿名で閲覧する受信者とリンクできます。 ユーザーが Web サイトのタグ付きページを閲覧すると、この閲覧情報が収集され、Adobe Campaignから送信された E メールをクリックすると、その情報が識別され、情報が自動的にリンクされます。

>[!IMPORTANT]
>
>Web サイトで匿名トラッキングを設定すると、大量のトラッキングログのトリガーが作成され、データベースの操作に影響を与える可能性があります。 慎重に設定します。\
>トラッキングログは、トラッキングデータがパージされるまで、データベースに保存されます。 デプロイウィザードを使用して、パージの頻度を設定します。 詳しくは、[この節](../../installation/using/deploying-an-instance.md#purging-data)を参照してください。

インスタンスで匿名 Web トラッキングを有効にするには、次の要素を設定する必要があります。

* The **trackWebVisitors** のパラメーター **リダイレクト** の要素 **serverConf.xml** トラッキングサーバーのファイルを「 」に設定する必要があります&#x200B;**true**&#39;，永続的な Cookie を配置する (**uuid230**) を使用します。
* The **匿名 Web トラッキング** デプロイウィザードのトラッキング設定画面で、モードを選択する必要があります。

  ![](assets/webtracking_anonymous_set.png)

* Web フォームは、トラッキングサーバー上で公開および実行する必要があります。 デプロイウィザードで、一致するオプションを選択する必要があります。

  ![](assets/webtracking_publication_set_for_webapps.png)
