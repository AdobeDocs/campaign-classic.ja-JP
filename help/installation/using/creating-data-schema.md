---
product: campaign
title: FDA のデータスキーマの作成
description: FDA のデータスキーマを作成する方法を説明します
exl-id: 8702499b-1700-4d1f-a0e0-f7a9dfb4b88f
source-git-commit: 40da5774c8a6a228992c4aa400e2d9924215611e
workflow-type: tm+mt
source-wordcount: '199'
ht-degree: 46%

---

# データスキーマの作成 {#creating-the-data-schema}

![](../../assets/v7-only.svg)

外部データベースにスキーマを作成する手順は、次のとおりです。

1. データスキーマのリストの上にある「**[!UICONTROL 新規]**」ボタンをクリックし、「**[!UICONTROL 外部データにアクセス]**」を選択します。

   ![](assets/wf_new_schema_fda.png)

1. を入力します。 **[!UICONTROL 名前空間]** および  **[!UICONTROL 名前]** スキーマのを選択し、 **[!UICONTROL 外部アカウント]** データベースへの接続を有効にします。 これにより、外部データベースで使用できるテーブルのリストにアクセスできます。

   ![](assets/wf_new_schema_select_table_fda.png)

1. 次の **[!UICONTROL テーブル名]** 「 」フィールドで、収集するデータが格納されているテーブルを選択します。

   Snowflakeを使用すると、データベース・ユーザーに正しい権限が付与されている場合に、ここでビューを選択できます。 ビューを使用する場合、Adobe Campaignで XML スキーマを自動的に生成することはできないので、自分で作成する必要があります。 ビューについて詳しくは、 [Snowflake文書](https://docs.snowflake.com/en/user-guide/views-introduction.html).

   ![](assets/wf_new_schema_select_table_fda.png)

1. 「**[!UICONTROL OK]**」をクリックして確定します。Adobe Campaign では選択したテーブルの構造が自動的に検出され、論理スキーマが生成されます。Adobe Campaign はリンクを生成しません。

1. 「**[!UICONTROL 保存]**」をクリックして作成を確定します。

   >[!CAUTION]
   >
   >Snowflake を使用する場合、プライマリキーは必須です。

   ![](assets/wf_new_schema_generate_fda.png)

テーブルをマッピングすると（標準または FDA マッピング）、インデックスが自動的に作成されます。
