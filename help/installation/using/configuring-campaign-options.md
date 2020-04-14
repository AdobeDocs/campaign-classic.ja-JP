---
title: キャンペーンオプション
seo-title: キャンペーンオプション
description: キャンペーンオプション
seo-description: null
page-status-flag: never-activated
uuid: 32e85e41-6898-4fb3-90c8-2201ceea2e91
contentOwner: sauviat
products: SG_CAMPAIGN/CLASSIC
audience: installation
content-type: reference
topic-tags: appendices
discoiquuid: 9c1884f6-1dd8-41ab-b8dc-604c8cc2dc89
index: y
internal: n
snippet: y
translation-type: tm+mt
source-git-commit: 05831dbcf2450600a9f2f91f87c4440d7e599c9d

---


# Campaign Classic のオプションのリスト{#configuring-campaign-options}

ノード **[!UICONTROL Administration / Platform / Options]** を使用して、Adobe Campaignオプション

>[!NOTE]
>
>Adobe Campaignオプションの変更または更新は、エキスパートユーザーのみが実行できます。

一部はインストール時に組み込まれ、他のキャンペーンは必要に応じて手動で追加できます。 使用できるオプションは、インスタンスと共にインストールされるパッケージによって異なります。

## 配信 {#delivery}

<table> 
 <thead> 
  <tr> 
   <th> オプション名 </th> 
   <th> 説明 </th> 
  </tr> 
 </thead> 
 <tbody> 
  <tr> 
   <td> <span class="uicontrol">Deliverability_LastBroadLogMsgDate</span><br /> </td> 
   <td> 配信品質インスタンスから最後に取得されたbroadLogMsgの日付。<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">Deliverability_LastBroadLogMsgSent</span><br /> </td> 
   <td> 配信品質インスタンスに最後に送信されたbroadLogMsgの日付。<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">DmRendering_cuid</span><br /> </td> 
   <td> 配信レポート識別子。識別子を取得するには、サポートにお問い合わせください。<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">DmRendering_SeedTargets</span><br /> </td> 
   <td> 受信ボックスレンダリングのテストアドレスを使用するスキーマのリスト。
