---
title: 配信の検証
seo-title: 配信の検証
description: 配信の検証
seo-description: null
page-status-flag: never-activated
uuid: 8bf70ea4-5f28-4d85-b5ce-0bd3ed3eea55
contentOwner: sauviat
products: SG_CAMPAIGN/CLASSIC
audience: delivery
content-type: reference
topic-tags: about-deliveries-and-channels
discoiquuid: df29492f-ed73-4ab8-b075-e76b3b9ebce3
index: y
internal: n
snippet: y
translation-type: ht
source-git-commit: 7bcf222f41c0e40368644b76197b07f2ded699f0

---


# 配信の検証 {#validating-the-delivery}

配信を作成して設定したら、メインターゲットに送信する前に検証する必要があります。

手順は次のとおりです。

1. **配信の分析**：この手順では、配信メッセージを準備できます。[配信の分析](#analyzing-the-delivery)を参照してください。

   使用可能な検証モードについて詳しくは、[承認モードの変更](../../delivery/using/steps-validating-the-delivery.md#changing-the-approval-mode)で説明しています。

1. **配達確認の送信**：この手順では、コンテンツ、URL、パーソナライゼーションフィールドなどを承認できます。[配達確認の送信](../../delivery/using/steps-validating-the-delivery.md#sending-a-proof)および[特定の配達確認ターゲットの定義](../../delivery/using/steps-defining-the-target-population.md#defining-a-specific-proof-target)を参照してください。

>[!CAUTION]
>
>メッセージコンテンツを変更するたびに、これらの手順を両方とも実行する必要があります。

## 配信の分析 {#analyzing-the-delivery}

分析は、ターゲット母集団が計算され、配信コンテンツが準備される段階です。この段階が完了すると、配信は送信できる状態になります。配信分析を開始するには、「**[!UICONTROL 送信]**」をクリックし、「**[!UICONTROL 可能な限り早く配信]**」を選択します。

![](assets/s_ncs_user_email_del_send.png)

「**[!UICONTROL 分析]**」ボタンをクリックすると、分析を手動で開始できます。分析の進行状況がプログレスバーに表示され、ウィンドウ下部のセクションに分析結果が表示されます。警告がある場合は、特別なアイコンが表示されます。

![](assets/s_ncs_user_interface_delivery04b.png)

>[!NOTE]
>
>検証ルールは、[タイポロジを使用したプロセスの検証](../../delivery/using/steps-validating-the-delivery.md#validation-process-with-typologies)で説明しています。

このジョブは、いつでも「**[!UICONTROL 停止]**」をクリックして停止できます。

![](assets/s_ncs_user_wizard_email01_16.png)

分析フェーズでは、メッセージが送信されないので、安全にジョブを開始またはキャンセルできます。

>[!CAUTION]
>
>分析を実行すると、その時点で、配信（または配達確認）が凍結されます。配信（または配達確認）への変更を適用するには、再度分析する必要があります。

最後のログメッセージには、エラーメッセージとエラー件数が表示されます。特殊なアイコンでエラータイプが示されます。黄色のアイコンは致命的でない処理エラーを、赤色のアイコンは配信開始を阻む致命的なエラーを示します。

![](assets/s_ncs_user_email_del_analyze_error.png)

「**[!UICONTROL 閉じる]**」をクリックし、エラーを修正します。変更を加えた後は、分析を再度実行する必要があります。

分析の結果をチェックしたら、「**[!UICONTROL 配信を確定]**」をクリックして、指定されたターゲットにメッセージを送信します。配信の開始を確認するメッセージが表示されます。

![](assets/s_ncs_user_email_del_analyze_ok.png)

>[!NOTE]
>
>送信するメッセージの数が設定と合っていない場合は、「**[!UICONTROL メインの配信ターゲットを変更]**」リンクをクリックします。これにより、ターゲット母集団の定義を変更して、分析を再度実行できます。

配信パラメーターの「**[!UICONTROL 分析]**」タブでは、分析フェーズ中のメッセージの準備に関する情報を定義できます。

![](assets/s_ncs_user_email_del_analyze_adv_param.png)

このタブで設定できるオプションを次に示します。

* **[!UICONTROL 配信のラベルとコード]**：この画面セクションに関するオプションは、配信分析フェーズでこれらのフィールドの値を計算するために使用されます。「**[!UICONTROL 配信分析中に実行フォルダーを計算]**」を選択すると、分析フェーズにこの配信アクションを格納するフォルダーの名前が計算されます。
* **[!UICONTROL 承認モード]**：このフィールドでは、配信承認のタイプを選択できます。承認モードは、[タイポロジを使用したプロセスの検証](../../delivery/using/steps-validating-the-delivery.md#validation-process-with-typologies)で説明しています。
* **[!UICONTROL ワークフローを使用してパーソナライゼーションデータを準備]**：このオプションでは、自動ワークフローの配信に含めるパーソナライゼーションデータを準備できます。これにより、大量のデータを処理する場合（特にパーソナライゼーションデータが FDA を通じて外部テーブルから提供される場合）、配信分析のパフォーマンスを大幅に向上させることが可能です。[外部データベース](../../platform/using/additional-options.md#optimizing-email-personalization-with-external-data)の節を参照してください。
* **[!UICONTROL 別のプロセスでジョブを開始]**：このオプションを選択すると、別のプロセスで配信分析を開始できます。分析機能は、デフォルトでは、Adobe Campaign アプリケーションサーバープロセス（web nlserver）を使用します。このオプションを選択すると、アプリケーションサーバーにエラーが発生した場合でも分析を完了できます。
* **[!UICONTROL ログの分析中に生成された SQL クエリを記録]**：分析フェーズ中、配信ログに SQL クエリのログを記録します。
* **[!UICONTROL 配信時にパーソナライゼーションスクリプトを無視]**：HTML コンテンツに含まれる JavaScript ディレクティブの解釈をスキップします。このオプションを選択すると、配信されるコンテンツ内に、**&lt;%=** タグで始まる JavaScript ディレクティブがそのまま表示されます。

### 分析の優先順位の設定 {#analysis-priority-}

配信をキャンペーンの一環として使用する場合は、「**[!UICONTROL 詳細設定]**」タブに特別なオプションが 1 つ追加されます。このオプションを使用すると、同じキャンペーンに含まれる配信の処理順を調整できます。

各配信は、送信前に分析されます。分析の所要時間は配信の抽出ファイルによって異なります。ファイルサイズが大きいほど、分析にかかる時間は長くなり、後に続く配信が遅くなります。

「**[!UICONTROL スケジューラーによるメッセージの準備]**」のオプションで、キャンペーンワークフローの配信分析を優先順位付けできます。

![](assets/delivery_analysis_priority.png)

配信が非常に大きい場合、低い優先順位を設定することが、同じワークフローに含まれる他の配信の遅延を防ぐために有効と考えられます。

>[!NOTE]
>
>「**[!UICONTROL 低アクティビティ時の実行をスケジュール]**」オプションを選択すると、大きな配信分析によってワークフロー全体の進行が遅くなるのを防ぐことができます。

## 配達確認の送信 {#sending-a-proof}

メッセージの設定にエラーが含まれていそうな箇所を見つけるために、配信の検証サイクルを設定することを強くお勧めします。必要に応じて、テスト受信者に配達確認を送信してコンテンツを承認するサイクルを実施します。この場合、変更を加えるたびに配達確認を送信して、コンテンツを承認することになります。

>[!NOTE]
>
>* 使用可能な検証モードについて詳しくは、[承認モードの変更](../../delivery/using/steps-validating-the-delivery.md#changing-the-approval-mode)で説明しています。
>* 配達確認のターゲットの設定について詳しくは、[特定の配達確認ターゲットの定義](../../delivery/using/steps-defining-the-target-population.md#defining-a-specific-proof-target)を参照してください。
>



配達確認を送信するには、以下の手順に従います。

1. [特定の配達確認ターゲットの定義](../../delivery/using/steps-defining-the-target-population.md#defining-a-specific-proof-target)の説明に従って、配達確認のターゲットを設定したことを確認します。
1. 配信ウィザードの上部のバーで「**[!UICONTROL 配達確認を送信]**」をクリックします。

   ![](assets/s_ncs_user_email_del_send_proof.png)

1. メッセージの分析を開始します。[配信の分析](../../delivery/using/steps-validating-the-delivery.md#analyzing-the-delivery)を参照してください。
1. これで、配信を送信できます（[配信の送信](../../delivery/using/steps-sending-the-delivery.md)を参照）。

   配信が送信されると、配達確認は自動的に作成されて番号が付けられ、配信リストに表示されます。コンテンツやプロパティにアクセスしたい場合は、配達確認を編集できます。詳しくは、この[ページ](../../delivery/using/monitoring-a-delivery.md#delivery-dashboard)を参照してください。

   ![](assets/s_ncs_user_delivery_validation_cycle_03a.png)

   >[!NOTE]
   >
   >配信に複数のメッセージ形式（HTML とテキスト）が含まれる場合は、ウィンドウ下部のセクションで、配達確認受信者に送信するメッセージの形式を選択できます。

   ![](assets/s_ncs_user_email_del_send_proof_formats.png)

配達確認を受信した検証グループからのコメントを踏まえて配信コンテンツを変更する場合は、変更後に分析を再度実行してから、再度配達確認を送信する必要があります。それぞれの新しい配達確認には、番号が付けられ、配信ログに記録されます。

配信が分析されると、ログ（「**[!UICONTROL 監査]**」タブ）の「**[!UICONTROL 配達確認]**」サブタブで、送信された様々な配達確認の記録を表示できます。

![](assets/s_ncs_user_delivery_validation_cycle_03.png)

配信のコンテンツが最終的に確定するまで、何度でも必要な回数だけ配達確認を送信する必要があります。その後、配信をメインターゲットに送信して検証サイクルを終了できます。

配信プロパティの「**[!UICONTROL 詳細設定]**」タブでは、配達確認のプロパティを定義できます。必要に応じて、受信者の除外ルールを上書きできます。

![](assets/s_ncs_user_wizard_email01_145.png)

次のオプションを使用できます。

* 最初のオプションを選択すると、配達確認のコピーを保持できます。
* 2 番目と 3 番目のオプションを使用すると、ブラックリストに記載されている強制隔離中の受信者とアドレスを保持できます。メインターゲットに対するこれらのオプション指定について詳しくは、[除外設定のカスタマイズ](../../delivery/using/steps-defining-the-target-population.md#customizing-exclusion-settings)を参照してください。これらのアドレスは、配信ターゲットの場合はデフォルトで除外されますが、配達確認ターゲットの場合はデフォルトで保持されます。
* 「**[!UICONTROL 配達確認の配信コードを保持]**」オプションを選択すると、配達確認の配信コードが、対応する配信の配信コードと同じ値になります。このコードは、配信ウィザードの最初の手順で指定されます。
* デフォルトでは、配達確認の件名の前には「配達確認#」が付けられます。ここで、「#」は配達確認の番号です。このプレフィックスは「**[!UICONTROL ラベルのプレフィックス]**」フィールドで変更できます。

## タイポロジを使用したプロセスの検証 {#validation-process-with-typologies}

メッセージを送信する前に、キャンペーンを分析して、コンテンツと設定を検証する必要があります。分析フェーズ中に適用されるチェックルールは、**タイポロジ**&#x200B;内に定義されています。E メールの場合、デフォルトでは、分析には次の点が含まれます。

* オブジェクトの検証
* URL と画像の検証
* URL ラベルの検証
* 購読解除リンクの検証
* 配達確認のサイズの検証
* 有効期間の検証
* ウェーブのスケジュールの検証

各配信に適用されるタイポロジは、配信パラメーターの「**[!UICONTROL タイポロジ]**」タブで選択されます。

**[!UICONTROL 管理／キャンペーン管理／タイポロジ管理]**&#x200B;ノードで、検証のルール、内容、実行順、詳しい説明を表示および編集できます。

このノードから、新しいルールを作成し、新しいタイポロジを定義できます。ただし、これらのタスクは JavaScript の知識があるエキスパートユーザー向けに用意されています。

現在のタイポロジを編集するには、「**[!UICONTROL タイポロジ]**」フィールドの右にある&#x200B;**[!UICONTROL リンクを編集]**&#x200B;アイコンをクリックします。

![](assets/s_ncs_user_email_del_typo_tab.png)

「**[!UICONTROL ルール]**」タブに、適用するタイポロジルールの一覧が表示されます。ルールを 1 つ選択し、「**[!UICONTROL 詳細]**」アイコンをクリックすると、設定が表示されます。

![](assets/s_ncs_user_email_del_typo_rules_edit.png)

>[!NOTE]
>
>**[!UICONTROL 判別]**&#x200B;タイプのタイポロジは、営業頻度管理のフレームワーク内で使用します。詳しくは、[この節](../../campaign/using/about-marketing-resource-management.md)を参照してください。

## 承認モードの変更 {#changing-the-approval-mode}

配信プロパティの「**[!UICONTROL 分析]**」タブでは、検証モードを選択できます。分析時に警告が発生した場合（例えば、あるアクセント記号付き文字が配信の件名に含まれていた場合）、配信を設定して、配信を実行するかどうかを定義できます。デフォルトでは、分析フェーズの最後に、メッセージの送信をユーザーが確認する必要があります（**手動**&#x200B;検証）。

承認モードのフィールドで、ドロップダウンリストから別の承認モードを選択します。

![](assets/s_ncs_user_email_del_validation_mode.png)

選択できる承認モードは次のとおりです。

* **[!UICONTROL 手動]**：分析の終了時に、配信の送信開始をユーザーが確認する必要があります。「**[!UICONTROL 配信を確定]**」ボタンをクリックすると、配信が開始されます。
* **[!UICONTROL 半自動]**：分析フェーズで警告が発生しなかった場合には送信が自動的に開始されます。
* **[!UICONTROL 自動]**：分析が終了した時点で、その結果にかかわらず送信が自動的に開始されます。
