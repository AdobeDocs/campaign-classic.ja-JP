---
product: campaign
title: 監視のガイドライン
description: Campaign インスタンスとプロセスを監視するためのガイドラインとベストプラクティスについて説明します
feature: Monitoring
exl-id: ca0c33c5-7350-462a-bc65-4cab51e529d9
source-git-commit: 0ed70b3c57714ad6c3926181334f57ed3b409d98
workflow-type: tm+mt
source-wordcount: '744'
ht-degree: 23%

---

# 監視のガイドライン {#monitoring-guidelines}



## インスタンス監視ダッシュボード {#instance-monitoring-dashboard}

Campaign Classicホームページからアクセスできる **[!UICONTROL 監視]** タブは、インスタンスを監視するための主なエントリポイントです。

インスタンスのステータス（ビルドバージョン、インストール済みパッケージなど）、システムインジケーター、ログ、現在実行中のワークフロー、最後に送信された配信の状態に関するダッシュボードが提供されます。

詳しくは、[こちら](../../production/using/monitoring-processes.md)を参照してください。

![](assets/monitoring_tab.png)

## Campaign Classicプロセスの監視 {#monitoring-campaign-classic-processes}

<table>
<tr><td><img src="assets/do-not-localize/icon_system.svg" width="60px"><p><a href="#monitoring-instance">インスタンスの監視</a></p></td>
<td><img src="assets/do-not-localize/icon_workflows.svg" width="60px"><p><a href="#monitoring-workflows">ワークフローの監視</a></p></td>
<td><img src="assets/do-not-localize/icon_send.svg" width="60px"><p><a href="#monitoring-deliveries">配信の監視</a></p></td>
<td><img src="assets/do-not-localize/icon_database.svg" width="60px"><p><a href="#monitoring-database">データベースの監視</a></p></td></tr>
</table>

様々なキャンペーンプロセスを監視するその他の方法を利用できます。 インスタンスを監視してシステムが正常であることを確認したり、最終的にワークフローの設定や配信の送信などで発生する可能性のある問題をトラブルシューティングしたりする方法がいくつか用意されています。

### インスタンスの監視 {#monitoring-instance}

<img src="assets/do-not-localize/icon_system.svg" width="60px">

**自動監視ツール**