(要素名はコンマ区切りで指定)
例 : custom_nms_recipient.<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">NmsBilling_MainActionThreshold</span><br /> </td> 
   <td> 配信を請求レポートのメインの配信と見なすための最小受信者数。<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">NmsBroadcast_DefaultProvider</span><br /> </td> 
   <td> 新しいテンプレート用のデフォルトのルーティングサービスプロバイダー.<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">NmsBroadcast_LogsPerTransac</span><br /> </td> 
   <td> 一度に1つの配信に対して作成されたBroadLogの数。<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">NmsBroadcast_MaxDelayPerTransac</span><br /> </td> 
   <td> トランザクションごとのログ(broadLogs)の挿入（テーブル内）:バッチごとに処理する行数。<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">NmsBroadcast_MidAnalyzeBatchSize</span><br /> </td> 
   <td> ミッドソーシング配信を分析する際の配信分割のグループ化サイズ.<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">NmsBroadcast_MsgValidityDuration</span><br /> </td> 
   <td> デフォルトの配信期間 (秒).<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">NmsBroadcast_RegexRules</span><br /> </td> 
   <td> 配信メッセージを正規化するための正規表現.<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">NmsBroadcast_RemoveBlackList</span><br /> </td> 
   <td> 値として「1」を入力すると、連絡を希望しない受信者を除外できます。<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">NmsBroadcast_RemoveDuplicatesRecipients</span><br /> </td> 
   <td> 値として「1」を入力すると、自動的に無視される重複。<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">Nms_DefaultRcpSchema</span><br /> </td> 
   <td> Adobe Campaignは、「Nms_DefaultRcpSchema」グローバル変数を使用して、デフォルトの受信者データベース(nms:受信者)との対話を行います。<br /> オプションの値は、外部のオプションテーブルと一致するスキーマの名前に対応する必要があります。受信者の値は、<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">NmsDelivery_ErrorAddressMasks</span><br /> </td> 
   <td> メッセージに返信する際に使用するエラーアドレスの構文を定義できます。<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">NmsDelivery_FromAddressMasks</span><br /> </td> 
   <td> メッセージの送信時に使用するFromアドレスの構文を定義できます。<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">NmsDelivery_MaxRetry</span><br /> </td> 
   <td> 分析中の再試行の最大数.<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">NmsDelivery_PublishingScript</span><br /> </td> 
   <td> パブリッシュスクリプト.<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">NmsDelivery_NoCountBroadLogMsgPush</span><br /> </td> 
   <td> プッシュメッセージの broadLogMsg カウントを無効にする.<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">NmsDeliveryWizard_ShowDeliveryWeight</span><br /> </td> 
   <td> メッセージの重み付けを配信ウィザードに表示します.<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">NmsEmail_DefaultErrorAddr</span><br /> </td> 
   <td> ユーザーが空のままにした場合、インスタンスのレベルで電子メール配信に使用されるデフォルトの「エラー」電子メールアドレス。<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">NmsEmail_DefaultFromAddr</span><br /> </td> 
   <td> ユーザーが空のままにした場合、インスタンスのレベルで電子メール配信に使用されるデフォルトの「送信者」電子メールアドレス。<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">NmsEmail_DefaultReplyToAddr</span><br /> </td> 
   <td> ユーザーが空のままにした場合、インスタンスのレベルで電子メール配信に使用されるデフォルトの「返信」電子メールアドレス。<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">NmsEmail_ExpOrganization</span><br /> </td> 
   <td> 顧客の共通名. 一部の警告メッセージで使用され、受信者に表示されます。<br /> 「*****または関連会社と連絡を取っているので、このメッセージを受け取っています。 *****"からのメッセージの受信を停止します。<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">NmsEmail_FromName</span><br /> </td> 
   <td> ユーザーが空のままにした場合、インスタンスのレベルで電子メールの配信に使用されるデフォルトの「送信者」のラベル。<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">NmsEmail_ReplyToName</span><br /> </td> 
   <td> ユーザーが空のままにした場合、インスタンスのレベルで電子メールの配信に使用されるデフォルトの「返信」ラベル。<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">NmsEmail_RetryCount</span><br /> </td> 
   <td> 電子メールメッセージの2再試行間の期間（秒）。<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">NmsEmail_RetryPeriod</span><br /> </td> 
   <td> 電子メール再試行の期間。<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">NmsForecast_MsgWeightFormula</span><br /> </td> 
   <td> 暫定的な配信メッセージの重み付けを計算するときに使用する数式.<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">NmsInmail_WhitelistEmails</span><br /> </td> 
   <td> List of authorized forwarding email addresses (from the inbound mail processing module). The addresses have to be separated by commas (or * to allow all). E.g. xyz@abc.com,pqr@abc.com.<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">NmsNPAI_EmailMaxError</span><br /> </td> 
   <td> チャネル「email」（デフォルトとして使用）:送信中のSOFTエラーに対して受け入れられる、受信者を強制隔離にする前のエラーの最大数。<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">NmsNPAI_EmailSignificantErrorDelay</span><br /> </td> 
   <td> チャネル「email」（デフォルトとして使用）:新しいSOFTエラーを考慮する前に、前回参照したSOFTエラー以降に費やす最小期間。<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">NmsNPAI_MobileMaxError</span><br /> </td> 
   <td> チャネル「mobile」:送信中のSOFTエラーに対して受け入れられる、受信者を強制隔離にする前のエラーの最大数。<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">NmsNPAI_MobileSignificantErrorDelay</span><br /> </td> 
   <td> チャネル「mobile」:新しいSOFTエラーを考慮する前に、前回参照したSOFTエラー以降に費やす最小期間。<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">NmsServer_MirrorPageUrl</span><br /> </td> 
   <td> URL of the mirror page server (by default, should be identical to NmsTracking_ServerUrl).<br /> It is the default value of email deliveries when the URL is not specified in the routing definition.<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">NmsPaper_SenderLine1</span><br /> </td> 
   <td> 送信者の住所の1行目。<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">NmsPaper_SenderLine3</span><br /> </td> 
   <td> 送信者の住所の3行目。<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">NmsPaper_SenderLine4</span><br /> </td> 
   <td> 送信者の住所の4行目。<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">NmsPaper_SenderLine6</span><br /> </td> 
   <td> 送信者の住所の6行目。<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">NmsPaper_SenderLine7</span><br /> </td> 
   <td> 送信者の住所の7行目。<br /> </td> 
  </tr>
    <tr> 
   <td> <span class="uicontrol">NmsOperation_DeliveryPreparationWindow</span><br /> </td> 
   <td><p>このオプションは、実行中の <span class="uicontrol"><a href="../../workflow/using/campaign.md">配信数をカウントする際に、operationMgt</a></span> 技術ワークフローで使用されます。</p>これにより、ステータスが矛盾する配信が実行中の配信の数から除外される日数を定義できます。</p><p>デフォルトでは、この値は「7」に設定されているので、7日より古い配信の整合性が失われます。</p></td> 
  </tr>
  <tr> 
   <td> <span class="uicontrol">NmsSMS_Priority</span><br /> </td> 
   <td> 送信されたSMSメッセージのパラメータ：メッセージの優先度を示すためにSMSゲートウェイに送信される情報。<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">NmsSMS_RetryCount</span><br /> </td> 
   <td> SMSメッセージを送信する際の再試行の数。<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">NmsSMS_RetryPeriod</span><br /> </td> 
   <td> SMSメッセージの再試行が実行される期間。<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">XtkEmail_Characters</span><br /> </td> 
   <td> E メールアドレスで有効な文字.<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">NmsMidSourcing_LogsPeriodHour</span><br /> </td>
   <td> 同期ワークフローが実行されるたびにリカバリされるブロードログの数を制限するために、最大期間（時間単位）を指定できます。</a>.<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">NmsMidSourcing_PrepareFlow</span><br /> </td> 
   <td> 並行して実行できるMidSourcingセッションの最大呼び出し数（デフォルトでは3）。<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">NMS_ActivateOwnerConfirmation</span><br /> </td> 
   <td><p> 特定の演算子またはオペレーターのグループが配信のプロパティで配信を開始するように指定されている場合、配信の担当者が送信を確認できるようにします。</p><p> これを行うには、値として「1」を入力して、このオプションをアクティブにします。 このオプションを非アクティブにするには、「0」と入力します。</p><p> すると、送信確認プロセスがデフォルトとして機能します。つまり、配信プロパティで送信用に指定されたオペレーターまたはオペレーターのグループ（または管理者）のみが、送信を確認し、実行できるようになります。<a href="../../campaign/using/marketing-campaign-deliveries.md#starting-an-online-delivery">この節</a>を参照してください。</p> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">NmsMTA_Alert_Delay</span><br /> </td> 
   <td> カスタムの遅延（分単位）。その後、配信が「delayed」と見なされ、デフォルトで30分になります。<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">XtkBarcode_SpecialChar</span><br /> </td> 
   <td> Code128 の特殊文字のサポートを有効化 / 無効化.<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">NmsLine_AESKey</span><br /> </td> 
   <td> URL をエンコードするために「lineImage」サーブレットで使用される AES キー (LINE チャネル).<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">NmsWebSegments_LastStates</span><br /> </td> 
   <td> Webセグメントとその状態を含むオプションの名前。<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">NmsUserAgentStats_LastConsolidation</span><br /> </td> 
   <td> NmsUserAgent統計の最終 <span class="uicontrol">統合日</span> 。<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">XtkSecurity_Restrict_EditXML</span> </td> 
   <td> こ追加のオプションに「0」値を指定すると、配信のXMLコードのエディションが無効になります(右クリック/ <span class="uicontrol">XMLソースを編集</span> 、または <span class="uicontrol"></span> Ctrl + F4ショートカット)。<br /> </td> 
  </tr> 
  <!--<tr> 
   <td> <span class="uicontrol">EMTA_BCC_ADDRESS</span> </td> 
   <td> BCC email address for Momentum to send a raw copy of the sent emails. <br /> </td> 
  </tr> 
 </tbody> 
