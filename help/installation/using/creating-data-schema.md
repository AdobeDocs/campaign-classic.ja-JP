---
product: campaign
title: FDA 用のデータスキーマの作成
description: FDA のデータスキーマを作成する方法を説明します
feature: Installation, Instance Settings, Federated Data Access
exl-id: 8702499b-1700-4d1f-a0e0-f7a9dfb4b88f
source-git-commit: b666535f7f82d1b8c2da4fbce1bc25cf8d39d187
workflow-type: tm+mt
source-wordcount: '195'
ht-degree: 47%

---

# データスキーマの作成 {#creating-the-data-schema}



外部データベースにスキーマを作成する手順は、次のとおりです。

1. データスキーマのリストの上にある「**[!UICONTROL 新規]**」ボタンをクリックし、「**[!UICONTROL 外部データにアクセス]**」を選択します。

   ![](assets/wf_new_schema_fda.png)

1. を入力 **[!UICONTROL 名前空間]** および  **[!UICONTROL 名前]** スキーマのを選択し、 **[!UICONTROL 外部アカウント]** これにより、データベースへの接続が可能になります。 これにより、外部データベースで使用できるテーブルのリストにアクセスできます。

   ![](assets/wf_new_schema_select_table_fda.png)

1. から **[!UICONTROL テーブル名]** フィールドで、収集するデータを含むテーブルを選択します。

   データベース・ユーザーに正しい権限が付与されている場合は、Snowflakeを使用してビューを選択できます。 なお、ビューを使用する場合、Adobe Campaignでは XML スキーマを自動生成できません。ユーザー自身で作成する必要があります。 ビューの詳細については、次を参照してください。 [Snowflakeドキュメント](https://docs.snowflake.com/en/user-guide/views-introduction.html).

   ![](assets/wf_new_schema_select_table_fda.png)

1. 「**[!UICONTROL OK]**」をクリックして確定します。Adobe Campaign では選択したテーブルの構造が自動的に検出され、論理スキーマが生成されます。Adobe Campaign はリンクを生成しません。

1. 「**[!UICONTROL 保存]**」をクリックして作成を確定します。

   >[!CAUTION]
   >
   >Snowflake を使用する場合、プライマリキーは必須です。

   ![](assets/wf_new_schema_generate_fda.png)

テーブルをマッピングすると（標準または FDA マッピング）、インデックスが自動的に作成されます。
