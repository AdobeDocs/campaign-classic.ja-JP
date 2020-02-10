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
index: y
internal: n
snippet: y
translation-type: tm+mt
source-git-commit: 579329d9194115065dff2c192deb0376c75e67bd

---


# データベース構造の更新{#updating-the-database-structure}

スキーマに対して行われた変更を適用するには、データベース更新ウィザードを起動します。 このウィザードには、を使用してアクセスできま **[!UICONTROL Tools > Advanced > Update database structure]** す。 データベースの物理構造が論理記述と一致するかどうかを確認し、SQL更新スクリプトを実行します。

![](assets/d_ncs_integration_schema_update.png)

データベース内のモジュールが自動的に入力され、アクティブ化されます。

![](assets/d_ncs_integration_schema_update_select.png)

とのオ **[!UICONTROL Add stored procedures]** プシ **[!UICONTROL Import initialization data]** ョンを使用して、初期SQLスクリプトと、データベースの作成時に実行されるデータパッケージを起動します。

外部データパッケージからデータのセットを読み込むことができます。 これを行うには、パッケージ **[!UICONTROL Import a package]** のXMLファイルを選択して入力します。

次の手順に従って、データベース更新SQLスクリプトを表示します。

![](assets/d_ncs_integration_schema_update2.png)

>[!NOTE]
>
>これは編集フィールドにあり、SQLコードを削除または追加するために変更できます。

次に、データベースの更新を起動します。

![](assets/d_ncs_integration_schema_update3.png)

