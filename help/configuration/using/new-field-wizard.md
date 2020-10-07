---
title: 新しいフィールドウィザード
seo-title: 新しいフィールドウィザード
description: 新しいフィールドウィザード
seo-description: null
page-status-flag: never-activated
uuid: 2c8d35db-042a-47cf-a7a6-3bb63bf40d94
contentOwner: sauviat
products: SG_CAMPAIGN/CLASSIC
audience: configuration
content-type: reference
topic-tags: editing-schemas
discoiquuid: 6da65fb5-18a1-41a0-96d8-588e383f944b
translation-type: tm+mt
source-git-commit: 70b143445b2e77128b9404e35d96b39694d55335
workflow-type: tm+mt
source-wordcount: '209'
ht-degree: 5%

---


# 新しいフィールドウィザード{#new-field-wizard}

ツ **** ール/詳細/追加新規フィールドからアクセスできるウィザードを使用すると、データベース内のテーブルに1つ以上のフィールドを追加できます。

ウィザードを検証すると、拡張するテーブルの拡張スキーマが更新され、SQLスクリプトが起動してデータベースの物理構造が変更されます。

このアシスタントの利点は、データスキーマの構造を知る必要なく、すばやくフィールドを追加できることです。

主な短所は、データおよび拡張するプロパティの制限です。

ウィザードの画面には、次の手順が含まれます。

1. 最初のページでは、拡張するスキーマの名前と、変更を保存する拡張スキーマの名前空間を入力できます。

   ![](assets/d_ncs_integration_schema_addfield.png)

1. 次のページでは、追加するフィールドのプロパティを入力できます。

   ![](assets/d_ncs_integration_schema_addfield2.png)

1. 変更を確認するには、「 **[!UICONTROL 完了]** 」ボタンをクリックします。

この例では、「cus:受信者」と呼ばれる拡張子ファイルが自動的に作成され、対応するSQLスクリプトが実行されます。

```
<srcSchema extendedSchema="nms:recipient" label="Recipients" name="recipient"  namespace="cus">  
  <element name="recipient">    
    <attribute belongsTo="cus:recipient" dataPolicy="email" label="Email" length="80" name="email1" sqlname="sEmail1" type="string" user="true"/>  
  </element>
</srcSchema>
```

>[!NOTE]
>
>デフォルトでは、追加されたフィールドはプロパティ **user** （値が「true」）で宣言されます。 これにより、「treeEdit」型のコントロール（「Input Form」を参照）を使用して、拡張スキーマの入力フォーム内のフィールドを表示および編集できます。