</table>-->

## リソース {#resources}

<table> 
 <thead> 
  <tr> 
   <th> オプション名 </th> 
   <th> 説明 </th> 
  </tr> 
 </thead> 
 <tbody> 
  <tr> 
   <td> <span class="uicontrol">NcmResourcesDir</span><br /> </td> 
   <td> リソースクライアントコンソールで発行するAdobe Campaignの場所です。 <a href="../../delivery/using/formatting.md#image-referencing">この節</a>を参照してください。<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">NcmResourcesDirPreview</span><br /> </td> 
   <td> プレビュー用のリソースの場所をAdobe Campaignクライアントコンソールで表示します。 <a href="../../delivery/using/formatting.md#image-referencing">この節</a>を参照してください。<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">NmsDelivery_DefaultIgnoredImage</span><br /> </td> 
   <td> アップロード時にスキップする画像の URL マスクのリスト.<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">NmsDelivery_ImagePublishing</span> </td> 
   <td> 画像のアップロードの設定. 値は、なし/追跡/スクリプト/リスト（演算子のオプション設定で上書き可能）にできます。 </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">NmsDelivery_ImageSubDirectory</span><br /> </td> 
   <td> サーバー上の画像を保存するフォルダー.<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">NmsServer_LogoPath</span><br /> </td> 
   <td> ロゴを表示するスペース.<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">NcmPublishingDir</span><br /> </td> 
   <td> パブリッシュ用ルートフォルダー.<br /> HTMLおよびテキストコンテンツの生成について詳しくは、この節を参 <a href="../../delivery/using/using-a-content-template.md">照してくださ</a>い。<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">XtkImageUrl</span><br /> </td> 
   <td> ブラウザーで使用する画像を保存する配信を定義し、ブラウザーで取得できるようにします。<br /> ビルドバージョン&lt;= 5098の場合、インスタンスにアップロードされた画像のURLを使用します。<br /> ビルドバージョン5098より前の場合は、配信のパブリックURLまたは <span class="uicontrol">XtkFileRes_Public_URL</span> オプションのURLを使用します。<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">NmsDelivery_MediaInstance</span><br /> </td> 
   <td> 画像をアップロードする際のインスタンス名を設定できます。<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">NmsDelivery_MediaPassword</span><br /> </td> 
   <td> 画像のアップロード用のパスワードを設定できます。<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">NmsDelivery_MediaServers</span><br /> </td> 
   <td> 画像をアップロードするためのメディアURLを設定できます。<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">NmsBroadcast_MsgWebValidityDuration</span><br /> </td> 
   <td> 配信のオンラインリソースのデフォルトの有効持続期間 (秒).<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">XtkFileRes_Public_URL</span><br /> </td> 
   <td> パブリックリソースファイルの新しい URL.<br /> </td> 
  </tr> 
 </tbody> 
</table>

## キャンペーンとワークフローの管理 {#campaign-e-workflow-management}

<table> 
 <thead> 
  <tr> 
   <th> オプション名 </th> 
   <th> 説明 </th> 
  </tr> 
 </thead> 
 <tbody> 
  <tr> 
   <td> <span class="uicontrol">CrmMarketingActivityWindow</span><br /> </td> 
   <td> この月数で表示するマーケティング履歴。<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">NmsOperation_Duration</span><br /> </td> 
   <td> キャンペーンのデフォルトの有効期間 (秒).<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">NmsOperation_LimitConcurrency</span><br /> </td> 
   <td> operationMgtワークフローによって開始され、一度に処理できる配信/ワークフロー/仮説/シミュレーションジョブの最大数。<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">NmsOperation_OperationMgtDebug</span><br /> </td> 
   <td> operationMgt技術的なワークフローの実 <a href="../../workflow/using/campaign.md">行を監視できます</a> 。 アクティブ化されると（値「1」）、実行情報はワークフロー監査ログに記録されます。<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">NmsOperation_TimeRange</span><br /> </td> 
   <td> スケジュールモードのターゲティング期間と抽出条件。<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">Workflow_AnalysisThreshold</span><br /> </td> 
   <td> テーブルの統計の自動再計算により影響を受けるレコードの数。<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">XtkReport_Logo</span><br /> </td> 
   <td> エクスポートされたレポートの右上隅に表示するロゴ.<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">NmsServer_PausedWorkflowPeriod</span><br /> </td> 
   <td> Number of days to wait between checks for paused workflows.<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">NmsCampaign_Activate_OwnerConfirmation</span><br /> </td> 
   <td> 値として「1」を入力し、配信の所有者による操作の検証をアクティブ化します。 このオプションを非アクティブにするには、「0」と入力します。<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">NmsAsset_JavascriptExt</span><br /> </td> 
   <td> ワークフローの「マーケティングリソース通知」に読み込む追加のJSアクティビティ。<br /> </td> 
  </tr> 
 </tbody> 
</table>

## セキュリティ {#security}

