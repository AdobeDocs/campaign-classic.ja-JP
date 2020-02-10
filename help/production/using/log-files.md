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
index: y
internal: n
snippet: y
translation-type: tm+mt
source-git-commit: 9f018df9a2f7516b92f1f25a757065ef268136a5

---


# ログファイル{#log-files}

ログファイルは次のように整理されます。

![](assets/d_ncs_directory.png)

各nlserver **モジュールは** 、次のディレクトリに保存されたログファイルを生成します。 **`<installation directory>`/var/`<instance>`/log/`<module>`.log **.

nlserver syslogd **モジュールは** 、ログをディスクに保存します。 このモジュールはUnixの **syslogデーモンに似ています**&#x200B;が、UnixとWindowsの互換性を考慮したものです。 他のAdobe Campaignモジュールは、ログをディスクに保存しません。このタスクは、UDPパケットを送 **信して** 、syslogdモジュールに委任します。

デフォルトでは、Adobe Campaignプラットフォームには **syslogd** モジュールがインストールされていますが、別の **syslogデーモンを使用できます**。 このモジュールは、ログディレクトリにログファイルを **作成します** 。

マルチインスタンスモジュールのログは、次のディレクトリに保存されます。 **`<installation directory>`/var/default/log/**. 同じログファイルは、すべてのインスタンス(**web.log **)で共有されます。

その他のモジュールのログは、インスタンスの名前を付けたサブフォルダーに保存されます。 各インスタンスには独自のログファイルがあります。

次の表に、マルチインスタンスのログファイルを示します。

| ファイル | 説明 |
|---|---|
| web.log | Webモジュールログ（クライアントコンソール、レポート、SOAP APIなど） |
| webmdl.log | リダイレクトモジュールからのログ |
| watchdog.log | Adobe Campaignプロセス監視モジュールからのログ |
| trackinglogd.log | トラッキングログ |

モノラルインスタンスのログファイルを次の表に示します。

| ファイル | 説明 |
|---|---|
| mta.log | mtaモジュールログ |
| mtachild.log | メッセージ配信処理ログ |
| wfserver.log | ワークフローサーバーモジュールのログ |
| runwf.log | ワークフローの実行ログ |
| inMail.log | バウンスメールモジュールログ |
| logins.log | Adobe Campaignへのすべてのログイン試行をログに記録します（成功または失敗）。 |

>[!CAUTION]
>
>redirディレ **クトリは** 、リダイレクトサーバー上にのみ存在します。 urlサブデ **ィレクトリには** 、リダイレクトするURLと一致するURLが格納され、サブディレクトリログには **トラッキング** ログが格納されます。 トラッキングログを生成するには、 **trackinglogdモジュール** が実行中である必要があります。

パフォーマンスとストレージの最適化のために、logins.logファイルは複数のファイルに分割され、毎日1つ(logins.yy-mm-dd.log)のファイルが保持されます。最大365個のファイルが保持されます。 日数は、serverConf.xmlのsyslogd(**maxNumberOfLoginsFiles** option)で変更できます。 サーバー設定ファイルのドキュメ [ントを参照してくださ](../../installation/using/the-server-configuration-file.md#syslogd)い。

デフォルトでは、ログはモジュールごととインスタンスごとに2つの10 MBのファイルに制限されます。 2つ目のファイルは次のように呼び出されます。 **`<modulename>`_2.log **. したがって、ログのサイズはモジュールごとおよびインスタンスごとに2*10 MBに制限されます。

ただし、大きいファイルは保持できます。 これを有効にするには、conf/serverConf.xmlファイルの **syslogd** ノードのmaxFileSizeMb=&quot;10&quot;設定の **値を変更****** します。 この値は、ログファイルの最大サイズ（MB単位）を表します。

ログの詳細レベルをさらに維持する場合は、 **-verboseパラメーターを使用してAdobe Campaignモジュールを起動で** きます。

**nlserver start`<MODULE>`@`<INSTANCE>`-verbose**
