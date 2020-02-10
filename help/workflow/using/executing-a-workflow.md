---
title: ワークフローの実行
seo-title: ワークフローの実行
description: ワークフローの実行
seo-description: null
page-status-flag: never-activated
uuid: 7668f1a2-fcd0-41f8-b8f6-71d77bc47486
contentOwner: sauviat
products: SG_CAMPAIGN/CLASSIC
audience: workflow
content-type: reference
topic-tags: -general-operation
discoiquuid: 9ac4c60a-b0f6-42fb-a081-74b57820cb16
index: y
internal: n
snippet: y
translation-type: tm+mt
source-git-commit: 4b4ec97e52a494dd88b2516650ae514294f00934

---


# ワークフローの実行{#executing-a-workflow}

ワークフローの実行に関するトラブルシューティングガイドラインにつ [いては、この節](../../production/using/workflow-execution.md)。

## ワークフローの開始 {#starting-a-workflow}

ワークフローは、必ず手動で開始します。When started, it can however remain inactive depending on the information specified via a scheduler (see [Scheduler](../../workflow/using/scheduler.md)) or activity scheduling.

ターゲティングワークフローの実行に関連するアクション（開始、停止、一時停止など）は、**非同期**&#x200B;プロセスです。プロセスの実行順序は記録され、サーバーが順序を適用できるようになるとすぐに実行されます。

ツールバーを使用して、ワークフローの実行を開始およびトラッキングできます。

The list of options available in the **[!UICONTROL Actions]** menu and the right-click menu are detailed below.

### アクションツールバー {#actions-toolbar}

