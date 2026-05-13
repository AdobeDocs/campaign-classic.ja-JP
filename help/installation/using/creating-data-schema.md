---
product: campaign
title: FDAのデータスキーマの作成
description: FDAのデータスキーマを作成する方法を説明します
feature: Installation, Instance Settings, Federated Data Access
exl-id: 8702499b-1700-4d1f-a0e0-f7a9dfb4b88f
TQID: https://experienceleague.adobe.com/eC7jDm92g943ymcfEQjaeevS7qzIJWJR0zCtnP2Ny7o
product_v2: id: dfc56824-e8b9-499e-85d4-21aedb507314
feature_v2: id: b82389f8-9b5e-4083-8e3b-3cef299fb8b9
subfeature_v2: id: cfc95e9b-b035-4403-a6a9-b27a8a053a37
source-git-commit: 4c295c0dabae8aba298390a3da2422a3fa1219f9
workflow-type: tm+mt
source-wordcount: 201
ht-degree: 46%

---

# データスキーマの作成 {#creating-the-data-schema}



外部データベースにスキーマを作成する手順は、次のとおりです。

1. データスキーマのリストの上にある「**[!UICONTROL 新規]**」ボタンをクリックし、「**[!UICONTROL 外部データにアクセス]**」を選択します。

   ![](assets/wf_new_schema_fda.png)

1. スキーマの&#x200B;**[!UICONTROL 名前空間]**&#x200B;と&#x200B;**[!UICONTROL 名前]**&#x200B;を入力し、データベースへの接続を有効にする&#x200B;**[!UICONTROL 外部アカウント]**&#x200B;を選択します。 これにより、外部データベースで使用できるテーブルのリストにアクセスできます。

   ![](assets/wf_new_schema_select_table_fda.png)

1. **[!UICONTROL テーブル名]** フィールドから、収集するデータを含むテーブルを選択します。

   Snowflakeでは、データベースユーザーに正しい権限が付与されている場合は、ここでビューを選択できます。 ビューを使用する場合、Adobe CampaignはXML スキーマを自動生成できませんが、自分で作成する必要があります。 ビューについて詳しくは、[Snowflake ドキュメント ](https://docs.snowflake.com/en/user-guide/views-introduction.html)を参照してください。

   ![](assets/wf_new_schema_select_table_fda.png)

1. 「**[!UICONTROL OK]**」をクリックして確定します。 Adobe Campaign では選択したテーブルの構造が自動的に検出され、論理スキーマが生成されます。 Adobe Campaign はリンクを生成しません。

1. 「**[!UICONTROL 保存]**」をクリックして作成を確定します。

   >[!CAUTION]
   >
   >Snowflake を使用する場合、プライマリキーは必須です。

   ![](assets/wf_new_schema_generate_fda.png)

テーブルをマッピングすると（標準または FDA マッピング）、インデックスが自動的に作成されます。
