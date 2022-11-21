---
product: campaign
title: 移行のテスト
description: 移行のテスト
audience: migration
content-type: reference
topic-tags: migration-procedure
exl-id: 228ee9e4-46a0-4d82-b8ba-b019bc0e7cac
source-git-commit: 2594e4943ba24ae65d1fc005da589dc674aa2b0f
workflow-type: tm+mt
source-wordcount: '706'
ht-degree: 4%

---

# 移行テスト{#testing-the-migration}

![](../../assets/v7-only.svg)

## 一般的な手順 {#general-procedure}

設定に応じて、移行テストを実行する方法がいくつかあります。

移行テストを実行するには、テスト/開発環境が必要です。 Adobe Campaign環境は、次のライセンスを受けることができます。ライセンス契約を確認するか、Adobe担当者にお問い合わせください。

1. 進行中のすべての開発を停止し、実稼動環境に引き継ぎます。
1. 開発環境データベースのバックアップを作成します。
1. 開発インスタンスですべてのAdobe Campaignプロセスを停止します。
1. 実稼動環境のデータベースのバックアップを作成し、開発環境として復元します。
1. Adobe Campaignサービスを開始する前に、 **freezeInstance.js** バックアップの開始時に実行されていたオブジェクトのデータベースをクリアするための注意スクリプト。

   ```
   nlserver javascript nms:freezeInstance.js -instance:<instance> -arg:<run|dry>
   ```

   >[!NOTE]
   >
   >コマンドは、デフォルトで **乾燥、乾燥** モードとに分類され、そのコマンドによって実行されたすべてのリクエストが一覧表示されます。 注意喚起リクエストを実行するには、 **実行** 」と入力します。

1. バックアップを復元しようとして、バックアップが正しいことを確認します。 データベース、テーブル、データなどにアクセスできることを確認します。
1. 開発環境で移行手順をテストします。
1. 開発環境の移行が成功した場合は、実稼動環境を移行できます。

>[!CAUTION]
>
>データ構造が変更されたので、v5 プラットフォームと v7 プラットフォームの間では、データパッケージのインポートおよびエクスポートはできません。


## 移行ツール {#migration-tools}

様々なオプションを使用すると、移行による影響を測定し、潜在的な問題を特定できます。 以下のオプションが実行されます。

* 内 **config** コマンド：

   ```
   nlserver.exe config <option> -instance:<instanceName>
   ```

* または、ポストアップグレード時に次の操作を行います。

   ```
   nlserver.exe config -postupgrade <option> -instance:<instanceName>
   ```

>[!NOTE]
>
>* 次を使用する必要があります。 **-instance:`<instanceame>`** オプション。 この **-allinstances** オプション。
>* Adobe Campaign update コマンド (**postupgrade**) を使用すると、リソースを同期し、スキーマとデータベースを更新できます。 この操作は、アプリケーションサーバー上で 1 回だけ実行できます。 リソースを同期した後、 **postupgrade** コマンドを使用すると、同期でエラーが発生したか警告が発生したかを検出できます。


### 非標準のオブジェクトまたは見つからないオブジェクト

* この **-showCustomEntities** 「 」オプションは、非標準オブジェクトのリストを表示します。

   ```
   nlserver.exe config -showCustomEntities -instance:<instanceName>
   ```

   送信メッセージの例：

   ```
   xtk_migration:opsecurity2 xtk:entity
   ```

* この **-showDeletedEntities** 「 」オプションは、データベースまたはファイルシステムに存在しないすべての標準オブジェクトのリストを表示します。 見つからない各オブジェクトに対して、パスが指定されます。

   ```
   nlserver.exe config -showDeletedEntities -instance:<instanceName>
   ```

   送信メッセージの例：

   ```
   Out of the box object 'nms:deliveryCustomizationMdl' belonging to the 'xtk:srcSchema' schema has not been found in the file system.
   ```

### 検証プロセス {#verification-process}

ポストアップグレードコマンドの標準として統合され、このプロセスにより、移行が失敗する可能性のある警告およびエラーを表示できます。 **エラーが表示される場合、移行は実行されていません。** この場合は、すべてのエラーを修正し、アップグレード後に再起動します。

