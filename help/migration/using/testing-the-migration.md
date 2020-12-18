---
solution: Campaign Classic
product: campaign
title: 移行のテスト
description: 移行のテスト
audience: migration
content-type: reference
topic-tags: migration-procedure
translation-type: tm+mt
source-git-commit: 972885c3a38bcd3a260574bacbb3f507e11ae05b
workflow-type: tm+mt
source-wordcount: '667'
ht-degree: 3%

---


# 移行のテスト{#testing-the-migration}

## 一般的な手順{#general-procedure}

設定に応じて、いくつかの方法で移行テストを実施できます。

移行テストを実施するには、テスト/開発環境が必要です。 開発環境は、次のライセンスの対象となります。ライセンス契約を確認するか、Adobe Campaignの営業サービスに連絡してください。

1. 進行中の開発をすべて停止し、制作環境に持ち越します。
1. 開発環境データベースのバックアップを作成します。
1. 開発インスタンスのすべてのAdobe Campaignプロセスを停止します。
1. 本番環境・データベースのバックアップを作成し、開発環境としてリストアします。
1. Adobe Campaignサービスを開始する前に、**freezeInstance.js**&#x200B;の焼灼スクリプトを実行し、バックアップの開始時に実行していたオブジェクトのデータベースを消去できます。

   ```
   nlserver javascript nms:freezeInstance.js -instance:<instance> -arg:<run|dry>
   ```

   >[!NOTE]
   >
   >コマンドはデフォルトで&#x200B;**dry**&#x200B;モードで起動し、コマンドが実行したすべての要求をリストします。起動は行われません。 焼灼要求を実行するには、コマンドで&#x200B;**run**&#x200B;を使用します。

1. バックアップを復元して、正しいバックアップであることを確認します。 データベース、テーブル、データなどにアクセスできることを確認します。
1. 開発環境で移行手順をテストします。

   詳細な手順については、[Adobe Campaign7](../../migration/using/prerequisites-for-migration-to-adobe-campaign-7.md)への移行に必要な前提条件の節を参照してください。

1. 開発環境の移行に成功した場合は、実稼働環境を移行できます。

>[!IMPORTANT]
>
>データ構造が変更されたため、v5プラットフォームとv7プラットフォームの間では、データパッケージの読み込みと書き出しを行うことはできません。

>[!NOTE]
>
>Adobe Campaignの更新コマンド(**postupgrade**)を使用すると、リソースの同期とスキーマおよびデータベースの更新を行うことができます。 この操作は、アプリケーションサーバー上でのみ1回実行できます。 リソースを同期した後、**postupgrade**&#x200B;コマンドを使用して、同期でエラーが発生したか警告が発生したかを検出できます。

## 移行ツール{#migration-tools}

様々なオプションを使用して、移行による影響を測定し、潜在的な問題を特定できます。 以下のオプションが実行されます。

* を設定します。****

   ```
   nlserver.exe config <option> -instance:<instanceName>
   ```

* またはアップグレード後：

   ```
   nlserver.exe config -postupgrade <option> -instance:<instanceName>
   ```

>[!NOTE]
>
>**-instance:`<instanceame>`**&#x200B;オプションを使用する必要があります。 **-allinstances**&#x200B;オプションは使用しないことをお勧めします。

### -showCustomEntitiesと —showDeletedEntitiesのオプション{#showcustomentities-and--showdeletedentities-options}

* **-showCustomEntities**&#x200B;オプションは、次の非標準オブジェクトのリストを表示します。

   ```
   nlserver.exe config -showCustomEntities -instance:<instanceName>
   ```

   送信済みメッセージの例：

   ```
   xtk_migration:opsecurity2 xtk:entity
   ```

* **-showDeletedEntities**&#x200B;オプションは、データベースまたはファイルシステムに存在しないすべての標準オブジェクトのリストを表示します。 見つからない各オブジェクトに対して、パスが指定されます。

   ```
   nlserver.exe config -showDeletedEntities -instance:<instanceName>
   ```

   送信済みメッセージの例：

   ```
   Out of the box object 'nms:deliveryCustomizationMdl' belonging to the 'xtk:srcSchema' schema has not been found in the file system.
   ```

### 検証プロセス{#verification-process}

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
   <td> このタイプの構文は、配信のパーソナライゼーションではサポートされなくなりました。 <a href="../../migration/using/general-configurations.md#javascript" target="_blank">JavaScript</a>を参照してください。 それ以外の場合は、値の型が正しいかどうかを確認します。<br /> </td> 
  </tr> 
  <tr> 
   <td> common.js<br /> </td> 
   <td> PU-0002<br /> </td> 
   <td> 警告<br /> </td> 
   <td> このライブラリは使用できません。<br /> </td> 
  </tr> 
  <tr> 
   <td> logon(<br /> </td> 
   <td> PU-0003<br /> </td> 
   <td> 警告<br /> </td> 
   <td> この接続メソッドは使用しなくなります。 <a href="../../migration/using/general-configurations.md#identified-web-applications" target="_blank">識別されたWebアプリケーション</a>を参照してください。<br /> </td> 
  </tr> 
  <tr> 
   <td> new SoapMethodCall(<br /> </td> 
   <td> PU-0004<br /> </td> 
   <td> 警告<br /> </td> 
   <td> この関数は、<strong>sessionTokenOnly</strong>モードのセキュリティゾーンから実行されるJavaScriptコードで使用される場合にのみサポートされます。<br /> </td> 
  </tr> 
  <tr> 
   <td> sql=<br /> </td> 
   <td> PU-0005<br /> </td> 
   <td> エラー<br /> </td> 
   <td> このタイプのエラーは、移行エラーの原因となります。 <a href="../../migration/using/general-configurations.md#sqldata" target="_blank">SQLData</a>を参照してください。<br /> </td> 
  </tr> 
  <tr> 
   <td> SQLDATA<br /> </td> 
   <td> PU-0006<br /> </td> 
   <td> エラー<br /> </td> 
   <td> このタイプのエラーは、移行エラーの原因となります。 <a href="../../migration/using/general-configurations.md#sqldata" target="_blank">SQLData</a>を参照してください。 概要タイプのWebアプリケーションエラーログ（v6.02からの移行）を取得する場合は、<a href="../../migration/using/specific-configurations-in-v6-02.md#web-applications" target="_blank">Web アプリケーション</a>を参照してください。<br /> </td> 
  </tr> 
 </tbody> 
</table>

データベースとスキーマコヒーレンス・チェックも行う。

### 復元オプション{#restoration-option}

このオプションを使用すると、既に変更されている場合に、そのまま使用できるオブジェクトを復元できます。 復元された各オブジェクトに対して、変更のバックアップが選択したフォルダに保存されます。

```
nlserver.exe config -postupgrade -restoreFactory:<backupfolder> -instance:<instanceName>
```

>[!NOTE]
>
>フォルダーの絶対パスを使用し、フォルダーツリー構造を維持することを強くお勧めします。 次に例を示します。backupFolder\nms\srcSchema\billing.xml

### 移行を再開しています{#resuming-migration}

移行の失敗後にアップグレード後に再起動すると、停止した場所と同じ場所から再開されます。
