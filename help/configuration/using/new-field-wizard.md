---
product: campaign
title: 新しいフィールドアシスタント
description: 新しいフィールドアシスタント
feature: Schema Extension
role: Developer
exl-id: 2350a531-7a26-4f26-90fe-8dac0cc26605
source-git-commit: 9f5205ced6b8d81639d4d0cb6a76905a753cddac
workflow-type: tm+mt
source-wordcount: '206'
ht-degree: 4%

---

# 新しいフィールドアシスタント{#new-field-wizard}


**[!UICONTROL ツール/詳細/新しいフィールドを追加]**&#x200B;でアクセスできるアシスタントを使用すると、データベースのテーブルに1つ以上のフィールドを追加できます。

アシスタントを検証すると、拡張するテーブルの拡張スキーマが更新され、SQL スクリプトが起動して、データベースの物理構造が変更されます。

このアシスタントは、データスキーマの構造を知らなくてもフィールドを迅速に追加できるという利点があります。

主な欠点は、拡張するデータとプロパティの制限です。

アシスタント画面には、次の手順が含まれます。

1. 最初のページでは、拡張するスキーマの名前と、変更を保存する拡張スキーマの名前空間を入力できます。

   ![](assets/d_ncs_integration_schema_addfield.png)

1. 次のページでは、追加するフィールドのプロパティを入力できます。

   ![](assets/d_ncs_integration_schema_addfield2.png)

1. 変更を確認するには、「**[!UICONTROL 完了]**」ボタンをクリックします。

この例の「cus:recipient」という拡張子ファイルが自動的に作成され、対応するSQL スクリプトが実行されます。

```
<srcSchema extendedSchema="nms:recipient" label="Recipients" name="recipient"  namespace="cus">  
  <element name="recipient">    
    <attribute belongsTo="cus:recipient" dataPolicy="email" label="Email" length="80" name="email1" sqlname="sEmail1" type="string" user="true"/>  
  </element>
</srcSchema>
```

>[!NOTE]
>
>デフォルトでは、追加されたフィールドはプロパティ **user**&#x200B;で宣言されます（値は「true」）。 これにより、「treeEdit」タイプのコントロール（「入力フォーム」を参照）を使用して、拡張スキーマの入力フォームでフィールドを表示および編集できます。
