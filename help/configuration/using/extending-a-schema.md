---
product: campaign
title: スキーマの拡張
description: スキーマの拡張方法を学ぶ
badge-v7-only: label="v7" type="Informative" tooltip="Applies to Campaign Classic v7 only"
feature: Schema Extension
exl-id: 6e3e666d-6ab3-4346-93ca-fb0155a4660d
source-git-commit: 8debcd3d8fb883b3316cf75187a86bebf15a1d31
workflow-type: tm+mt
source-wordcount: '327'
ht-degree: 11%

---

# スキーマの拡張{#extending-a-schema}

>[!IMPORTANT]
>
>一部の組み込みスキーマは拡張できません。主に、次の設定が定義されているものです。\
>**dataSource=&quot;file&quot;** および **mappingType=&quot;xmlFile&quot;**.\
>次のスキーマは拡張できません。 **xtk:entityBackupNew**, **xtk:entityBackupOriginal**, **xtk:entityOriginal**, **xtk:form**, **xtk:srcSchema**, **ncm:publishing**, **nl:monitoring**, **nms:calendar**, **nms:remoteTracking**, **nms:userAgentRules**, **xtk:builder**, **xtk:connections**, **xtk:dbInit**, **xtk:funcList**, **xtk:fusion**, **xtk:jst**, **xtk:navtree**, **xtk:queryDef**, **xtk:resourceMenu**, **xtk:schema**, **xtk:scriptContext**, **xtk:session**, **xtk:sqlSchema**, **xtk:strings**.
>このリストが完全なものではありません。

既存のスキーマを拡張するには、次の 2 つの方法があります。

1. ソーススキーマを直接変更する。
1. 同じ名前で異なる名前空間を持つ別のスキーマを作成する。 利点は、元のスキーマを変更する必要なくテーブルを拡張できることです。

   スキーマのルート要素には、 **extendedSchema** 属性の値は、拡張するスキーマの名前です。

   拡張スキーマには、独自のスキーマはありません。ソーススキーマから生成されたスキーマは、拡張スキーマのフィールドで入力されます。

   >[!IMPORTANT]
   >
   >アプリケーションの組み込みスキーマではなく、スキーマ拡張メカニズムを変更することはできます。 標準スキーマを変更すると、今後アプリケーションのアップグレード時にスキーマが更新されなくなり、これは、Adobe Campaignの使用に誤作動を引き起こす可能性があります。

   **例**:拡張 **nms:recipient** スキーマ。

   ```
   <srcSchema extendedSchema="nms:recipient" name="recipient" namespace="cus">
     <element name="recipient">
       <attribute name="code" label="Branch code" type="long"/>
     </element>
   </srcSchema>
   ```

   この **nms:recipient** 拡張スキーマには、拡張スキーマに入力されたフィールドが入力されます。

   ```
   <schema dependingSchemas="cus:recipient" name="recipient" namespace="nms">
     ...
     <attribute belongsTo="cus:recipient" label="Branch code" name="code" sqlname="iCode" type="long"/>
     ...
   </schema>
   ```

   この **dependingSchemas** スキーマのルート要素の属性は、拡張スキーマへの依存関係を参照します。

   この **belongsTo** 属性をフィールドに設定すると、宣言されたスキーマに値が設定されます。

>[!IMPORTANT]
>
>変更を考慮に入れるには、スキーマを再生成する必要があります。 詳しくは、[このページ](../../configuration/using/regenerating-schemas.md)を参照してください。\
>変更がデータベースの構造に影響を与える場合は、更新を実行する必要があります。 詳しくは、[このページ](../../configuration/using/updating-the-database-structure.md)を参照してください。
