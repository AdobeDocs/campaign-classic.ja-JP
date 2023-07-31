---
product: campaign
title: データベースクリーンアップのワークフロー
description: 古いデータが自動的にクリーンアップされる方法を説明します。
feature: Monitoring, Workflows
badge-v7-only: label="v7" type="Informative" tooltip="Campaign Classicv7 にのみ適用"
audience: production
content-type: reference
topic-tags: data-processing
exl-id: 75d3a0af-9a14-4083-b1da-2c1b22f57cbe
source-git-commit: 3a9b21d626b60754789c3f594ba798309f62a553
workflow-type: tm+mt
source-wordcount: '2917'
ht-degree: 2%

---

# データベースクリーンアップのワークフロー{#database-cleanup-workflow}



## はじめに {#introduction}

**[!UICONTROL 管理／プロダクション／テクニカルワークフロー]**&#x200B;ノードからアクセスできる&#x200B;**[!UICONTROL データベースクリーンアップ]**&#x200B;ワークフローを使用すると、古いデータを削除して、データベースの急激な増加を回避できます。ワークフローは、ユーザーの操作なしで自動的にトリガーされます。

![cleanup](assets/ncs_cleanup_workflow.png)

## 設定 {#configuration}

データベースクリーンアップは、ワークフロースケジューラーとデプロイウィザードの 2 つのレベルで設定します。

### ワークフロースケジューラー {#the-scheduler}

>[!NOTE]
>
>スケジューラーについて詳しくは、[この節](../../workflow/using/scheduler.md)を参照してください。

デフォルトでは、 **[!UICONTROL データベースのクリーンアップ]** 毎日午前 4 時に開始するようにワークフローが設定されている。 スケジューラーを使用すると、ワークフローのトリガー頻度を変更できます。 次の頻度を使用できます。

* **[!UICONTROL 1 日に数回]**
* **[!UICONTROL 日]**
* **[!UICONTROL 毎週]**
* **[!UICONTROL 1 回]**

![scheduler](assets/ncs_cleanup_scheduler.png)

>[!IMPORTANT]
>
>次に対して **[!UICONTROL データベースのクリーンアップ]** ワークフローがスケジューラーで定義された日時に開始するには、ワークフローエンジン (wfserver) を開始する必要があります。

### デプロイメントウィザード {#deployment-wizard}

The **[!UICONTROL デプロイウィザード]**（経由でアクセス） **[!UICONTROL ツール/詳細]** メニューを使用して、データの保存期間を設定できます。 値は日数で表します。 これらの値が変更されない場合、ワークフローはデフォルト値を使用します。

![](assets/ncs_cleanup_deployment-wizard.png)

のフィールド **[!UICONTROL データのパージ]** ウィンドウは次のオプションと一致します。 これらは、 **[!UICONTROL データベースのクリーンアップ]** ワークフロー：

