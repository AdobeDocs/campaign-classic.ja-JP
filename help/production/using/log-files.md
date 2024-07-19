---
product: campaign
title: ログファイル
description: ログファイル
feature: Monitoring
badge-v7-prem: label="オンプレミス／ハイブリッドのみ" type="Caution" url="https://experienceleague.adobe.com/docs/campaign-classic/using/installing-campaign-classic/architecture-and-hosting-models/hosting-models-lp/hosting-models.html?lang=ja" tooltip="オンプレミスデプロイメントとハイブリッドデプロイメントにのみ適用されます"
audience: production
content-type: reference
topic-tags: production-procedures
exl-id: c9d427da-6965-4945-90f0-d0770701d55e
source-git-commit: 14ba450ebff9bba6a36c0df07d715b7279604222
workflow-type: tm+mt
source-wordcount: '445'
ht-degree: 5%

---

# ログファイル{#log-files}



ログファイルは、次のように整理されます。

![](assets/d_ncs_directory.png)

各 **nlserver** モジュールは、**`<installation directory>`/var/`<instance>`/log/`<module>`.log** ディレクトリに保存されるログファイルを生成します。

**nlserver syslogd** モジュールは、ログをディスクに保存します。 このモジュールは Unix **syslog デーモン** に似ていますが、Unix と Windows の互換性のために適応されています。 他のAdobe Campaign モジュールは、ログをディスクに保存しません。UDP パケットを送信することで、このタスクを **syslogd** モジュールにデリゲートします。

デフォルトでは、Adobe Campaign プラットフォームには **syslogd** モジュールがインストールされていますが、別の **syslog デーモン** を使用することもできます。 このモジュールは、**log** ディレクトリにログファイルを作成します。

マルチインスタンスモジュールのログは、**`<installation directory>`/var/default/log/** ディレクトリに格納されています。 同じログファイルがすべてのインスタンスで共有されます（例：**web.log**）。

他のモジュールのログは、インスタンスにちなんで命名されたサブフォルダーに保存されます。 各インスタンスには独自のログファイルがあります。

次の表に、複数インスタンスのログファイルを示します。

| ファイル | 説明 |
|---|---|
| web.log | Web モジュールログ（クライアントコンソール、レポート、SOAP API など） |
| webmdl.log | リダイレクトモジュールからのログ |
| watchdog.log | Adobe Campaign プロセスモニタリングモジュールからのログ |
| trackinglogd.log | トラッキングログ |

モノインスタンスログファイルを次の表に示します。

| ファイル | 説明 |
|---|---|
| mta.log | mta モジュールログ |
| mtachild.log | メッセージ配信処理ログ |
| wfserver.log | ワークフローサーバーモジュールのログ |
| runwf.log | ワークフロー実行ログ |
| inMail.log | バウンスメールモジュールログ |
| logins.log | Adobe Campaignへのログイン試行をすべて記録します（成功または失敗） |

>[!IMPORTANT]
>
>**redir** ディレクトリは、リダイレクト サーバーにのみ存在します。 **url** サブディレクトリには、リダイレクトされる URL の一致が含まれ、サブディレクトリ **log** には、トラッキングログが含まれます。 トラッキングログを生成するには、**trackinglogd** モジュールが実行されている必要があります。

パフォーマンスとストレージの最適化のために、logins.log ファイルは複数のファイルに分割されます。毎日 1 つのファイル（logins.yy-mm-dd.log）が保持され、最大 365 個のファイルが保持されます。 日数は、syslogd の下の serverConf.xml で変更できます（**maxNumberOfLoginsFiles** オプション）。 [ サーバー設定ファイル ](../../installation/using/the-server-configuration-file.md#syslogd) に関するドキュメントを参照してください。

デフォルトでは、ログは、モジュールあたり、およびインスタンスあたり 2 つの 10 MB のファイルに制限されます。 2 つ目のファイルは **`<modulename>`_2.log** です。 したがって、ログのサイズは、モジュールごと、およびインスタンスごとに 2&#42;10MB に制限されます。

ただし、大きなファイルは保持できます。 これを有効にするには、**conf/serverConf.xml** ファイルの **syslogd** ノードにある **maxFileSizeMb=&quot;10&quot;** 設定の値を変更します。 この値は、ログファイルの最大サイズ（MB 単位）を表します。

ログの詳細レベルを維持する場合は、**-verbose** パラメーターを使用してAdobe Campaign モジュールを開始できます。

**nlserver start `<MODULE>`@`<INSTANCE>` -verbose**
