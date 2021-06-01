---
product: campaign
title: フィルタリングスキーマ
description: フィルタリングスキーマ
audience: configuration
content-type: reference
topic-tags: editing-schemas
exl-id: 009bed25-cd35-437c-b789-5b58a6d2d7c6
source-git-commit: 98d646919fedc66ee9145522ad0c5f15b25dbf2e
workflow-type: tm+mt
source-wordcount: '411'
ht-degree: 0%

---

# フィルタースキーマ{#filtering-schemas}

## システムフィルタ{#system-filters}

権限に応じて、特定のユーザーに対するスキーマアクセスをフィルタリングできます。 システムフィルターを使用すると、スキーマで詳細に説明されているエンティティの読み取りおよび書き込み権限を、**readAccess**&#x200B;および&#x200B;**writeAccess**&#x200B;パラメーターを使用して管理できます。

>[!NOTE]
>
>この制限は、技術以外のユーザーにのみ適用されます。関連する権限を持つ技術ユーザーや、ワークフローを使用して、データを取得および更新できます。

* **readAccess**:は、スキーマデータへの読み取り専用アクセスを提供します。

   **警告**  — リンクされたすべてのテーブルに同じ制限を設定する必要があります。この設定は、パフォーマンスに影響を与える可能性があります。

* **writeAccess**:は、スキーマデータへの書き込みアクセスを提供します。

これらのフィルターは、スキーマのメインの&#x200B;**要素**&#x200B;レベルで入力され、次の例に示すように、アクセスを制限するために形成できます。

* WRITE権限の制限

   ここでは、フィルターを使用して、管理権限のないオペレーターのスキーマに対する書き込み権限を無効にします。 つまり、管理者のみが、このスキーマで記述されたエンティティに対する書き込み権限を持ちます。

   ```
   <sysFilter name="writeAccess">      
    <condition enabledIf="hasNamedRight('admin')=false" expr="FALSE"/>    
   </sysFilter>
   ```

* 読み取りおよび書き込み権限の制限：

   ここでは、フィルターを使用して、すべてのオペレーターに対して、スキーマに対する読み取りと書き込みの両方の権限を許可しません。 式「$(loginId)!」で表される&#x200B;**内部**&#x200B;アカウントのみ。=0&quot;の場合は、次の権限が設定されます。

   ```
   <sysFilter name="readAccess"> 
    <condition enabledIf="$(loginId)!=0" expr="FALSE"/>
   </sysFilter>
   
   <sysFilter name="writeAccess">  
    <condition enabledIf="$(loginId)!=0" expr="FALSE"/>
   </sysFilter>
   ```

   条件の定義に使用できる&#x200B;**expr**&#x200B;属性値は、TRUEまたはFALSEです。

>[!NOTE]
>
>フィルターを指定しない場合、すべてのオペレーターにはスキーマに対する読み取りおよび書き込み権限が付与されます。

## Protect組み込みスキーマ{#protecting-built-in-schemas}

デフォルトでは、組み込みスキーマは、管理権限を持つオペレーターの書き込み権限でのみアクセスできます。

* ncm:publishing
* nl：監視
* nms:calendar
* xtk:builder
* xtk:connections
* xtk:dbInit
* xtk:entityBackupNew
* xtk:entityBackupOriginal
* xtk:entityOriginal
* xtk:form
* xtk:funcList
* xtk:fusion
* xtk:image
* xtk:javascript
* xtk:jssp
* xtk:jst
* xtk:navtree
* xtk:operatorGroup
* xtk:package
* xtk:queryDef
* xtk:resourceMenu
* xtk:rights
* xtk:schema
* xtk:scriptContext
* xtk:specFile
* xtk:sql
* xtk:sqlSchema
* xtk:srcSchema
* xtk:strings
* xtk:xslt

>[!IMPORTANT]
>
>**xtk:sessionInfo**&#x200B;スキーマの読み取りおよび書き込み権限は、Adobe Campaignインスタンスの内部アカウントからのみアクセスできます。

## 組み込みスキーマのシステムフィルタを変更する{#modifying-system-filters-of-built-in-schemas}

古いバージョンとの互換性の問題によりデフォルトで保護されている、標準搭載のスキーマのシステムフィルターを変更することもできます。

>[!NOTE]
>
>ただし、Adobeでは、最適なセキュリティを確保するために、デフォルトのパラメーターを変更しないことをお勧めします。

1. 関係するスキーマの拡張を作成するか、既存の拡張を開きます。
1. 元のスキーマと同じ下にあるフィルターの適用を削除する子要素&#x200B;**`<sysfilter name="<filter name>" _operation="delete"/>`**&#x200B;をメイン要素に追加します。
1. 必要に応じて、[システムフィルター](#system-filters)で説明されているように、新しいフィルターを追加できます。
