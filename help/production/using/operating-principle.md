---
title: 動作の仕組み
seo-title: 動作の仕組み
description: 動作の仕組み
seo-description: null
page-status-flag: never-activated
uuid: a15929ca-5b1f-499a-a883-43fd0a318c98
contentOwner: sauviat
products: SG_CAMPAIGN/CLASSIC
audience: production
content-type: reference
topic-tags: production-procedures
discoiquuid: 5e9c17ad-14d2-4173-9fc9-0e48a21426c8
index: y
internal: n
snippet: y
translation-type: tm+mt
source-git-commit: 2a11a73b0679c0a65dc10f71869bf2a6c6efc008

---


# 動作の仕組み{#operating-principle}

技術的には、Adobe Campaignプラットフォームは複数のモジュールに基づいています。

Adobe Campaignモジュールは多数あります。 継続的に動作するタスクもあれば、管理タスク（データベース接続の設定など）や繰り返しタスク（追跡情報の統合など）を実行するタスクも時折起動するタスクもあります。

Adobe Campaignモジュールには3つのタイプがあります。

* マルチインスタンスモジュール：1つのプロセスがすべてのインスタンスに対して実行されます。 これは、次のモジュールに適用されます。Web **、** syslogd **、** trackinglogd **、お** よび **(** アクティビティは **** config-default.xml file)。
* モノラルインスタンスモジュール：1つのプロセスがインスタンスごとに実行されます。 これは、次のモジュールに適用されます。 **mta, wfserver**, **inMail****,** sms **sms** tast and the **stat (activities the****`<instance>`** wfserver config xmlファイルから)
* ユーティリティモジュール：これらは、時折、または繰り返し操作(クリーンアップ、**設定**、トラッキングログのダウンロード ****&#x200B;など)を実行するモジュールです。

モジュール管理は、インストールフォルダーの **binディレクトリにインストー** ルされた **** 、コマンドラインツールnlserverを使用して実行します。

nlserverツールの一般的な構 **文は** 、次のとおりです。

**nlserver`<command>``<command arguments>`**

使用可能なモジュールのリストには、 **nlserver** コマンドを使用します。

次の表に、利用可能なモジュールの詳細を示します。

| コマンド | 説明 |
|---|---|
| aliasCleansing | 列挙値の標準化 |
| billing | システムアクティビティレポートをbilling@neolane.netに送信する |
| cleanup | データベースのクレンジング：データベースから古いデータを削除し、データベースエンジンオプティマイザが使用する統計の更新を実行します。 |
| config | サーバー設定の変更 |
| copybase | データベースのコピー |
| エクスポート | コマンドラインに書き出し中：Adobe Campaignクライアントコンソールで作成したエクスポートモデルをコマンドラインに送信できます。 |
| fileconvert | 設定サイズファイルの変換 |
| インポート | コマンドラインに読み込み中：コマンドラインに、Adobe Campaignクライアントコンソールで作成したインポートモデルを送信できます。 |
| inMail | 受信メールアナライザ |
| installsetup | お客様のインストールファイルの可用性 |
| javascript | SOAP APIへのアクセス権を持つJavaScriptスクリプトを実行する。 |
| ジョブ | コマンドライン処理 |
| merge | フォームの結合 |
| midSourcing | 中間ソーシングモードでの配信情報の回復 |
| モニタ | XMLサーバープロセスとスケジュールされたタスクのステータスをインスタンス別に表示します。 |
| MTA | メインエージェント転送メッセージ |
| パッケージ | エンティティパッケージファイルの読み込みまたは書き出し |
| pdump | サーバープロセスのステータスの表示 |
| prepareda | 配信アクションの準備 |
| 再起動 | サーバーの部分的な再起動 |
| runwf | ワークフローインスタンスの実行 |
| 停止 | システムの完全シャットダウン |
| SMS | SMS通知処理 |
| sql | SQL スクリプトの実行 |
| 開始 | その他の開始 |
| stat | MTA 接続統計を維持 |
| stop | システムの一部停止 |
| submitda | 配信アクションの送信 |
| syslogd | ログとトレースの書き込みサーバー |
| tracking | トラッキングログの統合と取得 |
| trackinglogd | トラッキングログの書き込みとサーバーの削除 |
| 番犬 | 起動および監視インスタンス |
| Web | アプリケーションサーバー（HTTPおよびSOAP） |
| wfserver | ワークフローサーバー |

>[!CAUTION]
>
>最後のモジュールが1つあります。パフォーマンスを考慮して、ネイティブのメカニズムを介してダイナミックライブラリを介してApacheまたはIIS webサーバーに統合される、アプリケーションサーバーにリンクされたトラッキングおよびリレーモジュール。 このモジュールを開始または管理できるAdobe Campaignコマンドはありません。 したがって、Webサーバ自体のコマンドを使用する必要があります。

モジュールの使用状況とそのパラメーターの構文は、次のコマンドを使用して表示します。 **nlserver`[module]`-?**

例：

**nlserver config -?**

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

