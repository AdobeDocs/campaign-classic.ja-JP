---
product: campaign
title: フィルタリングスキーマ
description: フィルタリングスキーマ
feature: Custom Resources
role: Developer
exl-id: 009bed25-cd35-437c-b789-5b58a6d2d7c6
source-git-commit: 9f5205ced6b8d81639d4d0cb6a76905a753cddac
workflow-type: tm+mt
source-wordcount: '387'
ht-degree: 61%

---

# フィルタースキーマ{#filtering-schemas}

## システムフィルター {#system-filters}

権限に応じて、特定のユーザーに対するスキーマアクセスをフィルタリングできます。 システムフィルターを使用すると、スキーマで詳しく説明されているエンティティの読み取りおよび書き込み権限を、**readAccess** および **writeAccess** パラメーターを使用して管理できます。

>[!NOTE]
>
>この制限は、技術者以外のユーザーにのみ適用されます。関連する権限を持つ、またはワークフローを使用するテクニカルユーザーは、データを取得および更新できます。

* **readAccess**：スキーマデータへの読み取り専用アクセスを提供します。

  **警告** - リンクされたすべてのテーブルに同じ制限を設定する必要があります。 この設定は、パフォーマンスに影響を与える可能性があります。

* **writeAccess**：スキーマデータへの書き込みアクセスを提供します。

これらのフィルターは、スキーマのメイン&#x200B;**要素**&#x200B;レベルで入力し、次の例に示すように、アクセスを制限するために形成できます。

* 書き込み権限の制限

  ここでは、フィルターを使用して、管理権限を持たないオペレーターのスキーマに対する書き込み権限を無効にします。 つまり、このスキーマで記述されたエンティティに対する書き込み権限を持つのは管理者だけです。

  ```
  <sysFilter name="writeAccess">      
   <condition enabledIf="hasNamedRight('admin')=false" expr="FALSE"/>    
  </sysFilter>
  ```

* 読み取りおよび書き込み権限の制限：

  ここでは、すべてのオペレーターに対して、スキーマに対する読み取りと書き込みの両方の権限を許可しないためにフィルターを使用しています。 式「$（loginId）!=0」で表される&#x200B;**internal** アカウントのみが、これらの権限を持ちます。

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

## ビルトインのスキーマの保護 {#protecting-built-in-schemas}

デフォルトでは、ビルトインのスキーマは、管理権限を持つオペレーターの書き込み権限でのみアクセスできます。

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
>**xtk:sessionInfo** スキーマの読み取り権限と書き込み権限には、Adobe Campaign インスタンスの内部アカウントのみがアクセスできます。

## ビルトインのスキーマのシステムフィルターの変更 {#modifying-system-filters-of-built-in-schemas}

古いバージョンとの互換性の問題により、デフォルトで保護されている、すぐに使用できるスキーマのシステムフィルターを変更することもできます。

>[!NOTE]
>
>ただし、最適なセキュリティを保証するために、Adobeではデフォルトのパラメーターを変更しないことをお勧めします。

1. 関連するスキーマの拡張機能を作成するか、既存の拡張機能を開きます。
1. メイン要素に子要素&#x200B;**`<sysfilter name="<filter name>" _operation="delete"/>`**&#x200B;を追加し、元のスキーマの同じ下のフィルターの適用を削除します。
1. 必要に応じて、新しいフィルターを追加できます（[ システムフィルター](#system-filters)で詳しく説明しています）。
