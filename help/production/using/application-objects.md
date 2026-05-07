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
source-wordcount: '523'
ht-degree: 9%

---

# アプリケーションオブジェクト{#application-objects}



組み込みオブジェクトは監視する必要があり、それらを過度に成長させないようにすることが重要です。

## ID シーケンス {#sequence-of-ids}

Adobe Campaignでは、それに応じて消費する必要があるID シーケンスが使用されています：**xtkNewId**。 シーケンスが非常に迅速に消費される場合（1日あたり10万から）、1日あたり数百万メールを送信するなど、ビジネス要件に合致していることを確認する必要があります。 特定のテーブルの専用シーケンスを定義できます。 IDの使用状況を監視するワークフローを設定できます。

シーケンスが20億以上（2,147,483,648が正確な数）に達すると、ゼロに戻ります。 それは回避されなければならず、問題を生み出す必要があります。そのため、このシーケンスを監視する必要があります。

大きなテーブルでこれを防ぐには、特定のシーケンスを使用することを検討してください。 これは、スキーマの&#x200B;**pkSequence**&#x200B;属性を使用して実行できます。

多数のログを作成する高頻度のワークフローでは、多くのIDが使用されます。 そのため、ワークフロー内のログが多すぎたり、高頻度になったりすることを避けることが強くお勧めします。

シーケンスが既に循環している場合、最善の解決策は–2,147,483,648から始まる負のIDに切り替えることです。

## フォルダー {#folders}

どのインスタンスにも1000未満のフォルダーが存在する必要があります。 これより多くのフォルダーがあると、Campaign クライアントのパフォーマンスに問題が発生する可能性があります。 監視ジョブを設定して、フォルダー数やワークフロー数などをカウントし、定期的にレポートを作成できます。

この方法は、オブジェクトを作成しすぎているユーザーにも表示されます。

## 配信 {#deliveries}

インスタンスには、常に1000未満の配信が存在する必要があります。 配信が多いと、データベースの容量が消費され、問題が発生します。 1日に10件を超える配信を作成するインスタンスは、ビジネス要件に照らし合わせてチェックする必要があります。 より少ない配信数を実現するために、継続的な配信の使用を検討する。 詳しくは、[Campaign v8 ドキュメント](https://experienceleague.adobe.com/docs/campaign/automation/workflows/wf-activities/action-activities/continuous-delivery.html?lang=ja){target="_blank"}を参照してください。

2年以上の配信は、インスタンスからパージする必要があります。

## ファイル {#files}

アプリケーションサーバーディスク上のファイルの数は無期限に増加しないでください。

インポートワークフローはファイルを作成するため、ディスクの拡張が発生します。 これは、標準の[&#x200B; ファイルコレクター](https://experienceleague.adobe.com/docs/campaign/automation/workflows/wf-activities/event-activities/file-collector.html?lang=ja){target="_blank"} アクティビティを使用することで防ぐことができます。 ファイルコレクターは一時フォルダーにファイルを移動し、自動的にパージします。

ワークフローがファイルを読み込み、標準機能を使用しない場合は、ディスク容量を最小限に抑えるためにパージする必要があります。

## トランザクションデータとログ {#transactional-data-and-logs}

Adobe Campaignにデータを読み込むワークフローごとに、データベースのサイズが大きくなります。 [Campaign v8 ドキュメント](https://experienceleague.adobe.com/docs/campaign/automation/workflows/introduction/use-workflow-data.html?lang=ja){target="_blank"}を参照してください。

クリーンアップまたはパージのワークフローが実行され、レコードが効果的にパージされていることを確認します。 すべてのトランザクションデータとログをパージする必要があります。 クリーンアップタスクでは、トラッキングログとブロックリグの標準テーブルのみがパージされます。 特定のワークフローでは、特定のテーブルをパージする必要があります。 [Campaign v8 ドキュメント](https://experienceleague.adobe.com/docs/campaign/automation/workflows/monitoring-workflows/monitor-workflow-execution.html?lang=ja){target="_blank"}を参照してください。

レコードの最も古い作成日をチェックして、トランザクションデータのエージングを監視します。
