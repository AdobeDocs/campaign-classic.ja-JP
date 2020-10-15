---
title: 監視のガイドライン
description: Campaign インスタンスとプロセスを監視するためのガイドラインとベストプラクティスを確認します。
page-status-flag: never-activated
uuid: cf0d782d-47bf-40ae-ab6f-d1d47fa15792
contentOwner: sauviat
products: SG_CAMPAIGN/CLASSIC
audience: production
content-type: reference
topic-tags: introduction
discoiquuid: 8b33e6af-15c3-4b30-8ad6-d76a1f33be21
translation-type: tm+mt
source-git-commit: 70b143445b2e77128b9404e35d96b39694d55335
workflow-type: tm+mt
source-wordcount: '713'
ht-degree: 17%

---


# 監視のガイドライン {#monitoring-guidelines}

## インスタンスの監視ダッシュボード {#instance-monitoring-dashboard}

Campaign Classicのホームページからアクセスできる **[!UICONTROL 「監視]** 」タブは、インスタンスの監視に役立つ主なエントリポイントです。

インスタンスで何が起きているかのダッシュボードを提供します。ステータス（ビルドバージョン、インストール済みパッケージなど）、システムインジケータ、ログ、現在実行中のワークフロー、最後に送信された配信の状態など。

詳しくは、[こちら](../../production/using/monitoring-processes.md)を参照してください。

![](assets/monitoring_tab.png)

## Monitoring Campaign Classic processes {#monitoring-campaign-classic-processes}

<table>
<tr><td><img src="assets/do-not-localize/icon_system.svg" width="60px"><p><a href="#monitoring-instance">インスタンスの監視</a></p></td>
<td><img src="assets/do-not-localize/icon_workflows.svg" width="60px"><p><a href="#moniroting-workflows">ワークフローの監視</a></p></td>
<td><img src="assets/do-not-localize/icon_send.svg" width="60px"><p><a href="#monitoring-deliveries">配信の監視</a></p></td>
<td><img src="assets/do-not-localize/icon_database.svg" width="60px"><p><a href="#monitoring-database">データベースの監視</a></p></td></tr>
</table>

様々なキャンペーンプロセスを監視するその他の方法を使用できます。 システムが正常であることを確認し、ワークフローの設定や配信の送信時に発生する可能性のある問題のトラブルシューティングを行うために、インスタンスをいくつかの方法で監視します。

### インスタンスの監視 {#monitoring-instance}

<img src="assets/do-not-localize/icon_system.svg" width="60px">

**自動監視ツール**

