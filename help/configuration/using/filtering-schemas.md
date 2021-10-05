---
product: campaign
title: フィルタリングスキーマ
description: フィルタリングスキーマ
audience: configuration
content-type: reference
topic-tags: editing-schemas
exl-id: 009bed25-cd35-437c-b789-5b58a6d2d7c6
source-git-commit: bd9f035db1cbad883e1f27fe901e34dfbc9c1229
workflow-type: tm+mt
source-wordcount: '411'
ht-degree: 0%

---

# フィルタースキーマ{#filtering-schemas}

![](../../assets/v7-only.svg)

## システムフィルター {#system-filters}

権限に応じて、特定のユーザーに対するスキーマアクセスをフィルタリングできます。 システムフィルターを使用すると、スキーマで詳しく説明されているエンティティの読み取りおよび書き込み権限を、**readAccess** および **writeAccess** パラメーターを使用して管理できます。

>[!NOTE]
>
>この制限は、技術者以外のユーザーにのみ適用されます。関連する権限を持つテクニカルユーザーや、ワークフローを使用して、データを取得および更新できます。

* **readAccess**:は、スキーマデータへの読み取り専用アクセスを提供します。

   **警告**  — リンクされたすべてのテーブルに同じ制限を設定する必要があります。この設定は、パフォーマンスに影響を与える可能性があります。

* **writeAccess**:は、スキーマデータへの書き込みアクセスを提供します。

これらのフィルタは、スキーマのメインの **要素** レベルで入力し、次の例に示すように、アクセスを制限するために形成できます。

* WRITE 権限の制限

   ここでは、フィルターを使用して、ADMINISTRATION 権限を持たないオペレーターのスキーマに対する WRITE 権限を無効にします。 つまり、このスキーマで記述されたエンティティに対する書き込み権限を持つのは管理者だけです。

   ```
   <sysFilter name="writeAccess">      
    <condition enabledIf="hasNamedRight('admin')=false" expr="FALSE"/>    
   </sysFilter>
   ```

* 読み取りおよび書き込み権限の制限：

   ここでは、フィルターを使用して、すべてのオペレーターに対して、スキーマに対する読み取りと書き込みの両方の権限を許可しません。 式「$(loginId)」で表される **内部** アカウントのみ！=0&quot;の場合は、これらの権限を持ちます。

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

## Protectの組み込みスキーマ {#protecting-built-in-schemas}

デフォルトでは、組み込みスキーマは、管理権限を持つオペレーターの書き込み権限でのみアクセスできます。

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

>[!IMPORTANT]
>
>**xtk:sessionInfo** スキーマの読み取りおよび書き込み権限は、Adobe Campaignインスタンスの内部アカウントからのみアクセスできます。

## 組み込みスキーマのシステムフィルターの変更 {#modifying-system-filters-of-built-in-schemas}

古いバージョンとの互換性の問題によりデフォルトで保護されている、標準搭載のスキーマのシステムフィルターを変更することもできます。

>[!NOTE]
>
>ただし、Adobeでは、最適なセキュリティを確保するために、デフォルトのパラメーターを変更しないことをお勧めします。

1. 対象のスキーマの拡張を作成するか、既存の拡張を開きます。
1. 元のスキーマと同じ下にあるフィルターの適用を削除するには、メイン要素に子要素 **`<sysfilter name="<filter name>" _operation="delete"/>`** を追加します。
1. 必要に応じて、[ システムフィルター ](#system-filters) で説明されているように、新しいフィルターを追加できます。
