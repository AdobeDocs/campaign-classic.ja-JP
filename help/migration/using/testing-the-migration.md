---
product: campaign
title: 移行のテスト
description: 移行のテスト
feature: Upgrade
audience: migration
content-type: reference
topic-tags: migration-procedure
hide: true
exl-id: 228ee9e4-46a0-4d82-b8ba-b019bc0e7cac
TQID: https://experienceleague.adobe.com/Oi8b9GLlXTfD62SjhRfEZJviiLN5VXNUG4hYkSOjC8Y
product_v2:
  - id: dfc56824-e8b9-499e-85d4-21aedb507314
feature_v2:
  - id: b82389f8-9b5e-4083-8e3b-3cef299fb8b9
subfeature_v2:
  - id: cfc95e9b-b035-4403-a6a9-b27a8a053a37
topic_v2:
  - id: d095671a-1355-40aa-8b5f-06c33c68080b
  - id: e0eb8757-182f-49f3-94a4-1587d16f5094
source-git-commit: 4c295c0dabae8aba298390a3da2422a3fa1219f9
workflow-type: tm+mt
source-wordcount: 722
ht-degree: 0%

---

# 移行テスト{#testing-the-migration}



## 一般手続 {#general-procedure}

設定に応じて、移行テストを実行する方法がいくつかあります。

移行テストを実行するには、テスト/開発環境が必要です。 Adobe Campaign環境にはライセンスが適用されます。ライセンス契約を確認するか、Adobe担当者にお問い合わせください。

1. 進行中のすべての開発を停止し、本番環境に引き継ぎます。
1. 開発環境データベースのバックアップを作成します。
1. 開発インスタンス上のすべてのAdobe Campaign プロセスを停止します。
1. 実稼動環境データベースのバックアップを作成し、開発環境として復元します。
1. Adobe Campaign サービスを開始する前に、**freezeInstance.js**&#x200B;焼結スクリプトを実行して、バックアップ開始時に実行中のオブジェクトのデータベースをクリアします。

   ```
   nlserver javascript nms:freezeInstance.js -instance:<instance> -arg:<run|dry>
   ```

   >[!NOTE]
   >
   >コマンドはデフォルトで&#x200B;**dry** モードで起動し、そのコマンドによって実行されたすべてのリクエストを、起動せずに一覧表示します。 焼灼要求を実行するには、コマンドで&#x200B;**run**&#x200B;を使用します。

1. バックアップを復元して、バックアップが正しいことを確認します。 データベース、テーブル、データなどにアクセスできることを確認します。
1. 開発環境で移行手順をテストします。
1. 開発環境の移行が成功した場合は、実稼動環境を移行できます。

>[!CAUTION]
>
>データ構造に変更が加えられたため、v5 プラットフォームとv7 プラットフォームの間でデータパッケージの読み込みと書き出しができません。


## 移行ツール {#migration-tools}

様々なオプションを使用して、移行の影響を測定し、潜在的な問題を特定できます。 これらのオプションを実行します。

* **config** コマンドで次の操作を行います。

  ```
  nlserver.exe config <option> -instance:<instance-name>
  ```

* アップグレード後に以下を実行します。

  ```
  nlserver.exe config -postupgrade <option> -instance:<instance-name>
  ```

>[!NOTE]
>
>* **-instance:`<instanceame>`** オプションを使用する必要があります。 **-allinstances** オプションを使用することはお勧めしません。
>* Adobe Campaign update コマンド （**postupgrade**）を使用すると、リソースを同期し、スキーマとデータベースを更新できます。 この操作は、アプリケーションサーバー上で1回だけ実行できます。 リソースを同期した後、**postupgrade** コマンドを使用すると、同期によってエラーまたは警告が生成されるかどうかを検出できます。

### 標準外または見つからないオブジェクト

* **-showCustomEntities** オプションには、すべての非標準オブジェクトのリストが表示されます。

  ```
  nlserver.exe config -showCustomEntities -instance:<instance-name>
  ```

  送信されたメッセージの例：

  ```
  xtk_migration:opsecurity2 xtk:entity
  ```

* **-showDeletedEntities** オプションは、データベースまたはファイルシステムに存在しないすべての標準オブジェクトのリストを表示します。 見つからないオブジェクトごとに、パスが指定されます。

  ```
  nlserver.exe config -showDeletedEntities -instance:<instance-name>
  ```

  送信されたメッセージの例：

  ```
  Out of the box object 'nms:deliveryCustomizationMdl' belonging to the 'xtk:srcSchema' schema has not been found in the file system.
  ```