ツールバーのボタンについて詳しくは、この[節](../../campaign/using/marketing-campaign-deliveries.md#building-the-main-target-in-a-workflow)を参照してください。The **[!UICONTROL Actions]** button gives you access to additional execution options for acting on selected workflows. You can also use the **[!UICONTROL File > Actions]** menu, or right-click a workflow and select **[!UICONTROL Actions]**.

![](assets/purge_historique.png)

* **[!UICONTROL Start]**

   このアクションは、ワークフローの実行を開始します。「**終了**」、「**編集中**」、「**一時停止**」のワークフローのステータスが、「**開始済み**」に変わります。続いて、ワークフローエンジンが、ワークフローの実行を処理します。ワークフローが一時停止していた場合は再開します。それ以外の場合は、ワークフローが最初から開始し、初期のアクティビティが有効化されます。

   開始は非同期プロセスです。リクエストが保存され、ワークフローサーバーによって可能な限り早く処理されます。

* **[!UICONTROL Pause]**

   このアクションは、ワークフローのステータスを「**一時停止**」に設定します。ワークフローが再開するまでは、一切のアクティビティは有効化されません。ただし、進行中の操作は一時停止されません。

* **[!UICONTROL Stop]**

   このアクションは、現在実行中のワークフローを停止します。インスタンスのステータスは「**終了**」に設定されます。可能な場合、進行中の操作を中止します。インポートおよび SQL クエリはただちにキャンセルされます。

   停止は非同期プロセスです。停止リクエストが登録されると、ワークフローサーバーは進行中の操作をキャンセルします。このため、ワークフローインスタンスの停止には時間がかかります。特に、ワークフローが複数のサーバーで実行されている場合は、各サーバーがそれぞれ進行中のタスクのキャンセルを処理する必要があるので、時間がかかります。

* **[!UICONTROL Restart]**

   ワークフローを停止したあとに、再起動します。多くの場合、この操作をおこなうことでワークフローの再起動が高速化されます。また、停止にある程度の時間がかかるときに、再起動を自動化するのに便利です。再起動を自動化する理由は、ワークフローの停止中は「停止」コマンドを利用できないからです。

   アクション **[!UICONTROL Start / Pause / Stop / Restart]** は、ツールバーの実行アイコンからも使用できます。 詳しくは、[この節](../../campaign/using/marketing-campaign-deliveries.md#creating-a-targeting-workflow)を参照してください。

* **[!UICONTROL Purge history]**

   このアクションでは、ワークフローの履歴をパージできます。For more on this, refer to [Purging the logs](../../workflow/using/monitoring-workflow-execution.md#purging-the-logs).

* **[!UICONTROL Start in simulation mode]**

   ワークフローを、リアルモードとは対照的なシミュレーションモードで開始できます。This means that when you enable this mode, only activities that do not impact the database or the file system are executed (e.g. **[!UICONTROL Query]**, **[!UICONTROL Union]**, **[!UICONTROL Intersection]**, etc.). 影響を与えるアクティビティ(例： **[!UICONTROL Export]**、 **[!UICONTROL Import]**&#x200B;など)（同じブランチ内の）後のものは実行されない。

* **[!UICONTROL Execute pending tasks now]**

   このアクションでは、保留中のタスクをただちに開始できます。特定のタスクを開始するには、そのタスクのアクティビティを右クリックし、を選択しま **[!UICONTROL Execute pending task(s) now]**&#x200B;す。

* **[!UICONTROL Unconditional stop]**

   This option changes the workflow status to **[!UICONTROL Finished]**. 通常の停止プロセスが実施数分後に失敗する場合にのみ、最終手段として使用します。条件なしの停止を使用できるのは、進行中の実際のワークフロージョブが何もないことを確認できている場合だけです。

   >[!CAUTION]
   >
   >このオプションはエキスパートユーザー向け機能として予約されています。

* **[!UICONTROL Save as template]**

   このアクションは、選択したワークフローに基づいて、新しいワークフローテンプレートを作成します。You need to specify the folder where it will be saved (in the **[!UICONTROL Folder]** field).

   とのオプシ **[!UICONTROL Mass update of selected lines]** ョンは、す **[!UICONTROL Merge selected lines]** べてのメニューで使用できる汎用プラットフォームオプシ **[!UICONTROL Actions]** ョンです。 詳しくは、[この節](../../platform/using/updating-data.md)を参照してください。

### 右クリックメニュー {#right-click-menu}

1 つまたは複数のワークフローアクティビティが選択されている場合、右クリックすることで選択したものを操作できます。

![](assets/contextual_menu.png)

右クリックメニューでは、次のオプションを使用できます。

**[!UICONTROL Open]**:このオプションを使用すると、アクティビティのプロパティにアクセスできます。

**[!UICONTROL Display logs:]** このオプションを使用すると、選択したアクティビティのタスク実行ログを表示できます。 ログの表示を参 [照してください](../../workflow/using/monitoring-workflow-execution.md#displaying-logs)。

**[!UICONTROL Execute pending task(s) now:]** この操作により、可能な限り早く保留中のタスクを開始できます。

**[!UICONTROL Workflow restart from a task:]** このオプションを使用すると、このアクティビティに対して以前に保存された結果を使用してワークフローを再開できます。

**[!UICONTROL Cut/Copy/Paste/Delete:]** これらのオプションを使用すると、アクティビティの切り取り、コピー、貼り付けおよび削除を行うことができます。

**[!UICONTROL Copy as bitmap:]** このオプションを使用すると、すべてのアクティビティのスクリーンショットを取得できます。

**[!UICONTROL Normal execution / Enable but do not execute / Do not enable:]** これらのオプションは、アクティビティのプ **[!UICONTROL Advanced]** ロパティのタブでも使用できます。 They are detailed in [Execution](../../workflow/using/advanced-parameters.md#execution).

**[!UICONTROL Save / Cancel:]** ワークフローに対する変更を保存またはキャンセルできます。

>[!NOTE]
>
>アクティビティのグループを選択し、上記のいずれかのコマンドを適用することができます。

右クリックメニューの詳しい説明は、この[節](../../campaign/using/marketing-campaign-deliveries.md#executing-a-workflow)でも参照できます。

## ワークフローのライフサイクル {#workflow-life-cycle}

ワークフローサイクルは、3つの主要なステップがあります。

* **編集中**

   初期設計段階は次のとおりです。が新しいワークフローを作成すると、そのステータスは「編集中」になります。 ワークフローのサーバーによる処理はまだ開始されず、編集しても問題は発生しません。

* **開始済み**

   初期のデザインフェースが完了したら、ワークフローを開始できます。このフェーズでは、インスタンスがサーバーによって処理され、個々のタスクが実行されます。ワークフローは、このフェーズでも編集できますが、いくつか注意事項があります。

* **終了**

   進行中のタスクがなくなったとき、またはオペレーターがインスタンスを明示的に停止したときに、ワークフローは「終了」となります。

例えば、次のワークフローでは、「**開始**」アクティビティと「**配信**」アクティビティがアウトライン化され、「**承認**」アクティビティが点滅します。

![](assets/new-workflow-6.png)

つまり、最初の 2 つのアクティビティの実行は成功し、承認アクティビティは進行中です（作成されたが、まだ完了していないなど）。

「**配信**」アクティビティに続くトランジションの上に表示されている「**574 -Ok**」という文字列は、配信準備で 574 人の受信者がターゲッティングされ、操作に成功したことを示しています。実行時にトランジションに追加されるこの情報は、データを処理するアクティビティによって自動生成されます。

ワークフローは開始され、「**承認**」アクティビティ内に指定されたグループに属するオペレータが意思決定するのを待機しています。グループに属しているオペレーターが、E メールアドレスまたは携帯電話番号を登録している場合、通知が届きます。

オペレーターの管理について詳しくは、この[節](../../platform/using/access-management.md)を参照してください。

ワークフローの監視方法について詳しくは、この節を参照 [してください](../../workflow/using/monitoring-workflow-execution.md)。

## データのライフサイクル {#data-life-cycle}

### 作業用テーブル {#work-table}

ワークフローでは、1 つのアクティビティから別のアクティビティへ移されたデータは、一時的な作業用テーブルに保存されます。

このデータは、適切なトランジションを右クリックすることで、表示して分析することができます。

![](assets/wf-right-click-analyze.png)

これを実行するには、該当するメニューを選択します。

* ターゲットを表示

   This menu displays the available data on the target population as well as the structure of the work table (**[!UICONTROL Schema]** tab).

   ![](assets/wf-right-click-display.png)

   詳しくは、「ワークテーブルとワークフ [ロースキーマ」を参照してくださ](../../workflow/using/monitoring-workflow-execution.md#worktables-and-workflow-schema)い。

* ターゲットを分析

   このメニューは、トランジションのデータの統計とレポートを作成できる記述的分析ウィザードを表示します。

   詳しくは、[この節](../../reporting/using/using-the-descriptive-analysis-wizard.md)を参照してください。

ワークフローが実行されると、ターゲットデータはパージされます。最後の作業用テーブルだけにアクセスできます。ワークフローを設定して、すべての作業テーブルにアクセスできるようにします。ワークフロープロ **[!UICONTROL Keep the result of interim populations between two executions]** パティのオプションをオンにします。

ただし、データが大量にある場合、このオプションを有効化しないことをお勧めします。

![](assets/wf-purge-data-option.png)

### データをターゲット {#target-data}

ワークフローの作業用テーブルに保存されたデータは、パーソナライゼーションフィールドからアクセスできます。

このようにすることで、リストを経由して収集したデータ、または調査に対する回答に基づくデータを使用できます。それには、次の構文を使用します。

```
%= targetData.FIELD %
```

**[!UICONTROL Target extension]** (targetData)タイプのパーソナライゼーション要素は、ターゲット設定ワークフローでは使用できません。 配信ターゲットは、ワークフロー内に作成され、配信のインバウンドトランジション内に指定される必要があります。

If you want to create delivery proofs, the proof target needs to be built based on the **[!UICONTROL Address substitution]** mode so that the personalization data can be entered. 詳しくは、[この節](../../delivery/using/steps-defining-the-target-population.md#using-address-substitution-in-proof)を参照してください。

次の例では、パーソナライズしたメールで使用するために、顧客に関する情報のリストを収集しようとしています。

次の手順に従います。

1. 情報を収集するワークフローを作成し、既にデータベース内にあるデータと紐付けをおこなってから、配信を開始します。

   ![](assets/wf-targetdata-sample-1.png)

   この例では、ファイルの内容は次のようになります。

   ```
   Music,First name,Last name,Account,CD/DVD,Card
   Pop,David,BLAIR,4323,CD,0
   Rock,Daniel,ARCARI,3222,DVD,1
   Disco,Uma,ALTON,0488,DVD,0
   Jazz,Paul,BOLES,6475,CD,1
   Jazz,David,BOUKHARI,0841,DVD,1
   [...]
   ```

   ファイルを読み込むには、次の手順を適用します。

   ![](assets/wf-targetdata-sample-2.png)

1. Configure the **[!UICONTROL Enrichment]** type activity to reconcile the collected data with that already in the Adobe Campaign database.

   ここでは、紐付けキーがアカウント番号です。

   ![](assets/wf-targetdata-sample-3.png)

1. Then configure the **[!UICONTROL Delivery]**: it is created based on a template, and the recipients are specified by the inbound transition.

   ![](assets/wf-targetdata-sample-4.png)

   >[!CAUTION]
   >
   >トランジションに含まれているデータのみが、配信のパーソナライズに使用されます。**targetData型のパーソナライゼーションフィールドは** 、アクティビティの受信訪問者に対してのみ使用 **[!UICONTROL Delivery]** できます。

1. 配信テンプレートで、ワークフローで収集したフィールドを使用します。

   To do this, insert **[!UICONTROL Target extension]** type personalization fields.

   ![](assets/wf-targetdata-sample-5.png)

   ここでは、ワークフローで収集されたファイル内に記述された顧客の好きな音楽ジャンルとメディアタイプ（CD または DVD）を挿入します。

   さらに、ロイヤリティのあるカード所有者（例えば Card の値が 1 と等しい受信者）にクーポンを追加します。

   ![](assets/wf-targetdata-sample-6.png)

   **[!UICONTROL Target extension]** (targetData)タイプのデータは、すべてのパーソナライゼーションフィールドと同じ特性を使用して配信に挿入されます。 これらのデータは、本文、リンクラベル、またはリンク自体に使用されます。

   収集された受信者宛てのメッセージには、次のデータが含まれます。

   ![](assets/wf-targetdata-sample-7.png)

## 承認の定義 {#defining-approvals}

承認により、オペレーターはワークフロー管理に関する意思決定をおこなったり、実行の継続を確定したりできます。

オペレーターのグループにメッセージが送信され、ワークフローは応答を待って再開します。ワークフローは停止せず、その他の操作が実行されます。例えば、複数の保留中の承認が同時に存在する場合があります。

承認には、オペレーターが選択できるオプションが複数含まれていることがあります。ただし、オペレーターに実行してもらうタスク（ターゲティングの実施など）を送信するために、選択肢の数を 1 つに制限することもできます。オペレーターは、そのタスクが実行された後で、応答できるようになります（その後、プロセスが再開します）。次の例に、これらの承認タイプを示します。

![](assets/validation-1.png)

操作では、承認が必要なすべてのステージは、同じ原則に基づきます。

![](assets/validation-1-in-op.png)

承認の例については、この[節](../../campaign/using/marketing-campaign-approval.md#checking-and-approving-deliveries)を参照してください。

オペレーターは、2 つの方法（メールメッセージ内にリンクされた Web ページを使用するか、コンソール経由）のいずれかで、応答できます。

>[!NOTE]
>
>いったん保存した応答は、変更できません。

### E メールの送信 {#sending-emails}

Web ページへのリンクが記載された承認メッセージを受け取り、ページ上で応答することができます。ターゲット済みのオペレーターが、承認 E メールを受け取るようにするには、オペレーターの E メールアドレスが入力されている必要があります。入力していない場合、オペレータは応答にコンソールを使用する必要があります。

オペレーターの管理について詳しくは、この[節](../../platform/using/access-management.md)を参照してください。

承認の E メールは、継続的に送信されます。デフォルトの配信テンプレートは次のとおりで **[!UICONTROL notifyAssignee]**&#x200B;す。フォルダーに保存され **[!UICONTROL Administration > Campaign management > Technical delivery templates]** ます。 このシナリオは、カスタマイズ可能です。テンプレートのコピーを作成して、アクティビティごとに編集することをお勧めします。

このテンプレートを使用して作成された配信は、フォルダーに保存 **[!UICONTROL Administration > Production > Objects created automatically > Technical deliveries > Workflow notifications]** されます。

### コンソールからの承認 {#approval-via-the-console}

操作では、承認される要素はキャンペーンダッシュボードに表示されます。

技術的なワークフローでは、ユーザーが承認できるタスクは、フォルダー内のツリー構造からアクセスで **[!UICONTROL Administration > Production > Objects created automatically > Pending approvals]** きます。

![](assets/validation-node.png)

### グループ {#groups}

承認は、フィルター条件を使用して選択されたオペレーターのグループ、1 人のオペレーター、またはオペレーターセットに割り当てられます。

1. 最もシンプルな承認形態は、オペレーターの応答と同時にタスクが完了することです。その他のオペレーターが応答を試みた場合、既に別のオペレータによって応答済みであると通知されます。
1. 複数の承認については、複数の承認を参 [照してください](#multiple-approval)。

承認をおこなうオペレーターグループには、個人ではなく、役割または機能を指名します。例えば、「ハリーのグループ」ではなく、「キャンペーンの予算」グループの方が適切です。グループには、タスクを承認するオペレーターを最低でも 2 人以上含めることをお勧めします。オペレーターが 2 人いれば、1 人が不在の場合にもう 1 人が応答できます。

### 有効期限 {#expirations}

有効期限は、異なるタイプのアクティビティ、特に承認で使用される専用のトランジションです。有効期限は、所定の時間が経過しても応答がない場合、またはワークフローを続行する場合に、アクションのトリガーとして使用できます（例えば、異なるグループに承認を割り当てるなど）。

アクティビティの承認プロパティの 2 番目のタブで、1 つ以上の有効期限を定義できます。さらに、複数の有効期限タイプを定義できます。

![](assets/expiration.png)

To add a new expiration, click **[!UICONTROL Add]**. 作成される有効期限ごとに、トランジションが追加されます。次の操作をおこなうことができます。

* リスト内でセルをクリックする（または F2 キーを押す）ことで、代表的なパラメーターを変更できます。
* or edit the expression by clicking the **[!UICONTROL Detail...]** button.

>[!NOTE]
>
>有効期限は時系列で処理されるので、順序を指定する必要はありません。

このオプ **[!UICONTROL Do not terminate the task]** ションは、遅延がオーバーランの場合に、承認をアクティブなままにします。 このモードでは、承認をアクティブにしたまま、リマインダーを管理をできます。オペレーターは引き続き応答できます。このオプションはデフォルトでは無効になっています。有効期限に達したタスクは完了したと見なされ、期限後にオペレーターが応答することはありません。

次の 4 つのタイプの有効期限を作成できます。

* **タスク開始後の遅延**:有効期限は、承認がアクティブ化された日付に指定した時間を追加して計算されます。
* **指定した日付以降の遅延**:有効期限は、指定した日付に時間を追加して計算されます。
* **指定日より前の遅延**:有効期限は、指定した日付から時間を引いて計算されます。
* **有効期限の計算元スクリプト**:有効期限はJavaScriptを使用して計算されます。

   次の例では、（**vars.deliveryId** によって識別される）配信開始日付の 24 時間前に有効期限を計算します。

   ```
   var delivery = nms.delivery.get(vars.deliveryId)
   var expiration = delivery.scheduling.contactDate
   var oneDay = 1000*60*60*24
   expiration.setTime(expiration.getTime() - oneDay)
   return expiration
   ```

### 複数の承認 {#multiple-approval}

複数の承認は、すべての承認オペレーターが応答できるようにするメカニズムです。トランジションは応答ごとに有効化されます。

複数の承認は、投票または調査のメカニズムに有用です。期日を追加することで、所定の期間が経過した後に回答数を数え、結果を処理することができます。

### 必要な権限 {#required-rights}

承認リクエストに応答できるように、グループ内のオペレーターには少なくとも次の権限が必要です。

* ワークフローへの書き込み権限
* 承認するタスクが含まれているフォルダーへの読み取り/書き込み権限

「ワークフローの実行」グループにはこれらの 3 つの権限が付与されています。このグループに追加されたオペレーターは、承認リクエストに応答する権限を持ちます。

## アーキテクチャ {#architecture}

ワークフローは特定のモジュールによって処理されます。このモジュールは、複数のサーバーから起動し、処理の負荷を分散することができます。

![](assets/architecture.png)

* ‘Workflow Instance Runner&#39;（runwf）プロセスは、所定のワークフローインスタンスのすべてのタスクを実行します。一定期間、実行されるタスクがない場合、プロセスは「passive」になります。つまり、データベース内でステータスを保存し、停止します。
* &#39;Workflow Server&#39;（wfserver）モジュールは、現在のワークフローインスタンスを監視します。実行するタスクがある場合、このモジュールは対応するインスタンスを有効化（または再有効化）するプロセスを作成します。

オペレーターがワークフローに対するアクションを実行すると（開始、停止、一時停止など）、アクションは nlserver モジュールによって即座に実行されるのではなく、ワークフローモジュールに処理されるまでキューに入れられます。
