---
title: データベースクリーンアップワークフロー
description: 古いデータが自動的にクリーンアップされる方法を説明します。
page-status-flag: never-activated
uuid: a7478641-cdf6-4bd4-9dd7-0c84416c9de6
contentOwner: sauviat
products: SG_CAMPAIGN/CLASSIC
audience: production
content-type: reference
topic-tags: data-processing
discoiquuid: 6b188d78-abb4-4f03-80b9-051ce960f43c
translation-type: tm+mt
source-git-commit: 2a82493deada11cb22ef37d215b6eae8274ce890
workflow-type: tm+mt
source-wordcount: '2997'
ht-degree: 2%

---


# データベースクリーンアップワークフロー{#database-cleanup-workflow}

## はじめに {#introduction}

**[!UICONTROL 管理／プロダクション／テクニカルワークフロー]**&#x200B;ノードからアクセスできる&#x200B;**[!UICONTROL データベースクリーンアップ]**&#x200B;ワークフローを使用すると、古いデータを削除して、データベースの急激な増加を回避できます。ワークフローは、ユーザーの操作なしで自動的にトリガーされます。

![](assets/ncs_cleanup_workflow.png)

## 設定 {#configuration}

データベースのクリーンアップは次の2つのレベルで構成されます。」をクリックします。

### ワークフロースケジューラー {#the-scheduler}

>[!NOTE]
>
>スケジューラーについて詳しくは、[この節](../../workflow/using/scheduler.md)を参照してください。

デフォルトでは、 **[!UICONTROL Database cleanup]** workflowは毎日午前4時に開始するように設定されています。 スケジューラーを使用すると、ワークフローのトリガー頻度を変更できます。 次の頻度を使用できます。

* **[!UICONTROL 1 日に数回]**
* **[!UICONTROL 日次]**
* **[!UICONTROL 毎週]**
* **[!UICONTROL 1 回]**

![](assets/ncs_cleanup_scheduler.png)

>[!CAUTION]
>
>スケジューラーで定義された日時に **[!UICONTROL Database cleanup]** workflowを開始するには、ワークフローエンジン(wfserver)を起動する必要があります。 そうでない場合、データベースのクレンジングは、次回ワークフローエンジンが起動するまで行われません。

### デプロイメントウィザード {#deployment-wizard}

**[!UICONTROL デプロイメントウィザード]**( **[!UICONTROL ツール/詳細]** メニューからアクセス)では、データの保存期間を設定できます。 値は日単位で表します。 これらの値を変更しない場合、ワークフローではデフォルト値が使用されます。

![](assets/ncs_cleanup_deployment-wizard.png)

[データの **[!UICONTROL 削除]** ]ウィンドウのフィールドは、次のオプションと一致します。 これらは、 **[!UICONTROL Database cleanup]** workflowで実行されるタスクの一部で使用されます。

