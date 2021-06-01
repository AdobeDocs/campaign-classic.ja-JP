---
product: campaign
title: データベース構造の更新
description: データベース構造の更新
audience: configuration
content-type: reference
topic-tags: editing-schemas
exl-id: 6c1e061b-8636-4285-8d83-97474544d252
source-git-commit: 98d646919fedc66ee9145522ad0c5f15b25dbf2e
workflow-type: tm+mt
source-wordcount: '151'
ht-degree: 49%

---

# データベース構造の更新{#updating-the-database-structure}

スキーマに対する変更を適用するには、データベース更新ウィザードを起動します。 このウィザードには、 **[!UICONTROL ツール/詳細設定/データベース構造を更新]**&#x200B;からアクセスできます。 データベースの物理構造が論理的な記述と一致するかどうかを確認し、SQL 更新スクリプトを実行します。

![](assets/d_ncs_integration_schema_update.png)

データベース内のモジュールが自動的に入力され、アクティブ化されます。

![](assets/d_ncs_integration_schema_update_select.png)

「**[!UICONTROL ストアド・プロシージャの追加]**」および「**[!UICONTROL 初期化データのインポート]**」オプションを使用して、初期SQLスクリプトと、データベースの作成時に実行されるデータ・パッケージを起動します。

外部データパッケージから一連のデータを読み込むことができます。 これをおこなうには、「**[!UICONTROL パッケージをインポート]**」を選択し、パッケージのXMLファイルを入力します。

手順に従い、データベース更新 SQL スクリプトを表示します。

![](assets/d_ncs_integration_schema_update2.png)

>[!NOTE]
>
>このスクリプトは編集フィールドにあり、編集して SQL コードを削除または追加することもできます。

次に、データベースの更新を起動します。

![](assets/d_ncs_integration_schema_update3.png)
