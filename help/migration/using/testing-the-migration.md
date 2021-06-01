---
product: campaign
title: 移行のテスト
description: 移行のテスト
audience: migration
content-type: reference
topic-tags: migration-procedure
exl-id: 228ee9e4-46a0-4d82-b8ba-b019bc0e7cac
source-git-commit: 98d646919fedc66ee9145522ad0c5f15b25dbf2e
workflow-type: tm+mt
source-wordcount: '667'
ht-degree: 3%

---

# 移行のテスト{#testing-the-migration}

## 一般的な手順{#general-procedure}

設定に応じて、移行テストを実行する方法がいくつかあります。

移行テストを実行するには、テスト/開発環境が必要です。 開発環境には、次のライセンスが適用されます。ライセンス契約を確認するか、Adobe Campaignの販売サービスにお問い合わせください。

1. 進行中のすべての開発を停止し、実稼動環境に引き継ぎます。
1. 開発環境データベースのバックアップを作成します。
1. 開発インスタンスですべてのAdobe Campaignプロセスを停止します。
1. 実稼動環境データベースのバックアップを作成し、開発環境として復元します。
1. Adobe Campaignサービスを開始する前に、**freezeInstance.js**&#x200B;焼灼スクリプトを実行して、バックアップの開始時に実行中だったオブジェクトをデータベースから消去します。

   ```
   nlserver javascript nms:freezeInstance.js -instance:<instance> -arg:<run|dry>
   ```

   >[!NOTE]
   >
   >コマンドは、デフォルトで&#x200B;**dry**&#x200B;モードで起動し、そのコマンドで実行されたすべてのリクエストが、起動されずにリストされます。 注意喚起要求を実行するには、コマンドで&#x200B;**run**&#x200B;を使用します。

1. バックアップを復元しようとして、正しいバックアップを作成してください。 データベース、テーブル、データなどにアクセスできることを確認します。
1. 開発環境で移行手順をテストします。

   完全な手順については、 [Adobe Campaign 7への移行の前提条件](../../migration/using/prerequisites-for-migration-to-adobe-campaign-7.md)の節で詳しく説明しています。

1. 開発環境の移行が成功した場合は、実稼動環境を移行できます。

>[!IMPORTANT]
>
>データ構造が変更されたので、v5プラットフォームとv7プラットフォームの間でデータパッケージのインポートおよびエクスポートはできません。

>[!NOTE]
>
>Adobe Campaign updateコマンド(**postupgrade**)を使用すると、リソースを同期し、スキーマとデータベースを更新できます。 この操作は、アプリケーションサーバー上で1回だけ実行できます。 リソースを同期した後に、**postupgrade**&#x200B;コマンドを使用して、同期でエラーが発生したか警告が発生したかを検出できます。

## 移行ツール{#migration-tools}

様々なオプションを使用して、移行による影響を測定し、潜在的な問題を特定できます。 以下のオプションが実行されます。

* **config**&#x200B;コマンドで、次の操作を実行します。

   ```
   nlserver.exe config <option> -instance:<instanceName>
   ```

* またはポストアップグレード時に次の操作を行います。

   ```
   nlserver.exe config -postupgrade <option> -instance:<instanceName>
   ```

>[!NOTE]
>
>**-instance:`<instanceame>`**&#x200B;オプションを使用する必要があります。 **-allinstances**&#x200B;オプションは使用しないことをお勧めします。

### -showCustomEntitiesおよび —showDeletedEntitiesオプション{#showcustomentities-and--showdeletedentities-options}

* **-showCustomEntities**&#x200B;オプションは、非標準オブジェクトのリストを表示します。

   ```
   nlserver.exe config -showCustomEntities -instance:<instanceName>
   ```

   送信メッセージの例：

   ```
   xtk_migration:opsecurity2 xtk:entity
   ```

