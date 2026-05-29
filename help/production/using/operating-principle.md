---
product: campaign
title: 動作の原則
description: 動作の原則
feature: Monitoring
badge-v7-prem: label="オンプレミス／ハイブリッドのみ" type="Caution" url="https://experienceleague.adobe.com/docs/campaign-classic/using/installing-campaign-classic/architecture-and-hosting-models/hosting-models-lp/hosting-models.html?lang=ja" tooltip="オンプレミスデプロイメントとハイブリッドデプロイメントにのみ適用されます"
audience: production
content-type: reference
topic-tags: production-procedures
exl-id: 1c032ef9-af11-4947-90c6-76cb9434ae85
TQID: https://experienceleague.adobe.com/HCoIXlpEtxAHVh-rj51UD1GTNRnXh8Ir8x4t3QZT9YU
product_v2:
  - id: dfc56824-e8b9-499e-85d4-21aedb507314
feature_v2:
  - id: b12f6872-9271-4369-85e5-86969a0b99a2
  - id: b82389f8-9b5e-4083-8e3b-3cef299fb8b9
  - id: c5474392-5419-4296-9e41-f6f4ce4f6e9b
subfeature_v2:
  - id: c03a11ff-bdf9-4e5b-b279-f468b4293464
  - id: e519a22f-a06a-42fc-9d09-d78a3ab2c434
topic_v2:
  - id: eddd9b14-83bd-4ff4-9072-54a4a484abb7
source-git-commit: 38eab6b8da73163e4476e91c0ef73f25c3f57546
workflow-type: tm+mt
source-wordcount: 530
ht-degree: 15%

---

# 動作の原則{#operating-principle}



Adobe Campaignは、技術的にはいくつかのモジュールを基盤としています。

Adobe Campaignには多くのモジュールがあります。 一部のツールは継続的に動作しますが、一部のツールは管理タスク（データベース接続の設定など）を実行したり、繰り返しタスク（トラッキング情報の統合など）を実行したりするために一時的に起動されます。

Adobe Campaign モジュールには 3 つのタイプがあります。

* マルチインスタンスモジュール：すべてのインスタンスに対して 1 つのプロセスを実行します。 これは、次のモジュールに適用されます。**web**、**syslogd**、**trackinglogd**、**watchdog** （**config-default.xml** ファイルのアクティビティ）。
* モノインスタンスモジュール：インスタンスごとに 1 つのプロセスを実行します。 これは、次のモジュールに適用されます。**mta**、**wfserver**、**inMail**、**sms**、**stat** （**config-`<instance>`.xml** ファイルのアクティビティ）。
* ユーティリティモジュール：これらは、時折または繰り返しの操作（**cleanup**、**config**、トラッキングログのダウンロードなど）を実行するために実行されるモジュールです。

モジュール管理は、インストールフォルダーの&#x200B;**bin** ディレクトリにインストールされているコマンドラインツール **nlserver**&#x200B;を使用して実行します。

**nlserver** ツールの一般的な構文は次のとおりです。

**nlserver `<command>` `<command arguments>`**

使用可能なモジュールのリストについては、**nlserver** コマンドを使用してください。

使用可能なモジュールについて詳しくは、次の表を参照してください。

| コマンド | 説明 |
|---|---|
| aliasCleansing | 列挙値の標準化 |
| billing | システムアクティビティレポートをbilling@neolane.netに送信しています |
| cleanup | データベースのクレンジング：データベースから古いデータを削除し、データベースエンジンオプティマイザーが使用する統計の更新を実行します。 |
| 設定 | サーバー設定の変更 |
| エクスポート | コマンドラインへの書き出し：Adobe Campaign クライアントコンソールで作成された書き出しモデルをコマンドラインに送信できます |
| fileconvert | セットサイズファイルの変換 |
| 読み込み | コマンドラインへのインポート：Adobe Campaign クライアントコンソールで作成したインポートモデルをコマンドラインに送信できます。 |
| inMail | インバウンドメールアナライザー |
| installsetup | お客様のインストールファイルの可用性 |
| javascript | SOAP APIにアクセスしながら、JavaScriptスクリプトを実行。 |
| ジョブ | コマンドライン処理 |
| 結合 | フォーム結合 |
| midSourcing | ミッドソーシングモードでの配信情報の回復 |
| モニター | XML サーバープロセスとスケジュールされたタスクのステータスをインスタンス別に表示します。 |
| MTA | メインエージェント転送メッセージ |
| パッケージ | エンティティパッケージファイルの読み込みや書き出し |
| ポンプ | サーバープロセスのステータスの表示 |
| prepareda | 配信アクションの準備 |
| 再起動 | サーバーの部分的な再起動 |
| runwf | ワークフローインスタンスの実行 |
| 停止 | システムの完全なシャットダウン |
| SMS | SMS通知処理 |
| sql | SQL スクリプトの実行 |
| 開始 | その他の開始 |
| 統計 | MTA 接続統計を維持 |
| 停止 | 部分的なシステムシャットダウン |
| submitda | 配信アクションの送信 |
| syslogd | ログおよびトレース書き込みサーバー |
| tracking | トラッキングログの統合と取得 |
| trackinglogd | ログの書き込みとパージ サーバーのトラッキング |
| ウォッチドッグ | 起動と監視のインスタンス |
| Web | アプリケーションサーバー（HTTPおよびSOAP） |
| wfserver | ワークフローサーバー |

>[!IMPORTANT]
>
>最後の1つのモジュールは、アプリケーションサーバーにリンクされたトラッキングおよびリレーモジュールです。このモジュールは、パフォーマンスのために、ネイティブメカニズムを介してダイナミックライブラリを介してApacheまたはIIS web サーバーに統合されます。 このモジュールを起動または管理できるAdobe Campaign コマンドはありません。 したがって、Web サーバー自体のコマンドを使用する必要があります。

モジュールの使用状況とそのパラメーターの構文は、次のコマンドを使用して表示されます。**nlserver `[module]` -?**

例：

**nlserver設定 – ?**

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
