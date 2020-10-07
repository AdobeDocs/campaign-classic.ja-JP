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
translation-type: tm+mt
source-git-commit: 70b143445b2e77128b9404e35d96b39694d55335
workflow-type: tm+mt
source-wordcount: '333'
ht-degree: 12%

---


# スキーマの拡張{#extending-a-schema}

>[!IMPORTANT]
>
>次の組み込みスキーマの中には、拡張できないものがあります。主に、次の設定が定義されます。\
>**dataSource=&quot;file&quot;** and **mappingType=&quot;xmlFile&quot;**.\
>次のスキーマは拡張できません。 **xtk:entityBackupNew**, **xx:entityBackup** Entity **,** xx:entityBackupEntityオリジナルxtk:form **************************************************original xtk:schemasksck:ntk, ntk:nl監視， nltkリモートntarkingnms:user AgentAgentRules nuser nuser xtk:connections  xtk:tk:db xtk:db xlist initlist initlest nustk:xfusion netuserAgentRules neturs netures ners ners netures nets nes ners nets nets nets nets ners nets nets nets nets xts接続接続接続接続xtk接続xtk接続xtk接続接続xtk接続接続xtk接続xtk接続xtk接続接続xtk接続xtk接続xtk接続xtktktktktk接続接続tktk接続接続xtk接続tk接続接続接続xtk：接続xtk接続**, **, xx:nav**, **xx:queryDef**, **queryDef:resourceMenuメニュー， tk:tkスキーマ,**********************xtkスクリプトtk:tk tk stktk tk skema tk sql skem.xsql xstrings.xs
>このリストは完全なものではありません。

既存のスキーマを拡張する方法は2つあります。

1. ソーススキーマを直接変更する。
1. 同じ名前で別の名前空間を持つ別のスキーマを作成する。 メリットは、元のスキーマを変更する必要なく、テーブルを拡張できる点です。

   スキーマのルート要素には、拡張するスキーマの名前を値として持つ **extendedSchema** 属性が含まれている必要があります。

   拡張スキーマには独自のスキーマがありません。ソーススキーマから生成されたスキーマは、拡張スキーマのフィールドに入力されます。

   >[!IMPORTANT]
   >
   >アプリケーションの組み込みスキーマを変更することはできません。スキーマの拡張メカニズムを変更することはできません。 標準スキーマを変更すると、今後アプリケーションのアップグレード時にスキーマが更新されなくなり、これは、Adobe Campaignの使用に誤りを生じさせる可能性があります。

   **例**:nms: **受信者** スキーマの拡張。

   ```
   <srcSchema extendedSchema="nms:recipient" name="recipient" namespace="cus">
     <element name="recipient">
       <attribute name="code" label="Branch code" type="long"/>
     </element>
   </srcSchema>
   ```

   nms: **受信者** 拡張スキーマに、拡張スキーマに入力された次のフィールドが入力されます。

   ```
   <schema dependingSchemas="cus:recipient" name="recipient" namespace="nms">
     ...
     <attribute belongsTo="cus:recipient" label="Branch code" name="code" sqlname="iCode" type="long"/>
     ...
   </schema>
   ```

   スキーマのルート要素の **dependingSchemas** 属性は、拡張スキーマの依存関係を参照します。

   フィールドの **belongsTo** 属性は、宣言されたスキーマを入力します。

>[!IMPORTANT]
>
>変更を考慮するには、スキーマを再生成する必要があります。 For more on this, refer to the [Regenerating schemas](../../configuration/using/regenerating-schemas.md) section.\
>変更がデータベースの構造に影響する場合は、更新を実行する必要があります。 詳しくは、[データベース構造の更新](../../configuration/using/updating-the-database-structure.md)の節を参照してください。

