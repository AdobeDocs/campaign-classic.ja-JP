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
source-git-commit: 14ba450ebff9bba6a36c0df07d715b7279604222
workflow-type: tm+mt
source-wordcount: '1140'
ht-degree: 1%

---

# 維持するテーブル{#tables-to-maintain}



管理するテーブルのリストは、Adobe Campaignのバージョン、使用方法およびデータモデル設定によって異なります。

次のリストは、断片化の影響が最も大きいテーブルのみを示しています。 影響は次のとおりです。

* ディスク領域の過剰消費。データベースへのアクセスに影響する。
* 定期的に更新されていないインデックス。クエリパフォーマンスが低下します。

## Adobe Campaign テーブル {#adobe-campaign-tables}

<table> 
 <thead> 
  <tr> 
   <th> <strong> テーブル名 </strong><br /> </th> 
   <th> <strong> サイズ </strong><br /> </th> 
   <th> <strong> アクティビティの主なタイプ </strong><br /> </th> 
   <th> <strong> コメント </strong><br /> </th> 
  </tr> 
 </thead> 
 <tbody> 
  <tr> 
   <td> NmsDelivery <br /> </td> 
   <td> 小 <br /> </td> 
   <td> 更新 <br /> </td> 
   <td> 配信アクションごとに 1 つのレコードがあります。 単一のレコードを複数回更新して配信の進行状況を反映させることができるので、このテーブルのインデックスは迅速にフラグメント化される傾向があります。<br /> </td> 
  </tr> 
  <tr> 
   <td> NmsDeliveryPart<br /> </td> 
   <td> Medium<br /> </td> 
   <td> 挿入、更新、削除 <br /> </td> 
   <td> 配信の準備中に挿入されるレコードのワークテーブル。 その後、配信中に更新され、配信が完了すると最後に削除されます。<br /> このテーブルは、平均サイズがかなり限られていても、急速にフラグメント化される傾向があります。<br /> </td> 
  </tr> 
  <tr> 
   <td> NmsMirrorPageInfo <br /> </td> 
   <td> 大 <br /> </td> 
   <td> 挿入、削除 <br /> </td> 
   <td> この表には、パーソナライズされたミラーページを生成するために必要な情報が含まれています。 メモ （CLOB） フィールドが含まれているため、サイズが非常に大きくなる傾向があります。 ボリュームは、保持されるミラーページの履歴に正比例します。<br /> </td> 
  </tr> 
  <tr> 
   <td> NmsDeliveryStat<br /> </td> 
   <td> Medium<br /> </td> 
   <td> 挿入、更新、削除 <br /> </td> 
   <td> このテーブルには、配信プロセスに関する統計が含まれています。 そのレコードは定期的に更新されます。<br /> </td> 
  </tr> 
  <tr> 
   <td> NmsAddress<br /> </td> 
   <td> Medium<br /> </td> 
   <td> 更新、挿入 <br /> </td> 
   <td> このテーブルには、メールアドレスに関する情報が含まれています。 これは、強制隔離プロセスの一環として頻繁に更新されます（レコードは最初の配信エラーで作成され、カウンターが変更されると更新され、配信が成功すると削除されます）。<br /> </td> 
  </tr> 
  <tr> 
   <td> XtkWorkflow<br /> </td> 
   <td> 小 <br /> </td> 
   <td> 更新 <br /> </td> 
   <td> ワークフローインスタンスごとに 1 つのレコードがあるので、レコードはほとんどありません。 ただし、テーブルは定期的に更新され、ステータスと進行状況が反映されます。<br /> </td> 
  </tr> 
  <tr> 
   <td> XtkWorkflowTask<br /> </td> 
   <td> 小 <br /> </td> 
   <td> 挿入、更新、削除 <br /> </td> 
   <td> ワークフローアクティビティを実行するたびに、このテーブルにレコードが作成されます。 パージのメカニズムによって、有効期限が切れたら削除されます。<br /> </td> 
  </tr> 
  <tr> 
   <td> XtkWorkflowEvent<br /> </td> 
   <td> 小 <br /> </td> 
   <td> 挿入、更新、削除 <br /> </td> 
   <td> ワークフローのタスク間でアクティブ化された各トランジションによって、このテーブルにレコードが作成されます。 パージメカニズムは、有効期限が切れたらそれらを削除します。<br /> </td> 
  </tr> 
  <tr> 
   <td> XtkWorkflowJob<br /> </td> 
   <td> 非常に小さい <br /> </td> 
   <td> 挿入、更新、削除 <br /> </td> 
   <td> このテーブルは、ワークフローエンジンに固有のテーブルです。 ワークフローへのコマンドの送信を有効にします（開始、停止、一時停止など）。 小さいテーブルですが、ワークフローにリンクされたトランザクションテーブルのパージ時には、このテーブルが考慮されます。<br /> </td> 
  </tr> 
  <tr> 
   <td> NmsBroadlog<br /> </td> 
   <td> 最大 <br /> </td> 
   <td> 挿入、更新、削除 <br /> </td> 
   <td> これはシステム最大のテーブルです。 送信されたメッセージごとに 1 つのレコードがあり、これらのレコードは、配信ステータスを追跡するために挿入、更新され、履歴がパージされると削除されます。<br /> </td> 
  </tr> 
  <tr> 
   <td> NmsTrackingLog<br /> </td> 
   <td> 大 <br /> </td> 
   <td> 挿入、削除 <br /> </td> 
   <td> トラッキングログは、履歴がパージされると挿入および削除されますが、更新されません。<br /> </td> 
  </tr> 
  <tr> 
   <td> NmsBroadlogMsg <br /> </td> 
   <td> 小 <br /> </td> 
   <td> 更新 <br /> </td> 
   <td> このテーブルには、SMTP エラーの検証に使用する情報が含まれています。 かなり小さいですが、大幅に更新されるので、このテーブルのインデックスは急速にフラグメント化される傾向があります。<br /> </td> 
  </tr> 
  <tr> 
   <td> NmsEmailErrorStat<br /> </td> 
   <td> Medium<br /> </td> 
   <td> 挿入、更新、削除 <br /> </td> 
   <td> このテーブルには、SMTP エラーの集計がドメイン別に並べ替えられています。 最初に含まれる詳細情報は、古くなった後にクリーンアップタスクによって集計されます。<br /> </td> 
  </tr> 
  <tr> 
   <td> NmsBroadLogMid （ミッドソーシングインスタンス上） <br /> </td> 
   <td> 大 <br /> </td> 
   <td> 挿入、更新、削除 <br /> </td> 
   <td> 5.10 （またはそれ以降）インスタンスがミッドソーシングインスタンスとして使用される場合のみ。 これはデータベースで最大のテーブルの 1 つです。 送信されたメッセージごとに 1 つのレコードがあり、これらのレコードは、配信ステータスを追跡するために挿入、更新され、履歴がパージされると削除されます。 ミッドソーシングを使用する場合、履歴を制限することをお勧めします（通常は 2 か月未満）。そのため、このテーブルはサイズの面で妥当ですが（6,000 万行に対して 30 未満、data+index）、時々再構築することが非常に重要です。<br /> </td> 
  </tr> 
  <tr> 
   <td> NmsBroadLogRcp （NmsRecipient テーブルが使用される場合） <br /> </td> 
   <td> 大 <br /> </td> 
   <td> 挿入、更新、削除 <br /> </td> 
   <td> これはシステム最大のテーブルです。 送信されたメッセージごとに 1 つのレコードがあり、これらのレコードは、配信ステータスを追跡するために挿入、更新され、履歴がパージされると削除されます。 5.10 では、SMTP メッセージテキストが 5.10 バージョンの NmsBroadLogMsg テーブルでファクタリングされるので、このテーブルは 4.05 （NmsBroadLog）の同等のテーブルよりも小さいことに注意してください。 ただし、このテーブルのインデックスを定期的に（最初の処理を 1 週間おきに）再作成し、ときどき（月に 1 回、またはパフォーマンスに影響が出たとき）完全に再構築する必要があります。<br /> </td> 
  </tr> 
  <tr> 
   <td> YyyBroadLogXxx （外部受信者テーブルを使用する場合） <br /> </td> 
   <td> 大 <br /> </td> 
   <td> 挿入、更新、削除 <br /> </td> 
   <td> NmsBroadLogRcp と同じですが、外部受信者テーブルがあります。 Yyy と Xxx を配信マッピングの値に適応させてください。<br /> </td> 
  </tr> 
  <tr> 
   <td> NmsTrackingLogRcp （NmsRecipient テーブルが使用される場合） <br /> </td> 
   <td> 大 <br /> </td> 
   <td> 挿入、削除 <br /> </td> 
   <td> トラッキングログは、履歴がパージされると挿入および削除されますが、更新されません。 ボリュームは、データ保持の長さによって異なります。<br /> </td> 
  </tr> 
  <tr> 
   <td> YyyTrackingLogXxx （外部受信者テーブルを使用する場合） <br /> </td> 
   <td> 大 <br /> </td> 
   <td> 挿入、削除 <br /> </td> 
   <td> NmsTrackingLogRcp と同じですが、外部受信者テーブルが含まれます。 Yyy と Xxx を、配信マッピングで使用されている値に適応させてください。<br /> </td> 
  </tr> 
  <tr> 
   <td> NmsBroadLogRtEvent （Message Center 実行インスタンス） <br /> </td> 
   <td> 大 <br /> </td> 
   <td> 挿入、更新、削除 <br /> </td> 
   <td> 他の broadlog テーブルと似ていますが、NmsRecipient.<br /> の代わりに NmsRtEvent を持ちます。 </td> 
  </tr> 
  <tr> 
   <td> NmsTrackingLogRtEvent （Message Center 実行インスタンス） <br /> </td> 
   <td> 大 <br /> </td> 
   <td> 挿入、削除 <br /> </td> 
   <td> 他の trackingLog テーブルと同様ですが、NmsRecipient.<br /> の代わりに NmsRtEvent テーブルを使用します。 </td> 
  </tr> 
  <tr> 
   <td> NmsRtEvent （Message Center 実行インスタンス） <br /> </td> 
   <td> 大 <br /> </td> 
   <td> 挿入、更新、削除 <br /> </td> 
   <td> Message Center のイベントキューを含むテーブル。 これらのイベントのステータスは、処理されると Message Center によって更新されます。 削除はパージ中に実行されます。 このテーブルのインデックスを定期的に再作成し、再構築することをお勧めします。<br /> </td> 
  </tr> 
  <tr> 
   <td> NmsEventHisto （Message Center コントロールインスタンス） <br /> </td> 
   <td> 大 <br /> </td> 
   <td> 挿入、更新、削除 <br /> </td> 
   <td> NmsRtEvent と同様です。 このテーブルは、すべての実行インスタンスのすべてのイベントをアーカイブします。 リアルタイムプロセスでは使用されず、レポートでのみ使用されます。<br /> </td> 
  </tr> 
  <tr> 
   <td> NmsMobileApp<br /> </td> 
   <td> 非常に小さい <br /> </td> 
   <td> 挿入、更新、削除 <br /> </td> 
   <td> モバイルアプリケーションとその設定を含むテーブル。<br /> </td> 
  </tr> 
  <tr> 
   <td> NmsAppSubscriptionRcp<br /> </td> 
   <td> 大 <br /> </td> 
   <td> 挿入、更新 <br /> </td> 
   <td> 通知の送信に使用されるモバイルデバイスの識別子（アドレス）を含むテーブル （受信者テーブルと同様）。<br /> </td> 
  </tr> 
  <tr> 
   <td> NmsBroadLogAppSubrcp<br /> </td> 
   <td> 大 <br /> </td> 
   <td> 挿入、更新、削除 <br /> </td> 
   <td> 他の broadlog テーブルと同様ですが、NmsRecipient.<br /> の代わりに NmsappSubscriptionRcp を使用します。 </td> 
  </tr> 
  <tr> 
   <td> NmsTrackingLogAppSubRcp<br /> </td> 
   <td> 大 <br /> </td> 
   <td> 挿入、削除 <br /> </td> 
   <td> 他の trackingLog テーブルと同様ですが、NmsRecipient.<br /> の代わりに NmsappSubscriptionRcp テーブルを使用します。 </td> 
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

前述のリストに加えて、お客様がプラットフォーム設定時に作成した（Adobe Campaign データモデルに存在しない）テーブルも、特にデータの読み込み中や同期処理中に頻繁に更新される場合、断片化の影響を受ける可能性があります。 これらのテーブルは、デフォルトのAdobe Campaign データモデル（例：**NmsRecipient**）の一部にすることができます。 この場合、カスタムテーブルを見つけるには、Adobe Campaign プラットフォームの管理者が個々のデータベースモデルの監査を実施する必要があります。 これらのテーブルは、アドビのメンテナンス手順で必ずしも明示的に言及されているわけではありません。
