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
>**dataSource=&quot;file&quot;** および **mappingType=&quot;xmlFile&quot;**.\
>次のスキーマは拡張できません。 **xtk:entityBackupNew**, **xtk:entityBackupOriginal**, **xtk:entityOriginal**, **xtk:form**, **xtk:srcSchema**, **ncm:publishing**, **nl：モニタリング**, **nms:calendar**, **nms:remoteTracking**, **nms:userAgentRules**, **xtk:builder**, **xtk:connections**, **xtk:dbInit**, **xtk:funcList**, **xtk:fusion**, **xtk: jst**, **xtk:navtree**, **xtk:queryDef**, **xtk:resourceMenu**, **xtk:schema**, **xtk:scriptContext**, **xtk:session**, **xtk:sqlSchema**, **xtk:strings**.
>このリストは網羅的ではありません。

既存のスキーマを拡張するには、次の 2 つの方法があります。

1. ソーススキーマを直接変更します。
1. 同じ名前で別の名前空間を持つ別のスキーマを作成します。 この利点は、元のスキーマを変更しなくてもテーブルを拡張できることです。

   スキーマのルート要素には、次を含める必要があります **extendedSchema** 値として拡張するスキーマの名前を持つ属性。

   拡張スキーマに独自のスキーマはありません。ソーススキーマから生成されたスキーマは、拡張スキーマのフィールドで入力されます。

   >[!IMPORTANT]
   >
   >アプリケーションのビルトインスキーマではなく、スキーマ拡張メカニズムを変更できます。 標準スキーマを変更すると、今後アプリケーションのアップグレード時にスキーマが更新されなくなり、これは、Adobe Campaignの使用における誤動作の原因となる可能性があります。

   **例**：の拡張 **nms:recipient** スキーマ。

   ```
   <srcSchema extendedSchema="nms:recipient" name="recipient" namespace="cus">
     <element name="recipient">
       <attribute name="code" label="Branch code" type="long"/>
     </element>
   </srcSchema>
   ```

   この **nms:recipient** 拡張スキーマは、拡張スキーマに入力されたフィールドで入力されます。

   ```
   <schema dependingSchemas="cus:recipient" name="recipient" namespace="nms">
     ...
     <attribute belongsTo="cus:recipient" label="Branch code" name="code" sqlname="iCode" type="long"/>
     ...
   </schema>
   ```

   この **dependingSchemas** スキーマのルート要素の属性は、拡張スキーマの依存関係を参照します。

   この **belonesTo** フィールドの属性が、宣言されているスキーマに入力されます。

>[!IMPORTANT]
>
>変更を考慮するには、スキーマを再生成する必要があります。 詳しくは、[このページ](../../configuration/using/regenerating-schemas.md)を参照してください。\
>変更がデータベースの構造に影響を与える場合は、更新を実行する必要があります。 詳しくは、[このページ](../../configuration/using/updating-the-database-structure.md)を参照してください。
