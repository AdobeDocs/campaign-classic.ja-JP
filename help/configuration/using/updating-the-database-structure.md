---
product: campaign
title: データベース構造の更新
description: データベース構造の更新
feature: Configuration
audience: configuration
content-type: reference
topic-tags: editing-schemas
exl-id: 6c1e061b-8636-4285-8d83-97474544d252
source-git-commit: 3a9b21d626b60754789c3f594ba798309f62a553
workflow-type: tm+mt
source-wordcount: '151'
ht-degree: 49%

---

# データベース構造の更新{#updating-the-database-structure}



スキーマに加えた変更を適用するには、データベース更新ウィザードを起動します。 このウィザードには、 **[!UICONTROL ツール/詳細設定/データベース構造を更新]** . データベースの物理構造が論理的な記述と一致するかどうかを確認し、SQL 更新スクリプトを実行します。

![](assets/d_ncs_integration_schema_update.png)

データベース内のモジュールが自動的に入力され、アクティブ化されます。

![](assets/d_ncs_integration_schema_update_select.png)

The **[!UICONTROL ストアドプロシージャの追加]** および **[!UICONTROL 初期化データをインポート]** オプションは、最初の SQL スクリプトと、データベースの作成時に実行されるデータパッケージを起動するために使用されます。

外部データパッケージから一連のデータを読み込むことができます。 それには、「 」を選択します。 **[!UICONTROL パッケージのインポート]** パッケージの XML ファイルを入力します。

手順に従い、データベース更新 SQL スクリプトを表示します。

![](assets/d_ncs_integration_schema_update2.png)

>[!NOTE]
>
>このスクリプトは編集フィールドにあり、編集して SQL コードを削除または追加することもできます。

次に、データベースの更新を起動します。

![](assets/d_ncs_integration_schema_update3.png)
