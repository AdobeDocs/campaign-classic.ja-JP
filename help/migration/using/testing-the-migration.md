---
product: campaign
title: 移行のテスト
description: 移行のテスト
feature: Upgrade
audience: migration
content-type: reference
topic-tags: migration-procedure
hide: true
hidefromtoc: true
exl-id: 228ee9e4-46a0-4d82-b8ba-b019bc0e7cac
source-git-commit: 0ed70b3c57714ad6c3926181334f57ed3b409d98
workflow-type: tm+mt
source-wordcount: '715'
ht-degree: 0%

---

# 移行テスト{#testing-the-migration}



## 一般的な手順 {#general-procedure}

設定に応じて、移行テストを実行する方法はいくつかあります。

移行テストを実行するためのテスト/開発環境が必要です。 Adobe Campaign環境はライセンスの対象です。ライセンス契約を確認するか、Adobe担当者にお問い合わせください。

1. 進行中のすべての開発を停止して、実稼動環境に引き継ぎます。
1. 開発環境データベースのバックアップを作成します。
1. 開発インスタンスでAdobe Campaign プロセスをすべて停止します。
1. 実稼動環境のデータベースのバックアップを作成し、開発環境として復元します。
1. Adobe Campaign サービスを開始する前に、**freezeInstance.js** 焼灼スクリプトを実行すると、バックアップの開始時に実行されていたオブジェクトのデータベースを消去できます。

   ```
   nlserver javascript nms:freezeInstance.js -instance:<instance> -arg:<run|dry>
   ```

   >[!NOTE]
   >
   >コマンドは、デフォルトでは **ドライ** モードで起動し、起動せずに、そのコマンドで実行されたすべてのリクエストをリストします。 焼灼リクエストを実行するには、コマンドで **run** を使用します。

1. バックアップを復元して、バックアップが正しいことを確認します。 データベース、テーブル、データなどにアクセスできることを確認します。
1. 開発環境で移行手順をテストします。
1. 開発環境の移行が成功した場合は、実稼動環境を移行できます。

>[!CAUTION]
>
>データ構造が変更されたので、v5 プラットフォームと v7 プラットフォームの間でデータパッケージを読み込んだり書き出したりすることはできません。


## 移行ツール {#migration-tools}

様々なオプションを使用して、移行による影響を測定し、潜在的な問題を特定できます。 次のオプションが実行されます。

* **config** コマンドで以下を実行します。

  ```
  nlserver.exe config <option> -instance:<instance-name>
  ```

* アップグレード後は、以下が行われます。

  ```
  nlserver.exe config -postupgrade <option> -instance:<instance-name>
  ```

>[!NOTE]
>
>* **-instance:`<instanceame>`** オプションを使用する必要があります。 **-allinstances** オプションを使用することはお勧めしません。
>* Adobe Campaign更新コマンド（**postupgrade**）を使用すると、リソースを同期し、スキーマとデータベースを更新できます。 この操作は、アプリケーションサーバーで 1 回だけ実行できます。 リソースを同期した後、**postupgrade** コマンドを使用して、同期でエラーまたは警告が生成されるかどうかを検出できます。

### 非標準オブジェクトまたは不足オブジェクト

* **-showCustomEntities** オプションは、すべての非標準オブジェクトのリストを表示します。

  ```
  nlserver.exe config -showCustomEntities -instance:<instance-name>
  ```

  送信済みメッセージの例：

  ```
  xtk_migration:opsecurity2 xtk:entity
  ```

* **-showDeletedEntities** オプションは、データベースまたはファイル・システムに存在しないすべての標準オブジェクトのリストを表示します。 不足している各オブジェクトに対して、パスが指定されます。

  ```
  nlserver.exe config -showDeletedEntities -instance:<instance-name>
  ```

  送信済みメッセージの例：

  ```
  Out of the box object 'nms:deliveryCustomizationMdl' belonging to the 'xtk:srcSchema' schema has not been found in the file system.
  ```

### 検証プロセス {#verification-process}

アップグレード後のコマンドに標準として統合されているので、このプロセスを使用すると、移行が失敗する可能性のある警告とエラーを表示できます。 **エラーが表示された場合、移行は実行されていません。** この場合は、すべてのエラーを修正し、アップグレード後に再起動します。

