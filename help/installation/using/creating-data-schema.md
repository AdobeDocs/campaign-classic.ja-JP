---
product: campaign
title: 外部データベースへのアクセス
description: 外部データベースへのアクセス
audience: platform
content-type: reference
topic-tags: connectors
exl-id: 8702499b-1700-4d1f-a0e0-f7a9dfb4b88f
source-git-commit: d2d0ff575edbee18febb5ec895fcec1e0ae34de7
workflow-type: tm+mt
source-wordcount: '192'
ht-degree: 52%

---

# データスキーマの作成 {#creating-the-data-schema}

![](../../assets/v7-only.svg)

外部データベースにスキーマを作成する手順は、次のとおりです。

1. データスキーマのリストの上にある「**[!UICONTROL 新規]**」ボタンをクリックし、「**[!UICONTROL 外部データにアクセス]**」を選択します。

   ![](assets/wf_new_schema_fda.png)

1. スキーマに **[!UICONTROL 名前空間]** と **[!UICONTROL 名前]** を入力し、**[!UICONTROL 外部アカウント]** を選択して、データベースへの接続を有効にします。 これにより、外部データベースで使用できるテーブルのリストにアクセスできます。

   ![](assets/wf_new_schema_select_table_fda.png)

1. 「**[!UICONTROL テーブル名]**」フィールドから、収集するデータが格納されているテーブルを選択します。

   Snowflakeを使用すると、データベース・ユーザーに正しい権限が付与されている場合は、ここでビューを選択できます。 ビューを使用する場合、Adobe Campaignは XML スキーマを自動的に生成できないので、自分で作成する必要があります。 ビューの詳細については、[Snowflakeのドキュメント ](https://docs.snowflake.com/en/user-guide/views-introduction.html) を参照してください。

   ![](assets/wf_new_schema_select_table_fda.png)

1. 「**[!UICONTROL OK]**」をクリックして確定します。Adobe Campaign では選択したテーブルの構造が自動的に検出され、論理スキーマが生成されます。Adobe Campaign はリンクを生成しません。

1. 「**[!UICONTROL 保存]**」をクリックして作成を確定します。

   >[!CAUTION]
   >
   >Snowflake を使用する場合、プライマリキーは必須です。

   ![](assets/wf_new_schema_generate_fda.png)

テーブルをマッピングすると（標準または FDA マッピング）、インデックスが自動的に作成されます。
