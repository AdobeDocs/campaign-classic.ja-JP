---
product: campaign
title: データベースクリーンアップのワークフロー
description: 古いデータが自動的にクリーンアップされる仕組みを説明します
feature: Monitoring, Workflows
audience: production
content-type: reference
topic-tags: data-processing
exl-id: 75d3a0af-9a14-4083-b1da-2c1b22f57cbe
source-git-commit: 0ed70b3c57714ad6c3926181334f57ed3b409d98
workflow-type: tm+mt
source-wordcount: '2914'
ht-degree: 1%

---

# データベースクリーンアップのワークフロー{#database-cleanup-workflow}



## はじめに {#introduction}

**[!UICONTROL 管理／プロダクション／テクニカルワークフロー]**&#x200B;ノードからアクセスできる&#x200B;**[!UICONTROL データベースクリーンアップ]**&#x200B;ワークフローを使用すると、古いデータを削除して、データベースの急激な増加を回避できます。ワークフローは、ユーザーの操作なしで自動的にトリガーされます。

![ クリーンアップ ](assets/ncs_cleanup_workflow.png)

## 設定 {#configuration}

データベースのクリーンアップは、ワークフロースケジューラーとデプロイメントウィザードの 2 つのレベルで設定します。

### ワークフロースケジューラー {#the-scheduler}

>[!NOTE]
>
>スケジューラーについて詳しくは、[この節](../../workflow/using/scheduler.md)を参照してください。

デフォルトでは、**[!UICONTROL データベースクリーンアップ]** ワークフローは、毎日午前 4 時に開始するように設定されています。 スケジューラーを使用すると、ワークフローのトリガー頻度を変更できます。 次の頻度を使用できます。

* **[!UICONTROL 1 日に数回]**
* **[!UICONTROL 毎日]**
* **[!UICONTROL 毎週]**
* **[!UICONTROL 1 回]**

![ スケジューラー ](assets/ncs_cleanup_scheduler.png)

>[!IMPORTANT]
>
>**[!UICONTROL データベースクリーンアップ]** ワークフローを、スケジューラーで定義された日時に開始するには、ワークフローエンジン（wfserver）を開始する必要があります。

### 配置ウィザード {#deployment-assistant}

**[!UICONTROL ツール/詳細]** メニューからアクセスできる **[!UICONTROL デプロイメントウィザード]** を使用すると、データを保存する期間を設定できます。 値は日数で表します。 これらの値が変更されない場合、ワークフローではデフォルト値が使用されます。

![](assets/ncs_cleanup_deployment-wizard.png)

**[!UICONTROL データのパージ]** ウィンドウのフィールドは、次のオプションと一致します。 これらは、**[!UICONTROL データベースクリーンアップ]** ワークフローで実行される一部のタスクで使用されます。

