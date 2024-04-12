---
product: campaign
title: データベースクリーンアップのワークフロー
description: 古いデータが自動的にクリーンアップされる仕組みを説明します
feature: Monitoring, Workflows
audience: production
content-type: reference
topic-tags: data-processing
exl-id: 75d3a0af-9a14-4083-b1da-2c1b22f57cbe
source-git-commit: b666535f7f82d1b8c2da4fbce1bc25cf8d39d187
workflow-type: tm+mt
source-wordcount: '2914'
ht-degree: 1%

---

# データベースクリーンアップのワークフロー{#database-cleanup-workflow}



## はじめに {#introduction}

**[!UICONTROL 管理／プロダクション／テクニカルワークフロー]**&#x200B;ノードからアクセスできる&#x200B;**[!UICONTROL データベースクリーンアップ]**&#x200B;ワークフローを使用すると、古いデータを削除して、データベースの急激な増加を回避できます。ワークフローは、ユーザーの操作なしで自動的にトリガーされます。

![クリーンアップ](assets/ncs_cleanup_workflow.png)

## 設定 {#configuration}

データベースのクリーンアップは、ワークフロースケジューラーとデプロイメントウィザードの 2 つのレベルで設定します。

### ワークフロースケジューラー {#the-scheduler}

>[!NOTE]
>
>スケジューラーについて詳しくは、[この節](../../workflow/using/scheduler.md)を参照してください。

デフォルトでは、 **[!UICONTROL データベースのクリーンアップ]** ワークフローは、毎日午前 4 時に開始するように設定されています。 スケジューラーを使用すると、ワークフローのトリガー頻度を変更できます。 次の頻度を使用できます。

* **[!UICONTROL 1 日に数回]**
* **[!UICONTROL 日次]**
* **[!UICONTROL 毎週]**
* **[!UICONTROL 1 回]**

![スケジューラ](assets/ncs_cleanup_scheduler.png)

>[!IMPORTANT]
>
>の目的で **[!UICONTROL データベースのクリーンアップ]** ワークフローは、スケジューラーで定義された日時に開始するには、ワークフローエンジン（wfserver）を開始する必要があります。

### 配置ウィザード {#deployment-wizard}

この **[!UICONTROL 配置ウィザード]**、経由でアクセス **[!UICONTROL ツール /詳細]** メニューを使用すると、データを保存する期間を設定できます。 値は日数で表します。 これらの値が変更されない場合、ワークフローではデフォルト値が使用されます。

![](assets/ncs_cleanup_deployment-wizard.png)

のフィールド **[!UICONTROL データのパージ]** ウィンドウは次のオプションと一致します。 これらは、で実行される一部のタスクで使用されます **[!UICONTROL データベースのクリーンアップ]** ワークフロー：

