---
title: 新規フィールドウィザード
seo-title: 新規フィールドウィザード
description: 新規フィールドウィザード
seo-description: null
page-status-flag: never-activated
uuid: 2c8d35db-042a-47cf-a7a6-3bb63bf40d94
contentOwner: sauviat
products: SG_CAMPAIGN/CLASSIC
audience: configuration
content-type: reference
topic-tags: editing-schemas
discoiquuid: 6da65fb5-18a1-41a0-96d8-588e383f944b
index: y
internal: n
snippet: y
translation-type: tm+mt
source-git-commit: 579329d9194115065dff2c192deb0376c75e67bd

---


# 新規フィールドウィザード{#new-field-wizard}

ウィザードを使用してアクセ **[!UICONTROL Tools > Advanced > Add new fields]** スし、データベース内のテーブルに1つ以上のフィールドを追加できます。

ウィザードを検証すると、拡張するテーブルの拡張スキーマが更新され、SQLスクリプトが起動してデータベースの物理構造が変更されます。

このアシスタントには、データスキーマの構造を知る必要なく、すばやくフィールドを追加するという利点があります。

主な欠点は、拡張するデータとプロパティの制限です。

ウィザードの画面には、次の手順が含まれます。

1. 最初のページでは、拡張するスキーマの名前と、変更を保存する拡張スキーマの名前空間を入力できます。

   ![](assets/d_ncs_integration_schema_addfield.png)

1. 次のページでは、追加するフィールドのプロパティを入力できます。

   ![](assets/d_ncs_integration_schema_addfield2.png)

1. 変更を確認するには、ボタンをクリック **[!UICONTROL Finish]** します。

この例では、「cus:recipient」という拡張子ファイルが自動的に作成され、対応するSQLスクリプトが実行されます。

```
<srcSchema extendedSchema="nms:recipient" label="Recipients" name="recipient"  namespace="cus">  
  <element name="recipient">    
    <attribute belongsTo="cus:recipient" dataPolicy="email" label="Email" length="80" name="email1" sqlname="sEmail1" type="string" user="true"/>  
  </element>
</srcSchema>
```

>[!NOTE]
>
>デフォルトでは、追加されたフィールドは **user** （値「true」）プロパティで宣言されます。 これにより、「treeEdit」型のコントロール（「Input Form」を参照）を使用して、拡張スキーマの入力フォーム内のフィールドを表示および編集できます。

