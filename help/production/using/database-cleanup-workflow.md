---
title: データベースクリーンアップワークフロー
seo-title: データベースクリーンアップワークフロー
description: データベースクリーンアップワークフロー
seo-description: null
page-status-flag: never-activated
uuid: a7478641-cdf6-4bd4-9dd7-0c84416c9de6
contentOwner: sauviat
products: SG_CAMPAIGN/CLASSIC
audience: production
content-type: reference
topic-tags: data-processing
discoiquuid: 6b188d78-abb4-4f03-80b9-051ce960f43c
index: y
internal: n
snippet: y
translation-type: tm+mt
source-git-commit: d5813af76e3cad16d9094a19509dcb855e36c01f

---


# Database cleanup workflow{#database-cleanup-workflow}

## はじめに {#introduction}

ノードを **[!UICONTROL Database cleanup]** 介してアクセス可能なワ **[!UICONTROL Administration > Production > Technical workflows]** ークフローを使用すると、古いデータを削除して、データベースの指数的な増加を回避できます。 ワークフローは、ユーザーの操作なしで自動的にトリガーされます。

![](assets/ncs_cleanup_workflow.png)

## 設定 {#configuration}

データベースのクリーンアップは、次の2つのレベルで構成されます。」をクリックします。

### スケジューラ {#the-scheduler}

>[!NOTE]
>
>For more on the scheduler, refer to [this section](../../workflow/using/scheduler.md).

デフォルトでは、ワー **[!UICONTROL Database cleanup]** クフローは毎日午前4時に開始するように設定されています。 スケジューラーを使用すると、ワークフローのトリガー頻度を変更できます。 次の頻度を使用できます。

* **[!UICONTROL Several times a day]**
* **[!UICONTROL Daily]**
* **[!UICONTROL Weekly]**
* **[!UICONTROL Once]**

![](assets/ncs_cleanup_scheduler.png)

>[!CAUTION]
>
>ワークフローをスケジューラ **[!UICONTROL Database cleanup]** ーで定義された日時に開始するには、ワークフローエンジン(wfserver)を起動する必要があります。 そうでない場合、データベースのクレンジングは、次回ワークフローエンジンが起動するまで行われません。

### デプロイウィザード {#deployment-wizard}

メニュー **[!UICONTROL Deployment wizard]** からアクセス **[!UICONTROL Tools > Advanced]** できるので、データの保存期間を設定できます。 値は日単位で表されます。 これらの値が変更されない場合、ワークフローではデフォルト値が使用されます。

![](assets/ncs_cleanup_deployment-wizard.png)

ウィンドウのフィールド **[!UICONTROL Purge of data]** は、次のオプションと一致します。 これらは、ワークフローで実行される一部のタスクで使用さ **[!UICONTROL Database cleanup]** れます。