### 検証プロセス {#verification-process}

アップグレード後のコマンドに標準として統合されたこのプロセスでは、移行が失敗する可能性のある警告とエラーを表示できます。 **エラーが表示された場合、移行は実行されていません。** この場合は、すべてのエラーを修正してから、アップグレード後に再起動してください。

次のコマンドを使用して、検証プロセスを単独で（移行なしで）開始できます。

```
nlserver.exe config -postupgrade -check -instance:<instance-name>
```

>[!NOTE]
>
>JST-310040 コードを使用すると、すべての警告とエラーを無視できます。

次の式が検索されます（大文字と小文字が区別されます）。

<table> 
 <thead> 
  <tr> 
   <th> 式<br /> </th> 
   <th> エラーコード <br /> </th> 
   <th> ログの種類<br /> </th> 
   <th> コメント <br /> </th> 
  </tr> 
 </thead> 
 <tbody> 
  <tr> 
   <td> .@<br /> </td> 
   <td> PU-0001<br /> </td> 
   <td> 警告<br /> </td> 
   <td> この種類の構文は、配信パーソナライゼーションではサポートされなくなりました。<br /> </td> 
  </tr> 
  <tr> 
   <td> common.js<br /> </td> 
   <td> PU-0002<br /> </td> 
   <td> 警告<br /> </td> 
   <td> このライブラリは使用できません。<br /> </td> 
  </tr> 
  <tr> 
   <td> ログオン （<br /> </td> 
   <td> PU-0003<br /> </td> 
   <td> 警告<br /> </td> 
   <td> この接続メソッドは使用できません。<br /> </td> 
  </tr> 
  <tr> 
   <td> 新規SoapMethodCall （<br /> </td> 
   <td> PU-0004<br /> </td> 
   <td> 警告<br /> </td> 
   <td> この関数は、<strong>sessionTokenOnly</strong> モードのセキュリティゾーンから実行されるJavaScript コードで使用される場合にのみサポートされます。<br /> </td> 
  </tr> 
  <tr> 
   <td> sql=<br /> </td> 
   <td> PU-0005<br /> </td> 
   <td> エラー<br /> </td> 
   <td> この種類のエラーは、移行エラーにつながります。<br /> </td> 
  </tr> 
  <tr> 
   <td> crmDeploymentType="onpremise"<br /> </td> 
   <td> PU-0007<br /> </td> 
   <td> エラー<br /> </td> 
   <td> このタイプのデプロイメントはサポートされなくなりました。 Office 365およびオンプレミスのMicrosoft CRM コネクタのデプロイメントタイプは非推奨（廃止予定）になりました。 
   </br>外部アカウントでこれらの非推奨のデプロイメントタイプのいずれかを使用している場合は、この外部アカウントを削除し、<b>postupgrade</b> コマンドを実行する必要があります。 
   </br>Web API デプロイメントに変更するには、<a href="../../platform/using/crm-ms-dynamics.md#configure-acc-for-microsoft" target="_blank">Web アプリケーション </a>を参照してください。<br /> </td>
  </tr> 
  <tr> 
   <td> CRM v1 （mscrmWorkflow/sfdcWorkflow） <br /> </td> 
   <td> PU-0008<br /> </td> 
   <td> エラー<br /> </td> 
   <td> Microsoft CRM、Salesforce、Oracle CRM On Demand アクションアクティビティは使用できなくなりました。 Adobe CampaignとCRM システム間のデータ同期を設定するには、<a href="../../workflow/using/crm-connector.md" target="_blank">CRM コネクタ </a> ターゲティングアクティビティ <br />を使用する必要があります。 </td>
  </tr> 
 </tbody> 
</table>

データベースとスキーマのコヒーレンスのチェックも実行されます。

### 復元オプション {#restoration-option}

このオプションを使用すると、変更されたオブジェクトをすぐに復元できます。 復元された各オブジェクトに対して、変更のバックアップが選択したフォルダーに保存されます。

```
nlserver.exe config -postupgrade -restoreFactory:<backupfolder> -instance:<instance-name>
```

>[!NOTE]
>
>絶対フォルダーパスを使用し、フォルダーツリー構造を維持することを強くお勧めします。 例：backupFolder\nms\srcSchema\billing.xml

### 移行の再開 {#resuming-migration}

移行エラーの後にアップグレード後を再起動すると、停止した場所と同じ場所から再開されます。
