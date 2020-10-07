---
title: 維持するテーブル
seo-title: 維持するテーブル
description: 維持するテーブル
seo-description: null
page-status-flag: never-activated
uuid: 1085e929-65cc-48fa-9c31-0508a14b4704
contentOwner: sauviat
products: SG_CAMPAIGN/CLASSIC
audience: production
content-type: reference
topic-tags: database-maintenance
discoiquuid: 6ec4e566-7116-4d7f-835d-cb0f3c3a6a7a
translation-type: tm+mt
source-git-commit: 70b143445b2e77128b9404e35d96b39694d55335
workflow-type: tm+mt
source-wordcount: '1126'
ht-degree: 3%

---


# 維持するテーブル{#tables-to-maintain}

維持するテーブルのリストは、Adobe Campaignのバージョン、使用方法、データモデル設定によって異なります。

次のリストには、フラグメントの対象となるテーブルのみが含まれています。 影響は次のとおりです。

* ディスク領域の過剰消費、データベース・アクセスに影響
* 定期的に更新されていないインデックスの場合、クエリのパフォーマンスが低下します。

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
   <td> 小<br /> </td> 
   <td> アップデート<br /> </td> 
   <td> 配信の操作ごとに1つのレコードがあります。 1つのレコードは配信の進行状況を反映するために複数回更新できるので、このテーブルのインデックスは急速にフラグメント化する傾向があります。 <br /> </td> 
  </tr> 
  <tr> 
   <td> NmsDeliveryPart<br /> </td> 
   <td> 実線（中）<br /> </td> 
   <td> 挿入、更新、削除<br /> </td> 
   <td> 配信の準備中に挿入されるレコードの作業テーブル。 その後、配信中に更新され、配信が完了すると、最後に削除されます。<br /> このテーブルは、平均サイズがかなり制限されているにもかかわらず、速くフラグメント化される傾向があります。<br /> </td> 
  </tr> 
  <tr> 
   <td> NmsMirrorPageInfo<br /> </td> 
   <td> 大<br /> </td> 
   <td> 挿入、削除<br /> </td> 
   <td> 次の表に、パーソナライズされたミラーページを生成するために必要な情報を示します。 メモ型(CLOB)フィールドが含まれているので、非常に大きくなりがちです。 ボリュームは、保存されるミラーページの履歴に正比例します。 <br /> </td> 
  </tr> 
  <tr> 
   <td> NmsDeliveryStat<br /> </td> 
   <td> 実線（中）<br /> </td> 
   <td> 挿入、更新、削除<br /> </td> 
   <td> 次の表に、配信プロセスの統計を示します。 レコードは定期的に更新されます。 <br /> </td> 
  </tr> 
  <tr> 
   <td> NmsAddress<br /> </td> 
   <td> 実線（中）<br /> </td> 
   <td> 更新、挿入<br /> </td> 
   <td> 次の表に、電子メールアドレスに関する情報を示します。 このレポートは、強制隔離処理の一環として頻繁に更新されます(最初の配信エラー時にレコードが作成され、カウンターが変更され、配信が成功すると削除されます)。 <br /> </td> 
  </tr> 
  <tr> 
   <td> XtkWorkflow<br /> </td> 
   <td> 小<br /> </td> 
   <td> アップデート<br /> </td> 
   <td> ワークフローインスタンスごとに1つのレコードがあるので、レコードはほとんどありません。 ただし、ステータスと進行状況を反映して、テーブルは定期的に更新されます。<br /> </td> 
  </tr> 
  <tr> 
   <td> XtkWorkflowTask<br /> </td> 
   <td> 小<br /> </td> 
   <td> 挿入、更新、削除<br /> </td> 
   <td> ワークフローアクティビティを実行するたびに、このテーブルにレコードが作成されます。 削除メカニズムは、有効期限が切れると削除します。<br /> </td> 
  </tr> 
  <tr> 
   <td> XtkWorkflowEvent<br /> </td> 
   <td> 小<br /> </td> 
   <td> 挿入、更新、削除<br /> </td> 
   <td> ワークフロー内のタスク間でアクティブ化された各トランジションは、このテーブル内にレコードを作成することになります。 削除メカニズムは、有効期限が切れると削除します。 <br /> </td> 
  </tr> 
  <tr> 
   <td> XtkWorkflowJob<br /> </td> 
   <td> 非常に小さい <br /> </td> 
   <td> 挿入、更新、削除<br /> </td> 
   <td> この表はワークフローエンジンに固有です。 ワークフロー(開始、停止、一時停止など)に対するコマンドの送信を有効にします。 この表は小さいですが、ワークフローにリンクされたトランザクション表の削除時に、この表が考慮されます。<br /> </td> 
  </tr> 
  <tr> 
   <td> NmsBroadLog<br /> </td> 
   <td> 最大<br /> </td> 
   <td> 挿入、更新、削除<br /> </td> 
   <td> これはシステム内で最も大きなテーブルです。 送信されたメッセージごとに1つのレコードがあり、これらのレコードが挿入され、配信のステータスを追跡するために更新され、履歴が削除されると削除されます。 <br /> </td> 
  </tr> 
  <tr> 
   <td> NmsTrackingLog<br /> </td> 
   <td> 大<br /> </td> 
   <td> 挿入、削除<br /> </td> 
   <td> トラッキングログは、履歴が削除されると挿入および削除されますが、更新はされません。 <br /> </td> 
  </tr> 
  <tr> 
   <td> NmsBroadlogMsg <br /> </td> 
   <td> 小<br /> </td> 
   <td> アップデート<br /> </td> 
   <td> このテーブルには、SMTPエラーの適用に使用される情報が含まれています。 この値は非常に小さいですが、大幅に更新されるので、この表のインデックスは急速にフラグメント化しがちです。 <br /> </td> 
  </tr> 
  <tr> 
   <td> NmsEmailErrorStat<br /> </td> 
   <td> 実線（中）<br /> </td> 
   <td> 挿入、更新、削除<br /> </td> 
   <td> 次の表に、SMTPエラーの集計をドメイン順に並べ替えます。 最初は、古くなった後にクリーンアップタスクによって集計された詳細情報が含まれます。 <br /> </td> 
  </tr> 
  <tr> 
   <td> NmsBroadLogMid(ミッドソーシングインスタンス)<br /> </td> 
   <td> 大<br /> </td> 
   <td> 挿入、更新、削除<br /> </td> 
   <td> 5.10（以降）インスタンスがミッドソーシングインスタンスとして使用される場合のみ。 これは、データベース内で最も大きいテーブルの1つです。 送信されたメッセージごとに1つのレコードがあり、これらのレコードが挿入され、配信のステータスを追跡するために更新され、履歴が削除されると削除されます。 ミッドソーシングを使用する場合、履歴を制限することを推奨します（通常は2か月未満）。したがって、この表は妥当なサイズ（6,000万行、data+indexについて30Go未満）ですが、時折再構築することが非常に重要です。 <br /> </td> 
  </tr> 
  <tr> 
   <td> NmsBroadLogRcp（NmsRecipientテーブルを使用する場合） <br /> </td> 
   <td> 大<br /> </td> 
   <td> 挿入、更新、削除<br /> </td> 
   <td> これはシステム内で最も大きなテーブルです。 送信されたメッセージごとに1つのレコードがあり、これらのレコードが挿入され、配信のステータスを追跡するために更新され、履歴が削除されると削除されます。 5.10では、SMTPメッセージテキストが5.10バージョンのNmsBroadLogMsgテーブルに含まれているので、このテーブルは4.05 (NmsBroadLog)での等価な値より小さくなっています。 ただし、定期的に(開始を行うために1週間おきに)このテーブルのインデックスを再作成し、時々（月に1回、またはパフォーマンスに影響が出た場合に）完全に再構築する必要があります。 <br /> </td> 
  </tr> 
  <tr> 
   <td> YyyBroadLogXxx(外部受信者テーブルを使用する場合)<br /> </td> 
   <td> 大<br /> </td> 
   <td> 挿入、更新、削除<br /> </td> 
   <td> NmsBroadLogRcpと同じですが、外部受信者テーブルがあります。 YyyとXxxは、配信マッピングの値に合わせて調整してください。 <br /> </td> 
  </tr> 
  <tr> 
   <td> NmsTrackingLogRcp（NmsRecipientテーブルが使用される場合） <br /> </td> 
   <td> 大<br /> </td> 
   <td> 挿入、削除<br /> </td> 
   <td> トラッキングログは、履歴が削除されると挿入および削除されますが、更新はされません。 ボリュームは、データの保存期間に応じて異なります。 <br /> </td> 
  </tr> 
  <tr> 
   <td> YyyTrackingLogXxx(外部受信者テーブルを使用する場合)<br /> </td> 
   <td> 大<br /> </td> 
   <td> 挿入、削除<br /> </td> 
   <td> NmsTrackingLogRcpと同じですが、外部受信者テーブルがあります。 YyyとXxxは、配信マッピングで使用する値に合わせて調整してください。 <br /> </td> 
  </tr> 
  <tr> 
   <td> NmsBroadLogRtEvent (Message Center execution instance)<br /> </td> 
   <td> 大<br /> </td> 
   <td> 挿入、更新、削除<br /> </td> 
   <td> 他のブロードローグテーブルと同様ですが、NmsRecipientではなくNmsRtEventを使用します。<br /> </td> 
  </tr> 
  <tr> 
   <td> NmsTrackingLogRtEvent( Message Center execution instance)<br /> </td> 
   <td> 大<br /> </td> 
   <td> 挿入、削除<br /> </td> 
   <td> 他のtrackingLogテーブルと同様ですが、NmsRecipientテーブルではなくNmsRtEventテーブルを使用します。<br /> </td> 
  </tr> 
  <tr> 
   <td> NmsRtEvent (Message Center execution instance)<br /> </td> 
   <td> 大<br /> </td> 
   <td> 挿入、更新、削除<br /> </td> 
   <td> Message Centerイベントキューを含む表。 これらのイベントのステータスは、処理されるとMessage Centerによって更新されます。 削除は、削除中に実行されます。 このテーブルのインデックスを定期的に再作成し、再構築することをお勧めします。<br /> </td> 
  </tr> 
  <tr> 
   <td> NmsEventHisto(Message Centerのコントロールインスタンス)<br /> </td> 
   <td> 大<br /> </td> 
   <td> 挿入、更新、削除<br /> </td> 
   <td> NmsRtEventと同様です。 この表は、すべての実行インスタンスのすべてのイベントをアーカイブします。 リアルタイムプロセスなしで、レポートでのみ使用されます。<br /> </td> 
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
   <td> 通知の送信に使用されるモバイルデバイス（アドレス）の識別子を含む表(受信者表と同様)。<br /> </td> 
  </tr> 
  <tr> 
   <td> NmsBroadLogAppSubRcp<br /> </td> 
   <td> 大<br /> </td> 
   <td> 挿入、更新、削除<br /> </td> 
   <td> 他のブロードローグテーブルと同様ですが、NmsRecipientではなくNmsappSubscriptionRcpを使用します。<br /> </td> 
  </tr> 
  <tr> 
   <td> NmsTrackingLogAppSubRcp<br /> </td> 
   <td> 大<br /> </td> 
   <td> 挿入、削除<br /> </td> 
   <td> 他のtrackingLogテーブルと同様ですが、NmsRecipientテーブルではなく、NmsappSubscriptionRcpテーブルを使用します。<br /> </td> 
  </tr> 
  <tr> 
   <td> XtkSessionInfo<br /> </td> 
   <td> 小<br /> </td> 
   <td> 挿入、削除<br /> </td> 
   <td> ユーザーセッションを含むテーブル。 挿入と削除の数は非常に重要です。<br /> </td> 
  </tr> 
 </tbody> 
</table>

## 顧客テーブル {#customer-tables}

上記のリストに加えて、プラットフォームの設定時にお客様が作成した(Adobe Campaignデータモデルに存在しない)テーブルも、フラグメントの対象となります。特に、データの読み込みや同期の手順時に頻繁に更新される場合があります。 これらのテーブルは、デフォルトのAdobe Campaignデータモデル( **NmsRecipientなど**)の一部にすることができます。 この場合、特定のAdobe Campaignモデルの監査を実行して、これらのカスタム表を見つけるのは、データベースプラットフォームの管理者次第です。 これらのテーブルは、メンテナンス手順で明示的に説明されているわけではありません。