いくつかの自動メソッドを使用できます。 を使用して、インスタンスを監視できます。 例えば、検出された異常値を含む電子メールレポートを設定したり、XML形式のインジケーターのリストを取得したりできます。 [詳しくは、ここをクリックしてください。](../../production/using/monitoring-processes.md#automatic-monitoring)

**監査記録**

監査証跡では、インスタンス内のオプション、ワークフローおよびスキーマに関連する変更の履歴を視覚化できます。 [詳しくは、ここをクリックしてください。](../../production/using/audit-trail.md)

**コントロールパネル**

このCampaign コントロールパネルでは、インスタンスのいくつかの設定を管理できます。URL権限の管理、サーバーのビルドバージョンなど、インスタンスの詳細を確認します。 また、インスタンスに接続されているSFTPサーバーの使用可能な領域を監視することもできます。 [詳しくは、ここをクリックしてください。](https://docs.adobe.com/content/help/ja-JP/control-panel/using/control-panel-home.html)

>[!NOTE]
>
>Campaign コントロールパネルは管理者ユーザーのみがアクセスでき、Adobe Managed Servicesを使用するすべてのお客様が利用できます。

### ワークフローの監視 {#monitoring-workflows}

<img src="assets/do-not-localize/icon_workflows.svg" width="60px">

**ワークフローヒートマップ**

Workflow HeatMapは、インスタンスで実行されているすべてのワークフローを視覚的に表現します。 これにより、インスタンスの負荷を簡単に監視し、それに応じてワークフローを計画できます。 [詳しくは、ここをクリックしてください。](../../workflow/using/heatmap.md)

**監査記録**

監査証跡では、ワークフローで行われたすべての変更と現在の状態を視覚化できます。 [ここをクリック](../../production/using/audit-trail.md).

**ワークフローのトラブルシューティング**

ワークフローの実行で問題が発生した場合は、特定のアクションを実行できます。 [詳細については](../../production/using/workflow-execution.md) 、ここをクリックしてください

**ワークフローの状態の監視**

ヒートマップに加えて、ワークフローを作成して、一連のワークフローの状態を監視し、定期的に監視者にメッセージを送信することもできます。 [詳しくは、ここをクリックしてください。](../../workflow/using/supervising-workflows.md)

**一般的なガイドライン**

ワークフローを使用する際のガイドラインとベストプラクティスに従うと、パフォーマンスの向上に役立ちます。 詳しくは、次の節を参照してください。
* [ワークフロー使用時のベストプラクティス](../../workflow/using/workflow-best-practices.md)
* [ワークフロー実行の監視](../../workflow/using/monitoring-workflow-execution.md)

### 配信の監視 {#monitoring-deliveries}

<img src="assets/do-not-localize/icon_send.svg" width="60px">

**SMTPレポート**

SMTPレポートには、配信の統計とSMTPエラーがドメイン別に表示されます。 [詳細情報](../../production/using/monitoring-processes.md)

**ベストプラクティス**

[配信の送信とデザインのベストプラクティスは](../../delivery/using/delivery-best-practices.md) 、パフォーマンスの向上に役立ちます。

**配信のトラブルシューティング**&#x200B;特定のアクションは、配信の問題が発生した場合に実行できます。
* [配信品質の問題](../../production/using/performance-and-throughput-issues.md#deliverability_issues)
* [画像の表示の問題](../../production/using/image-display-issues.md)
* [配信パフォーマンスの問題](../../delivery/using/monitoring-a-delivery.md#performance_issues)
* [一時的なファイルの問題](../../production/using/temporary-files.md) — オンプレミス *のホスティングモデルのみ*

### データベースの監視 {#monitoring-database}

<img src="assets/do-not-localize/icon_database.svg" width="60px">

**データベースクリーンアップワークフロー**

データベースのクリーンアップワークフローを使用すると、古いデータをデータベースから削除できます。 データベースの指数的な増加を避けることをお勧めします。 [詳しくは、ここをクリックしてください。](../../production/using/database-cleanup-workflow.md)

**データベースのパフォーマンスのトラブルシューティング**

データベースのパフォーマンスの問題が発生した場合は、特定のアクションを実行できます。 [詳しくは、ここをクリックしてください。](../../production/using/database-performances.md)

**データベースのメンテナンス**

*オンプレミスおよびハイブリッドのホスティングモデルのみ*

ディスク領域の過剰消費を回避し、データベースアクセスに影響を与えないように、定期的にデータベースメンテナンスを行うことをお勧めします。 [詳しくは、ここをクリックしてください。](../../production/using/recommendations.md)

**バックアップと復元**

*オンプレミスおよびハイブリッドのホスティングモデルのみ*

マシン上の問題（物理的な問題でもシステム関連の問題でも）のイベントにデータが失われないように、バックアップは不可欠です。 [詳しくは、ここをクリックしてください。](../../production/using/backup.md)復元手順については、 [この節で説明します](../../production/using/restoration.md)。

## Campaign Classic技術原則 {#campaign-classic-technical-principles}

テクニカルリソースは、Campaign Classicドキュメントで参照できます。 インスタンスで技術的な操作を実行する前に、これらのトピックについて理解しておくことをお勧めします。

**モデルと機能のホスト**

* [Campaign Classicホスティングモデル](../../installation/using/hosting-models.md)
* [ホスティングモデル機能](https://helpx.adobe.com/jp/campaign/kb/acc-on-prem-vs-hosted.html)

**サーバー設定**

*オンプレミスおよびハイブリッドのホスティングモデルのみ*

* [必須のサーバー設定](../../installation/using/campaign-server-configuration.md)
* [Serverconf.xmlファイルの設定](../../installation/using/the-server-configuration-file.md)
* [配信品質のサーバ設定](../../installation/using/email-deliverability.md)
* [インスタンスを作成し、データベースを宣言するコマンドライン](../../installation/using/command-lines.md)

**一般原則**

* [Campaign Classic構造](../../production/using/general-architecture.md)
* [Campaign Classicモジュール](../../production/using/operating-principle.md)
* [Campaign Classicオプション](../../installation/using/configuring-campaign-options.md)
* [モジュールの自動起動の設定方法](../../production/using/administration.md)
* [キャンペーン構成原則](../../production/using/configuration-principle.md)
* [トラブルシューティング手順](../../production/using/performance-and-throughput-issues.md)
