---
product: campaign
title: 実稼動環境のトラブルシューティング
description: Adobe Campaignの設定、監視、アップグレードプロセス、データ処理、データベースのメンテナンス手順に関する実稼動環境のトラブルシューティング手順について説明します。
feature: Monitoring, Troubleshooting
badge-v7-only: label="v7" type="Informative" tooltip="Campaign Classicv7 にのみ適用"
audience: production
content-type: reference
topic-tags: troubleshooting
exl-id: 78c65b31-e3d9-4a46-a101-26f35d00a4ee
source-git-commit: 3a9b21d626b60754789c3f594ba798309f62a553
workflow-type: tm+mt
source-wordcount: '226'
ht-degree: 20%

---

# 実稼動環境のトラブルシューティング{#troubleshooting}



この節では、配信とワークフローの実行、監視、データベースのメンテナンス、接続など、Adobe Campaignの一般的な実稼動の問題に関するトラブルシューティング手順について説明します。

## よくある問題と一般的な問題 {#common-and-general-issues}

* この [ページ](../../production/using/modules-and-frequent-issues.md) は、リストに表示されているモジュールで発生した最も頻繁な問題を示します。
* この [ページ](../../production/using/workflow-execution.md) ワークフローの実行に関する問題が発生した場合に従う必要がある一般的なトラブルシューティング手順を示します。
* この [ページ](../../production/using/lost-password.md) 失われたパスワードを変更または復元する方法の詳細。
* この [ページ](../../production/using/console-update.md) 対応するオプションを無効にした場合に、コンソールの更新リクエストを再アクティブ化する方法の詳細を説明します。

## 配信のトラブルシューティング {#delivery-troubleshooting}

配信に問題が発生した場合は、特定のアクションを実行できます。
* [配信品質の問題](../../production/using/performance-and-throughput-issues.md#deliverability_issues)
* [画像の表示の問題](../../production/using/image-display-issues.md)
* [画像がありません](../../production/using/images-missing.md)
* [一時ファイルの問題](../../production/using/temporary-files.md) (*オンプレミスホスティングモデルのみ*)

**関連トピック**：

[配信パフォーマンスの問題](../../delivery/using/delivery-performances.md)

## ログの操作 {#working-with-logs}

ログの操作性を向上させるためのヒントを以下にいくつか示します。

* [ログの精度](../../production/using/log-precision.md)
* [トラッキングログの問題](../../production/using/tracking-logs-issues.md)

## データベースの問題 {#database-issues}

次の節を読んで、パフォーマンスの問題を解決する方法を見つけます。

* [データベースのパフォーマンス](../../production/using/database-performances.md)
* [Oracle データベースのエンコード](../../production/using/encoding-of-the-oracle-database.md)

## 接続の向上 {#connection-improvements}

接続の問題が発生した場合は、次の方法で修正できます。

* [接続の失敗](../../production/using/failure-to-connect.md)
* [接続のしきい値](../../production/using/connection-thresholds.md)

## 技術的なトラブルシューティング {#technical-troubleshooting}

具体的な問題について詳しくは、以下の節を参照してください。

* [Linux でのスタックトレース](../../production/using/stack-trace-in-linux.md)
* [JSP の動作](../../production/using/jsp-behavior.md)
* [Tomcat バージョンを検索](../../production/using/locate-tomcat-version.md)
