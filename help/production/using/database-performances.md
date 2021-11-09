---
product: campaign
title: データベースのパフォーマンス
description: データベースのパフォーマンス
audience: production
content-type: reference
topic-tags: troubleshooting
exl-id: 33dcfd4b-51fd-44f4-98e0-23eafb79d7da
source-git-commit: bd9f035db1cbad883e1f27fe901e34dfbc9c1229
workflow-type: tm+mt
source-wordcount: '490'
ht-degree: 8%

---

# データベースのパフォーマンス{#database-performances}

![](../../assets/v7-only.svg)

パフォーマンスの問題の多くは、データベースのメンテナンスに関連しています。 パフォーマンスが低下する原因を見つけるのに役立つ主な 4 つのリードを次に示します。

* 設定
* Adobe Campaignプラットフォームのインストールと設定
* データベースのメンテナンス
* リアルタイム診断

## 設定 {#configuration}

最初のAdobe Campaignプラットフォーム設定が引き続き有効であることを確認し、必要に応じて、配信品質またはデータベースサイズの観点から、お客様のニーズを再評価します。 また、完全なハードウェアチェック（CPU、RAM、IO システム）を実行することをお勧めします。

>[!NOTE]
>
>以下を参照してください。 [Adobe Campaign Hardware Sizing ガイド](https://helpx.adobe.com/jp/campaign/kb/hardware-sizing-guide.html) インサイト用

## Platform の設定 {#platform-configuration}

不適切な設定は、プラットフォームのパフォーマンスに影響を与える可能性があります。 ネットワークの設定、プラットフォームの配信品質オプション、MTA の設定を、 **serverConf.xml** ファイル。

## データベースのメンテナンス {#database-maintenance}

**データベースのクリーンアップタスク**

データベースのクリーンアップタスクが動作していることを確認してください。 これをおこなうには、ログファイルを表示して、エラーが含まれているかどうかを確認します。 詳しくは、[この節](../../production/using/database-cleanup-workflow.md)を参照してください。

**メンテナンスプラン**

データベースのメンテナンスが正しくスケジュールされ、実行されていることを確認します。 これをおこなうには、データベース管理者に問い合わせて、次の詳細を確認してください。

* メンテナンススケジュール
* 以前に実行したメンテナンスプラン
* スクリプトログの表示

詳しくは、[この節](../../production/using/recommendations.md)を参照してください。

>[!IMPORTANT]
>
>ミッドソーシング設定を使用する場合は、データベースを定期的に管理する必要があります。 マーケティングプラットフォームで配信を分析する際、マーケティングインスタンスはミッドソーシングインスタンスに情報を送信します。 プロセスが遅くなると、マーケティングインスタンスに影響が出ます。

**作業用テーブルの管理**

作業用テーブルの数とサイズを確認してください。 特定のサイズを超えると、データベースのパフォーマンスに影響します。 これらのテーブルは、ワークフローと配信によって作成されます。 ワークフローと配信がアクティブな間、これらはデータベースに残ります。 作業用テーブルのサイズを制限するには、次の操作を実行します。

* 次のステータスの配信を停止または削除します。 **[!UICONTROL 失敗]**, **[!UICONTROL 処理中]**, **[!UICONTROL 配信準備完了]**&#x200B;または **[!UICONTROL 一時停止]**.
* エラーが原因で一時停止したワークフローを停止または削除します。
* 次の項目を含まないテストに使用されるすべてのワークフローを停止 **[!UICONTROL 終了]** その状態が残っている活動 **[!UICONTROL 一時停止]**.

>[!IMPORTANT]
>
>操作に時間がかかり、大量の空き容量が解放される場合は、詳細なメンテナンス（インデックスの再構築など）が必要です。 詳しくは、[この節](../../production/using/recommendations.md)を参照してください。

**Adobe Campaignプロセス監視**

Adobe Campaignのインストール設定に応じて、プラットフォームの監視には次の 2 つのツールを使用できます。

* インスタンス実稼動ページ。 詳しくは、 [手動監視](../../production/using/monitoring-processes.md#manual-monitoring).
* この *netreport* スクリプト 詳しくは、 [Adobe Campaignスクリプトを使用した自動監視](../../production/using/monitoring-processes.md#automatic-monitoring-via-adobe-campaign-scripts).

## 詳細 {#specifics}

問題の原因を特定するために、リアルタイム診断を実行する必要が生じる場合があります。 まず、プロセスとプラットフォームのログファイルを確認し、問題を再作成しながらデータベースのアクティビティを監視します。 特に、以下の点に注意してください。

* メンテナンス実行プラン
* 実行中の SQL クエリ
* 外部プロセスが同時に実行されているかどうか（クレンジング、インポート、集計計算など）。
