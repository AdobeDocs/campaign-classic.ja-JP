---
title: 外部データベースへのアクセス
seo-title: 外部データベースへのアクセス
description: 外部データベースへのアクセス
seo-description: null
page-status-flag: never-activated
uuid: b84359b9-c584-431d-80d5-71146d9b6854
contentOwner: sauviat
products: SG_CAMPAIGN/CLASSIC
audience: platform
content-type: reference
topic-tags: connectors
discoiquuid: dd3d14cc-5153-428d-a98a-32b46f0fe811
index: y
internal: n
snippet: y
translation-type: tm+mt
source-git-commit: 9a26ec7ed1c8463270ac9f97079f49e00d5b258e

---


# データスキーマの作成 {#creating-the-data-schema}

外部データベースにスキーマを作成する手順は、次のとおりです。

1. データスキーマ **[!UICONTROL New]** のリストの上にあるボタンをクリックし、を選択しま **[!UICONTROL Access external data]**&#x200B;す。

   ![](assets/wf_new_schema_fda.png)

1. スキーマの名前と説明を入力し、データベースへの接続を有効にする外部アカウントを選択します。これにより、外部データベースで使用できるテーブルのリストにアクセスできます。収集するデータを含むテーブルを選択します。

   ![](assets/wf_new_schema_select_table_fda.png)

1. Click **[!UICONTROL OK]** to confirm. Adobe Campaign では選択したテーブルの構造が自動的に検出され、論理スキーマが生成されます。Adobe Campaignではリンクは生成されませんのでご注意ください。

1. Click **[!UICONTROL Save]** to confirm creation.

   >[!CAUTION]
   >
   >雪片を使用する場合、主キーは必須です。

   ![](assets/wf_new_schema_generate_fda.png)

テーブルをマッピングすると（標準または FDA マッピング）、インデックスが自動的に作成されます。
