---
product: campaign
title: データベースクリーンアップのワークフロー
description: 古いデータが自動的にクリーンアップされる方法を説明します
audience: production
content-type: reference
topic-tags: data-processing
exl-id: 75d3a0af-9a14-4083-b1da-2c1b22f57cbe
source-git-commit: 6d53ba957fb567a9a921544418a73a9bde37c97b
workflow-type: tm+mt
source-wordcount: '2997'
ht-degree: 2%

---

# データベースクリーンアップのワークフロー{#database-cleanup-workflow}

![](../../assets/v7-only.svg)

## はじめに {#introduction}

**[!UICONTROL 管理／プロダクション／テクニカルワークフロー]**&#x200B;ノードからアクセスできる&#x200B;**[!UICONTROL データベースクリーンアップ]**&#x200B;ワークフローを使用すると、古いデータを削除して、データベースの急激な増加を回避できます。ワークフローは、ユーザーの操作なしで自動的にトリガーされます。

![](assets/ncs_cleanup_workflow.png)

## 設定 {#configuration}

データベースのクリーンアップは、次の 2 つのレベルで設定します。（ワークフロースケジューラーおよびデプロイウィザード内）。

### ワークフロースケジューラ {#the-scheduler}

>[!NOTE]
>
>スケジューラーについて詳しくは、[この節](../../workflow/using/scheduler.md)を参照してください。

デフォルトでは、**[!UICONTROL データベースのクリーンアップ]** ワークフローは、毎日午前 4 時に開始するように設定されています。 スケジューラーを使用して、ワークフローのトリガー頻度を変更できます。 次の頻度を使用できます。

* **[!UICONTROL 1 日に数回]**
* **[!UICONTROL 毎日]**
* **[!UICONTROL 毎週]**
* **[!UICONTROL 1 回]**

![](assets/ncs_cleanup_scheduler.png)

>[!IMPORTANT]
>
>**[!UICONTROL データベースのクリーンアップ]** ワークフローをスケジューラーで定義した日時に開始するには、ワークフローエンジン (wfserver) を起動する必要があります。 そうでない場合、データベースのクレンジングは次回ワークフローエンジンが起動されるまでは実行されません。

### デプロイメントウィザード {#deployment-wizard}

**[!UICONTROL ツール/詳細]** メニューからアクセスできる **[!UICONTROL デプロイウィザード]** を使用して、データの保存期間を設定できます。 値は日数で表されます。 これらの値を変更しない場合、ワークフローはデフォルト値を使用します。

![](assets/ncs_cleanup_deployment-wizard.png)

**[!UICONTROL データのパージ]** ウィンドウのフィールドは、次のオプションと一致します。 これらは、**[!UICONTROL データベースクリーンアップ]** ワークフローで実行されるタスクの一部で使用されます。

