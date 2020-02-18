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
source-git-commit: d2758b5e81d1720a4f01a610e51c4a33995d88d1

---


# データマッピングの削除 {#defining-data-mapping}

Adobe Campaign では、外部テーブルのデータでマッピングを定義できます。

そのためには、外部テーブルのスキーマを作成した後に、新しい配信マッピングを作成してこのテーブルのデータを配信ターゲットとして使用する必要があります。

それには、次の手順に従います。

1. 新しい配信マッピングを作成し、ターゲティングディメンション（先ほど作成したスキーマなど）を選択します。

   ![](assets/wf_new_mapping_create_fda.png)

1. 配信情報が格納されるフィールド（姓、名前、E メール、住所など）を指定します。

   ![](assets/wf_new_mapping_define_join.png)

1. 拡張スキーマを識別しやすくするためのサフィックスなど、情報ストレージのパラメーターを指定します。

   ![](assets/wf_new_mapping_define_names.png)

   除外（**excludelog**）をメッセージ付き（**broadlog**）で格納するか、個々のテーブルに格納するかを選択できます。

   この配信マッピングのトラッキングを管理するかどうかを選択することもできます（**trackinglog**）。

1. 次に、考慮する拡張を選択します。拡張タイプは、プラットフォームのパラメーターとオプション（ライセンス契約の表示）によって異なります。

   ![](assets/wf_new_mapping_define_extensions.png)

   Click the **[!UICONTROL Save]** button to launch delivery mapping creation: all linked tables are created automatically based on the selected parameters.
