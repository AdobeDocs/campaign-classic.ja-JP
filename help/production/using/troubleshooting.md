---
solution: Campaign Classic
product: campaign
title: 実稼動環境のトラブルシューティング
description: Adobe Campaignの設定、監視、アップグレードプロセス、データ処理、データベースの保守手順に関する実稼働時のトラブルシューティング手順を検出します。
audience: production
content-type: reference
topic-tags: troubleshooting
translation-type: tm+mt
source-git-commit: a490744e4a94a498fbd0205f119617137910d40c
workflow-type: tm+mt
source-wordcount: '167'
ht-degree: 23%

---


# 本番用トラブルシューティング{#troubleshooting}

この節では、配信とワークフローの実行、監視、データベースの保守、接続など、Adobe Campaignの一般的な実稼働上の問題に関するトラブルシューティングの手順について説明します。

## 一般的な問題と一般的な問題{#common-and-general-issues}

* この[ページ](../../production/using/modules-and-frequent-issues.md)には、リストされたモジュールで最も頻繁に発生する問題が示されています。
* この[page](../../production/using/workflow-execution.md)リストは、ワークフローの実行に関する問題が発生した場合に従うべき一般的なトラブルシューティングの手順です。
* この[page](../../production/using/lost-password.md)には、パスワードを失った場合の変更や回復方法の詳細が記載されています。
* この[page](../../production/using/console-update.md)には、対応するオプションを無効にした場合にコンソール更新要求を再開する方法が詳しく説明されています。

## 配信のトラブルシューティング {#delivery-troubleshooting}

配信に関する問題が発生した場合は、特定のアクションを実行できます。
* [配信品質の問題](../../production/using/performance-and-throughput-issues.md#deliverability_issues)
* [画像の表示の問題](../../production/using/image-display-issues.md) と[イメージが見つかりません](../../production/using/images-missing.md)
* [一時的なファイルの問題](../../production/using/temporary-files.md) (*オンプレミスホスティングモデルのみ*)

**関連トピック**：

[配信パフォーマンスの問題](../../delivery/using/delivery-performances.md)

## ログの操作{#working-with-logs}

* [ログの精度](../../production/using/log-precision.md)
* [ログの問題の追跡](../../production/using/tracking-logs-issues.md)

## データベースの問題{#database-issues}

* [データベースのパフォーマンス](../../production/using/database-performances.md)
* [Oracle データベースのエンコード](../../production/using/encoding-of-the-oracle-database.md)

## 接続の強化{#connection-improvements}

* [接続の失敗](../../production/using/failure-to-connect.md)
* [接続のしきい値](../../production/using/connection-thresholds.md)

## 技術的なトラブルシューティング{#technical-troubleshooting}

* [Linux でのスタックトレース](../../production/using/stack-trace-in-linux.md)
* [JSP の動作](../../production/using/jsp-behavior.md)
<!-- * [Locating Tomcat version](../../production/using/locate-tomcat-version.md)-->