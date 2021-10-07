---
product: campaign
title: 維持するテーブル
description: 維持するテーブル
audience: production
content-type: reference
topic-tags: database-maintenance
exl-id: 194f12de-4671-4a56-8cdc-cd5e3dac147b
source-git-commit: 20509f44c5b8e0827a09f44dffdf2ec9d11652a1
workflow-type: tm+mt
source-wordcount: '1123'
ht-degree: 3%

---

# 維持するテーブル{#tables-to-maintain}

![](../../assets/v7-only.svg)

保持するテーブルのリストは、Adobe Campaignのバージョン、使用方法、データモデル設定によって異なります。

次のリストには、断片化の対象として最も多いテーブルのみが表示されます。 影響は次のとおりです。

* ディスク領域の過剰消費により、データベース・アクセスに影響を与える
* 定期的に更新されていないインデックスがあり、クエリのパフォーマンスが低下します。

## Adobe Campaignテーブル {#adobe-campaign-tables}

<table> 
 <thead> 
  <tr> 
   <th> <strong>テーブル名 </strong><br /> </th> 
   <th> <strong>サイズ</strong><br /> </th> 
   <th> <strong>アクティビティの主なタイプ</strong><br /> </th> 
   <th> <strong>コメント</strong><br /> </th> 
  </tr> 
 </thead> 
 <tbody> 
  <tr> 
   <td> NmsDelivery<br /> </td> 
   <td> 小 <br /> </td> 
   <td> アップデート<br /> </td> 
   <td> 配信アクションごとに 1 つのレコードがあります。 1 つのレコードは、配信の進行状況を反映するために複数回更新できるので、このテーブルのインデックスは急速にフラグメント化する傾向があります。<br /> </td> 
  </tr> 
  <tr> 
   <td> NmsDeliveryPart<br /> </td> 
   <td> 中<br /> </td> 
   <td> 挿入、更新、削除 <br /> </td> 
   <td> 配信の準備中にレコードが挿入される作業用テーブル。 その後、配信中に更新され、配信が完了すると最後に削除されます。<br /> このテーブルは、平均サイズがかなり限られているにもかかわらず、急速にフラグメント化する傾向があります。<br /> </td> 
  </tr> 
  <tr> 
   <td> NmsMirrorPageInfo<br /> </td> 
   <td> 大<br /> </td> 
   <td> 挿入、削除 <br /> </td> 
   <td> この表には、パーソナライズされたミラーページの生成に必要な情報が含まれています。 メモ (CLOB) フィールドが含まれているので、非常に大きい傾向があります。 ボリュームは、保持するミラーページの履歴に正比例します。<br /> </td> 
  </tr> 
  <tr> 
   <td> NmsDeliveryStat<br /> </td> 
   <td> 中<br /> </td> 
   <td> 挿入、更新、削除 <br /> </td> 
   <td> このテーブルには、配信プロセスに関する統計情報が含まれています。 レコードは定期的に更新されます。<br /> </td> 
  </tr> 
  <tr> 
   <td> NmsAddress<br /> </td> 
   <td> 中<br /> </td> 
   <td> 更新、挿入 <br /> </td> 
   <td> このテーブルには、E メールアドレスに関する情報が含まれます。 この値は、強制隔離プロセスの一環として頻繁に更新されます（最初の配信エラー時にレコードが作成され、配信が正常に完了するとカウンターが変更および削除されます）。<br /> </td> 
  </tr> 
  <tr> 
   <td> XtkWorkflow<br /> </td> 
   <td> 小 <br /> </td> 
   <td> アップデート<br /> </td> 
   <td> ワークフローインスタンスごとに 1 つのレコードがあるので、レコードはほとんどありません。 ただし、テーブルは定期的に更新され、ステータスと進行状況を反映します。<br /> </td> 
  </tr> 
  <tr> 
   <td> XtkWorkflowTask<br /> </td> 
   <td> 小 <br /> </td> 
   <td> 挿入、更新、削除 <br /> </td> 
   <td> ワークフローアクティビティを実行するたびに、このテーブルにレコードが作成されます。 パージメカニズムは、期限切れになると削除します。<br /> </td> 
  </tr> 
  <tr> 
   <td> XtkWorkflowEvent<br /> </td> 
   <td> 小 <br /> </td> 
   <td> 挿入、更新、削除 <br /> </td> 
   <td> ワークフロー内のタスク間でアクティブ化された各トランジションは、このテーブル内にレコードを作成します。 パージメカニズムは、期限切れになると削除します。<br /> </td> 
  </tr> 
  <tr> 
   <td> XtkWorkflowJob<br /> </td> 
   <td> 非常に小さい <br /> </td> 
   <td> 挿入、更新、削除 <br /> </td> 
   <td> このテーブルはワークフローエンジンに固有です。 ワークフローへのコマンドの送信（開始、停止、一時停止など）が可能です。 このテーブルは小さいですが、ワークフローにリンクされたトランザクションテーブルのパージ中にこのテーブルが考慮されます。<br /> </td> 
  </tr> 
  <tr> 
   <td> NmsBroadLog<br /> </td> 
   <td> 最大 <br /> </td> 
   <td> 挿入、更新、削除 <br /> </td> 
   <td> これはシステム内で最も大きなテーブルです。 送信されるメッセージごとに 1 つのレコードがあり、これらのレコードが挿入され、配信ステータスを追跡するように更新され、履歴がパージされると削除されます。<br /> </td> 
  </tr> 
  <tr> 
   <td> NmsTrackingLog<br /> </td> 
   <td> 大<br /> </td> 
   <td> 挿入、削除 <br /> </td> 
   <td> 履歴がパージされると、トラッキングログは挿入および削除されますが、更新はされません。<br /> </td> 
  </tr> 
  <tr> 
   <td> NmsBroadlogMsg <br /> </td> 
   <td> 小 <br /> </td> 
   <td> アップデート<br /> </td> 
   <td> この表は、SMTP エラーの検証に使用する情報を示しています。 この値はかなり小さいですが、大量に更新されるので、このテーブルのインデックスは急速にフラグメント化する傾向があります。<br /> </td> 
  </tr> 
  <tr> 
   <td> NmsEmailErrorStat<br /> </td> 
   <td> 中<br /> </td> 
   <td> 挿入、更新、削除 <br /> </td> 
   <td> この表には、SMTP エラーの集計がドメイン別に並べ替えられています。 最初は、クリーンアップタスクが期限切れになった後にクリーンアップタスクによって集計される詳細な情報が含まれます。<br /> </td> 
  </tr> 
  <tr> 
   <td> NmsBroadLogMid（ミッドソーシングインスタンスの場合）<br /> </td> 
   <td> 大<br /> </td> 
   <td> 挿入、更新、削除 <br /> </td> 
   <td> 5.10 以降のインスタンスがミッドソーシングインスタンスとして使用される場合のみ。 これは、データベース内で最も大きいテーブルの 1 つです。 送信されるメッセージごとに 1 つのレコードがあり、これらのレコードが挿入され、配信ステータスを追跡するように更新され、履歴がパージされると削除されます。 ミッドソーシングを使用する場合は、履歴を制限することをお勧めします（通常は 2 ヶ月未満）。この表は、サイズの面では妥当ですが（6,000 万行、データ+インデックスの場合は 30 Go 未満）、時々再構築することが非常に重要です。<br /> </td> 
  </tr> 
  <tr> 
   <td> NmsBroadLogRcp （NmsRecipient テーブルを使用する場合） <br /> </td> 
   <td> 大<br /> </td> 
   <td> 挿入、更新、削除 <br /> </td> 
   <td> これはシステム内で最も大きなテーブルです。 送信されるメッセージごとに 1 つのレコードがあり、これらのレコードが挿入され、配信ステータスを追跡するように更新され、履歴がパージされると削除されます。 5.10 では、SMTP メッセージテキストが 5.10 バージョンの NmsBroadLogMsg テーブルに組み込まれるので、このテーブルは 4.05(NmsBroadLog) の同等のテーブルよりも小さいことに注意してください。 ただし、このテーブルを定期的に（最初は 1 週間おきに）再インデックス化し、時々（月に 1 回、またはパフォーマンスに影響が出た場合）完全に再構築する必要があります。<br /> </td> 
  </tr> 
  <tr> 
   <td> YyyBroadLogXxx （外部の受信者テーブルを使用する場合）<br /> </td> 
   <td> 大<br /> </td> 
   <td> 挿入、更新、削除 <br /> </td> 
   <td> NmsBroadLogRcp と同じですが、外部の受信者テーブルがあります。 Yyy および Xxx は、配信マッピングの値に合わせて調整してください。<br /> </td> 
  </tr> 
  <tr> 
   <td> NmsTrackingLogRcp （NmsRecipient テーブルを使用する場合） <br /> </td> 
   <td> 大<br /> </td> 
   <td> 挿入、削除 <br /> </td> 
   <td> 履歴がパージされると、トラッキングログは挿入および削除されますが、更新はされません。 ボリュームは、データ保持の長さによって異なります。<br /> </td> 
  </tr> 
  <tr> 
   <td> YyyTrackingLogXxx （外部の受信者テーブルを使用する場合）<br /> </td> 
   <td> 大<br /> </td> 
   <td> 挿入、削除 <br /> </td> 
   <td> NmsTrackingLogRcp と同じですが、外部の受信者テーブルがあります。 Yyy および Xxx は、配信マッピングで使用する値に合わせて調整してください。<br /> </td> 
  </tr> 
  <tr> 
   <td> NmsBroadLogRtEvent（Message Center 実行インスタンス）<br /> </td> 
   <td> 大<br /> </td> 
   <td> 挿入、更新、削除 <br /> </td> 
   <td> 他の broadLog テーブルと同様ですが、NmsRecipient.<br /> ではなく NmsRtEvent を使用します。 </td> 
  </tr> 
  <tr> 
   <td> NmsTrackingLogRtEvent（ Message Center 実行インスタンス）<br /> </td> 
   <td> 大<br /> </td> 
   <td> 挿入、削除 <br /> </td> 
   <td> 他の trackingLog テーブルと同様ですが、NmsRecipient.<br /> ではなく NmsRtEvent テーブルを使用します。 </td> 
  </tr> 
  <tr> 
   <td> NmsRtEvent（Message Center 実行インスタンス）<br /> </td> 
   <td> 大<br /> </td> 
   <td> 挿入、更新、削除 <br /> </td> 
   <td> Message Center のイベントキューを含む表。 これらのイベントのステータスは、処理時に Message Center によって更新されます。 削除はパージ中に実行されます。 このテーブルのインデックスを定期的に再作成し、再構築することをお勧めします。<br /> </td> 
  </tr> 
  <tr> 
   <td> NmsEventHisto（Message Center コントロールインスタンス）<br /> </td> 
   <td> 大<br /> </td> 
   <td> 挿入、更新、削除 <br /> </td> 
   <td> NmsRtEvent と同様です。 この表は、すべての実行インスタンスのすべてのイベントをアーカイブします。 リアルタイムのプロセスではなく、レポートでのみ使用されます。<br /> </td> 
  </tr> 
  <tr> 
   <td> NmsMobileApp<br /> </td> 
   <td> 非常に小さい <br /> </td> 
   <td> 挿入、更新、削除 <br /> </td> 
   <td> モバイルアプリケーションとその設定を含む表。<br /> </td> 
  </tr> 
  <tr> 
   <td> NmsAppSubscriptionRcp<br /> </td> 
   <td> 大<br /> </td> 
   <td> 挿入、更新 <br /> </td> 
   <td> 通知の送信に使用するモバイルデバイス（アドレス）の識別子を含む表（受信者の表と同様）。<br /> </td> 
  </tr> 
  <tr> 
   <td> NmsBroadLogAppSubRcp<br /> </td> 
   <td> 大<br /> </td> 
   <td> 挿入、更新、削除 <br /> </td> 
   <td> 他の broadLog テーブルと同様ですが、NmsRecipient.<br /> ではなく NmsappSubscriptionRcp を使用します。 </td> 
  </tr> 
  <tr> 
   <td> NmsTrackingLogAppSubRcp<br /> </td> 
   <td> 大<br /> </td> 
   <td> 挿入、削除 <br /> </td> 
   <td> 他の trackingLog テーブルと同様ですが、NmsRecipient.<br /> ではなく NmsappSubscriptionRcp テーブルを使用します。 </td> 
  </tr> 
  <tr> 
   <td> XtkSessionInfo<br /> </td> 
   <td> 小 <br /> </td> 
   <td> 挿入、削除 <br /> </td> 
   <td> ユーザーセッションを含むテーブル。 挿入と削除の数は非常に重要です。<br /> </td> 
  </tr> 
 </tbody> 
</table>

## 顧客テーブル {#customer-tables}

上記のリストに加えて、(Adobe Campaignデータモデルに存在しない ) プラットフォームの設定時に顧客が作成したテーブルも、断片化の対象になる場合があります。特に、データの読み込みや同期の手順時に頻繁に更新される場合があります。 これらのテーブルは、デフォルトのAdobe Campaignデータモデルの一部にすることができます（例：**NmsRecipient**）。 この場合、Adobe Campaignプラットフォームの管理者が、特定のデータベースモデルを監査して、これらのカスタムテーブルを見つけます。 これらの表は、必ずしもメンテナンス手順で明示的に言及されているわけではありません。
