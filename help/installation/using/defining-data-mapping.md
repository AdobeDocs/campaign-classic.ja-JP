---
product: campaign
title: 外部データマッピングの定義
description: 外部データベースにデータをマッピングする方法を説明します
feature: Installation, Instance Settings
exl-id: a7253ca7-47e5-4def-849d-3ce1c9b948fb
TQID: https://experienceleague.adobe.com/9mE5BjrDg-E4FDyFFL0GVAVPof0rlSSOlzyj2zk21ag
product_v2: id: dfc56824-e8b9-499e-85d4-21aedb507314
feature_v2: id: b82389f8-9b5e-4083-8e3b-3cef299fb8b9
subfeature_v2: id: cfc95e9b-b035-4403-a6a9-b27a8a053a37
source-git-commit: 4c295c0dabae8aba298390a3da2422a3fa1219f9
workflow-type: tm+mt
source-wordcount: 195
ht-degree: 91%

---

# 外部データマッピングの定義 {#defining-data-mapping}



Adobe Campaign では、外部テーブルのデータでマッピングを定義できます。

そのためには、外部テーブルのスキーマを作成した後に、新しい配信マッピングを作成してこのテーブルのデータを配信ターゲットとして使用する必要があります。

それには、次の手順に従います。

1. 新しい配信マッピングを作成し、ターゲティングディメンション（先ほど作成したスキーマなど）を選択します。

   ![](assets/wf_new_mapping_create_fda.png)

1. 配信情報が格納されるフィールド（姓、名前、メール、住所など）を指定します。

   ![](assets/wf_new_mapping_define_join.png)

1. 拡張スキーマを識別しやすくするためのサフィックスなど、情報ストレージのパラメーターを指定します。

   ![](assets/wf_new_mapping_define_names.png)

   除外（**excludelog**）をメッセージ付き（**broadlog**）で格納するか、個々のテーブルに格納するかを選択できます。

   この配信マッピングのトラッキングを管理するかどうかを選択することもできます（**trackinglog**）。

1. 次に、考慮する拡張を選択します。 拡張タイプは、プラットフォームのパラメーターとオプション（ライセンス契約の表示）によって異なります。

   ![](assets/wf_new_mapping_define_extensions.png)

   「**[!UICONTROL 保存]**」ボタンをクリックし、配信マッピングの作成を開始します。リンクされているすべてのテーブルは、選択したパラメーターに基づいて自動的に作成されます。
