---
product: campaign
title: 実稼動のトラブルシューティング
description: Adobe Campaign設定、モニタリング、アップグレードプロセス、データ処理、データベース保守手順に関する実稼動のトラブルシューティング手順について説明します。
feature: Monitoring, Troubleshooting
audience: production
content-type: reference
topic-tags: troubleshooting
exl-id: 78c65b31-e3d9-4a46-a101-26f35d00a4ee
source-git-commit: b666535f7f82d1b8c2da4fbce1bc25cf8d39d187
workflow-type: tm+mt
source-wordcount: '219'
ht-degree: 14%

---

# 実稼動のトラブルシューティング{#troubleshooting}



この節では、配信とワークフローの実行、監視、データベースのメンテナンス、接続など、Adobe Campaignの一般的な実稼働の問題に関するトラブルシューティング手順を示します。

## よくある問題と一般的な問題 {#common-and-general-issues}

* この [ページ](../../production/using/modules-and-frequent-issues.md) リストされたモジュールで最も頻繁に発生する問題を示します。
* この [ページ](../../production/using/workflow-execution.md) では、ワークフローの実行に関する問題が発生した場合に従うべき、一般的なトラブルシューティング手順を示します。
* この [ページ](../../production/using/lost-password.md) 失われたパスワードを変更または回復する方法の詳細です。
* この [ページ](../../production/using/console-update.md) 対応するオプションを非アクティブ化した場合に、コンソールの更新要求を再アクティブ化する方法について詳しく説明します。

## 配信のトラブルシューティング {#delivery-troubleshooting}

配信に関する問題が発生した場合は、特定のアクションを実行できます。
* [配信品質の問題](../../production/using/performance-and-throughput-issues.md#deliverability_issues)
* [画像の表示の問題](../../production/using/image-display-issues.md)
* [画像がありません](../../production/using/images-missing.md)
* [一時ファイルの問題](../../production/using/temporary-files.md) （*オンプレミス ホスティングモデルのみ*）

**関連トピック**：

[配信パフォーマンスの問題](../../delivery/using/delivery-performances.md)

## ログの操作 {#working-with-logs}

ログのエクスペリエンスを向上させるために役立つヒントを次に示します。

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
* [Tomcat バージョンを探します](../../production/using/locate-tomcat-version.md)
