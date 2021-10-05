---
product: campaign
title: ログファイル
description: ログファイル
audience: production
content-type: reference
topic-tags: production-procedures
exl-id: c9d427da-6965-4945-90f0-d0770701d55e
source-git-commit: bd9f035db1cbad883e1f27fe901e34dfbc9c1229
workflow-type: tm+mt
source-wordcount: '431'
ht-degree: 2%

---

# ログファイル{#log-files}

![](../../assets/v7-only.svg)

ログファイルは次のように整理されます。

![](assets/d_ncs_directory.png)

各 **nlserver** モジュールは、次のディレクトリに保存されたログファイルを生成します。**`<installation directory>`/var/`<instance>`/log/`<module>`.log**

**nlserver syslogd** モジュールは、ログをディスクに保存します。 このモジュールは Unix の **syslog デーモン** に似ていますが、Unix と Windows の互換性を保つように変更されています。 他のAdobe Campaignモジュールは、ログをディスクに保存しません。このタスクは、UDP パケットを送信することで **syslogd** モジュールに委任されます。

デフォルトでは、Adobe Campaignプラットフォームには **syslogd** モジュールがインストールされていますが、別の **syslog デーモン** を使用することもできます。 このモジュールは、**log** ディレクトリにログファイルを作成します。

マルチインスタンスモジュールのログは、次のディレクトリに保存されます。**`<installation directory>`/var/default/log/**. 同じログファイルがすべてのインスタンスで共有されます ( 例：**web.log**) と同じです。

その他のモジュールのログは、インスタンスの名前を取ったサブフォルダーに保存されます。 各インスタンスには、独自のログファイルがあります。

次の表に、複数インスタンスのログファイルを示します。

| ファイル | 説明 |
|---|---|
| web.log | Web モジュールのログ（クライアントコンソール、レポート、SOAP API など） |
| webmdl.log | リダイレクトモジュールからのログ |
| watchdog.log | Adobe Campaignプロセス監視モジュールからのログ |
| trackinglogd.log | トラッキングログ |

モノラルインスタンスログファイルを次の表に示します。

| ファイル | 説明 |
|---|---|
| mta.log | mta モジュールログ |
| mtachild.log | メッセージ配信処理ログ |
| wfserver.log | ワークフローサーバーモジュールのログ |
| runwf.log | ワークフロー実行ログ |
| inMail.log | バウンスメールモジュールのログ |
| logins.log | Adobe Campaignへのすべてのログイン試行を記録します（成功/失敗）。 |

>[!IMPORTANT]
>
>**redir** ディレクトリは、リダイレクションサーバーにのみ存在します。 **url** サブディレクトリには、リダイレクトする URL に一致する URL が格納され、サブディレクトリ **log** にはトラッキングログが格納されます。 トラッキングログを生成するには、**trackinglogd** モジュールが実行されている必要があります。

パフォーマンスとストレージを最適化するために、 logins.log ファイルは複数のファイルに分割され、1 日に 1 つ (logins.yy-mm-dd.log)、最大 365 個のファイルが保持されます。 日数は、 serverConf.xml の syslogd （**maxNumberOfLoginsFiles** オプション）で変更できます。 [ サーバー設定ファイル ](../../installation/using/the-server-configuration-file.md#syslogd) のドキュメントを参照してください。

デフォルトでは、ログはモジュールごとと、インスタンスごとに 2 つの 10 MB のファイルに制限されます。 2 つ目のファイルは次のように呼び出されます。**`<modulename>`_2.log**. したがって、ログのサイズは、モジュールごとおよびインスタンスごとに 2*10 MB に制限されます。

ただし、大きなファイルは保持できます。 これを有効にするには、**conf/serverConf.xml** ファイルの **syslogd** ノードの **maxFileSizeMb=&quot;10&quot;** 設定の値を変更します。 この値は、ログファイルの最大サイズ（MB 単位）を表します。

ログの詳細レベルをさらに維持する場合は、**-verbose** パラメーターを使用してAdobe Campaignモジュールを起動できます。

**nlserver start  `<MODULE>`@`<INSTANCE>`  -verbose**
