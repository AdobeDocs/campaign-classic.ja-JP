---
title: 保守するテーブル
seo-title: 保守するテーブル
description: 保守するテーブル
seo-description: null
page-status-flag: never-activated
uuid: 1085e929-65cc-48fa-9c31-0508a14b4704
contentOwner: sauviat
products: SG_CAMPAIGN/CLASSIC
audience: production
content-type: reference
topic-tags: database-maintenance
discoiquuid: 6ec4e566-7116-4d7f-835d-cb0f3c3a6a7a
index: y
internal: n
snippet: y
translation-type: tm+mt
source-git-commit: 579329d9194115065dff2c192deb0376c75e67bd

---


# 保守するテーブル{#tables-to-maintain}

保守する表のリストは、使用するAdobe Campaignのバージョン、使用方法およびデータモデル設定によって異なります。

次のリストには、フラグメンテーションの対象となるテーブルのみが表示されます。 影響は次のとおりです。

* ディスク領域の過剰消費により、データベースへのアクセスに影響が及ぶ
* 定期的に更新されていないインデックスの場合、クエリのパフォーマンスが低下します。

## Adobe Campaignの表 {#adobe-campaign-tables}

<table> 
 <thead> 
  <tr> 
   <th> <strong>テーブル名 </strong><br /> </th> 
   <th> <strong>サイズ</strong><br /> </th> 
   <th> <strong>活動の主なタイプ</strong><br /> </th> 
   <th> <strong>コメント</strong><br /> </th> 
  </tr> 
 </thead> 
 <tbody> 
  <tr> 
   <td> NmsDelivery<br /> </td> 
   <td> 小<br /> </td> 
   <td> 更新<br /> </td> 
   <td> 配信アクションごとに1つのレコードがあります。 単一のレコードは、配信の進行状況を反映するために複数回更新できるので、このテーブルのインデックスは急速にフラグメント化される傾向があります。 <br /> </td> 
  </tr> 
  <tr> 
   <td> NmsDeliveryPart<br /> </td> 
   <td> 実線（中）<br /> </td> 
   <td> 挿入、更新、削除<br /> </td> 
   <td> 配信の準備中にレコードが挿入される作業テーブル。 その後、配信中に更新され、配信が完了すると最後に削除されます。<br /> このテーブルは、平均サイズがかなり制限されているにもかかわらず、速くフラグメント化される傾向があります。<br /> </td> 
  </tr> 
  <tr> 
   <td> NmsMirrorPageInfo<br /> </td> 
   <td> 大<br /> </td> 
   <td> 挿入、削除<br /> </td> 
   <td> この表には、パーソナライズされたミラーページを生成するために必要な情報が含まれています。 メモ型(CLOB)フィールドが含まれているので、非常に大きくなる傾向があります。 ボリュームは、保存されるミラーページの履歴に正比例します。 <br /> </td> 
  </tr> 
  <tr> 
   <td> NmsDeliveryStat<br /> </td> 
   <td> 実線（中）<br /> </td> 
   <td> 挿入、更新、削除<br /> </td> 
   <td> この表には、配信プロセスに関する統計が含まれています。 そのレコードは定期的に更新されます。 <br /> </td> 
  </tr> 
  <tr> 
   <td> NmsAddress<br /> </td> 
   <td> 実線（中）<br /> </td> 
   <td> 更新、挿入<br /> </td> 
   <td> この表には、電子メールアドレスに関する情報が含まれています。 検疫処理の一環として頻繁に更新されます（レコードは最初の配信エラー時に作成され、カウンターが変更され、配信が成功すると削除されます）。 <br /> </td> 
  </tr> 
  <tr> 
   <td> XtkWorkflow<br /> </td> 
   <td> 小<br /> </td> 
   <td> 更新<br /> </td> 
   <td> ワークフローインスタンスごとに1つのレコードが存在するので、レコードはほとんどありません。 ただし、ステータスと進行状況を反映して、テーブルは定期的に更新されます。<br /> </td> 
  </tr> 
  <tr> 
   <td> XtkWorkflowTask<br /> </td> 
   <td> 小<br /> </td> 
   <td> 挿入、更新、削除<br /> </td> 
   <td> ワークフローアクティビティを実行するたびに、このテーブルにレコードが作成されます。 パージメカニズムは、有効期限が切れると削除します。<br /> </td> 
  </tr> 
  <tr> 
   <td> XtkWorkflowEvent<br /> </td> 
   <td> 小<br /> </td> 
   <td> 挿入、更新、削除<br /> </td> 
   <td> ワークフロー内のタスク間でアクティブ化される各遷移によって、このテーブルにレコードが作成されます。 パージメカニズムは、有効期限が切れると削除します。 <br /> </td> 
  </tr> 
  <tr> 
   <td> XtkWorkflowJob<br /> </td> 
   <td> 非常に小さい <br /> </td> 
   <td> 挿入、更新、削除<br /> </td> 
   <td> この表は、ワークフローエンジンに固有です。 ワークフローに対するコマンドの送信（開始、停止、一時停止など）を有効にします。 この表は小さいですが、ワークフローにリンクされたトランザクション表の削除時に考慮されます。<br /> </td> 
  </tr> 
  <tr> 
   <td> NmsBroadLog<br /> </td> 
   <td> 最大<br /> </td> 
   <td> 挿入、更新、削除<br /> </td> 
   <td> これはシステム内で最も大きなテーブルです。 送信されたメッセージごとに1件のレコードがあり、これらのレコードが挿入され、配信ステータスを追跡するために更新され、履歴が削除されると削除されます。 <br /> </td> 
  </tr> 
  <tr> 
   <td> NmsTrackingLog<br /> </td> 
   <td> 大<br /> </td> 
   <td> 挿入、削除<br /> </td> 
   <td> 履歴が削除されると、トラッキングログは挿入および削除されますが、更新はされません。 <br /> </td> 
  </tr> 
  <tr> 
   <td> NmsBroadlogMsg <br /> </td> 
   <td> 小<br /> </td> 
   <td> 更新<br /> </td> 
   <td> この表には、SMTPエラーの修正に使用する情報が含まれています。 これはかなり小さいですが、大量に更新されるので、このテーブルのインデックスは急速にフラグメント化される傾向があります。 <br /> </td> 
  </tr> 
  <tr> 
   <td> NmsEmailErrorStat<br /> </td> 
   <td> 実線（中）<br /> </td> 
   <td> 挿入、更新、削除<br /> </td> 
   <td> このテーブルには、SMTPエラーの集計がドメイン順に並べ替えられています。 最初は、古くなった後にクリーンアップタスクによって集計された詳細情報が含まれます。 <br /> </td> 
  </tr> 
  <tr> 
   <td> NmsBroadLogMid（中間ソーシングインスタンス）<br /> </td> 
   <td> 大<br /> </td> 
   <td> 挿入、更新、削除<br /> </td> 
   <td> 5.10（以降）インスタンスが中間ソーシングインスタンスとして使用される場合のみ。 これは、データベース内で最も大きなテーブルの1つです。 送信されたメッセージごとに1件のレコードがあり、これらのレコードが挿入され、配信ステータスを追跡するために更新され、履歴が削除されると削除されます。 ミッドソーシングを使用する場合、履歴を制限することが推奨されます（通常は2か月未満）。この表のサイズは妥当です（3,000万行未満、データ+インデックス）が、時折再構築することが非常に重要です。 <br /> </td> 
  </tr> 
  <tr> 
   <td> NmsBroadLogRcp（NmsRecipientテーブルが使用される場合） <br /> </td> 
   <td> 大<br /> </td> 
   <td> 挿入、更新、削除<br /> </td> 
   <td> これはシステム内で最も大きなテーブルです。 送信されたメッセージごとに1件のレコードがあり、これらのレコードが挿入され、配信ステータスを追跡するために更新され、履歴が削除されると削除されます。 5.10では、SMTPメッセージテキストが5.10バージョンのNmsBroadLogMsgテーブルでファクタリングされるので、このテーブルは4.05(NmsBroadLog)の同等のテーブルより小さくなります。 ただし、このテーブルのインデックスを定期的に（最初は1週間おきに）再作成し、時折（月に1回、またはパフォーマンスに影響が出た場合に）完全に再構築する必要があります。 <br /> </td> 
  </tr> 
  <tr> 
   <td> YyyBroadLogXxx（外部受信者テーブルを使用する場合）<br /> </td> 
   <td> 大<br /> </td> 
   <td> 挿入、更新、削除<br /> </td> 
   <td> NmsBroadLogRcpと同じですが、外部受信者テーブルがあります。 配信マッピングの値を使用して、YyyとXxxを適応させてください。 <br /> </td> 
  </tr> 
  <tr> 
   <td> NmsTrackingLogRcp（NmsRecipientテーブルが使用される場合） <br /> </td> 
   <td> 大<br /> </td> 
   <td> 挿入、削除<br /> </td> 
   <td> 履歴が削除されると、トラッキングログは挿入および削除されますが、更新はされません。 ボリュームは、データ保持期間によって異なります。 <br /> </td> 
  </tr> 
  <tr> 
   <td> YyyTrackingLogXxx（外部受信者テーブルが使用される場合）<br /> </td> 
   <td> 大<br /> </td> 
   <td> 挿入、削除<br /> </td> 
   <td> NmsTrackingLogRcpと同じで、外部受信者テーブルがある。 YyyとXxxは、配信マッピングで使用する値に合わせて調整してください。 <br /> </td> 
  </tr> 
  <tr> 
   <td> NmsBroadLogRtEvent (Message Center execution instance)<br /> </td> 
   <td> 大<br /> </td> 
   <td> 挿入、更新、削除<br /> </td> 
   <td> 他のブロードローグテーブルと同様ですが、NmsRecipientの代わりにNmsRtEventを使用します。<br /> </td> 
  </tr> 
  <tr> 
   <td> NmsTrackingLogRtEvent( Message Center execution instance)<br /> </td> 
   <td> 大<br /> </td> 
   <td> 挿入、削除<br /> </td> 
   <td> 他のtrackingLogテーブルと同様ですが、NmsRecipientの代わりにNmsRtEventテーブルを使用します。<br /> </td> 
  </tr> 
  <tr> 
   <td> NmsRtEvent (Message Center execution instance)<br /> </td> 
   <td> 大<br /> </td> 
   <td> 挿入、更新、削除<br /> </td> 
   <td> Message centerイベントキューを含むテーブル。 これらのイベントのステータスは、処理されるとMessage Centerによって更新されます。 削除は削除中に実行されます。 このテーブルのインデックスを定期的に再作成し、再構築することをお勧めします。<br /> </td> 
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
   <td> 通知の送信に使用されるモバイルデバイス（アドレス）の識別子を含む表（受信者テーブルと同様）。<br /> </td> 
  </tr> 
  <tr> 
   <td> NmsBroadLogAppSubRcp<br /> </td> 
   <td> 大<br /> </td> 
   <td> 挿入、更新、削除<br /> </td> 
   <td> 他のブロードローグテーブルと同様ですが、NmsRecipientの代わりにNmsappSubscriptionRcpを使用します。<br /> </td> 
  </tr> 
  <tr> 
   <td> NmsTrackingLogAppSubRcp<br /> </td> 
   <td> 大<br /> </td> 
   <td> 挿入、削除<br /> </td> 
   <td> 他のtrackingLogテーブルと同様ですが、NmsRecipientの代わりにNmsappSubscriptionRcpテーブルを使用します。<br /> </td> 
  </tr> 
  <tr> 
   <td> XtkSessionInfo<br /> </td> 
   <td> 小<br /> </td> 
   <td> 挿入、削除<br /> </td> 
   <td> ユーザーセッションを含む表。 挿入と削除の数は非常に重要です。<br /> </td> 
  </tr> 
 </tbody> 
</table>

## 顧客テーブル {#customer-tables}

上記のリストに加えて、プラットフォームのセットアップ中に顧客が作成した表（Adobe Campaignデータモデルに存在しない）も、フラグメンテーションの対象となる場合があります。特に、データの読み込みまたは同期の手順中に頻繁に更新される場合があります。 これらのテーブルは、デフォルトのAdobe Campaignデータモデル(例えば、NmsRecipient ****)の一部にすることができます。 この場合、特定のデータベースモデルの監査を実行して、これらのカスタムテーブルを見つけるのは、Adobe Campaignプラットフォームの管理者に任されます。 これらのテーブルは、メンテナンス手順で明示的に説明されているわけではありません。
