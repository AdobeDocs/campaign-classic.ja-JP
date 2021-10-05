---
product: campaign
title: 動作原理
description: 動作原理
audience: production
content-type: reference
topic-tags: production-procedures
exl-id: 1c032ef9-af11-4947-90c6-76cb9434ae85
source-git-commit: bd9f035db1cbad883e1f27fe901e34dfbc9c1229
workflow-type: tm+mt
source-wordcount: '500'
ht-degree: 10%

---

# 動作原理{#operating-principle}

![](../../assets/v7-only.svg)

技術的には、Adobe Campaignプラットフォームは複数のモジュールに基づいています。

Adobe Campaignモジュールは多数あります。 継続的に動作する場合もあれば、管理タスク（データベース接続を設定する場合など）を実行する場合や、繰り返し実行するタスク（追跡情報の統合など）を実行する場合に起動する場合もあります。

Adobe Campaign モジュールには 3 つのタイプがあります。

* マルチインスタンスモジュール：すべてのインスタンスに対して 1 つのプロセスを実行します。 これは、次のモジュールに当てはまります。**web**、**syslogd**、**trackinglogd** および **watchdog**（**config-default.xml** ファイルのアクティビティ）。
* モノインスタンスモジュール：インスタンスごとに 1 つのプロセスを実行します。 これは、次のモジュールに当てはまります。**mta**、**wfserver**、**inMail**、**sms**、**stat**（**config-`<instance>`.xml** ファイルのアクティビティ）。
* ユーティリティモジュール：これらは、時々実行され、時々または繰り返し実行される操作（**cleanup**、**config**、トラッキングログのダウンロードなど）を実行するモジュールです。

モジュールの管理は、インストールフォルダーの **bin** ディレクトリにインストールされたコマンドラインツール **nlserver** を使用して実行します。

**nlserver** ツールの一般的な構文は次のとおりです。

**nlserver  `<command>``<command arguments>`**

使用可能なモジュールのリストには、**nlserver** コマンドを使用します。

次の表に、使用可能なモジュールの詳細を示します。

| コマンド | 説明 |
|---|---|
| aliasCleansing | 列挙値の標準化 |
| billing | システムアクティビティレポートをbilling@neolane.netに送信 |
| cleanup | データベースのクレンジング：データベースから古いデータを削除し、データベースエンジンオプティマイザが使用する統計の更新を実行します。 |
| config | サーバー設定の変更 |
| copybase | データベースのコピー |
| エクスポート | コマンドラインに書き出し中：Adobe Campaignのクライアントコンソールで作成した書き出しモデルをコマンドラインに送信できます。 |
| fileconvert | 設定サイズのファイルの変換 |
| インポート | コマンドラインに読み込み中：を使用すると、Adobe Campaignクライアントコンソールで作成したインポートモデルをコマンドラインに送信できます。 |
| inMail | 受信メール分析 |
| installsetup | 顧客インストールファイルの可用性 |
| javascript | SOAP API へのアクセス権を持つ JavaScript スクリプトを実行する。 |
| ジョブ | コマンドライン処理 |
| 結合 | フォームの結合 |
| midSourcing | ミッドソーシングモードでの配信情報の復元 |
| モニター | XML サーバープロセスとスケジュールされたタスクのステータスをインスタンス別に表示します。 |
| MTA | メインエージェント転送メッセージ |
| 荷物 | エンティティパッケージファイルのインポートまたはエクスポート |
| pdump | サーバープロセスのステータスの表示 |
| prepareda | 配信アクションの準備 |
| 再起動 | サーバーの部分的な再起動 |
| runwf | ワークフローインスタンスの実行 |
| 停止 | システムの完全シャットダウン |
| SMS | SMS 通知処理 |
| sql | SQL スクリプトの実行 |
| 開始 | 追加の開始 |
| stat | MTA 接続統計を維持 |
| 停止 | システムの一部シャットダウン |
| 提出者 | 配信アクションの送信 |
| syslogd | ログおよびトレース書き込みサーバー |
| tracking | トラッキングログの統合と取得 |
| trackinglogd | トラッキングログの書き込みとサーバーのパージ |
| 監視 | 起動および監視インスタンス |
| Web | アプリケーションサーバー（HTTP および SOAP） |
| wfserver | ワークフローサーバー |

>[!IMPORTANT]
>
>最後のモジュールが 1 つあります。パフォーマンスを考慮して、ネイティブメカニズムを介して動的ライブラリを介して Apache または IIS Web サーバーに統合される、アプリケーションサーバーにリンクされたトラッキングおよびリレーモジュール。 このモジュールを開始または管理できるAdobe Campaignコマンドはありません。 したがって、Web サーバー自体のコマンドを使用する必要があります。

モジュールの使用と、そのパラメーターの構文は、次のコマンドを使用して表示されます。**nlserver `[module]` -?**

例：

**nlserver 設定 —?**

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
-monoinstance : initializes for a single instance ().
-addtrackinginstance : adds a new tracking instance.
-trackingpassword : changes the tracking password of an instance
-setproxy : sets the parameters for connection to a proxy server. The protocol can be 'http', 'https' or 'all'.
-reload : asks the server to reload the configuration of the instances. 
-applyxsl : applies an XSL stylesheet to all entities of a schema. 
-filter : applies the XTK filter contained in the file during loading of the schema entities.
-setactivationkey : sets the activation key
```
