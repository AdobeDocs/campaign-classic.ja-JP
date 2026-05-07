---
product: campaign
title: 維持するテーブル
description: 維持するテーブル
feature: Monitoring
badge-v7-prem: label="オンプレミス／ハイブリッドのみ" type="Caution" url="https://experienceleague.adobe.com/docs/campaign-classic/using/installing-campaign-classic/architecture-and-hosting-models/hosting-models-lp/hosting-models.html?lang=ja" tooltip="オンプレミスデプロイメントとハイブリッドデプロイメントにのみ適用されます"
audience: production
content-type: reference
topic-tags: database-maintenance
exl-id: 194f12de-4671-4a56-8cdc-cd5e3dac147b
source-git-commit: 517b85f5d7691acc2522bf4541f07c34c60c7fbf
workflow-type: tm+mt
source-wordcount: '1165'
ht-degree: 3%

---

# 維持するテーブル{#tables-to-maintain}



管理するテーブルのリストは、お使いのAdobe Campaignのバージョン、使用方法、およびデータモデル設定によって異なります。

次のリストには、断片化の対象となるテーブルのみが含まれています。 その結果は以下のとおりである。

* ディスク領域の過剰消費が原因で、データベースアクセスに影響を及ぼします。
* 定期的に更新されていないインデックスは、クエリのパフォーマンスが低下します。

## Adobe Campaign テーブル {#adobe-campaign-tables}

