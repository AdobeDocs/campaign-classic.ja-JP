---
product: campaign
title: ログファイル
description: ログファイル
feature: Monitoring
badge-v7-prem: label="オンプレミスおよびハイブリッド" type="Caution" url="https://experienceleague.adobe.com/docs/campaign-classic/using/installing-campaign-classic/architecture-and-hosting-models/hosting-models-lp/hosting-models.html?lang=ja" tooltip="オンプレミスデプロイメントとハイブリッドデプロイメントにのみ適用されます"
audience: production
content-type: reference
topic-tags: production-procedures
exl-id: c9d427da-6965-4945-90f0-d0770701d55e
source-git-commit: b666535f7f82d1b8c2da4fbce1bc25cf8d39d187
workflow-type: tm+mt
source-wordcount: '444'
ht-degree: 4%

---

# ログファイル{#log-files}



ログファイルは、次のように整理されます。

![](assets/d_ncs_directory.png)

Each **nlserver** モジュールは、次のディレクトリに保存されるログファイルを生成します。 **`<installation directory>`/var/`<instance>`/log/`<module>`.log**.

この **nlserver syslogd** モジュールはログをディスクに保存します。 このモジュールは Unix に似ています **syslog デーモン**&#x200B;ただし、UNIX と Windows の互換性を考慮して設計されています。 その他のAdobe Campaign モジュールは、ログをディスクに保存せず、このタスクを次のユーザーにデリゲートします **syslogd** UDP パケットを送信してモジュール化します。

Adobe Campaign プラットフォームのデフォルトでは、 **syslogd** モジュールはそれにインストールされていますが、別のものを使用することができます **syslog デーモン**. このモジュールは、 **ログ** ディレクトリ。

マルチインスタンスモジュールのログは、次のディレクトリに格納されます。 **`<installation directory>`/var/default/log/**. すべてのインスタンスで同じログファイルが共有されます（例： **web.log**）に設定します。

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
>この **redir** ディレクトリはリダイレクトサーバーにのみ存在します。 この **url** サブディレクトリには、リダイレクトされる URL とサブディレクトリの一致が含まれます **ログ** トラッキングログが含まれます。 トラッキングログを生成するには、 **trackinglogd** モジュールが実行中である必要があります。

パフォーマンスとストレージの最適化のために、logins.log ファイルは複数のファイルに分割されます。毎日 1 つのファイル（logins.yy-mm-dd.log）が保持され、最大 365 個のファイルが保持されます。 日数は、syslogd （**maxNumberOfLoginsFiles** （オプション）。 のドキュメントを参照してください。 [サーバー設定ファイル](../../installation/using/the-server-configuration-file.md#syslogd).

デフォルトでは、ログは、モジュールあたり、およびインスタンスあたり 2 つの 10 MB のファイルに制限されます。 2 つ目のファイルは次のとおりです。 **`<modulename>`_2.log**. したがって、ログのサイズは 2 に制限されます&#42;モジュールおよびインスタンスあたり 10 MB。

ただし、大きなファイルは保持できます。 これを有効にするには、 **maxFileSizeMb=&quot;10&quot;** での設定 **syslogd** のノード **conf/serverConf.xml** ファイル。 この値は、ログファイルの最大サイズ（MB 単位）を表します。

ログの詳細レベルを維持する場合は、次のコードを使用してAdobe Campaign モジュールを開始できます。 **-verbose** パラメーター：

**nlserver 開始 `<MODULE>`@`<INSTANCE>` -verbose**
