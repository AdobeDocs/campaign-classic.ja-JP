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

各 **nlserver** モジュールは、次のディレクトリに保存されたログファイルを生成します。 **`<installation directory>`/var/`<instance>`/log/`<module>`.log**.

この **nlserver syslogd** モジュールはログをディスクに保存します。 このモジュールは Unix に似ています。 **syslog デーモン**&#x200B;を使用していますが、UNIX と Windows の互換性を確保するために変更されています。 その他のAdobe Campaign・モジュールは、ログをディスクに保存しません。彼らはこのタスクをに委任する **syslogd** モジュールに送信します。

デフォルトでは、Adobe Campaignプラットフォームには **syslogd** モジュールがインストールされていますが、別のモジュールを使用することも可能です **syslog デーモン**. このモジュールは、 **ログ** ディレクトリ。

マルチインスタンスモジュールのログは、次のディレクトリに保存されます。 **`<installation directory>`/var/default/log/**. 同じログファイルがすべてのインスタンスで共有されます ( 例： **web.log**) をクリックします。

他のモジュールのログは、インスタンスの名前を持つサブフォルダーに保存されます。 各インスタンスには独自のログファイルがあります。

マルチインスタンスログファイルを次の表に示します。

| ファイル | 説明 |
|---|---|
| web.log | Web モジュールログ（クライアントコンソール、レポート、SOAP API など） |
| webmdl.log | リダイレクトモジュールからのログ |
| watchdog.log | Adobe Campaign Process Monitoring モジュールからのログ |
| trackinglogd.log | トラッキングログ |

次の表に、モノラルインスタンスログファイルを示します。

| ファイル | 説明 |
|---|---|
| mta.log | mta モジュールログ |
| mtachild.log | メッセージ配信処理ログ |
| wfserver.log | ワークフローサーバーモジュールのログ |
| runwf.log | ワークフロー実行ログ |
| inMail.log | バウンスメールモジュールのログ |
| logins.log | Adobe Campaignへのログイン試行をすべて記録します（成功または失敗） |

>[!IMPORTANT]
>
>この **redir** ディレクトリはリダイレクトサーバー上にのみ存在します。 この **url** サブディレクトリには、リダイレクトする URL とサブディレクトリの一致が含まれます。 **ログ** には、トラッキングログが含まれます。 トラッキングログを生成するには、 **trackinglogd** モジュールを実行する必要があります。

パフォーマンスとストレージを最適化するために、 logins.log ファイルは複数のファイルに分割され、1 日に 1 つ (logins.yy-mm-dd.log)、最大 365 個のファイルが保持されます。 日数は、serverConf.xml の syslogd (**maxNumberOfLoginsFiles** オプション )。 詳しくは、 [サーバー設定ファイル](../../installation/using/the-server-configuration-file.md#syslogd).

デフォルトでは、ログはモジュールごととインスタンスごとに 2 つの 10 MB のファイルに制限されます。 2 つ目のファイルの名前は次のようになります。 **`<modulename>`_2.log**. したがって、ログのサイズは、モジュールごとおよびインスタンスごとに 2*10 MB に制限されます。

ただし、大きなファイルを保持することはできます。 これを有効にするには、 **maxFileSizeMb=&quot;10&quot;** 設定 **syslogd** ノード **conf/serverConf.xml** ファイル。 この値は、ログファイルの最大サイズ (MB) を表します。

ログの詳細レベルをさらに維持する場合は、Adobe Campaignモジュールを **-verbose** パラメーター：

**nlserver start `<MODULE>`@`<INSTANCE>` -verbose**