* 統合トラッキング： **NmsCleanup_TrackingStatPurgeDelay** (トラッキングログの [クリーンアップを参照](#cleanup-of-tracking-logs))
* 配信ログ: **NmsCleanup_BroadLogPurgeDelay** (配信ログの [クリーンアップを参照](#cleanup-of-delivery-logs))
* トラッキングログ: **NmsCleanup_TrackingLogPurgeDelay** (トラッキングログの [クリーンアップを参照](#cleanup-of-tracking-logs))
* 削除された配信: **NmsCleanup_RecycledDeliveryPurgeDelay** (削除またはリサイクルする配信の [クリーンアップを参照](#cleanup-of-deliveries-to-be-deleted-or-recycled))
* 拒否の読み込み： **NmsCleanup_RejectsPurgeDelay** (インポートによって生成された拒否の [クリーンアップを参照](#cleanup-of-rejects-generated-by-imports-))
* 訪問者プロファイル: **NmsCleanup_VisitorPurgeDelay** (訪問者の [クリーンアップを参照](#cleanup-of-visitors))
* オファーの提案: **NmsCleanup_PropositionPurgeDelay** (「提案の [クリーンアップ](#cleanup-of-propositions)」を参照)

   >[!NOTE]
   >
   >「 **[!UICONTROL オファーの提案]** 」フィールドは、インタラクション **** モジュールがインストールされている場合にのみ使用できます。

* イベント: **NmsCleanup_EventPurgeDelay** ( [クレンジングの有効期限切れイベントを参照](#cleansing-expired-events))
* アーカイブされたイベント: **NmsCleanup_EventHistoPurgeDelay** ( [クレンジングの有効期限切れイベントを参照](#cleansing-expired-events))

   >[!NOTE]
   >
   >「 **[!UICONTROL イベント]** 」フィールドと「 **[!UICONTROL アーカイブ済みのイベント]** 」フィールドは、 **Message Center** モジュールがインストールされている場合にのみ使用できます。

* 監査証跡： **XtkCleanup_AuditTrailPurgeDelay** (「Cleanup of Audit trail [](#cleanup-of-audit-trail)」を参照)

「 **[!UICONTROL Database cleanup]** workflow」で実行されるすべてのタスクについて、以下の節で説明します。

## データベースクリーンアップワークフローで実行されるタスク {#tasks-carried-out-by-the-database-cleanup-workflow}

ワークフロースケジューラーで定義された日時(スケジューラー [を参照](#the-scheduler))に、ワークフローエンジンはデータベースのクリーンアップ処理を開始します。 データベースのクリーンアップは、データベースに接続し、以下に示すシーケンスのタスクを実行します。

>[!CAUTION]
>
>これらのタスクの1つが失敗した場合、次のエラーは実行されません。\
>LIMIT **** 属性を持つSQLクエリは、すべての情報が処理されるまで繰り返し実行されます。

>[!NOTE]
>
>データベースのクリーンアップ・ワークフローで実行されるタスクについては、以下の節で説明します。データベース管理者またはSQL言語に詳しいユーザ向けに用意されています。

### クリーンアップを削除するリスト {#lists-to-delete-cleanup}

デー **[!UICONTROL タベースのクリーンアップ]****・ワークフローで最初に実行されたタスクは、deleteStatus != 0** attribute from the **NmsGroup**. これらのグループにリンクされ、他のテーブルに存在するレコードも削除されます。

1. 削除するリストは、次のSQLクエリを使用して回復します。

   ```
   SELECT iGroupId, sLabel, iType FROM NmsGroup WHERE iDeleteStatus <> 0 OR tsExpirationDate <= GetDate() 
   ```

1. 各リストには、他のテーブルへのリンクが複数あります。 これらのリンクはすべて、次のクエリを使用して一括で削除されます。

   ```
   DELETE FROM $(relatedTable) WHERE iGroupId=$(l) IN (SELECT iGroupId FROM $(relatedTable) WHERE iGroupId=$(l) LIMIT 5000) 
   ```

   ここで、 **$(relatedTable)** はNmsGroup **に関連するテーブルで、** $(l) **** はリストの識別子です。

1. リストが「リスト」タイプのリストの場合、次のクエリを使用して関連付けられたテーブルが削除されます。

   ```
   DROP TABLE grp$(l)
   ```

1. 操作によって回復されたすべての **Select** Typeリストは、次のクエリを使用して削除されます。

   ```
   DELETE FROM NmsGroup WHERE iGroupId=$(l) 
   ```

   ここで、 **$(l)** はリスト識別子です。

### 削除またはリサイクルする配信のクリーンアップ {#cleanup-of-deliveries-to-be-deleted-or-recycled}

このタスクは、削除またはリサイクルするすべての配信を削除します。

1. **[!UICONTROL Database Cleanup]** Workflowは、DeleteStatusの値がYesRecycledRecycledField ********************、deleteDateの値がYesRecycledDeleteDeletedFieldの値よりも前の配信を、DeleteDRetatabaseDDDDDelelyDDDDDelyDDDDのDDDの値よりも前の配信(DDDelilyDDDDDDDeliverelyDDeliveriveDelyDDelyDelyDDelyDelyDelyDelelyDelyDelyDely For more on this, refer to [Deployment wizard](#deployment-wizard). この期間は、現在のサーバーの日付に関連して計算されます。
1. タスクは、各ミッドソーシングサーバに対して、削除する配信のリストを選択する。
1. 「 **[!UICONTROL Database cleanup]** workflow」を使用すると、配信ログ、添付ファイル、ミラーページ情報、およびその他すべての関連データが削除されます。
1. 適切な場合は、配信を削除する前に、次の表のリンク情報を削除します。

   * 配信の除外テーブル(**NmsDlvExclusion**)では、次のクエリが使用されます。

      ```
      DELETE FROM NmsDlvExclusion WHERE iDeliveryId=$(l)
      ```

      ここで、 **$(l)** は配信の識別子です。

   * クーポンテーブル(**NmsCouponValue**)では、次のクエリが使用されます（一括削除の場合）。

      ```
      DELETE FROM NmsCouponValue WHERE iMessageId IN (SELECT iMessageId FROM NmsCouponValue WHERE EXISTS (SELECT B.iBroadLogId FROM $(BroadLogTableName) B WHERE B.iDeliveryId = $(l) AND B.iBroadLogId = iMessageId ) LIMIT 5000)
      ```

      ここで、 **$(l)** は配信の識別子です。

   * 配信・ログ・テーブル(**NmsBroadlogXxx**)では、大量削除は20,000件のレコードのバッチで実行されます。
   * オファーの提案テーブル(**NmsPropositionXxx**)では、大量削除は20,000件のレコードのバッチで実行されます。
   * 追跡ログテーブル(NmsTrackinglogXxx ****)では、大量削除は20,000件のレコードのバッチで実行されます。
   * 配信フラグメントテーブル(**NmsDeliveryPart**)では、大量削除は500,000件のレコードのバッチで実行されます。 次の表に、配信される残りのメッセージに関するパーソナライゼーション情報を示します。
   * ミラーページデータフラグメントテーブル(**NmsMirrorPageInfo**)では、大量削除は、期限切れの配信部分と、完了またはキャンセルされた部分に対して、20,000件のレコードのバッチで実行されます。 次の表に、ミラーページの生成に使用されるすべてのメッセージのパーソナライゼーション情報を示します。
   * ミラーページ検索テーブル(**NmsMirrorPageSearch**)では、大量削除は20,000件のレコードのバッチで実行されます。 このテーブルは、NmsMirrorPageInfoテーブルに保存されたパーソナライゼーション情報へのアクセスを提供する検索 **インデックス** 。
   * バッチ処理ログテーブル(**XtkJobLog**)では、大量削除は20,000件のレコードのバッチで実行されます。 次の表に、削除する配信のログを示します。
   * 配信URL追跡テーブル(**NmsTrackingUrl**)では、次のクエリが使用されます。

      ```
      DELETE FROM NmsTrackingUrl WHERE iDeliveryId=$(l)
      ```

      ここで、 **$(l)** は配信の識別子です。

      次の表に、削除対象の配信ーで検出されたURLを示して、そのユーザーの追跡を有効にします。

1. 配信が配信テーブル(**NmsDelivery**)から削除されます。

   ```
   DELETE FROM NmsDelivery WHERE iDeliveryId = $(l)
   ```

   ここで、 **$(l)** は配信の識別子です。

#### ミッドソーシングを使用する配信 {#deliveries-using-mid-sourcing}

[ **[!UICONTROL データベースのクリーンアップ]** ]ワークフローは、ミッドソーシングサーバ上の配信も削除します。

1. これを行うには、各配信が（そのステータスに基づいて）非アクティブであるかどうかを確認します。 配信がアクティブな場合は、削除前に停止されます。 チェックは、次のクエリを実行して実行されます。

   ```
   SELECT iState FROM NmsDelivery WHERE iDeliveryId = $(l) AND iState <> 100;
   ```

   ここで、 **$(l)** は配信の識別子です。

1. 状態の値が「 **[!UICONTROL 開始保留]** 」、「進行中」 **[!UICONTROL 、「回復待ち」]** 、「回復待ち」 **[!UICONTROL 、「進行中」、「回復待ち」、「進行中」、「復]****************** 帰中」、「復帰中」、「復帰中」、「一時停止中」、「進行中」、「一時停止中」、「配信」、「5」、「5」が停止し、タスクがリンクされた情報を削除します。

### 期限切れの配信のクリーンアップ {#cleanup-of-expired-deliveries}

このタスクは、有効期間が切れた配信を停止します。

1. 「 **[!UICONTROL Database cleanup]** 」ワークフローは、有効期限が切れた配信のリストを作成します。 このリストには、「 **** 完了」以外のステータスを持つすべての期限切れ配信と、10,000件を超える未処理のメッセージを持つ最近停止した配信が含まれます。 次のクエリが使用されます。

   ```
   SELECT iDeliveryId, iState FROM NmsDelivery WHERE iDeleteStatus=0 AND iIsModel=0 AND iDeliveryMode=1 AND ( (iState >= 51 AND iState < 85 AND tsValidity IS NOT NULL AND tsValidity < $(currentDate) ) OR (iState = 85 AND DateMinusDays(15) < tsLastModified AND iToDeliver - iProcessed >= 10000 ))
   ```

   **配信1** は **[!UICONTROL 質量配信モードに一致し、状態511は、状態51]** は、状態511は、状態 **開始状態5は、************** 状態8の保留状態に一致し、配信サーバは、停止状態最高配信ログ数は、10,000に一致する。

1. 次に、ミッドソーシングを使用する最近期限切れの配信のリストが含まれます。 ミッドソーシングサーバを介して配信ログがまだ回復されていない配信は除外されます。

   次のクエリが使用されます。

   ```
   SELECT iDeliveryId, tsValidity, iMidRemoteId, mData FROM NmsDelivery WHERE (iDeliveryMode = 4 AND (iState = 85 OR iState = 95) AND tsValidity IS NOT NULL AND (tsValidity < SubDays(GetDate() , 15) OR tsValidity < $(DateOfLastLogPullUp)) AND tsLastModified > SubDays(GetDate() , 15))
   ```

1. 次のクエリは、配信を日付でフィルタリングするために、外部アカウントがアクティブかどうかを検出するために使用します。

   ```
   SELECT iExtAccountId FROM NmsExtAccount WHERE iActive<>0 AND sName=$(providerName)
   ```

1. 期限切れの配信のリストでは、ステータスが **[!UICONTROL 保留中の配信ログ]** 、 **[!UICONTROL 配信に切り替えて取り消し]** 、このリスト内のすべての配信が **[!UICONTROL 完了に切り替わります]** 。

   次のクエリが使用されます。

   ```
   UPDATE $(BroadLogTableName) SET tsLastModified=$(curdate), iStatus=7, iMsgId=$(bl) WHERE iDeliveryId=$(dl) AND iStatus=6
   ```

   ここで、 **$(curdate)** は配信ログサーバの現在の日付 **、$()は配信配信のID、$()は配信メッセージのID、********************** $()はID ID、6は配信ステータス、7はキャンセルされた状態を表します。

   ```
   UPDATE NmsDelivery SET iState = 95, tsLastModified = $(curdate), tsBroadEnd = tsValidity WHERE iDeliveryId = $(dl)
   ```

   ここで、 **配信状態95** は **[!UICONTROL 完了]** ( **Finished** )ステータスと一致し、$(dl)は配信の識別子です。

1. 古い配信のすべてのフラグメント(**deliveryParts**)が削除され、進行中の通知配信の古いフラグメントがすべて削除されます。 これらの両方のタスクに対して、一括削除が使用されます。

   次のクエリが使用されます。

   ```
   DELETE FROM NmsDeliveryPart WHERE iDeliveryPartId IN (SELECT iDeliveryPartId FROM NmsDeliveryPart WHERE iDeliveryId IN (SELECT iDeliveryId FROM NmsDelivery WHERE iState=95 OR iState=85) LIMIT 5000)
   ```

   ```
   DELETE FROM NmsDeliveryPart WHERE iDeliveryPartId IN (SELECT iDeliveryPartId FROM NmsDeliveryPart WHERE tsValidity < $(curDate) LIMIT 500000)
   ```

   ここで、 **配信状態95** は **[!UICONTROL 完了状態]** 、 **配信状態855は** Finished状態を、 ******** Stopped状態、Stopped状態、Date(Date Date)は現在のサーバ日を表します。

### ミラーページのクリーンアップ {#cleanup-of-mirror-pages}

このタスクは、配信が使用するWebリソース(ミラーページ)を削除します。

1. まず、次のクエリを使用して、パージする配信のリストをリカバリします。

   ```
   SELECT iDeliveryId, iNeedMirrorPage FROM NmsDelivery WHERE iWebResPurged = 0 AND tsWebValidity IS NOT NULL AND tsWebValidity < $(curdate)"
   ```

   ここで、 **$(curDate)** は、現在のサーバーの日付です。

1. 次に、必要に応じて、以前にリカバリした **配信のIDを使用して、NmsMirrorPageInfo** テーブルをパージします。 一括削除は、次のクエリを生成するために使用します。

   ```
   DELETE FROM NmsMirrorPageInfo WHERE iMirrorPageInfoId IN (SELECT iMirrorPageInfoId FROM NmsMirrorPageInfo WHERE iDeliveryId = $(dl)) LIMIT 5000)
   ```

   ```
   DELETE FROM NmsMirrorPageSearch WHERE iMessageId IN (SELECT iMessageId FROM NmsMirrorPageSearch WHERE iDeliveryId = $(dl)) LIMIT 5000)
   ```

   ここで、 **$(dl)** は配信の識別子です。

1. エントリが配信ログに追加されます。
1. 次に、削除された配信が識別され、後で再処理する必要がなくなります。 次のクエリが実行されます。

   ```
   UPDATE NmsDelivery SET iWebResPurged = 1 WHERE iDeliveryId IN ($(strIn))
   ```

   ここで、 **$(strIn)** は配信識別子のリストです。

### 作業テーブルのクリーンアップ {#cleanup-of-work-tables}

このタスクは、ステータスが「編集中」、「 **[!UICONTROL 停止」]** 、または「 **[!UICONTROL 削除」の配信に一致するすべての作業テーブルをデータベースから削除します]****** 。

1. wkDlv_で始まる名前を持つテーブルのリストは、 **最初に次のクエリ** (postgresql)で回復されます。

   ```
   SELECT relname FROM pg_class WHERE relname LIKE Lower('wkDlv_') ESCAPE E'\\' AND relkind IN ('r','v') AND pg_get_userbyid(relowner)<>'postgres'
   ```

1. その後、進行中のワークフローが使用するテーブルは除外されます。 これを行うには、進行中の配信のリストを次のクエリを使用して回復します。

   ```
   SELECT iDeliveryId FROM NmsDelivery WHERE iDeliveryId<>0 AND iDeleteStatus=0 AND iState NOT IN (0,85,100);
   ```

   ここで、0は編集 **[!UICONTROL 中の]** 配信のステータスに一致する値、85は **[!UICONTROL 停止済みのステータスに一致し、100は]****** 削除済みのステータスに一致します。

1. 使用されなくなったテーブルは、次のクエリを使用して削除されます。

   ```
   DROP TABLE wkDlv_15487_1;
   ```

### インポートによって生成された拒否のクリーンアップ {#cleanup-of-rejects-generated-by-imports-}

この手順では、読み込み中にすべてのデータが処理されなかったレコードを削除できます。

1. XtkReject **** テーブルでは、次のクエリを使って一括削除が行われます。

   ```
   DELETE FROM XtkReject WHERE iRejectId IN (SELECT iRejectId FROM XtkReject WHERE tsLog < $(curDate)) LIMIT $(l))
   ```

   ここで、 **$(curDate)** は、NmsCleanup_RejectsPurgeDelay **オプションに定義した期間を引いた現在のサーバーの日付です(** Deploymentウィザード [を参照)。](#deployment-wizard)**** $(l)は、一括削除されるレコードの最大数です。

1. その後、すべてのオーファンの拒否は次のクエリを使用して削除されます。

   ```
   DELETE FROM XtkReject WHERE iJobId NOT IN (SELECT iJobId FROM XtkJob)
   ```

### ワークフローインスタンスのクリーンアップ {#cleanup-of-workflow-instances}

このタスクは、識別子(lWorkflowId **)と履歴(lHistory******)を使用して各ワークフローインスタンスを削除します。 この操作により、作業テーブルのクリーンアップタスクを再度実行して、非アクティブなテーブルが削除されます。 また、削除されたワークフローの親なし作業テーブル（wkf%およびwkfhisto%）もすべて削除されます。

>[!NOTE]
>
>履歴の削除頻度は、「 **History in days** （履歴の日数）」フィールドの各ワークフローに対して指定します（デフォルト値は30日）。 このフィールドは、ワークフロープロパティの「 **実行** 」タブにあります。 詳しくは、[この節](../../workflow/using/workflow-properties.md#execution)を参照してください。

1. 削除するワークフローのリストを回復するには、次のクエリを使用します。

   ```
   SELECT iWorkflowId, iHistory FROM XtkWorkflow WHERE iWorkflowId<>0
   ```

1. このクエリは、次のクエリを使用して、すべてのリンクされたログ、完了したタスク、および完了したイベントを削除するために使用されるワークフローのリストを生成します。

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

1. 未使用のテーブルはすべて削除されます。 この目的のために、すべてのテーブルは **wkf%** 型のマスクを使って次のクエリ(postgresql)を使って収集されます。

   ```
   SELECT relname FROM pg_class WHERE relname LIKE Lower('wkf%') ESCAPE E'\\' AND relkind IN ('r','v') AND pg_get_userbyid(relowner)<>'postgres'
   ```

1. 次に、保留中のワークフローインスタンスで使用されるすべてのテーブルが除外されます。 アクティブなワークフローのリストは、次のクエリを使用して回復します。

   ```
   SELECT iWorkflowId FROM XtkWorkflow WHERE iWorkflowId<>0 AND iState<>20
   ```

1. 次に、各ワークフロー識別子が復元され、進行中のワークフローが使用するテーブルの名前が見つかります。 これらの名前は、以前にリカバリされたテーブルのリストから除外されます。
1. 「インクリメンタルクエリ」タイプのアクティビティ履歴テーブルは、次のクエリを使用して除外されます。

   ```
   SELECT relname FROM pg_class WHERE relname LIKE Lower('wkfhisto%') ESCAPE E'\\' AND relkind IN ('r','v') AND pg_get_userbyid(relowner)<>'postgres'
   ```

   ```
   SELECT iWorkflowId FROM XtkWorkflow WHERE iWorkflowId IN ($(strCondition))
   ```

   ここで、 **$(strcondition)** は、wkfhisto% **** マスクに一致するテーブルのリストです。

1. 残りのテーブルは次のクエリを使用して削除されます。

   ```
   DROP TABLE wkf15487_12;
   ```

### ワークフローログインのクリーンアップ {#cleanup-of-workflow-logins}

このタスクは次のクエリを使用してワークフローログインを削除します。

```
DELETE FROM XtkWorkflowLogin WHERE iWorkflowId NOT IN (SELECT iWorkflowId FROM XtkWorkflow)
```

### 単独作業テーブルのクリーンアップ {#cleanup-of-orphan-work-tables}

このタスクは、グループにリンクされた単独の作業テーブルを削除します。 NmsGroup **** テーブルには、クリーンアップ対象のグループ（0とは異なる型）が格納されます。 テーブル名のプレフィックスは **grp**&#x200B;です。 クリーンアップするグループを識別するには、次のクエリを使用します。

```
SELECT iGroupId FROM NmsGroup WHERE iType>0"
```

### 訪問者のクリーンアップ {#cleanup-of-visitors}

このタスクは、一括削除を使用して、古いレコードを訪問者テーブルから削除します。 古いレコードは、最後の変更が配置ウィザードで定義された保存期間より前のものです( [配置ウィザードを参照](#deployment-wizard))。 次のクエリが使用されます。

```
DELETE FROM NmsVisitor WHERE iVisitorId IN (SELECT iVisitorId FROM NmsVisitor WHERE iRecipientId = 0 AND tsLastModified < AddDays(GetDate(), -30) AND iOrigin = 0 LIMIT 20000)
```

ここ **で、** $(tsDate) **は現在のサーバーの日付で、NmsCleanup_VisitorPurgeDelay** オプションに定義された期間を引きます。

### NPAIの浄化 {#cleanup-of-npai}

このタスクを使用すると、NmsAddressテー **ブルから有効なアドレスと一致するレコードを削除できます** 。 一括削除の実行には、次のクエリを使用します。

```
DELETE FROM NmsAddress WHERE iAddressId IN (SELECT iAddressId FROM NmsAddress WHERE iStatus=2 AND tsLastModified < $(tsDate1) AND tsLastModified >= $(tsDate2) LIMIT 5000)
```

ここで、 **status 2** は **[!UICONTROL Valid]** statusと一致し、$(tsDate) **は現在のサーバーの日付、$(tsDate1)は$(ts22)** は日付、日付、msmsCleanup_CleanupはValid ******** ステータスと一致します。

### 購読のクリーンアップ {#cleanup-of-subscriptions-}

このタスクは、ユーザーが削除したすべての購読をNmsSubscription **** テーブルから一括削除を使用して削除します。 次のクエリが使用されます。

```
DELETE FROM NmsSubscription WHERE iDeleteStatus <>0
```

### トラッキングログのクリーンアップ {#cleanup-of-tracking-logs}

このタスクは、追跡およびWeb追跡ログテーブルから古いレコードを削除します。 古いレコードは、配置ウィザードで定義された保存期間より前のものです( [配置ウィザードを参照](#deployment-wizard))。

1. 最初に、次のクエリを使用して、トラッキングログテーブルのリストが回復されます。

   ```
   SELECT distinct(sTrackingLogSchema) FROM NmsDeliveryMapping WHERE sTrackingLogSchema IS NOT NULL;
   ```

1. 一括削除は、以前にリカバリしたテーブルのリスト内のすべてのテーブルをパージするために使用します。 次のクエリが使用されます。

   ```
   DELETE FROM XtkTrackingLogRcp WHERE iTrackingLogId IN (SELECT iTrackingLogId FROM XtkTrackingLogRcp WHERE tsLog < $(tsDate) LIMIT 5000) 
   ```

   ここ **で** $(tsDate) **は、NmsCleanup_TrackingLogPurgeDelay** オプションに定義した期間を差し引いた、現在のサーバーの日付です。

1. 追跡統計テーブルは、一括削除を使用して削除されます。 次のクエリが使用されます。

   ```
   DELETE FROM NmsTrackingStats WHERE iTrackingStatsId IN (SELECT iTrackingStatsId FROM NmsTrackingStats WHERE tsStart < $(tsDate) LIMIT 5000) 
   ```

   ここ **で** $(tsDate) **は、NmsCleanup_TrackingStatPurgeDelay** オプションに定義した期間を差し引いた、現在のサーバーの日付です。

### 配信ログのクリーンアップ {#cleanup-of-delivery-logs}

このタスクを使用すると、様々なテーブルに保存されている配信ログを削除できます。

1. このため、配信ログスキーマのリストは、次のクエリを使用して回復されます。

   ```
   SELECT distinct(sBroadLogSchema) FROM NmsDeliveryMapping WHERE sBroadLogSchema IS NOT NULL UNION SELECT distinct(sBroadLogExclSchema) FROM NmsDeliveryMapping WHERE sBroadLogExclSchema IS NOT NULL
   ```

1. ミッドソーシングを使用する場合、 **NmsBroadLogMid** テーブルは配信マッピングで参照されません。 nms:broadLogMid **** スキーマは、前のクエリでリカバリされたリストに追加されます。
1. 次に、 **データベースのクリーンアップ** ・ワークフローは、以前にリカバリされたテーブルから古いデータを削除します。 次のクエリが使用されます。

   ```
   DELETE FROM $(tableName) WHERE iBroadLogId IN (SELECT iBroadLogId FROM $(tableName) WHERE tsLastModified < $(option) LIMIT 5000) 
   ```

   ここで、 **$(tableName)** はスキーマのリスト内の各テーブルの名前で、 **$(option)** はNmsCleanup_BroadLogPurgeDelay **オプションに対して定義された日付です(『**[](#deployment-wizard)Deployment Wizard』を参照)。

1. 最後に、ワークフローはNmsProviderMsgIdテーブルが存在するかどうかを確認 **します** 。 古いデータが含まれている場合は、次のクエリを使用して古いデータがすべて削除されます。

   ```
   DELETE FROM NmsProviderMsgId WHERE iBroadLogId IN (SELECT iBroadLogId FROM NmsProviderMsgId WHERE tsCreated < $(option) LIMIT 5000)
   ```

   ここで、 **$(option)** は、NmsCleanup_BroadLogPurgeDelay **オプションに対して定義された日付と一致します(** デプロイメントウィザードを参照 [](#deployment-wizard))。

### NmsEmailErrorStatテーブルのクリーンアップ {#cleanup-of-the-nmsemailerrorstat-table-}

このタスクは、 **NmsEmailErrorStat** テーブルをクリーンアップします。 メインプログラム(**coalesceErrors**)は2つの日付を定義します。

* **開始日**:NmsLastErrorStatCoalesce **オプションまたはテーブル内の最新の日付に一致する次のプロセスの日付** 。
* **終了日**:現在のサーバーの日付。

開始日が終了日以上の場合は、処理は行われません。 この場合、 **coalesceUpToDate** メッセージが表示されます。

開始日が終了日より前の場合、 **NmsEmailErrorStat** テーブルはクリーンアップされます。

開始日から終了日の間のNmsEmailErrorStat **** テーブルのエラーの合計数は、次のクエリを使用して回復されます。

```
"SELECT COUNT(*) FROM NmsEmailErrorStat WHERE tsDate>= $(start) AND tsDate< $(end)"
```

$end **と** $ **開始** は、以前に定義した開始と終了日です。

合計が0より大きい場合：

1. 特定のしきい値（20に等しい）を超えるエラーのみを保持するために、次のクエリが実行されます。

   ```
   "SELECT iMXIP, iPublicId, SUM(iTotalConnections), SUM(iTotalErrors), SUM(iMessageErrors), SUM(iAbortedConnections), SUM(iFailedConnections), SUM(iRefusedConnections), SUM(iTimeoutConnections) FROM NmsEmailErrorStat WHERE tsDate>=$(start ) AND tsDate<$(end ) GROUP BY iMXIP, iPublicId HAVING SUM(iTotalErrors) >= 20"
   ```

1. coalessingErrors **** メッセージが表示されます。
1. 開始と終了日の間に発生したすべてのエラーを削除する新しい接続が作成されます。 次のクエリが使用されます。

   ```
   "DELETE FROM NmsEmailErrorStat WHERE tsDate>=$(start) AND tsDate<$(end)"
   ```

1. 各エラーは、次のクエリを使用してNmsEmailErrorStat **** テーブルに保存されます。

   ```
   "INSERT INTO NmsEmailErrorStat(iMXIP, iPublicId, tsDate, iTotalConnections, iTotalErrors, iTimeoutConnections, iRefusedConnections, iAbortedConnections, iFailedConnections, iMessageErrors) VALUES($(lmxip ), $(lpublicId ), $(tsstart ), $(lconnections ), $(lconnectionErrors ),$(ltimeoutConnections ), $(lrefusedConnections ), $(labortedConnections ), $(lfailedConnections ), $(lmessageErrors))"
   ```

   各変数は、前のクエリで復元された値と一致します。

1. 開始 **** 変数は、前のプロセスの値で更新され、ループが終了します。

ループとタスクが停止します。

クリーンアップは、NmsEmailError **テーブルと** cleanupNmsMxDomain **** テーブルで実行されます。

### NmsEmailErrorテーブルのクリーンアップ {#cleanup-of-the-nmsemailerror-table-}

次のクエリが使用されます。

```
DELETE FROM NmsEmailError WHERE iMXIP NOT IN (SELECT DISTINCT iMXIP FROM NmsEmailErrorStat)
```

このクエリは、NmsEmailError **テーブルから、NmsEmailErrorStat****** 内のリンクされたレコードがない行をすべて削除します。

### NmsMxDomainテーブルのクリーンアップ {#cleanup-of-the-nmsmxdomain-table-}

次のクエリが使用されます。

```
DELETE FROM NmsMxDomain WHERE iMXIP NOT IN (SELECT DISTINCT iMXIP FROM NmsEmailErrorStat)
```

このクエリは、NmsMxDomainテー **ブルからNmsEmailErrorStat** テーブル内のリンクされたレコードのない行をすべて削除します **** 。

### 提案のクリーンアップ {#cleanup-of-propositions}

Interaction **Moduleがインストールされている場合、この** タスクはNmsPropositionXxx **** テーブルを削除するために実行されます。

次のクエリを用いて、プロポジションテーブルのリストを回復し、各テーブルに対して一括削除を行う。

```
DELETE FROM NmsPropositionXxx WHERE iPropositionId IN (SELECT iPropositionId FROM NmsPropositionXxx WHERE tsLastModified < $(option) LIMIT 5000) 
```

ここで、 **$(option)** はNmsCleanup_PropositionPurgeDelay **(** デプロイメントウィザードを参照 [](#deployment-wizard))オプションに定義された日付です。

### シミュレーションテーブルのクリーンアップ {#cleanup-of-simulation-tables}

このタスクは、孤立したシミュレーションテーブル(オファーシミュレーションまたは配信シミュレーションにリンクされなくなったテーブル)を削除します。

1. クリーンアップが必要なシミュレーションのリストを回復するには、次のクエリを使用します。

   ```
   SELECT iSimulationId FROM NmsSimulation WHERE iSimulationId<>0
   ```

1. 削除するテーブルの名前は、 **wkSimu_** プレフィックスに続いてシミュレーションのIDで構成されます(例： **wkSimu_456831_aggr**):

   ```
   DROP TABLE wkSimu_456831_aggr
   ```

### 監査証跡のクリーンアップ {#cleanup-of-audit-trail}

次のクエリが使用されます。

```
DELETE FROM XtkAudit WHERE tsChanged < $(tsDate)
```

ここで **$(tsDate)** は、XtkCleanup_AuditTrailPurgeDelay **** オプションに定義された期間が停止される現在のサーバーの日付です。

### Nmsaddressのクリーンアップ {#cleanup-of-nmsaddress}

次のクエリが使用されます。

```
DELETE FROM NmsAddress WHERE iAddressId IN (SELECT iAddressId FROM NmsAddress WHERE iStatus=STATUS_QUARANTINE AND tsLastModified < $(NmsCleanup_AppSubscriptionRcpPurgeDelay + 5d) AND iType IN (MESSAGETYPE_IOS, MESSAGETYPE_ANDROID ) LIMIT 5000)
```

このクエリは、iOSとAndroidに関連するすべてのエントリを削除します。

### 統計の更新とストレージの最適化 {#statistics-update}

XtkCleanup_ **NoStats** オプションを使用すると、クリーンアップワークフローのストレージ最適化手順の動作を制御できます。

XtkCleanup_NoStats **** オプションが存在しない場合、または値が0の場合、PostgreSQLでストレージの最適化(VACUUM VERBOSE ANALYZE)が実行され、他のすべてのデータベースの統計が更新されます。 このコマンドが実行されていることを確認するには、PostgreSQLログを調べます。 VACUUMは次の形式で行を出力します。 `INFO: vacuuming "public.nmsactivecontact"` とANALYZEは次の形式で行を出力します。 `INFO: analyzing "public.nmsactivecontact"`.

このオプションの値が1の場合、統計の更新はどのデータベースでも実行されません。 次のログ行がワークフローログに表示されます。 `Option 'XtkCleanup_NoStats' is set to '1'`.

このオプションの値が2の場合、ストレージ分析はPostgreSQLで冗長モード(ANALYZE VERBOSE)で実行され、他のすべてのデータベースで統計が更新されます。 このコマンドが実行されていることを確認するには、PostgreSQLログを調べます。 ANALYZEは次の形式で行を出力します。 `INFO: analyzing "public.nmsactivecontact"`.

### 購読のクリーンアップ(NMAC) {#subscription-cleanup--nmac-}

このタスクは、削除したサービスまたはモバイルアプリケーションに関連する購読をすべて削除します。

ブロードローグスキーマのリストを回復するには、次のクエリを使用します。

```
SELECT distinct(sBroadLogSchema) FROM NmsDeliveryMapping WHERE sBroadLogSchema IS NOT NULL
```

次に、タスクはappSubscriptionリンクにリンクされたテーブルの名前を復元し、 **これらのテーブルを削除します** 。

また、このクリーンアップワークフローは、NmsCleanup_AppSubscriptionRcpPurgeDelay **** オプションで設定された時刻以降に更新されていないdisabled = 1のエントリをすべて削除します。

### クレンジングセッション情報 {#cleansing-session-information}

このタスクは、 **sessionInfo** テーブルから情報を消去します。次のクエリが使用されます。

```
 DELETE FROM XtkSessionInfo WHERE tsexpiration < $(curdate) 
```

### クレンジング期限切れイベント {#cleansing-expired-events}

このタスクは、実行インスタンスに受け取って保存されたイベントと、コントロールインスタンスにアーカイブされたイベントを消去します。

### クレンジング反応 {#cleansing-reactions}

このタスクは、仮説自体が削除されたリアクション(テーブル **NmsRemaMatchRcp**)をクリーンアップします。
