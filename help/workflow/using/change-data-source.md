---
title: データソースの変更
description: データソースを変更アクティビティの詳細を説明します
audience: workflow
content-type: reference
topic-tags: targeting-activities
source-git-commit: 9fc4add3f12e3f06b031c4969bd8409c67e4359e
workflow-type: tm+mt
source-wordcount: '326'
ht-degree: 60%

---

# データソースの変更 {#change-data-source}

>[!NOTE]
>
> **[!UICONTROL データソース]**&#x200B;を変更アクティビティは、**[!UICONTROL 外部データへのアクセス(Federated Data Access)]**&#x200B;パッケージでのみ使用できます。 Adobe Campaign Classicの組み込みパッケージについて詳しくは、この[ページ](../../installation/using/installing-campaign-standard-packages.md)を参照してください。

「**[!UICONTROL データソースを変更]**」アクティビティを使用すると、ワークフロー&#x200B;**[!UICONTROL 作業用テーブル]**&#x200B;のデータソースを変更できます。これにより、FDA、FFDA、ローカルデータベースなど、様々なデータソースにわたって、より柔軟にデータを管理できます。

**[!UICONTROL 作業用テーブル]**を使用すると、Adobe Campaign Classicワークフローでデータを処理し、ワークフローアクティビティとデータを共有できます。
デフォルトでは、**[!UICONTROL 作業用テーブル]**&#x200B;は、クエリ対象のデータのソースと同じデータベースに作成されます。

例えば、クラウドデータベースに格納された&#x200B;**[!UICONTROL プロファイル]**&#x200B;テーブルに対してクエリを実行する場合、同じクラウドデータベースに&#x200B;**[!UICONTROL 作業用テーブル]**を作成します。
これを変更するには、「**[!UICONTROL データソースを変更]**」アクティビティを追加して、**[!UICONTROL 作業用テーブル]**&#x200B;に別のデータソースを選択します。

なお、「**[!UICONTROL データソースを変更]**」アクティビティを使用する場合、ワークフローの実行を続行するには、クラウドデータベースに戻す必要があります。

「**[!UICONTROL データソースを変更]**」アクティビティを使用するには：

1. ワークフローを作成します。

1. 「**[!UICONTROL クエリ]**」アクティビティでターゲット受信者にクエリを実行します。

   **[!UICONTROL クエリ]**&#x200B;アクティビティの詳細については、この[ページ](../../workflow/using/query.md#creating-a-query)を参照してください。

1. 「**[!UICONTROL ターゲティング]**」タブから、「**[!UICONTROL データソースを変更]**」アクティビティを追加します。

   ![](assets/change-data-source.png)

1. **[!UICONTROL データソース]**&#x200B;を変更アクティビティをダブルクリックして、「**[!UICONTROL デフォルトのデータソース]**」を選択します。

   クエリの結果を含んだ作業用テーブルが、デフォルトの PostgreSQL データベースに移動されます。

   ![](assets/change-data-source_2.png)

1. 「**[!UICONTROL アクション]**」タブから、「**[!UICONTROL JavaScript コード]**」アクティビティをドラッグ＆ドロップして、作業用テーブルに対して単一の操作を実行します。

   **[!UICONTROL JavaScriptコード]**&#x200B;アクティビティについて詳しくは、 [JavaScriptコードと高度なJavaScriptコード](../../workflow/using/sql-code-and-javascript-code.md#javascript-code)のページを参照してください。

1. 別の「**[!UICONTROL データソースを変更]**」アクティビティを追加して、クラウドデータベースに戻します。

1. アクティビティをダブルクリックし、「**[!UICONTROL アクティブなFDA外部アカウント]**」を選択してから、対応する&#x200B;**[!UICONTROL 外部データベース]**&#x200B;外部アカウントを選択します。

   ![](assets/change-data-source_3.png)

1. これで、ワークフローを開始できます。