<table> 
 <thead> 
  <tr> 
   <th> オプション名 </th> 
   <th> 説明 </th> 
  </tr> 
 </thead> 
 <tbody> 
  <tr> 
   <td> <span class="uicontrol">XtkAcceptOldPasswords</span><br /> </td> 
   <td> （インストール互換モード：build&gt;6000）「1」が入力されると、このオプションは保存されたパスワードの互換性モードをアクティブにします。 このオプションを変更すると、データベースに保存されている古いパスワードが使用されなくなります。<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">XtkKey</span><br /> </td> 
   <td> This key is used to encrypt most passwords in the database. (external accounts, LDAP password...).<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">XtkSecurity_Allow_PrivilegeEscalation</span><br /> </td> 
   <td> 1を選択した場合、このオプションを使用してjavascriptのprivilegeEscalationを許可します。<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">XtkSecurity_Disable_ControlsOnFileDownload</span><br /> </td> 
   <td> 1を選択すると、ファイルのダウンロード中（fileDownload.jsp経由）にACLコントロールが無効になります。<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">XtkSecurity_Disable_JSFileSandboxing</span><br /> </td> 
   <td> 1を選択すると、JavaScript内のファイルサンドボックスが無効になります。<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">XtkSecurity_SaveOptions_AllowNonAdmin</span><br /> </td> 
   <td> 'true'に設定した場合、xtkOption値を更新する権限を持つ管理者以外の演算子がデプロイメントウィザードから実行されます。<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">XtkSecurity_Unsafe_DecryptString</span><br /> </td> 
   <td> 1を選択した場合、このオプションではdecryptStringを使用して一部のパスワードを復号化できます。<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">XtkTraceDeleteLogin</span><br /> </td> 
   <td> 「1」値を入力し、レコードを削除する前に「変更者」フィールドを変更して、mDataの監査証跡情報を持つ要素の削除を追跡します。<br /> </td> 
  </tr> 
 </tbody> 
</table>

## Message Center {#message-center}

<table> 
 <thead> 
  <tr> 
   <th> オプション名 </th> 
   <th> 説明 </th> 
  </tr> 
 </thead> 
 <tbody> 
  <tr> 
   <td> <span class="uicontrol">MC_EnlictionCustomJs</span><br /> </td> 
   <td> JavaScriptライブラリをパーソナライズし、イベントを強化。次の2つの関数の実装を含める必要があります。<br /> 
    <ul> 
     <li> <p> <span class="uicontrol">enrichRtEvents(aiEventId);</span> :データベース内のイベントをリッチ化し、保存し <span class="uicontrol">ます</span> (aiEventIdは、処理されたリアルタイムイベントの表に対応します)。</p> </li> 
     <li> <p> <span class="uicontrol">enrichBatchEvents(aiEventId);</span> :データベース内のイベントを強化し、保存し <span class="uicontrol">ます</span> (aiEventIdは、処理されたバッチイベントのIDテーブルに対応します)。</p> </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">MC_LastUpdateFromBL</span><br /> </td> 
   <td> 配信ログ経由での前回のイベントステータス更新の日付。<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">MC_RoutingCustomJs</span><br /> </td> 
   <td> JavaScriptライブラリをカスタマイズし、ルーティングイベント用に。次の2つの関数の実装を含める必要があります。<br /> 
    <ul> 
     <li> <p> <span class="uicontrol">dispatchRtEvent(iEventId);</span> :リアルタイムイベントを処理するために選択されたトランザクションメッセージの内部名を返します( <span class="uicontrol">iEventId</span> は、処理されたリアルタイムイベントのIDに対応します)。</p> </li> 
     <li> <p> <span class="uicontrol">dispatchBatchEvent(iEventId);</span> :バッチイベントを処理するために選択されたトランザクションメッセージの内部名を返します( <span class="uicontrol">iEventId</span> は、処理されたバッチイベントのIDに対応します)。</p> </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">MC_RtEventAvgDeliveryTimeAlert</span><br /> </td> 
   <td> リアルタイムイベントの平均送信時間のアラートしきい値.<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">MC_RtEventAvgDeliveryTimeWarning</span><br /> </td> 
   <td> リアルタイムイベントの平均送信時間の警告しきい値。<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">MC_RtEventAvgProcessTimeAlert</span><br /> </td> 
   <td> リアルタイムイベントの平均処理時間のアラートしきい値。<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">MC_RtEventAvgProcessTimeWarning</span><br /> </td> 
   <td> リアルタイムイベントの平均処理時間の警告しきい値。<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">MC_RtEventAvgQueueAlert</span><br /> </td> 
   <td> 待機中リアルタイムイベントの平均数のアラートしきい値。<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">MC_RtEventAvgQueueTimeAlert</span><br /> </td> 
   <td> リアルタイムイベントの平均キュー時間のアラートしきい値。<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">MC_RtEventAvgQueueTimeWarning</span><br /> </td> 
   <td> リアルタイムイベントの平均キュー時間の警告しきい値。<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">MC_RtEventAvgQueueWarning</span><br /> </td> 
   <td> 待機中リアルタイムイベントの平均数の警告しきい値。<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">MC_RtEventErrorAlert</span><br /> </td> 
   <td> リアルタイムイベントの処理エラーのアラートしきい値。<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">MC_RtEventErrorWarning</span><br /> </td> 
   <td> リアルタイムイベントの処理エラーの警告しきい値。<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">MC_RtEventMaxQueueAlert</span><br /> </td> 
   <td> 待機中リアルタイムイベントの最大数のアラートしきい値。<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">MC_RtEventMaxQueueWarning</span><br /> </td> 
   <td> 待機中リアルタイムイベントの最大数の警告しきい値。<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">MC_RtEventMinQueueAlert</span><br /> </td> 
   <td> 待機中リアルタイムイベントの最小数のアラートしきい値。<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">MC_RtEventMinQueueWarning</span><br /> </td> 
   <td> 待機中リアルタイムイベントの最低数の警告しきい値。<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">MC_RtEventQueueAlert</span><br /> </td> 
   <td> 保留中リアルタイムイベントのキューのアラートしきい値。<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">MC_RtEventQueueWarning</span><br /> </td> 
   <td> 保留中リアルタイムイベントのキューの警告しきい値。<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">MC_RtEventThroughputAlert</span><br /> </td> 
   <td> リアルタイムイベントのスループットのアラートしきい値。<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">MC_RtEventThroughputWarning</span><br /> </td> 
   <td> リアルタイムイベントのスループットの警告しきい値。<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">NmsMessageCenter_RoutingBatchSize</span><br /> </td> 
   <td> イベントのルーティングに使用する再グループ化のサイズ<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">MC_LastRtEventStat</span><br /> </td> 
   <td> RtEventステータス（データが取得される前の最終日）のポインターを更新します。<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">NmsLine_MessageCenterURL</span><br /> </td> 
   <td> Message Center server URL used to send welcome messages (LINE channel).<br /> </td> 
  </tr> 
 </tbody> 
