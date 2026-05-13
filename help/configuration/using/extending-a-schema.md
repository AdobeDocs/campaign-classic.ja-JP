---
product: campaign
title: スキーマの拡張
description: スキーマの拡張方法を学ぶ
role: Developer
feature: Schema Extension
exl-id: 6e3e666d-6ab3-4346-93ca-fb0155a4660d
TQID: https://experienceleague.adobe.com/w-Pe9dOgxIRB0KnOggStMDqzaNkCFGsh-5sOISc-t2E
product_v2: id: dfc56824-e8b9-499e-85d4-21aedb507314
feature_v2: id: b82389f8-9b5e-4083-8e3b-3cef299fb8b9
subfeature_v2: id: a72a22e0-8c8d-4019-ba42-3f2644aa91a3id: cfc95e9b-b035-4403-a6a9-b27a8a053a37
role_v2: id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
source-git-commit: 4c295c0dabae8aba298390a3da2422a3fa1219f9
workflow-type: tm+mt
source-wordcount: 304
ht-degree: 12%

---

# スキーマの拡張{#extending-a-schema}

>[!IMPORTANT]
>
>一部の組み込みスキーマは拡張できません。主に、次の設定が定義されているスキーマです。\
>**dataSource=&quot;file&quot;**&#x200B;および&#x200B;**mappingType=&quot;xmlFile&quot;**。\
>次のスキーマは拡張できません：**xtk:entityBackupNew**、**xtk:entityBackupOriginal**、**xtk:entityOriginal**、**xtk:form**、**xtk:srcSchema**、**ncm:publishing**、**nl:monitoring**、**nms:calendar**、**nms:remoteTracking**、**nms:userAgentRules**、**xtk:builder**、**xtk:connections**、**xtk:dbInit**、**xtk:funcList**、**xtk:fusion**、**xtk: jst**、**xtk:navtree**、**xtk:queryDef**、**xtk:resourceMenu**、**xtk:scriptContext**、**** xtk :sqlSchema**、** xtk :strings**。:schema****:session**
>このリストは網羅的ではありません。

既存のスキーマを拡張するには、次の2つの方法があります。

1. ソーススキーマを直接変更する。
1. 同じ名前で異なる名前空間を持つ別のスキーマを作成しています。 この利点は、元のスキーマを変更することなくテーブルを拡張できることです。

   スキーマのルート要素には、拡張するスキーマの名前を値として持つ&#x200B;**extendedSchema**&#x200B;属性を含める必要があります。

   拡張スキーマには独自のスキーマがありません。ソーススキーマから生成されたスキーマには、拡張スキーマのフィールドが入力されます。

   >[!IMPORTANT]
   >
   >アプリケーションの組み込みスキーマを変更することはできず、スキーマ拡張メカニズムを変更することはできません。 標準スキーマを変更すると、今後アプリケーションのアップグレード時にスキーマが更新されなくなり、 これは、Adobe Campaignの使用における誤動作につながる可能性があります。

   **例**: **nms:recipient** スキーマの拡張。

   ```
   <srcSchema extendedSchema="nms:recipient" name="recipient" namespace="cus">
     <element name="recipient">
       <attribute name="code" label="Branch code" type="long"/>
     </element>
   </srcSchema>
   ```

   拡張スキーマ **nms:recipient**&#x200B;は、拡張スキーマに入力されたフィールドで入力されます。

   ```
   <schema dependingSchemas="cus:recipient" name="recipient" namespace="nms">
     ...
     <attribute belongsTo="cus:recipient" label="Branch code" name="code" sqlname="iCode" type="long"/>
     ...
   </schema>
   ```

   スキーマのルート要素の&#x200B;**dependingSchemas**&#x200B;属性は、拡張スキーマの依存関係を参照しています。

   フィールドの&#x200B;**belongsTo**&#x200B;属性は、宣言されたスキーマに入力されます。

>[!IMPORTANT]
>
>変更を考慮に入れるには、スキーマを再生成する必要があります。 詳しくは、[このページ](../../configuration/using/regenerating-schemas.md)を参照してください。\
>変更がデータベースの構造に影響を与える場合は、更新を実行する必要があります。 詳しくは、[このページ](../../configuration/using/updating-the-database-structure.md)を参照してください。
