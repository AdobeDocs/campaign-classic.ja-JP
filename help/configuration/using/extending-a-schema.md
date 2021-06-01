---
product: campaign
title: スキーマの拡張
description: スキーマの拡張方法を説明します
audience: configuration
content-type: reference
topic-tags: editing-schemas
exl-id: 6e3e666d-6ab3-4346-93ca-fb0155a4660d
source-git-commit: 98d646919fedc66ee9145522ad0c5f15b25dbf2e
workflow-type: tm+mt
source-wordcount: '333'
ht-degree: 10%

---

# スキーマの拡張{#extending-a-schema}

>[!IMPORTANT]
>
>一部の組み込みスキーマは拡張できません。主に、次の設定が定義されているものです。\
>**dataSource=&quot;file&quot;** および **mappingType=&quot;xmlFile&quot;**&#x200B;を参照してください。\
>次のスキーマは拡張できません。**xtk:entityBackupNew**、**xtk:entityBackupOriginal**、**xtk:entityOriginal**、**xtk:form**、**xtk:srcSchema**、**ncm:publishing**、**nl:monitoring**、**nms:calendar**、**nms:remoteTracking**、**nms:userAgentRules** 19/>, **xtk:builder**, **xtk:connections**, **xtk:dbInit**, **xtk:funcList**, **xtk:fusion**, **xtk:**, **xtk:navtree**, **xtk:queryDef**, **xtk:resourceMenu**, **xtk:schema**, **xtk:scriptContext**, **xtk:session**, **xtk:sqlSchema**, **xtk:strings**.
>このリストは完全なものではありません。

既存のスキーマを拡張するには、次の2つの方法があります。

1. ソーススキーマを直接変更する。
1. 同じ名前で異なる名前空間を持つ別のスキーマを作成する。 利点は、元のスキーマを変更する必要なくテーブルを拡張できることです。

   スキーマのルート要素には、拡張するスキーマの名前を値として持つ&#x200B;**extendedSchema**&#x200B;属性が含まれている必要があります。

   拡張機能スキーマには、独自のスキーマはありません。ソーススキーマから生成されたスキーマは、拡張スキーマのフィールドで入力されます。

   >[!IMPORTANT]
   >
   >アプリケーションの組み込みスキーマではなく、スキーマ拡張メカニズムを変更することはできません。 標準スキーマを変更すると、今後アプリケーションのアップグレード時にスキーマが更新されなくなり、これは、Adobe Campaignの使用に誤作動を引き起こす可能性があります。

   **例**: **nms:** recipientschemaの拡張。

   ```
   <srcSchema extendedSchema="nms:recipient" name="recipient" namespace="cus">
     <element name="recipient">
       <attribute name="code" label="Branch code" type="long"/>
     </element>
   </srcSchema>
   ```

   **nms:recipient**&#x200B;拡張スキーマに、拡張スキーマ内のフィールドが入力されます。

   ```
   <schema dependingSchemas="cus:recipient" name="recipient" namespace="nms">
     ...
     <attribute belongsTo="cus:recipient" label="Branch code" name="code" sqlname="iCode" type="long"/>
     ...
   </schema>
   ```

   スキーマのルート要素の&#x200B;**dependingSchemas**&#x200B;属性は、拡張スキーマの依存関係を参照します。

   フィールドの&#x200B;**bengsTo**&#x200B;属性が、宣言先のスキーマを設定します。

>[!IMPORTANT]
>
>変更を考慮するには、スキーマを再生成する必要があります。 詳しくは、[スキーマの再生成](../../configuration/using/regenerating-schemas.md)の節を参照してください。\
>変更がデータベースの構造に影響を与える場合は、更新を実行する必要があります。 詳しくは、[データベース構造の更新](../../configuration/using/updating-the-database-structure.md)の節を参照してください。
