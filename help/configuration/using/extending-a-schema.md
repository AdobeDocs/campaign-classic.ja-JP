---
title: スキーマの拡張
seo-title: スキーマの拡張
description: スキーマの拡張
seo-description: null
page-status-flag: never-activated
uuid: 1767b9de-1d72-4ece-aeec-87f83862d81c
contentOwner: sauviat
products: SG_CAMPAIGN/CLASSIC
audience: configuration
content-type: reference
topic-tags: editing-schemas
discoiquuid: 1c9af980-4e6b-44dc-af61-dd284863ec7d
index: y
internal: n
snippet: y
translation-type: tm+mt
source-git-commit: e7ff12260d875b85256c8678fa8d100fd355398e

---


# スキーマの拡張{#extending-a-schema}

>[!CAUTION]
>
>一部の組み込みスキーマは拡張できません。主に、次の設定が定義されます。\
>**dataSource=&quot;file&quot;** and **mappingType=&quot;xmlFile&quot;**.\
>次のスキーマは拡張できません。xxtk:entityBackupNew ****, **xtk:entityBackupOriginal**, **xxxxxxx:entity:form** xtk:form **************************************************xtk schemasTK tk, tk cm NTK NL:NLカレンダーNNMSの監視， NNT NNT, userAgentRulesUserXtk:Connections, xtk:connections db:init init tk tk:connections .xtk:fusion xtk:**, **xxxx:navtree,** xx:queryDef **,** xxxDefリソースメニューリソースメニュー： tk **schema, schema Xscript tk tk tk tk schema tk tk schema xtk:sql sql sql sql SQL? xxxtring**, ********************?
>このリストは完全ではありません。

既存のスキーマを拡張する方法は2つあります。

1. ソーススキーマを直接変更する。
1. 同じ名前で別の名前空間を持つ別のスキーマを作成しています。 メリットは、元のスキーマを変更する必要なくテーブルを拡張できる点です。

   スキーマのルート要素には、拡張するス **キーマの名前を値として持つextendedSchema** 属性が含まれている必要があります。

   拡張スキーマに独自のスキーマがありません：ソーススキーマから生成されたスキーマは、拡張スキーマのフィールドに入力されます。

   >[!CAUTION]
   >
   >アプリケーションの組み込みスキーマを変更する代わりに、スキーマ拡張メカニズムを変更することはできません。 標準スキーマを変更すると、今後アプリケーションのアップグレード時にスキーマが更新されなくなり、これは、Adobe Campaignの使用に誤りが生じる可能性があります。

   **例**:nms:recipientスキ **ーマの拡張** 。

   ```
   <srcSchema extendedSchema="nms:recipient" name="recipient" namespace="cus">
     <element name="recipient">
       <attribute name="code" label="Branch code" type="long"/>
     </element>
   </srcSchema>
   ```

   nms:recipient **拡張スキーマに** 、拡張スキーマに入力されたフィールドが入力されます。

   ```
   <schema dependingSchemas="cus:recipient" name="recipient" namespace="nms">
     ...
     <attribute belongsTo="cus:recipient" label="Branch code" name="code" sqlname="iCode" type="long"/>
     ...
   </schema>
   ```

   スキーマ **のルート要素のdependingSchemas** 属性は、拡張スキーマの依存関係を参照します。

   フィールド **のbelongsTo** 属性は、宣言されたスキーマを入力します。

>[!CAUTION]
>
>変更を考慮するには、スキーマを再生成する必要があります。 For more on this, refer to the [Regenerating schemas](../../configuration/using/regenerating-schemas.md) section.\
>変更がデータベースの構造に影響を与える場合は、更新を実行する必要があります。 詳しくは、「データベース構造の更新 [」の節を参照してください](../../configuration/using/updating-the-database-structure.md) 。

