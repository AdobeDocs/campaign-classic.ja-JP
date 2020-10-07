---
title: ログファイル
seo-title: ログファイル
description: ログファイル
seo-description: null
page-status-flag: never-activated
uuid: 266bc067-0218-4b3e-941c-dc5cd0b6a10d
contentOwner: sauviat
products: SG_CAMPAIGN/CLASSIC
audience: production
content-type: reference
topic-tags: production-procedures
discoiquuid: fac3e3ec-82a7-4087-ba88-2b28b0f69d1c
translation-type: tm+mt
source-git-commit: 70b143445b2e77128b9404e35d96b39694d55335
workflow-type: tm+mt
source-wordcount: '433'
ht-degree: 3%

---


# ログファイル{#log-files}

ログファイルは、次のように整理されます。

![](assets/d_ncs_directory.png)

各 **nlserver** モジュールは、次のディレクトリに保存されたログファイルを生成します。 **`<installation directory>`/var/`<instance>`/log/`<module>`.log**.

nlserver syslogd **** モジュールは、ログをディスクに保存します。 このモジュールはUnixの **syslogデーモンに似ていますが**、UnixとWindowsの互換性に対応しています。 他のAdobe Campaignモジュールは、ログをディスクに保存しません。このタスクは、UDPパケットを送信することで **syslogd** モジュールに委任されます。

デフォルトでは、Adobe Campaignプラットフォームには **syslogd** モジュールがインストールされていますが、別の **syslogデーモンを使用することも可能です**。 このモジュールは、 **log** ディレクトリにログファイルを作成します。

マルチインスタンスモジュールのログは、次のディレクトリに保存されます。 **`<installation directory>`/var/default/log/**. 同じログファイルがすべてのインスタンス( **web.log**)で共有されます。

他のモジュールのログは、インスタンスの名前を付けたサブフォルダーに保存されます。 各インスタンスには、独自のログファイルがあります。

マルチインスタンスのログファイルを次の表に示します。

| ファイル | 説明 |
|---|---|
| web.log | Webモジュールログ（クライアントコンソール、レポート、SOAP APIなど） |
| webmdl.log | リダイレクトモジュールからのログ |
| watchdog.log | Adobe Campaignプロセス監視モジュールからのログ |
| trackinglogd.log | トラッキングログ |

モノインスタンスログファイルを次の表に示します。

| ファイル | 説明 |
|---|---|
| mta.log | mtaモジュールログ |
| mtachild.log | メッセージ配信の処理ログ |
| wfserver.log | ワークフローサーバーモジュールのログ |
| runwf.log | ワークフローの実行ログ |
| inMail.log | バウンスメールモジュールログ |
| logins.log | Adobe Campaignに対するすべてのログイン試行をログに記録します（成功したかどうか） |

>[!CAUTION]
>
>redir **** ディレクトリは、リダイレクトサーバーにのみ存在します。 url **サブディレクトリには、リダイレクトするURLと一致するURLが含まれ、サブディレクトリ** ログにはトラッキングログが含まれます **** 。 トラッキングログを生成するには、 **trackinglogd** モジュールが実行されている必要があります。

パフォーマンスとストレージの最適化のために、logins.logファイルは複数のファイルに分割され、毎日1つ(logins.yy-mm-dd.log)が保持されます。最大365個のファイルが保持されます。 日数は、syslogd(**maxNumberOfLoginsFiles** オプション)の下のserverConf.xmlで変更できます。 サー [バー設定ファイルのドキュメントを参照してください](../../installation/using/the-server-configuration-file.md#syslogd)。

デフォルトでは、ログの10 MBのファイルはモジュールあたり2個、インスタンスあたり2個に制限されます。 2つ目のファイルは次のように呼び出されます。 **`<modulename>`_2.log**. したがって、ログのサイズは、モジュールあたり2*10 MBまたはインスタンスあたりに制限されます。

ただし、大きいファイルは保持できます。 これを有効にするには、conf/serverConf.xml **ファイルの** syslogd **ノードのmaxFileSizeMb=&quot;10&quot;** 設定を変更し **** ます。 この値は、ログファイルの最大サイズ（MB単位）を表します。

ログの詳細レベルをさらに高く維持したい場合は、 **-verbose** パラメータを使用してAdobe Campaignモジュールを開始できます。

**nlserver開始`<MODULE>`@`<INSTANCE>`-verbose**