</table>

## データベース {#database}

<table> 
 <thead> 
  <tr> 
   <th> オプション名 </th> 
   <th> 説明 </th> 
  </tr> 
 </thead> 
 <tbody> 
  <tr> 
   <td> <span class="uicontrol">NmsCleanup_LastCleanup</span><br /> </td> 
   <td> クリーンアップ処理が最後に実行された時刻を定義します。<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">NmsCleanup_BroadLogPurgeDelay</span><br /> </td> 
   <td> <p>ブロードローグがデータベースから消去されるまでの遅延を定義できます。</p><p>このオプションは、インターフェイス内で遅延が変更されると自動的に作成されます。 オプションリストで値を変更する場合は、秒単位で表します。</p><br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">NmsCleanup_EventHistoPurgeDelay</span><br /> </td> 
   <td><p> データベースのデータを消去するまでのイベント履歴の遅延を定義できます。</p><p>
   このオプションは、インターフェイス内で遅延が変更されると自動的に作成されます。 オプションリストで値を変更する場合は、秒単位で表します。</p><br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">NmsCleanup_EventPurgeDelay</span><br /> </td> 
   <td><p> データベースからデータを消去するまでのイベントの遅延を定義できます。</p><p>このオプションは、インターフェイス内で遅延が変更されると自動的に作成されます。 オプションリストで値を変更する場合は、秒単位で表します。</p><br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">NmsCleanup_EventStatPurgeDelay</span><br /> </td> 
   <td><p> データベースの統計が消去されるまでのイベントの遅延を定義できます。</p><p>このオプションは、インターフェイス内で遅延が変更されると自動的に作成されます。 オプションリストで値を変更する場合は、秒単位で表します。</p><br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">NmsCleanup_PropositionPurgeDelay</span><br /> </td> 
   <td><p> データベースから提案が削除されるまでの遅延を定義できます。</p><p> このオプションは、インターフェイス内で遅延が変更されると自動的に作成されます。 オプションリストで値を変更する場合は、秒単位で表します。</p><br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">NmsCleanup_QuarantineMailboxFull</span><br /> </td> 
   <td> <p>データベースからデータを消去するまでの強制隔離の遅延を定義できます。</p><p> このオプションは、インターフェイス内で遅延が変更されると自動的に作成されます。 オプションリストで値を変更する場合は、秒単位で表します。</p><br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">NmsCleanup_RecycledDeliveryPurgeDelay</span><br /> </td> 
   <td> <p>データベースからリサイクル配信を消去する遅延を定義できます。</p><p> このオプションは、インターフェイス内で遅延が変更されると自動的に作成されます。 オプションリストで値を変更する場合は、秒単位で表します。</p><br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">NmsCleanup_RejectsPurgeDelay</span><br /> </td> 
   <td> <p>データベースから拒否を消去するまでの遅延を定義できます。</p><p>このオプションは、インターフェイス内で遅延が変更されると自動的に作成されます。 オプションリストで値を変更する場合は、秒単位で表します。</p><br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">NmsCleanup_TrackingLogPurgeDelay</span><br /> </td> 
   <td> <p>データベースからデータを消去するまでのトラッキングログの遅延を定義できます。</p><p>このオプションは、インターフェイス内で遅延が変更されると自動的に作成されます。 オプションリストで値を変更する場合は、秒単位で表します。</p><br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">NmsCleanup_TrackingStatPurgeDelay</span><br /> </td> 
   <td><p> データベースから追跡統計が消去されるまでの遅延を定義できます。</p><p> このオプションは、インターフェイス内で遅延が変更されると自動的に作成されます。 オプションリストで値を変更する場合は、秒単位で表します。</p><br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">NmsCleanup_VisitorPurgeDelay</span><br /> </td> 
   <td> <p>データベースからデータを消去するまでの訪問者の遅延を定義できます。</p><p> このオプションは、インターフェイス内で遅延が変更されると自動的に作成されます。 オプションリストで値を変更する場合は、秒単位で表します。</p><br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">NmsCleanup_WorkflowResultPurgeDelay</span><br /> </td> 
   <td> <p>ワークフローの結果がデータベースから消去されるまでの遅延を定義できます。</p><p> このオプションは、インターフェイス内で遅延が変更されると自動的に作成されます。 オプションリストで値を変更する場合は、秒単位で表します。</p><br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">WdbcCapabilities_AzureDw</span><br /> </td> 
   <td> Azure SQL Datawarehouse コネクタオプション.<br /> </td> 
  </tr>
   <tr> 
   <td> <span class="uicontrol">WdbcKillSessionPolicy</span><br /> </td> 
   <td>以下の潜在的な値に従って、すべてのワークフローとPostgreSQLデータベースクエリの無条件停止動作に影響を与えます。<ul>
    <li><p>0 — デフォルト：ワークフロープロセスを停止し、データベースに影響を与えない<p></li>
    <li><p>1 - pg_cancel_backend:ワークフロープロセスを停止し、データベース内のクエリをキャンセルします<p></li>
    <li><p>2 - pg_terminate_backend:ワークフロープロセスを停止し、データベース内のクエリを終了します。<p></li></ul></td> 
  </tr>  
  <tr> 
   <td> <span class="uicontrol">WdbcOptions_TableSpaceIndex</span><br /> </td> 
   <td> Adobe Campaign の標準テーブルのインデックスを格納するためのテーブル領域の名前.<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">WdbcOptions_TableSpaceUser</span><br /> </td> 
   <td> Adobe Campaign の標準テーブルのデータを格納するためのテーブル領域の名前.<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">WdbcOptions_TableSpaceWork</span><br /> </td> 
   <td> Adobe Campaign 作業用テーブルのデータを格納するテーブル領域の名前.<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">WdbcOptions_TableSpaceWorkIndex</span><br /> </td> 
   <td> Adobe Campaign 作業用テーブルのインデックスを含むテーブル領域の名前.<br /> </td> 
  </tr> 
    <tr> 
   <td> <span class="uicontrol">WdbcOptions_TempDbName</span><br /> </td> 
   <td> バックアップとレプリケーションを最適化するために、Microsoft SQL Server上でテーブルを作成するための別のデータベースを設定できます。 このオプションは、一時データベースの名前に対応します。指定した場合、作業テーブルはこのデータベースに書き込まれます。 例：「tempdb.dbo」 （名前はドットで終わる必要があります）。</desc> <a href="../../production/using/rdbms-specific-recommendations.md#microsoft-sql-server">詳細を表示</a> <br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">WdbcTimeZone</span><br /> </td> 
   <td> Adobe Campaignインスタンスのタイムゾーン。 設定を参 <a href="../../installation/using/time-zone-management.md#configuration" target="_blank">照してくださ</a>い。<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">WdbcUseNChar</span><br /> </td> 
   <td> データベースの文字列フィールドはNCharで定義されていますか？<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">WdbcUseTimeStampWithTZ</span><br /> </td> 
   <td> データベースの「datetime」フィールドにタイムゾーン情報が格納されますか。<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">XtkDatabaseId</span><br /> </td> 
   <td> データベースのID。 Unicode DataBaseの場合は'u'で始まります。<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">XtkInstancePrefix</span><br /> </td> 
   <td> 自動生成された内部名に追加されるプレフィックス.<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">XtkQuery_スキーマ_LineCount</span><br /> </td> 
   <td> 結果の最大数は、xtk:schema および xtk:srcSchema のクエリによって返されます。<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">XtkSequence_AutoGeneration</span><br /> </td> 
   <td> この時点以降に作成されたカスタマイズされたスキーマは、autok="true"で属性"pkSequence"を指定しないと、自動生成されたシーケンス"auto_ &lt;schemanamespace&gt; &lt;schemaname&gt; _seqが生成されます。 
   </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">NlMigration_KeepFolderStructure</span><br /> </td> 
   <td> 移行時に、ツリー構造は新しいバージョン標準に基づいて自動的に再編成されます。<br /> このオプションを使用すると、ナビゲーションツリーの自動移行を無効にできます。 使用する場合は、移行後に古いフォルダを削除する必要があります。新しいフォルダを追加し、必要なチェックをすべて実行します。<br /> 
    <ul> 
     <li> <p> <span class="uicontrol">データタイプ：</span> 整数</p> </li> 
     <li> <p> <span class="uicontrol">値（テキスト）</span> :1 </p> </li> 
    </ul> このオプションは、標準搭載のナビゲーションツリーが変更を加えすぎた場合にのみ使用してください。<br /> 詳しくは、この節を参照し <a href="../../migration/using/specific-configurations-in-v5-11.md#campaign-vseven-tree-structure">てください</a>。<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">NmsLastErrorStatCoalesce</span><br /> </td> 
   <td> NmsEmailErrorStatテーブルのクリーンアップの <span class="uicontrol">最終処理日</span> 。<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">PostUpgradeLastError</span><br /> </td> 
   <td> 次の構文に従って、アップグレード後に発生したエラーに関する情報です。<br /><strong>{ビルド番号}:{モード：pre/post/...}:{エラーが発生した'lessThan'/'greaterOrEquelThan' +サブステップ}</strong> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">XtkCleanup_NoStats</span><br /> </td> 
   <td> 「1」の値を入力して、統計の更新がクリーンアップワークフローで実行されないようにします。<br /> </td> 
  </tr> 
 </tbody> 
