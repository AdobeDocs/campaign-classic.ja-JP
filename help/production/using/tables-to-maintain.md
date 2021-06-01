---
product: campaign
title: 維持するテーブル
description: 維持するテーブル
audience: production
content-type: reference
topic-tags: database-maintenance
exl-id: 194f12de-4671-4a56-8cdc-cd5e3dac147b
source-git-commit: 98d646919fedc66ee9145522ad0c5f15b25dbf2e
workflow-type: tm+mt
source-wordcount: '1123'
ht-degree: 3%

---

# 維持するテーブル{#tables-to-maintain}

保持するテーブルのリストは、Adobe Campaignのバージョン、使用方法、データモデル設定によって異なります。

次のリストには、断片化の対象となるテーブルのみが表示されます。 影響は次のとおりです。

* ディスク領域の過剰消費により、データベース・アクセスに影響を与える
* 定期的に更新されていないインデックスがあり、クエリのパフォーマンスが低下します。

## Adobe Campaignテーブル{#adobe-campaign-tables}

<table> 
 <thead> 
  <tr> 
   <th> <strong>テーブル名 </strong><br /> </th> 
   <th> <strong>サイズ</strong><br /> </th> 
   <th> <strong>アクティビティのメインタイプ</strong><br /> </th> 
   <th> <strong>コメント</strong><br /> </th> 
  </tr> 
 </thead> 
 <tbody> 
  <tr> 
   <td> NmsDelivery<br /> </td> 
   <td> 小<br /> </td> 
   <td> アップデート<br /> </td> 
   <td> 配信アクションごとに1つのレコードがあります。 1つのレコードは、配信の進行状況を反映するために複数回更新される可能性があるので、このテーブルのインデックスは急速にフラグメント化する傾向があります。<br /> </td> 
  </tr> 
  <tr> 
   <td> NmsDeliveryPart<br /> </td> 
   <td> 中<br /> </td> 
   <td> 挿入、更新、削除<br /> </td> 
   <td> 配信の準備中にレコードが挿入される作業用テーブル。 その後、配信中に更新され、配信が完了すると最終的に削除されます。<br /> このテーブルは、平均サイズがかなり制限されているにもかかわらず、急速にフラグメント化する傾向があります。<br /> </td> 
  </tr> 
  <tr> 
   <td> NmsMirrorPageInfo<br /> </td> 
   <td> 大<br /> </td> 
   <td> 挿入、削除<br /> </td> 
   <td> この表には、パーソナライズされたミラーページの生成に必要な情報が含まれます。 メモ(CLOB)フィールドが含まれているので、非常に大きくなりがちです。 ボリュームは、保持するミラーページの履歴に正比例します。<br /> </td> 
  </tr> 
  <tr> 
   <td> NmsDeliveryStat<br /> </td> 
   <td> 中<br /> </td> 
   <td> 挿入、更新、削除<br /> </td> 
   <td> このテーブルには、配信プロセスに関する統計情報が含まれています。 レコードは定期的に更新されます。<br /> </td> 
  </tr> 
  <tr> 
   <td> NmsAddress<br /> </td> 
   <td> 中<br /> </td> 
   <td> 更新、挿入<br /> </td> 
   <td> このテーブルには、Eメールアドレスに関する情報が含まれます。 このレポートは、強制隔離プロセスの一環として頻繁に更新されます（最初の配信エラー時にレコードが作成され、配信が正常に完了するとカウンターが変更および削除されます）。<br /> </td> 
  </tr> 
  <tr> 
   <td> XtkWorkflow<br /> </td> 
   <td> 小<br /> </td> 
   <td> アップデート<br /> </td> 
   <td> ワークフローインスタンスごとに1つのレコードがあるので、レコード数は非常に少なくなります。 ただし、テーブルは定期的に更新され、ステータスと進行状況が反映されます。<br /> </td> 
  </tr> 
  <tr> 
   <td> XtkWorkflowTask<br /> </td> 
   <td> 小<br /> </td> 
   <td> 挿入、更新、削除<br /> </td> 
   <td> ワークフローアクティビティを実行するたびに、このテーブルにレコードが作成されます。 パージメカニズムは、期限切れになると削除します。<br /> </td> 
  </tr> 
  <tr> 
   <td> XtkWorkflowEvent<br /> </td> 
   <td> 小<br /> </td> 
   <td> 挿入、更新、削除<br /> </td> 
   <td> ワークフロー内のタスク間でアクティブ化された各トランジションは、このテーブル内にレコードを作成します。 パージメカニズムは、期限切れになると削除します。<br /> </td> 
  </tr> 
  <tr> 
   <td> XtkWorkflowJob<br /> </td> 
   <td> 非常に小さい<br /> </td> 
   <td> 挿入、更新、削除<br /> </td> 
   <td> このテーブルはワークフローエンジンに固有です。 ワークフローへのコマンドの送信（例えば、開始、停止、一時停止）を可能にします。 ワークフローにリンクされたトランザクションテーブルのパージ中に、このテーブルが考慮されます。<br /> </td> 
  </tr> 
  <tr> 
   <td> NmsBroadLog<br /> </td> 
   <td> 最大<br /> </td> 
   <td> 挿入、更新、削除<br /> </td> 
   <td> これはシステム内で最も大きなテーブルです。 送信されたメッセージごとに1件のレコードがあり、これらのレコードが挿入され、配信ステータスを追跡するために更新され、履歴がパージされると削除されます。<br /> </td> 
  </tr> 
  <tr> 
   <td> NmsTrackingLog<br /> </td> 
   <td> 大<br /> </td> 
   <td> 挿入、削除<br /> </td> 
   <td> 履歴がパージされると、トラッキングログは挿入および削除されますが、更新はされません。<br /> </td> 
  </tr> 
  <tr> 
   <td> NmsBroadlogMsg <br /> </td> 
   <td> 小<br /> </td> 
   <td> アップデート<br /> </td> 
   <td> この表には、SMTPエラーの検証に使用する情報が含まれます。 これはかなり小さいものの、大規模に更新されるので、このテーブルのインデックスは急速にフラグメント化する傾向があります。<br /> </td> 
  </tr> 
  <tr> 
   <td> NmsEmailErrorStat<br /> </td> 
   <td> 中<br /> </td> 
   <td> 挿入、更新、削除<br /> </td> 
   <td> この表には、SMTPエラーの集計がドメイン別に並べ替えられています。 最初は、クリーンアップタスクが期限切れになった後にクリーンアップタスクによって集計される詳細情報が含まれます。<br /> </td> 
  </tr> 
  <tr> 
   <td> NmsBroadLogMid（ミッドソーシングインスタンスの場合）<br /> </td> 
   <td> 大<br /> </td> 
   <td> 挿入、更新、削除<br /> </td> 
   <td> 5.10（以降）インスタンスがミッドソーシングインスタンスとして使用される場合のみ。 これは、データベース内で最も大きいテーブルの1つです。 送信されたメッセージごとに1件のレコードがあり、これらのレコードが挿入され、配信ステータスを追跡するために更新され、履歴がパージされると削除されます。 ミッドソーシングを使用する場合、履歴を制限することをお勧めします（通常は2ヶ月未満）。このテーブルは、サイズ（6,000万行、データ+インデックスの場合は30 Go未満）が妥当ですが、時々再構築することが非常に重要です。<br /> </td> 
  </tr> 
  <tr> 
   <td> NmsBroadLogRcp（NmsRecipientテーブルを使用する場合） <br /> </td> 
   <td> 大<br /> </td> 
   <td> 挿入、更新、削除<br /> </td> 
   <td> これはシステム内で最も大きなテーブルです。 送信されたメッセージごとに1件のレコードがあり、これらのレコードが挿入され、配信ステータスを追跡するために更新され、履歴がパージされると削除されます。 5.10では、SMTPメッセージテキストが5.10バージョンのNmsBroadLogMsgテーブルに分解されているので、このテーブルは4.05(NmsBroadLog)での同等のテーブルよりも小さいことに注意してください。 ただし、このテーブルのインデックスを定期的に再作成し（最初は1週間おき）、時々（月に1回、またはパフォーマンスに影響が出た場合）、完全に再構築する必要があります。<br /> </td> 
  </tr> 
  <tr> 
   <td> YyyBroadLogXxx（外部の受信者テーブルを使用する場合）<br /> </td> 
   <td> 大<br /> </td> 
   <td> 挿入、更新、削除<br /> </td> 
   <td> NmsBroadLogRcpと同じですが、外部の受信者テーブルがあります。 配信マッピングの値を使用して、YyyおよびXxxを適応させてください。<br /> </td> 
  </tr> 
  <tr> 
   <td> NmsTrackingLogRcp （NmsRecipientテーブルを使用する場合） <br /> </td> 
   <td> 大<br /> </td> 
   <td> 挿入、削除<br /> </td> 
   <td> 履歴がパージされると、トラッキングログは挿入および削除されますが、更新はされません。 ボリュームは、データ保持の長さによって異なります。<br /> </td> 
  </tr> 
  <tr> 
   <td> YyyTrackingLogXxx（外部の受信者テーブルを使用する場合）<br /> </td> 
   <td> 大<br /> </td> 
   <td> 挿入、削除<br /> </td> 
   <td> NmsTrackingLogRcpと同じですが、外部の受信者テーブルがある場合。 配信マッピングで使用する値を使用して、YyyおよびXxxを適応させてください。<br /> </td> 
  </tr> 
  <tr> 
   <td> NmsBroadLogRtEvent（Message Center実行インスタンス）<br /> </td> 
   <td> 大<br /> </td> 
   <td> 挿入、更新、削除<br /> </td> 
   <td> 他のbroadlogテーブルと同様ですが、NmsRecipient.<br />ではなくNmsRtEventを使用します。 </td> 
  </tr> 
  <tr> 
   <td> NmsTrackingLogRtEvent（ Message Center実行インスタンス）<br /> </td> 
   <td> 大<br /> </td> 
   <td> 挿入、削除<br /> </td> 
   <td> 他のtrackingLogテーブルと同様ですが、NmsRecipient.<br />ではなくNmsRtEventテーブルを使用します。 </td> 
  </tr> 
  <tr> 
   <td> NmsRtEvent（Message Center実行インスタンス）<br /> </td> 
   <td> 大<br /> </td> 
   <td> 挿入、更新、削除<br /> </td> 
   <td> Message Centerのイベントキューを含む表。 これらのイベントのステータスは、処理時にMessage Centerによって更新されます。 削除はパージ中に実行されます。 このテーブルのインデックスを定期的に再作成し、再構築することをお勧めします。<br /> </td> 
  </tr> 
  <tr> 
   <td> NmsEventHisto（Message Centerコントロールインスタンス）<br /> </td> 
   <td> 大<br /> </td> 
   <td> 挿入、更新、削除<br /> </td> 
   <td> NmsRtEventと同様です。 この表は、すべての実行インスタンスからすべてのイベントをアーカイブします。 リアルタイムプロセスではなく、レポートでのみ使用されます。<br /> </td> 
  </tr> 
  <tr> 
   <td> NmsMobileApp<br /> </td> 
   <td> 非常に小さい<br /> </td> 
   <td> 挿入、更新、削除<br /> </td> 
   <td> モバイルアプリケーションとその設定を含む表。<br /> </td> 
  </tr> 
  <tr> 
   <td> NmsAppSubscriptionRcp<br /> </td> 
   <td> 大<br /> </td> 
   <td> 挿入、更新<br /> </td> 
   <td> 通知の送信に使用するモバイルデバイス（アドレス）の識別子を含む表（受信者の表と同様）。<br /> </td> 
  </tr> 
  <tr> 
   <td> NmsBroadLogAppSubRcp<br /> </td> 
   <td> 大<br /> </td> 
   <td> 挿入、更新、削除<br /> </td> 
   <td> 他のbroadlogテーブルと同様ですが、NmsRecipient.<br />ではなく、NmsappSubscriptionRcpを使用します。 </td> 
  </tr> 
  <tr> 
   <td> NmsTrackingLogAppSubRcp<br /> </td> 
   <td> 大<br /> </td> 
   <td> 挿入、削除<br /> </td> 
   <td> 他のtrackingLogテーブルと同様ですが、NmsRecipient.<br />ではなくNmsappSubscriptionRcpテーブルを使用します。 </td> 
  </tr> 
  <tr> 
   <td> XtkSessionInfo<br /> </td> 
   <td> 小<br /> </td> 
   <td> 挿入、削除<br /> </td> 
   <td> ユーザーセッションを含むテーブル。 挿入と削除の数は非常に重要です。<br /> </td> 
  </tr> 
 </tbody> 
</table>

## 顧客テーブル{#customer-tables}

上記のリストに加えて、プラットフォームの設定時に(Adobe Campaignデータモデルに存在しない)お客様が作成したテーブルも、フラグメント化の対象になる場合があります。特に、データの読み込みや同期の手順で頻繁に更新される場合があります。 これらのテーブルは、デフォルトのAdobe Campaignデータモデルの一部にすることができます（例えば、**NmsRecipient**）。 この場合、Adobe Campaignプラットフォームの管理者が、特定のデータベースモデルを監査して、これらのカスタムテーブルを見つける必要があります。 これらのテーブルは、必ずしもメンテナンス手順で明示的に言及されているわけではありません。