* 統合トラッキング：NmsCleanup_TrackingStatPurgeDelay **(トラッキングロ** グのクリーンアップを参照 [](#cleanup-of-tracking-logs))
* 配信ログ：NmsCleanup_ **BroadLogPurgeDelay** (配信ログのク [リーンアップを参照](#cleanup-of-delivery-logs))
* トラッキングログ：NmsCleanup_ **TrackingLogPurgeDelay** (トラッキングロ [グのクリーンアップを参照](#cleanup-of-tracking-logs))
* 配信の削除：NmsCleanup_RecycledDeliveryPurgeDelay **(削除またはリ** サイクルする配信のクリーンアップを参照 [](#cleanup-of-deliveries-to-be-deleted-or-recycled))
* 拒否の読み込み：NmsCleanup_RejectsPurgeDelay **(インポートによって生** 成された拒否のクリーンアップを参照 [](#cleanup-of-rejects-generated-by-imports-))
* 訪問者プロファイル：NmsCleanup_ **VisitorPurgeDelay** (訪問者のク [リーンアップを参照](#cleanup-of-visitors))
* オファーの提案：NmsCleanup_PropositionPurgeDelay **(提案のクリ** ーンアップを参照 [](#cleanup-of-propositions))

   >[!NOTE]
   >
   >このフィ **[!UICONTROL Offer propositions]** ールドは、インタラクションモジュールがインス **トールされ** ている場合にのみ使用できます。

* イベント：NmsCleanup_EventPurgeDelay **(期限切れのイベ** ントのクレンジングを参照 [](#cleansing-expired-events))
* アーカイブされたイベント：NmsCleanup_EventHistoPurgeDelay **(期限切れのイベ** ントのクレンジングを参照 [](#cleansing-expired-events))

   >[!NOTE]
   >
   >フィールド **[!UICONTROL Events]** とフィー **[!UICONTROL Archived events]** ルドは、 **Message Centerモジュールがインストールされている場合にのみ使用できます** 。

* 監査証跡： **XtkCleanup_AuditTrailPurgeDelay** (「監査トレール [のクリーンアップ](#cleanup-of-audit-trail)」を参照)

ワークフローで実行されるすべ **[!UICONTROL Database cleanup]** てのタスクについて、以下の節で説明します。

## データベースクリーンアップワークフローで実行されるタスク {#tasks-carried-out-by-the-database-cleanup-workflow}

ワークフロースケジューラーで定義された日時(スケジューラ [ーを参照](#the-scheduler))に、ワークフローエンジンはデータベースクリーンアッププロセスを開始します。 データベースクリーンアップは、データベースに接続し、以下に示す順序でタスクを実行します。

>[!CAUTION]
>
>これらのタスクの1つが失敗した場合、次のタスクは実行されません。\
>LIMIT属性を持つSQLクエリ **は** 、すべての情報が処理されるまで繰り返し実行されます。

>[!NOTE]
>
>データベースクリーンアップワークフローで実行されるタスクについて、以下の節は、データベース管理者またはSQL言語に詳しいユーザー向けに予約されています。

### クリーンアップを削除するリスト {#lists-to-delete-cleanup}

ワークフローによって実行される最初のタ **[!UICONTROL Database cleanup]****スクは、deleteStatus != NmsGroupの** 0属性 ****。 これらのグループにリンクされ、他のテーブルに存在するレコードも削除されます。

1. 削除するリストは、次のSQLクエリを使用してリカバリされます。

   ```
   SELECT iGroupId, sLabel, iType FROM NmsGroup WHERE iDeleteStatus <> 0 OR tsExpirationDate <= GetDate() 
   ```

1. 各リストには、他のテーブルへのリンクが複数あります。 これらのリンクはすべて、次のクエリを使用して一括で削除されます。

   ```
   DELETE FROM $(relatedTable) WHERE iGroupId=$(l) IN (SELECT iGroupId FROM $(relatedTable) WHERE iGroupId=$(l) LIMIT 5000) 
   ```

   ここ **で、$(relatedTable)** は **NmsGroupに関連するテーブルで、** $(l) **** はリスト識別子です。

1. リストが「リスト」タイプのリストの場合、次のクエリを使用して関連付けられたテーブルが削除されます。

   ```
   DROP TABLE grp$(l)
   ```

1. 操作によ **って回復された** [Select Type]リストは、次のクエリを使用して削除されます。

   ```
   DELETE FROM NmsGroup WHERE iGroupId=$(l) 
   ```

   ここ **で、$(l)** はリスト識別子です。

### 削除またはリサイクルする配信のクリーンアップ {#cleanup-of-deliveries-to-be-deleted-or-recycled}

このタスクにより、すべての配信が削除またはリサイクルされます。

1. ワークフ **[!UICONTROL Database cleanup]** ローは、 **deleteStatus** フィールドの値が指定されている配信、または削除日が、配置ウィザードの **[!UICONTROL Yes]** ( **[!UICONTROL Recycled]****[!UICONTROL Deleted deliveries]****** NmsNms_RecycledDeliveryDeliveryDelayPurgeDelay cleanupPurge)フィールドで定義された期間より前の配信を選択します。 For more on this, refer to [Deployment wizard](#deployment-wizard). この期間は、現在のサーバーの日付を基準にして計算されます。
1. タスクは、ミッドソーシングサーバーごとに、削除する配信のリストを選択します。
1. ワークフロー **[!UICONTROL Database cleanup]** は、配信ログ、添付ファイル、ミラーページ情報、およびその他すべての関連データを削除します。
1. 配信を適切に削除する前に、ワークフローは次の表からリンクされた情報を削除します。

   * 配信の除外テーブル(**NmsDlvExclusion**)では、次のクエリが使用されます。

      ```
      DELETE FROM NmsDlvExclusion WHERE iDeliveryId=$(l)
      ```

      ここ **で、** $(l)は配信の識別子です。

   * クーポンテーブル(**NmsCouponValue**)では、次のクエリが使用されます（一括削除を使用）。

      ```
      DELETE FROM NmsCouponValue WHERE iMessageId IN (SELECT iMessageId FROM NmsCouponValue WHERE EXISTS (SELECT B.iBroadLogId FROM $(BroadLogTableName) B WHERE B.iDeliveryId = $(l) AND B.iBroadLogId = iMessageId ) LIMIT 5000)
      ```

      ここ **で、** $(l)は配信の識別子です。

   * 配信ログテーブル(**NmsBroadlogXxx**)では、一括削除は10,000件のレコードのバッチで実行されます。
   * オファー提案テーブル(**NmsPropositionXxx**)では、一括削除は10,000件のレコードのバッチで実行されます。
   * トラッキングログテーブル(**NmsTrackinglogXxx**)では、大量削除は5,000件のレコードのバッチで実行されます。
   * 配信フラグメントテーブル(**NmsDeliveryPart**)では、5,000件のレコードのバッチで大量削除が実行されます。 この表には、配信される残りのメッセージに関するパーソナライゼーション情報が含まれています。
   * ミラーページデータフラグメントテーブル(**NmsMirrorPageInfo**)では、5,000件のレコードのバッチで大量削除が実行されます。 この表には、ミラーページの生成に使用されるすべてのメッセージに関するパーソナライゼーション情報が含まれています。
   * ミラーページ検索テーブル(**NmsMirrorPageSearch**)では、5,000件のレコードのバッチで大量削除が実行されます。 このテーブルは、NmsMirrorPageInfoテーブルに保存されたパーソナライゼーション情報にアクセスできる検索イ **ンデックス** 。
   * バッチ処理ログテーブル(**XtkJobLog**)では、5,000件のレコードのバッチで大量削除が実行されます。 この表には、削除する配信のログが含まれます。
   * 配信URL追跡テーブル(**NmsTrackingUrl**)では、次のクエリが使用されます。

      ```
      DELETE FROM NmsTrackingUrl WHERE iDeliveryId=$(l)
      ```

      ここ **で、** $(l)は配信の識別子です。

      この表には、削除する配信で見つかったURLが含まれ、そのURLの追跡が有効になります。

1. 配信が配信テーブル(**NmsDelivery**)から削除されます。

   ```
   DELETE FROM NmsDelivery WHERE iDeliveryId = $(l)
   ```

   ここ **で、** $(l)は配信の識別子です。

#### ミッドソーシングを使用した配信 {#deliveries-using-mid-sourcing}

ワークフロー **[!UICONTROL Database cleanup]** は、ミッドソーシングサーバー上の配信も削除します。

1. これを行うには、ワークフローは各配信が非アクティブであることを（状態に基づいて）確認します。 配信がアクティブな場合は、削除される前に停止されます。 チェックは、次のクエリを実行して実行されます。

   ```
   SELECT iState FROM NmsDelivery WHERE iDeliveryId = $(l) AND iState <> 100;
   ```

   ここ **で、** $(l)は配信の識別子です。

1. ステータスの値が、、、、、、 **[!UICONTROL Start pending]** 、、、、、 **[!UICONTROL In progress]** 、 **[!UICONTROL Recovery pending]** 、、、または **[!UICONTROL Recovery in progress]****[!UICONTROL Pause requested]****[!UICONTROL Pause in progress]****[!UICONTROL Paused]** （値51、55、61、62、71、72、75）の場合、配信は停止され、タスクはリンクされた情報を削除します。

### 期限切れの配信のクリーンアップ {#cleanup-of-expired-deliveries}

このタスクは、有効期間が終了した配信を停止します。

1. ワークフ **[!UICONTROL Database cleanup]** ローは、有効期限が切れた配信のリストを作成します。 このリストには、ステータスが以外の期限切れのすべての配信と、 **[!UICONTROL Finished]** 10,000件を超える未処理のメッセージを含む最近停止した配信が含まれます。 次のクエリが使用されます。

   ```
   SELECT iDeliveryId, iState FROM NmsDelivery WHERE iDeleteStatus=0 AND iIsModel=0 AND iDeliveryMode=1 AND ( (iState >= 51 AND iState < 85 AND tsValidity IS NOT NULL AND tsValidity < $(currentDate) ) OR (iState = 85 AND DateMinusDays(15) < tsLastModified AND iToDeliver - iProcessed >= 10000 ))
   ```

   配信モ **ード** 1は、状態51 **[!UICONTROL Mass delivery]** は、状態 **85** 、状態 **[!UICONTROL Start pending]********[!UICONTROL Stopped]** 85は、状態を一致させ、配信サーバ上の配信ログの最大質量更新数は、10,000となる。

1. 次に、ミッドソーシングを使用する最近期限切れの配信のリストがワークフローに含まれます。 配信ログがまだミッドソーシングサーバーを介して回復されていない配信は除外されます。

   次のクエリが使用されます。

   ```
   SELECT iDeliveryId, tsValidity, iMidRemoteId, mData FROM NmsDelivery WHERE (iDeliveryMode = 4 AND (iState = 85 OR iState = 95) AND tsValidity IS NOT NULL AND (tsValidity < SubDays(GetDate() , 15) OR tsValidity < $(DateOfLastLogPullUp)) AND tsLastModified > SubDays(GetDate() , 15))
   ```

1. 次のクエリは、配信を日付でフィルタリングするために、外部アカウントがアクティブかどうかを検出するために使用します。

   ```
   SELECT iExtAccountId FROM NmsExtAccount WHERE iActive<>0 AND sName=$(providerName)
   ```

1. 期限切れの配信のリストで、ステータスが **[!UICONTROL Pending]** 、に切り替え、このリス **[!UICONTROL Delivery cancelled]** ト内のすべての配信がに切り替わりま **[!UICONTROL Finished]** す。

   次のクエリが使用されます。

   ```
   UPDATE $(BroadLogTableName) SET tsLastModified=$(curdate), iStatus=7, iMsgId=$(bl) WHERE iDeliveryId=$(dl) AND iStatus=6
   ```

   ここで、 **$(curdate)** はデータベース・サーバの現在の日付、$(bl) **は配信ログ・メッセージのID、$(** $(bl)は配信ID配信ステータス6は配信ID配信ステータス **********[!UICONTROL Pending]********[!UICONTROL Delivery cancelled]** 6は配信ステータス7は配信ステータス

   ```
   UPDATE NmsDelivery SET iState = 95, tsLastModified = $(curdate), tsBroadEnd = tsValidity WHERE iDeliveryId = $(dl)
   ```

   配信 **状態95** は状態 **[!UICONTROL Finished]** に一致し、 **$(dl)** は配信の識別子です。

1. 古い配信のすべてのフ&#x200B;**ラグメント**(deliveryParts)が削除され、処理中の通知配信の古いフラグメントがすべて削除されます。 一括削除は、これらの両方のタスクに使用されます。

   次のクエリが使用されます。

   ```
   DELETE FROM NmsDeliveryPart WHERE iDeliveryPartId IN (SELECT iDeliveryPartId FROM NmsDeliveryPart WHERE iDeliveryId IN (SELECT iDeliveryId FROM NmsDelivery WHERE iState=95 OR iState=85) LIMIT 5000)
   ```

   ```
   DELETE FROM NmsDeliveryPart WHERE iDeliveryPartId IN (SELECT iDeliveryPartId FROM NmsDeliveryPart WHERE tsValidity < $(curDate) LIMIT 500000)
   ```

   配信状 **態95** はステータス **[!UICONTROL Finished]** に、配信状態85 **はステータスに、** $(curDate)は現在のサーバ **[!UICONTROL Stopped]****** ー日に一致します。

### ミラーページのクリーンアップ {#cleanup-of-mirror-pages}

このタスクは、配信で使用されるWebリソース（ミラーページ）を削除します。

1. まず、パージされる配信のリストは、次のクエリーを使用してリカバリされます。

   ```
   SELECT iDeliveryId, iNeedMirrorPage FROM NmsDelivery WHERE iWebResPurged = 0 AND tsWebValidity IS NOT NULL AND tsWebValidity < $(curdate)"
   ```

   ここ **で、$(curDate)** は現在のサーバーの日付です。

1. その後 **** 、必要に応じて、以前にリカバリされた配信の識別子を使用してNmsMirrorPageInfoテーブルがクリアされます。 一括削除は、次のクエリーの生成に使用します。

   ```
   DELETE FROM NmsMirrorPageInfo WHERE iMirrorPageInfoId IN (SELECT iMirrorPageInfoId FROM NmsMirrorPageInfo WHERE iDeliveryId = $(dl)) LIMIT 5000)
   ```

   ```
   DELETE FROM NmsMirrorPageSearch WHERE iMessageId IN (SELECT iMessageId FROM NmsMirrorPageSearch WHERE iDeliveryId = $(dl)) LIMIT 5000)
   ```

   ここ **で、** $(dl)は配信の識別子です。

1. その後、エントリが配信ログに追加されます。
1. その後、パージされた配信が識別され、後で再処理する必要がなくなります。 次のクエリーが実行されます。

   ```
   UPDATE NmsDelivery SET iWebResPurged = 1 WHERE iDeliveryId IN ($(strIn))
   ```

   ここで **、$(strIn)** は配信識別子のリストです。

### 作業テーブルのクリーンアップ {#cleanup-of-work-tables}

このタスクは、ステータスが、またはの配信に一致するすべての作業テーブルをデータベース **[!UICONTROL Being edited]** から削 **[!UICONTROL Stopped]** 除しま **[!UICONTROL Deleted]** す。

1. 名前がwkDlv_で始まるテーブルのリスト **は、最初に** 次のクエリ(postgresql)を使用して回復されます。

   ```
   SELECT relname FROM pg_class WHERE relname LIKE Lower('wkDlv_') ESCAPE E'\\' AND relkind IN ('r','v') AND pg_get_userbyid(relowner)<>'postgres'
   ```

1. その後、進行中のワークフローで使用されるテーブルは除外されます。 これを行うには、進行中の配信のリストを次のクエリを使用して回復します。

   ```
   SELECT iDeliveryId FROM NmsDelivery WHERE iDeliveryId<>0 AND iDeleteStatus=0 AND iState NOT IN (0,85,100);
   ```

   ここで、0は配信ステータスに一致する値、85 **[!UICONTROL Being edited]** はステータスに一致し、100 **[!UICONTROL Stopped]** はステータスに一致する値 **[!UICONTROL Deleted]** です。

1. 使用されなくなったテーブルは、次のクエリを使用して削除されます：

   ```
   DROP TABLE wkDlv_15487_1;
   ```

### インポートによって生成された拒否のクリーンアップ {#cleanup-of-rejects-generated-by-imports-}

この手順を使用すると、インポート中に処理されなかったすべてのデータのレコードを削除できます。

1. XtkRejectテーブルでは、次のクエ **リを使って** 、一括削除が行われます。

   ```
   DELETE FROM XtkReject WHERE iRejectId IN (SELECT iRejectId FROM XtkReject WHERE tsLog < $(curDate)) LIMIT $(l))
   ```

   ここで **$(curDate)** は、NmsCleanup_RejectsPurgeDelayオプションに定義した期間を差し引いた現在のサーバの日付です( **Deployment wizardを参照** )。 [](#deployment-wizard)**** $(l)は、削除するレコードの最大数を示します。

1. 次に、すべてのオーファン・リジェクトが次のクエリーを使用して削除されます。

   ```
   DELETE FROM XtkReject WHERE iJobId NOT IN (SELECT iJobId FROM XtkJob)
   ```

### ワークフローインスタンスのクリーンアップ {#cleanup-of-workflow-instances}

このタスクでは、識別子(lWorkflowId **)と履歴(** lHistory ****)を使用して各ワークフローインスタンスを削除します。 作業テーブルのクリーンアップタスクを再実行して、非アクティブなテーブルを削除します。

>[!NOTE]
>
>履歴の削除頻度は、「 **History in days** 」フィールド（デフォルト値は30日）の各ワークフローに対して指定します。 このフィールドは、ワークフロープロパ **ティの** 「実行」タブにあります。 詳しくは、[この節](../../workflow/using/workflow-properties.md#execution)を参照してください。

1. 削除するワークフローのリストを回復するには、次のクエリを使用します。

   ```
   SELECT iWorkflowId, iHistory FROM XtkWorkflow WHERE iWorkflowId<>0
   ```

1. このクエリは、次のクエリを使用して、リンクされたすべてのログ、完了したタスクおよび完了したイベントの削除に使用されるワークフローのリストを生成します。

   ```
   DELETE FROM XtkWorkflowLog WHERE iWorkflowId=$(lworkflow) AND tsLog < DateMinusDays($(lhistory))
   ```

   ```
   DELETE FROM XtkWorkflowTask WHERE iWorkflowId=$(lworkflow) AND iStatus<>0 AND tsCompletion < DateMinusDays($(lhistory)) 
   ```

   ```
   DELETE FROM XtkWorkflowEvent WHERE iWorkflowId=$(l) AND iStatus>2 AND tsProcessing < DateMinusDays($(lHistory))
   ```

   ここ **で、** $(lworkflow)はワークフローの識別子、 **** $(lhistory)は履歴の識別子です。

1. 未使用のテーブルはすべて削除されます。 このため、全てのテーブルは次の問い合わせを使っ **てwkf%** 型のマスクを使って収集されます。 (postgresql)

   ```
   SELECT relname FROM pg_class WHERE relname LIKE Lower('wkf%') ESCAPE E'\\' AND relkind IN ('r','v') AND pg_get_userbyid(relowner)<>'postgres'
   ```

1. 次に、保留中のワークフローインスタンスで使用されるすべてのテーブルが除外されます。 アクティブなワークフローのリストは、次のクエリを使用して回復されます。

   ```
   SELECT iWorkflowId FROM XtkWorkflow WHERE iWorkflowId<>0 AND iState<>20
   ```

1. 次に、各ワークフロー識別子が復元され、処理中のワークフローで使用されるテーブルの名前が見つかります。 これらの名前は、以前にリカバリされたテーブルのリストから除外されます。
1. 「増分クエリー」タイプのアクティビティ履歴テーブルは、次のクエリーを使用して除外されます。

   ```
   SELECT relname FROM pg_class WHERE relname LIKE Lower('wkfhisto%') ESCAPE E'\\' AND relkind IN ('r','v') AND pg_get_userbyid(relowner)<>'postgres'
   ```

   ```
   SELECT iWorkflowId FROM XtkWorkflow WHERE iWorkflowId IN ($(strCondition))
   ```

   ここ **で、$(strcondition)** は、wkfhisto%マスクに一致するテーブルのリ **ストです** 。

1. 残りのテーブルは次のクエリを使用して削除されます。

   ```
   DROP TABLE wkf15487_12;
   ```

### ワークフローログインのクリーンアップ {#cleanup-of-workflow-logins}

このタスクは、次のクエリを使用してワークフローログインを削除します。

```
DELETE FROM XtkWorkflowLogin WHERE iWorkflowId NOT IN (SELECT iWorkflowId FROM XtkWorkflow)
```

### 単独作業テーブルのクリーンアップ {#cleanup-of-orphan-work-tables}

このタスクは、グループにリンクされた単独の作業テーブルを削除します。 NmsGroupテ **ーブルには** 、クリーンアップするグループ（0とは異なるタイプ）が格納されます。 テーブル名のプレフィックスは **grpです**。 クリーンアップするグループを識別するために、次のクエリーが使用されます。

```
SELECT iGroupId FROM NmsGroup WHERE iType>0"
```

### 訪問者のクリーンアップ {#cleanup-of-visitors}

このタスクは、一括削除を使用して訪問者テーブルから古いレコードを削除します。 古いレコードは、最後の変更が配置ウィザードで定義された保存期間より前のものです(配置ウィザード [を参照](#deployment-wizard))。 次のクエリが使用されます。

```
DELETE FROM NmsVisitor WHERE iVisitorId IN (SELECT iVisitorId FROM NmsVisitor WHERE iRecipientId = 0 AND tsLastModified < $(tsDate) LIMIT 5000)
```

ここで **$(tsDate)** は、現在のサーバーの日付で、NmsCleanup_VisitorPurgeDelayオプションに定義された期間 **を引きます** 。

### NAPIの浄化 {#cleanup-of-npai}

このタスクを実行すると、有効なアドレスに一致するレコードを **NmsAddressテーブルから削除できます** 。 次のクエリーを使用して、一括削除を実行します。

```
DELETE FROM NmsAddress WHERE iAddressId IN (SELECT iAddressId FROM NmsAddress WHERE iStatus=2 AND tsLastModified < $(tsDate1) AND tsLastModified >= $(tsDate2) LIMIT 5000)
```

ここで、 **status** 2 **[!UICONTROL Valid]** はと一致し、$(tsDate1)はサーバの日付、$(tsDate2)は現在の日付、 **$(tsDate2)は********** 、cleanup_msCleanup lastCleanup Cleanupオプションと一致します。

### 購読のクリーンアップ {#cleanup-of-subscriptions-}

このタスクでは、NmsSubscriptionテーブルからユーザーが削除したすべての **購読を** 、一括削除を使用して削除します。 次のクエリが使用されます。

```
DELETE FROM NmsSubscription WHERE iDeleteStatus <>0
```

### トラッキングログのクリーンアップ {#cleanup-of-tracking-logs}

このタスクは、追跡およびWeb追跡ログテーブルから古いレコードを削除します。 古いレコードは、配置ウィザードで定義された保存期間より前のものです(配置ウィザード [を参照](#deployment-wizard))。

1. 最初に、次のクエリを使用して、トラッキングログテーブルのリストを回復します。

   ```
   SELECT distinct(sTrackingLogSchema) FROM NmsDeliveryMapping WHERE sTrackingLogSchema IS NOT NULL;
   ```

1. 一括削除は、以前にリカバリされたテーブルのリスト内のすべてのテーブルをパージするために使用します。 次のクエリが使用されます。

   ```
   DELETE FROM XtkTrackingLogRcp WHERE iTrackingLogId IN (SELECT iTrackingLogId FROM XtkTrackingLogRcp WHERE tsLog < $(tsDate) LIMIT 5000) 
   ```

   ここで **$(tsDate)** は、NmsCleanup_TrackingLogPurgeDelayオプションに定義された期間を差し引いた現在のサーバ **** ーの日付です。

1. 追跡統計テーブルは、一括削除を使用して削除されます。 次のクエリが使用されます。

   ```
   DELETE FROM NmsTrackingStats WHERE iTrackingStatsId IN (SELECT iTrackingStatsId FROM NmsTrackingStats WHERE tsStart < $(tsDate) LIMIT 5000) 
   ```

   ここで **$(tsDate)** は、NmsCleanup_TrackingStatPurgeDelayオプションに定義された期間を差し引いた現在のサーバ **** ーの日付です。

### 配信ログのクリーンアップ {#cleanup-of-delivery-logs}

このタスクを使用すると、様々なテーブルに保存された配信ログを削除できます。

1. このため、配信ログスキーマのリストは、次のクエリを使用して回復されます。

   ```
   SELECT distinct(sBroadLogSchema) FROM NmsDeliveryMapping WHERE sBroadLogSchema IS NOT NULL UNION SELECT distinct(sBroadLogExclSchema) FROM NmsDeliveryMapping WHERE sBroadLogExclSchema IS NOT NULL
   ```

1. ミッドソーシングを使用する場合、 **NmsBroadLogMidテーブルは** 、配信マッピングで参照されません。 nms: **broadLogMidスキーマは** 、前のクエリでリカバリされたリストに追加されます。
1. 次に、デー **タベースのクリーンアップ** ・ワークフローは、以前にリカバリされたテーブルから古いデータを削除します。 次のクエリが使用されます。

   ```
   DELETE FROM $(tableName) WHERE iBroadLogId IN (SELECT iBroadLogId FROM $(tableName) WHERE tsLastModified < $(option) LIMIT 5000) 
   ```

   ここ **で、$(tableName)** はスキーマリスト内の各テーブルの名前、 **$(option)はNmsCleanup_BroadLogPurgeDelayオプションに定義された日付です(** Deployment ****[](#deployment-wizard)Wizardを参照)。

1. 最後に、ワークフローはNmsProviderMsgIdテーブルが存在する **かどうかを確認します** 。 古いデータが含まれている場合は、次のクエリを使用して古いデータがすべて削除されます。

   ```
   DELETE FROM NmsProviderMsgId WHERE iBroadLogId IN (SELECT iBroadLogId FROM NmsProviderMsgId WHERE tsCreated < $(option) LIMIT 5000)
   ```

   ここで **$(option)** は、NmsCleanup_BroadLogPurgeDelay **(デプロイメントウィザードを参照** )オプションで定義された日付と一致し [](#deployment-wizard)ます。

### NmsEmailErrorStatテーブルのクリーンアップ {#cleanup-of-the-nmsemailerrorstat-table-}

このタスクは、NmsEmailErrorStatテーブルをク **リーンアップします** 。 メインプログラム(**coalesceErrors**)は、次の2つの日付を定義します。

* **開始日**:NmsLastErrorStatCoalesceオプションまたはテーブル内 **の最新の日付** に一致する次のプロセスの日付。
* **終了日**:現在のサーバーの日付。

開始日が終了日以上の場合、処理は実行されません。 この場合、coalesceUpToDateメッセージ **が表示され** ます。

開始日が終了日より前の場合、NmsEmailErrorStatテーブルはク **リーンアップされます** 。

開始日と終了日の間の **NmsEmailErrorStatテーブルのエラーの総数は** 、次のクエリを使用して回復されます。

```
"SELECT COUNT(*) FROM NmsEmailErrorStat WHERE tsDate>= $(start) AND tsDate< $(end)"
```

ここで **$end** と$startは **** 、以前に定義した開始日と終了日です。

合計が0より大きい場合：

1. 特定のしきい値（20に等しい）を超えるエラーのみを保持するために、次のクエリが実行されます。

   ```
   "SELECT iMXIP, iPublicId, SUM(iTotalConnections), SUM(iTotalErrors), SUM(iMessageErrors), SUM(iAbortedConnections), SUM(iFailedConnections), SUM(iRefusedConnections), SUM(iTimeoutConnections) FROM NmsEmailErrorStat WHERE tsDate>=$(start ) AND tsDate<$(end ) GROUP BY iMXIP, iPublicId HAVING SUM(iTotalErrors) >= 20"
   ```

1. coalescingErrorsメッ **セージが** 表示されます。
1. 開始日と終了日の間に発生したすべてのエラーを削除する新しい接続が作成されます。 次のクエリが使用されます。

   ```
   "DELETE FROM NmsEmailErrorStat WHERE tsDate>=$(start) AND tsDate<$(end)"
   ```

1. 各エラーは、次のクエリを使 **用して** 、NmsEmailErrorStatテーブルに保存されます。

   ```
   "INSERT INTO NmsEmailErrorStat(iMXIP, iPublicId, tsDate, iTotalConnections, iTotalErrors, iTimeoutConnections, iRefusedConnections, iAbortedConnections, iFailedConnections, iMessageErrors) VALUES($(lmxip ), $(lpublicId ), $(tsstart ), $(lconnections ), $(lconnectionErrors ),$(ltimeoutConnections ), $(lrefusedConnections ), $(labortedConnections ), $(lfailedConnections ), $(lmessageErrors))"
   ```

   各変数は、前のクエリでリカバリされた値と一致します。

1. start変 **数は** 、ループを終了するために前のプロセスの値で更新されます。

ループとタスクの停止。

クリーンアップは、 **NmsEmailErrorテーブルと** cleanupNmsMxDomain **テーブルで** 実行されます。

### NmsEmailErrorテーブルのクリーンアップ {#cleanup-of-the-nmsemailerror-table-}

次のクエリが使用されます。

```
DELETE FROM NmsEmailError WHERE iMXIP NOT IN (SELECT DISTINCT iMXIP FROM NmsEmailErrorStat)
```

このクエリは、NmsEmailErrorテーブルからNmsEmailErrorStat内のリンクされたレコードを含まな **い** すべての行 **を削除します** 。

### NmsMxDomainテーブルのクリーンアップ {#cleanup-of-the-nmsmxdomain-table-}

次のクエリが使用されます。

```
DELETE FROM NmsMxDomain WHERE iMXIP NOT IN (SELECT DISTINCT iMXIP FROM NmsEmailErrorStat)
```

このクエリは、NmsMxDomainテーブルからNmsEmailErrorStatテーブル内のリンクされたレコ **ードのない** すべての行 **を削除します** 。

### 提案の整理 {#cleanup-of-propositions}

Interactionモジュール **がインストールされている場合** 、このタスクはNmsPropositionXxxテーブルを削除するために実 **行されます** 。

提案テーブルのリストが復元され、次のクエリを使用して各提案テーブルに対して一括削除が実行されます。

```
DELETE FROM NmsPropositionXxx WHERE iPropositionId IN (SELECT iPropositionId FROM NmsPropositionXxx WHERE tsLastModified < $(option) LIMIT 5000) 
```

ここ **で、** $(option)はNmsCleanup_PropositionPurgeDelay **(デプロイメントウィザードを** 参照 [](#deployment-wizard))オプションで定義された日付です。

### シミュレーションテーブルのクリーンアップ {#cleanup-of-simulation-tables}

このタスクは、孤立したシミュレーションテーブル（オファーシミュレーションまたは配信シミュレーションにリンクされなくなったテーブル）をクリーンアップします。

1. クリーンアップが必要なシミュレーションのリストを回復するには、次のクエリを使用します。

   ```
   SELECT iSimulationId FROM NmsSimulation WHERE iSimulationId<>0
   ```

1. 削除するテーブルの名前は、wkSimu_ **prefixに続くシミュレーションの識別子** (例： **wkSimu_456831_aggr**):

   ```
   DROP TABLE wkSimu_456831_aggr
   ```

### 統計の更新とストレージの最適化 {#statistics-update}

XtkCleanup_NoStats **オプションを使用すると** 、クリーンアップワークフローのストレージ最適化手順の動作を制御できます。

XtkCleanup_NoStats **** オプションが存在しない場合、またはその値が0の場合、PostgreSQL上の冗長モード(VACUUM VERBOSE ANALYZE)で記憶領域の最適化を実行し、他のすべてのデータベースの統計を更新します。 このコマンドが確実に実行されるように、PostgreSQLログを調べます。 VACUUMは次の形式で行を出力します。と `INFO: vacuuming "public.nmsactivecontact"` ANALYZEは次の形式で行を出力します。 `INFO: analyzing "public.nmsactivecontact"`.

このオプションの値が1の場合、統計の更新はどのデータベースでも実行されません。 次のログ行がワークフローログに表示されます。 `Option 'XtkCleanup_NoStats' is set to '1'`.

このオプションの値が2の場合、これはPostgreSQL上で冗長モード(ANALYZE VERBOSE)で記憶解析を実行し、他の全てのデータベースの統計を更新します。 このコマンドが確実に実行されるように、PostgreSQLログを調べます。 ANALYZEは次の形式で行を出力します。 `INFO: analyzing "public.nmsactivecontact"`.

### 購読のクリーンアップ(NMAC) {#subscription-cleanup--nmac-}

このタスクは、削除されたサービスまたはモバイルアプリケーションに関連する購読をすべて削除します。

1. ブロードログスキーマのリストを回復するには、次のクエリーを使用します。

   ```
   SELECT distinct(sBroadLogSchema) FROM NmsDeliveryMapping WHERE sBroadLogSchema IS NOT NULL
   ```

1. 次に、タスクは、appSubscriptionリンクにリンクされたテーブルの名前を回復し **、** これらのテーブルを削除します。

### セッション情報のクレンジング {#cleansing-session-information}

このタスクは、 **sessionInfoテーブルから情報をク** リーンします。次のクエリが使用されます。

```
 DELETE FROM XtkSessionInfo WHERE tsexpiration < $(curdate) 
```

### 期限切れイベントのクレンジング {#cleansing-expired-events}

このタスクは、受け取って実行インスタンスに保存されたイベントと、制御インスタンスにアーカイブされたイベントをクリーンアップします。

### 洗浄反応 {#cleansing-reactions}

このタスクは、仮説自体が削除さ **れた反応(表NmsRemaMatchRcp**)を洗浄します。

### 監査証跡のクリーンアップ {#cleanup-of-audit-trail}

次のクエリが使用されます。

```
DELETE FROM XtkAudit WHERE tsChanged < $(tsDate)
```

ここで **$(tsDate)** は、XtkCleanup_AuditTrailPurgeDelayオプションに対して定義された期間が停止された、現在のサー **** バーの日付です。
