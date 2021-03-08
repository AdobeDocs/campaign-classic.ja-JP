---
solution: Campaign Classic
product: campaign
title: フィルタースキーマ
description: フィルタースキーマ
audience: configuration
content-type: reference
topic-tags: editing-schemas
translation-type: tm+mt
source-git-commit: 693e38477b318ee44e0373a04d8524ddf128fe36
workflow-type: tm+mt
source-wordcount: '411'
ht-degree: 0%

---


# フィルタスキーマ{#filtering-schemas}

## システムフィルター{#system-filters}

権限に応じて、特定のスキーマに対するユーザーアクセスをフィルタリングできます。 システムフィルターを使用すると、**readAccess**&#x200B;パラメーターと&#x200B;**writeAccess**&#x200B;パラメーターを使用して、スキーマに詳細なエンティティの読み取り権限と書き込み権限を管理できます。

>[!NOTE]
>
>この制限は、技術者以外のユーザーにのみ適用されます。関連する権限を持つ技術ユーザー、またはワークフローを使用するユーザーは、データを取得して更新できます。

* **readAccess**:スキーマデータへの読み取り専用アクセスを提供します。

   **警告**  — リンクされたすべてのテーブルに同じ制限を設定する必要があります。この構成は、パフォーマンスに影響を与える可能性があります。

* **writeAccess**:スキーマデータへの書き込みアクセスを提供します。

これらのフィルターは、スキーマのメイン&#x200B;**要素**&#x200B;レベルで入力され、次の例に示すように、アクセスを制限するための要素を形成できます。

* WRITE権限の制限

   ここでは、フィルタを使用して、ADMINISTRATION権限を持たない演算子のスキーマに対するWRITE権限を許可しません。 つまり、このスキーマで記述されるエンティティに対する書き込み権限は管理者のみが持ちます。

   ```
   <sysFilter name="writeAccess">      
    <condition enabledIf="hasNamedRight('admin')=false" expr="FALSE"/>    
   </sysFilter>
   ```

* 読み取り/書き込み権限の制限：

   このフィルタは、すべての演算子に対してスキーマのREAD権限とWRITE権限の両方を許可しないために使用します。 **内部**&#x200B;アカウントのみ。式&quot;$(loginId)!=0&quot;の場合は、次の権限を持ちます。

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
>フィルターが指定されていない場合、すべての演算子には、スキーマに対する読み取りと書き込みの権限があります。

## Protect組み込みスキーマ{#protecting-built-in-schemas}

デフォルトでは、組み込みスキーマは、管理者権限を持つオペレーターのWRITE権限でのみアクセスできます。

* ncm：公開
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
* xtk:スキーマ
* xtk:scriptContext
* xtk:specFile
* xtk:sql
* xtk:sqlSchema
* xtk:srcSchema
* xtk:strings
* xtk:xslt

>[!IMPORTANT]
>
>**xtk:sessionInfo**&#x200B;スキーマの読み取り権限と書き込み権限は、Adobe Campaignインスタンスの内部アカウントからのみアクセスできます。

## 組み込みスキーマのシステムフィルターの変更{#modifying-system-filters-of-built-in-schemas}

そのまま、標準搭載されたスキーマのシステムフィルターを変更することもできます。これらのシステムは、以前のバージョンとの互換性の問題が原因で、デフォルトで保護されています。

>[!NOTE]
>
>ただし、最適なセキュリティを確保するために、Adobeではデフォルトのパラメーターを変更しないことをお勧めします。

1. 関連するスキーマの拡張機能を作成するか、既存の拡張機能を開きます。
1. メ追加イン要素内の子要素&#x200B;**`<sysfilter name="<filter name>" _operation="delete"/>`**。接触チャネルスキーマ内の同じ要素の下でフィルターの適用を削除します。
1. 必要に応じて、[システムフィルター](#system-filters)で詳しく説明しているように、新しいフィルタを追加できます。

