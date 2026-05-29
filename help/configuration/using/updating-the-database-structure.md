---
product: campaign
title: データベース構造の更新
description: データベース構造の更新
feature: Configuration
role: Developer
exl-id: 6c1e061b-8636-4285-8d83-97474544d252
TQID: https://experienceleague.adobe.com/y4P6bZcEyVIdfI4LHMivPIRVzb1Z4sV7ewISWqk29F0
product_v2:
  - id: dfc56824-e8b9-499e-85d4-21aedb507314
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
feature_v2: []
subfeature_v2: []
source-git-commit: bb41e9407ab5853b0194bb325bbf3f17bc3ea232
workflow-type: tm+mt
source-wordcount: 151
ht-degree: 64%

---

# データベース構造の更新{#updating-the-database-structure}



スキーマに加えた変更を適用するには、データベース更新アシスタントを起動します。 このアシスタント機能は、**[!UICONTROL ツール／詳細／データベース構造を更新]**&#x200B;から利用できます。 データベースの物理構造が論理的な記述と一致するかどうかを確認し、SQL 更新スクリプトを実行します。

![](assets/d_ncs_integration_schema_update.png)

データベース内のモジュールが自動的に入力され、アクティブ化されます。

![](assets/d_ncs_integration_schema_update_select.png)

**[!UICONTROL ストアド プロシージャの追加]**&#x200B;および&#x200B;**[!UICONTROL 初期化データのインポート]** オプションを使用して、データベースの作成時に実行される初期SQL スクリプトとデータ パッケージを起動します。

外部データパッケージから一連のデータを読み込むことができます。 これを行うには、**[!UICONTROL パッケージの読み込み]**&#x200B;を選択し、パッケージのXML ファイルを入力します。

手順に従い、データベース更新 SQL スクリプトを表示します。

![](assets/d_ncs_integration_schema_update2.png)

>[!NOTE]
>
>このスクリプトは編集フィールドにあり、編集して SQL コードを削除または追加することもできます。

次に、データベースの更新を起動します。

![](assets/d_ncs_integration_schema_update3.png)
