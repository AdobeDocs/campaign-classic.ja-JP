---
product: campaign
title: 新しいフィールドウィザード
description: 新しいフィールドウィザード
feature: Schema Extension
role: Data Engineer, Developer
exl-id: 2350a531-7a26-4f26-90fe-8dac0cc26605
source-git-commit: b666535f7f82d1b8c2da4fbce1bc25cf8d39d187
workflow-type: tm+mt
source-wordcount: '206'
ht-degree: 4%

---

# 新しいフィールドウィザード{#new-field-wizard}


**[!UICONTROL ツール/詳細/新しいフィールドを追加]** からアクセスできるウィザードを使用すると、データベースのテーブルに 1 つ以上のフィールドを追加できます。

ウィザードを検証すると、拡張するテーブルの拡張スキーマが更新され、SQL スクリプトが起動してデータベースの物理構造が変更されます。

このウィザードには、データスキーマの構造を知る必要なく、フィールドをすばやく追加できるという利点があります。

主な欠点は、拡張するデータとプロパティが制限されることです。

ウィザード画面には、次の手順が表示されます。

1. 最初のページでは、拡張するスキーマの名前と、変更が保存される拡張スキーマの名前空間を入力できます。

   ![](assets/d_ncs_integration_schema_addfield.png)

1. 次のページでは、追加するフィールドのプロパティを入力できます。

   ![](assets/d_ncs_integration_schema_addfield2.png)

1. 変更を確定するには、「**[!UICONTROL 完了]**」ボタンをクリックします。

この例では「cus:recipient」という拡張子ファイルが自動的に作成され、対応する SQL スクリプトが実行されます。

```
<srcSchema extendedSchema="nms:recipient" label="Recipients" name="recipient"  namespace="cus">  
  <element name="recipient">    
    <attribute belongsTo="cus:recipient" dataPolicy="email" label="Email" length="80" name="email1" sqlname="sEmail1" type="string" user="true"/>  
  </element>
</srcSchema>
```

>[!NOTE]
>
>デフォルトでは、追加されたフィールドはプロパティ **user** （値「true」）で宣言されます。 これにより、「treeEdit」タイプのコントロールを使用して、拡張スキーマの入力フォームのフィールドを表示および編集できます（入力フォームを参照）。
