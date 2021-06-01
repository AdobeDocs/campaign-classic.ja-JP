---
product: campaign
title: ログファイル
description: ログファイル
audience: production
content-type: reference
topic-tags: production-procedures
exl-id: c9d427da-6965-4945-90f0-d0770701d55e
source-git-commit: 98d646919fedc66ee9145522ad0c5f15b25dbf2e
workflow-type: tm+mt
source-wordcount: '431'
ht-degree: 2%

---

# ログファイル{#log-files}

ログファイルは次のように構成されます。

![](assets/d_ncs_directory.png)

各&#x200B;**nlserver**&#x200B;モジュールは、次のディレクトリに保存されたログファイルを生成します。**`<installation directory>`/var/`<instance>`/log/`<module>`.log**.

**nlserver syslogd**&#x200B;モジュールは、ログをディスクに保存します。 このモジュールは、Unixの&#x200B;**syslogデーモン**&#x200B;に似ていますが、UnixとWindowsの互換性を保つように変更されています。 他のAdobe Campaignモジュールでは、ログはディスクに保存されません。このタスクは、UDPパケットを送信することで&#x200B;**syslogd**&#x200B;モジュールに委任されます。

デフォルトでは、Adobe Campaignプラットフォームには&#x200B;**syslogd**&#x200B;モジュールがインストールされていますが、別の&#x200B;**syslogデーモン**&#x200B;を使用することもできます。 このモジュールは、**log**&#x200B;ディレクトリにログファイルを作成します。

マルチインスタンスモジュールのログは、次のディレクトリに格納されます。**`<installation directory>`/var/default/log/**. 同じログファイルがすべてのインスタンスで共有される(例：**web.log**)を読み込みます。

その他のモジュールのログは、インスタンスの名前を持つサブフォルダーに保存されます。 各インスタンスには、独自のログファイルがあります。

次の表に、複数インスタンスのログファイルを示します。

| ファイル | 説明 |
|---|---|
| web.log | Webモジュールのログ（クライアントコンソール、レポート、SOAP APIなど） |
| webmdl.log | リダイレクトモジュールからのログ |
| watchdog.log | Adobe Campaignプロセス監視モジュールからのログ |
| trackinglogd.log | トラッキングログ |

次の表に、モノラルインスタンスログファイルを示します。

| ファイル | 説明 |
|---|---|
| mta.log | mtaモジュールログ |
| mtachild.log | メッセージ配信処理ログ |
| wfserver.log | ワークフローサーバーモジュールのログ |
| runwf.log | ワークフロー実行ログ |
| inMail.log | バウンスメールモジュールのログ |
| logins.log | Adobe Campaignに対するすべてのログイン試行を記録します（成功か失敗かを問わず）。 |

>[!IMPORTANT]
>
>**redir**&#x200B;ディレクトリは、リダイレクトサーバー上にのみ存在します。 **url**&#x200B;サブディレクトリには、リダイレクトするURLに一致する情報が格納され、サブディレクトリ&#x200B;**log**&#x200B;にはトラッキングログが格納されます。 トラッキングログを生成するには、**trackinglogd**&#x200B;モジュールが実行されている必要があります。

パフォーマンスとストレージを最適化するために、 logins.logファイルは複数のファイルに分割され、1日に1つ(logins.yy-mm-dd.log)、最大365個のファイルが保持されます。 日数は、serverConf.xmlのsyslogd（**maxNumberOfLoginsFiles**&#x200B;オプション）で変更できます。 [サーバー設定ファイル](../../installation/using/the-server-configuration-file.md#syslogd)のドキュメントを参照してください。

デフォルトでは、ログはモジュールごととインスタンスごとに2つの10 MBのファイルに制限されます。 2つ目のファイルの名前は次のとおりです。**`<modulename>`_2.log**. したがって、ログのサイズは、モジュールごとおよびインスタンスごとに2*10 MBに制限されます。

ただし、大きなファイルは保持できます。 これを有効にするには、**conf/serverConf.xml**&#x200B;ファイルの&#x200B;**syslogd**&#x200B;ノードの&#x200B;**maxFileSizeMb=&quot;10&quot;**&#x200B;設定の値を変更します。 この値は、ログファイルの最大サイズ（MB単位）を表します。

ログの詳細レベルをさらに維持する場合は、**-verbose**&#x200B;パラメーターを使用してAdobe Campaignモジュールを起動できます。

**nlserver start  `<MODULE>`@`<INSTANCE>`  -verbose**
