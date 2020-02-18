---
title: 移行のテスト
seo-title: 移行のテスト
description: 移行のテスト
seo-description: null
page-status-flag: never-activated
uuid: 3ee6a10b-dea2-41c6-9aef-ee3ac922b459
contentOwner: sauviat
products: SG_CAMPAIGN/CLASSIC
audience: migration
content-type: reference
topic-tags: migration-procedure
discoiquuid: 30e3082f-a367-4c3b-bff2-208ccf97acd4
index: y
internal: n
snippet: y
translation-type: tm+mt
source-git-commit: 9f7cf3d530f141a661df5fcc8cbcf0bb4c8d3e89

---


# 移行のテスト{#testing-the-migration}

## 一般的な手順 {#general-procedure}

設定に応じて、移行テストを実行する方法がいくつかあります。

移行テストを実行するには、テスト/開発環境が必要です。 開発環境は、次のライセンスの対象となります。ライセンス契約を確認するか、Adobe Campaignの販売サービスにお問い合わせください。

1. 進行中の開発をすべて停止し、実稼働環境に持ち越します。
1. 開発環境データベースのバックアップを作成します。
1. 開発インスタンスですべてのAdobe Campaignプロセスを停止します。
1. 実稼働環境データベースのバックアップを作成し、開発環境として復元します。
1. Adobe Campaignサービスを開始する前に、 **** freezeInstance.jsの焼灼スクリプトを実行し、バックアップの開始時に実行されていたオブジェクトのデータベースをクリアできます。

   ```
   nlserver javascript nms:freezeInstance.js -instance:<instance> -arg:<run|dry>
   ```

   >[!NOTE]
   >
   >コマンドはデフォルトでドライモ **ードで起動し** 、そのコマンドで実行されたすべての要求が一覧表示されます。起動は行われません。 焼灼リクエストを実行するには、コ **マンドの** runを使用します。

1. バックアップを復元して、バックアップが正しいことを確認します。 データベース、テーブル、データなどにアクセスできることを確認します。
1. 開発環境で移行手順をテストします。

   詳しい手順は、「Adobe Campaign 7への移行 [の前提条件」の節に説明されています](../../migration/using/prerequisites-for-migration-to-adobe-campaign-7.md) 。

1. 開発環境の移行に成功した場合は、実稼働環境を移行できます。

>[!IMPORTANT]
>
>データ構造が変更されたため、v5プラットフォームとv7プラットフォームの間でデータパッケージの読み込みと書き出しを行うことはできません。

>[!NOTE]
>
>Adobe Campaignの更新コマンド(アップグレード後&#x200B;****)を使用すると、リソースを同期し、スキーマとデータベースを更新できます。 この操作は、アプリケーションサーバー上でのみ1回だけ実行できます。 リソースを同期した後、postupgrade **** コマンドを使用して、同期でエラーが発生したか警告が発生したかを検出できます。

## 移行ツール {#migration-tools}

様々なオプションを使用して、移行による影響を測定し、潜在的な問題を特定できます。 以下のオプションが実行されます。

* configコマ **ンド** :

   ```
   nlserver.exe config <option> -instance:<instanceName>
   ```

* またはアップグレード後に

   ```
   nlserver.exe config -postupgrade <option> -instance:<instanceName>
   ```

>[!NOTE]
>
>**インスタンスを使用する必`<instanceame>`**要があります。」オプションを選択します。 -allinstancesオプションの使用はお**&#x200B;勧めしません&#x200B;**。

### -showCustomEntitiesおよび —showDeletedEntitiesオプション {#showcustomentities-and--showdeletedentities-options}

* -showCustomEntities **オプションは** 、標準以外のすべてのオブジェクトのリストを表示します。

   ```
   nlserver.exe config -showCustomEntities -instance:<instanceName>
   ```

   送信済みメッセージの例：

   ```
   xtk_migration:opsecurity2 xtk:entity
   ```

* -showDeletedEntities **オプションは** 、データベースまたはファイルシステムに存在しないすべての標準オブジェクトのリストを表示します。 見つからないオブジェクトごとに、パスが指定されます。

   ```
   nlserver.exe config -showDeletedEntities -instance:<instanceName>
   ```

   送信済みメッセージの例：

   ```
   Out of the box object 'nms:deliveryCustomizationMdl' belonging to the 'xtk:srcSchema' schema has not been found in the file system.
   ```

### Verification process {#verification-process}

このプロセスは、アップグレード後のコマンドの標準として統合され、移行が失敗する可能性のある警告やエラーを表示できます。 **エラーが表示された場合は、移行は実行されていません。** この場合は、すべてのエラーを修正し、アップグレード後に再起動します。

次のコマンドを使用して、検証プロセスを独自に（移行せずに）開始できます。

```
nlserver.exe config -postupgrade -check -instance:<instanceName>
```

>[!NOTE]
>
>JST-310040コードを持つすべての警告およびエラーを無視してください。

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
   <td> このタイプの構文は、配信のパーソナライゼーションでサポートされなくなりました。 詳しくは、 <a href="../../migration/using/general-configurations.md#javascript" target="_blank">JavaScriptを参照してください</a>。 それ以外の場合は、値のタイプが正しいことを確認します。<br /> </td> 
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
   <td> この接続方法は使用しなくてもかまいません。 「識別されたWebアプ <a href="../../migration/using/general-configurations.md#identified-web-applications" target="_blank">リケーション」を参照してくださ</a>い。<br /> </td> 
  </tr> 
  <tr> 
   <td> new soapMethodCall(<br /> </td> 
   <td> PU-0004<br /> </td> 
   <td> 警告<br /> </td> 
   <td> この関数は、sessionTokenOnlyモードのセキュリティゾーンから実行されるJavaScriptコードで使用される場合にのみサポートさ <strong>れます</strong> 。<br /> </td> 
  </tr> 
  <tr> 
   <td> sql=<br /> </td> 
   <td> PU-0005<br /> </td> 
   <td> エラー<br /> </td> 
   <td> このタイプのエラーは、移行に失敗する原因となります。 SQLDataを参照し <a href="../../migration/using/general-configurations.md#sqldata" target="_blank">てください</a>。<br /> </td> 
  </tr> 
  <tr> 
   <td> SQLDATA<br /> </td> 
   <td> PU-0006<br /> </td> 
   <td> エラー<br /> </td> 
   <td> このタイプのエラーは、移行に失敗する原因となります。 SQLDataを参照し <a href="../../migration/using/general-configurations.md#sqldata" target="_blank">てください</a>。 概要タイプのWebアプリケーションエラーログ（v6.02からの移行）を取得する場合は、 <a href="../../migration/using/specific-configurations-in-v6-02.md#web-applications" target="_blank">Webアプリケーションを参照してください</a>。<br /> </td> 
  </tr> 
 </tbody> 
</table>

データベースとスキーマコヒーレンスチェックも実行される。

### Restorationオプション {#restoration-option}

このオプションを使用すると、変更済みのオブジェクトをそのまま使用して元に戻すことができます。 復元された各オブジェクトに対して、変更のバックアップが選択したフォルダに保存されます。

```
nlserver.exe config -postupgrade -restoreFactory:<backupfolder> -instance:<instanceName>
```

>[!NOTE]
>
>絶対フォルダーパスを使用し、フォルダーツリー構造を維持することを強くお勧めします。 例：backupFolder\nms\srcSchema\billing.xml.

### 移行の再開 {#resuming-migration}

移行の失敗後にアップグレード後に再起動すると、停止した場所と同じ場所から再開されます。