<table> 
 <thead> 
  <tr> 
   <th> <strong> テーブル名</strong><br /> </th> 
   <th> <strong> サイズ </strong><br /> </th> 
   <th> <strong> アクティビティの主なタイプ </strong><br /> </th> 
   <th> <strong>コメント</strong><br /> </th> 
  </tr> 
 </thead> 
 <tbody> 
  <tr> 
   <td> NmsDelivery<br /> </td> 
   <td> 小<br /> </td> 
   <td> 更新<br /> </td> 
   <td> 配信アクションごとに1つのレコードがあります。 配信の進捗状況を反映するために、単一のレコードを何度も更新できるため、このテーブルのインデックスは迅速にフラグメント化される傾向があります。<br /> </td> 
  </tr> 
  <tr> 
   <td> NmsDeliveryPart<br /> </td> 
   <td> Medium<br /> </td> 
   <td> 挿入、更新、削除<br /> </td> 
   <td> 配信の準備中にレコードが挿入される作業テーブル。 その後、配信中に更新され、配信が完了したら最終的に削除されます。<br /> このテーブルは、平均サイズがかなり制限されているにもかかわらず、急速にフラグメント化される傾向があります。<br /> </td> 
  </tr> 
  <tr> 
   <td> NmsMirrorPageInfo<br /> </td> 
   <td> 大<br /> </td> 
   <td> 挿入、削除<br /> </td> 
   <td> この表には、パーソナライズされたミラーページの生成に必要な情報が含まれています。 メモ（CLOB）フィールドが含まれているため、サイズが非常に大きくなる傾向があります。 ボリュームは、保持されるミラーページの履歴に直接比例します。<br /> </td> 
  </tr> 
  <tr> 
   <td> NmsDeliveryStat<br /> </td> 
   <td> Medium<br /> </td> 
   <td> 挿入、更新、削除<br /> </td> 
   <td> このテーブルには、配信プロセスに関する統計が含まれています。 その記録は定期的に更新されます。<br /> </td> 
  </tr> 
  <tr> 
   <td> NmsAddress<br /> </td> 
   <td> Medium<br /> </td> 
   <td> 更新、挿入<br /> </td> 
   <td> この表には、電子メールアドレスに関する情報が含まれています。 検疫プロセスの一部として頻繁に更新されます（レコードは、最初の配信エラーで作成され、カウンターが変更されたときに更新され、配信が成功すると削除されます）。<br /> </td> 
  </tr> 
  <tr> 
   <td> XtkWorkflow<br /> </td> 
   <td> 小<br /> </td> 
   <td> 更新<br /> </td> 
   <td> ワークフローインスタンスごとに1つのレコードがあるので、レコードは非常に少なくなります。 ただし、状態と進行状況を反映するようにテーブルが定期的に更新されます。<br /> </td> 
  </tr> 
  <tr> 
   <td> XtkWorkflowTask<br /> </td> 
   <td> 小<br /> </td> 
   <td> 挿入、更新、削除<br /> </td> 
   <td> ワークフローアクティビティを実行するたびに、このテーブル内のレコードが作成されます。 パージ メカニズムは、有効期限が切れると、削除します。<br /> </td> 
  </tr> 
  <tr> 
   <td> XtkWorkflowEvent<br /> </td> 
   <td> 小<br /> </td> 
   <td> 挿入、更新、削除<br /> </td> 
   <td> ワークフロー内のタスク間でアクティブ化された各遷移は、このテーブルのレコードの作成につながります。 パージ機能は、有効期限が切れると削除します。<br /> </td> 
  </tr> 
  <tr> 
   <td> XtkWorkflowJob<br /> </td> 
   <td> 非常に小さい<br /> </td> 
   <td> 挿入、更新、削除<br /> </td> 
   <td> この表は、ワークフローエンジンに固有です。 ワークフローへのコマンドの送信（開始、停止、一時停止など）が有効になります。 このテーブルは小さいですが、ワークフローにリンクされたトランザクションテーブルのパージ中に、このテーブルが考慮されます。<br /> </td> 
  </tr> 
  <tr> 
   <td> NmsBroadLog<br /> </td> 
   <td> Largest<br /> </td> 
   <td> 挿入、更新、削除<br /> </td> 
   <td> これはシステムで最大のテーブルです。 送信されるメッセージごとに1つのレコードがあり、これらのレコードは挿入され、配信ステータスを追跡するために更新され、履歴が消去されたときに削除されます。<br /> </td> 
  </tr> 
  <tr> 
   <td> NmsTrackingLog<br /> </td> 
   <td> 大<br /> </td> 
   <td> 挿入、削除<br /> </td> 
   <td> トラッキングログは、履歴が消去されたときに挿入および削除されますが、更新されません。<br /> </td> 
  </tr> 
  <tr> 
   <td> NmsBroadlogMsg <br /> </td> 
   <td> 小<br /> </td> 
   <td> 更新<br /> </td> 
   <td> この表には、SMTP エラーの選定に使用される情報が含まれています。 このテーブルのインデックスは非常に小さいですが、大幅に更新されるので、このテーブルのインデックスは急速にフラグメント化される傾向があります。<br /> </td> 
  </tr> 
  <tr> 
   <td> NmsEmailErrorStat<br /> </td> 
   <td> Medium<br /> </td> 
   <td> 挿入、更新、削除<br /> </td> 
   <td> このテーブルには、ドメイン別に並べ替えられたSMTP エラーの集計が含まれています。 最初は、クリーンアップタスクが古くなると、クリーンアップタスクによって集計される詳細な情報が含まれます。<br /> </td> 
  </tr> 
  <tr> 
   <td> NmsBroadLogMid （ミッドソーシングインスタンス上） <br /> </td> 
   <td> 大<br /> </td> 
   <td> 挿入、更新、削除<br /> </td> 
   <td> 5.10 （またはそれ以降）のインスタンスがミッドソーシングインスタンスとして使用されている場合のみ。 これはデータベースで最大のテーブルの1つです。 送信されるメッセージごとに1つのレコードがあり、これらのレコードは挿入され、配信ステータスを追跡するために更新され、履歴が消去されたときに削除されます。 ミッドソーシングを使用する場合、履歴を制限することをお勧めします（通常は2か月未満）。そのため、この表はサイズで合理的なままです（6000万行、data+indexの場合は30 Go未満）。ただし、時間をかけて再構築することが非常に重要です。<br /> </td> 
  </tr> 
  <tr> 
   <td> NmsBroadLogRcp （NmsRecipient テーブルが使用されている場合） <br /> </td> 
   <td> 大<br /> </td> 
   <td> 挿入、更新、削除<br /> </td> 
   <td> これはシステムで最大のテーブルです。 送信されるメッセージごとに1つのレコードがあり、これらのレコードは挿入され、配信ステータスを追跡するために更新され、履歴が消去されたときに削除されます。 5.10では、SMTP メッセージ テキストは5.10 バージョンのNmsBroadLogMsg テーブルで因数分解されるので、このテーブルは4.05 （NmsBroadLog）の同等のテーブルよりも小さくなることに注意してください。 ただし、このテーブルのインデックスを定期的に（開始する週ごとに）再び作成し、時間ごとに（月に1回、またはパフォーマンスに影響を与える場合）完全に再構築することは依然として不可欠です。<br /> </td> 
  </tr> 
  <tr> 
   <td> YyyBroadLogXxx （外部受信者テーブルを使用する場合） <br /> </td> 
   <td> 大<br /> </td> 
   <td> 挿入、更新、削除<br /> </td> 
   <td> NmsBroadLogRcpと同じですが、外部の受信者テーブルがあります。 YyyとXxxを配信マッピングの値に合わせてください。<br /> </td> 
  </tr> 
  <tr> 
   <td> NmsTrackingLogRcp （NmsRecipient テーブルが使用されている場合） <br /> </td> 
   <td> 大<br /> </td> 
   <td> 挿入、削除<br /> </td> 
   <td> トラッキングログは、履歴が消去されたときに挿入および削除されますが、更新されません。 ボリュームは、データ保持の長さによって異なります。<br /> </td> 
  </tr> 
  <tr> 
   <td> YyyTrackingLogXxx （外部受信者テーブルが使用されている場合） <br /> </td> 
   <td> 大<br /> </td> 
   <td> 挿入、削除<br /> </td> 
   <td> NmsTrackingLogRcpと同じですが、外部の受信者テーブルがあります。 YyyとXxxは、配信マッピングで使用する値に合わせてください。<br /> </td> 
  </tr> 
  <tr> 
   <td> NmsBroadLogRtEvent （Message Center実行インスタンス） <br /> </td> 
   <td> 大<br /> </td> 
   <td> 挿入、更新、削除<br /> </td> 
   <td> 他のブロードログテーブルと同様ですが、NmsRecipientの代わりにNmsRtEventを使用します。<br /> </td> 
  </tr> 
  <tr> 
   <td> NmsTrackingLogRtEvent （Message Center実行インスタンス） <br /> </td> 
   <td> 大<br /> </td> 
   <td> 挿入、削除<br /> </td> 
   <td> 他のtrackingLog テーブルと同様ですが、NmsRecipientの代わりにNmsRtEvent テーブルを使用します。<br /> </td> 
  </tr> 
  <tr> 
   <td> NmsRtEvent （Message Center実行インスタンス） <br /> </td> 
   <td> 大<br /> </td> 
   <td> 挿入、更新、削除<br /> </td> 
   <td> メッセージセンターイベントキューを含むテーブル。 これらのイベントのステータスは、処理中にMessage Centerによって更新されます。 削除はパージ中に実行されます。 このテーブルのインデックスを定期的に再作成し、再構築することをお勧めします。<br /> </td> 
  </tr> 
  <tr> 
   <td> NmsEventHisto （Message Center コントロール インスタンス） <br /> </td> 
   <td> 大<br /> </td> 
   <td> 挿入、更新、削除<br /> </td> 
   <td> NmsRtEventと同様です。 このテーブルは、すべての実行インスタンスのすべてのイベントをアーカイブします。 リアルタイム プロセスではなく、レポートでのみ使用されます。<br /> </td> 
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
   <td> 通知の送信に使用されるモバイル デバイス （アドレス）の識別子を含むテーブル （受信者テーブルと同様）。<br /> </td> 
  </tr> 
  <tr> 
   <td> NmsBroadLogAppSubRcp<br /> </td> 
   <td> 大<br /> </td> 
   <td> 挿入、更新、削除<br /> </td> 
   <td> 他のブロードログテーブルと同様ですが、NmsRecipientの代わりにNmsappSubscriptionRcpを使用します。<br /> </td> 
  </tr> 
  <tr> 
   <td> NmsTrackingLogAppSubRcp<br /> </td> 
   <td> 大<br /> </td> 
   <td> 挿入、削除<br /> </td> 
   <td> 他のtrackingLog テーブルと同様ですが、NmsRecipientの代わりにNmsappSubscriptionRcp テーブルを使用します。<br /> </td> 
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

上記のリストに加えて、プラットフォームのセットアップ中に（Adobe Campaign データモデルに存在しない）お客様が作成したテーブルも、特にデータの読み込み中または同期中に頻繁に更新される場合、断片化の対象になる可能性があります。 これらのテーブルは、デフォルトのAdobe Campaign データモデル（**NmsRecipient**&#x200B;など）の一部にできます。 この場合、これらのカスタムテーブルを見つけるには、特定のデータベースモデルの監査を実施するのは、Adobe Campaign プラットフォームの管理者の役割です。 これらの表は、必ずしもメンテナンス手順で明示的に言及されているわけではありません。