</table>

## Integration {#integration}

<table> 
 <thead> 
  <tr> 
   <th> オプション名 </th> 
   <th> 説明 </th> 
  </tr> 
 </thead> 
 <tbody> 
  <tr> 
   <td> <span class="uicontrol">AEMResourceTypeFilter</span><br /> </td> 
   <td> 使用できるAEMリソースのタイプです。Adobe Campaign 値はコンマで区切る必要があります。<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">nmsPipeline_config</span><br /> </td> 
   <td> Experience Cloud Triggersを設定できます。 データ型は「long text」で、JSON形式である必要があります。 詳しくは、 <a class="anchorLink" href="https://helpx.adobe.com/campaign/kb/triggers-and-campaign.html#PipelineoptionNmsPipelineConfig" target="_blank">Experience Cloud TriggersをExperience Classicで使用する方法をAdobe Campaignします</a>。<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">LASTIMPORT_&lt;%=instance.internalName%&gt;_&lt;%=activityName%&gt;</span><br /> </td> 
   <td> このオプションは、CRMコネクタを介してサードパーティのシステムからデータをインポートする場合に使用されます。 このオプションを有効にすると、前回の読み込み以降に変更されたオブジェクトのみを収集できます。 このオプションは、次のように手動で作成し、設定する必要があります。 
    <ul> 
     <li> <p> <span class="uicontrol">内部名</span> :LASTIMPORT_&lt;%=instance.internalName%&gt;_&lt;%=activityName%&gt;</p> </li> 
     <li> <p> <span class="uicontrol">値（フィールド）</span> :最後にインポートされた日付（yyyy/MM/dd hh:mm:ss形式）。 </p> </li> 
    </ul><br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">TNT_EdgeServer</span><br /> </td> 
   <td> 統合に使用される Adobe Target サーバー。このオプションは、デフォルトで選択されています。この値は Adobe Target のドメインサーバーに対応し、値 /m2 が続きます。例：tt.omtrdc.net/m2。<br /> この節を <a href="../../integrations/using/configuring-the-integration-with-adobe-target.md">参照してください</a>。<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">TNT_TenantName</span><br /> </td> 
   <td> Adobe Target 組織名。この値は Adobe Target のクライアント名に対応します。<br /> この節を <a href="../../integrations/using/configuring-the-integration-with-adobe-target.md">参照してください</a>。<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">AAM_DataSourceId</span><br /> </td> 
   <td> Adobe Adobe Managerとの統合に使用するオーディエンス。<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">AAM_DestinationId</span><br /> </td> 
   <td> Adobe Adobe Managerとの統合に使用するオーディエンス。<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">WdbcCapabilities_Teradata</span><br /> </td> 
   <td> Teradata コネクタオプション.<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">WdbcCapabilities_Hive</span><br /> </td> 
   <td> Hive コネクタオプション.<br /> </td> 
  </tr> 
 </tbody> 
