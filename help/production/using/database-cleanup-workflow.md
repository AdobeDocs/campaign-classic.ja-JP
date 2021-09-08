---
product: campaign
title: データベースクリーンアップのワークフロー
description: 古いデータが自動的にクリーンアップされる方法を説明します
audience: production
content-type: reference
topic-tags: data-processing
exl-id: 75d3a0af-9a14-4083-b1da-2c1b22f57cbe
source-git-commit: f232588b981d262ef67ff8b7a6f39ff3ea2505d3
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

データベースのクリーンアップは、次の2つのレベルで設定します。（ワークフロースケジューラー）と、デプロイウィザードで、

### ワークフロースケジューラ {#the-scheduler}

>[!NOTE]
>
>スケジューラーについて詳しくは、[この節](../../workflow/using/scheduler.md)を参照してください。

デフォルトでは、**[!UICONTROL データベースクリーンアップ]**&#x200B;ワークフローは、毎日午前4時に開始するように設定されています。 スケジューラーを使用すると、ワークフローのトリガー頻度を変更できます。 次の頻度を使用できます。

* **[!UICONTROL 1 日に数回]**
* **[!UICONTROL 毎日]**
* **[!UICONTROL 毎週]**
* **[!UICONTROL 1 回]**

![](assets/ncs_cleanup_scheduler.png)

>[!IMPORTANT]
>
>**[!UICONTROL データベースクリーンアップ]**&#x200B;ワークフローをスケジューラーで定義された日時に開始するには、ワークフローエンジン(wfserver)を起動する必要があります。 そうでない場合、データベースクレンジングは次回ワークフローエンジンが起動されるまで実行されません。

### デプロイメントウィザード {#deployment-wizard}

**[!UICONTROL デプロイウィザード]**（**[!UICONTROL ツール/詳細]**&#x200B;メニューからアクセス）を使用して、データの保存期間を設定できます。 値は日数で表します。 これらの値が変更されない場合、ワークフローはデフォルト値を使用します。

![](assets/ncs_cleanup_deployment-wizard.png)

**[!UICONTROL データのパージ]**&#x200B;ウィンドウのフィールドは、次のオプションと一致します。 これらは、**[!UICONTROL データベースクリーンアップ]**&#x200B;ワークフローで実行されるタスクの一部で使用されます。

