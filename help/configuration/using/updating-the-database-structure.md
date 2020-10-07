---
title: データベース構造の更新
seo-title: データベース構造の更新
description: データベース構造の更新
seo-description: null
page-status-flag: never-activated
uuid: 084dcc7b-f890-4dff-a322-c9a8f1d614b8
contentOwner: sauviat
products: SG_CAMPAIGN/CLASSIC
audience: configuration
content-type: reference
topic-tags: editing-schemas
discoiquuid: b82ae459-30b5-4a1c-91cc-5c7b8f128333
translation-type: tm+mt
source-git-commit: 70b143445b2e77128b9404e35d96b39694d55335
workflow-type: tm+mt
source-wordcount: '155'
ht-degree: 10%

---


# データベース構造の更新{#updating-the-database-structure}

データベースに行った変更を適用するには、スキーマの更新ウィザードを起動します。 このウィザードにアクセスするには、 **[!UICONTROL ツール/詳細/データベース構造を更新を選択します]** 。 データベースの物理構造が論理的な記述と一致するかどうかを確認し、SQL更新スクリプトを実行します。

![](assets/d_ncs_integration_schema_update.png)

データベース内のモジュールが自動的に入力され、アクティブ化されます。

![](assets/d_ncs_integration_schema_update_select.png)

初期SQLスクリプ **[!UICONTROL トとデータベースの作成時に実行されるデータパッケージを起動するには、]** ストアドプロシージャ **[!UICONTROL (stored procedures)と]** インポート初期化データ(Import initialization data)の各オプションを使用します。

外部データパッケージから一連のデータを読み込むことができます。 これを行うには、「パッケージの **[!UICONTROL 読み込み]** 」を選択し、パッケージのXMLファイルを入力します。

次の手順に従い、データベース更新SQLスクリプトを表示します。

![](assets/d_ncs_integration_schema_update2.png)

>[!NOTE]
>
>これは編集フィールドにあり、SQLコードを削除または追加するために変更できます。

次に、データベースの更新を起動します。

![](assets/d_ncs_integration_schema_update3.png)