</table>

## オファー {#offers}

<table> 
 <thead> 
  <tr> 
   <th> オプション名 </th> 
   <th> 説明 </th> 
  </tr> 
 </thead> 
 <tbody> 
  <tr> 
   <td> <span class="uicontrol">NmsCoupons_MaxPerTransac</span><br /> </td> 
   <td> SQLトランザクションごとに更新されたクーポンの数。<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">NmsInteraction_LastPropositionSynchControl_</span><br /> </td> 
   <td> '+ [提案のスキーマ] + "_" + extAccountSource.@executionInstanceId + [proposition'sスキーマ] + "_" + vars.executionInstanceIdFilter<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">NmsInteraction_LastPropositionSynchExec_</span><br /> </td> 
   <td> '+ [提案のスキーマ] + "_" + extAccountSource.@executionInstanceId + "_" + extAccountTarget。@executionInstanceId<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">NmsInteraction_SynchWorkflowIds</span><br /> </td> 
   <td> 同期ワークフローのトラッキング。<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">NmsInteraction_UseDaemon</span><br /> </td> 
   <td> Enable/disable asynchronous proposition writing ("0" to disable, "1" to enable).<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">NmsModule_CouponsEnabled</span><br /> </td> 
   <td> クーポンを有効にできます。<br /> </td> 
  </tr> 
 </tbody> 
</table>

## サーバー {#server}

<table> 
 <thead> 
  <tr> 
   <th> オプション名 </th> 
   <th> 説明 </th> 
  </tr> 
 </thead> 
 <tbody> 
  <tr> 
   <td> <span class="uicontrol">NmsExecutionInstanceId</span><br /> </td> 
   <td> 実行インスタンスの識別子.<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">NmsServer_CustomerId</span><br /> </td> 
   <td> 請求レポートの送信時に使用する顧客識別子.<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">NmsServer_IntranetURL</span><br /> </td> 
   <td> アプリケーションサーバーにアクセスするための内部ベース URL.<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">NmsServer_LastPostUpgrade</span><br /> </td> 
   <td> 前回のアップグレードの前にACインスタンスのビルド番号。<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">NmsServer_URL</span><br /> </td> 
   <td> パブリック Web アプリケーションサーバーのベース URL.<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">XtkPassUnknownSQLFunctionsToRDBMS</span><br /> </td> 
   <td> 移行後も、古い非宣言SQL関数を引き続き使用できます。 セキュリティ上のリスクがあるので、このオプションの使用を避けることを強くお勧めします。<br /> </td> 
  </tr> 
 </tbody> 
</table>

## トラッキング {#tracking}

<table> 
 <thead> 
  <tr> 
   <th> オプション名 </th> 
   <th> 説明 </th> 
  </tr> 
 </thead> 
 <tbody> 
  <tr> 
   <td> <span class="uicontrol">NmsTracking_Available</span><br /> </td> 
   <td> 追跡をアクティブにするオプション。<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">NmsTracking_ClickFormula</span><br /> </td> 
   <td> トラッキングする URL の計算スクリプト.<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">NmsTracking_ExtAccount</span><br /> </td> 
   <td> トラッキングサーバーの外部アカウントを定義します。<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">NmsTracking_Instance</span><br /> </td> 
   <td> トラッキングサーバー上でインスタンス名を定義できます。<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">NmsTracking_LastConsolidation</span><br /> </td> 
   <td> 前回、トラッキング情報が新しいデータと統合された時刻。<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">NmsTracking_OpenFormula</span><br /> </td> 
   <td> URL 計算スクリプトを開く.<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">NmsTracking_Password</span><br /> </td> 
   <td> トラッキングサーバーのパスワード<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">NmsTracking_Pointer</span><br /> </td> 
   <td> ポインターは、IDと日付を通じて処理された最後のイベントメッセージを追跡します。<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">NmsTracking_SecureServerUrl</span><br /> </td> 
   <td> フロントトラッキングサーバーのセキュア URL.<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">NmsTracking_ServerUrl</span><br /> </td> 
   <td> フロントトラッキングサーバーの URL.<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">NmsTracking_ServerUrlList</span><br /> </td> 
   <td> トラッキングサーバーに接続するために使用される URL のリスト.<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">NmsTracking_UserAgentRules</span><br /> </td> 
   <td> ブラウザー識別ルールセット.<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">NmsTracking_WebFormula</span><br /> </td> 
   <td> Web トラッキングタグの処理に使用するスクリプト.<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">NmsTracking_WebTrackingDelivery</span><br /> </td> 
   <td> Web トラッキング管理向けの仮想配信の名前。<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">NmsTracking_WebTrackingMode</span><br /> </td> 
   <td> Webトラッキングモードを定義できます。<br /> </td> 
  </tr> 
 </tbody> 
