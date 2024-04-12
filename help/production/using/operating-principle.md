---
product: campaign
title: 動作の原則
description: 動作の原則
feature: Monitoring
badge-v7-prem: label="オンプレミス/ハイブリッドのみ" type="Caution" url="https://experienceleague.adobe.com/docs/campaign-classic/using/installing-campaign-classic/architecture-and-hosting-models/hosting-models-lp/hosting-models.html?lang=ja" tooltip="オンプレミスデプロイメントとハイブリッドデプロイメントにのみ適用されます"
audience: production
content-type: reference
topic-tags: production-procedures
exl-id: 1c032ef9-af11-4947-90c6-76cb9434ae85
source-git-commit: 14ba450ebff9bba6a36c0df07d715b7279604222
workflow-type: tm+mt
source-wordcount: '506'
ht-degree: 11%

---

# 動作の原則{#operating-principle}



技術的には、Adobe Campaign プラットフォームは、複数のモジュールに基づいています。

Adobe Campaignには多くのモジュールがあります。 連続して実行されるものもあれば、一時的に起動するものもあります。一時的に起動して、管理タスク（データベース接続の設定など）や繰り返しタスク（トラッキング情報の統合など）を実行するタスクもあります。

Adobe Campaign モジュールには 3 つのタイプがあります。

* マルチインスタンスモジュール：すべてのインスタンスに対して 1 つのプロセスを実行します。 これは、次のモジュールに適用されます。 **web**, **syslogd**, **trackinglogd** および **ウォッチドッグ** （の活動 **config-default.xml** ファイル）に含まれます。
* モノインスタンスモジュール：インスタンスごとに 1 つのプロセスを実行します。 これは、次のモジュールに適用されます。 **mta**, **wfserver**, **inMail**, **sms** および **統計** （の活動 **config-`<instance>`.xml** ファイル）に含まれます。
* ユーティリティモジュール：一時的に起動するモジュールです。一時的な操作や繰り返しの操作（**クリーンアップ**, **config**、トラッキングログのダウンロードなど）。

モジュール管理は、コマンドラインツールを使用して実行します **nlserver** にインストールされています **bin** インストールフォルダーのディレクトリ。

の一般構文 **nlserver** ツールは次のとおりです。

**nlserver `<command>``<command arguments>`**

使用可能なモジュールのリストについては、 **nlserver** コマンド。

使用可能なモジュールについて詳しくは、次の表を参照してください。

| コマンド | 説明 |
|---|---|
| aliasCleansing | 列挙値の標準化 |
| billing | billing@neolane.netへのシステムアクティビティレポートの送信 |
| cleanup | データベースのクレンジング：データベースから古いデータを削除し、データベースエンジンオプティマイザーで使用される統計の更新を実行します。 |
| config | サーバー設定の変更 |
| エクスポート | コマンドラインへの書き出し：Adobe Campaign クライアントコンソールで作成した書き出しモデルをコマンドラインに送信できます。 |
| fileconvert | セットサイズファイルの変換 |
| 読み込み | コマンドラインへの読み込み：Adobe Campaign クライアントコンソールで作成した読み込みモデルをコマンドラインに送信できます。 |
| inMail | 受信メール分析 |
| installsetup | カスタマーインストールファイルの可用性 |
| javascript | SOAP API にアクセスして JavaScript スクリプトを実行 |
| ジョブ | コマンドライン処理 |
| 結合 | フォームの結合 |
| ミッドソーシング | ミッドソーシングモードでの配信情報の回復 |
| モニタ | XML サーバープロセスおよびスケジュールされたタスクのステータスをインスタンスごとに表示します。 |
| MTA | メインエージェント転送メッセージ |
| package | エンティティパッケージファイルのインポートまたはエクスポート |
| pdump | サーバープロセスのステータスの表示 |
| 準備 | 配信アクションの準備 |
| 再起動 | 部分的なサーバーの再起動 |
| runwf | ワークフローインスタンスの実行 |
| 停止 | システム全体のシャットダウン |
| SMS | SMS 通知処理 |
| sql | SQL スクリプトの実行 |
| 開始 | 追加の開始 |
| 統計 | MTA 接続統計を維持 |
| 停止 | 部分的なシステム停止 |
| submitda | 配信アクションの送信 |
| syslogd | ログおよびトレース書き込みサーバー |
| tracking | トラッキングログの統合と取得 |
| trackinglogd | トラッキングログの書き込みおよびパージサーバー |
| ウォッチドッグ | 起動および監視インスタンス |
| Web | アプリケーションサーバー（HTTP および SOAP） |
| wfserver | ワークフローサーバー |

>[!IMPORTANT]
>
>最後にモジュールが 1 つあります。アプリケーションサーバーにリンクされたトラッキングモジュールとリレーモジュールです。このモジュールは、パフォーマンスを向上させるために、ネイティブメカニズムを介して動的ライブラリを介して Apache または IIS web サーバーに統合されます。 このモジュールを開始または管理できるAdobe Campaign コマンドはありません。 したがって、Web サーバー自体のコマンドを使用する必要があります。

次のコマンドを使用すると、モジュールの使用状況とそのパラメーターの構文が表示されます。 **nlserver `[module]` -?**

例：

**nlserver 構成 – ?**

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
