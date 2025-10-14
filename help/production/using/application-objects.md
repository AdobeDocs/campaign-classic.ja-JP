---
product: campaign
title: アプリケーションオブジェクト
description: アプリケーションオブジェクト
feature: Monitoring
audience: production
content-type: reference
topic-tags: database-maintenance
exl-id: fb4798d7-0a2c-455b-86b6-3dcb5fd25c82
source-git-commit: ad6f3f2cf242d28de9e6da5cec100e096c5cbec2
workflow-type: tm+mt
source-wordcount: '480'
ht-degree: 2%

---

# アプリケーションオブジェクト{#application-objects}



組み込みオブジェクトは監視して、過度に大きくならないようにすることが重要です。

## ID のシーケンス {#sequence-of-ids}

Adobe Campaignは、それに応じて使用する必要がある ID シーケンスを使用します：**xtkNewId**。 シーケンスが非常に迅速に（1 日あたり 100,000 件から）消費される場合、1 日に数百万のメールを送信するなど、ビジネス要件に一致していることを確認する必要があります。 特定のテーブルに専用のシーケンスを定義できます。 ID の使用状況を監視するワークフローを設定できます。

シーケンスが 20 億以上（2,147,483,648 が正確な数）に達すると、ゼロに戻ります。 このシーケンスを監視する必要があるのは、これを避けて問題を発生させる必要があります。

大きなテーブルでこれを防ぐには、特定のシーケンスの使用を検討します。 これは、スキーマの **pkSequence** 属性を使用して実行できます。

多数のログを作成する高頻度ワークフローでは、多数の ID が使用されます。 したがって、ワークフローでのログの数が多くなりすぎたり高頻度になることを避けることを強くお勧めします。

シーケンスがすでにサイクルされている場合は、-2,147,483,648 から負の ID に切り替えることが最適な解決策です。

## フォルダー {#folders}

インスタンスのフォルダー数は 1,000 個未満にする必要があります。 これ以上のフォルダーがあると、Campaign クライアントでパフォーマンスの問題が発生する可能性があります。 監視ジョブを設定して、フォルダーやワークフローなどの数をカウントし、定期的にレポートを返すことができます。

この方法では、作成するオブジェクトが多すぎるユーザーも強調表示されます。

## 配信 {#deliveries}

インスタンスに存在する配信の数は常に 1000 個未満にする必要があります。 多くの配信を使用すると、データベース領域が消費され、問題が発生します。 1 日に 10 件を超える配信を作成するインスタンスは、ビジネス要件に照らして確認する必要があります。 連続配信を使用して、作成する配信の数を減らすことを検討してください。 詳しくは、[Campaign v8 ドキュメント ](https://experienceleague.adobe.com/docs/campaign/automation/workflows/wf-activities/action-activities/continuous-delivery.html){target="_blank"} を参照してください。

2 年以上前の配信はインスタンスからパージする必要があります。

## ファイル {#files}

アプリケーションサーバーのディスク上のファイル数は、無制限に増えることはできません。

インポートワークフローではファイルが作成されるので、ディスクが拡張されます。 この問題は、標準の [ ファイルコレクター ](https://experienceleague.adobe.com/docs/campaign/automation/workflows/wf-activities/event-activities/file-collector.html){target="_blank"} アクティビティを使用することで回避できます。 ファイルコレクターは、ファイルを一時フォルダーに移動し、自動的にパージします。

ワークフローでファイルをインポートしても標準の機能が使用されない場合は、ディスク領域を最小限に抑えるために、ワークフローをパージする必要があります。

## トランザクションデータとログ {#transactional-data-and-logs}

データをAdobe Campaignに読み込むワークフローによって、データベースのサイズが大きくなります。 [Campaign v8 ドキュメント ](https://experienceleague.adobe.com/docs/campaign/automation/workflows/introduction/use-workflow-data.html?lang=ja){target="_blank"} を参照してください。

クリーンアップまたはパージワークフローが実行中であり、レコードを効果的にパージしていることを確認します。 すべてのトランザクションデータとログはパージする必要があります。 クリーンアップタスクでは、標準テーブル（トラッキングログと広範ログ）のみをパージします。 特定のテーブルは、特定のワークフローによってパージする必要があります。 [Campaign v8 ドキュメント ](https://experienceleague.adobe.com/docs/campaign/automation/workflows/monitoring-workflows/monitor-workflow-execution.html?lang=ja){target="_blank"} を参照してください。

レコードの最も古い作成日を確認して、古いトランザクションデータを監視します。