</table>

## プライバシー {#privacy}

<table> 
 <thead> 
  <tr> 
   <th> オプション名 </th> 
   <th> 説明 </th> 
  </tr> 
 </thead> 
 <tbody> 
  <tr> 
   <td> <span class="uicontrol">Privacy_Request_ConfirmDeletePending</span><br /> </td> 
   <td> オプション1を選択した場合は、2番目の手順で、インターフェイスで手動で削除を確認する必要があります。 そうしないと、データは確認なしで削除されます。<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">Privacy_Request_ConfirmDeletePendingDelay</span><br /> </td> 
   <td> 削除の確認待ちのリクエストとリクエストのキャンセルの間の遅延。<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">Privacy_Request_MaxErrorAllowed</span><br /> </td> 
   <td> プライバシーリクエストの処理中 / 削除中に許可されるエラーの最大数。<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">Privacy_Request_PurgeDelay</span><br /> </td> 
   <td> キューでのリクエストの作成とリクエストデータの削除の間の遅延。<br /> </td> 
  </tr> 
 </tbody> 
</table>

## LDAP {#ldap}

<table> 
 <thead> 
  <tr> 
   <th> オプション名 </th> 
   <th> 説明 </th> 
  </tr> 
 </thead> 
 <tbody> 
  <tr> 
   <td> <span class="uicontrol">XtkLdap_Active</span><br /> </td> 
   <td> LDAP サーバーをユーザーの認証とユーザーへの権限の付与に使用できるようにする.<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">XtkLdap_AppLogin</span><br /> </td> 
   <td> 様々な検索を目的としてサーバーに接続するためのアプリケーションログイン.<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">XtkLdap_AppPassword</span><br /> </td> 
   <td> アプリケーションログイン用の暗号化されたパスワード.<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">XtkLdap_AutoOperator</span><br /> </td> 
   <td> Adobe Campaign でオペレーターと権限の自動作成を有効にする.<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">XtkLdap_DN</span><br /> </td> 
   <td> ログインに基づく LDAP DN の計算式.<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">XtkLdap_DNSearch</span><br /> </td> 
   <td> ディレクトリの DN 検索を有効にする.<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">XtkLdap_DNSearchBase</span><br /> </td> 
   <td> 検索ベース.<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">XtkLdap_DNSearchFilter</span><br /> </td> 
   <td> DN 検索フィルター.<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">XtkLdap_DNSearchScope</span><br /> </td> 
   <td> 検索範囲.<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">XtkLdap_Mechanism</span><br /> </td> 
   <td> LDAP サーバーへの接続に使用される認証タイプ (plain、md5、lds、ntlm、dpa).<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">XtkLdap_Rights</span><br /> </td> 
   <td> LDAP ディレクトリから Adobe Campaign のネームド権限への認証およびグループの同期を有効にします.<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">XtkLdap_RightsAttr</span><br /> </td> 
   <td> 認証名を含む LDAP 属性.<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">XtkLdap_RightsBase</span><br /> </td> 
   <td> 検索ベース.<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">XtkLdap_RightsFilter</span><br /> </td> 
   <td> ユーザー認証用の検索フィルター.<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">XtkLdap_RightsMask</span><br /> </td> 
   <td> LDAP 認証から Adobe Campaign 権限の名前を抽出するための式です.<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">XtkLdap_RightsScope</span><br /> </td> 
   <td> 検索範囲.<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">XtkLdap_Server</span><br /> </td> 
   <td> LDAP サーバーのアドレス (「:」を区切り記号として指定してポートを指定することができます).<br /> </td> 
  </tr> 
 </tbody> 
</table>

## Web フォーム {#web-forms}

<table> 
 <thead> 
  <tr> 
   <th> オプション名 </th> 
   <th> 説明 </th> 
  </tr> 
 </thead> 
 <tbody> 
  <tr> 
   <td> <span class="uicontrol">XtkUseScrollBar</span><br /> </td> 
   <td> 値を1に設定すると、詳細フォームにスクロールバーを追加できます。<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">XtkWebForm_Instance</span><br /> </td> 
   <td> 「その他のサーバー」モードで Web フォームの無効化用に使用されるインスタンス<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">XtkWebForm_Password</span><br /> </td> 
   <td> 「その他のサーバー」モードで Web フォームの無効化に使用するインスタンスのパスワード。<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">XtkWebForm_ServersMode</span><br /> </td> 
   <td> Web フォームの無効化モードを指定できるオプション : デフォルトではローカルです。「トラッキング」オプションの場合はトラッキングサーバーを使用し、「その他のサーバー」オプションの場合はパーソナライズされたリストを使用します。<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">XtkWebForm_ServersURLs</span><br /> </td> 
   <td> Web フォームの無効化のために連絡されるサーバーのパーソナライズ済みアドレスリスト (「その他のサーバー」モード)。<br /> </td> 
  </tr> 
 </tbody> 
</table>

