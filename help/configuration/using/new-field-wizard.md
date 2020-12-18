---
solution: Campaign Classic
product: campaign
title: 新しいフィールドウィザード
description: 新しいフィールドウィザード
audience: configuration
content-type: reference
topic-tags: editing-schemas
translation-type: tm+mt
source-git-commit: 972885c3a38bcd3a260574bacbb3f507e11ae05b
workflow-type: tm+mt
source-wordcount: '206'
ht-degree: 4%

---


# 新しいフィールドウィザード{#new-field-wizard}

**[!UICONTROL ツール/詳細/追加新しいフィールド]**&#x200B;からアクセスできるウィザードを使用すると、1つ以上のフィールドをデータベースのテーブルに追加できます。

ウィザードを検証すると、拡張するテーブルの拡張スキーマが更新され、SQLスクリプトが起動してデータベースの物理構造が変更されます。

このアシスタントの利点は、データスキーマの構造を知る必要なく、すばやくフィールドを追加できることです。

主な短所は、データおよび拡張するプロパティの制限です。

ウィザードの画面には、次の手順が含まれます。

1. 最初のページでは、拡張するスキーマの名前と、変更を保存する拡張スキーマの名前空間を入力できます。

   ![](assets/d_ncs_integration_schema_addfield.png)

1. 次のページでは、追加するフィールドのプロパティを入力できます。

   ![](assets/d_ncs_integration_schema_addfield2.png)

1. 変更を確認するには、「**[!UICONTROL 完了]**」ボタンをクリックします。

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
>デフォルトでは、追加されたフィールドは、プロパティ&#x200B;**user**（値が「true」の）を使用して宣言されます。 これにより、「treeEdit」型のコントロール（「Input Form」を参照）を使用して、拡張スキーマの入力フォーム内のフィールドを表示および編集できます。