次のコマンドを使用して、検証プロセスを移行せずに独自に開始できます。

```
nlserver.exe config -postupgrade -check -instance:<instanceName>
```

>[!NOTE]
>
>JST-310040コードでは、すべての警告およびエラーを無視できます。

次の式が検索されます（大文字と小文字が区別されます）。

<table> 
 <thead> 
  <tr> 
   <th> 式<br /> </th> 
   <th> エラーコード<br /> </th> 
   <th> ログタイプ<br /> </th> 
   <th> コメント<br /> </th> 
  </tr> 
 </thead> 
 <tbody> 
  <tr> 
   <td> .@<br /> </td> 
   <td> PU-0001<br /> </td> 
   <td> 警告<br /> </td> 
   <td> このタイプの構文は、配信のパーソナライゼーションではサポートされなくなりました。 <br /> </td> 
  </tr> 
  <tr> 
   <td> common.js<br /> </td> 
   <td> PU-0002<br /> </td> 
   <td> 警告<br /> </td> 
   <td> このライブラリは使用しないでください。<br /> </td> 
  </tr> 
  <tr> 
   <td> logon(<br /> </td> 
   <td> PU-0003<br /> </td> 
   <td> 警告<br /> </td> 
   <td> この接続方法は使用できなくなりました。<br /> </td> 
  </tr> 
  <tr> 
   <td> new SoapMethodCall(<br /> </td> 
   <td> PU-0004<br /> </td> 
   <td> 警告<br /> </td> 
   <td> この関数は、 <strong>sessionTokenOnly</strong> モード。<br /> </td> 
  </tr> 
  <tr> 
   <td> sql=<br /> </td> 
   <td> PU-0005<br /> </td> 
   <td> エラー<br /> </td> 
   <td> このタイプのエラーは、移行エラーにつながります。<br /> </td> 
  </tr> 
  <tr> 
   <td> crmDeploymentType="onpremise"<br /> </td> 
   <td> PU-0007<br /> </td> 
   <td> エラー<br /> </td> 
   <td> このタイプのデプロイメントはサポートされなくなりました。 Office 365 およびオンプレミスのMicrosoft CRM コネクタの展開の種類は非推奨（廃止予定）となりました。 
   </br>外部アカウントでこれらの非推奨のデプロイメントタイプのいずれかを使用している場合は、この外部アカウントを削除し、 <b>postupgrade</b> コマンドを使用します。 
   </br>Web API のデプロイメントに変更するには、 <a href="../../platform/using/crm-ms-dynamics.md#configure-acc-for-microsoft" target="_blank">Web アプリケーション</a>.<br /> </td>
  </tr> 
  <tr> 
   <td> CRM v1(mscrmWorkflow/sfdcWorkflow)<br /> </td> 
   <td> PU-0008<br /> </td> 
   <td> エラー<br /> </td> 
   <td> Microsoft CRM、Salesforce、Oracle CRM On Demand のアクションアクティビティは使用できなくなりました。Adobe Campaignと CRM システム間のデータ同期を設定するには、 <a href="../../workflow/using/crm-connector.md" target="_blank">CRM コネクタ</a> ターゲティングアクティビティ。<br /> </td>
  </tr> 
 </tbody> 
</table>

また、データベースとスキーマの一貫性チェックも実行されます。

### 復元オプション {#restoration-option}

このオプションを使用すると、標準のオブジェクトが変更されている場合にそのオブジェクトを復元できます。 復元された各オブジェクトに対して、変更のバックアップが選択したフォルダに保存されます。

```
nlserver.exe config -postupgrade -restoreFactory:<backupfolder> -instance:<instanceName>
```

>[!NOTE]
>
>絶対フォルダーパスを使用し、フォルダーツリー構造を維持することを強くお勧めします。 例：backupFolder\nms\srcSchema\billing.xml.

### 移行を再開 {#resuming-migration}

移行エラーが発生した後にポストアップグレードを再起動すると、停止した場所から再開されます。
