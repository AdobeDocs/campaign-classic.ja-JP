---
product: campaign
title: 実稼動のトラブルシューティング
description: Adobe Campaignの設定、モニタリング、アップグレードプロセス、データ処理、データベースのメンテナンス手順に関する実稼動トラブルシューティング手順について説明します
feature: Monitoring, Troubleshooting
audience: production
content-type: reference
topic-tags: troubleshooting
exl-id: 78c65b31-e3d9-4a46-a101-26f35d00a4ee
source-git-commit: 0c639cc8b9636c190c868980ab5182a0eccb5f74
workflow-type: tm+mt
source-wordcount: '220'
ht-degree: 20%

---

# 実稼動のトラブルシューティング{#troubleshooting}



この節では、配信とワークフローの実行、モニタリング、データベースメンテナンス、接続など、Adobe Campaignの一般的な実稼動環境の問題に関するトラブルシューティング手順について説明します。

## よくある問題と一般的な問題 {#common-and-general-issues}

* この[&#x200B; ページ &#x200B;](../../production/using/modules-and-frequent-issues.md)は、リストされたモジュールで最も頻繁に発生する問題を示しています。
* この[&#x200B; ページ &#x200B;](../../production/using/workflow-execution.md)には、ワークフロー実行に関する問題に直面した場合に従うべき一般的なトラブルシューティング手順が記載されています。
* この[&#x200B; ページ &#x200B;](../../production/using/lost-password.md)では、失われたパスワードを変更または復元する方法について詳しく説明しています。
* この[&#x200B; ページ &#x200B;](../../production/using/console-update.md)では、対応するオプションを非アクティブ化した場合に、コンソール更新リクエストを再アクティブ化する方法について詳しく説明しています。

## 配信のトラブルシューティング {#delivery-troubleshooting}

配信に問題がある場合は、特定のアクションを実行できます。
* [配信品質の問題](../../production/using/performance-and-throughput-issues.md#deliverability_issues)
* [画像の表示の問題](../../production/using/image-display-issues.md)
* [画像がありません](../../production/using/images-missing.md)
* [一時ファイルの問題](../../production/using/temporary-files.md) （*オンプレミスホスティングモデルのみ*）

**関連トピック**：

[配信パフォーマンスの問題](../../delivery/using/delivery-performance-troubleshooting.md)

## ログの操作 {#working-with-logs}

ここでは、ログを利用してエクスペリエンスを向上させるためのヒントをいくつか紹介します。

* [ログの精度](../../production/using/log-precision.md)
* [トラッキングログの問題](../../production/using/tracking-logs-issues.md)

## データベースの問題 {#database-issues}

以下の節を読んで、パフォーマンスの問題を解決する方法を説明します。

* [データベースのパフォーマンス](../../production/using/database-performances.md)
* [Oracle データベースのエンコード](../../production/using/encoding-of-the-oracle-database.md)

## 接続の向上 {#connection-improvements}

接続の問題が発生した場合は、次の方法で解決できます。

* [接続の失敗](../../production/using/failure-to-connect.md)
* [接続のしきい値](../../production/using/connection-thresholds.md)

## 技術的なトラブルシューティング {#technical-troubleshooting}

具体的な問題については、次の節を参照してください。

* [Linux でのスタックトレース](../../production/using/stack-trace-in-linux.md)
* [JSP の動作](../../production/using/jsp-behavior.md)
* [Tomcat バージョンの検索](../../production/using/locate-tomcat-version.md)
