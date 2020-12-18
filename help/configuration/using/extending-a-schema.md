---
solution: Campaign Classic
product: campaign
title: スキーマの拡張
description: スキーマの拡張方法を学ぶ
audience: configuration
content-type: reference
topic-tags: editing-schemas
translation-type: tm+mt
source-git-commit: 972885c3a38bcd3a260574bacbb3f507e11ae05b
workflow-type: tm+mt
source-wordcount: '333'
ht-degree: 10%

---


# スキーマの拡張{#extending-a-schema}

>[!IMPORTANT]
>
>次の組み込みスキーマの中には、拡張できないものがあります。主に、次の設定が定義されます。\
>**dataSource=&quot;file&quot;** および **mappingType=&quot;xmlFile&quot;**。\
>次のスキーマは拡張できません。**xtk:entityBackupNew**、**xtk:entityBackupOriginal**、**xtk:entityOriginal**、**xtk:form**、**xtk:srcSchema**、&lt;a10>ncm:publishing **,** nl:monitoring **,** nms:calendar **,** nms:remoteTracking **,** nms:userAgentRules a19/>, **xtk:builder**, **xtk:connections**, **xtk:dbInit**, **xtk:funcList**, **xtk:fusion**, **xtk:**, **xtk:navtree**, **xtk:queryDef**, **xtk:resourceMenu**, **xtk:スキーマ**、**xtk:scriptContext**、**xtk:session**、**xtk:sqlSchema**、**xtk:strings**。****
>このリストは完全なものではありません。

既存のスキーマを拡張する方法は2つあります。

1. ソーススキーマを直接変更する。
1. 同じ名前で別の名前空間を持つ別のスキーマを作成する。 メリットは、元のスキーマを変更する必要なく、テーブルを拡張できる点です。

   スキーマのルート要素には、拡張するスキーマの名前を値として持つ&#x200B;**extendedSchema**&#x200B;属性を含める必要があります。

   拡張スキーマには独自のスキーマがありません。ソーススキーマから生成されたスキーマは、拡張スキーマのフィールドに入力されます。

   >[!IMPORTANT]
   >
   >アプリケーションの組み込みスキーマを変更することはできません。スキーマの拡張メカニズムを変更することはできません。 標準スキーマを変更すると、今後アプリケーションのアップグレード時にスキーマが更新されなくなり、これは、Adobe Campaignの使用に誤りを生じさせる可能性があります。

   **例**:nms: **recipientschemaの拡張** 。

   ```
   <srcSchema extendedSchema="nms:recipient" name="recipient" namespace="cus">
     <element name="recipient">
       <attribute name="code" label="Branch code" type="long"/>
     </element>
   </srcSchema>
   ```

   **nms:受信者**&#x200B;拡張スキーマに、拡張スキーマに入力されたフィールドが入力されます。

   ```
   <schema dependingSchemas="cus:recipient" name="recipient" namespace="nms">
     ...
     <attribute belongsTo="cus:recipient" label="Branch code" name="code" sqlname="iCode" type="long"/>
     ...
   </schema>
   ```

   スキーマのルート要素の&#x200B;**dependingSchemas**&#x200B;属性は、拡張スキーマの依存関係を参照します。

   フィールドの&#x200B;**belongsTo**&#x200B;属性は、宣言されたスキーマを入力します。

>[!IMPORTANT]
>
>変更を考慮するには、スキーマを再生成する必要があります。 詳しくは、「[スキーマの再生成](../../configuration/using/regenerating-schemas.md)」を参照してください。\
>変更がデータベースの構造に影響する場合は、更新を実行する必要があります。 詳しくは、[データベース構造の更新](../../configuration/using/updating-the-database-structure.md)の節を参照してください。