検証プロセスは、コマンドを使用して（移行を行わずに）単独で開始できます。

```
nlserver.exe config -postupgrade -check -instance:<instance-name>
```

>[!NOTE]
>
>すべての警告とエラーは、JST-310040 コードで無視できます。

次の式が検索されます（大文字と小文字が区別されます）。

<table> 
 <thead> 
  <tr> 
   <th> 式 <br /> </th> 
   <th> エラーコード <br /> </th> 
   <th> ログの種類 <br /> </th> 
   <th> コメント <br /> </th> 
  </tr> 
 </thead> 
 <tbody> 
  <tr> 
   <td> .@<br /> </td> 
   <td> PU-0001<br /> </td> 
   <td> 警告 <br /> </td> 
   <td> このタイプの構文は、配信のパーソナライゼーションではサポートされなくなりました。<br /> </td> 
  </tr> 
  <tr> 
   <td> common.js<br /> </td> 
   <td> PU-0002<br /> </td> 
   <td> 警告 <br /> </td> 
   <td> このライブラリは使用できません。<br /> </td> 
  </tr> 
  <tr> 
   <td> logon （<br /> </td> 
   <td> PU-0003<br /> </td> 
   <td> 警告 <br /> </td> 
   <td> この接続方法は使用しないでください。<br /> </td> 
  </tr> 
  <tr> 
   <td> 新しい SoapMethodCall （<br /> </td> 
   <td> PU-0004<br /> </td> 
   <td> 警告 <br /> </td> 
   <td> この関数は、<strong>sessionTokenOnly</strong> モードのセキュリティゾーンから実行されるJavaScript コードで使用される場合にのみサポートされ <br /> す。 </td> 
  </tr> 
  <tr> 
   <td> sql=<br /> </td> 
   <td> PU-0005<br /> </td> 
   <td> エラー <br /> </td> 
   <td> このタイプのエラーは移行エラーを引き起こします。<br /> </td> 
  </tr> 
  <tr> 
   <td> crmDeploymentType="onpremise"<br /> </td> 
   <td> PU-0007<br /> </td> 
   <td> エラー <br /> </td> 
   <td> このタイプのデプロイメントはサポートされなくなりました。 Office 365 およびオンプレミス Microsoft CRM コネクタのデプロイメントタイプは非推奨（廃止予定）になりました。 
   </br> 外部アカウントでこれらの非推奨のデプロイメントタイプのいずれかを使用している場合は、この外部アカウントを削除し、<b>postupgrade</b> コマンドを実行する必要があります。 
   </br>Web API デプロイメントに変更するには、<a href="../../platform/using/crm-ms-dynamics.md#configure-acc-for-microsoft" target="_blank">Web アプリケーション </a> を参照してください。<br /> </td>
  </tr> 
  <tr> 
   <td> CRM v1 （mscrmWorkflow/sfdcWorkflow） <br /> </td> 
   <td> PU-0008<br /> </td> 
   <td> エラー <br /> </td> 
   <td> Microsoft CRM、Salesforce、OracleCRM オンデマンドのアクションアクティビティは使用できなくなりました。 Adobe Campaignと CRM システム間のデータ同期を設定するには、<a href="../../workflow/using/crm-connector.md" target="_blank">CRM コネクタ </a> ターゲティングアクティビティを使用する必要があり <br /> す。 </td>
  </tr> 
 </tbody> 
</table>

データベースとスキーマのコヒーレンスチェックも実行されます。

### 復元オプション {#restoration-option}

このオプションを使用すると、既製のオブジェクトが変更されている場合に、そのオブジェクトを復元できます。 復元された各オブジェクトについて、変更のバックアップが選択したフォルダーに保存されます。

```
nlserver.exe config -postupgrade -restoreFactory:<backupfolder> -instance:<instance-name>
```

>[!NOTE]
>
>絶対フォルダーパスを使用し、フォルダーツリー構造を維持することを強くお勧めします。 例：backupFolder\nms\srcSchema\billing.xml

### 移行の再開 {#resuming-migration}

移行失敗後にアップグレード後を再開した場合、アップグレードは停止した場所から再開されます。