いくつかの自動方法が利用できます。 インスタンスの監視に役立ちます。 例えば、異常が検出されたメールレポートの設定や、XML 形式の指標のリストの取得などを行うことができます。 詳しくは、[ここをクリック](../../production/using/monitoring-processes.md#automatic-monitoring)してください。

**監査記録**

監査記録を使用すると、インスタンス内のオプション、ワークフロー、スキーマに関連する変更の完全な履歴を視覚化できます。 詳しくは、[ここをクリック](../../production/using/audit-trail.md)してください。

**コントロールパネル**

Campaign コントロールパネルを使用すると、インスタンスの複数の設定を管理できます。URL 権限の管理、サーバーのビルドバージョンなどのインスタンスの詳細の確認などです。 また、インスタンスに接続されている SFTP サーバーの使用可能な領域を監視することもできます。 詳しくは、[ここをクリック](https://experienceleague.adobe.com/docs/control-panel/using/control-panel-home.html?lang=ja)してください。

>[!NOTE]
>
>コントロールパネルは、すべての管理者ユーザーがアクセスできます。 ユーザーに管理者アクセス権を付与する手順については、[このページ](https://experienceleague.adobe.com/docs/control-panel/using/discover-control-panel/managing-permissions.html?lang=ja#discover-control-panel)で詳しく説明しています。
>
>インスタンスは AWS でホストされ、[最新の GA ビルド](../../rn/using/rn-overview.md)でアップグレードされている必要があります。バージョンを確認する方法については、[この節](../../platform/using/launching-adobe-campaign.md#getting-your-campaign-version)を参照してください。インスタンスが AWS でホストされているかどうかを確認するには、[このページ](https://experienceleague.adobe.com/docs/control-panel/using/faq.html?lang=ja)に記載されている手順に従います。

### ワークフローの監視 {#monitoring-workflows}

<img src="assets/do-not-localize/icon_workflows.svg" width="60px">

**ワークフローヒートマップ**

ワークフローヒートマップは、お使いのインスタンスで実行されているすべてのワークフローを視覚的に表現したものです。 これにより、インスタンスの負荷を簡単に監視し、それに応じてワークフローを計画できます。 詳しくは、[ここをクリック](../../workflow/using/heatmap.md)してください。

**監査記録**

監査記録を使用すると、ワークフローで行われたすべての変更とその現在の状態を視覚化できます。 [ ここをクリック ](../../production/using/audit-trail.md)。

**ワークフローのトラブルシューティング**

ワークフローの実行に関する問題が発生した場合は、特定のアクションを実行できます。 詳しくは、[ ここをクリック ](../../production/using/workflow-execution.md) してください

**ワークフローステータスの監視**

ヒートマップに加えて、一連のワークフローのステータスを監視し、スーパーバイザーに繰り返しメッセージを送信するワークフローを作成できます。 詳しくは、[ここをクリック](../../workflow/using/supervising-workflows.md)してください。

**一般的なガイドライン**

ワークフローを使用する際に、ガイドラインとベストプラクティスに従うと、パフォーマンスの向上に役立ちます。 詳しくは、次の節を参照してください。
* [ワークフロー使用時のベストプラクティス](../../workflow/using/workflow-best-practices.md)
* [ワークフローの実行の監視](../../workflow/using/monitoring-workflow-execution.md)

### 配信の監視 {#monitoring-deliveries}

<img src="assets/do-not-localize/icon_send.svg" width="60px">

**SMTP レポート**

SMTP レポートには、配信統計と SMTP エラーがドメイン別に表示されます。 [詳細情報](../../production/using/monitoring-processes.md)

**ベストプラクティス**

[ 配信の送信とデザインのベストプラクティス ](../../delivery/using/delivery-best-practices.md) は、パフォーマンスの向上に役立ちます。

**配信のトラブルシューティング**
配信に関する問題が発生した場合は、特定のアクションを実行できます。
* [配信品質の問題](../../production/using/performance-and-throughput-issues.md#deliverability_issues)
* [画像の表示の問題](../../production/using/image-display-issues.md)
* [配信パフォーマンスの問題](../../delivery/using/delivery-performances.md)
* [ 一時ファイルの問題 ](../../production/using/temporary-files.md) - *オンプレミスホスティングモデルのみ*

### データベースの監視 {#monitoring-database}

<img src="assets/do-not-localize/icon_database.svg" width="60px">

**データベースクリーンアップワークフロー**

データベースクリーンアップワークフローを使用すると、古いデータをデータベースから削除できます。 データベースの急激な増加を避けることをお勧めします。 詳しくは、[ここをクリック](../../production/using/database-cleanup-workflow.md)してください。

**データベースパフォーマンスのトラブルシューティング**

データベースのパフォーマンスに関する問題が発生した場合は、特定のアクションを実行できます。 詳しくは、[ここをクリック](../../production/using/database-performances.md)してください。

**データベースのメンテナンス**

*オンプレミスおよびハイブリッドホスティングモデルのみ*

データベースへのアクセスに影響を与えるディスク領域の過剰消費を避けるために、定期的にデータベースのメンテナンスを実行することをお勧めします。 詳しくは、[ここをクリック](../../production/using/recommendations.md)してください。

**バックアップと復元**

*オンプレミスおよびハイブリッドホスティングモデルのみ*

マシン上で（物理またはシステムに関連する）問題が発生した場合にデータが失われないようにするには、バックアップが不可欠です。 詳しくは、[ ここをクリック ](../../production/using/backup.md) してください。 復元手順については、[ この節 ](../../production/using/restoration.md) で説明します。

## Campaign Classicの技術原則 {#campaign-classic-technical-principles}

技術リソースは、Campaign Classicドキュメントで入手できます。 インスタンスに対して技術的な操作を実行する前に、これらのトピックについて理解しておくことをお勧めします。

**ホスティングモデルと機能**

* [Campaign Classicホスティングモデル](../../installation/using/hosting-models.md)
* [ホスティングモデルの機能](../../installation/using/capability-matrix.md)

**サーバー設定**

*オンプレミスおよびハイブリッドホスティングモデルのみ*

* [サーバー設定](../../installation/using/configuring-campaign-server.md)
* [Serverconf.xml ファイル設定](../../installation/using/the-server-configuration-file.md)
* [配信品質を考慮したサーバー設定](../../installation/using/email-deliverability.md)
* [インスタンスを作成しデータベースを宣言するためのコマンドライン](../../installation/using/command-lines.md)

**一般原則**

* [Campaign Classic構造](../../production/using/general-architecture.md)
* [Campaign Classicモジュール](../../production/using/operating-principle.md)
* [Campaign Classicオプション](../../installation/using/configuring-campaign-options.md)
* [モジュールの自動スタートアップの設定方法](../../production/using/administration.md)
* [キャンペーン設定の原則](../../production/using/configuration-principle.md)
* [トラブルシューティング手順](../../production/using/performance-and-throughput-issues.md)