* 統合されたトラッキング：**NmsCleanup_TrackingStatPurgeDelay**（[ トラッキングログのクリーンアップ ](#cleanup-of-tracking-logs) を参照）
* 配信ログ：**NmsCleanup_BroadLogPurgeDelay**（[ 配信ログのクリーンアップ ](#cleanup-of-delivery-logs) を参照）
* トラッキングログ：**NmsCleanup_TrackingLogPurgeDelay**（[ トラッキングログのクリーンアップ ](#cleanup-of-tracking-logs) を参照）
* 削除された配信：**NmsCleanup_RecycledDeliveryPurgeDelay**（[ 削除またはリサイクルする配信のクリーンアップ ](#cleanup-of-deliveries-to-be-deleted-or-recycled) を参照）
* 却下をインポート：**NmsCleanup_RejectsPurgeDelay**（[ 読み込みによって生成された却下のクリーンアップ ](#cleanup-of-rejects-generated-by-imports-) を参照）
* 訪問者プロファイル：**NmsCleanup_VisitorPurgeDelay**（[ 訪問者のクリーンアップ ](#cleanup-of-visitors) を参照）
* オファーの提案：**NmsCleanup_PropositionPurgeDelay**（[ 提案のクリーンアップ ](#cleanup-of-propositions) を参照）

   >[!NOTE]
   >
   >**[!UICONTROL オファーの提案]** フィールドは、**インタラクション** モジュールがインストールされている場合にのみ使用できます。

* イベント：**NmsCleanup_EventPurgeDelay**（[ 期限切れのイベントのクレンジング ](#cleansing-expired-events) を参照）
* アーカイブしたイベント：**NmsCleanup_EventHistoPurgeDelay**（[ 期限切れのイベントのクレンジング ](#cleansing-expired-events) を参照）

   >[!NOTE]
   >
   >「**[!UICONTROL イベント]**」および「**[!UICONTROL アーカイブされたイベント]**」フィールドは、**Message Center** モジュールがインストールされている場合にのみ使用できます。

* 監査記録：**XtkCleanup_AuditTrailPurgeDelay**（[ 監査記録のクリーンアップ ](#cleanup-of-audit-trail) を参照）

**[!UICONTROL データベースクリーンアップ]** ワークフローで実行されるすべてのタスクについて、次の節で説明します。

## データベースクリーンアップワークフローによって実行されるタスク {#tasks-carried-out-by-the-database-cleanup-workflow}

ワークフロースケジューラーで定義された日時（[ スケジューラー ](#the-scheduler) を参照）に、ワークフローエンジンがデータベースのクリーンアッププロセスを開始します。 データベースクリーンアップは、データベースに接続し、以下に示す順序でタスクを実行します。

>[!IMPORTANT]
>
>これらのタスクの 1 つが失敗した場合、次のタスクは実行されません。\
>**LIMIT** 属性を持つ SQL クエリは、すべての情報が処理されるまで繰り返し実行されます。

>[!NOTE]
>
>以下の節では、データベースクリーンアップワークフローで実行されるタスクについて説明します。これらのタスクは、SQL 言語に精通したデータベース管理者やユーザー向けに用意されています。

### クリーンアップを削除するリスト {#lists-to-delete-cleanup}

**[!UICONTROL データベースクリーンアップ]** ワークフローで最初に実行されたタスクは、**deleteStatus !=** NmsGroup **の 0** 属性。 これらのグループにリンクされ、他のテーブルに存在するレコードも削除されます。

1. 削除するリストは、次の SQL クエリを使用して復元されます。

   ```
   SELECT iGroupId, sLabel, iType FROM NmsGroup WHERE iDeleteStatus <> 0 OR tsExpirationDate <= GetDate() 
   ```

1. 各リストは、他のテーブルへのリンクを複数持ちます。 次のクエリを使用して、これらのリンクがすべて一括削除されます。

   ```
   DELETE FROM $(relatedTable) WHERE iGroupId=$(l) IN (SELECT iGroupId FROM $(relatedTable) WHERE iGroupId=$(l) LIMIT 5000) 
   ```

   ここで、 **$(relatedTable)** は **NmsGroup** に関連するテーブルで、 **$(l)** はリストの識別子です。

1. リストが「リスト」タイプのリストの場合、関連付けられたテーブルは次のクエリを使用して削除されます。

   ```
   DROP TABLE grp$(l)
   ```

1. 操作で回復された **選択** タイプリストは、次のクエリを使用して削除されます。

   ```
   DELETE FROM NmsGroup WHERE iGroupId=$(l) 
   ```

   ここで、**$(l)** はリスト識別子です。

### 削除またはリサイクルする配信のクリーンアップ {#cleanup-of-deliveries-to-be-deleted-or-recycled}

このタスクでは、削除またはリサイクルするすべての配信を削除します。

1. **[!UICONTROL データベースクリーンアップ]** ワークフローは、**deleteStatus** フィールドの値が **[!UICONTROL はい]** または **[!UICONTROL リサイクル]** で、削除日が **[!UICONTROL 削除された配信]**（**デプロイウィザードの nmsCleanup_RecycledDeliveryPurgeDelay**）フィールド。 詳しくは、[ デプロイウィザード ](#deployment-wizard) を参照してください。 この期間は、現在のサーバーの日付に基づいて計算されます。
1. タスクでは、ミッドソーシングサーバーごとに、削除する配信のリストを選択します。
1. **[!UICONTROL データベースクリーンアップ]** ワークフローは、配信ログ、添付ファイル、ミラーページ情報、およびその他すべての関連データを削除します。
1. 配信を適切に削除する前に、ワークフローは次のテーブルからリンクされた情報を削除します。

   * 配信の除外テーブル (**NmsDlvExclusion**) では、次のクエリが使用されます。

      ```
      DELETE FROM NmsDlvExclusion WHERE iDeliveryId=$(l)
      ```

      **$(l)** は配信の識別子です。

   * クーポンテーブル (**NmsCouponValue**) では、次のクエリが使用されます（一括削除を含む）。

      ```
      DELETE FROM NmsCouponValue WHERE iMessageId IN (SELECT iMessageId FROM NmsCouponValue WHERE EXISTS (SELECT B.iBroadLogId FROM $(BroadLogTableName) B WHERE B.iDeliveryId = $(l) AND B.iBroadLogId = iMessageId ) LIMIT 5000)
      ```

      **$(l)** は配信の識別子です。

   * 配信ログテーブル (**NmsBroadlogXxx**) では、大量削除は 20,000 件のレコードのバッチで実行されます。
   * オファーの提案テーブル (**NmsPropositionXxx**) では、大量削除は 20,000 件のレコードのバッチで実行されます。
   * 追跡ログテーブル (**NmsTrackinglogXxx**) では、大量の削除が 20,000 件のレコードのバッチで実行されます。
   * 配信フラグメントテーブル (**NmsDeliveryPart**) では、500,000 件のレコードのバッチで大量削除が実行されます。 この表には、配信される残りのメッセージに関するパーソナライゼーション情報が含まれます。
   * ミラーページデータフラグメントテーブル (**NmsMirrorPageInfo**) では、期限切れの配信部品と、完了または取り消された配信部品に対して、20,000 件のレコードのバッチで大量削除が実行されます。 この表には、ミラーページの生成に使用されるすべてのメッセージに関するパーソナライゼーション情報が含まれます。
   * ミラーページ検索テーブル (**NmsMirrorPageSearch**) では、20,000 件のレコードのバッチで大量削除が実行されます。 このテーブルは、**NmsMirrorPageInfo** テーブルに格納されたパーソナライゼーション情報へのアクセスを提供する検索インデックスです。
   * バッチ処理ログテーブル (**XtkJobLog**) では、20,000 件のレコードのバッチで大量削除が実行されます。 このテーブルには、削除する配信のログが含まれています。
   * 配信 URL トラッキングテーブル (**NmsTrackingUrl**) では、次のクエリが使用されます。

      ```
      DELETE FROM NmsTrackingUrl WHERE iDeliveryId=$(l)
      ```

      **$(l)** は配信の識別子です。

      このテーブルには、削除される配信の URL が含まれ、その URL のトラッキングが有効になっています。

1. 配信が配信テーブル (**NmsDelivery**) から削除されます。

   ```
   DELETE FROM NmsDelivery WHERE iDeliveryId = $(l)
   ```

   **$(l)** は配信の識別子です。

#### ミッドソーシングを使用した配信 {#deliveries-using-mid-sourcing}

**[!UICONTROL データベースのクリーンアップ]** ワークフローは、ミッドソーシングサーバー上の配信も削除します。

1. これをおこなうには、ワークフローで、（ステータスに基づいて）各配信が非アクティブであることを確認します。 アクティブな配信は、削除前に停止されます。 チェックは、次のクエリを実行して実行します。

   ```
   SELECT iState FROM NmsDelivery WHERE iDeliveryId = $(l) AND iState <> 100;
   ```

   **$(l)** は配信の識別子です。

1. ステータスの値が **[!UICONTROL 開始待ち]** 、 **[!UICONTROL 進行中]** 、 **[!UICONTROL 回復待ち]** 、 **[!UICONTROL 回復中]** 、 **[!UICONTROL 一時停止要求]** 、 **[!UICONTROL 進行中]** の一時停止または **[!UICONTROL 一時停止]**（値 51、55、61、62、71、72、75）、配信が停止し、タスクがリンクされた情報を削除します。

### 期限切れの配信のクリーンアップ {#cleanup-of-expired-deliveries}

有効期間が過ぎた配信を停止します。

1. **[!UICONTROL データベースのクリーンアップ]** ワークフローは、期限切れの配信のリストを作成します。 このリストには、ステータスが **[!UICONTROL 完了]** 以外のすべての期限切れの配信と、処理されていないメッセージが 10,000 件を超える最近停止された配信が含まれます。 次のクエリが使用されます。

   ```
   SELECT iDeliveryId, iState FROM NmsDelivery WHERE iDeleteStatus=0 AND iIsModel=0 AND iDeliveryMode=1 AND ( (iState >= 51 AND iState < 85 AND tsValidity IS NOT NULL AND tsValidity < $(currentDate) ) OR (iState = 85 AND DateMinusDays(15) < tsLastModified AND iToDeliver - iProcessed >= 10000 ))
   ```

   **配信モード 1** が **[!UICONTROL 一括配信]** モードに一致し、**状態 51** が **[!UICONTROL 開始保留]** 状態に一致し、**状態 85** が **[!UICONTROL 停止]** 状態に一致し、配信サーバーで一括更新された配信ログの最大数が 10,000 に等しい。

1. 次に、ミッドソーシングを使用する最近期限切れの配信のリストがワークフローに含まれます。 ミッドソーシングサーバー経由で配信ログをまだ復元していない配信は除外されます。

   次のクエリが使用されます。

   ```
   SELECT iDeliveryId, tsValidity, iMidRemoteId, mData FROM NmsDelivery WHERE (iDeliveryMode = 4 AND (iState = 85 OR iState = 95) AND tsValidity IS NOT NULL AND (tsValidity < SubDays(GetDate() , 15) OR tsValidity < $(DateOfLastLogPullUp)) AND tsLastModified > SubDays(GetDate() , 15))
   ```

1. 次のクエリは、日付で配信をフィルタリングするために、外部アカウントがアクティブかどうかを検出するために使用します。

   ```
   SELECT iExtAccountId FROM NmsExtAccount WHERE iActive<>0 AND sName=$(providerName)
   ```

1. 期限切れの配信のリストで、ステータスが **[!UICONTROL 保留]** 、 **[!UICONTROL 配信がキャンセル]** 、このリスト内のすべての配信が **[!UICONTROL 完了]** に切り替わります。

   次のクエリが使用されます。

   ```
   UPDATE $(BroadLogTableName) SET tsLastModified=$(curdate), iStatus=7, iMsgId=$(bl) WHERE iDeliveryId=$(dl) AND iStatus=6
   ```

   **$(curdate)** はデータベースサーバーの現在の日付、 **$(bl)** は配信ログメッセージの識別子、 **$(dl)** は配信識別子、 **配信ステータス 6** は **[!UICONTROL 保留]** ステータスと **配信ステータス 7** は、「**[!UICONTROL 配信がキャンセルされました]**」のステータスに一致します。

   ```
   UPDATE NmsDelivery SET iState = 95, tsLastModified = $(curdate), tsBroadEnd = tsValidity WHERE iDeliveryId = $(dl)
   ```

   **配信状態 95** は **[!UICONTROL 完了]** ステータスと一致し、 **$(dl)** は配信の識別子です。

1. 古い配信のすべてのフラグメント (**deliveryParts**) が削除され、進行中の通知配信の古いフラグメントがすべて削除されます。 一括削除は、両方のタスクに使用されます。

   次のクエリが使用されます。

   ```
   DELETE FROM NmsDeliveryPart WHERE iDeliveryPartId IN (SELECT iDeliveryPartId FROM NmsDeliveryPart WHERE iDeliveryId IN (SELECT iDeliveryId FROM NmsDelivery WHERE iState=95 OR iState=85) LIMIT 5000)
   ```

   ```
   DELETE FROM NmsDeliveryPart WHERE iDeliveryPartId IN (SELECT iDeliveryPartId FROM NmsDeliveryPart WHERE tsValidity < $(curDate) LIMIT 500000)
   ```

   **配信状態 95** は **[!UICONTROL 完了]** 状態と一致し、**配信状態 85** は **[!UICONTROL 停止]** 状態と一致し、**$(curDate)** は現在のサーバー日付です。

### ミラーページのクリーンアップ {#cleanup-of-mirror-pages}

このタスクでは、配信で使用された Web リソース（ミラーページ）が削除されます。

1. まず、パージされる配信のリストは、次のクエリを使用して復元します。

   ```
   SELECT iDeliveryId, iNeedMirrorPage FROM NmsDelivery WHERE iWebResPurged = 0 AND tsWebValidity IS NOT NULL AND tsWebValidity < $(curdate)"
   ```

   ここで、**$(curDate)** は現在のサーバーの日付です。

1. 必要に応じて、以前に復元した配信の識別子を使用して、 **NmsMirrorPageInfo** テーブルがパージされます。 一括削除は、次のクエリーの生成に使用されます。

   ```
   DELETE FROM NmsMirrorPageInfo WHERE iMirrorPageInfoId IN (SELECT iMirrorPageInfoId FROM NmsMirrorPageInfo WHERE iDeliveryId = $(dl)) LIMIT 5000)
   ```

   ```
   DELETE FROM NmsMirrorPageSearch WHERE iMessageId IN (SELECT iMessageId FROM NmsMirrorPageSearch WHERE iDeliveryId = $(dl)) LIMIT 5000)
   ```

   **$(dl)** は配信の識別子です。

1. 次に、エントリが配信ログに追加されます。
1. パージされた配信は識別され、後で再処理する必要がなくなります。 次のクエリが実行されます。

   ```
   UPDATE NmsDelivery SET iWebResPurged = 1 WHERE iDeliveryId IN ($(strIn))
   ```

   **$(strIn)** は配信識別子のリストです。

### 作業用テーブルのクリーンアップ {#cleanup-of-work-tables}

このタスクは、ステータスが **[!UICONTROL 編集中]** 、 **[!UICONTROL 停止]** または **[!UICONTROL 削除]** の配信に一致するすべての作業用テーブルをデータベースから削除します。

1. 名前が **wkDlv_** で始まるテーブルのリストは、まず次のクエリ (postgresql) を使用して復元されます。

   ```
   SELECT relname FROM pg_class WHERE relname LIKE Lower('wkDlv_') ESCAPE E'\\' AND relkind IN ('r','v') AND pg_get_userbyid(relowner)<>'postgres'
   ```

1. その後、進行中のワークフローで使用されるテーブルは除外されます。 これをおこなうには、進行中の配信のリストを、次のクエリを使用して復元します。

   ```
   SELECT iDeliveryId FROM NmsDelivery WHERE iDeliveryId<>0 AND iDeleteStatus=0 AND iState NOT IN (0,85,100);
   ```

   ここで、0 は **[!UICONTROL 編集中]** の配信ステータスに一致する値で、85 は **[!UICONTROL 停止]** ステータスに一致し、100 は **[!UICONTROL 削除]** ステータスに一致します。

1. 使用されなくなったテーブルは、次のクエリを使用して削除されます。

   ```
   DROP TABLE wkDlv_15487_1;
   ```

### インポートによって生成された却下のクリーンアップ {#cleanup-of-rejects-generated-by-imports-}

この手順では、インポート中にすべてのデータが処理されなかったレコードを削除できます。

1. 一括削除は、次のクエリを使用して **XtkReject** テーブルに対して実行されます。

   ```
   DELETE FROM XtkReject WHERE iRejectId IN (SELECT iRejectId FROM XtkReject WHERE tsLog < $(curDate)) LIMIT $(l))
   ```

   **$(curDate)** は、**NmsCleanup_RejectsPurgeDelay** オプションに定義した期間を差し引いた現在のサーバーの日付です（[Deployment wizard](#deployment-wizard) を参照）。**$(l)** は、最大レコード数です削除されました。

1. すべてのオーファン却下は、次のクエリを使用して削除されます。

   ```
   DELETE FROM XtkReject WHERE iJobId NOT IN (SELECT iJobId FROM XtkJob)
   ```

### ワークフローインスタンスのクリーンアップ {#cleanup-of-workflow-instances}

このタスクは、識別子 (**lWorkflowId**) と履歴 (**lHistory**) を使用して、各ワークフローインスタンスを削除します。 作業用テーブルのクリーンアップタスクを再実行することで、非アクティブなテーブルを削除します。 また、削除されたワークフローの孤立した作業用テーブル（wkf%と wkfhisto%）もすべて削除されます。

>[!NOTE]
>
>履歴のパージ頻度は、「**History in days**」フィールド（デフォルト値は 30 日）で各ワークフローに対して指定します。 このフィールドは、ワークフロープロパティの「**実行**」タブにあります。 詳しくは、[この節](../../workflow/using/workflow-properties.md#execution)を参照してください。

1. 削除するワークフローのリストを復元するには、次のクエリを使用します。

   ```
   SELECT iWorkflowId, iHistory FROM XtkWorkflow WHERE iWorkflowId<>0
   ```

1. このクエリは、次のクエリを使用して、リンクされたすべてのログ、完了したタスクおよび完了したイベントを削除するために使用されるワークフローのリストを生成します。

   ```
   DELETE FROM XtkWorkflowLog WHERE iWorkflowId=$(lworkflow) AND tsLog < DateMinusDays($(lhistory))
   ```

   ```
   DELETE FROM XtkWorkflowTask WHERE iWorkflowId=$(lworkflow) AND iStatus<>0 AND tsCompletion < DateMinusDays($(lhistory)) 
   ```

   ```
   DELETE FROM XtkWorkflowEvent WHERE iWorkflowId=$(l) AND iStatus>2 AND tsProcessing < DateMinusDays($(lHistory))
   ```

   ここで、 **$(lworkflow)** はワークフローの識別子、 **$(lhistory)** は履歴の識別子です。

1. 未使用のテーブルはすべて削除されます。 この目的のために、**wkf%** タイプのマスクを使用して、次のクエリ (postgresql) を使用して、すべてのテーブルを収集します。

   ```
   SELECT relname FROM pg_class WHERE relname LIKE Lower('wkf%') ESCAPE E'\\' AND relkind IN ('r','v') AND pg_get_userbyid(relowner)<>'postgres'
   ```

1. 保留中のワークフローインスタンスで使用されるすべてのテーブルが除外されます。 アクティブなワークフローのリストは、次のクエリを使用して復元されます。

   ```
   SELECT iWorkflowId FROM XtkWorkflow WHERE iWorkflowId<>0 AND iState<>20
   ```

1. 次に、各ワークフロー識別子が復元され、進行中のワークフローで使用されるテーブルの名前が確認されます。 これらの名前は、以前に復元したテーブルのリストから除外されます。
1. 「増分処理クエリ」タイプのアクティビティ履歴テーブルは、次のクエリを使用して除外されます。

   ```
   SELECT relname FROM pg_class WHERE relname LIKE Lower('wkfhisto%') ESCAPE E'\\' AND relkind IN ('r','v') AND pg_get_userbyid(relowner)<>'postgres'
   ```

   ```
   SELECT iWorkflowId FROM XtkWorkflow WHERE iWorkflowId IN ($(strCondition))
   ```

   ここで、**$(strcondition)** は、**wkfhisto%** マスクに一致するテーブルのリストです。

1. 残りのテーブルは、次のクエリを使用して削除されます。

   ```
   DROP TABLE wkf15487_12;
   ```

### ワークフローログインのクリーンアップ {#cleanup-of-workflow-logins}

このタスクでは、次のクエリを使用してワークフローログインを削除します。

```
DELETE FROM XtkWorkflowLogin WHERE iWorkflowId NOT IN (SELECT iWorkflowId FROM XtkWorkflow)
```

### 孤立した作業用テーブルのクリーンアップ {#cleanup-of-orphan-work-tables}

このタスクは、グループにリンクされた孤立した作業用テーブルを削除します。 **NmsGroup** テーブルには、クレンジングするグループ（0 とは異なるタイプ）が格納されます。 テーブル名のプレフィックスは **grp** です。 クレンジングするグループを識別するには、次のクエリを使用します。

```
SELECT iGroupId FROM NmsGroup WHERE iType>0"
```

### 訪問者のクリーンアップ {#cleanup-of-visitors}

このタスクでは、一括削除を使用して訪問者テーブルから古いレコードを削除します。 古い記録は、最後の変更がデプロイウィザードで定義された保存期間よりも早いものです（[ デプロイウィザード ](#deployment-wizard) を参照）。 次のクエリが使用されます。

```
DELETE FROM NmsVisitor WHERE iVisitorId IN (SELECT iVisitorId FROM NmsVisitor WHERE iRecipientId = 0 AND tsLastModified < AddDays(GetDate(), -30) AND iOrigin = 0 LIMIT 20000)
```

ここで、**$(tsDate)** は現在のサーバーの日付です。この日付から、**NmsCleanup_VisitorPurgeDelay** オプションに定義した期間を引きます。

### NPAI のクリーンアップ {#cleanup-of-npai}

このタスクを実行すると、有効なアドレスと一致するレコードを **NmsAddress** テーブルから削除できます。 一括削除の実行には、次のクエリが使用されます。

```
DELETE FROM NmsAddress WHERE iAddressId IN (SELECT iAddressId FROM NmsAddress WHERE iStatus=2 AND tsLastModified < $(tsDate1) AND tsLastModified >= $(tsDate2) LIMIT 5000)
```

**ステータス 2** は **[!UICONTROL 有効な]** ステータスに一致し、**$(tsDate1)** は現在のサーバーの日付に一致します。**$(tsDate2)** は **NmsCleanup_LastCleanup** オプションに一致します。

### 購読のクリーンアップ {#cleanup-of-subscriptions-}

このタスクは、一括削除を使用して、ユーザーが **NmsSubscription** テーブルから削除したすべての購読を削除します。 次のクエリが使用されます。

```
DELETE FROM NmsSubscription WHERE iDeleteStatus <>0
```

### トラッキングログのクリーンアップ {#cleanup-of-tracking-logs}

このタスクは、トラッキングおよび Web トラッキングログテーブルから古いレコードを削除します。 古いレコードは、デプロイウィザードで定義した保存期間より前のものです（[ デプロイウィザード ](#deployment-wizard) を参照）。

1. まず、次のクエリを使用して、トラッキングログテーブルのリストを復元します。

   ```
   SELECT distinct(sTrackingLogSchema) FROM NmsDeliveryMapping WHERE sTrackingLogSchema IS NOT NULL;
   ```

1. 一括削除は、以前に復元したテーブルのリスト内のすべてのテーブルをパージする場合に使用します。 次のクエリが使用されます。

   ```
   DELETE FROM NmsTrackingLogRcp WHERE iTrackingLogId IN (SELECT iTrackingLogId FROM NmsTrackingLogRcp WHERE tsLog < $(tsDate) LIMIT 5000) 
   ```

   ここで、**$(tsDate)** は、**NmsCleanup_TrackingLogPurgeDelay** オプションに定義した期間を差し引いた現在のサーバーの日付です。

1. トラッキング統計テーブルは、一括削除を使用してパージされます。 次のクエリが使用されます。

   ```
   DELETE FROM NmsTrackingStats WHERE iTrackingStatsId IN (SELECT iTrackingStatsId FROM NmsTrackingStats WHERE tsStart < $(tsDate) LIMIT 5000) 
   ```

   ここで、**$(tsDate)** は、**NmsCleanup_TrackingStatPurgeDelay** オプションに定義した期間を差し引いた現在のサーバーの日付です。

### 配信ログのクリーンアップ {#cleanup-of-delivery-logs}

このタスクでは、様々なテーブルに保存されている配信ログをパージできます。

1. この目的で、配信ログスキーマのリストは、次のクエリを使用して復元します。

   ```
   SELECT distinct(sBroadLogSchema) FROM NmsDeliveryMapping WHERE sBroadLogSchema IS NOT NULL UNION SELECT distinct(sBroadLogExclSchema) FROM NmsDeliveryMapping WHERE sBroadLogExclSchema IS NOT NULL
   ```

1. ミッドソーシングを使用する場合、**NmsBroadLogMid** テーブルは配信マッピングで参照されません。 **nms:broadLogMid** スキーマが、前のクエリで復元したリストに追加されます。
1. 次に、**データベースのクリーンアップ** ワークフローは、以前に復元したテーブルから古いデータを削除します。 次のクエリが使用されます。

   ```
   DELETE FROM $(tableName) WHERE iBroadLogId IN (SELECT iBroadLogId FROM $(tableName) WHERE tsLastModified < $(option) LIMIT 5000) 
   ```

   **$(tableName)** はスキーマのリスト内の各テーブルの名前で、 **$(option)** は **NmsCleanup_BroadLogPurgeDelay** オプション用に定義された日付です（[ デプロイウィザード ](#deployment-wizard) を参照）。

1. 最後に、**NmsProviderMsgId** テーブルが存在するかどうかを確認します。 その場合、古いデータはすべて次のクエリを使用して削除されます。

   ```
   DELETE FROM NmsProviderMsgId WHERE iBroadLogId IN (SELECT iBroadLogId FROM NmsProviderMsgId WHERE tsCreated < $(option) LIMIT 5000)
   ```

   **$(option)** は、**NmsCleanup_BroadLogPurgeDelay** オプションに定義した日付と一致します（[ デプロイウィザード ](#deployment-wizard) を参照）。

### NmsEmailErrorStat テーブルのクリーンアップ {#cleanup-of-the-nmsemailerrorstat-table-}

このタスクは、**NmsEmailErrorStat** テーブルをクレンジングします。 メインプログラム (**coalesceErrors**) は、次の 2 つの日付を定義します。

* **開始日**:NmsLastErrorStatCoalesce オプションまたはテー **** ブル内の最新の日付に一致する次のプロセスの日付。
* **終了日**:現在のサーバーの日付。

開始日が終了日以上の場合、処理はおこなわれません。 この場合、 **coalesceUpToDate** メッセージが表示されます。

開始日が終了日より前の場合は、**NmsEmailErrorStat** テーブルがクレンジングされます。

**NmsEmailErrorStat** テーブルの開始日と終了日の間のエラーの合計数は、次のクエリを使用して復元します。

```
"SELECT COUNT(*) FROM NmsEmailErrorStat WHERE tsDate>= $(start) AND tsDate< $(end)"
```

ここで、 **$end** と **$start** は、前に定義した開始日と終了日です。

合計が 0 より大きい場合：

1. 特定のしきい値（20 に等しい）を超えるエラーのみを保持するために、次のクエリが実行されます。

   ```
   "SELECT iMXIP, iPublicId, SUM(iTotalConnections), SUM(iTotalErrors), SUM(iMessageErrors), SUM(iAbortedConnections), SUM(iFailedConnections), SUM(iRefusedConnections), SUM(iTimeoutConnections) FROM NmsEmailErrorStat WHERE tsDate>=$(start ) AND tsDate<$(end ) GROUP BY iMXIP, iPublicId HAVING SUM(iTotalErrors) >= 20"
   ```

1. **coalescingErrors** メッセージが表示されます。
1. 開始日と終了日の間に発生したすべてのエラーを削除する新しい接続が作成されます。 次のクエリが使用されます。

   ```
   "DELETE FROM NmsEmailErrorStat WHERE tsDate>=$(start) AND tsDate<$(end)"
   ```

1. 各エラーは、次のクエリを使用して **NmsEmailErrorStat** テーブルに保存されます。

   ```
   "INSERT INTO NmsEmailErrorStat(iMXIP, iPublicId, tsDate, iTotalConnections, iTotalErrors, iTimeoutConnections, iRefusedConnections, iAbortedConnections, iFailedConnections, iMessageErrors) VALUES($(lmxip ), $(lpublicId ), $(tsstart ), $(lconnections ), $(lconnectionErrors ),$(ltimeoutConnections ), $(lrefusedConnections ), $(labortedConnections ), $(lfailedConnections ), $(lmessageErrors))"
   ```

   各変数は、前のクエリで取得した値と一致します。

1. **start** 変数が更新され、前のプロセスの値でループが終了します。

ループとタスクが停止します。

クリーンアップは、**NmsEmailError** および **cleanupNmsMxDomain** テーブルで実行されます。

### NmsEmailError テーブルのクリーンアップ {#cleanup-of-the-nmsemailerror-table-}

次のクエリが使用されます。

```
DELETE FROM NmsEmailError WHERE iMXIP NOT IN (SELECT DISTINCT iMXIP FROM NmsEmailErrorStat)
```

このクエリは、**NmsEmailErrorStat** 内のリンクされたレコードを持たない行をすべて **NmsEmailError** テーブルから削除します。

### NmsMxDomain テーブルのクリーンアップ {#cleanup-of-the-nmsmxdomain-table-}

次のクエリが使用されます。

```
DELETE FROM NmsMxDomain WHERE iMXIP NOT IN (SELECT DISTINCT iMXIP FROM NmsEmailErrorStat)
```

このクエリは、**NmsEmailErrorStat** テーブル内のリンクされたレコードを持たない行をすべて、**NmsMxDomain** テーブルから削除します。

### 提案のクリーンアップ {#cleanup-of-propositions}

**Interaction** モジュールがインストールされている場合、このタスクが実行され、**NmsPropositionXxx** テーブルがパージされます。

提案テーブルのリストが復元され、次のクエリを使用して、各提案テーブルに対して一括削除が実行されます。

```
DELETE FROM NmsPropositionXxx WHERE iPropositionId IN (SELECT iPropositionId FROM NmsPropositionXxx WHERE tsLastModified < $(option) LIMIT 5000) 
```

**$(option)** は、**NmsCleanup_PropositionPurgeDelay** オプション用に定義された日付です（[ デプロイウィザード ](#deployment-wizard) を参照）。

### シミュレーションテーブルのクリーンアップ {#cleanup-of-simulation-tables}

このタスクは、孤立したシミュレーションテーブル（オファーのシミュレーションや配信のシミュレーションにリンクされなくなったテーブル）を消去します。

1. クリーンアップが必要なシミュレーションのリストを復元するには、次のクエリを使用します。

   ```
   SELECT iSimulationId FROM NmsSimulation WHERE iSimulationId<>0
   ```

1. 削除するテーブルの名前は、 **wkSimu_** というプレフィックスに続くシミュレーションの識別子で構成されます ( 例：**wkSimu_456831_aggr**):

   ```
   DROP TABLE wkSimu_456831_aggr
   ```

### 監査記録のクリーンアップ {#cleanup-of-audit-trail}

次のクエリが使用されます。

```
DELETE FROM XtkAudit WHERE tsChanged < $(tsDate)
```

**$(tsDate)** は、現在のサーバーの日付です。この日付から、**XtkCleanup_AuditTrailPurgeDelay** オプションに定義した期間が差し引かれます。

### Nmsaddress のクリーンアップ {#cleanup-of-nmsaddress}

次のクエリが使用されます。

```
DELETE FROM NmsAddress WHERE iAddressId IN (SELECT iAddressId FROM NmsAddress WHERE iStatus=STATUS_QUARANTINE AND tsLastModified < $(NmsCleanup_AppSubscriptionRcpPurgeDelay + 5d) AND iType IN (MESSAGETYPE_IOS, MESSAGETYPE_ANDROID ) LIMIT 5000)
```

このクエリは、iOS と Android に関連するすべてのエントリを削除します。

### 統計の更新とストレージの最適化 {#statistics-update}

**XtkCleanup_NoStats** オプションを使用すると、クリーンアップワークフローのストレージ最適化手順の動作を制御できます。

**XtkCleanup_NoStats** オプションが存在しない場合、またはその値が 0 の場合は、PostgreSQL の詳細モード (VACUUM VERBOSE ANALYZE) でストレージの最適化が実行され、他のすべてのデータベースの統計が更新されます。 このコマンドが実行されていることを確認するには、PostgreSQL のログを確認します。 VACUUM は次の形式で行を出力します。`INFO: vacuuming "public.nmsactivecontact"` と ANALYZE は、次の形式で行を出力します。`INFO: analyzing "public.nmsactivecontact"`.

このオプションの値が 1 の場合、統計の更新はどのデータベースでも実行されません。 次のログ行がワークフローログに表示されます。`Option 'XtkCleanup_NoStats' is set to '1'`.

オプションの値が 2 の場合、PostgreSQL の詳細モード (ANALYZE VERBOSE) でストレージ分析が実行され、他のすべてのデータベースの統計情報が更新されます。 このコマンドが実行されていることを確認するには、PostgreSQL のログを確認します。 ANALYZE は、次の形式で行を出力します。`INFO: analyzing "public.nmsactivecontact"`.

### サブスクリプションクリーンアップ (NMAC) {#subscription-cleanup--nmac-}

このタスクは、削除されたサービスまたはモバイルアプリケーションに関連する購読をすべて削除します。

broadLog スキーマのリストを復元するには、次のクエリを使用します。

```
SELECT distinct(sBroadLogSchema) FROM NmsDeliveryMapping WHERE sBroadLogSchema IS NOT NULL
```

次に、このタスクは、**appSubscription** リンクにリンクされているテーブルの名前を復元し、これらのテーブルを削除します。

また、このクリーンアップワークフローでは、**NmsCleanup_AppSubscriptionRcpPurgeDelay** オプションで設定された時刻以降に更新されていない disabled = 1 のエントリをすべて削除します。

### セッション情報のクレンジング {#cleansing-session-information}

このタスクは、**sessionInfo** テーブルから情報をクレンジングします。次のクエリが使用されます。

```
 DELETE FROM XtkSessionInfo WHERE tsexpiration < $(curdate) 
```

### 有効期限切れのイベントのクレンジング {#cleansing-expired-events}

このタスクは、実行インスタンスで受信および保存されたイベントと、コントロールインスタンスでアーカイブされたイベントをクレンジングします。

### クレンジング反応 {#cleansing-reactions}

このタスクは、仮説自体が削除された反応（表 **NmsRemaMatchRcp**）をクレンジングします。
