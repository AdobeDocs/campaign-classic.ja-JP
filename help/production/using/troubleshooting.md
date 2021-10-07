---
product: campaign
title: 実稼動環境のトラブルシューティング
description: Adobe Campaignの設定、監視、アップグレードプロセス、データ処理、データベースのメンテナンス手順に関する実稼動環境のトラブルシューティング手順について説明します。
audience: production
content-type: reference
topic-tags: troubleshooting
exl-id: 78c65b31-e3d9-4a46-a101-26f35d00a4ee
source-git-commit: 20509f44c5b8e0827a09f44dffdf2ec9d11652a1
workflow-type: tm+mt
source-wordcount: '219'
ht-degree: 20%

---

# 実稼動環境のトラブルシューティング{#troubleshooting}

![](../../assets/v7-only.svg)

この節では、配信とワークフローの実行、監視、データベースのメンテナンス、接続など、Adobe Campaignの一般的な実稼動上の問題に関するトラブルシューティング手順について説明します。

## よくある問題と一般的な問題 {#common-and-general-issues}

* この [page](../../production/using/modules-and-frequent-issues.md) は、リストに表示されているモジュールで最も頻繁に発生する問題を示します。
* この [page](../../production/using/workflow-execution.md) には、ワークフローの実行に問題が発生した場合に従う必要がある一般的なトラブルシューティング手順が記載されています。
* この [page](../../production/using/lost-password.md) では、パスワードを失った場合の変更や回復の方法について詳しく説明します。
* この [page](../../production/using/console-update.md) では、対応するオプションを無効にした場合に、コンソールの更新リクエストを再開する方法について詳しく説明します。

## 配信のトラブルシューティング {#delivery-troubleshooting}

配信に問題が発生した場合は、特定のアクションを実行できます。
* [配信品質の問題](../../production/using/performance-and-throughput-issues.md#deliverability_issues)
* [画像の表示の問題](../../production/using/image-display-issues.md)
* [画像が見つかりません](../../production/using/images-missing.md)
* [一時ファイルの問題](../../production/using/temporary-files.md) (*オンプレミスホスティングモデルのみ*)

**関連トピック**：

[配信パフォーマンスの問題](../../delivery/using/delivery-performances.md)

## ログの操作 {#working-with-logs}

ログの操作性を向上させるためのヒントを以下に示します。

* [ログの精度](../../production/using/log-precision.md)
* [トラッキングログの問題](../../production/using/tracking-logs-issues.md)

## データベースの問題 {#database-issues}

パフォーマンスの問題を解決する方法については、次の節を参照してください。

* [データベースのパフォーマンス](../../production/using/database-performances.md)
* [Oracle データベースのエンコード](../../production/using/encoding-of-the-oracle-database.md)

## 接続の向上 {#connection-improvements}

接続の問題が発生した場合は、次の方法で修正できます。

* [接続の失敗](../../production/using/failure-to-connect.md)
* [接続のしきい値](../../production/using/connection-thresholds.md)

## 技術的なトラブルシューティング {#technical-troubleshooting}

より具体的な問題については、以下の節を参照してください。

* [Linux でのスタックトレース](../../production/using/stack-trace-in-linux.md)
* [JSP の動作](../../production/using/jsp-behavior.md)
* [Tomcat バージョンの検索](../../production/using/locate-tomcat-version.md)