* 統合されたトラッキング：**NmsCleanup_TrackingStatPurgeDelay**（[トラッキングログのクリーンアップ](#cleanup-of-tracking-logs)を参照）
* 配信ログ：**NmsCleanup_BroadLogPurgeDelay**（[配信ログのクリーンアップ](#cleanup-of-delivery-logs)を参照）
* トラッキングログ：**NmsCleanup_TrackingLogPurgeDelay**（[トラッキングログのクリーンアップ](#cleanup-of-tracking-logs)を参照）
* 削除された配信：**NmsCleanup_RecycledDeliveryPurgeDelay**（[削除またはリサイクルする配信のクリーンアップ](#cleanup-of-deliveries-to-be-deleted-or-recycled)を参照）
* 却下をインポート：**NmsCleanup_RejectsPurgeDelay**（[インポートによって生成された却下のクリーンアップ](#cleanup-of-rejects-generated-by-imports-)を参照）
* 訪問者プロファイル：**NmsCleanup_VisitorPurgeDelay**（[訪問者のクリーンアップ](#cleanup-of-visitors)を参照）
* オファーの提案：**NmsCleanup_PropositionPurgeDelay**（[提案のクリーンアップ](#cleanup-of-propositions)を参照）

   >[!NOTE]
   >
   >**[!UICONTROL オファーの提案]**&#x200B;フィールドは、**インタラクション**&#x200B;モジュールがインストールされている場合にのみ使用できます。

* イベント：**NmsCleanup_EventPurgeDelay**（[期限切れのイベントのクレンジング](#cleansing-expired-events)を参照）
* アーカイブしたイベント：**NmsCleanup_EventHistoPurgeDelay**（[期限切れのイベントのクレンジング](#cleansing-expired-events)を参照）

   >[!NOTE]
   >
   >**[!UICONTROL イベント]**&#x200B;および&#x200B;**[!UICONTROL アーカイブされたイベント]**&#x200B;フィールドは、**Message Center**&#x200B;モジュールがインストールされている場合にのみ使用できます。

* 監査記録：**XtkCleanup_AuditTrailPurgeDelay**（[監査記録のクリーンアップ](#cleanup-of-audit-trail)を参照）

**[!UICONTROL データベースクリーンアップ]**&#x200B;ワークフローで実行されるすべてのタスクについて、以下の節で説明します。

## データベースクリーンアップワークフローで実行されるタスク {#tasks-carried-out-by-the-database-cleanup-workflow}

ワークフロースケジューラーで定義された日時（[スケジューラー](#the-scheduler)を参照）に、ワークフローエンジンがデータベースのクリーンアッププロセスを開始します。 データベースクリーンアップは、データベースに接続し、以下に示す順序でタスクを実行します。

>[!IMPORTANT]
>
>これらのタスクの1つが失敗した場合、次のタスクは実行されません。\
>**LIMIT**&#x200B;属性を持つSQLクエリは、すべての情報が処理されるまで繰り返し実行されます。

>[!NOTE]
>
>以下の節では、データベースクリーンアップワークフローで実行されるタスクについて説明します。これらのタスクは、SQL言語に詳しいデータベース管理者やユーザー向けに用意されています。

### クリーンアップを削除するリスト {#lists-to-delete-cleanup}

**[!UICONTROL データベースクリーンアップ]**&#x200B;ワークフローで最初に実行されたタスクは、**deleteStatus !=** NmsGroup **の0**&#x200B;属性。 これらのグループにリンクされ、他のテーブルに存在するレコードも削除されます。

1. 削除するリストは、次のSQLクエリを使用して復元されます。

   ```
   SELECT iGroupId, sLabel, iType FROM NmsGroup WHERE iDeleteStatus <> 0 OR tsExpirationDate <= GetDate() 
   ```

1. 各リストは、他のテーブルへのリンクを複数持ちます。 次のクエリを使用して、これらのリンクがすべて一括削除されます。

   ```
   DELETE FROM $(relatedTable) WHERE iGroupId=$(l) IN (SELECT iGroupId FROM $(relatedTable) WHERE iGroupId=$(l) LIMIT 5000) 
   ```

   ここで、 **$(relatedTable)**&#x200B;は&#x200B;**NmsGroup**&#x200B;に関連するテーブルで、 **$(l)**&#x200B;はリスト識別子です。

1. リストが「リスト」タイプのリストの場合、次のクエリを使用して関連付けられたテーブルが削除されます。

   ```
   DROP TABLE grp$(l)
   ```

1. 操作で復元された&#x200B;**Select**&#x200B;タイプリストは、次のクエリを使用して削除されます。

   ```
   DELETE FROM NmsGroup WHERE iGroupId=$(l) 
   ```

   ここで、**$(l)**&#x200B;はリスト識別子です。

### 削除またはリサイクルする配信のクリーンアップ {#cleanup-of-deliveries-to-be-deleted-or-recycled}

このタスクは、削除またはリサイクルするすべての配信を削除します。

1. **[!UICONTROL データベースクリーンアップ]**&#x200B;ワークフローは、**deleteStatus**&#x200B;フィールドの値が&#x200B;**[!UICONTROL Yes]**&#x200B;または&#x200B;**[!UICONTROL Recycled]**&#x200B;で、削除日が&#x200B;**[!UICONTROL Deleted deliveries]**（**デプロイウィザードのnmsCleanup_RecycledDeliveryPurgeDelay**）フィールド。 詳しくは、[デプロイウィザード](#deployment-wizard)を参照してください。 この期間は、現在のサーバーの日付に基づいて計算されます。
1. タスクでは、ミッドソーシングサーバーごとに、削除する配信のリストを選択します。
1. **[!UICONTROL データベースクリーンアップ]**&#x200B;ワークフローは、配信ログ、添付ファイル、ミラーページ情報およびその他すべての関連データを削除します。
1. 配信を適切に削除する前に、ワークフローは次のテーブルからリンクされた情報を削除します。

   * 配信の除外テーブル(**NmsDlvExclusion**)では、次のクエリが使用されます。

      ```
      DELETE FROM NmsDlvExclusion WHERE iDeliveryId=$(l)
      ```

      **$(l)**&#x200B;は配信の識別子です。

   * クーポンテーブル(**NmsCouponValue**)では、次のクエリが使用されます（一括削除を含む）。

      ```
      DELETE FROM NmsCouponValue WHERE iMessageId IN (SELECT iMessageId FROM NmsCouponValue WHERE EXISTS (SELECT B.iBroadLogId FROM $(BroadLogTableName) B WHERE B.iDeliveryId = $(l) AND B.iBroadLogId = iMessageId ) LIMIT 5000)
      ```

      **$(l)**&#x200B;は配信の識別子です。

   * 配信ログテーブル(**NmsBroadlogXxx**)では、大量削除は20,000件のレコードのバッチで実行されます。
   * オファーの提案テーブル(**NmsPropositionXxx**)では、大量削除は20,000件のレコードのバッチで実行されます。
   * トラッキングログテーブル(**NmsTrackinglogXxx**)では、大量削除は20,000件のレコードのバッチで実行されます。
   * 配信フラグメントテーブル(**NmsDeliveryPart**)では、500,000件のレコードのバッチで一括削除が実行されます。 この表には、配信される残りのメッセージに関するパーソナライゼーション情報が含まれます。
   * ミラーページデータフラグメントテーブル(**NmsMirrorPageInfo**)では、期限切れの配信部分と完了またはキャンセルされた配信部分に対して、20,000件のレコードのバッチで一括削除が実行されます。 この表には、ミラーページの生成に使用されるすべてのメッセージに関するパーソナライゼーション情報が含まれます。
   * ミラーページ検索テーブル(**NmsMirrorPageSearch**)では、20,000レコードのバッチで大量削除が実行されます。 このテーブルは、**NmsMirrorPageInfo**&#x200B;テーブルに格納されたパーソナライゼーション情報にアクセスできる検索インデックスです。
   * バッチ処理ログテーブル(**XtkJobLog**)では、20,000件のレコードのバッチで一括削除が実行されます。 このテーブルには、削除する配信のログが含まれます。
   * 配信URLトラッキングテーブル(**NmsTrackingUrl**)では、次のクエリが使用されます。

      ```
      DELETE FROM NmsTrackingUrl WHERE iDeliveryId=$(l)
      ```

      **$(l)**&#x200B;は配信の識別子です。

      このテーブルには、削除される配信内の、トラッキングを有効にするURLが含まれています。

1. 配信が配信テーブル(**NmsDelivery**)から削除されます。

   ```
   DELETE FROM NmsDelivery WHERE iDeliveryId = $(l)
   ```

   **$(l)**&#x200B;は配信の識別子です。

#### ミッドソーシングを使用した配信 {#deliveries-using-mid-sourcing}

**[!UICONTROL データベースクリーンアップ]**&#x200B;ワークフローは、ミッドソーシングサーバー上の配信も削除します。

1. これをおこなうには、ワークフローで、（ステータスに基づいて）各配信が非アクティブであることを確認します。 アクティブな配信は、削除される前に停止されます。 チェックは、次のクエリを実行して実行されます。

   ```
   SELECT iState FROM NmsDelivery WHERE iDeliveryId = $(l) AND iState <> 100;
   ```

   **$(l)**&#x200B;は配信の識別子です。

1. ステータスの値が&#x200B;**[!UICONTROL 開始保留中]** 、 **[!UICONTROL 処理中]** 、 **[!UICONTROL 回復待ち]** 、 **[!UICONTROL 回復中]** 、 **[!UICONTROL 一時停止要求]** 、 **[!UICONTROL 進行中]**&#x200B;の場合または&#x200B;**[!UICONTROL 一時停止]**（値51、55、61、62、71、72、75）、配信が停止し、タスクがリンクされた情報を削除します。

### 期限切れの配信のクリーンアップ {#cleanup-of-expired-deliveries}

このタスクは、有効期間が切れた配信を停止します。

1. **[!UICONTROL データベースクリーンアップ]**&#x200B;ワークフローは、期限切れの配信のリストを作成します。 このリストには、ステータスが&#x200B;**[!UICONTROL 完了]**&#x200B;以外の期限切れの配信と、処理されていないメッセージが10,000件を超える最近停止された配信が含まれます。 次のクエリが使用されます。

   ```
   SELECT iDeliveryId, iState FROM NmsDelivery WHERE iDeleteStatus=0 AND iIsModel=0 AND iDeliveryMode=1 AND ( (iState >= 51 AND iState < 85 AND tsValidity IS NOT NULL AND tsValidity < $(currentDate) ) OR (iState = 85 AND DateMinusDays(15) < tsLastModified AND iToDeliver - iProcessed >= 10000 ))
   ```

   **配信モード1**&#x200B;は&#x200B;**[!UICONTROL 一括配信]**&#x200B;モード、**状態51**&#x200B;は&#x200B;**[!UICONTROL 開始保留]**&#x200B;状態、**状態85**&#x200B;は&#x200B;**[!UICONTROL 停止]**&#x200B;状態、配信サーバー上で一括更新された配信ログの最大数が10,000に等しい。

1. 次に、ミッドソーシングを使用する最近期限切れの配信のリストがワークフローに含まれます。 ミッドソーシングサーバー経由で配信ログがまだ復元されていない配信は除外されます。

   次のクエリが使用されます。

   ```
   SELECT iDeliveryId, tsValidity, iMidRemoteId, mData FROM NmsDelivery WHERE (iDeliveryMode = 4 AND (iState = 85 OR iState = 95) AND tsValidity IS NOT NULL AND (tsValidity < SubDays(GetDate() , 15) OR tsValidity < $(DateOfLastLogPullUp)) AND tsLastModified > SubDays(GetDate() , 15))
   ```

1. 次のクエリは、日付で配信をフィルタリングするために、外部アカウントがアクティブかどうかを検出するために使用します。

   ```
   SELECT iExtAccountId FROM NmsExtAccount WHERE iActive<>0 AND sName=$(providerName)
   ```

1. 期限切れの配信のリストで、ステータスが&#x200B;**[!UICONTROL 保留中]**&#x200B;の配信ログを&#x200B;**[!UICONTROL 配信がキャンセル]**&#x200B;に切り替え、このリストにあるすべての配信を&#x200B;**[!UICONTROL 完了]**&#x200B;に切り替えます。

   次のクエリが使用されます。

   ```
   UPDATE $(BroadLogTableName) SET tsLastModified=$(curdate), iStatus=7, iMsgId=$(bl) WHERE iDeliveryId=$(dl) AND iStatus=6
   ```

   **$(curdate)**&#x200B;はデータベースサーバーの現在の日付、**$(bl)**&#x200B;は配信ログメッセージの識別子、**$(dl)**&#x200B;は配信識別子、**配信ステータス6**&#x200B;は&#x200B;**[!UICONTROL 保留]**&#x200B;ステータスと&#x200B;**配信ステータス7**&#x200B;は、「**[!UICONTROL 配信がキャンセルされました]**」ステータスに一致します。

   ```
   UPDATE NmsDelivery SET iState = 95, tsLastModified = $(curdate), tsBroadEnd = tsValidity WHERE iDeliveryId = $(dl)
   ```

   **配信状態95**&#x200B;は&#x200B;**[!UICONTROL 完了]**&#x200B;ステータスと一致し、**$(dl)**&#x200B;は配信の識別子です。

1. 古い配信のすべてのフラグメント(**deliveryParts**)が削除され、進行中の通知配信の古いフラグメントがすべて削除されます。 一括削除は、両方のタスクに使用されます。

   次のクエリが使用されます。

   ```
   DELETE FROM NmsDeliveryPart WHERE iDeliveryPartId IN (SELECT iDeliveryPartId FROM NmsDeliveryPart WHERE iDeliveryId IN (SELECT iDeliveryId FROM NmsDelivery WHERE iState=95 OR iState=85) LIMIT 5000)
   ```

   ```
   DELETE FROM NmsDeliveryPart WHERE iDeliveryPartId IN (SELECT iDeliveryPartId FROM NmsDeliveryPart WHERE tsValidity < $(curDate) LIMIT 500000)
   ```

   **配信状態95**&#x200B;は&#x200B;**[!UICONTROL 完了]**&#x200B;ステータスに、**配信状態85**&#x200B;は&#x200B;**[!UICONTROL 停止]**&#x200B;ステータスに、**$(curDate)**&#x200B;は現在のサーバー日に一致します。

### ミラーページのクリーンアップ {#cleanup-of-mirror-pages}

このタスクでは、配信で使用されているWebリソース（ミラーページ）を削除します。

1. まず、パージされる配信のリストは、次のクエリを使用して復元します。

   ```
   SELECT iDeliveryId, iNeedMirrorPage FROM NmsDelivery WHERE iWebResPurged = 0 AND tsWebValidity IS NOT NULL AND tsWebValidity < $(curdate)"
   ```

   ここで、**$(curDate)**&#x200B;は現在のサーバーの日付です。

1. 必要に応じて、以前に復元した配信の識別子を使用して、 **NmsMirrorPageInfo**&#x200B;テーブルがパージされます。 一括削除は、次のクエリを生成するために使用されます。

   ```
   DELETE FROM NmsMirrorPageInfo WHERE iMirrorPageInfoId IN (SELECT iMirrorPageInfoId FROM NmsMirrorPageInfo WHERE iDeliveryId = $(dl)) LIMIT 5000)
   ```

   ```
   DELETE FROM NmsMirrorPageSearch WHERE iMessageId IN (SELECT iMessageId FROM NmsMirrorPageSearch WHERE iDeliveryId = $(dl)) LIMIT 5000)
   ```

   **$(dl)**&#x200B;は配信の識別子です。

1. エントリが配信ログに追加されます。
1. パージされた配信は識別され、後で再処理する必要がなくなります。 次のクエリが実行されます。

   ```
   UPDATE NmsDelivery SET iWebResPurged = 1 WHERE iDeliveryId IN ($(strIn))
   ```

   ここで、**$(strIn)**&#x200B;は配信識別子のリストです。

### 作業用テーブルのクリーンアップ {#cleanup-of-work-tables}

このタスクは、ステータスが&#x200B;**[!UICONTROL 編集中]** 、 **[!UICONTROL 停止]**&#x200B;または&#x200B;**[!UICONTROL 削除]**&#x200B;の配信に一致するすべての作業用テーブルをデータベースから削除します。

1. 名前が&#x200B;**wkDlv_**&#x200B;で始まるテーブルのリストは、まず次のクエリ(postgresql)を使用して復元されます。

   ```
   SELECT relname FROM pg_class WHERE relname LIKE Lower('wkDlv_') ESCAPE E'\\' AND relkind IN ('r','v') AND pg_get_userbyid(relowner)<>'postgres'
   ```

1. その後、進行中のワークフローで使用されるテーブルが除外されます。 これをおこなうには、進行中の配信のリストを、次のクエリを使用して復元します。

   ```
   SELECT iDeliveryId FROM NmsDelivery WHERE iDeliveryId<>0 AND iDeleteStatus=0 AND iState NOT IN (0,85,100);
   ```

   ここで、0は&#x200B;**[!UICONTROL 編集中の]**&#x200B;配信ステータスに一致する値、85は&#x200B;**[!UICONTROL 停止中の]**&#x200B;ステータス、100は&#x200B;**[!UICONTROL 削除済みの]**&#x200B;ステータスに一致します。

1. 使用されなくなったテーブルは、次のクエリを使用して削除されます。

   ```
   DROP TABLE wkDlv_15487_1;
   ```

### インポートによって生成された却下のクリーンアップ {#cleanup-of-rejects-generated-by-imports-}

この手順を使用すると、インポート中にすべてのデータが処理されなかったレコードを削除できます。

1. 一括削除は、次のクエリを使用して&#x200B;**XtkReject**&#x200B;テーブルに対して実行されます。

   ```
   DELETE FROM XtkReject WHERE iRejectId IN (SELECT iRejectId FROM XtkReject WHERE tsLog < $(curDate)) LIMIT $(l))
   ```

   ここで、 **$(curDate)**&#x200B;は、**NmsCleanup_RejectsPurgeDelay**&#x200B;オプションに定義した期間を差し引いた現在のサーバー日付です（[Deployment wizard](#deployment-wizard)を参照）。**$(l)**&#x200B;は、質量の最大レコード数削除されました。

1. すべてのオーファン却下は、次のクエリを使用して削除されます。

   ```
   DELETE FROM XtkReject WHERE iJobId NOT IN (SELECT iJobId FROM XtkJob)
   ```

### ワークフローインスタンスのクリーンアップ {#cleanup-of-workflow-instances}

このタスクは、識別子(**lWorkflowId**)と履歴(**lHistory**)を使用して各ワークフローインスタンスを削除します。 作業用テーブルのクリーンアップタスクを再実行すると、非アクティブなテーブルが削除されます。 また、削除されたワークフローの孤立した作業用テーブル（wkf%とwkfhisto%）もすべて削除されます。

>[!NOTE]
>
>履歴のパージ頻度は、「**History in days**」フィールド（デフォルト値は30日）で各ワークフローに対して指定します。 このフィールドは、ワークフロープロパティの「**実行**」タブにあります。 詳しくは、[この節](../../workflow/using/workflow-properties.md#execution)を参照してください。

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

   ここで、 **$(lworkflow)**&#x200B;はワークフローの識別子、 **$(lhistory)**&#x200B;は履歴の識別子です。

1. 未使用のテーブルはすべて削除されます。 この目的のために、次のクエリ(postgresql)を使用する&#x200B;**wkf%**&#x200B;タイプのマスクを使用して、すべてのテーブルを収集します。

   ```
   SELECT relname FROM pg_class WHERE relname LIKE Lower('wkf%') ESCAPE E'\\' AND relkind IN ('r','v') AND pg_get_userbyid(relowner)<>'postgres'
   ```

1. その後、保留中のワークフローインスタンスで使用されるすべてのテーブルが除外されます。 アクティブなワークフローのリストは、次のクエリを使用して復元されます。

   ```
   SELECT iWorkflowId FROM XtkWorkflow WHERE iWorkflowId<>0 AND iState<>20
   ```

1. 各ワークフロー識別子が復元され、進行中のワークフローで使用されるテーブルの名前が確認されます。 これらの名前は、以前に復元したテーブルのリストから除外されます。
1. 「増分処理クエリ」タイプのアクティビティ履歴テーブルは、次のクエリを使用して除外されます。

   ```
   SELECT relname FROM pg_class WHERE relname LIKE Lower('wkfhisto%') ESCAPE E'\\' AND relkind IN ('r','v') AND pg_get_userbyid(relowner)<>'postgres'
   ```

   ```
   SELECT iWorkflowId FROM XtkWorkflow WHERE iWorkflowId IN ($(strCondition))
   ```

   ここで、**$(strcondition)**&#x200B;は、**wkfhisto%**&#x200B;マスクに一致するテーブルのリストです。

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

このタスクは、グループにリンクされた孤立した作業用テーブルを削除します。 **NmsGroup**&#x200B;テーブルには、クレンジング対象のグループ（0とは異なる型）が格納されます。 テーブル名のプレフィックスは&#x200B;**grp**&#x200B;です。 クレンジング対象のグループを識別するには、次のクエリを使用します。

```
SELECT iGroupId FROM NmsGroup WHERE iType>0"
```

### 訪問者のクリーンアップ {#cleanup-of-visitors}

このタスクでは、一括削除を使用して、古いレコードを訪問者テーブルから削除します。 古いレコードは、最後の変更がデプロイウィザードで定義された保存期間より前のものです（[デプロイウィザード](#deployment-wizard)を参照）。 次のクエリが使用されます。

```
DELETE FROM NmsVisitor WHERE iVisitorId IN (SELECT iVisitorId FROM NmsVisitor WHERE iRecipientId = 0 AND tsLastModified < AddDays(GetDate(), -30) AND iOrigin = 0 LIMIT 20000)
```

ここで、**$(tsDate)**&#x200B;は現在のサーバーの日付です。この日付から、**NmsCleanup_VisitorPurgeDelay**&#x200B;オプションに定義した期間を引きます。

### NPAIのクリーンアップ {#cleanup-of-npai}

このタスクを実行すると、有効なアドレスと一致するレコードを&#x200B;**NmsAddress**&#x200B;テーブルから削除できます。 一括削除の実行には、次のクエリが使用されます。

```
DELETE FROM NmsAddress WHERE iAddressId IN (SELECT iAddressId FROM NmsAddress WHERE iStatus=2 AND tsLastModified < $(tsDate1) AND tsLastModified >= $(tsDate2) LIMIT 5000)
```

**status 2**&#x200B;は&#x200B;**[!UICONTROL 有効な]**&#x200B;ステータスに一致し、**$(tsDate1)**&#x200B;は現在のサーバーの日付に一致します。**$(tsDate2)**&#x200B;は&#x200B;**NmsCleanup_LastCleanup**&#x200B;オプションに一致します。

### 購読のクリーンアップ {#cleanup-of-subscriptions-}

このタスクは、一括削除を使用して、ユーザーが&#x200B;**NmsSubscription**&#x200B;テーブルから削除したすべてのサブスクリプションを削除します。 次のクエリが使用されます。

```
DELETE FROM NmsSubscription WHERE iDeleteStatus <>0
```

### トラッキングログのクリーンアップ {#cleanup-of-tracking-logs}

このタスクは、トラッキングおよびWebトラッキングログテーブルから古いレコードを削除します。 古いレコードは、デプロイウィザードで定義された保存期間より前のレコードです（[デプロイウィザード](#deployment-wizard)を参照）。

1. まず、次のクエリを使用して、トラッキングログテーブルのリストを復元します。

   ```
   SELECT distinct(sTrackingLogSchema) FROM NmsDeliveryMapping WHERE sTrackingLogSchema IS NOT NULL;
   ```

1. 一括削除は、以前に復元したテーブルのリスト内のすべてのテーブルをパージするために使用します。 次のクエリが使用されます。

   ```
   DELETE FROM NmsTrackingLogRcp WHERE iTrackingLogId IN (SELECT iTrackingLogId FROM NmsTrackingLogRcp WHERE tsLog < $(tsDate) LIMIT 5000) 
   ```

   ここで、 **$(tsDate)**&#x200B;は、**NmsCleanup_TrackingLogPurgeDelay**&#x200B;オプションに定義した期間を差し引いた現在のサーバー日です。

1. トラッキング統計テーブルは、一括削除を使用してパージされます。 次のクエリが使用されます。

   ```
   DELETE FROM NmsTrackingStats WHERE iTrackingStatsId IN (SELECT iTrackingStatsId FROM NmsTrackingStats WHERE tsStart < $(tsDate) LIMIT 5000) 
   ```

   ここで、 **$(tsDate)**&#x200B;は、**NmsCleanup_TrackingStatPurgeDelay**&#x200B;オプションに定義した期間を差し引いた現在のサーバー日付です。

### 配信ログのクリーンアップ {#cleanup-of-delivery-logs}

このタスクでは、様々なテーブルに保存されている配信ログをパージできます。

1. この目的で、配信ログスキーマのリストは、次のクエリを使用して復元されます。

   ```
   SELECT distinct(sBroadLogSchema) FROM NmsDeliveryMapping WHERE sBroadLogSchema IS NOT NULL UNION SELECT distinct(sBroadLogExclSchema) FROM NmsDeliveryMapping WHERE sBroadLogExclSchema IS NOT NULL
   ```

1. ミッドソーシングを使用する場合、**NmsBroadLogMid**&#x200B;テーブルは配信マッピングで参照されません。 **nms:broadLogMid**&#x200B;スキーマが、前のクエリで復元されたリストに追加されます。
1. 次に、**データベースのクリーンアップ**&#x200B;ワークフローは、以前に復元したテーブルから古いデータを削除します。 次のクエリが使用されます。

   ```
   DELETE FROM $(tableName) WHERE iBroadLogId IN (SELECT iBroadLogId FROM $(tableName) WHERE tsLastModified < $(option) LIMIT 5000) 
   ```

   ここで、 **$(tableName)**&#x200B;はスキーマのリスト内の各テーブルの名前で、 **$(option)**&#x200B;は&#x200B;**NmsCleanup_BroadLogPurgeDelay**&#x200B;オプション用に定義された日付です（ [デプロイウィザード](#deployment-wizard)を参照）。

1. 最後に、ワークフローは、**NmsProviderMsgId**&#x200B;テーブルが存在するかどうかを確認します。 その場合、古いデータはすべて次のクエリを使用して削除されます。

   ```
   DELETE FROM NmsProviderMsgId WHERE iBroadLogId IN (SELECT iBroadLogId FROM NmsProviderMsgId WHERE tsCreated < $(option) LIMIT 5000)
   ```

   ここで、 **$(option)**&#x200B;は、 **NmsCleanup_BroadLogPurgeDelay**&#x200B;オプションに定義された日付と一致します（[デプロイウィザード](#deployment-wizard)を参照）。

### NmsEmailErrorStatテーブルのクリーンアップ {#cleanup-of-the-nmsemailerrorstat-table-}

このタスクは、**NmsEmailErrorStat**&#x200B;テーブルをクレンジングします。 メインプログラム(**coalesceErrors**)は、次の2つの日付を定義します。

* **開始日**:NmsLastErrorStatCoalesceオプションまたはテー **** ブル内の最新の日付に一致する次のプロセスの日付。
* **終了日**:現在のサーバーの日付。

開始日が終了日以上の場合、処理はおこなわれません。 この場合、 **coalesceUpToDate**&#x200B;メッセージが表示されます。

開始日が終了日より前の場合は、**NmsEmailErrorStat**&#x200B;テーブルがクレンジングされます。

**NmsEmailErrorStat**&#x200B;テーブル内の開始日と終了日の間のエラーの合計数は、次のクエリを使用して復元します。

```
"SELECT COUNT(*) FROM NmsEmailErrorStat WHERE tsDate>= $(start) AND tsDate< $(end)"
```

ここで、 **$end**&#x200B;と&#x200B;**$start**&#x200B;は、前に定義した開始日と終了日です。

合計が0より大きい場合：

1. 特定のしきい値（20に等しい）を超えるエラーのみを保持するために、次のクエリが実行されます。

   ```
   "SELECT iMXIP, iPublicId, SUM(iTotalConnections), SUM(iTotalErrors), SUM(iMessageErrors), SUM(iAbortedConnections), SUM(iFailedConnections), SUM(iRefusedConnections), SUM(iTimeoutConnections) FROM NmsEmailErrorStat WHERE tsDate>=$(start ) AND tsDate<$(end ) GROUP BY iMXIP, iPublicId HAVING SUM(iTotalErrors) >= 20"
   ```

1. **coalescingErrors**&#x200B;メッセージが表示されます。
1. 開始日と終了日の間に発生したすべてのエラーを削除する新しい接続が作成されます。 次のクエリが使用されます。

   ```
   "DELETE FROM NmsEmailErrorStat WHERE tsDate>=$(start) AND tsDate<$(end)"
   ```

1. 各エラーは、次のクエリを使用して&#x200B;**NmsEmailErrorStat**&#x200B;テーブルに保存されます。

   ```
   "INSERT INTO NmsEmailErrorStat(iMXIP, iPublicId, tsDate, iTotalConnections, iTotalErrors, iTimeoutConnections, iRefusedConnections, iAbortedConnections, iFailedConnections, iMessageErrors) VALUES($(lmxip ), $(lpublicId ), $(tsstart ), $(lconnections ), $(lconnectionErrors ),$(ltimeoutConnections ), $(lrefusedConnections ), $(labortedConnections ), $(lfailedConnections ), $(lmessageErrors))"
   ```

   各変数は、前のクエリで取得した値と一致します。

1. **start**&#x200B;変数が、前のプロセスの値で更新され、ループが終了します。

ループとタスクが停止します。

クリーンアップは、**NmsEmailError**&#x200B;テーブルと&#x200B;**cleanupNmsMxDomain**&#x200B;テーブルで実行されます。

### NmsEmailErrorテーブルのクリーンアップ {#cleanup-of-the-nmsemailerror-table-}

次のクエリが使用されます。

```
DELETE FROM NmsEmailError WHERE iMXIP NOT IN (SELECT DISTINCT iMXIP FROM NmsEmailErrorStat)
```

このクエリは、**NmsEmailErrorStat**&#x200B;内のリンクされたレコードを持たない行を&#x200B;**NmsEmailError**&#x200B;テーブルからすべて削除します。

### NmsMxDomainテーブルのクリーンアップ {#cleanup-of-the-nmsmxdomain-table-}

次のクエリが使用されます。

```
DELETE FROM NmsMxDomain WHERE iMXIP NOT IN (SELECT DISTINCT iMXIP FROM NmsEmailErrorStat)
```

このクエリは、**NmsEmailErrorStat**&#x200B;テーブル内のリンクされたレコードを持たない行を、**NmsMxDomain**&#x200B;テーブルからすべて削除します。

### 提案のクリーンアップ {#cleanup-of-propositions}

**インタラクション**&#x200B;モジュールがインストールされている場合、このタスクが実行され、**NmsPropositionXxx**&#x200B;テーブルがパージされます。

提案テーブルのリストが復元され、次のクエリを使用して、各提案テーブルに対して一括削除が実行されます。

```
DELETE FROM NmsPropositionXxx WHERE iPropositionId IN (SELECT iPropositionId FROM NmsPropositionXxx WHERE tsLastModified < $(option) LIMIT 5000) 
```

ここで、 **$(option)**&#x200B;は、 **NmsCleanup_PropositionPurgeDelay**&#x200B;オプション用に定義された日付です（[デプロイウィザード](#deployment-wizard)を参照）。

### シミュレーションテーブルのクリーンアップ {#cleanup-of-simulation-tables}

このタスクは、孤立したシミュレーションテーブル（オファーのシミュレーションや配信のシミュレーションにリンクされなくなったテーブル）を消去します。

1. クリーンアップが必要なシミュレーションのリストを復元するには、次のクエリを使用します。

   ```
   SELECT iSimulationId FROM NmsSimulation WHERE iSimulationId<>0
   ```

1. 削除するテーブルの名前は、 **wkSimu_**&#x200B;プレフィックスに続くシミュレーションの識別子で構成されます(例：**wkSimu_456831_aggr**):

   ```
   DROP TABLE wkSimu_456831_aggr
   ```

### 監査記録のクリーンアップ {#cleanup-of-audit-trail}

次のクエリが使用されます。

```
DELETE FROM XtkAudit WHERE tsChanged < $(tsDate)
```

ここで、 **$(tsDate)**&#x200B;は、**XtkCleanup_AuditTrailPurgeDelay**&#x200B;オプションに定義した期間が停止される現在のサーバーの日付です。

### Nmsaddressのクリーンアップ {#cleanup-of-nmsaddress}

次のクエリが使用されます。

```
DELETE FROM NmsAddress WHERE iAddressId IN (SELECT iAddressId FROM NmsAddress WHERE iStatus=STATUS_QUARANTINE AND tsLastModified < $(NmsCleanup_AppSubscriptionRcpPurgeDelay + 5d) AND iType IN (MESSAGETYPE_IOS, MESSAGETYPE_ANDROID ) LIMIT 5000)
```

このクエリは、iOSとAndroidに関連するすべてのエントリを削除します。

### 統計の更新とストレージの最適化 {#statistics-update}

**XtkCleanup_NoStats**&#x200B;オプションを使用すると、クリーンアップワークフローのストレージ最適化手順の動作を制御できます。

**XtkCleanup_NoStats**&#x200B;オプションが存在しない場合、またはその値が0の場合は、PostgreSQLの詳細モード(VACUUM VERBOSE ANALYZE)でストレージの最適化が実行され、他のすべてのデータベースの統計が更新されます。 このコマンドが実行されることを確認するには、PostgreSQLのログを確認します。 VACUUMは、次の形式で行を出力します。`INFO: vacuuming "public.nmsactivecontact"`とANALYZEは、次の形式で行を出力します。`INFO: analyzing "public.nmsactivecontact"`.

このオプションの値が1の場合、統計の更新はどのデータベースでも実行されません。 次のログ行がワークフローログに表示されます。`Option 'XtkCleanup_NoStats' is set to '1'`.

オプションの値が2の場合、PostgreSQLの詳細モード(ANALYZE VERBOSE)でストレージ分析が実行され、他のすべてのデータベースの統計が更新されます。 このコマンドが実行されることを確認するには、PostgreSQLのログを確認します。 ANALYZEは、次の形式で行を出力します。`INFO: analyzing "public.nmsactivecontact"`.

### サブスクリプションクリーンアップ(NMAC) {#subscription-cleanup--nmac-}

このタスクは、削除されたサービスまたはモバイルアプリケーションに関連する購読をすべて削除します。

broadlogスキーマのリストを復元するには、次のクエリを使用します。

```
SELECT distinct(sBroadLogSchema) FROM NmsDeliveryMapping WHERE sBroadLogSchema IS NOT NULL
```

次に、このタスクは、**appSubscription**&#x200B;リンクにリンクされたテーブルの名前を復元し、これらのテーブルを削除します。

また、このクリーンアップワークフローでは、**NmsCleanup_AppSubscriptionRcpPurgeDelay**&#x200B;オプションで設定された時間以降に更新されていない無効= 1のエントリもすべて削除します。

### セッション情報のクレンジング {#cleansing-session-information}

このタスクは、**sessionInfo**&#x200B;テーブルから情報をクレンジングします。次のクエリが使用されます。

```
 DELETE FROM XtkSessionInfo WHERE tsexpiration < $(curdate) 
```

### 有効期限切れのイベントのクレンジング {#cleansing-expired-events}

このタスクは、実行インスタンスで受信および保存されたイベントと、コントロールインスタンスでアーカイブされたイベントをクレンジングします。

### クレンジング反応 {#cleansing-reactions}

このタスクは、仮説自体が削除された反応（テーブル&#x200B;**NmsRemaMatchRcp**）をクレンジングします。
