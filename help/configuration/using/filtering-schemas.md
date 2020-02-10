---
title: スキーマのフィルタ
seo-title: スキーマのフィルタ
description: スキーマのフィルタ
seo-description: null
page-status-flag: never-activated
uuid: 04a90785-3084-42fd-85af-77bc28687579
contentOwner: sauviat
products: SG_CAMPAIGN/CLASSIC
audience: configuration
content-type: reference
topic-tags: editing-schemas
discoiquuid: 64d4c5b8-db0b-4287-8d30-4bf09878a401
index: y
internal: n
snippet: y
translation-type: tm+mt
source-git-commit: 1c86322fa95aee024f6c691b61a10c21a9a22eb7

---


# スキーマのフィルタ{#filtering-schemas}

## システムフィルタ {#system-filters}

権限に応じて、特定のユーザーに対するスキーマアクセスをフィルタリングできます。 システムフィルターを使用すると、readAccessパラメーターとwriteAccessパラメーターを使用して、スキーマに詳細なエンティティの読み取り権限と書き込み権限 **を管理で** きます **** 。

>[!NOTE]
>
>この制限は、技術者以外のユーザーにのみ適用されます。関連する権限を持つ技術ユーザーやワークフローを使用するユーザーは、データを取得して更新できます。

* **readAccess**:スキーマデータへの読み取り専用アクセスを提供します。

   **警告** — リンクされたすべてのテーブルに同じ制限を設定する必要があります。 この構成は、パフォーマンスに影響を与える可能性があります。

* **writeAccess**:スキーマデータへの書き込みアクセスを提供します。

これらのフィルタは、スキーマのメ **イン要素** ・レベルで入力され、次の例に示すように、アクセスを制限するために作成できます。

* WRITE権限の制限

   ここでは、このフィルタを使用して、ADMINISTRATION権限を持たない演算子のスキーマに対するWRITE権限を無効にします。 つまり、管理者のみがこのスキーマで記述されたエンティティに対する書き込み権限を持ちます。

   ```
   <sysFilter name="writeAccess">      
    <condition enabledIf="hasNamedRight('admin')=false" expr="FALSE"/>    
   </sysFilter>
   ```

* 読み取り権限と書き込み権限の制限：

   ここでは、フィルタを使用して、すべての演算子のスキーマに対するREAD権限とWRITE権限の両方を許可しません。 内部アカ **ウント** (式「$(loginId)!=0&quot;の場合は、次の権限を持ちます。

   ```
   <sysFilter name="readAccess"> 
    <condition enabledIf="$(loginId)!=0" expr="FALSE"/>
   </sysFilter>
   
   <sysFilter name="writeAccess">  
    <condition enabledIf="$(loginId)!=0" expr="FALSE"/>
   </sysFilter>
   ```

   条件 **の定義に** 、使用可能なexpr属性値はTRUEまたはFALSEです。

>[!NOTE]
>
>フィルターが指定されていない場合、すべての演算子にスキーマへの読み取りおよび書き込み権限が付与されます。

## 組み込みスキーマの保護 {#protecting-built-in-schemas}

デフォルトでは、組み込みスキーマは、管理権限を持つ演算子のWRITE権限でのみアクセスできます。

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
* xtk:schema
* xtk:scriptContext
* xtk:specFile
* xtk:sql
* xtk:sqlSchema
* xtk:srcSchema
* xtk:strings
* xtk:xslt

>[!CAUTION]
>
>xtk:sessionInfoスキーマの読み取り権限と書き込み権限は **** 、Adobe Campaignインスタンスの内部アカウントからのみアクセスできます。

## 組み込みスキーマのシステムフィルターの変更 {#modifying-system-filters-of-built-in-schemas}

そのままで、以前のバージョンとの互換性の問題によりデフォルトで保護されている、あらかじめ用意されたスキーマのシステムフィルターを変更することもできます。

>[!NOTE]
>
>ただし、最適なセキュリティを保証するために、デフォルトのパラメーターを変更しないことをお勧めします。

1. 関連するスキーマの拡張を作成するか、既存の拡張を開きます。
1. 元のスキーマと同 **`<sysfilter name="<filter name>" _operation="delete"/>`** じ下にあるフィルターの適用を削除するには、メイン要素に子要素を追加します。
1. 必要に応じて、「システムフィルター」で詳しく説明した新しいフィルターを追 [加できます](#system-filters)。

