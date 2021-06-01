---
product: campaign
title: 外部データベースへのアクセス
description: 外部データベースへのアクセス
audience: platform
content-type: reference
topic-tags: connectors
exl-id: 8702499b-1700-4d1f-a0e0-f7a9dfb4b88f
source-git-commit: 98d646919fedc66ee9145522ad0c5f15b25dbf2e
workflow-type: tm+mt
source-wordcount: '132'
ht-degree: 100%

---

# データスキーマの作成 {#creating-the-data-schema}

外部データベースにスキーマを作成する手順は、次のとおりです。

1. データスキーマのリストの上にある「**[!UICONTROL 新規]**」ボタンをクリックし、「**[!UICONTROL 外部データにアクセス]**」を選択します。

   ![](assets/wf_new_schema_fda.png)

1. スキーマの名前と説明を入力し、データベースへの接続を有効にする外部アカウントを選択します。これにより、外部データベースで使用できるテーブルのリストにアクセスできます。収集するデータを含むテーブルを選択します。

   ![](assets/wf_new_schema_select_table_fda.png)

1. 「**[!UICONTROL OK]**」をクリックして確定します。Adobe Campaign では選択したテーブルの構造が自動的に検出され、論理スキーマが生成されます。Adobe Campaign はリンクを生成しません。

1. 「**[!UICONTROL 保存]**」をクリックして作成を確定します。

   >[!CAUTION]
   >
   >Snowflake を使用する場合、プライマリキーは必須です。

   ![](assets/wf_new_schema_generate_fda.png)

テーブルをマッピングすると（標準または FDA マッピング）、インデックスが自動的に作成されます。
