---
product: campaign
title: 動作の原則
description: 動作の原則
audience: production
content-type: reference
topic-tags: production-procedures
exl-id: 1c032ef9-af11-4947-90c6-76cb9434ae85
source-git-commit: 98d646919fedc66ee9145522ad0c5f15b25dbf2e
workflow-type: tm+mt
source-wordcount: '500'
ht-degree: 10%

---

# 動作の原則{#operating-principle}

技術的には、Adobe Campaignプラットフォームは複数のモジュールに基づいています。

Adobe Campaignモジュールは多数あります。 継続的に動作するタスクもあれば、管理タスク（データベース接続を設定する場合など）を実行するために起動するタスクもあれば、繰り返し実行するタスク（トラッキング情報の統合など）もあります。

Adobe Campaign モジュールには 3 つのタイプがあります。

* マルチインスタンスモジュール：すべてのインスタンスに対して 1 つのプロセスを実行します。 これは、次のモジュールに適用されます。**web**、**syslogd**、**trackinglogd**&#x200B;および&#x200B;**ウォッチドッグ**（**config-default.xml**&#x200B;ファイルのアクティビティ）。
* モノインスタンスモジュール：インスタンスごとに 1 つのプロセスを実行します。 これは、次のモジュールに適用されます。**mta**、**wfserver**、**inMail**、**sms**、**stat**（**config-`<instance>`.xml**&#x200B;ファイルのアクティビティ）。
* ユーティリティモジュール：これらは、時々実行され、不定期または繰り返し操作（**cleanup**、**config**、トラッキングログのダウンロードなど）を実行するモジュールです。

モジュールの管理は、インストールフォルダーの&#x200B;**bin**&#x200B;ディレクトリにインストールされたコマンドラインツール&#x200B;**nlserver**&#x200B;を使用して実行します。

**nlserver**&#x200B;ツールの一般的な構文は次のとおりです。

**nlserver  `<command>``<command arguments>`**

使用可能なモジュールのリストには、**nlserver**&#x200B;コマンドを使用します。

使用可能なモジュールについて、次の表で詳しく説明します。

| コマンド | 説明 |
|---|---|
| aliasCleansing | 列挙値の標準化 |
| billing | システムアクティビティレポートをbilling@neolane.netに送信する |
| cleanup | データベースのクレンジング：データベースから古いデータを削除し、データベースエンジンオプティマイザが使用する統計の更新を実行します。 |
| config | サーバー設定の変更 |
| copybase | データベースのコピー |
| エクスポート | コマンドラインに書き出し中：Adobe Campaignクライアントコンソールで作成した書き出しモデルをコマンドラインに送信できます。 |
| fileconvert | 設定サイズのファイルの変換 |
| import | コマンドラインに読み込み中：Adobe Campaignクライアントコンソールで作成したインポートモデルをコマンドラインに送信できます。 |
| inMail | 受信メールアナライザー |
| installsetup | 顧客インストールファイルの可用性 |
| javascript | SOAP APIへのアクセス権を持つJavaScriptスクリプトの実行 |
| ジョブ | コマンドライン処理 |
| 結合 | フォームの結合 |
| midSourcing | ミッドソーシングモードでの配信情報の復元 |
| モニター | XMLサーバープロセスとスケジュールされたタスクのステータスをインスタンス別に表示します。 |
| MTA | メインエージェント転送メッセージ |
| 荷物 | エンティティパッケージファイルのインポートまたはエクスポート |
| pdump | サーバープロセスのステータスの表示 |
| prepareda | 配信アクションの準備 |
| 再起動 | サーバーの部分的な再起動 |
| runwf | ワークフローインスタンスの実行 |
| 停止 | システムの完全シャットダウン |
| SMS | SMS通知処理 |
| sql | SQL スクリプトの実行 |
| 開始 | 追加の開始 |
| stat | MTA 接続統計を維持 |
| 停止 | システムの一部シャットダウン |
| 亜密 | 配信アクションの送信 |
| syslogd | ログとトレース書き込みサーバー |
| tracking | トラッキングログの統合と取得 |
| trackinglogd | トラッキングログの書き込みとサーバーのパージ |
| ウォッチ | 起動および監視インスタンス |
| Web | アプリケーションサーバー（HTTPおよびSOAP） |
| wfserver | ワークフローサーバー |

>[!IMPORTANT]
>
>最後のモジュールは1つあります。パフォーマンスを考慮して、アプリケーションサーバーにリンクされたトラッキングとリレーモジュールは、ネイティブメカニズムを介してダイナミックライブラリを介してApacheまたはIIS Webサーバーに統合されます。 このモジュールを開始または管理できるAdobe Campaignコマンドはありません。 したがって、Webサーバー自体のコマンドを使用する必要があります。

モジュールの使用と、そのパラメーターの構文は、次のコマンドを使用して表示されます。**nlserver `[module]` -?**

例：

**nlserver設定 —?**

```
Usage: nlserver [-verbose:<verbose mode>] [-?|h|H] [-version] [-noconsole]
 [-tracefile:<file>] [-tracefilter:<[type|!type],...>]
 [-instance:<instance>] [-low] [-high] [-queryplans] [-detach]
 [-internalpassword:<[password/newpassword]>] [-postupgrade]
 [-nogenschema] [-force] [-allinstances]
 [-addinstance:<instance/DNS masks[/language]>]
 [-setdblogin:<[dbms:]account[:database][/password]@server>]
 [-monoinstance]
 [-addtrackinginstance:<instance/masks DNS[/databaseId/[/language[/password]]]>]
 [-trackingpassword:<[password][/newpassword]>]
 [-setproxy:<protocol/server:port[/login]>] [-reload]
 [-applyxsl:<schema/file.xsl>] [-filter:<file>]
 [-setactivationkey:<activation key>]
 [-getactivationkey:<client identifier>]
-verbose : verbose mode
-? : display this help message
-version : display version number
-noconsole : no longer display logs and traces on the console
-tracefile : name of trace file to be generated (without extension)
-tracefilter : filter for the traces to be generated e.g.: wdbc,soap,!xtkquery.
-instance : instance to be used (default instance if this option is not present).
-low : start up with low priority
-high : start up with high priority (not recommended)
-queryplans : generate traces with the execution plans of SQL queries.
-detach : detaches the process from its parent (internal option)
-internalpassword : changes the password of the server internal account.
-postupgrade : updates the database following upgrade to a higher version. 
-nogenschema : does not recompute the schemas during database update
-force : updates the database even if this has already been done with the current build 
-allinstances : updates the database over all configured instances
-addinstance : adds a new instance.
-setdblogin : sets the parameters for connection to the database of an instance. The DBMS can be 'oracle', 'postgresql', 'mssql' or 'odbc' (default=postgresql)
-monoinstance : initialises for a single instance ().
-addtrackinginstance : adds a new tracking instance.
-trackingpassword : changes the tracking password of an instance
-setproxy : sets the parameters for connection to a proxy server. The protocol can be 'http', 'https' or 'all'.
-reload : asks the server to reload the configuration of the instances. 
-applyxsl : applies an XSL stylesheet to all entities of a schema. 
-filter : applies the XTK filter contained in the file during loading of the schema entities.
-setactivationkey : sets the activation key
```