* 統合されたトラッキング： **NmsCleanup_TrackingStatPurgeDelay** ( [トラッキングログのクリーンアップ](#cleanup-of-tracking-logs))
* 配信ログ： **NmsCleanup_BroadLogPurgeDelay** ( [配信ログのクリーンアップ](#cleanup-of-delivery-logs))
* トラッキングログ： **NmsCleanup_TrackingLogPurgeDelay** ( [トラッキングログのクリーンアップ](#cleanup-of-tracking-logs))
* 削除された配信： **NmsCleanup_RecycledDeliveryPurgeDelay** ( [削除またはリサイクルする配信のクリーンアップ](#cleanup-of-deliveries-to-be-deleted-or-recycled))
* 却下をインポート： **NmsCleanup_RejectsPurgeDelay** ( [インポートによって生成された却下のクリーンアップ](#cleanup-of-rejects-generated-by-imports-))
* 訪問者プロファイル： **NmsCleanup_VisitorPurgeDelay** ( [訪問者のクリーンアップ](#cleanup-of-visitors))
* オファーの提案： **NmsCleanup_PropositionPurgeDelay** ( [提案のクリーンアップ](#cleanup-of-propositions))

  >[!NOTE]
  >
  >The **[!UICONTROL オファーの提案]** フィールドは、 **インタラクション** モジュールがインストールされている。

* イベント： **NmsCleanup_EventPurgeDelay** ( [期限切れのイベントのクレンジング](#cleansing-expired-events))
* アーカイブしたイベント： **NmsCleanup_EventHistoPurgeDelay** ( [期限切れのイベントのクレンジング](#cleansing-expired-events))

  >[!NOTE]
  >
  >The **[!UICONTROL イベント]** および **[!UICONTROL アーカイブしたイベント]** フィールドは、 **Message Center** モジュールがインストールされている。

* 監査証跡： **XtkCleanup_AuditTrailPurgeDelay** ( [監査証跡のクリーンアップ](#cleanup-of-audit-trail))

が実行するすべてのタスク **[!UICONTROL データベースのクリーンアップ]** ワークフローについては、次の節で説明します。

## データベースクリーンアップワークフローで実行されるタスク {#tasks-carried-out-by-the-database-cleanup-workflow}

ワークフロースケジューラーで定義された日時 ( [スケジューラ](#the-scheduler)) の場合、ワークフローエンジンはデータベースのクリーンアッププロセスを開始します。 データベースクリーンアップは、データベースに接続し、以下に示す順序でタスクを実行します。

>[!IMPORTANT]
>
>これらのタスクの 1 つが失敗した場合、次のタスクは実行されません。
>
>を使用した SQL クエリ **制限** 属性は、すべての情報が処理されるまで繰り返し実行されます。


### クリーンアップを削除するリスト {#lists-to-delete-cleanup}

が実行する最初のタスク **[!UICONTROL データベースのクリーンアップ]** ワークフローは、 **deleteStatus != 0** 属性 **NmsGroup**. これらのグループにリンクされ、他のテーブルに存在するレコードも削除されます。

1. 削除するリストは、次の SQL クエリを使用して復元します。

   ```sql
   SELECT iGroupId, sLabel, iType FROM NmsGroup WHERE iDeleteStatus <> 0 OR tsExpirationDate <= GetDate() 
   ```

1. 各リストには、他のテーブルへのリンクが複数あります。 次のクエリを使用すると、これらのリンクはすべて一括削除されます。

   ```sql
   DELETE FROM $(relatedTable) WHERE iGroupId=$(l) IN (SELECT iGroupId FROM $(relatedTable) WHERE iGroupId=$(l) LIMIT 5000) 
   ```

   場所 `$(relatedTable)` は、 **NmsGroup** および `$(l)` はリスト識別子です。

1. リストが「リスト」タイプのリストの場合、関連するテーブルは次のクエリを使用して削除されます。

   ```sql
   DROP TABLE grp$(l)
   ```

1. 毎 **選択** 操作で復元されたタイプリストは、次のクエリを使用して削除されます。

   ```sql
   DELETE FROM NmsGroup WHERE iGroupId=$(l) 
   ```

   場所 `$(l)` はリスト識別子です。

### 削除またはリサイクルする配信のクリーンアップ {#cleanup-of-deliveries-to-be-deleted-or-recycled}

このタスクは、削除またはリサイクルするすべての配信を削除します。

1. The **[!UICONTROL データベースのクリーンアップ]** ワークフローは、 **deleteStatus** フィールドの値が **[!UICONTROL はい]** または **[!UICONTROL リサイクル済み]** 削除日が、 **[!UICONTROL 削除された配信]** (**NmsCleanup_RecycledDeliveryPurgeDelay**) フィールドに値を入力する必要があります。 詳しくは、 [デプロイウィザード](#deployment-wizard). この期間は、現在のサーバーの日付に基づいて計算されます。
1. タスクはミッドソーシングサーバーごとに、削除する配信のリストを選択します。
1. The **[!UICONTROL データベースのクリーンアップ]** 配信ログ、添付ファイル、ミラーページの情報、およびその他すべての関連データを削除します。
1. 配信を適切に削除する前に、ワークフローは次のテーブルからリンクされた情報を削除します。

   * 配信の除外テーブル (**NmsDlvExclusion**) の場合は、次のクエリが使用されます。

     ```sql
     DELETE FROM NmsDlvExclusion WHERE iDeliveryId=$(l)
     ```

     場所 **$(l)** は、配信の識別子です。

   * クーポンテーブル (**NmsCouponValue**) の場合は、次のクエリが使用されます（一括削除の場合）。

     ```sql
     DELETE FROM NmsCouponValue WHERE iMessageId IN (SELECT iMessageId FROM NmsCouponValue WHERE EXISTS (SELECT B.iBroadLogId FROM $(BroadLogTableName) B WHERE B.iDeliveryId = $(l) AND B.iBroadLogId = iMessageId ) LIMIT 5000)
     ```

     場所 `$(l)` は、配信の識別子です。

   * 配信ログテーブル (**NmsBroadlogXxx**)、大量削除は 20,000 個のレコードのバッチで実行されます。
   * オファーの提案テーブル (**NmsPropositionXxx**)、大量削除は 20,000 個のレコードのバッチで実行されます。
   * トラッキングログテーブル (**NmsTrackinglogXxx**)、大量削除は 20,000 個のレコードのバッチで実行されます。
   * 配信フラグメントテーブル (**NmsDeliveryPart**)、大量削除は 500,000 個のレコードのバッチで実行されます。 このテーブルには、配信される残りのメッセージに関するパーソナライゼーション情報が含まれます。
   * ミラーページのデータフラグメントテーブル (**NmsMirrorPageInfo**)、一括削除は、期限切れの配信部分と完了またはキャンセルされた配信部分に対して、20,000 個のレコードのバッチで実行されます。 この表には、ミラーページの生成に使用されるすべてのメッセージに関するパーソナライゼーション情報が含まれています。
   * ミラーページの検索テーブル (**NmsMirrorPageSearch**)、大量削除は 20,000 個のレコードのバッチで実行されます。 このテーブルは、 **NmsMirrorPageInfo** 表。
   * バッチ処理ログテーブル (**XtkJobLog**)、大量削除は 20,000 個のレコードのバッチで実行されます。 このテーブルには、削除される配信のログが含まれています。
   * 配信 URL トラッキングテーブル (**NmsTrackingUrl**) の場合は、次のクエリが使用されます。

     ```sql
     DELETE FROM NmsTrackingUrl WHERE iDeliveryId=$(l)
     ```

     場所 `$(l)` は、配信の識別子です。

     このテーブルには、削除される配信内の、トラッキングを有効にする URL が含まれています。

1. 配信が配信テーブル (**NmsDelivery**):

   ```sql
   DELETE FROM NmsDelivery WHERE iDeliveryId = $(l)
   ```

   場所 `$(l)` は、配信の識別子です。

#### ミッドソーシングを使用する配信 {#deliveries-using-mid-sourcing}

The **[!UICONTROL データベースのクリーンアップ]** ワークフローは、ミッドソーシングサーバー上の配信も削除します。

1. これをおこなうには、ワークフローで、（ステータスに基づいて）各配信が非アクティブであることを確認します。 アクティブな配信は、削除される前に停止されます。 チェックは、次のクエリを実行して実行します。

   ```sql
   SELECT iState FROM NmsDelivery WHERE iDeliveryId = $(l) AND iState <> 100;
   ```

   場所 **$(l)** は、配信の識別子です。

1. ステータスの値が **[!UICONTROL 開始を保留中]** , **[!UICONTROL 処理中]** , **[!UICONTROL 回復待ち]** , **[!UICONTROL 復元中]** , **[!UICONTROL リクエストされた一時停止]** , **[!UICONTROL 一時停止中]** または **[!UICONTROL 一時停止]** （値 51、55、61、62、71、72、75）、配信が停止され、タスクがリンクされた情報をパージします。

### 期限切れの配信のクリーンアップ {#cleanup-of-expired-deliveries}

このタスクは、有効期間が過ぎた配信を停止します。

1. The **[!UICONTROL データベースのクリーンアップ]** ワークフローは、期限切れの配信のリストを作成します。 このリストには、以外のステータスを持つすべての期限切れの配信が含まれます **[!UICONTROL 完了]** に加えて、10,000 件を超える未処理のメッセージを含む、最近配信が停止されました。 次のクエリが使用されます。

   ```sql
   SELECT iDeliveryId, iState FROM NmsDelivery WHERE iDeleteStatus=0 AND iIsModel=0 AND iDeliveryMode=1 AND ( (iState >= 51 AND iState < 85 AND tsValidity IS NOT NULL AND tsValidity < $(currentDate) ) OR (iState = 85 AND DateMinusDays(15) < tsLastModified AND iToDeliver - iProcessed >= 10000 ))
   ```

   場所 `delivery mode 1` が **[!UICONTROL 一括配信]** モード、 `state 51` が **[!UICONTROL 開始を保留中]** 州、 `state 85` が **[!UICONTROL 停止]** と、配信サーバー上で一括更新された配信ログの最大数が 10,000 に等しい。

1. 次に、ミッドソーシングを使用する最近期限切れの配信のリストがワークフローに含まれます。 ミッドソーシングサーバー経由で復元された配信ログがまだない配信は除外されます。

   次のクエリが使用されます。

   ```sql
   SELECT iDeliveryId, tsValidity, iMidRemoteId, mData FROM NmsDelivery WHERE (iDeliveryMode = 4 AND (iState = 85 OR iState = 95) AND tsValidity IS NOT NULL AND (tsValidity < SubDays(GetDate() , 15) OR tsValidity < $(DateOfLastLogPullUp)) AND tsLastModified > SubDays(GetDate() , 15))
   ```

1. 次のクエリは、配信を日付でフィルタリングするために、外部アカウントがまだアクティブかどうかを検出するために使用します。

   ```sql
   SELECT iExtAccountId FROM NmsExtAccount WHERE iActive<>0 AND sName=$(providerName)
   ```

1. 期限切れの配信のリストで、ステータスが「 」の配信ログを **[!UICONTROL 保留中]** 、に切り替えます。 **[!UICONTROL 配信がキャンセル済み]** を選択し、このリスト内のすべての配信を **[!UICONTROL 完了]** .

   次のクエリが使用されます。

   ```sql
   UPDATE $(BroadLogTableName) SET tsLastModified=$(curdate), iStatus=7, iMsgId=$(bl) WHERE iDeliveryId=$(dl) AND iStatus=6
   ```

   場所 `$(curdate)`は、データベース・サーバの現在の日付です。 `$(bl)` は、配信ログメッセージの識別子です。 `$(dl)` は配信識別子です。 `delivery status 6` が **[!UICONTROL 保留中]** ステータスと `delivery status 7` が **[!UICONTROL 配信がキャンセル済み]** ステータス。

   ```sql
   UPDATE NmsDelivery SET iState = 95, tsLastModified = $(curdate), tsBroadEnd = tsValidity WHERE iDeliveryId = $(dl)
   ```

   場所 `delivery state 95` が **[!UICONTROL 完了]** ステータス、および `$(dl)` は、配信の識別子です。

1. すべてのフラグメント (**deliveryParts**) 古い配信の ) は削除され、進行中の通知配信の古いフラグメントはすべて削除されます。 一括削除は、両方のタスクに使用されます。

   次のクエリが使用されます。

   ```sql
   DELETE FROM NmsDeliveryPart WHERE iDeliveryPartId IN (SELECT iDeliveryPartId FROM NmsDeliveryPart WHERE iDeliveryId IN (SELECT iDeliveryId FROM NmsDelivery WHERE iState=95 OR iState=85) LIMIT 5000)
   ```

   ```sql
   DELETE FROM NmsDeliveryPart WHERE iDeliveryPartId IN (SELECT iDeliveryPartId FROM NmsDeliveryPart WHERE tsValidity < $(curDate) LIMIT 500000)
   ```

   場所 `delivery state 95` が **[!UICONTROL 完了]** ステータス、 `delivery state 85` が **[!UICONTROL 停止]** ステータス、および `$(curDate)` は、現在のサーバーの日付です。

### ミラーページのクリーンアップ {#cleanup-of-mirror-pages}

このタスクは、配信で使用されている Web リソース（ミラーページ）を削除します。

1. まず、パージされる配信のリストは、次のクエリを使用して復元します。

   ```sql
   SELECT iDeliveryId, iNeedMirrorPage FROM NmsDelivery WHERE iWebResPurged = 0 AND tsWebValidity IS NOT NULL AND tsWebValidity < $(curdate)
   ```

   場所 `$(curDate)` は、現在のサーバーの日付です。

1. The **NmsMirrorPageInfo** 必要に応じて、以前に復元した配信の識別子を使用して、テーブルがパージされます。 一括削除は、次のクエリの生成に使用されます。

   ```sql
   DELETE FROM NmsMirrorPageInfo WHERE iMirrorPageInfoId IN (SELECT iMirrorPageInfoId FROM NmsMirrorPageInfo WHERE iDeliveryId = $(dl)) LIMIT 5000
   ```

   ```sql
   DELETE FROM NmsMirrorPageSearch WHERE iMessageId IN (SELECT iMessageId FROM NmsMirrorPageSearch WHERE iDeliveryId = $(dl)) LIMIT 5000
   ```

   場所 `$(dl)` は、配信の識別子です。

1. 次に、エントリが配信ログに追加されます。
1. パージされた配信は識別され、後で再処理する必要がなくなります。 次のクエリが実行されます。

   ```sql
   UPDATE NmsDelivery SET iWebResPurged = 1 WHERE iDeliveryId IN ($(strIn))
   ```

   場所 `$(strIn)` は、配信 ID のリストです。

### 作業用テーブルのクリーンアップ {#cleanup-of-work-tables}

このタスクは、ステータスが「 」の配信に一致するすべての作業用テーブルをデータベースから削除します **[!UICONTROL 編集中]** , **[!UICONTROL 停止]** または **[!UICONTROL 削除済み]** .

1. 名前がで始まるテーブルのリスト **wkDlv_** は、最初に次のクエリ (postgresql) で復元されます。

   ```sql
   SELECT relname FROM pg_class WHERE relname LIKE Lower('wkDlv_') ESCAPE E'\\' AND relkind IN ('r','v') AND pg_get_userbyid(relowner)<>'postgres'
   ```

1. その後、進行中のワークフローで使用されるテーブルは除外されます。 これをおこなうには、処理中の配信のリストを、次のクエリを使用して復元します。

   ```sql
   SELECT iDeliveryId FROM NmsDelivery WHERE iDeliveryId<>0 AND iDeleteStatus=0 AND iState NOT IN (0,85,100);
   ```

   場所 `0` は、 **[!UICONTROL 編集中]** 配信ステータス `85` が **[!UICONTROL 停止]** ステータスと `100` が **[!UICONTROL 削除済み]** ステータス。

1. 使用されなくなったテーブルは、次のクエリを使用して削除されます：

   ```sql
   DROP TABLE wkDlv_15487_1;
   ```

### インポートによって生成された却下のクリーンアップ {#cleanup-of-rejects-generated-by-imports-}

この手順では、すべてのデータがインポート中に処理されなかったレコードを削除できます。

1. 一括削除は **XtkReject** 次のクエリを含むテーブル：

   ```sql
   DELETE FROM XtkReject WHERE iRejectId IN (SELECT iRejectId FROM XtkReject WHERE tsLog < $(curDate)) LIMIT $(l)
   ```

   場所 `$(curDate)` は、現在のサーバーの日付です。この日付から、 **NmsCleanup_RejectsPurgeDelay** オプション ( [デプロイウィザード](#deployment-wizard)) および `$(l)` は、一括削除するレコードの最大数です。

1. すべてのオーファンの却下は、次のクエリを使用して削除されます。

   ```sql
   DELETE FROM XtkReject WHERE iJobId NOT IN (SELECT iJobId FROM XtkJob)
   ```

### ワークフローインスタンスのクリーンアップ {#cleanup-of-workflow-instances}

このタスクは、各ワークフローインスタンスをその識別子 (**lWorkflowId**) および履歴 (**履歴**) をクリックします。 作業用テーブルのクリーンアップタスクを再度実行すると、非アクティブなテーブルが削除されます。 また、削除されたワークフローの孤立した作業用テーブル（wkf%と wkfhisto%）もすべて削除されます。

>[!NOTE]
>
>履歴のパージ頻度は、 **履歴（日数）** フィールド（デフォルト値は 30 日）。 このフィールドは、 **実行** 」タブを使用します。 詳しくは、[この節](../../workflow/using/workflow-properties.md#execution)を参照してください。

1. 削除するワークフローのリストを復元するには、次のクエリを使用します。

   ```sql
   SELECT iWorkflowId, iHistory FROM XtkWorkflow WHERE iWorkflowId<>0
   ```

1. このクエリは、次のクエリを使用して、リンクされたすべてのログ、完了したタスクおよび完了したイベントを削除するために使用されるワークフローのリストを生成します。

   ```sql
   DELETE FROM XtkWorkflowLog WHERE iWorkflowId=$(lworkflow) AND tsLog < DateMinusDays($(lhistory))
   ```

   ```sql
   DELETE FROM XtkWorkflowTask WHERE iWorkflowId=$(lworkflow) AND iStatus<>0 AND tsCompletion < DateMinusDays($(lhistory)) 
   ```

   ```sql
   DELETE FROM XtkWorkflowEvent WHERE iWorkflowId=$(l) AND iStatus>2 AND tsProcessing < DateMinusDays($(lHistory))
   ```

   場所 `$(lworkflow)` はワークフローの識別子で、は `$(lhistory)` は、履歴の識別子です。

1. 未使用のテーブルはすべて削除されます。 この目的で、すべてのテーブルは、 **wkf%** 次のクエリを使用して mask と入力します (postgresql)。

   ```sql
   SELECT relname FROM pg_class WHERE relname LIKE Lower('wkf%') ESCAPE E'\\' AND relkind IN ('r','v') AND pg_get_userbyid(relowner)<>'postgres'
   ```

1. 保留中のワークフローインスタンスで使用されるすべてのテーブルが除外されます。 アクティブなワークフローのリストは、次のクエリを使用して復元されます。

   ```sql
   SELECT iWorkflowId FROM XtkWorkflow WHERE iWorkflowId<>0 AND iState<>20
   ```

1. 次に、各ワークフロー識別子が復元され、進行中のワークフローで使用されるテーブルの名前が見つかります。 これらの名前は、以前に復元したテーブルのリストから除外されます。
1. 「増分処理クエリ」タイプのアクティビティ履歴テーブルは、次のクエリを使用して除外されます。

   ```sql
   SELECT relname FROM pg_class WHERE relname LIKE Lower('wkfhisto%') ESCAPE E'\\' AND relkind IN ('r','v') AND pg_get_userbyid(relowner)<>'postgres'
   ```

   ```sql
   SELECT iWorkflowId FROM XtkWorkflow WHERE iWorkflowId IN ($(strCondition))
   ```

   場所 `$(strcondition)` は、 **wkfhisto%** マスク。

1. 残りのテーブルは、次のクエリを使用して削除されます。

   ```sql
   DROP TABLE wkf15487_12;
   ```

### ワークフローログインのクリーンアップ {#cleanup-of-workflow-logins}

このタスクは、次のクエリを使用してワークフローログインを削除します。

```sql
DELETE FROM XtkWorkflowLogin WHERE iWorkflowId NOT IN (SELECT iWorkflowId FROM XtkWorkflow)
```

### 孤立した作業用テーブルのクリーンアップ {#cleanup-of-orphan-work-tables}

このタスクは、グループにリンクされた孤立した作業用テーブルを削除します。 The **NmsGroup** テーブルには、クレンジングするグループが格納されます（0 とは異なるタイプ）。 テーブル名のプレフィックスは、 **grp**. クレンジングするグループを識別するには、次のクエリを使用します。

```sql
SELECT iGroupId FROM NmsGroup WHERE iType>0"
```

### 訪問者のクリーンアップ {#cleanup-of-visitors}

このタスクでは、一括削除を使用して訪問者テーブルから古いレコードを削除します。 古いレコードは、最後の変更がデプロイウィザードで定義された保存期間よりも早いレコードです（を参照）。 [デプロイウィザード](#deployment-wizard)) をクリックします。 次のクエリが使用されます。

```sql
DELETE FROM NmsVisitor WHERE iVisitorId IN (SELECT iVisitorId FROM NmsVisitor WHERE iRecipientId = 0 AND tsLastModified < AddDays(GetDate(), -30) AND iOrigin = 0 LIMIT 20000)
```

場所 `$(tsDate)` は現在のサーバーの日付で、この日付から、 **NmsCleanup_VisitorPurgeDelay** オプション。

### NPAI のクリーンアップ {#cleanup-of-npai}

このタスクを使用すると、有効なアドレスと一致するレコードを **NmsAddress** 表。 一括削除の実行には、次のクエリを使用します。

```sql
DELETE FROM NmsAddress WHERE iAddressId IN (SELECT iAddressId FROM NmsAddress WHERE iStatus=2 AND tsLastModified < $(tsDate1) AND tsLastModified >= $(tsDate2) LIMIT 5000)
```

場所 `status 2` が **[!UICONTROL 有効]** ステータス、 `$(tsDate1)` は現在のサーバーの日付で、 `$(tsDate2)` が **NmsCleanup_LastCleanup** オプション。

### 購読のクリーンアップ {#cleanup-of-subscriptions-}

このタスクは、ユーザーが削除したすべての購読を **NmsSubscription** 一括削除を使用した表。 次のクエリが使用されます。

```sql
DELETE FROM NmsSubscription WHERE iDeleteStatus <>0
```

### トラッキングログのクリーンアップ {#cleanup-of-tracking-logs}

このタスクは、古いレコードをトラッキングおよび Web トラッキングログテーブルから削除します。 古いレコードは、デプロイウィザードで定義された保存期間より前のレコードです ( [デプロイウィザード](#deployment-wizard)) をクリックします。

1. まず、トラッキングログテーブルのリストを、次のクエリを使用して復元します。

   ```sql
   SELECT distinct(sTrackingLogSchema) FROM NmsDeliveryMapping WHERE sTrackingLogSchema IS NOT NULL;
   ```

1. 一括削除は、以前に復元したテーブルのリスト内のすべてのテーブルをパージするために使用します。 次のクエリが使用されます。

   ```sql
   DELETE FROM NmsTrackingLogRcp WHERE iTrackingLogId IN (SELECT iTrackingLogId FROM NmsTrackingLogRcp WHERE tsLog < $(tsDate) LIMIT 5000) 
   ```

   場所 `$(tsDate)` は、現在のサーバーの日付です。この日付から、 **NmsCleanup_TrackingLogPurgeDelay** オプション。

1. トラッキング統計テーブルは、一括削除を使用してパージされます。 次のクエリが使用されます。

   ```sql
   DELETE FROM NmsTrackingStats WHERE iTrackingStatsId IN (SELECT iTrackingStatsId FROM NmsTrackingStats WHERE tsStart < $(tsDate) LIMIT 5000) 
   ```

   場所 `$(tsDate)` は、現在のサーバーの日付です。この日付から、 **NmsCleanup_TrackingStatPurgeDelay** オプション。

### 配信ログのクリーンアップ {#cleanup-of-delivery-logs}

このタスクでは、様々なテーブルに保存されている配信ログをパージできます。

1. この目的で、配信ログスキーマのリストは、次のクエリを使用して復元されます。

   ```sql
   SELECT distinct(sBroadLogSchema) FROM NmsDeliveryMapping WHERE sBroadLogSchema IS NOT NULL UNION SELECT distinct(sBroadLogExclSchema) FROM NmsDeliveryMapping WHERE sBroadLogExclSchema IS NOT NULL
   ```

1. ミッドソーシングを使用する場合、 **NmsBroadLogMid** 配信マッピングでテーブルが参照されていません。 The **nms:broadLogMid** 前のクエリで復元されたリストにスキーマが追加されます。
1. The **データベースのクリーンアップ** 次に、以前に復元したテーブルから古いデータを削除します。 次のクエリが使用されます。

   ```sql
   DELETE FROM $(tableName) WHERE iBroadLogId IN (SELECT iBroadLogId FROM $(tableName) WHERE tsLastModified < $(option) LIMIT 5000) 
   ```

   場所 `$(tableName)` は、スキーマのリスト内の各テーブルの名前で、 `$(option)` は、 **NmsCleanup_BroadLogPurgeDelay** オプション ( [デプロイウィザード](#deployment-wizard)) をクリックします。

1. 最後に、ワークフローで **NmsProviderMsgId** テーブルが存在します。 その場合、古いデータはすべて次のクエリを使用して削除されます。

   ```sql
   DELETE FROM NmsProviderMsgId WHERE iBroadLogId IN (SELECT iBroadLogId FROM NmsProviderMsgId WHERE tsCreated < $(option) LIMIT 5000)
   ```

   場所 `$(option)` は、 **NmsCleanup_BroadLogPurgeDelay** オプション ( [デプロイウィザード](#deployment-wizard)) をクリックします。

### NmsEmailErrorStat テーブルのクリーンアップ {#cleanup-of-the-nmsemailerrorstat-table-}

このタスクは **NmsEmailErrorStat** 表。 メインプログラム (**coalesceErrors**) は 2 つの日付を定義します。

* **開始日**: **NmsLastErrorStatCoalesce** オプション、またはテーブル内の最新の日付。
* **終了日**：現在のサーバーの日付。

開始日が終了日以上の場合、処理は実行されません。 この場合、 **coalesceUpToDate** メッセージが表示されます。

開始日が終了日より前の場合、 **NmsEmailErrorStat** テーブルがクレンジングされている。

内のエラーの合計数 **NmsEmailErrorStat** 開始日から終了日の間のテーブルは、次のクエリを使用して復元されます。

```sql
SELECT COUNT(*) FROM NmsEmailErrorStat WHERE tsDate>= $(start) AND tsDate< $(end)
```

場所 `$end` および `$start` は、以前に定義した開始日と終了日です。

合計が 0 より大きい場合：

1. 特定のしきい値（20 に等しい）を超えるエラーのみを保持するために、次のクエリが実行されます。

   ```sql
   SELECT iMXIP, iPublicId, SUM(iTotalConnections), SUM(iTotalErrors), SUM(iMessageErrors), SUM(iAbortedConnections), SUM(iFailedConnections), SUM(iRefusedConnections), SUM(iTimeoutConnections) FROM NmsEmailErrorStat WHERE tsDate>=$(start ) AND tsDate<$(end ) GROUP BY iMXIP, iPublicId HAVING SUM(iTotalErrors) >= 20
   ```

1. The **coalesingErrors** メッセージが表示されます。
1. 開始日と終了日の間に発生したすべてのエラーを削除する新しい接続が作成されます。 次のクエリが使用されます。

   ```sql
   DELETE FROM NmsEmailErrorStat WHERE tsDate>=$(start) AND tsDate<$(end)
   ```

1. 各エラーは **NmsEmailErrorStat** 次のクエリを使用した表：

   ```sql
   INSERT INTO NmsEmailErrorStat(iMXIP, iPublicId, tsDate, iTotalConnections, iTotalErrors, iTimeoutConnections, iRefusedConnections, iAbortedConnections, iFailedConnections, iMessageErrors) VALUES($(lmxip ), $(lpublicId ), $(tsstart ), $(lconnections ), $(lconnectionErrors ),$(ltimeoutConnections ), $(lrefusedConnections ), $(labortedConnections ), $(lfailedConnections ), $(lmessageErrors))
   ```

   各変数は、前のクエリで取得した値と一致します。

1. The **開始** 変数が前のプロセスの値で更新され、ループが終了します。

ループとタスクが停止します。

クリーンアップは、 **NmsEmailError** および **cleanupNmsMxDomain** テーブル。

### NmsEmailError テーブルのクリーンアップ {#cleanup-of-the-nmsemailerror-table-}

次のクエリが使用されます。

```sql
DELETE FROM NmsEmailError WHERE iMXIP NOT IN (SELECT DISTINCT iMXIP FROM NmsEmailErrorStat)
```

このクエリでは、 **NmsEmailErrorStat** から **NmsEmailError** 表。

### NmsMxDomain テーブルのクリーンアップ {#cleanup-of-the-nmsmxdomain-table-}

次のクエリが使用されます。

```sql
DELETE FROM NmsMxDomain WHERE iMXIP NOT IN (SELECT DISTINCT iMXIP FROM NmsEmailErrorStat)
```

このクエリでは、リンクされたレコードのないすべての行を **NmsEmailErrorStat** テーブル **NmsMxDomain** 表。

### 提案のクリーンアップ {#cleanup-of-propositions}

次の場合、 **インタラクション** モジュールがインストールされている場合、このタスクが実行され、 **NmsPropositionXxx** テーブル。

提案テーブルのリストが復元され、次のクエリを使用して、各提案テーブルに対して一括削除が実行されます。

```sql
DELETE FROM NmsPropositionXxx WHERE iPropositionId IN (SELECT iPropositionId FROM NmsPropositionXxx WHERE tsLastModified < $(option) LIMIT 5000) 
```

場所 `$(option)` は、 **NmsCleanup_PropositionPurgeDelay** オプション ( [デプロイウィザード](#deployment-wizard)) をクリックします。

### シミュレーションテーブルのクリーンアップ {#cleanup-of-simulation-tables}

このタスクは、孤立したシミュレーションテーブル（オファーのシミュレーションや配信のシミュレーションにリンクされなくなったテーブル）を消去します。

1. クリーンアップが必要なシミュレーションのリストを復元するには、次のクエリを使用します。

   ```sql
   SELECT iSimulationId FROM NmsSimulation WHERE iSimulationId<>0
   ```

1. 削除するテーブルの名前は、 **wkSimu_** プレフィックスにシミュレーションの識別子を付けたもの ( 例： **wkSimu_456831_aggr**):

   ```sql
   DROP TABLE wkSimu_456831_aggr
   ```

### 監査証跡のクリーンアップ {#cleanup-of-audit-trail}

次のクエリが使用されます。

```sql
DELETE FROM XtkAudit WHERE tsChanged < $(tsDate)
```

場所 **$(tsDate)** は、現在のサーバーの日付です。この日付から、 **XtkCleanup_AuditTrailPurgeDelay** オプションが減算されます。

### Nmsaddress のクリーンアップ {#cleanup-of-nmsaddress}

次のクエリが使用されます。

```sql
DELETE FROM NmsAddress WHERE iAddressId IN (SELECT iAddressId FROM NmsAddress WHERE iStatus=STATUS_QUARANTINE AND tsLastModified < $(NmsCleanup_AppSubscriptionRcpPurgeDelay + 5d) AND iType IN (MESSAGETYPE_IOS, MESSAGETYPE_ANDROID ) LIMIT 5000)
```

このクエリは、iOSと Android に関連するすべてのエントリを削除します。

### 統計の更新とストレージの最適化 {#statistics-update}

The **XtkCleanup_NoStats** 「 」オプションを使用すると、クリーンアップワークフローのストレージ最適化手順の動作を制御できます。

次の場合、 **XtkCleanup_NoStats** オプションが存在しないか、その値が 0 の場合は、PostgreSQL の詳細モード (VACUUM VERBOSE ANALYZE) でストレージの最適化が実行され、他のすべてのデータベースの統計が更新されます。 このコマンドが実行されていることを確認するには、PostgreSQL ログを確認します。 VACUUM は次の形式で行を出力します。 `INFO: vacuuming "public.nmsactivecontact"` と ANALYZE は、次の形式で行を出力します。 `INFO: analyzing "public.nmsactivecontact"`.

このオプションの値が 1 の場合、統計の更新はどのデータベースでも実行されません。 次のログ行がワークフローログに表示されます。 `Option 'XtkCleanup_NoStats' is set to '1'`.

オプションの値が 2 の場合、これは PostgreSQL の詳細モード (ANALYZE VERBOSE) でストレージ分析を実行し、他のすべてのデータベースの統計を更新します。 このコマンドが実行されていることを確認するには、PostgreSQL ログを確認します。 ANALYZE は次の形式で行を出力します。 `INFO: analyzing "public.nmsactivecontact"`.

### 購読クリーンアップ (NMAC) {#subscription-cleanup--nmac-}

このタスクは、削除されたサービスまたはモバイルアプリケーションに関連するすべての購読を削除します。

broadlog スキーマのリストを復元するには、次のクエリを使用します。

```sql
SELECT distinct(sBroadLogSchema) FROM NmsDeliveryMapping WHERE sBroadLogSchema IS NOT NULL
```

次に、タスクは、 **appSubscription** これらのテーブルをリンクおよび削除します。

また、このクリーンアップワークフローは、無効= 1 で、 **NmsCleanup_AppSubscriptionRcpPurgeDelay** オプション。

### クレンジングセッション情報 {#cleansing-session-information}

このタスクは、 **sessionInfo** テーブルの場合、次のクエリが使用されます。

```sql
DELETE FROM XtkSessionInfo WHERE tsexpiration < $(curdate) 
```

### 期限切れのイベントのクレンジング {#cleansing-expired-events}

このタスクは、実行インスタンスで受信および格納されたイベントと、コントロールインスタンスでアーカイブされたイベントをクレンジングします。

### クレンジング反応 {#cleansing-reactions}

このタスクは反応をクレンジングします（テーブル） **NmsRemaMatchRcp**) をクリックし、仮説自体が削除されます。
