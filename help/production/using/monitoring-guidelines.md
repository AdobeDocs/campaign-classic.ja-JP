---
solution: Campaign Classic
product: campaign
title: 監視のガイドライン
description: Campaign インスタンスとプロセスを監視するためのガイドラインとベストプラクティスを確認します。
audience: production
content-type: reference
topic-tags: introduction
exl-id: ca0c33c5-7350-462a-bc65-4cab51e529d9
source-git-commit: bce114f36d1ec4582fc79e750d48155ba0d7cd1f
workflow-type: tm+mt
source-wordcount: '769'
ht-degree: 26%

---

# 監視のガイドライン {#monitoring-guidelines}

## インスタンスの監視ダッシュボード {#instance-monitoring-dashboard}

Campaign Classicのホームページからアクセスできる「**[!UICONTROL 監視]**」タブは、インスタンスの監視に役立つ主なエントリポイントです。

インスタンスで発生している内容のダッシュボードを提供します。ステータス（ビルドバージョン、インストール済みパッケージなど）、システム指標、ログ、現在実行中のワークフロー、最後に送信された配信の状態など。

詳しくは、[こちら](../../production/using/monitoring-processes.md)を参照してください。

![](assets/monitoring_tab.png)

## 監視Campaign Classicプロセス{#monitoring-campaign-classic-processes}

<table>
<tr><td><img src="assets/do-not-localize/icon_system.svg" width="60px"><p><a href="#monitoring-instance">インスタンスの監視</a></p></td>
<td><img src="assets/do-not-localize/icon_workflows.svg" width="60px"><p><a href="#moniroting-workflows">ワークフローの監視</a></p></td>
<td><img src="assets/do-not-localize/icon_send.svg" width="60px"><p><a href="#monitoring-deliveries">配信の監視</a></p></td>
<td><img src="assets/do-not-localize/icon_database.svg" width="60px"><p><a href="#monitoring-database">データベースの監視</a></p></td></tr>
</table>

様々なキャンペーンプロセスを監視するその他の方法を使用できます。 インスタンスを監視する方法はいくつかあり、システムが正常であることを確認し、ワークフローの設定や配信の送信などの際に発生する可能性のある問題のトラブルシューティングをおこなうことができます。

### インスタンスの監視{#monitoring-instance}

<img src="assets/do-not-localize/icon_system.svg" width="60px">

**自動監視ツール**

