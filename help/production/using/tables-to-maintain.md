---
product: campaign
title: 維持するテーブル
description: 維持するテーブル
feature: Monitoring
badge-v7-only: label="v7" type="Informative" tooltip="Campaign Classicv7 にのみ適用"
badge-v7-prem: label="オンプレミスおよびハイブリッド" type="Caution" url="https://experienceleague.adobe.com/docs/campaign-classic/using/installing-campaign-classic/architecture-and-hosting-models/hosting-models-lp/hosting-models.html?lang=ja" tooltip="オンプレミスデプロイメントとハイブリッドデプロイメントにのみ適用されます"
audience: production
content-type: reference
topic-tags: database-maintenance
exl-id: 194f12de-4671-4a56-8cdc-cd5e3dac147b
source-git-commit: 3a9b21d626b60754789c3f594ba798309f62a553
workflow-type: tm+mt
source-wordcount: '1148'
ht-degree: 4%

---

# 維持するテーブル{#tables-to-maintain}



保持するテーブルのリストは、Adobe Campaignのバージョン、使用方法、データモデル設定によって異なります。

次のリストには、フラグメンテーションの対象となるテーブルのみが表示されます。 影響は次のとおりです。

* ディスク容量の過剰消費により、データベース・アクセスに影響を及ぼします。
* インデックスが定期的に更新されておらず、クエリのパフォーマンスが低下します。