* 統合されたトラッキング： **NmsCleanup_TrackingStatPurgeDelay** （を参照）。 [トラッキングログのクリーンアップ](#cleanup-of-tracking-logs)）
* 配信ログ： **NmsCleanup_BroadLogPurgeDelay** （を参照）。 [配信ログのクリーンアップ](#cleanup-of-delivery-logs)）
* トラッキングログ： **NmsCleanup_TrackingLogPurgeDelay** （を参照）。 [トラッキングログのクリーンアップ](#cleanup-of-tracking-logs)）
* 削除された配信： **NmsCleanup_RecycledDeliveryPurgeDelay** （を参照）。 [削除またはリサイクルされる配信のクリーンアップ](#cleanup-of-deliveries-to-be-deleted-or-recycled)）
* 却下をインポート : **NmsCleanup_RejectsPurgeDelay** （を参照）。 [読み込みによって生成された却下のクリーンアップ](#cleanup-of-rejects-generated-by-imports-)）
* 訪問者プロファイル : **NmsCleanup_VisitorPurgeDelay** （を参照）。 [訪問者のクリーンアップ](#cleanup-of-visitors)）
* オファーの提案： **NmsCleanup_PropositionPurgeDelay** （を参照）。 [提案のクリーンアップ](#cleanup-of-propositions)）

  >[!NOTE]
  >
  >この **[!UICONTROL オファーの提案]** フィールドは、 **相互作用** モジュールがインストールされました。

* イベント： **NmsCleanup_EventPurgeDelay** （を参照）。 [期限切れイベントのクレンジング](#cleansing-expired-events)）
* アーカイブしたイベント： **NmsCleanup_EventHistoPurgeDelay** （を参照）。 [期限切れイベントのクレンジング](#cleansing-expired-events)）

  >[!NOTE]
  >
  >この **[!UICONTROL イベント]** および **[!UICONTROL アーカイブしたイベント]** フィールドは、 **Message Center** モジュールがインストールされました。

* 監査記録： **XtkCleanup_AuditTrailPurgeDelay** （を参照）。 [監査証跡のクリーンアップ](#cleanup-of-audit-trail)）

が実行するすべてのタスク **[!UICONTROL データベースのクリーンアップ]** ワークフローについては、次の節で説明します。

## データベースクリーンアップワークフローで実行されるタスク {#tasks-carried-out-by-the-database-cleanup-workflow}

ワークフロースケジューラーで定義された日時（を参照 [スケジューラー](#the-scheduler)）を選択した場合、ワークフローエンジンはデータベースクリーンアッププロセスを開始します。 データベースクリーンアップは、データベースに接続し、以下に示す順序でタスクを実行します。

>[!IMPORTANT]
>
>これらのタスクのいずれかが失敗した場合、次のタスクは実行されません。
>
>を使用した SQL クエリ **制限** 属性は、すべての情報が処理されるまで繰り返し実行されます。


### クリーンアップを削除するリスト {#lists-to-delete-cleanup}

が実行する最初のタスク **[!UICONTROL データベースのクリーンアップ]** を含むすべてのグループを削除します。 **deleteStatus != 0** からの属性 **NmsGroup**. これらのグループにリンクされ、他のテーブルに存在するレコードも削除されます。

1. 削除されるリストは、次の SQL クエリを使用して復元されます。

   ```sql
   SELECT iGroupId, sLabel, iType FROM NmsGroup WHERE iDeleteStatus <> 0 OR tsExpirationDate <= GetDate() 
   ```

1. 各リストには、他のテーブルへのリンクが複数あります。 これらのリンクはすべて、次のクエリを使用して一括で削除されます。

   ```sql
   DELETE FROM $(relatedTable) WHERE iGroupId=$(l) IN (SELECT iGroupId FROM $(relatedTable) WHERE iGroupId=$(l) LIMIT 5000) 
   ```

   ここで、 `$(relatedTable)` 関連テーブルです **NmsGroup** および `$(l)` はリスト識別子です。

1. リストが「リスト」タイプのリストの場合、以下のクエリを使用して、関連テーブルが削除されます。

   ```sql
   DROP TABLE grp$(l)
   ```

1. ごと **を選択** 操作によって復元されたタイプ リストは、次のクエリを使用して削除されます：

   ```sql
   DELETE FROM NmsGroup WHERE iGroupId=$(l) 
   ```

   ここで、 `$(l)` はリスト識別子です。

### 削除またはリサイクルされる配信のクリーンアップ {#cleanup-of-deliveries-to-be-deleted-or-recycled}

このタスクにより、削除またはリサイクルされるすべての配信がパージされます。

1. この **[!UICONTROL データベースのクリーンアップ]** ワークフローは、に該当するすべての配信を選択します **deleteStatus** フィールドの値が **[!UICONTROL はい]** または **[!UICONTROL 再利用済み]** 削除日がで定義された期間より前のもの **[!UICONTROL 削除された配信]** （**NmsCleanup_RecycledDeliveryPurgeDelay**）フィールドに入力します。 詳しくは、次を参照してください [配置ウィザード](#deployment-wizard). この期間は、現在のサーバーの日付を基準に計算されます。
1. ミッドソーシングサーバーごとに、タスクが削除する配信のリストを選択します。
1. この **[!UICONTROL データベースのクリーンアップ]** ワークフローでは、配信ログ、添付ファイル、ミラーページ情報およびその他すべての関連データが削除されます。
1. 配信を削除する前に、リンクされている情報が次の表から削除されます。

   * 配信除外テーブル（**NmsDlvExclusion**）、次のクエリが使用されます。

     ```sql
     DELETE FROM NmsDlvExclusion WHERE iDeliveryId=$(l)
     ```

     ここで、 **$（l）** は配信の識別子です。

   * クーポンテーブル（**NmsCouponValue**）を選択すると、次のクエリが使用されます（複数削除を使用）。

     ```sql
     DELETE FROM NmsCouponValue WHERE iMessageId IN (SELECT iMessageId FROM NmsCouponValue WHERE EXISTS (SELECT B.iBroadLogId FROM $(BroadLogTableName) B WHERE B.iDeliveryId = $(l) AND B.iBroadLogId = iMessageId ) LIMIT 5000)
     ```

     ここで、 `$(l)` は配信の識別子です。

   * 配信ログテーブル（**NmsBroadlogXxx**）に設定した場合は、2 万件のレコードに相当するバッチで一括削除が実行されます。
   * オファーの提案テーブル（**NmsPropositionXxx**）に設定した場合は、2 万件のレコードに相当するバッチで一括削除が実行されます。
   * トラッキングログテーブル（**NmsTrackinglogXxx**）に設定した場合は、2 万件のレコードに相当するバッチで一括削除が実行されます。
   * 配信フラグメントテーブル（**NmsDeliveryPart**）に設定した場合、50 万件のレコードに相当するバッチで一括削除が実行されます。 この表には、配信される残りのメッセージに関するパーソナライゼーション情報が含まれています。
   * ミラーページのデータフラグメントテーブル（**NmsMirrorPageInfo**）を選択すると、期限切れの配信部分と完了またはキャンセルされた配信部分に対して、20,000 件のレコードのバッチで一括削除が実行されます。 このテーブルには、ミラーページの生成に使用されるすべてのメッセージに関するパーソナライゼーション情報が含まれています。
   * ミラーページの検索テーブル（**NmsMirrorPageSearch**）に設定した場合は、2 万件のレコードに相当するバッチで一括削除が実行されます。 このテーブルは、に格納されたパーソナライゼーション情報へのアクセスを提供する検索インデックスです。 **NmsMirrorPageInfo** テーブル。
   * バッチ処理ログテーブル（**XtkJobLog**）に設定した場合は、2 万件のレコードに相当するバッチで一括削除が実行されます。 この表には、削除される配信のログが含まれています。
   * 配信 URL トラッキングテーブル（**NmsTrackingUrl**）、次のクエリが使用されます。

     ```sql
     DELETE FROM NmsTrackingUrl WHERE iDeliveryId=$(l)
     ```

     ここで、 `$(l)` は配信の識別子です。

     この表には、トラッキングを有効にするために削除する配信で見つかった URL が含まれています。

1. 配信が配信テーブルから削除されます（**NmsDelivery**）:

   ```sql
   DELETE FROM NmsDelivery WHERE iDeliveryId = $(l)
   ```

   ここで、 `$(l)` は配信の識別子です。

#### ミッドソーシングを使用した配信 {#deliveries-using-mid-sourcing}

この **[!UICONTROL データベースのクリーンアップ]** ワークフローでは、ミッドソーシングサーバー上の配信も削除します。

1. これを行うには、ワークフローは各配信が（ステータスに基づいて）非アクティブであることを確認します。 配信がアクティブな場合は、削除される前に停止されます。 チェックは、次のクエリを実行することで実行されます。

   ```sql
   SELECT iState FROM NmsDelivery WHERE iDeliveryId = $(l) AND iState <> 100;
   ```

   ここで、 **$（l）** は配信の識別子です。

1. ステータスの値がの場合 **[!UICONTROL 開始を保留中]** , **[!UICONTROL 処理中]** , **[!UICONTROL 回復を保留中]** , **[!UICONTROL リカバリ中]** , **[!UICONTROL 一時停止がリクエストされました]** , **[!UICONTROL 一時停止中]** 、または **[!UICONTROL 一時停止]** （値 51、55、61、62、71、72、75）、配信が停止され、タスクによってリンクされた情報がパージされます。

### 期限切れ配信のクリーンアップ {#cleanup-of-expired-deliveries}

このタスクにより、有効期限が切れた配信が停止します。

1. この **[!UICONTROL データベースのクリーンアップ]** ワークフローは、有効期限が切れた配信のリストを作成します。 このリストには、ステータスが以外の、期限切れの配信がすべて含まれます **[!UICONTROL 完了]** 、および 10,000 件を超える未処理メッセージを含む最近停止した配信。 次のクエリが使用されます。

   ```sql
   SELECT iDeliveryId, iState FROM NmsDelivery WHERE iDeleteStatus=0 AND iIsModel=0 AND iDeliveryMode=1 AND ( (iState >= 51 AND iState < 85 AND tsValidity IS NOT NULL AND tsValidity < $(currentDate) ) OR (iState = 85 AND DateMinusDays(15) < tsLastModified AND iToDeliver - iProcessed >= 10000 ))
   ```

   ここで、 `delivery mode 1` 次に一致 **[!UICONTROL 一括配信]** モード、 `state 51` 次に一致 **[!UICONTROL 開始を保留中]** 都道府県、 `state 85` 次に一致 **[!UICONTROL 停止]** 状態の場合、配信サーバー上の一括更新される配信ログの最大数は 10,000 に等しくなります。

1. 次に、ワークフローには、ミッドソーシングを使用する、最近期限切れの配信のリストが含まれます。 ミッドソーシングサーバーから復元された配信ログがまだない配信は除外されます。

   次のクエリが使用されます。

   ```sql
   SELECT iDeliveryId, tsValidity, iMidRemoteId, mData FROM NmsDelivery WHERE (iDeliveryMode = 4 AND (iState = 85 OR iState = 95) AND tsValidity IS NOT NULL AND (tsValidity < SubDays(GetDate() , 15) OR tsValidity < $(DateOfLastLogPullUp)) AND tsLastModified > SubDays(GetDate() , 15))
   ```

1. 次のクエリは、日付で配信をフィルタリングするために、外部アカウントがまだアクティブかどうかを検出するために使用されます。

   ```sql
   SELECT iExtAccountId FROM NmsExtAccount WHERE iActive<>0 AND sName=$(providerName)
   ```

1. 期限切れ配信のリストで、ステータスが「」の配信ログ **[!UICONTROL 保留中]** 、切り替え先 **[!UICONTROL 配信がキャンセルされました]** に変更すると、このリスト内のすべての配信がに切り替わります **[!UICONTROL 完了]** .

   次のクエリが使用されます。

   ```sql
   UPDATE $(BroadLogTableName) SET tsLastModified=$(curdate), iStatus=7, iMsgId=$(bl) WHERE iDeliveryId=$(dl) AND iStatus=6
   ```

   ここで、 `$(curdate)`は、データベースサーバーの現在の日付です。 `$(bl)` は、配信ログメッセージの識別子です。 `$(dl)` は配信識別子です。 `delivery status 6` 次に一致 **[!UICONTROL 保留中]** ステータスと `delivery status 7` 次に一致 **[!UICONTROL 配信がキャンセルされました]** ステータス。

   ```sql
   UPDATE NmsDelivery SET iState = 95, tsLastModified = $(curdate), tsBroadEnd = tsValidity WHERE iDeliveryId = $(dl)
   ```

   ここで、 `delivery state 95` 次に一致 **[!UICONTROL 完了]** ステータス、 `$(dl)` は配信の識別子です。

1. すべてのフラグメント （**deliveryParts**）の古い配信が削除され、処理中の古い通知配信のフラグメントがすべて削除されます。 一括削除は、両方のタスクで使用します。

   次のクエリが使用されます。

   ```sql
   DELETE FROM NmsDeliveryPart WHERE iDeliveryPartId IN (SELECT iDeliveryPartId FROM NmsDeliveryPart WHERE iDeliveryId IN (SELECT iDeliveryId FROM NmsDelivery WHERE iState=95 OR iState=85) LIMIT 5000)
   ```

   ```sql
   DELETE FROM NmsDeliveryPart WHERE iDeliveryPartId IN (SELECT iDeliveryPartId FROM NmsDeliveryPart WHERE tsValidity < $(curDate) LIMIT 500000)
   ```

   ここで、 `delivery state 95` 次に一致 **[!UICONTROL 完了]** ステータス、 `delivery state 85` 次に一致 **[!UICONTROL 停止]** ステータス、 `$(curDate)` は、現在のサーバーの日付です。

### ミラーページのクリーンアップ {#cleanup-of-mirror-pages}

配信で使用される web リソース（ミラーページ）を削除します。

1. まず、パージ対象の配信のリストは、次のクエリを使用して復元されます。

   ```sql
   SELECT iDeliveryId, iNeedMirrorPage FROM NmsDelivery WHERE iWebResPurged = 0 AND tsWebValidity IS NOT NULL AND tsWebValidity < $(curdate)
   ```

   ここで、 `$(curDate)` は、現在のサーバーの日付です。

1. この **NmsMirrorPageInfo** その後、必要に応じて、以前に復元した配信の識別子を使用してテーブルがパージされます。 一括削除は、次のクエリの生成に使用されます。

   ```sql
   DELETE FROM NmsMirrorPageInfo WHERE iMirrorPageInfoId IN (SELECT iMirrorPageInfoId FROM NmsMirrorPageInfo WHERE iDeliveryId = $(dl)) LIMIT 5000
   ```

   ```sql
   DELETE FROM NmsMirrorPageSearch WHERE iMessageId IN (SELECT iMessageId FROM NmsMirrorPageSearch WHERE iDeliveryId = $(dl)) LIMIT 5000
   ```

   ここで、 `$(dl)` は配信の識別子です。

1. 次に、エントリが配信ログに追加されます。
1. パージされた配信は識別されるので、後で再処理する必要がなくなります。 次のクエリが実行されます。

   ```sql
   UPDATE NmsDelivery SET iWebResPurged = 1 WHERE iDeliveryId IN ($(strIn))
   ```

   ここで、 `$(strIn)` は配信識別子のリストです。

### 作業用テーブルのクリーンアップ {#cleanup-of-work-tables}

ステータスがの配信に一致するすべての作業用テーブルをデータベースから削除します。 **[!UICONTROL 編集中]** , **[!UICONTROL 停止]** または **[!UICONTROL 削除済み]** .

1. で始まる名前のテーブルのリスト **wkDlv_** は、次のクエリ（postgresql）を使用して最初に復元されます。

   ```sql
   SELECT relname FROM pg_class WHERE relname LIKE Lower('wkDlv_%') ESCAPE E'\\' AND relkind IN ('r','v') AND pg_get_userbyid(relowner)<>'postgres'
   ```

1. その後、処理中のワークフローで使用されるテーブルは除外されます。 これを行うには、次のクエリを使用して、進行中の配信のリストを復元します。

   ```sql
   SELECT iDeliveryId FROM NmsDelivery WHERE iDeliveryId<>0 AND iDeleteStatus=0 AND iState NOT IN (0,85,100);
   ```

   ここで、 `0` は、に一致する値です **[!UICONTROL 編集中]** 配信ステータス、 `85` 次に一致 **[!UICONTROL 停止]** ステータスと `100` 次に一致 **[!UICONTROL 削除済み]** ステータス。

1. 使用されなくなったテーブルは、次のクエリを使用して削除されます。

   ```sql
   DROP TABLE wkDlv_15487_1;
   ```

### 読み込みによって生成された却下のクリーンアップ {#cleanup-of-rejects-generated-by-imports-}

この手順を使用すると、読み込み時にすべてのデータが処理されなかったレコードを削除できます。

1. 一括削除は次の場所で実行されます。 **XtkReject** 次のクエリを含むテーブル：

   ```sql
   DELETE FROM XtkReject WHERE iRejectId IN (SELECT iRejectId FROM XtkReject WHERE tsLog < $(curDate)) LIMIT $(l)
   ```

   ここで、 `$(curDate)` は、に定義された期間を引く現在のサーバーの日付です。 **NmsCleanup_RejectsPurgeDelay** オプション（を参照 [配置ウィザード](#deployment-wizard)）および `$(l)` は、一括削除されるレコードの最大数です。

1. すべての孤立した却下は、次のクエリを使用して削除されます。

   ```sql
   DELETE FROM XtkReject WHERE iJobId NOT IN (SELECT iJobId FROM XtkJob)
   ```

### ワークフローインスタンスのクリーンアップ {#cleanup-of-workflow-instances}

このタスクは、識別子（**lWorkflowId**）と履歴（**lHistory**）に設定します。 ワークテーブルのクリーンアップタスクを再度実行して、非アクティブなテーブルを削除します。 このクリーンアップでは、削除されたワークフローの孤立したすべてのワークテーブル（wkf% および wkfhisto%）も削除されます。

>[!NOTE]
>
>履歴のパージ頻度は、でワークフローごとに指定します **履歴（日数）** フィールド （デフォルト値は 30 日）。 このフィールドは **実行** ワークフローのプロパティの「」タブ。 詳しくは、[この節](../../workflow/using/workflow-properties.md#execution)を参照してください。

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

   ここで、 `$(lworkflow)` はワークフローの識別子で、は `$(lhistory)` は履歴の識別子です。

1. 未使用のテーブルはすべて削除されます。 この目的のために、すべてのテーブルは **wkf%** 次のクエリ（postgresql）を使用してマスクを入力します。

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

   ここで、 `$(strcondition)` は、に一致するテーブルのリストです。 **wkfhisto%** マスク。

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

グループにリンクされている孤立した作業用テーブルを削除します。 この **NmsGroup** テーブルには、クレンジングするグループ（タイプが 0 とは異なる）が格納されます。 テーブル名のプレフィックスは次のとおりです **グループ**. クレンジングするグループを識別するために、次のクエリを使用します。

```sql
SELECT iGroupId FROM NmsGroup WHERE iType>0"
```

### 訪問者のクリーンアップ {#cleanup-of-visitors}

このタスクは、一括削除を使用して訪問者テーブルから古いレコードを削除します。 古いレコードとは、最後の変更が配置ウィザードで定義された保存期間より前のレコードです（ [配置ウィザード](#deployment-wizard)）に設定します。 次のクエリが使用されます。

```sql
DELETE FROM NmsVisitor WHERE iVisitorId IN (SELECT iVisitorId FROM NmsVisitor WHERE iRecipientId = 0 AND tsLastModified < AddDays(GetDate(), -30) AND iOrigin = 0 LIMIT 20000)
```

ここで、 `$(tsDate)` は、現在のサーバー日付で、ここから用に定義された期間を減算します **NmsCleanup_VisitorPurgeDelay** オプション。

### NPAI のクリーンアップ {#cleanup-of-npai}

このタスクを使用すると、有効なアドレスに一致するレコードを **NmsAddress** テーブル。 次のクエリを使用して、一括削除を実行します。

```sql
DELETE FROM NmsAddress WHERE iAddressId IN (SELECT iAddressId FROM NmsAddress WHERE iStatus=2 AND tsLastModified < $(tsDate1) AND tsLastModified >= $(tsDate2) LIMIT 5000)
```

ここで、 `status 2` 次に一致 **[!UICONTROL 有効]** ステータス、 `$(tsDate1)` は現在のサーバーの日付で、 `$(tsDate2)` 次に一致 **NmsCleanup_LastCleanup** オプション。

### 購読のクリーンアップ {#cleanup-of-subscriptions-}

このタスクは、ユーザーが削除したすべての購読を次からパージします **NmsSubscription** 一括削除を使用するテーブル。 次のクエリが使用されます。

```sql
DELETE FROM NmsSubscription WHERE iDeleteStatus <>0
```

### トラッキングログのクリーンアップ {#cleanup-of-tracking-logs}

このタスクは、トラッキングログテーブルと Web トラッキングログテーブルから古いレコードを削除します。 古いレコードとは、配置ウィザードで定義された保存期間より前のレコードです（ [配置ウィザード](#deployment-wizard)）に設定します。

1. まず、次のクエリを使用して、トラッキングログテーブルのリストを復元します。

   ```sql
   SELECT distinct(sTrackingLogSchema) FROM NmsDeliveryMapping WHERE sTrackingLogSchema IS NOT NULL;
   ```

1. 一括削除は、以前に復元したテーブルのリスト内のすべてのテーブルをパージするために使用されます。 次のクエリが使用されます。

   ```sql
   DELETE FROM NmsTrackingLogRcp WHERE iTrackingLogId IN (SELECT iTrackingLogId FROM NmsTrackingLogRcp WHERE tsLog < $(tsDate) LIMIT 5000) 
   ```

   ここで、 `$(tsDate)` は、に定義された期間を引く現在のサーバーの日付です。 **NmsCleanup_TrackingLogPurgeDelay** オプション。

1. トラッキング統計テーブルは、一括削除を使用してパージされます。 次のクエリが使用されます。

   ```sql
   DELETE FROM NmsTrackingStats WHERE iTrackingStatsId IN (SELECT iTrackingStatsId FROM NmsTrackingStats WHERE tsStart < $(tsDate) LIMIT 5000) 
   ```

   ここで、 `$(tsDate)` は、に定義された期間を引く現在のサーバーの日付です。 **NmsCleanup_TrackingStatPurgeDelay** オプション。

### 配信ログのクリーンアップ {#cleanup-of-delivery-logs}

このタスクを使用すると、様々なテーブルに保存されている配信ログをパージできます。

1. この目的のために、次のクエリを使用して配信ログスキーマのリストを復元します。

   ```sql
   SELECT distinct(sBroadLogSchema) FROM NmsDeliveryMapping WHERE sBroadLogSchema IS NOT NULL UNION SELECT distinct(sBroadLogExclSchema) FROM NmsDeliveryMapping WHERE sBroadLogExclSchema IS NOT NULL
   ```

1. ミッドソーシングを使用する場合 **NmsBroadLogMid** テーブルが配信マッピングで参照されていません。 この **nms:broadLogMid** スキーマは、前のクエリで復元されたリストに追加されます。
1. この **データベースのクリーンアップ** 次に、ワークフローは、以前にリカバリされたテーブルから古いデータをパージします。 次のクエリが使用されます。

   ```sql
   DELETE FROM $(tableName) WHERE iBroadLogId IN (SELECT iBroadLogId FROM $(tableName) WHERE tsLastModified < $(option) LIMIT 5000) 
   ```

   ここで、 `$(tableName)` は、スキーマのリスト内の各テーブルの名前で、は `$(option)` は、に定義された日付です。 **NmsCleanup_BroadLogPurgeDelay** オプション（を参照 [配置ウィザード](#deployment-wizard)）に設定します。

1. 最後に、ワークフローによって **NmsProviderMsgId** テーブルが存在します。 その場合は、次のクエリを使用して、古いデータがすべて削除されます。

   ```sql
   DELETE FROM NmsProviderMsgId WHERE iBroadLogId IN (SELECT iBroadLogId FROM NmsProviderMsgId WHERE tsCreated < $(option) LIMIT 5000)
   ```

   ここで、 `$(option)` 次に対して定義された日付に一致 **NmsCleanup_BroadLogPurgeDelay** オプション（を参照 [配置ウィザード](#deployment-wizard)）に設定します。

### NmsEmailErrorStat テーブルのクリーンアップ {#cleanup-of-the-nmsemailerrorstat-table-}

このタスクはをクリーンアップします **NmsEmailErrorStat** テーブル。 メインプログラム （**coalesceErrors**）は、次の 2 つの日付を定義します。

* **開始日**：に一致する次のプロセスの日付 **NmsLastErrorStatCoalesce** オプションまたはテーブルの最新の日付。
* **終了日**：現在のサーバーの日付。

開始日が終了日以降の場合、プロセスは実行されません。 この場合、 **coalesceUpToDate** メッセージが表示されます。

開始日が終了日より前の場合、 **NmsEmailErrorStat** テーブルがクレンジングされます。

でのエラーの合計数 **NmsEmailErrorStat** 開始日と終了日の間にあるテーブルは、次のクエリを使用して復元されます。

```sql
SELECT COUNT(*) FROM NmsEmailErrorStat WHERE tsDate>= $(start) AND tsDate< $(end)
```

ここで、 `$end` および `$start` は、以前に定義した開始日と終了日です。

合計が 0 より大きい場合：

1. 特定のしきい値（20 に等しい）を超えるエラーのみを保持するには、次のクエリを実行します。

   ```sql
   SELECT iMXIP, iPublicId, SUM(iTotalConnections), SUM(iTotalErrors), SUM(iMessageErrors), SUM(iAbortedConnections), SUM(iFailedConnections), SUM(iRefusedConnections), SUM(iTimeoutConnections) FROM NmsEmailErrorStat WHERE tsDate>=$(start ) AND tsDate<$(end ) GROUP BY iMXIP, iPublicId HAVING SUM(iTotalErrors) >= 20
   ```

1. この **coalescingErrors** メッセージが表示されます。
1. 開始日と終了日の間に発生したすべてのエラーを削除する新しい接続が作成されます。 次のクエリが使用されます。

   ```sql
   DELETE FROM NmsEmailErrorStat WHERE tsDate>=$(start) AND tsDate<$(end)
   ```

1. 各エラーは、 **NmsEmailErrorStat** 次のクエリを使用したテーブル：

   ```sql
   INSERT INTO NmsEmailErrorStat(iMXIP, iPublicId, tsDate, iTotalConnections, iTotalErrors, iTimeoutConnections, iRefusedConnections, iAbortedConnections, iFailedConnections, iMessageErrors) VALUES($(lmxip ), $(lpublicId ), $(tsstart ), $(lconnections ), $(lconnectionErrors ),$(ltimeoutConnections ), $(lrefusedConnections ), $(labortedConnections ), $(lfailedConnections ), $(lmessageErrors))
   ```

   各変数は、前のクエリで復元された値と一致します。

1. この **開始** 変数は、前のプロセスの値で更新され、ループが終了します。

ループとタスクが停止します。

クリーンアップはで実行されます **NmsEmailError** および **cleanupNmsmxDomain** テーブル。

### NmsEmailError テーブルのクリーンアップ {#cleanup-of-the-nmsemailerror-table-}

次のクエリが使用されます。

```sql
DELETE FROM NmsEmailError WHERE iMXIP NOT IN (SELECT DISTINCT iMXIP FROM NmsEmailErrorStat)
```

このクエリは、内のリンクされたレコードがないすべての行を削除します **NmsEmailErrorStat** から **NmsEmailError** テーブル。

### NmsMxDomain テーブルのクリーンアップ {#cleanup-of-the-nmsmxdomain-table-}

次のクエリが使用されます。

```sql
DELETE FROM NmsMxDomain WHERE iMXIP NOT IN (SELECT DISTINCT iMXIP FROM NmsEmailErrorStat)
```

このクエリは、内のリンクされたレコードのない行をすべて削除します **NmsEmailErrorStat** テーブルを選択 **NmsMxDomain** テーブル。

### 提案のクリーンアップ {#cleanup-of-propositions}

次の場合 **相互作用** モジュールがインストールされました。このタスクは、 **NmsPropositionXxx** テーブル。

提案テーブルのリストが復元され、次のクエリを使用して各提案に対して一括削除が実行されます。

```sql
DELETE FROM NmsPropositionXxx WHERE iPropositionId IN (SELECT iPropositionId FROM NmsPropositionXxx WHERE tsLastModified < $(option) LIMIT 5000) 
```

ここで、 `$(option)` は、に定義された日付です。 **NmsCleanup_PropositionPurgeDelay** オプション（を参照 [配置ウィザード](#deployment-wizard)）に設定します。

### シミュレーションテーブルのクリーンアップ {#cleanup-of-simulation-tables}

このタスクにより、孤立したシミュレーションテーブル（オファーシミュレーションや配信シミュレーションにリンクされなくなったテーブル）がクレンジングされます。

1. クリーンアップが必要なシミュレーションのリストを復元するには、次のクエリを使用します。

   ```sql
   SELECT iSimulationId FROM NmsSimulation WHERE iSimulationId<>0
   ```

1. 削除するテーブルの名前は、 **wkSimu_** プレフィックスの後にシミュレーションの識別子（例： **wkSimu_456831_aggr**）:

   ```sql
   DROP TABLE wkSimu_456831_aggr
   ```

### 監査証跡のクリーンアップ {#cleanup-of-audit-trail}

次のクエリが使用されます。

```sql
DELETE FROM XtkAudit WHERE tsChanged < $(tsDate)
```

ここで、 **$（tsDate）** は、に対して定義された現在のサーバーの日付です。 **XtkCleanup_AuditTrailPurgeDelay** オプションが減算されます。

### Nmsaddress のクリーンアップ {#cleanup-of-nmsaddress}

次のクエリが使用されます。

```sql
DELETE FROM NmsAddress WHERE iAddressId IN (SELECT iAddressId FROM NmsAddress WHERE iStatus=STATUS_QUARANTINE AND tsLastModified < $(NmsCleanup_AppSubscriptionRcpPurgeDelay + 5d) AND iType IN (MESSAGETYPE_IOS, MESSAGETYPE_ANDROID ) LIMIT 5000)
```

このクエリは、iOSおよび Android に関連するすべてのエントリを削除します。

### 統計の更新とストレージの最適化 {#statistics-update}

この **XtkCleanup_NoStats** オプションを使用すると、クリーンアップワークフローのストレージを最適化する手順の動作を制御できます。

次の場合 **XtkCleanup_NoStats** オプションが存在しないか、その値が 0 の場合、これは PostgreSQL の詳細モード（VACUUM VERBOSE ANALYZE）でストレージの最適化を実行し、他のすべてのデータベースの統計を更新します。 このコマンドが実行されていることを確認するには、PostgreSQL のログを確認してください。 VACUUM は次のフォーマットで行を出力します： `INFO: vacuuming "public.nmsactivecontact"` ANALYZE は、次の形式の行を出力します。 `INFO: analyzing "public.nmsactivecontact"`.

オプションの値が 1 の場合、統計の更新はどのデータベースでも実行されません。 次のログ行がワークフローログに表示されます。 `Option 'XtkCleanup_NoStats' is set to '1'`.

オプションの値が 2 の場合、これにより、PostgreSQL で詳細モード（ANALYZE VERBOSE）でのストレージ分析が実行され、他のすべてのデータベースの統計が更新されます。 このコマンドが実行されていることを確認するには、PostgreSQL のログを確認してください。 ANALYZE は、次の形式の行を出力します。 `INFO: analyzing "public.nmsactivecontact"`.

### 購読のクリーンアップ（NMAC） {#subscription-cleanup--nmac-}

このタスクは、削除されたサービスまたはモバイルアプリケーションに関連する購読をすべて削除します。

broadlog スキーマのリストを復元するには、次のクエリを使用します。

```sql
SELECT distinct(sBroadLogSchema) FROM NmsDeliveryMapping WHERE sBroadLogSchema IS NOT NULL
```

次に、タスクは、にリンクされているテーブルの名前を復元します **appSubscription** これらのテーブルをリンクして削除します。

このクリーンアップワークフローは、idisabled = 1 で設定された時間以降に更新されていないエントリもすべて削除します。 **NmsCleanup_AppSubscriptionRcpPurgeDelay** オプション。

### クレンジングセッション情報 {#cleansing-session-information}

このタスクはから情報をクレンジングします **sessionInfo** テーブルでは、次のクエリが使用されます。

```sql
DELETE FROM XtkSessionInfo WHERE tsexpiration < $(curdate) 
```

### 期限切れイベントのクレンジング {#cleansing-expired-events}

このタスクにより、実行インスタンスで受信および保存されたイベントと、コントロールインスタンスでアーカイブされたイベントがクリーンアップされます。

### クレンジング反応 {#cleansing-reactions}

このタスクは反応（テーブル）をクレンジングします **NmsRemaMatchRcp**）に表示されます。このフィールドは仮説自体が削除されています。
