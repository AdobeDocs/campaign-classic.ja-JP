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
translation-type: tm+mt
source-git-commit: 70b143445b2e77128b9404e35d96b39694d55335
workflow-type: tm+mt
source-wordcount: '670'
ht-degree: 3%

---


# 移行のテスト{#testing-the-migration}

## 一般的な手順 {#general-procedure}

設定に応じて、いくつかの方法で移行テストを実施できます。

移行テストを実施するには、テスト/開発環境が必要です。 開発環境は、次のライセンスの対象となります。ライセンス契約を確認するか、Adobe Campaignの営業サービスに連絡してください。

1. 進行中の開発をすべて停止し、制作環境に持ち越します。
1. 開発環境データベースのバックアップを作成します。
1. 開発インスタンスのすべてのAdobe Campaignプロセスを停止します。
1. 本番環境・データベースのバックアップを作成し、開発環境としてリストアします。
1. Adobe Campaignサービスを開始する前に、 **freezeInstance.jsの** 焼灼スクリプトを実行し、バックアップの開始時に実行していたオブジェクトのデータベースを消去できます。

   ```
   nlserver javascript nms:freezeInstance.js -instance:<instance> -arg:<run|dry>
   ```

   >[!NOTE]
   >
   >コマンドはデフォルトで **ドライ** モードで起動し、コマンドが実行したすべての要求をリストします。起動は行われません。 焼灼要求を実行するには、コマンドで **run** を使用します。

1. バックアップを復元して、正しいバックアップであることを確認します。 データベース、テーブル、データなどにアクセスできることを確認します。
1. 開発環境で移行手順をテストします。

   手順の詳細については、「Adobe Campaign7への移行の [前提条件](../../migration/using/prerequisites-for-migration-to-adobe-campaign-7.md) 」の節を参照してください。

1. 開発環境の移行に成功した場合は、実稼働環境を移行できます。

>[!IMPORTANT]
>
>データ構造が変更されたため、v5プラットフォームとv7プラットフォームの間では、データパッケージの読み込みと書き出しを行うことはできません。

>[!NOTE]
>
>Adobe Campaignの更新コマンド(**postupgrade**)を使用すると、リソースを同期し、スキーマとデータベースを更新できます。 この操作は、アプリケーションサーバー上でのみ1回実行できます。 リソースを同期した後、 **postupgrade** コマンドを使用すると、同期でエラーが発生したか警告が発生したかを検出できます。

## 移行ツール {#migration-tools}

様々なオプションを使用して、移行による影響を測定し、潜在的な問題を特定できます。 以下のオプションが実行されます。

* config **コマンドで次の操作を行います** 。

   ```
   nlserver.exe config <option> -instance:<instanceName>
   ```

* またはアップグレード後：

   ```
   nlserver.exe config -postupgrade <option> -instance:<instanceName>
   ```

>[!NOTE]
>
>次の **インスタンスを使用する必要があります。`<instanceame>`** 」オプションを選択します。 「 **-allinstances** 」オプションは使用しないことをお勧めします。

### -showCustomEntitiesと —showDeletedEntitiesの各オプション {#showcustomentities-and--showdeletedentities-options}

* -showCustomEntities **オプションは** 、次の非標準オブジェクトのリストを表示します。

   ```
   nlserver.exe config -showCustomEntities -instance:<instanceName>
   ```

   送信済みメッセージの例：

   ```
   xtk_migration:opsecurity2 xtk:entity
   ```

* -showDeletedEntities **** (-showDeletedEntities)オプションは、データベースまたはファイルシステムに存在しないすべての標準オブジェクトのリストを表示します。 見つからない各オブジェクトに対して、パスが指定されます。

   ```
   nlserver.exe config -showDeletedEntities -instance:<instanceName>
   ```

   送信済みメッセージの例：

   ```
   Out of the box object 'nms:deliveryCustomizationMdl' belonging to the 'xtk:srcSchema' schema has not been found in the file system.
   ```

### Verification process {#verification-process}

アップグレード後のコマンドに標準として統合されているため、このプロセスにより、移行が失敗する可能性のある警告やエラーを表示できます。 **エラーが表示された場合、移行は実行されていません。** この場合は、すべてのエラーを修正し、アップグレード後に開始を再度行ってください。

次のコマンドを使用して、検証プロセスを個別に（移行せずに）開始できます。

```
nlserver.exe config -postupgrade -check -instance:<instanceName>
```

>[!NOTE]
>
>JST-310040コードを持つ警告とエラーはすべて無視してください。

次の式を検索します（大文字と小文字が区別されます）。

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
   <td> このタイプの構文は、配信のパーソナライゼーションではサポートされなくなりました。 JavaScriptを参照して <a href="../../migration/using/general-configurations.md#javascript" target="_blank">ください</a>。 それ以外の場合は、値のタイプが正しいことを確認します。<br /> </td> 
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
   <td> この接続メソッドは使用しなくなります。 「 <a href="../../migration/using/general-configurations.md#identified-web-applications" target="_blank">識別されたWebアプリケーション</a>」を参照してください。<br /> </td> 
  </tr> 
  <tr> 
   <td> new SoapMethodCall(<br /> </td> 
   <td> PU-0004<br /> </td> 
   <td> 警告<br /> </td> 
   <td> この関数は、 <strong>sessionTokenOnly</strong> モードのセキュリティゾーンから実行されるJavaScriptコードで使用される場合にのみサポートされます。<br /> </td> 
  </tr> 
  <tr> 
   <td> sql=<br /> </td> 
   <td> PU-0005<br /> </td> 
   <td> エラー<br /> </td> 
   <td> このタイプのエラーは、移行エラーの原因となります。 SQLDataを参照し <a href="../../migration/using/general-configurations.md#sqldata" target="_blank">てください</a>。<br /> </td> 
  </tr> 
  <tr> 
   <td> SQLDATA<br /> </td> 
   <td> PU-0006<br /> </td> 
   <td> エラー<br /> </td> 
   <td> このタイプのエラーは、移行エラーの原因となります。 SQLDataを参照し <a href="../../migration/using/general-configurations.md#sqldata" target="_blank">てください</a>。 概要タイプのWebアプリケーションエラーログ（v6.02からの移行）を取得する場合は、 <a href="../../migration/using/specific-configurations-in-v6-02.md#web-applications" target="_blank">Web アプリケーションを参照してください</a>。<br /> </td> 
  </tr> 
 </tbody> 
</table>

データベースとスキーマコヒーレンス・チェックも行う。

### Restorationオプション {#restoration-option}

このオプションを使用すると、既に変更されている場合に、そのまま使用できるオブジェクトを復元できます。 復元された各オブジェクトに対して、変更のバックアップが選択したフォルダに保存されます。

```
nlserver.exe config -postupgrade -restoreFactory:<backupfolder> -instance:<instanceName>
```

>[!NOTE]
>
>フォルダーの絶対パスを使用し、フォルダーツリー構造を維持することを強くお勧めします。 次に例を示します。backupFolder\nms\srcSchema\billing.xml

### 移行の再開 {#resuming-migration}

移行の失敗後にアップグレード後に再起動すると、停止した場所と同じ場所から再開されます。