いくつかの自動メソッドを使用できます。 を使用して、インスタンスを監視できます。 例えば、検出された異常値を含む電子メールレポートを設定したり、XML形式の指標のリストを取得したりできます。 詳しくは、[ここをクリック](../../production/using/monitoring-processes.md#automatic-monitoring)してください。

**監査記録**

監査記録を使用すると、インスタンス内のオプション、ワークフローおよびスキーマに関する変更の完全な履歴を視覚化できます。 詳しくは、[ここをクリック](../../production/using/audit-trail.md)してください。

**Campaign コントロールパネル**

「 」Campaign コントロールパネルでは、インスタンスの複数の設定を管理できます。URL権限の管理、サーバーのビルドバージョンなど、インスタンスの詳細の確認をおこないます。 また、インスタンスに接続されているSFTPサーバーの使用可能な領域を監視することもできます。 詳しくは、[ここをクリック](https://experienceleague.adobe.com/docs/control-panel/using/control-panel-home.html?lang=ja)してください。

>[!NOTE]
>
>コントロールパネルは、すべての管理者ユーザーがアクセスできます。 ユーザーに管理者アクセス権を付与する手順については、[このページ](https://experienceleague.adobe.com/docs/control-panel/using/discover-control-panel/managing-permissions.html?lang=ja#discover-control-panel)で詳しく説明しています。
>
>インスタンスは AWS でホストされ、最新の [Gold Standard](../../rn/using/gs-overview.md) ビルドまたは[最新の GA ビルド（21.1）](../../rn/using/latest-release.md)にアップグレードする必要があります。 バージョンを確認する方法については、[この節](../../platform/using/launching-adobe-campaign.md#getting-your-campaign-version)を参照してください。インスタンスが AWS でホストされているかどうかを確認するには、[このページ](https://experienceleague.adobe.com/docs/control-panel/using/faq.html?lang=ja)に記載されている手順に従います。

### ワークフローの監視 {#monitoring-workflows}

<img src="assets/do-not-localize/icon_workflows.svg" width="60px">

**ワークフローヒートマップ**

ワークフローヒートマップは、インスタンス上で実行されているすべてのワークフローを視覚的に示します。 これにより、インスタンスの負荷を簡単に監視し、それに応じてワークフローを計画できます。 詳しくは、[ここをクリック](../../workflow/using/heatmap.md)してください。

**監査記録**

監査記録を使用すると、ワークフローでおこなわれたすべての変更と現在の状態を視覚化できます。 [ここをクリック](../../production/using/audit-trail.md).

**ワークフローのトラブルシューティング**

ワークフローの実行で問題が発生した場合は、特定のアクションを実行できます。 [詳しく](../../production/using/workflow-execution.md) はここをクリック

**ワークフローステータスの監視**

さらに、ヒートマップに加えて、一連のワークフローのステータスを監視し、スーパーバイザーに繰り返しメッセージを送信するワークフローを作成できます。 詳しくは、[ここをクリック](../../workflow/using/supervising-workflows.md)してください。

**一般的なガイドライン**

ワークフローを使用する際のガイドラインとベストプラクティスに従うことで、パフォーマンスを向上できます。 詳しくは、次の節を参照してください。
* [ワークフローを使用する際のベストプラクティス](../../workflow/using/workflow-best-practices.md)
* [監視ワークフローの実行](../../workflow/using/monitoring-workflow-execution.md)

### 配信の監視 {#monitoring-deliveries}

<img src="assets/do-not-localize/icon_send.svg" width="60px">

**SMTPレポート**

SMTPレポートには、ドメインごとに配信統計とSMTPエラーが表示されます。 [詳細情報](../../production/using/monitoring-processes.md)

**ベストプラクティス**

[配信の送信とデザインのベストプラクティスは、パ](../../delivery/using/delivery-best-practices.md) フォーマンスの向上に役立ちます。

**配信のトラ**
ブルシューティング配信に関する問題が発生した場合は、具体的なアクションを実行できます。
* [配信品質の問題](../../production/using/performance-and-throughput-issues.md#deliverability_issues)
* [画像の表示の問題](../../production/using/image-display-issues.md)
* [配信パフォーマンスの問題](../../delivery/using/delivery-performances.md)
* [一時ファイルの問題](../../production/using/temporary-files.md)  — オンプレミ *スでのホスティングモデルのみ*

### データベース{#monitoring-database}の監視

<img src="assets/do-not-localize/icon_database.svg" width="60px">

**データベースクリーンアップワークフロー**

データベースクリーンアップワークフローを使用すると、古いデータをデータベースから削除できます。 データベースの急激な増加を避けることをお勧めします。 詳しくは、[ここをクリック](../../production/using/database-cleanup-workflow.md)してください。

**データベースパフォーマンスのトラブルシューティング**

データベースのパフォーマンスに関する問題が発生した場合は、特定のアクションを実行できます。 詳しくは、[ここをクリック](../../production/using/database-performances.md)してください。

**データベースのメンテナンス**

*オンプレミスおよびハイブリッドホスティングモデルのみ*

ディスク容量の過剰消費を避け、データベースアクセスに影響を与えるために、定期的にデータベースのメンテナンスを行うことをお勧めします。 詳しくは、[ここをクリック](../../production/using/recommendations.md)してください。

**バックアップと復元**

*オンプレミスおよびハイブリッドホスティングモデルのみ*

マシン上の問題（物理的な問題でもシステム関連の問題でも）が発生した場合にデータが失われないように、バックアップは不可欠です。 詳しくは、[ここをクリック](../../production/using/backup.md)してください。復元手順については、[この節](../../production/using/restoration.md)で説明します。

## Campaign Classicの技術原則{#campaign-classic-technical-principles}

技術リソースは、Campaign Classicドキュメントに記載されています。 インスタンスに対して技術的な操作を実行する前に、これらのトピックについて理解しておくことをお勧めします。

**モデルと機能のホスト**

* [Campaign Classicホスティングモデル](../../installation/using/hosting-models.md)
* [ホスティングモデル機能](../../installation/using/capability-matrix.md)

**サーバー設定**

*オンプレミスおよびハイブリッドホスティングモデルのみ*

* [サーバー設定](../../installation/using/configuring-campaign-server.md)
* [Serverconf.xmlファイルの設定](../../installation/using/the-server-configuration-file.md)
* [配信品質のサーバー設定](../../installation/using/email-deliverability.md)
* [インスタンスを作成し、データベースを宣言するコマンドライン](../../installation/using/command-lines.md)

**一般原則**

* [Campaign Classic構造](../../production/using/general-architecture.md)
* [Campaign Classicモジュール](../../production/using/operating-principle.md)
* [Campaign Classicオプション](../../installation/using/configuring-campaign-options.md)
* [モジュールの自動起動の設定方法](../../production/using/administration.md)
* [キャンペーンの設定の原則](../../production/using/configuration-principle.md)
* [トラブルシューティング手順](../../production/using/performance-and-throughput-issues.md)
