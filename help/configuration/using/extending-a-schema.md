---
product: campaign
title: スキーマの拡張
description: スキーマの拡張方法を学ぶ
role: Data Engineer, Developer
feature: Schema Extension
exl-id: 6e3e666d-6ab3-4346-93ca-fb0155a4660d
source-git-commit: b666535f7f82d1b8c2da4fbce1bc25cf8d39d187
workflow-type: tm+mt
source-wordcount: '327'
ht-degree: 11%

---

# スキーマの拡張{#extending-a-schema}

>[!IMPORTANT]
>
>一部のビルトインスキーマは、拡張できません。主に、次の設定が定義されているスキーマです。\
>**dataSource=&quot;file&quot;** および **mappingType=&quot;xmlFile&quot;**。\
>次のスキーマは拡張しないでください。**xtk:entityBackupNew**、**xtk:entityBackupOriginal**、**xtk:entityOriginal**、**xtk:form**、**xtk:srcSchema**、**ncm:publishing**、**nl:monitoring**、**nms:calendar**、**nms:remoteTracking**、**nms:userAgentRules**、**&#x200B;** **&#x200B;**&#x200B;**&#x200B;** **&#x200B;**&#x200B;**&#x200B;** **&#x200B;**&#x200B;**&#x200B;** **&#x200B;**&#x200B;**&#x200B;** **&#x200B;**&#x200B;**&#x200B;** **&#x200B;**&#x200B;**&#x200B;** **&#x200B;**&#x200B;xtk:builderconnections,
>このリストは網羅的ではありません。

既存のスキーマを拡張するには、次の 2 つの方法があります。

1. ソーススキーマを直接変更します。
1. 同じ名前で別の名前空間を持つ別のスキーマを作成します。 この利点は、元のスキーマを変更しなくてもテーブルを拡張できることです。

   スキーマのルート要素には、拡張するスキーマの名前をその値として持つ **extendedSchema** 属性が含まれている必要があります。

   拡張スキーマに独自のスキーマはありません。ソーススキーマから生成されたスキーマは、拡張スキーマのフィールドで入力されます。

   >[!IMPORTANT]
   >
   >アプリケーションのビルトインスキーマではなく、スキーマ拡張メカニズムを変更できます。 標準スキーマを変更すると、今後アプリケーションのアップグレード時にスキーマが更新されなくなり、これは、Adobe Campaignの使用における誤動作の原因となる可能性があります。

   **例**:**nms:recipient** スキーマの拡張。

   ```
   <srcSchema extendedSchema="nms:recipient" name="recipient" namespace="cus">
     <element name="recipient">
       <attribute name="code" label="Branch code" type="long"/>
     </element>
   </srcSchema>
   ```

   **nms:recipient** 拡張スキーマには、拡張スキーマ内に設定されたフィールドが入力されます。

   ```
   <schema dependingSchemas="cus:recipient" name="recipient" namespace="nms">
     ...
     <attribute belongsTo="cus:recipient" label="Branch code" name="code" sqlname="iCode" type="long"/>
     ...
   </schema>
   ```

   スキーマのルート要素の **dependingSchemas** 属性は、拡張スキーマの依存関係を参照します。

   フィールドの **belongsTo** 属性は、スキーマが宣言されている場所に入力されます。

>[!IMPORTANT]
>
>変更を考慮するには、スキーマを再生成する必要があります。 詳しくは、[このページ](../../configuration/using/regenerating-schemas.md)を参照してください。\
>変更がデータベースの構造に影響を与える場合は、更新を実行する必要があります。 詳しくは、[このページ](../../configuration/using/updating-the-database-structure.md)を参照してください。
