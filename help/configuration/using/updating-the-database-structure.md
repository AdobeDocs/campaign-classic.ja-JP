---
product: campaign
title: データベース構造の更新
description: データベース構造の更新
feature: Configuration
role: Data Engineer, Developer
exl-id: 6c1e061b-8636-4285-8d83-97474544d252
source-git-commit: c262c27e75869ae2e4bd45642f5a22adec4a5f1e
workflow-type: tm+mt
source-wordcount: '151'
ht-degree: 55%

---

# データベース構造の更新{#updating-the-database-structure}



スキーマに加えた変更を適用するには、データベース更新ウィザードを起動します。 この機能は、**[!UICONTROL ツール／詳細／データベース構造を更新]**&#x200B;から利用できます。 データベースの物理構造が論理的な記述と一致するかどうかを確認し、SQL 更新スクリプトを実行します。

![](assets/d_ncs_integration_schema_update.png)

データベース内のモジュールが自動的に入力され、アクティブ化されます。

![](assets/d_ncs_integration_schema_update_select.png)

**[!UICONTROL ストアド プロシージャの追加]** オプションと **[!UICONTROL 初期化データのインポート]** オプションは、最初の SQL スクリプトと、データベースの作成時に実行されるデータ パッケージの起動に使用されます。

外部データパッケージから一連のデータを読み込むことができます。 それには、「**[!UICONTROL パッケージをインポート]**」を選択し、パッケージの XML ファイルを入力します。

手順に従い、データベース更新 SQL スクリプトを表示します。

![](assets/d_ncs_integration_schema_update2.png)

>[!NOTE]
>
>このスクリプトは編集フィールドにあり、編集して SQL コードを削除または追加することもできます。

次に、データベースの更新を起動します。

![](assets/d_ncs_integration_schema_update3.png)