## Adobe Campaignテーブル {#adobe-campaign-tables}

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
   <td> 配信アクションごとに 1 つのレコードがあります。 1 つのレコードは配信の進行状況を反映するために複数回更新される可能性があるので、このテーブルのインデックスは急速にフラグメント化する傾向があります。 <br /> </td> 
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
   <td> この表には、パーソナライズされたミラーページの生成に必要な情報が含まれています。 メモ (CLOB) フィールドが含まれているので、非常に大きくなる傾向があります。 ボリュームは、保持されるミラーページの履歴に正比例します。 <br /> </td> 
  </tr> 
  <tr> 
   <td> NmsDeliveryStat<br /> </td> 
   <td> 中<br /> </td> 
   <td> 挿入、更新、削除<br /> </td> 
   <td> このテーブルには、配信プロセスに関する統計が含まれています。 そのレコードは定期的に更新されます。 <br /> </td> 
  </tr> 
  <tr> 
   <td> NmsAddress<br /> </td> 
   <td> 中<br /> </td> 
   <td> 更新、挿入<br /> </td> 
   <td> このテーブルには、E メールアドレスに関する情報が含まれます。 この値は、強制隔離プロセスの一環として頻繁に更新されます（最初の配信エラーでレコードが作成され、カウンターが変更されると更新され、配信に成功すると削除されます）。 <br /> </td> 
  </tr> 
  <tr> 
   <td> XtkWorkflow<br /> </td> 
   <td> 小<br /> </td> 
   <td> アップデート<br /> </td> 
   <td> ワークフローインスタンスごとに 1 つのレコードが存在するので、レコードはほとんどありません。 ただし、テーブルは定期的に更新され、ステータスと進行状況が反映されます。<br /> </td> 
  </tr> 
  <tr> 
   <td> XtkWorkflowTask<br /> </td> 
   <td> 小<br /> </td> 
   <td> 挿入、更新、削除<br /> </td> 
   <td> ワークフローアクティビティを実行するたびに、このテーブルにレコードが作成されます。 パージメカニズムは、有効期限が切れた後に削除します。<br /> </td> 
  </tr> 
  <tr> 
   <td> XtkWorkflowEvent<br /> </td> 
   <td> 小<br /> </td> 
   <td> 挿入、更新、削除<br /> </td> 
   <td> ワークフローのタスク間で有効化された各トランジションは、このテーブルにレコードを作成します。 パージメカニズムは、有効期限が切れた後に削除します。 <br /> </td> 
  </tr> 
  <tr> 
   <td> XtkWorkflowJob<br /> </td> 
   <td> 非常に小さい <br /> </td> 
   <td> 挿入、更新、削除<br /> </td> 
   <td> このテーブルは、ワークフローエンジンに固有です。 ワークフローへのコマンドの送信（例えば、開始、停止、一時停止）を有効にします。 このテーブルは小さいものの、ワークフローにリンクされたトランザクションテーブルのパージ時に考慮されます。<br /> </td> 
  </tr> 
  <tr> 
   <td> NmsBroadLog<br /> </td> 
   <td> 最大<br /> </td> 
   <td> 挿入、更新、削除<br /> </td> 
   <td> これはシステム内で最も大きなテーブルです。 送信されたメッセージごとに 1 つのレコードがあり、これらのレコードが挿入され、配信ステータスを追跡するために更新され、履歴がパージされると削除されます。 <br /> </td> 
  </tr> 
  <tr> 
   <td> NmsTrackingLog<br /> </td> 
   <td> 大<br /> </td> 
   <td> 挿入、削除<br /> </td> 
   <td> トラッキングログは、履歴がパージされると挿入および削除されますが、更新はされません。 <br /> </td> 
  </tr> 
  <tr> 
   <td> NmsBroadlogMsg <br /> </td> 
   <td> 小<br /> </td> 
   <td> アップデート<br /> </td> 
   <td> このテーブルには、SMTP エラーの検証に使用する情報が含まれています。 この値はかなり小さいですが、大規模に更新されるので、このテーブルのインデックスは急速に断片化する傾向があります。 <br /> </td> 
  </tr> 
  <tr> 
   <td> NmsEmailErrorStat<br /> </td> 
   <td> 中<br /> </td> 
   <td> 挿入、更新、削除<br /> </td> 
   <td> このテーブルには、SMTP エラーに関する集計がドメイン別に並べ替えられています。 最初に、クリーンアップタスクが期限切れになった後にクリーンアップタスクによって集計される詳細情報が含まれます。 <br /> </td> 
  </tr> 
  <tr> 
   <td> NmsBroadLogMid （ミッドソーシングインスタンス上）<br /> </td> 
   <td> 大<br /> </td> 
   <td> 挿入、更新、削除<br /> </td> 
   <td> 5.10 以降のインスタンスがミッドソーシングインスタンスとして使用されている場合にのみ有効です。 これは、データベース内で最も大きいテーブルの 1 つです。 送信されたメッセージごとに 1 つのレコードがあり、これらのレコードが挿入され、配信ステータスを追跡するために更新され、履歴がパージされると削除されます。 ミッドソーシングを使用する場合は、履歴（通常は 2 ヶ月未満）を制限することをお勧めします。このテーブルは、サイズ（6,000 万行、データ+インデックスの場合は 30 Go 未満）が妥当ですが、時々再構築することが非常に重要です。 <br /> </td> 
  </tr> 
  <tr> 
   <td> NmsBroadLogRcp （NmsRecipient テーブルを使用する場合） <br /> </td> 
   <td> 大<br /> </td> 
   <td> 挿入、更新、削除<br /> </td> 
   <td> これはシステム内で最も大きなテーブルです。 送信されたメッセージごとに 1 つのレコードがあり、これらのレコードが挿入され、配信ステータスを追跡するために更新され、履歴がパージされると削除されます。 5.10 では、SMTP メッセージテキストが 5.10 バージョンの NmsBroadLogMsg テーブルに組み込まれているので、このテーブルは 4.05(NmsBroadLog) での同等のテーブルよりも小さいことに注意してください。 ただし、このテーブルのインデックスを定期的に再作成し（最初は 1 週間おき）、時々（月に 1 回、またはパフォーマンスに影響が出た場合）、完全に再構築する必要があります。 <br /> </td> 
  </tr> 
  <tr> 
   <td> YyyBroadLogXxx（外部の受信者テーブルを使用する場合）<br /> </td> 
   <td> 大<br /> </td> 
   <td> 挿入、更新、削除<br /> </td> 
   <td> NmsBroadLogRcp と同じですが、外部の受信者テーブルがあります。 配信マッピングの値を使用して、Yyy および Xxx を調整してください。 <br /> </td> 
  </tr> 
  <tr> 
   <td> NmsTrackingLogRcp （NmsRecipient テーブルを使用する場合） <br /> </td> 
   <td> 大<br /> </td> 
   <td> 挿入、削除<br /> </td> 
   <td> トラッキングログは、履歴がパージされると挿入および削除されますが、更新はされません。 ボリュームは、データ保持の長さに応じて異なります。 <br /> </td> 
  </tr> 
  <tr> 
   <td> YyyTrackingLogXxx（外部の受信者テーブルを使用する場合）<br /> </td> 
   <td> 大<br /> </td> 
   <td> 挿入、削除<br /> </td> 
   <td> NmsTrackingLogRcp と同じですが、外部の受信者テーブルがあります。 配信マッピングで使用する値を使用して、 Yyy および Xxx を調整してください。 <br /> </td> 
  </tr> 
  <tr> 
   <td> NmsBroadLogRtEvent （Message Center 実行インスタンス）<br /> </td> 
   <td> 大<br /> </td> 
   <td> 挿入、更新、削除<br /> </td> 
   <td> 他の broadLog テーブルと同様ですが、NmsRecipient の代わりに NmsRtEvent を使用します。<br /> </td> 
  </tr> 
  <tr> 
   <td> NmsTrackingLogRtEvent（ Message Center 実行インスタンス）<br /> </td> 
   <td> 大<br /> </td> 
   <td> 挿入、削除<br /> </td> 
   <td> 他の trackingLog テーブルと同様ですが、NmsRecipient ではなく NmsRtEvent テーブルを使用します。<br /> </td> 
  </tr> 
  <tr> 
   <td> NmsRtEvent（Message Center 実行インスタンス）<br /> </td> 
   <td> 大<br /> </td> 
   <td> 挿入、更新、削除<br /> </td> 
   <td> Message Center のイベントキューを含む表。 これらのイベントのステータスは、処理時に Message Center によって更新されます。 削除はパージ中に実行されます。 このテーブルのインデックスを定期的に再作成し、再構築することをお勧めします。<br /> </td> 
  </tr> 
  <tr> 
   <td> NmsEventHisto（Message Center コントロールインスタンス）<br /> </td> 
   <td> 大<br /> </td> 
   <td> 挿入、更新、削除<br /> </td> 
   <td> NmsRtEvent と同様です。 この表は、すべての実行インスタンスからすべてのイベントをアーカイブします。 リアルタイムプロセスではなく、レポートでのみ使用されます。<br /> </td> 
  </tr> 
  <tr> 
   <td> NmsMobileApp<br /> </td> 
   <td> 非常に小さい<br /> </td> 
   <td> 挿入、更新、削除<br /> </td> 
   <td> モバイルアプリケーションとその設定を含むテーブル。<br /> </td> 
  </tr> 
  <tr> 
   <td> NmsAppSubscriptionRcp<br /> </td> 
   <td> 大<br /> </td> 
   <td> 挿入、更新<br /> </td> 
   <td> （受信者テーブルと同様に）通知の送信に使用されるモバイルデバイス（アドレス）の識別子を含むテーブル。<br /> </td> 
  </tr> 
  <tr> 
   <td> NmsBroadLogAppSubRcp<br /> </td> 
   <td> 大<br /> </td> 
   <td> 挿入、更新、削除<br /> </td> 
   <td> 他の broadLog テーブルと同様ですが、NmsRecipient ではなく NmsappSubscriptionRcp を使用します。<br /> </td> 
  </tr> 
  <tr> 
   <td> NmsTrackingLogAppSubRcp<br /> </td> 
   <td> 大<br /> </td> 
   <td> 挿入、削除<br /> </td> 
   <td> 他の trackingLog テーブルと同様ですが、NmsRecipient ではなく NmsappSubscriptionRcp テーブルが使用されます。<br /> </td> 
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

上記のリストに加えて、(Adobe Campaignのデータモデルに存在しない ) プラットフォーム設定時に顧客が作成したテーブルも、フラグメント化の対象となる場合があります。特に、データの読み込み中や同期手順中に頻繁に更新される場合です。 これらのテーブルは、デフォルトのAdobe Campaignデータモデルの一部にすることができます ( 例： **NmsRecipient**) をクリックします。 この場合、Adobe Campaignプラットフォームの管理者が、特定のデータベースモデルの監査を実行して、これらのカスタムテーブルを見つけるかどうかは、管理者次第です。 これらのテーブルは、必ずしもメンテナンス手順で明示的に言及されるわけではありません。