* 統合されたトラッキング：**NmsCleanup_TrackingStatPurgeDelay** （[ トラッキングログのクリーンアップ ](#cleanup-of-tracking-logs) を参照）
* 配信ログ：**NmsCleanup_BroadLogPurgeDelay** （[ 配信ログのクリーンアップ ](#cleanup-of-delivery-logs) を参照）
* トラッキングログ：**NmsCleanup_TrackingLogPurgeDelay** （[ トラッキングログのクリーンアップ ](#cleanup-of-tracking-logs) を参照）
* 削除された配信：**NmsCleanup_RecycledDeliveryPurgeDelay** （[ 削除またはリサイクルされる配信のクリーンアップ ](#cleanup-of-deliveries-to-be-deleted-or-recycled) を参照）
* 却下を読み込み：**NmsCleanup_RejectsPurgeDelay** （[ 読み込みによって生成された却下のクリーンアップ ](#cleanup-of-rejects-generated-by-imports-) を参照）
* 訪問者プロファイル：**NmsCleanup_VisitorPurgeDelay** （[ 訪問者のクリーンアップ ](#cleanup-of-visitors) を参照）
* オファーの提案：**NmsCleanup_PropositionPurgeDelay** （[ 提案のクリーンアップ ](#cleanup-of-propositions) を参照）

  >[!NOTE]
  >
  >**[!UICONTROL オファーの提案]** フィールドは、**インタラクション** モジュールがインストールされている場合にのみ使用できます。

* イベント：**NmsCleanup_EventPurgeDelay** （[ 期限切れイベントのクレンジング ](#cleansing-expired-events) を参照）
* アーカイブしたイベント：**NmsCleanup_EventHistoPurgeDelay** （[ 期限切れのイベントのクレンジング ](#cleansing-expired-events) を参照）

  >[!NOTE]
  >
  >**[!UICONTROL イベント]** および **[!UICONTROL アーカイブしたイベント]** フィールドは、**Message Center** モジュールがインストールされている場合にのみ使用できます。

* 監査証跡：**XtkCleanup_AuditTrailPurgeDelay** （[ 監査証跡のクリーンアップ ](#cleanup-of-audit-trail) を参照）

**[!UICONTROL データベースクリーンアップ]** ワークフローで実行されるすべてのタスクについては、次の節で説明します。

## データベースクリーンアップワークフローで実行されるタスク {#tasks-carried-out-by-the-database-cleanup-workflow}

ワークフロースケジューラーで定義された日時（「[ スケジューラー ](#the-scheduler)」を参照）に、ワークフローエンジンはデータベースのクリーンアッププロセスを開始します。 データベースクリーンアップは、データベースに接続し、以下に示す順序でタスクを実行します。

>[!IMPORTANT]
>
>これらのタスクのいずれかが失敗した場合、次のタスクは実行されません。
>
>**LIMIT** 属性を持つ SQL クエリは、すべての情報が処理されるまで繰り返し実行されます。


### クリーンアップを削除するリスト {#lists-to-delete-cleanup}

**[!UICONTROL データベースクリーンアップ]** ワークフローによって実行された最初のタスクでは、**deleteStatus != 0** **NmsGroup** の属性。 これらのグループにリンクされ、他のテーブルに存在するレコードも削除されます。

1. 削除されるリストは、次の SQL クエリを使用して復元されます。

   ```sql
   SELECT iGroupId, sLabel, iType FROM NmsGroup WHERE iDeleteStatus <> 0 OR tsExpirationDate <= GetDate() 
   ```

1. 各リストには、他のテーブルへのリンクが複数あります。 これらのリンクはすべて、次のクエリを使用して一括で削除されます。

   ```sql
   DELETE FROM $(relatedTable) WHERE iGroupId=$(l) IN (SELECT iGroupId FROM $(relatedTable) WHERE iGroupId=$(l) LIMIT 5000) 
   ```

   ここで、`$(relatedTable)` は **NmsGroup** に関連するテーブルで、`$(l)` はリスト識別子です。

1. リストが「リスト」タイプのリストの場合、以下のクエリを使用して、関連テーブルが削除されます。

   ```sql
   DROP TABLE grp$(l)
   ```

1. 操作によって復元されたすべての **選択** タイプリストは、次のクエリを使用して削除されます。

   ```sql
   DELETE FROM NmsGroup WHERE iGroupId=$(l) 
   ```

   ここで、`$(l)` はリスト識別子です

### 削除またはリサイクルされる配信のクリーンアップ {#cleanup-of-deliveries-to-be-deleted-or-recycled}

このタスクにより、削除またはリサイクルされるすべての配信がパージされます。

1. **[!UICONTROL データベースクリーンアップ]** ワークフローは、「**deleteStatus**」フィールドの値が **[!UICONTROL Yes]** または **[!UICONTROL Recycled]** で、削除日がデプロイメントウィザードの「**[!UICONTROL 削除済み配信]** （**NmsCleanup_RecycledDeliveryPurgeDelay**）」フィールドで定義された期間より前のすべての配信を選択します。 詳しくは、[ デプロイメントウィザード ](#deployment-assistant) を参照してください。 この期間は、現在のサーバーの日付を基準に計算されます。
1. ミッドソーシングサーバーごとに、タスクが削除する配信のリストを選択します。
1. **[!UICONTROL データベースクリーンアップ]** ワークフローでは、配信ログ、添付ファイル、ミラーページ情報およびその他すべての関連データが削除されます。
1. 配信を削除する前に、リンクされている情報が次の表から削除されます。

   * 配信除外テーブル（**NmsDlvExclusion**）では、次のクエリが使用されます。

     ```sql
     DELETE FROM NmsDlvExclusion WHERE iDeliveryId=$(l)
     ```

     ここで、**$（l）** は配信の識別子です。

   * クーポンテーブル（**NmsCouponValue**）では、次のクエリが（一括削除で）使用されます。

     ```sql
     DELETE FROM NmsCouponValue WHERE iMessageId IN (SELECT iMessageId FROM NmsCouponValue WHERE EXISTS (SELECT B.iBroadLogId FROM $(BroadLogTableName) B WHERE B.iDeliveryId = $(l) AND B.iBroadLogId = iMessageId ) LIMIT 5000)
     ```

     ここで、`$(l)` は配信の識別子です。

   * 配信ログテーブル（**NmsBroadlogXxx**）では、20,000 件のレコードに対してバッチで一括削除が実行されます。
   * オファーの提案テーブル（**NmsPropositionXxx**）では、一括削除が 20,000 件のレコードに対してバッチで実行されます。
   * トラッキングログテーブル（**NmsTrackinglogXxx**）では、20,000 件のレコードに対してバッチで一括削除が実行されます。
   * 配信フラグメントテーブル（**NmsDeliveryPart**）では、500,000 件のレコードに対してバッチで一括削除が実行されます。 この表には、配信される残りのメッセージに関するパーソナライゼーション情報が含まれています。
   * ミラーページデータフラグメントテーブル（**NmsMirrorPageInfo**）では、期限切れの配信部分と完了またはキャンセルされた配信部分に対して、20,000 件のレコードに相当するバッチで一括削除が実行されます。 このテーブルには、ミラーページの生成に使用されるすべてのメッセージに関するパーソナライゼーション情報が含まれています。
   * ミラーページ検索テーブル（**NmsMirrorPageSearch**）では、20,000 件のレコードに対して一括削除が実行されます。 このテーブルは、**NmsMirrorPageInfo** テーブルに格納されているパーソナライゼーション情報へのアクセスを提供する検索インデックスです。
   * バッチ処理ログテーブル（**XtkJobLog**）では、20,000 件のレコードに対してバッチで一括削除が実行されます。 この表には、削除される配信のログが含まれています。
   * 配信 URL トラッキングテーブル（**NmsTrackingUrl**）では、次のクエリが使用されます。

     ```sql
     DELETE FROM NmsTrackingUrl WHERE iDeliveryId=$(l)
     ```

     ここで、`$(l)` は配信の識別子です。

     この表には、トラッキングを有効にするために削除する配信で見つかった URL が含まれています。

1. 配信が配信テーブルから削除されます（**NmsDelivery**）。

   ```sql
   DELETE FROM NmsDelivery WHERE iDeliveryId = $(l)
   ```

   ここで、`$(l)` は配信の識別子です。

#### ミッドソーシングを使用した配信 {#deliveries-using-mid-sourcing}

**[!UICONTROL データベースクリーンアップ]** ワークフローでも、ミッドソーシングサーバー上の配信が削除されます。

1. これを行うには、ワークフローは各配信が（ステータスに基づいて）非アクティブであることを確認します。 配信がアクティブな場合は、削除される前に停止されます。 チェックは、次のクエリを実行することで実行されます。

   ```sql
   SELECT iState FROM NmsDelivery WHERE iDeliveryId = $(l) AND iState <> 100;
   ```

   ここで、**$（l）** は配信の識別子です。

1. ステータスの値が **[!UICONTROL 開始保留中]**、**[!UICONTROL 処理中]**、**[!UICONTROL 回復保留中]**、**[!UICONTROL 回復処理中]**、**[!UICONTROL 一時停止リクエスト]**、**[!UICONTROL 一時停止中]**、または **[!UICONTROL 一時停止]** の場合（値 51、55、61、62、71、72、75）、配信が停止され、タスクによってリンク情報がパージされます。

### 期限切れ配信のクリーンアップ {#cleanup-of-expired-deliveries}

このタスクにより、有効期限が切れた配信が停止します。

1. **[!UICONTROL データベースクリーンアップ]** ワークフローは、有効期限が切れた配信のリストを作成します。 このリストには、ステータスが **[!UICONTROL 完了]** 以外の期限切れ配信と、10,000 件を超える未処理メッセージが発生し最近停止した配信が含まれます。 次のクエリが使用されます。

   ```sql
   SELECT iDeliveryId, iState FROM NmsDelivery WHERE iDeleteStatus=0 AND iIsModel=0 AND iDeliveryMode=1 AND ( (iState >= 51 AND iState < 85 AND tsValidity IS NOT NULL AND tsValidity < $(currentDate) ) OR (iState = 85 AND DateMinusDays(15) < tsLastModified AND iToDeliver - iProcessed >= 10000 ))
   ```

   `delivery mode 1` が **[!UICONTROL 一括配信]** モードと一致する場合、`state 51` が **[!UICONTROL 開始保留]** 状態と一致する場合、`state 85` が **[!UICONTROL 停止済み]** 状態と一致する場合、配信サーバー上で一括更新される配信ログの最大数は 10,000 件になります。

1. 次に、ワークフローには、ミッドソーシングを使用する、最近期限切れの配信のリストが含まれます。 ミッドソーシングサーバーから復元された配信ログがまだない配信は除外されます。

   次のクエリが使用されます。

   ```sql
   SELECT iDeliveryId, tsValidity, iMidRemoteId, mData FROM NmsDelivery WHERE (iDeliveryMode = 4 AND (iState = 85 OR iState = 95) AND tsValidity IS NOT NULL AND (tsValidity < SubDays(GetDate() , 15) OR tsValidity < $(DateOfLastLogPullUp)) AND tsLastModified > SubDays(GetDate() , 15))
   ```

1. 次のクエリは、日付で配信をフィルタリングするために、外部アカウントがまだアクティブかどうかを検出するために使用されます。

   ```sql
   SELECT iExtAccountId FROM NmsExtAccount WHERE iActive<>0 AND sName=$(providerName)
   ```

1. 期限切れ配信のリストで、ステータスが **[!UICONTROL 保留中]** の配信ログは、**[!UICONTROL 配信キャンセル]** に切り替わり、このリスト内のすべての配信は **[!UICONTROL 完了]** に切り替わります。

   次のクエリが使用されます。

   ```sql
   UPDATE $(BroadLogTableName) SET tsLastModified=$(curdate), iStatus=7, iMsgId=$(bl) WHERE iDeliveryId=$(dl) AND iStatus=6
   ```

   ここで、`$(curdate)` はデータベースサーバーの現在の日付で、`$(bl)` は配信ログメッセージの識別子、`$(dl)` は配信識別子で、**[!UICONTROL 保留中]** ステータス `delivery status 6` 一致し、`delivery status 7` は **[!UICONTROL 配信がキャンセルされました]** ステータスと一致します。

   ```sql
   UPDATE NmsDelivery SET iState = 95, tsLastModified = $(curdate), tsBroadEnd = tsValidity WHERE iDeliveryId = $(dl)
   ```

   `delivery state 95` は **[!UICONTROL 完了]** ステータスと一致し、`$(dl)` は配信の識別子です。

1. 古い配信のすべてのフラグメント（**deliveryParts**）が削除され、処理中の通知配信のすべての古いフラグメントが削除されます。 一括削除は、両方のタスクで使用します。

   次のクエリが使用されます。

   ```sql
   DELETE FROM NmsDeliveryPart WHERE iDeliveryPartId IN (SELECT iDeliveryPartId FROM NmsDeliveryPart WHERE iDeliveryId IN (SELECT iDeliveryId FROM NmsDelivery WHERE iState=95 OR iState=85) LIMIT 5000)
   ```

   ```sql
   DELETE FROM NmsDeliveryPart WHERE iDeliveryPartId IN (SELECT iDeliveryPartId FROM NmsDeliveryPart WHERE tsValidity < $(curDate) LIMIT 500000)
   ```

   `delivery state 95` は **[!UICONTROL 完了]** ステータスに一致し、`delivery state 85` は **[!UICONTROL 停止]** ステータスに一致し、`$(curDate)` は現在のサーバーの日付です。

### ミラーページのクリーンアップ {#cleanup-of-mirror-pages}

配信で使用される web リソース（ミラーページ）を削除します。

1. まず、パージ対象の配信のリストは、次のクエリを使用して復元されます。

   ```sql
   SELECT iDeliveryId, iNeedMirrorPage FROM NmsDelivery WHERE iWebResPurged = 0 AND tsWebValidity IS NOT NULL AND tsWebValidity < $(curdate)
   ```

   ここで、`$(curDate)` は現在のサーバーの日付です。

1. その後、必要に応じて、以前に復元した配信の識別子を使用して、**NmsMirrorPageInfo** テーブルがパージされます。 一括削除は、次のクエリの生成に使用されます。

   ```sql
   DELETE FROM NmsMirrorPageInfo WHERE iMirrorPageInfoId IN (SELECT iMirrorPageInfoId FROM NmsMirrorPageInfo WHERE iDeliveryId = $(dl)) LIMIT 5000
   ```

   ```sql
   DELETE FROM NmsMirrorPageSearch WHERE iMessageId IN (SELECT iMessageId FROM NmsMirrorPageSearch WHERE iDeliveryId = $(dl)) LIMIT 5000
   ```

   ここで、`$(dl)` は配信の識別子です。

1. 次に、エントリが配信ログに追加されます。
1. パージされた配信は識別されるので、後で再処理する必要がなくなります。 次のクエリが実行されます。

   ```sql
   UPDATE NmsDelivery SET iWebResPurged = 1 WHERE iDeliveryId IN ($(strIn))
   ```

   ここで、`$(strIn)` は配信識別子のリストです。

### 作業用テーブルのクリーンアップ {#cleanup-of-work-tables}

このタスクは、ステータスが **[!UICONTROL 編集中]**、**[!UICONTROL 停止中]** または **[!UICONTROL 削除済み]** の配信に一致するすべての作業用テーブルをデータベースから削除します。

1. **wkDlv_** で始まる名前を持つテーブルのリストは、まず次のクエリ （postgresql）で回復されます。

   ```sql
   SELECT relname FROM pg_class WHERE relname LIKE Lower('wkDlv_%') ESCAPE E'\\' AND relkind IN ('r','v') AND pg_get_userbyid(relowner)<>'postgres'
   ```

1. その後、処理中のワークフローで使用されるテーブルは除外されます。 これを行うには、次のクエリを使用して、進行中の配信のリストを復元します。

   ```sql
   SELECT iDeliveryId FROM NmsDelivery WHERE iDeliveryId<>0 AND iDeleteStatus=0 AND iState NOT IN (0,85,100);
   ```

   ここで、`0` は **[!UICONTROL 編集中]** 配信ステータスに一致する値、`85` は **[!UICONTROL 停止済み]** ステータスに一致する値、`100` は **[!UICONTROL 削除済み]** ステータスに一致する値です。

1. 使用されなくなったテーブルは、次のクエリを使用して削除されます。

   ```sql
   DROP TABLE wkDlv_15487_1;
   ```

### 読み込みによって生成された却下のクリーンアップ {#cleanup-of-rejects-generated-by-imports-}

この手順を使用すると、読み込み時にすべてのデータが処理されなかったレコードを削除できます。

1. 一括削除は、次のクエリを使用して **XtkReject** テーブルで実行されます。

   ```sql
   DELETE FROM XtkReject WHERE iRejectId IN (SELECT iRejectId FROM XtkReject WHERE tsLog < $(curDate)) LIMIT $(l)
   ```

   ここで、`$(curDate)` は、「**NmsCleanup_RejectsPurgeDelay**」オプションで定義した期間を差し引く現在のサーバーの日付（「[ デプロイメントウィザード ](#deployment-assistant)」を参照）で、`$(l)` は、一括削除されるレコードの最大数です。

1. すべての孤立した却下は、次のクエリを使用して削除されます。

   ```sql
   DELETE FROM XtkReject WHERE iJobId NOT IN (SELECT iJobId FROM XtkJob)
   ```

### ワークフローインスタンスのクリーンアップ {#cleanup-of-workflow-instances}

このタスクは、識別子（**lWorkflowId**）と履歴（**lHistory**）を使用して各ワークフローインスタンスをパージします。 ワークテーブルのクリーンアップタスクを再度実行して、非アクティブなテーブルを削除します。 このクリーンアップでは、削除されたワークフローの孤立したすべてのワークテーブル（wkf% および wkfhisto%）も削除されます。

>[!NOTE]
>
>履歴のパージ頻度は、「履歴（日数 **フィールドでワークフローごとに指定します** （デフォルト値は 30 日）。 このフィールドは、ワークフロープロパティの「**実行**」タブにあります。 詳しくは、[この節](../../workflow/using/workflow-properties.md#execution)を参照してください。

1. 削除するワークフローのリストを復元するには、次のクエリを使用します。

   ```sql
   SELECT iWorkflowId, iHistory FROM XtkWorkflow WHERE iWorkflowId<>0
   ```

1. このクエリは、次のクエリを使用して、すべてのリンクされたログ、完了したタスクおよび完了したイベントを削除するために使用されるワークフローのリストを生成します。

   ```sql
   DELETE FROM XtkWorkflowLog WHERE iWorkflowId=$(lworkflow) AND tsLog < DateMinusDays($(lhistory))
   ```

   ```sql
   DELETE FROM XtkWorkflowTask WHERE iWorkflowId=$(lworkflow) AND iStatus<>0 AND tsCompletion < DateMinusDays($(lhistory)) 
   ```

   ```sql
   DELETE FROM XtkWorkflowEvent WHERE iWorkflowId=$(l) AND iStatus>2 AND tsProcessing < DateMinusDays($(lHistory))
   ```

   ここで、`$(lworkflow)` はワークフローの識別子、`$(lhistory)` は履歴の識別子です。

1. 未使用のテーブルはすべて削除されます。 この目的のために、以下のクエリ（postgresql）を使用した **wkf%** 型のマスクによってすべてのテーブルが収集されます。

   ```sql
   SELECT relname FROM pg_class WHERE relname LIKE Lower('wkf%') ESCAPE E'\\' AND relkind IN ('r','v') AND pg_get_userbyid(relowner)<>'postgres'
   ```

1. これにより、保留中のワークフローインスタンスで使用されているすべてのテーブルが除外されます。 次のクエリを使用して、アクティブなワークフローのリストが復元されます。

   ```sql
   SELECT iWorkflowId FROM XtkWorkflow WHERE iWorkflowId<>0 AND iState<>20
   ```

1. 次に、各ワークフロー識別子が復元され、実行中のワークフローで使用されているテーブルの名前が検索されます。 これらの名前は、以前にリカバリしたテーブルのリストから除外されます。
1. 「増分処理クエリ」タイプのアクティビティ履歴テーブルは、次のクエリを使用して除外されます。

   ```sql
   SELECT relname FROM pg_class WHERE relname LIKE Lower('wkfhisto%') ESCAPE E'\\' AND relkind IN ('r','v') AND pg_get_userbyid(relowner)<>'postgres'
   ```

   ```sql
   SELECT iWorkflowId FROM XtkWorkflow WHERE iWorkflowId IN ($(strCondition))
   ```

   ここで、`$(strcondition)` は **wkfhito%** マスクに一致するテーブルのリストです。

1. 残りのテーブルは、次のクエリを使用して削除されます。

   ```sql
   DROP TABLE wkf15487_12;
   ```

### ワークフローログインのクリーンアップ {#cleanup-of-workflow-logins}

このタスクでは、次のクエリを使用してワークフローログインを削除します。

```sql
DELETE FROM XtkWorkflowLogin WHERE iWorkflowId NOT IN (SELECT iWorkflowId FROM XtkWorkflow)
```

### 孤立した作業用テーブルのクリーンアップ {#cleanup-of-orphan-work-tables}

グループにリンクされている孤立した作業用テーブルを削除します。 **NmsGroup** テーブルには、クレンジングするグループ（タイプが 0 とは異なる）が格納されます。 テーブル名のプレフィックスは **grp** です。 クレンジングするグループを識別するために、次のクエリを使用します。

```sql
SELECT iGroupId FROM NmsGroup WHERE iType>0"
```

### 訪問者のクリーンアップ {#cleanup-of-visitors}

このタスクは、一括削除を使用して訪問者テーブルから古いレコードを削除します。 古いレコードは、最後の変更が配置ウィザードで定義された保存期間より前のレコードです（[ 配置ウィザード ](#deployment-assistant) を参照）。 次のクエリが使用されます。

```sql
DELETE FROM NmsVisitor WHERE iVisitorId IN (SELECT iVisitorId FROM NmsVisitor WHERE iRecipientId = 0 AND tsLastModified < AddDays(GetDate(), -30) AND iOrigin = 0 LIMIT 20000)
```

ここで、`$(tsDate)` は、現在のサーバーの日付です。ここから、**NmsCleanup_VisitorPurgeDelay** オプションに対して定義された期間を減算します。

### NPAI のクリーンアップ {#cleanup-of-npai}

このタスクを使用すると、有効なアドレスに一致するレコードを **NmsAddress** テーブルから削除できます。 次のクエリを使用して、一括削除を実行します。

```sql
DELETE FROM NmsAddress WHERE iAddressId IN (SELECT iAddressId FROM NmsAddress WHERE iStatus=2 AND tsLastModified < $(tsDate1) AND tsLastModified >= $(tsDate2) LIMIT 5000)
```

`status 2` が **[!UICONTROL 有効]** ステータスと一致する場合、`$(tsDate1)` は現在のサーバーの日付で、`$(tsDate2)` は **NmsCleanup_LastCleanup** オプションと一致します。

### 購読のクリーンアップ {#cleanup-of-subscriptions-}

このタスクは、一括削除を使用して、ユーザーが **NmsSubscription** テーブルから削除したすべての購読をパージします。 次のクエリが使用されます。

```sql
DELETE FROM NmsSubscription WHERE iDeleteStatus <>0
```

### トラッキングログのクリーンアップ {#cleanup-of-tracking-logs}

このタスクは、トラッキングログテーブルと Web トラッキングログテーブルから古いレコードを削除します。 古いレコードは、配置ウィザードで定義された保存期間より前のレコードです（[ 配置ウィザード ](#deployment-assistant) を参照）。

1. まず、次のクエリを使用して、トラッキングログテーブルのリストを復元します。

   ```sql
   SELECT distinct(sTrackingLogSchema) FROM NmsDeliveryMapping WHERE sTrackingLogSchema IS NOT NULL;
   ```

1. 一括削除は、以前に復元したテーブルのリスト内のすべてのテーブルをパージするために使用されます。 次のクエリが使用されます。

   ```sql
   DELETE FROM NmsTrackingLogRcp WHERE iTrackingLogId IN (SELECT iTrackingLogId FROM NmsTrackingLogRcp WHERE tsLog < $(tsDate) LIMIT 5000) 
   ```

   ここで、`$(tsDate)` は、**NmsCleanup_TrackingLogPurgeDelay** オプションに対して定義された期間を減算する現在のサーバーの日付です。

1. トラッキング統計テーブルは、一括削除を使用してパージされます。 次のクエリが使用されます。

   ```sql
   DELETE FROM NmsTrackingStats WHERE iTrackingStatsId IN (SELECT iTrackingStatsId FROM NmsTrackingStats WHERE tsStart < $(tsDate) LIMIT 5000) 
   ```

   ここで、`$(tsDate)` は、**NmsCleanup_TrackingStatPurgeDelay** オプションに対して定義された期間を減算する現在のサーバーの日付です。

### 配信ログのクリーンアップ {#cleanup-of-delivery-logs}

このタスクを使用すると、様々なテーブルに保存されている配信ログをパージできます。

1. この目的のために、次のクエリを使用して配信ログスキーマのリストを復元します。

   ```sql
   SELECT distinct(sBroadLogSchema) FROM NmsDeliveryMapping WHERE sBroadLogSchema IS NOT NULL UNION SELECT distinct(sBroadLogExclSchema) FROM NmsDeliveryMapping WHERE sBroadLogExclSchema IS NOT NULL
   ```

1. ミッドソーシングを使用する場合、**NmsBroadLogMid** テーブルは配信マッピングで参照されません。 **nms:broadLogMid** スキーマは、前のクエリで復元されたリストに追加されます。
1. 次に、**データベースクリーンアップ** ワークフローは、以前に復元されたテーブルから古いデータをパージします。 次のクエリが使用されます。

   ```sql
   DELETE FROM $(tableName) WHERE iBroadLogId IN (SELECT iBroadLogId FROM $(tableName) WHERE tsLastModified < $(option) LIMIT 5000) 
   ```

   ここで、`$(tableName)` はスキーマのリスト内の各テーブルの名前で、`$(option)` は **NmsCleanup_BroadLogPurgeDelay** オプションで定義された日付です（[ デプロイメントウィザード ](#deployment-assistant) を参照）。

1. 最後に、ワークフローは **NmsProviderMsgId** テーブルが存在するかどうかを確認します。 その場合は、次のクエリを使用して、古いデータがすべて削除されます。

   ```sql
   DELETE FROM NmsProviderMsgId WHERE iBroadLogId IN (SELECT iBroadLogId FROM NmsProviderMsgId WHERE tsCreated < $(option) LIMIT 5000)
   ```

   ここで、`$(option)` は、「**NmsCleanup_BroadLogPurgeDelay**」オプションで定義された日付と一致します（「[ デプロイメントウィザード ](#deployment-assistant)」を参照）。

### NmsEmailErrorStat テーブルのクリーンアップ {#cleanup-of-the-nmsemailerrorstat-table-}

このタスクにより、**NmsEmailErrorStat** テーブルがクレンジングされます。 メインプログラム（**coalesceErrors**）は 2 つの日付を定義します。

* **開始日**:「**NmsLastErrorStatCoalesce**」オプションまたはテーブル内の最新の日付に一致する次のプロセスの日付。
* **終了日**：現在のサーバーの日付。

開始日が終了日以降の場合、プロセスは実行されません。 この場合、「**coalesceUpToDate**」というメッセージが表示されます。

開始日が終了日より前の場合、**NmsEmailErrorStat** テーブルはクレンジングされます。

開始日と終了日の間にある **NmsEmailErrorStat** テーブルのエラーの合計数は、次のクエリを使用して復元されます。

```sql
SELECT COUNT(*) FROM NmsEmailErrorStat WHERE tsDate>= $(start) AND tsDate< $(end)
```

ここで、`$end` と `$start` は、以前に定義した開始日と終了日です。

合計が 0 より大きい場合：

1. 特定のしきい値（20 に等しい）を超えるエラーのみを保持するには、次のクエリを実行します。

   ```sql
   SELECT iMXIP, iPublicId, SUM(iTotalConnections), SUM(iTotalErrors), SUM(iMessageErrors), SUM(iAbortedConnections), SUM(iFailedConnections), SUM(iRefusedConnections), SUM(iTimeoutConnections) FROM NmsEmailErrorStat WHERE tsDate>=$(start ) AND tsDate<$(end ) GROUP BY iMXIP, iPublicId HAVING SUM(iTotalErrors) >= 20
   ```

1. **coalescingErrors** メッセージが表示されます。
1. 開始日と終了日の間に発生したすべてのエラーを削除する新しい接続が作成されます。 次のクエリが使用されます。

   ```sql
   DELETE FROM NmsEmailErrorStat WHERE tsDate>=$(start) AND tsDate<$(end)
   ```

1. 各エラーは、次のクエリを使用して **NmsEmailErrorStat** テーブルに保存されます。

   ```sql
   INSERT INTO NmsEmailErrorStat(iMXIP, iPublicId, tsDate, iTotalConnections, iTotalErrors, iTimeoutConnections, iRefusedConnections, iAbortedConnections, iFailedConnections, iMessageErrors) VALUES($(lmxip ), $(lpublicId ), $(tsstart ), $(lconnections ), $(lconnectionErrors ),$(ltimeoutConnections ), $(lrefusedConnections ), $(labortedConnections ), $(lfailedConnections ), $(lmessageErrors))
   ```

   各変数は、前のクエリで復元された値と一致します。

1. **start** 変数は、ループを終了するために前のプロセスの値で更新されます。

ループとタスクが停止します。

クリーンアップは、**NmsEmailError** テーブルと **cleanupNmsMxDomain** テーブルで実行されます。

### NmsEmailError テーブルのクリーンアップ {#cleanup-of-the-nmsemailerror-table-}

次のクエリが使用されます。

```sql
DELETE FROM NmsEmailError WHERE iMXIP NOT IN (SELECT DISTINCT iMXIP FROM NmsEmailErrorStat)
```

このクエリは、**NmsEmailError** テーブルから **NmsEmailErrorStat** にリンクされたレコードがないすべての行を削除します。

### NmsMxDomain テーブルのクリーンアップ {#cleanup-of-the-nmsmxdomain-table-}

次のクエリが使用されます。

```sql
DELETE FROM NmsMxDomain WHERE iMXIP NOT IN (SELECT DISTINCT iMXIP FROM NmsEmailErrorStat)
```

このクエリでは、**NmsMxDomain** テーブルから **NmsEmailErrorStat** テーブルのリンクされたレコードを含まないすべての行を削除します。

### 提案のクリーンアップ {#cleanup-of-propositions}

**インタラクション** モジュールがインストールされている場合、このタスクは、**NmsPropositionXxx** テーブルをパージするために実行されます。

提案テーブルのリストが復元され、次のクエリを使用して各提案に対して一括削除が実行されます。

```sql
DELETE FROM NmsPropositionXxx WHERE iPropositionId IN (SELECT iPropositionId FROM NmsPropositionXxx WHERE tsLastModified < $(option) LIMIT 5000) 
```

ここで、`$(option)` は、「**NmsCleanup_PropositionPurgeDelay**」オプションに対して定義された日付です（「[ デプロイメントウィザード ](#deployment-assistant)」を参照）。

### シミュレーションテーブルのクリーンアップ {#cleanup-of-simulation-tables}

このタスクにより、孤立したシミュレーションテーブル（オファーシミュレーションや配信シミュレーションにリンクされなくなったテーブル）がクレンジングされます。

1. クリーンアップが必要なシミュレーションのリストを復元するには、次のクエリを使用します。

   ```sql
   SELECT iSimulationId FROM NmsSimulation WHERE iSimulationId<>0
   ```

1. 削除するテーブルの名前は、**wkSimu_** プレフィックスとシミュレーションの識別子で構成されます（例：**wkSimu_456831_aggr**）。

   ```sql
   DROP TABLE wkSimu_456831_aggr
   ```

### 監査証跡のクリーンアップ {#cleanup-of-audit-trail}

次のクエリが使用されます。

```sql
DELETE FROM XtkAudit WHERE tsChanged < $(tsDate)
```

ここで、**$（tsDate）** は、**XtkCleanup_AuditTrailPurgeDelay** オプションに定義された期間が減算される現在のサーバーの日付です。

### Nmsaddress のクリーンアップ {#cleanup-of-nmsaddress}

次のクエリが使用されます。

```sql
DELETE FROM NmsAddress WHERE iAddressId IN (SELECT iAddressId FROM NmsAddress WHERE iStatus=STATUS_QUARANTINE AND tsLastModified < $(NmsCleanup_AppSubscriptionRcpPurgeDelay + 5d) AND iType IN (MESSAGETYPE_IOS, MESSAGETYPE_ANDROID ) LIMIT 5000)
```

このクエリを実行すると、iOSおよびAndroidに関連するすべてのエントリが削除されます。

### 統計の更新とストレージの最適化 {#statistics-update}

**XtkCleanup_NoStats** オプションを使用すると、クリーンアップワークフローのストレージ最適化手順の動作を制御できます。

**XtkCleanup_NoStats** オプションが存在しないか、その値が 0 の場合、これにより PostgreSQL で詳細モード（VACUUM VERBOSE ANALYZE）でストレージの最適化が実行され、他のすべてのデータベースの統計が更新されます。 このコマンドが実行されていることを確認するには、PostgreSQL のログを確認してください。 VACUUM は `INFO: vacuuming "public.nmsactivecontact"` 形式で行を出力し、ANALYZE は `INFO: analyzing "public.nmsactivecontact"` 形式で行を出力します。

オプションの値が 1 の場合、統計の更新はどのデータベースでも実行されません。 ワークフローログに、「`Option 'XtkCleanup_NoStats' is set to '1'`」というログ行が表示されます。

オプションの値が 2 の場合、これにより、PostgreSQL で詳細モード（ANALYZE VERBOSE）でのストレージ分析が実行され、他のすべてのデータベースの統計が更新されます。 このコマンドが実行されていることを確認するには、PostgreSQL のログを確認してください。 ANALYZE は、`INFO: analyzing "public.nmsactivecontact"` の形式で行を出力します。

### 購読のクリーンアップ（NMAC） {#subscription-cleanup--nmac-}

このタスクは、削除されたサービスまたはモバイルアプリケーションに関連する購読をすべて削除します。

broadlog スキーマのリストを復元するには、次のクエリを使用します。

```sql
SELECT distinct(sBroadLogSchema) FROM NmsDeliveryMapping WHERE sBroadLogSchema IS NOT NULL
```

次に、タスクは **appSubscription** リンクにリンクされているテーブルの名前を復元し、これらのテーブルを削除します。

このクリーンアップ ワークフローでは、**NmsCleanup_AppSubscriptionRcpPurgeDelay** オプションで設定された時間以降に更新されていない、idisabled = 1 のエントリもすべて削除されます。

### クレンジングセッション情報 {#cleansing-session-information}

このタスクでは、**sessionInfo** テーブルから情報をクレンジングします。次のクエリが使用されます。

```sql
DELETE FROM XtkSessionInfo WHERE tsexpiration < $(curdate) 
```

### 期限切れイベントのクレンジング {#cleansing-expired-events}

このタスクにより、実行インスタンスで受信および保存されたイベントと、コントロールインスタンスでアーカイブされたイベントがクリーンアップされます。

### クレンジング反応 {#cleansing-reactions}

このタスクにより、仮説自体が削除された反応（テーブル **NmsRemaMatchRcp**）がクレンジングされます。