* **-showDeletedEntities**&#x200B;オプションは、データベースまたはファイルシステムに見つからないすべての標準オブジェクトのリストを表示します。 見つからないオブジェクトごとに、パスが指定されます。

   ```
   nlserver.exe config -showDeletedEntities -instance:<instanceName>
   ```

   送信メッセージの例：

   ```
   Out of the box object 'nms:deliveryCustomizationMdl' belonging to the 'xtk:srcSchema' schema has not been found in the file system.
   ```

### 検証プロセス{#verification-process}

このプロセスは、ポストアップグレードコマンドの標準として統合され、移行が失敗する可能性のある警告およびエラーを表示できます。 **エラーが表示された場合、移行は実行されていません。** これが発生した場合は、すべてのエラーを修正し、ポストアップグレードを再起動します。

次のコマンドを使用して、検証プロセスを単独で（移行なしで）開始できます。

```
nlserver.exe config -postupgrade -check -instance:<instanceName>
```

>[!NOTE]
>
>JST-310040コードを持つ警告とエラーはすべて無視してください。

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
   <td> このタイプの構文は、配信のパーソナライゼーションではサポートされなくなりました。 <a href="../../migration/using/general-configurations.md#javascript" target="_blank">JavaScript</a>を参照してください。 正しくない場合は、値の型が正しいことを確認します。<br /> </td> 
  </tr> 
  <tr> 
   <td> common.js<br /> </td> 
   <td> PU-0002<br /> </td> 
   <td> 警告<br /> </td> 
   <td> このライブラリは使用しないでください。<br /> </td> 
  </tr> 
  <tr> 
   <td> logon(<br />) </td> 
   <td> PU-0003<br /> </td> 
   <td> 警告<br /> </td> 
   <td> この接続方法は使用しないでください。 <a href="../../migration/using/general-configurations.md#identified-web-applications" target="_blank">識別されたWebアプリケーション</a>を参照してください。<br /> </td> 
  </tr> 
  <tr> 
   <td> 新しいSoapMethodCall(<br /> </td> 
   <td> PU-0004<br /> </td> 
   <td> 警告<br /> </td> 
   <td> この関数は、<strong>sessionTokenOnly</strong>モードのセキュリティゾーンから実行されるJavaScriptコードで使用される場合にのみサポートされます。<br /> </td> 
  </tr> 
  <tr> 
   <td> sql=<br /> </td> 
   <td> PU-0005<br /> </td> 
   <td> エラー<br /> </td> 
   <td> このタイプのエラーは、移行エラーを引き起こします。 <a href="../../migration/using/general-configurations.md#sqldata" target="_blank">SQLData</a>.<br />を参照してください。 </td> 
  </tr> 
  <tr> 
   <td> SQLDATA<br /> </td> 
   <td> PU-0006<br /> </td> 
   <td> エラー<br /> </td> 
   <td> このタイプのエラーは、移行エラーを引き起こします。 <a href="../../migration/using/general-configurations.md#sqldata" target="_blank">SQLData</a>を参照してください。 概要タイプのWebアプリケーションエラーログを取得する場合（v6.02から移行する場合）、<a href="../../migration/using/specific-configurations-in-v6-02.md#web-applications" target="_blank">Webアプリケーション</a>.<br />を参照してください。 </td> 
  </tr> 
 </tbody> 
</table>

データベースとスキーマの一貫性チェックも実行されます。

### 復元オプション{#restoration-option}

このオプションを使用すると、標準のオブジェクトが変更されている場合に、そのオブジェクトを復元できます。 復元された各オブジェクトに対して、変更のバックアップが選択したフォルダに保存されます。

```
nlserver.exe config -postupgrade -restoreFactory:<backupfolder> -instance:<instanceName>
```

>[!NOTE]
>
>絶対フォルダーパスを使用し、フォルダーツリー構造を維持することを強くお勧めします。 例：backupFolder\nms\srcSchema\billing.xml.

### 移行を再開しています{#resuming-migration}

移行エラーの後にポストアップグレードを再開すると、停止した場所から再開されます。
