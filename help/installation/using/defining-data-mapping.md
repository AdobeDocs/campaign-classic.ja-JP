---
solution: Campaign Classic
product: campaign
title: 外部データベースへのアクセス
description: 外部データベースへのアクセス
audience: platform
content-type: reference
topic-tags: connectors
translation-type: tm+mt
source-git-commit: 972885c3a38bcd3a260574bacbb3f507e11ae05b
workflow-type: tm+mt
source-wordcount: '189'
ht-degree: 100%

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

   「**[!UICONTROL 保存]**」ボタンをクリックし、配信マッピングの作成を開始します。リンクされているすべてのテーブルは、選択したパラメーターに基づいて自動的に作成されます。
