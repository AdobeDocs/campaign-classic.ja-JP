---
product: campaign
title: 新しいフィールドウィザード
description: 新しいフィールドウィザード
badge-v7-only: label="v7" type="Informative" tooltip="Applies to Campaign Classic v7 only"
feature: Schema Extension
exl-id: 2350a531-7a26-4f26-90fe-8dac0cc26605
source-git-commit: 8debcd3d8fb883b3316cf75187a86bebf15a1d31
workflow-type: tm+mt
source-wordcount: '206'
ht-degree: 4%

---

# 新しいフィールドウィザード{#new-field-wizard}


ウィザードは、 **[!UICONTROL ツール/詳細設定/新しいフィールドを追加]** データベース内のテーブルに 1 つ以上のフィールドを追加できます。

ウィザードを検証すると、拡張するテーブルの拡張スキーマが更新され、SQL スクリプトが起動してデータベースの物理構造が変更されます。

このアシスタントには、データスキーマの構造を知る必要なく、すばやくフィールドを追加するというメリットがあります。

主な欠点は、拡張するデータとプロパティの制限です。

ウィザード画面には、次の手順が含まれます。

1. 最初のページでは、拡張するスキーマの名前と、変更が保存される拡張スキーマの名前空間を入力できます。

   ![](assets/d_ncs_integration_schema_addfield.png)

1. 次のページでは、追加するフィールドのプロパティを入力できます。

   ![](assets/d_ncs_integration_schema_addfield2.png)

1. 変更を確定するには、 **[!UICONTROL 完了]** 」ボタンをクリックします。

この例では、「cus:recipient」という拡張子ファイルが自動的に作成され、対応する SQL スクリプトが実行されます。

```
<srcSchema extendedSchema="nms:recipient" label="Recipients" name="recipient"  namespace="cus">  
  <element name="recipient">    
    <attribute belongsTo="cus:recipient" dataPolicy="email" label="Email" length="80" name="email1" sqlname="sEmail1" type="string" user="true"/>  
  </element>
</srcSchema>
```

>[!NOTE]
>
>デフォルトでは、追加したフィールドは、プロパティを使用して宣言されます **ユーザー** （値が「true」の場合） これにより、「treeEdit」タイプのコントロール（入力フォームを参照）を使用して、拡張スキーマの入力フォーム内のフィールドを表示および編集できます。
