---
product: campaign
title: フィルタリングスキーマ
description: フィルタリングスキーマ
badge-v7-only: label="v7" type="Informative" tooltip="Applies to Campaign Classic v7 only"
exl-id: 009bed25-cd35-437c-b789-5b58a6d2d7c6
source-git-commit: 8debcd3d8fb883b3316cf75187a86bebf15a1d31
workflow-type: tm+mt
source-wordcount: '411'
ht-degree: 79%

---

# フィルタースキーマ{#filtering-schemas}

## システムフィルター {#system-filters}

権限に応じて、特定のユーザーに対するスキーマアクセスをフィルタリングできます。システムフィルターを使用すると、スキーマで詳しく説明されているエンティティの読み取りおよび書き込み権限を、**readAccess** および **writeAccess** パラメーターを使用して管理できます。

>[!NOTE]
>
>この制限は、技術者以外のユーザーにのみ適用されます。関連する権限を持つ、またはワークフローを使用するテクニカルユーザーは、データを取得および更新できます。

* **readAccess**：スキーマデータへの読み取り専用アクセスを提供します。

   **警告** - リンクされたすべてのテーブルに同じ制限を設定する必要があります。この設定は、パフォーマンスに影響を与える可能性があります。

* **writeAccess**：スキーマデータへの書き込みアクセスを提供します。

これらのフィルターは、スキーマのメイン&#x200B;**要素**&#x200B;レベルで入力し、次の例に示すように、アクセスを制限するために形成できます。

* 書き込み権限の制限

   ここでは、フィルターを使用して、管理権限を持たないオペレーターのスキーマに対する書き込み権限を無効にします。つまり、このスキーマで記述されたエンティティに対する書き込み権限を持つのは管理者だけです。

   ```
   <sysFilter name="writeAccess">      
    <condition enabledIf="hasNamedRight('admin')=false" expr="FALSE"/>    
   </sysFilter>
   ```

* 読み取りおよび書き込み権限の制限：

   ここでは、すべてのオペレーターに対して、スキーマに対する読み取りと書き込みの両方の権限を許可しないためにフィルターを使用しています。**内部**&#x200B;アカウントのみ（式「$(loginId)!=0」で表される）が、これらの権限を持っています。

   ```
   <sysFilter name="readAccess"> 
    <condition enabledIf="$(loginId)!=0" expr="FALSE"/>
   </sysFilter>
   
   <sysFilter name="writeAccess">  
    <condition enabledIf="$(loginId)!=0" expr="FALSE"/>
   </sysFilter>
   ```

   条件の定義に使用できる **expr** 属性値は、TRUE または FALSE です。

>[!NOTE]
>
>フィルターを指定しない場合、すべてのオペレーターはスキーマに対する読み取りおよび書き込み権限を持ちます。

## 組み込みスキーマの保護 {#protecting-built-in-schemas}

デフォルトでは、組み込みスキーマは、管理権限を持つオペレーターの書き込み権限でのみアクセスできます。

* ncm:publishing
* nl:monitoring
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
>**xtk:sessionInfo** スキーマの読み取りおよび書き込み権限は、Adobe Campaign インスタンスの内部アカウントからのみアクセスできます。

## 組み込みスキーマのシステムフィルターの変更 {#modifying-system-filters-of-built-in-schemas}

それでも、既製のスキーマのシステムフィルターは、古いバージョンとの互換性の問題が原因でデフォルトで保護されているので、変更できます。

>[!NOTE]
>
>ただし、Adobeでは、最適なセキュリティを確保するために、デフォルトのパラメーターを変更しないことをお勧めします。

1. 対象のスキーマの拡張を作成するか、既存の拡張を開きます。
1. 子要素を追加 **`<sysfilter name="<filter name>" _operation="delete"/>`** をメイン要素内に追加し、元のスキーマ内の同じ配下にあるフィルターの適用を削除します。
1. 必要に応じて、新しいフィルターを追加できます。詳しくは、 [システムフィルター](#system-filters).
