---
title: キャンペーンオプションの設定
seo-title: キャンペーンオプションの設定
description: キャンペーンオプションの設定
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
source-git-commit: de1173786c94c2a526153e7e6948f71c9523fa7b
workflow-type: tm+mt
source-wordcount: '3906'
ht-degree: 25%

---


# Campaign Classic のオプションのリスト{#configuring-campaign-options}

「 **[!UICONTROL 管理/プラットフォーム/オプション]** 」ノードを使用すると、Adobe Campaignオプションを設定できます。

>[!NOTE]
>
>Adobe Campaignオプションの変更または更新は、エキスパートユーザーのみが実行できます。

一部はキャンペーンのインストール時に組み込まれており、必要に応じて手動で追加することもできます。 使用できるオプションは、インスタンスと共にインストールされるパッケージによって異なります。

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
   <td> <span class="uicontrol">Deliverability_LastBroadLogMsgDate</span> <br /> </td> 
   <td> 配信品質インスタンスから最後に取得されたbroadLogMsgの日付。<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">Deliverability_LastBroadLogMsgSent</span> <br /> </td> 
   <td> 配信品質インスタンスに送信された最後のbroadLogMsgの日付。<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">DmRendering_cuid</span> <br /> </td> 
   <td> 配信レポート識別子。IDを取得するには、サポートに問い合わせてください。<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">DmRendering_SeedTargets</span> <br /> </td> 
   <td> 受信ボックスレンダリングのテストアドレスを使用するスキーマのリスト。
(要素名はコンマ区切りで指定)
例 : custom_nms_recipient.<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">NMS_ActivateOwnerConfirmation</span> <br /> </td> 
   <td><p> 特定の演算子またはオペレーターのグループが配信のプロパティで配信を開始するように指定されている場合に、配信の担当者が送信を確認できるようにします。</p><p> これを行うには、値として「1」を入力して、オプションをアクティブにします。 このオプションを非アクティブにするには、"0"と入力します。</p><p> すると、送信確認プロセスがデフォルトとして機能します。つまり、配信プロパティで送信用に指定されたオペレーターまたはオペレーターのグループ（または管理者）のみが、送信を確認し、実行できるようになります。<a href="../../campaign/using/marketing-campaign-deliveries.md#starting-an-online-delivery">この節</a>を参照してください。</p> </td> 
   <tr> 
   <td> <span class="uicontrol">Nms_DefaultRcpSchema</span> <br /> </td> 
   <td> Adobe Campaignは、「Nms_DefaultRcpSchema」グローバル変数を使用して、デフォルトの受信者受信者(nms:database)との対話を行います。<br /> option値は、外部受信者テーブルと一致するスキーマの名前に対応する必要があります。<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">NmsBilling_MainActionThreshold</span> <br /> </td> 
   <td> 配信を請求レポートのメインの配信と見なすための最小受信者数。<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">NmsBroadcast_DefaultProvider</span> <br /> </td> 
   <td> 新しいテンプレート用のデフォルトのルーティングサービスプロバイダー.<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">NmsBroadcast_LogsPerTransac</span> <br /> </td> 
   <td> 一度に配信用に作成されたBroadLogの数。<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">NmsBroadcast_MaxDelayPerTransac</span> <br /> </td> 
   <td> トランザクションごとのログ(broadLogs)の挿入（テーブルに挿入）: バッチあたりに処理する行数。<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">NmsBroadcast_MidAnalyzeBatchSize</span> <br /> </td> 
   <td> ミッドソーシング配信を分析する際の配信分割のグループ化サイズ.<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">NmsBroadcast_MsgValidityDuration</span> <br /> </td> 
   <td> デフォルトの配信期間 (秒).<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">NmsBroadcast_RegexRules</span> <br /> </td> 
   <td> 配信メッセージを正規化するための正規表現.<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">NmsBroadcast_RemoveBlackList</span> <br /> </td> 
   <td> 値に「1」を入力すると、連絡を希望しない受信者を除外できます。<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">NmsBroadcast_RemoveDuplicatesRecipients</span> <br /> </td> 
   <td> 値に「1」を入力すると、重複が自動的に無視されます。<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">NmsDelivery_ErrorAddressMasks</span> <br /> </td> 
   <td> メッセージの返信時に使用するエラーアドレスの構文を定義できます。<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">NmsDelivery_FromAddressMasks</span> <br /> </td> 
   <td> メッセージの送信時に使用するFromアドレスの構文を定義できます。<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">NmsDelivery_ImageServerTimeout</span> <br /> </td> 
   <td> パーソナライズされたURLからダウンロードし、電子メールに添付した画像を取得する場合に、サーバーから応答を取得するためのタイムアウト制限（秒）を定義できます。 この値を超えると、メッセージを送信できません。 デフォルト値は 60 秒です。<br /> </td> 
  </tr> 
 <tr> 
   <td> <span class="uicontrol">NmsDelivery_MaxDownloadedImageSize</span> <br /> </td> 
   <td> パーソナライズされたURLからダウンロードし、電子メールに添付した画像に許可される最大サイズ（バイト）を定義できます。 デフォルト値は100,000バイトです。 配達確認を送信し、電子メールを処理するために画像をダウンロードする場合、画像のサイズがこの値を超えた場合、またはダウンロードの問題がある場合、配信ログにエラーが表示され、配達確認配信は失敗します。<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">NmsDelivery_MaxRecommendedAttachments</span> <br /> </td> 
   <td> 電子メールまたはトランザクション電子メールテンプレートに添付ファイルの最大数を設定できます。 この値を超えると、配信分析ログまたはトランザクション電子メールテンプレートの公開時に、警告が表示されます。 The default value is 1 attachment.<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">NmsDelivery_MaxRetry</span> <br /> </td> 
   <td> 分析中の再試行の最大数.<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">NmsDelivery_PublishingScript</span> <br /> </td> 
   <td> パブリッシュスクリプト.<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">NmsDelivery_NoCountBroadLogMsgPush</span> <br /> </td> 
   <td> プッシュメッセージの broadLogMsg カウントを無効にします.<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">NmsDeliveryWizard_ShowDeliveryWeight</span> <br /> </td> 
   <td> メッセージの重み付けを配信ウィザードに表示します.<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">NmsEmail_DefaultErrorAddr</span> <br /> </td> 
   <td> ユーザーが空のままにした場合、電子メールの配信に使用するインスタンスのレベルでデフォルトの「error」電子メールアドレス。<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">NmsEmail_DefaultFromAddr</span> <br /> </td> 
   <td> ユーザーが空のままにした場合、インスタンスのレベルで電子メール配信に使用されるデフォルトの'from'電子メールアドレス。<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">NmsEmail_DefaultReplyToAddr</span> <br /> </td> 
   <td> ユーザーが空のままにした場合、電子メールの配信に使用するインスタンスのレベルでデフォルトの「返信」電子メールアドレス。<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">NmsEmail_ExpOrganization</span> <br /> </td> 
   <td> 顧客の共通名. 受信者に表示される一部の警告メッセージで使用されます。<br /> 「*****または関連会社と連絡を取っているので、このメッセージが表示されます。 *****"からのメッセージを受信しなくなります。<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">NmsEmail_FromName</span> <br /> </td> 
   <td> ユーザーが空のままにした場合、インスタンスのレベルで電子メールの配信に使用されるデフォルトの「送信者」電子メールラベル。<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">NmsEmail_ReplyToName</span> <br /> </td> 
   <td> ユーザーが空のままにした場合、インスタンスのレベルで電子メールの配信に使用されるデフォルトの「返信」電子メールラベル。<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">NmsEmail_RetryCount</span> <br /> </td> 
   <td> 電子メールメッセージの2再試行間の期間（秒）。<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">NmsEmail_RetryPeriod</span> <br /> </td> 
   <td> 電子メールメッセージの再試行期間。<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">NmsForecast_MsgWeightFormula</span> <br /> </td> 
   <td> 暫定的な配信メッセージの重み付けを計算するときに使用する数式.<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">NmsInmail_WhitelistEmails</span> <br /> </td> 
   <td> List of authorized forwarding email addresses (from the inbound mail processing module). The addresses have to be separated by commas (or * to allow all). E.g. xyz@abc.com,pqr@abc.com.<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">NmsLine_AESKey</span> <br /> </td> 
   <td> URL をエンコードするために「lineImage」サーブレットで使用される AES キー (LINE チャネル).<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">NmsNPAI_EmailMaxError</span> <br /> </td> 
   <td> チャネル「email」（デフォルトとして使用）: 受信者を強制隔離にする前に、送信中にSOFTエラーが発生した場合に受け入れられるエラーの最大数です。<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">NmsNPAI_EmailSignificantErrorDelay</span> <br /> </td> 
   <td> チャネル「email」（デフォルトとして使用）: 新しいSOFTエラーを考慮する前に、前回参照したSOFTエラー以降に費やした最小期間。<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">NmsNPAI_MobileMaxError</span> <br /> </td> 
   <td> チャネル「mobile」の場合： 受信者を強制隔離にする前に、送信中にSOFTエラーが発生した場合に受け入れられるエラーの最大数です。<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">NmsNPAI_MobileSignificantErrorDelay</span> <br /> </td> 
   <td> チャネル「mobile」の場合： 新しいSOFTエラーを考慮する前に、前回参照したSOFTエラー以降に費やした最小期間。<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">NmsMidSourcing_LogsPeriodHour</span> <br /> </td>
   <td> 同期ワークフローが実行されるたびに回復されるブロードログの数を制限するために、最大期間（時間単位）を指定できます。</a>.<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">NmsMidSourcing_PrepareFlow</span> <br /> </td> 
   <td> MidSourcingセッションで並行して実行できる最大呼び出し数（デフォルトでは3）。<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">NmsMTA_Alert_Delay</span> <br /> </td> 
   <td> カスタムの遅延（分単位）。その後の配信は「遅延」と見なされます。デフォルトは30分です。<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">NmsOperation_DeliveryPreparationWindow</span> <br /> </td> 
   <td><p>このオプションは、実行中の配信の数をカウントする際に、 <span class="uicontrol"><a href="../../workflow/using/campaign.md">operationMgt</a></span> テクニカルワークフローで使用されます。</p>これにより、非整合なステータスの配信が実行中の配信の数から除外される日数を定義できます。</p><p>デフォルトでは、この値は「7」に設定されているので、7日より古い配信との矛盾は除外されます。</p></td> 
  </tr>
  <tr> 
   <td> <span class="uicontrol">NmsPaper_SenderLine1</span> <br /> </td> 
   <td> 送信者のアドレスの1行目。<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">NmsPaper_SenderLine3</span> <br /> </td> 
   <td> 送信者のアドレスの3行目。<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">NmsPaper_SenderLine4</span> <br /> </td> 
   <td> 送信者のアドレスの4行目。<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">NmsPaper_SenderLine6</span> <br /> </td> 
   <td> 送信者のアドレスの6行目。<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">NmsPaper_SenderLine7</span> <br /> </td> 
   <td> 送信者のアドレスの7行目。<br /> </td> 
  </tr>
  <tr> 
   <td> <span class="uicontrol">NmsServer_MirrorPageUrl</span> <br /> </td> 
   <td> URL of the mirror page server (by default, should be identical to NmsTracking_ServerUrl).<br /> It is the default value of email deliveries when the URL is not specified in the routing definition.<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">NmsSMS_Priority</span> <br /> </td> 
   <td> 送信されたSMSメッセージのパラメータ： メッセージの優先度を示すためにSMSゲートウェイに送信される情報。<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">NmsSMS_RetryCount</span> <br /> </td> 
   <td> SMSメッセージを送信する際の再試行数。<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">NmsSMS_RetryPeriod</span> <br /> </td> 
   <td> SMSメッセージの再試行を実行する期間。<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">NmsUserAgentStats_LastConsolidation</span> <br /> </td> 
   <td> NmsUserAgent <span class="uicontrol">統計の最終連結日</span> 。<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">NmsWebSegments_LastStates</span> <br /> </td> 
   <td> Webセグメントとその状態を含むオプションの名前。<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">XtkBarcode_SpecialChar</span> <br /> </td> 
   <td> Enable/disable support for special characters for Code128.<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">XtkEmail_Characters</span> <br /> </td> 
   <td> E メールアドレスで有効な文字.<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">XtkSecurity_Restrict_EditXML</span> </td> 
   <td> この追加オプションに「0」値を付けて、配信のXMLコードのエディションを無効にします(右クリック/XMLソースを <span class="uicontrol">編集</span> 、または <span class="uicontrol">Ctrl + F4</span> ショートカット)。<br /> </td> 
  </tr>  
 </tbody> 
</table>

<!--<tr> 
   <td> <span class="uicontrol">EMTA_BCC_ADDRESS</span> </td> 
   <td> BCC email address for Momentum to send a raw copy of the sent emails. <br /> </td> 
  </tr>
-->

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
   <td> <span class="uicontrol">NcmResourcesDir</span> <br /> </td> 
   <td> Adobe Campaignクライアントコンソールでのパブリケーションに関するリソースの場所。 <a href="../../delivery/using/formatting.md#image-referencing">この節</a>を参照してください。<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">NcmResourcesDirPreview</span> <br /> </td> 
   <td> Adobe Campaignクライアントコンソールでプレビューするリソースの場所。 <a href="../../delivery/using/formatting.md#image-referencing">この節</a>を参照してください。<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">NmsDelivery_DefaultIgnoredImage</span> <br /> </td> 
   <td> アップロード時にスキップする画像の URL マスクのリスト.<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">NmsDelivery_ImagePublishing</span> </td> 
   <td> 画像のアップロードの設定. 値はnone / tracking / script /リストにすることができます（演算子のオプション設定で上書きできます）。 </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">NmsDelivery_ImageSubDirectory</span> <br /> </td> 
   <td> サーバー上の画像を保存するフォルダー.<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">NmsServer_LogoPath</span> <br /> </td> 
   <td> ロゴを表示するスペース.<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">NcmPublishingDir</span> <br /> </td> 
   <td> パブリッシュ用ルートフォルダー.<br /> HTMLおよびテキストコンテンツの生成について詳しくは、 <a href="../../delivery/using/using-a-content-template.md">この節を参照してください</a>。<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">XtkImageUrl</span> <br /> </td> 
   <td> 配信で使用される画像を保存するサーバを定義して、ブラウザがそれらを取得できるようにします。<br /> ビルドバージョン&lt;= 5098の場合、インスタンスにアップロードされた画像のURLを使用します。<br /> ビルドバージョン5098より大きい場合は、配信のパブリックURLまたは <span class="uicontrol">XtkFileRes_Public_URL</span> オプションのURLを使用します。<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">NmsDelivery_MediaInstance</span> <br /> </td> 
   <td> 画像をアップロードするためのインスタンス名を設定できます。<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">NmsDelivery_MediaPassword</span> <br /> </td> 
   <td> 画像のアップロード用のパスワードを設定できます。<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">NmsDelivery_MediaServers</span> <br /> </td> 
   <td> 画像のアップロード用にメディアのURLを設定できます。<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">NmsBroadcast_MsgWebValidityDuration</span> <br /> </td> 
   <td> 配信のオンラインリソースのデフォルトの有効持続期間 (秒).<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">XtkFileRes_Public_URL</span> <br /> </td> 
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
   <td> <span class="uicontrol">CrmMarketingActivityWindow</span> <br /> </td> 
   <td> この月数で表示するマーケティング履歴。<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">NmsOperation_Duration</span> <br /> </td> 
   <td> キャンペーンのデフォルトの有効期間 (秒).<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">NmsOperation_LimitConcurrency</span> <br /> </td> 
   <td> operationMgtワークフローによって開始され、一度に処理できる配信/ワークフロー/仮説/シミュレーションジョブの最大数です。<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">NmsOperation_OperationMgtDebug</span> <br /> </td> 
   <td> operationMgt <a href="../../workflow/using/campaign.md"></a> 技術的なワークフローの実行を監視できます。 アクティブ化されると（値「1」）、実行情報はワークフロー監査ログに記録されます。<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">NmsOperation_TimeRange</span> <br /> </td> 
   <td> スケジュールモードのターゲティング期間と抽出条件。<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">Workflow_AnalysisThreshold</span> <br /> </td> 
   <td> テーブルの統計の自動再計算により影響を受けるレコードの数。<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">XtkReport_Logo</span> <br /> </td> 
   <td> エクスポートされたレポートの右上隅に表示するロゴ.<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">NmsServer_PausedWorkflowPeriod</span> <br /> </td> 
   <td> Number of days to wait between checks for paused workflows.<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">NmsCampaign_Activate_OwnerConfirmation</span> <br /> </td> 
   <td> 操作の所有者による配信検証をアクティブ化します。値として「1」を入力します。 このオプションを非アクティブにするには、"0"と入力します。<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">NmsAsset_JavascriptExt</span> <br /> </td> 
   <td> ワークフローのアクティビティ「マーケティングリソース通知」に読み込む追加のJSライブラリ。<br /> </td> 
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
   <td> <span class="uicontrol">XtkAcceptOldPasswords</span> <br /> </td> 
   <td> (互換モードのインストール： build&gt;6000)アクティブ化された場合（値"1"）、このオプションを使用すると、データベースに格納されている古いパスワードを、外部アカウントまたはインスタンスへの接続に使用できます。<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">XtkKey</span> <br /> </td> 
   <td> This key is used to encrypt most passwords in the database. (external accounts, LDAP password...).<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">XtkSecurity_Allow_PrivilegeEscalation</span> <br /> </td> 
   <td> 1を選択した場合、このオプションはjavascriptでprivilegeEscalationを許可します。<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">XtkSecurity_Disable_ControlsOnFileDownload</span> <br /> </td> 
   <td> 1を選択すると、ファイルのダウンロード中（fileDownload.jsp経由）にACLコントロールが無効になります。<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">XtkSecurity_Disable_JSFileSandboxing</span> <br /> </td> 
   <td> 1を選択すると、JavaScript内のファイルサンドボックスが無効になります。<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">XtkSecurity_SaveOptions_AllowNonAdmin</span> <br /> </td> 
   <td> 'true'に設定した場合、管理者以外の演算子が展開ウィザードを使用してxtkOption値を更新することを許可します。<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">XtkSecurity_Unsafe_DecryptString</span> <br /> </td> 
   <td> 1を選択した場合、このオプションではdecryptStringを使用して一部のパスワードを復号化できます。<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">XtkTraceDeleteLogin</span> <br /> </td> 
   <td> 「1」の値を入力して、レコードを削除する前にmDataの「変更者」フィールドを変更して、監査証跡情報を持つ要素の削除を追跡します。<br /> </td> 
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
   <td> <span class="uicontrol">MC_EnlictionCustomJs</span> <br /> </td> 
   <td> イベントを豊かにするためにパーソナライズするJavaScriptライブラリ。 次の2つの関数の実装が含まれている必要があります。<br /> 
    <ul> 
     <li> <p> <span class="uicontrol">enrichRtEvents(aiEventId);</span> : データベース内のイベントを富化し、保存します( <span class="uicontrol">aiEventId</span> は、処理されたリアルタイムイベントの表に対応します)。</p> </li> 
     <li> <p> <span class="uicontrol">enrichBatchEvents(aiEventId);</span> : データベース内のイベントを富化し、保存します( <span class="uicontrol">aiEventId</span> は、処理されたバッチイベントのIDテーブルに対応します)。</p> </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">MC_LastUpdateFromBL</span> <br /> </td> 
   <td> 配信ログ経由での前回のイベントステータス更新の日付。<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">MC_RoutingCustomJs</span> <br /> </td> 
   <td> ルーティングイベントに合わせてパーソナライズするJavaScriptライブラリ。 次の2つの関数の実装が含まれている必要があります。<br /> 
    <ul> 
     <li> <p> <span class="uicontrol">dispatchRtEvent(iEventId);</span> : リアルタイムイベントを処理するために選択されたトランザクションメッセージの内部名を返します( <span class="uicontrol">iEventId</span> は、処理されたリアルタイムイベントのIDに対応します)。</p> </li> 
     <li> <p> <span class="uicontrol">dispatchBatchEvent(iEventId);</span> : バッチイベントを処理するために選択されたトランザクションメッセージの内部名を返します( <span class="uicontrol">iEventId</span> は、処理されたバッチイベントのIDに対応します)。</p> </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">MC_RtEventAvgDeliveryTimeAlert</span> <br /> </td> 
   <td> リアルタイムイベントの平均送信時間のアラートしきい値.<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">MC_RtEventAvgDeliveryTimeWarning</span> <br /> </td> 
   <td> リアルタイムイベントの平均送信時間の警告しきい値。<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">MC_RtEventAvgProcessTimeAlert</span> <br /> </td> 
   <td> リアルタイムイベントの平均処理時間のアラートしきい値。<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">MC_RtEventAvgProcessTimeWarning</span> <br /> </td> 
   <td> リアルタイムイベントの平均処理時間の警告しきい値。<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">MC_RtEventAvgQueueAlert</span> <br /> </td> 
   <td> 待機中リアルタイムイベントの平均数のアラートしきい値。<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">MC_RtEventAvgQueueTimeAlert</span> <br /> </td> 
   <td> リアルタイムイベントの平均キュー時間のアラートしきい値。<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">MC_RtEventAvgQueueTimeWarning</span> <br /> </td> 
   <td> リアルタイムイベントの平均キュー時間の警告しきい値。<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">MC_RtEventAvgQueueWarning</span> <br /> </td> 
   <td> 待機中リアルタイムイベントの平均数の警告しきい値。<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">MC_RtEventErrorAlert</span> <br /> </td> 
   <td> リアルタイムイベントの処理エラーのアラートしきい値。<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">MC_RtEventErrorWarning</span> <br /> </td> 
   <td> リアルタイムイベントの処理エラーの警告しきい値。<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">MC_RtEventMaxQueueAlert</span> <br /> </td> 
   <td> 待機中リアルタイムイベントの最大数のアラートしきい値。<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">MC_RtEventMaxQueueWarning</span> <br /> </td> 
   <td> 待機中リアルタイムイベントの最大数の警告しきい値。<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">MC_RtEventMinQueueAlert</span> <br /> </td> 
   <td> 待機中リアルタイムイベントの最小数のアラートしきい値。<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">MC_RtEventMinQueueWarning</span> <br /> </td> 
   <td> 待機中リアルタイムイベントの最低数の警告しきい値。<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">MC_RtEventQueueAlert</span> <br /> </td> 
   <td> 保留中リアルタイムイベントのキューのアラートしきい値。<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">MC_RtEventQueueWarning</span> <br /> </td> 
   <td> 保留中リアルタイムイベントのキューの警告しきい値。<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">MC_RtEventThroughputAlert</span> <br /> </td> 
   <td> リアルタイムイベントのスループットのアラートしきい値。<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">MC_RtEventThroughputWarning</span> <br /> </td> 
   <td> リアルタイムイベントのスループットの警告しきい値。<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">NmsMessageCenter_RoutingBatchSize</span> <br /> </td> 
   <td> イベントのルーティングに使用する再グループ化のサイズ<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">MC_LastRtEventStat</span> <br /> </td> 
   <td> RtEventステータスの更新ポインタ（データが取得される最終日までの日付）。<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">NmsLine_MessageCenterURL</span> <br /> </td> 
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
   <td> <span class="uicontrol">NmsCleanup_LastCleanup</span> <br /> </td> 
   <td> クリーンアップ処理が最後に実行された時刻を定義します。<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">NmsCleanup_BroadLogPurgeDelay</span> <br /> </td> 
   <td> <p>ブロードローグをデータベースから消去するまでの遅延を定義できます。</p><p>このオプションは、インターフェイス内で遅延が変更されると自動的に作成されます。 optionsリストーの値を変更した場合は、秒単位で表します。</p><br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">NmsCleanup_EventHistoPurgeDelay</span> <br /> </td> 
   <td><p> イベント履歴をデータベースから消去するまでの遅延を定義できます。</p><p>
   このオプションは、インターフェイス内で遅延が変更されると自動的に作成されます。 optionsリストーの値を変更した場合は、秒単位で表します。</p><br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">NmsCleanup_EventPurgeDelay</span> <br /> </td> 
   <td><p> データベースからイベントを消去するまでの遅延を定義できます。</p><p>このオプションは、インターフェイス内で遅延が変更されると自動的に作成されます。 optionsリストーの値を変更した場合は、秒単位で表します。</p><br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">NmsCleanup_EventStatPurgeDelay</span> <br /> </td> 
   <td><p> データベースからイベント統計を消去するまでの遅延を定義できます。</p><p>このオプションは、インターフェイス内で遅延が変更されると自動的に作成されます。 optionsリストーの値を変更した場合は、秒単位で表します。</p><br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">NmsCleanup_PropositionPurgeDelay</span> <br /> </td> 
   <td><p> データベースから配置を削除するまでの遅延を定義できます。</p><p> このオプションは、インターフェイス内で遅延が変更されると自動的に作成されます。 optionsリストーの値を変更した場合は、秒単位で表します。</p><br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">NmsCleanup_QuarantineMailboxFull</span> <br /> </td> 
   <td> <p>データベースから強制隔離を消去するまでの遅延を定義できます。</p><p> このオプションは、インターフェイス内で遅延が変更されると自動的に作成されます。 optionsリストーの値を変更した場合は、秒単位で表します。</p><br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">NmsCleanup_RecycledDeliveryPurgeDelay</span> <br /> </td> 
   <td> <p>データベースからリサイクル配信を消去するまでの遅延を定義できます。</p><p> このオプションは、インターフェイス内で遅延が変更されると自動的に作成されます。 optionsリストーの値を変更した場合は、秒単位で表します。</p><br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">NmsCleanup_RejectsPurgeDelay</span> <br /> </td> 
   <td> <p>データベースから拒否を消去するまでの遅延を定義できます。</p><p>このオプションは、インターフェイス内で遅延が変更されると自動的に作成されます。 optionsリストーの値を変更した場合は、秒単位で表します。</p><br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">NmsCleanup_TrackingLogPurgeDelay</span> <br /> </td> 
   <td> <p>データベースからトラッキングログを消去するまでの遅延を定義できます。</p><p>このオプションは、インターフェイス内で遅延が変更されると自動的に作成されます。 optionsリストーの値を変更した場合は、秒単位で表します。</p><br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">NmsCleanup_TrackingStatPurgeDelay</span> <br /> </td> 
   <td><p> データベースから追跡統計情報を消去するまでの遅延を定義できます。</p><p> このオプションは、インターフェイス内で遅延が変更されると自動的に作成されます。 optionsリストーの値を変更した場合は、秒単位で表します。</p><br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">NmsCleanup_VisitorPurgeDelay</span> <br /> </td> 
   <td> <p>データベースから訪問者を消去するまでの遅延を定義できます。</p><p> このオプションは、インターフェイス内で遅延が変更されると自動的に作成されます。 optionsリストーの値を変更した場合は、秒単位で表します。</p><br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">NmsCleanup_WorkflowResultPurgeDelay</span> <br /> </td> 
   <td> <p>ワークフローの結果がデータベースから消去されるまでの遅延を定義できます。</p><p> このオプションは、インターフェイス内で遅延が変更されると自動的に作成されます。 optionsリストーの値を変更した場合は、秒単位で表します。</p><br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">WdbcCapabilities_AzureDw</span> <br /> </td> 
   <td> Azure SQL Datawarehouse コネクタオプション.<br /> </td> 
  </tr>
   <tr> 
   <td> <span class="uicontrol">WdbcKillSessionPolicy</span> <br /> </td> 
   <td>以下の潜在的な値に従って、すべてのワークフローとPostgreSQLデータベースクエリに対する無条件停止動作に影響を与えます。<ul>
    <li><p>0 — デフォルト： ワークフロープロセスを停止し、データベースに影響を与えない<p></li>
    <li><p>1 - pg_cancel_backend: ワークフロープロセスを停止し、データベース内のクエリをキャンセル<p></li>
    <li><p>2 - pg_terminate_backend: ワークフロープロセスを停止し、データベース内のクエリを終了します<p></li></ul></td> 
  </tr>  
  <tr> 
   <td> <span class="uicontrol">WdbcOptions_TableSpaceIndex</span> <br /> </td> 
   <td> Adobe Campaign の標準テーブルのインデックスを格納するためのテーブル領域の名前.<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">WdbcOptions_TableSpaceUser</span> <br /> </td> 
   <td> Adobe Campaign の標準テーブルのデータを格納するためのテーブル領域の名前.<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">WdbcOptions_TableSpaceWork</span> <br /> </td> 
   <td> Adobe Campaign 作業用テーブルのデータを格納するテーブル領域の名前.<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">WdbcOptions_TableSpaceWorkIndex</span> <br /> </td> 
   <td> Adobe Campaign 作業用テーブルのインデックスを含むテーブル領域の名前.<br /> </td> 
  </tr> 
    <tr> 
   <td> <span class="uicontrol">WdbcOptions_TempDbName</span> <br /> </td> 
   <td> バックアップとレプリケーションを最適化するために、Microsoft SQL Serverで作業テーブル用に別々のデータベースを構成できます。 このオプションは、一時データベースの名前に対応します。 指定した場合、このデータベースに作業テーブルが書き込まれます。 例： 「tempdb.dbo」 （名前はドットで終わる必要があります）。</desc> <a href="../../production/using/rdbms-specific-recommendations.md#microsoft-sql-server">詳細を表示</a> <br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">WdbcTimeZone</span> <br /> </td> 
   <td> Adobe Campaignインスタンスのタイムゾーン。 「 <a href="../../installation/using/time-zone-management.md#configuration" target="_blank">設定</a>」を参照してください。<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">WdbcUseNChar</span> <br /> </td> 
   <td> データベースの文字列フィールドはNCharで定義されていますか？<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">WdbcUseTimeStampWithTZ</span> <br /> </td> 
   <td> データベースの'datetime'フィールドにタイムゾーン情報が格納されますか。<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">XtkDatabaseId</span> <br /> </td> 
   <td> データベースのID。 Unicode DataBaseの場合は'u'で始まります。<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">XtkInstancePrefix</span> <br /> </td> 
   <td> 自動生成された内部名に追加されるプレフィックス.<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">XtkQuery_スキーマ_LineCount</span> <br /> </td> 
   <td> 結果の最大数は、xtk:schema および xtk:srcSchema のクエリによって返されます。<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">XtkSequence_AutoGeneration</span> <br /> </td> 
   <td> この時点以降に作成されるカスタマイズされたスキーマは、autopk="true"で属性"pkSequence"を含まない場合、自動生成されたシーケンス"auto_ &lt;schemanamespace&gt; &lt;schemaname&gt; _seq. 
   </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">NlMigration_KeepFolderStructure</span> <br /> </td> 
   <td> 移行中、ツリー構造は、新しいバージョン標準に基づいて自動的に再編成されます。<br /> このオプションを使用すると、ナビゲーションツリーの自動移行を無効にできます。 使用する場合は、移行後に古いフォルダーを削除する必要があります。新しいフォルダーを追加し、必要なチェックをすべて実行します。<br /> 
    <ul> 
     <li> <p> <span class="uicontrol">データタイプ：</span> 整数</p> </li> 
     <li> <p> <span class="uicontrol">値（テキスト）</span> : 1 </p> </li> 
    </ul> このオプションは、標準搭載のナビゲーションツリーに加えられた変更が多すぎる場合にのみ使用してください。<br /> 詳しくは、 <a href="../../migration/using/specific-configurations-in-v5-11.md#campaign-vseven-tree-structure">この節を参照してください</a>。<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">NmsLastErrorStatCoalesce</span> <br /> </td> 
   <td> NmsEmailErrorStatテーブルのクリー <span class="uicontrol">ンアップの最終処理日</span> 。<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">PostUpgradeLastError</span> <br /> </td> 
   <td> 次の構文に従い、Postupgradeで発生したエラーに関する情報です。<br /> <strong>{ビルド番号}:{モード： pre/post/...}:{エラーが発生した'lessThan'/'greaterOrEquelThan'、エラー+サブステップ}</strong> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">XtkCleanup_NoStats</span> <br /> </td> 
   <td> 「1」の値を入力して、クリーンアップワークフローを通じて統計の更新が行われないようにします。<br /> </td> 
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
   <td> <span class="uicontrol">AEMResourceTypeFilter</span> <br /> </td> 
   <td> Adobe Campaignで使用できるAEMリソースのタイプ。 値はコンマで区切る必要があります。<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">nmsPipeline_config</span> <br /> </td> 
   <td> Experience Cloud Triggersを設定できます。 データタイプは「long text」で、JSON形式である必要があります。 詳しくは、Experience Cloud TriggersをAdobe Campaign <a class="anchorLink" href="https://helpx.adobe.com/campaign/kb/triggers-and-campaign.html#PipelineoptionNmsPipelineConfig" target="_blank">クラシックと共に使用する方法を参照してください</a>。<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">LASTIMPORT_&lt;%=instance.internalName%&gt;_&lt;%=activityName%&gt;</span> <br /> </td> 
   <td> このオプションは、CRMコネクタを介してサードパーティ製システムからデータを読み込む場合に使用します。 このオプションを有効にすると、前回の読み込み以降に変更されたオブジェクトのみを収集できます。 このオプションは、次のように手動で作成し、設定する必要があります。 
    <ul> 
     <li> <p> <span class="uicontrol">内部名</span> : LASTIMPORT_&lt;%=instance.internalName%&gt;_&lt;%=activityName%&gt;</p> </li> 
     <li> <p> <span class="uicontrol">値（フィールド）</span> : 最後にインポートした日付。形式yyyy/MM/dd hh:mm:ss。 </p> </li> 
    </ul><br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">TNT_EdgeServer</span> <br /> </td> 
   <td> 統合に使用される Adobe Target サーバー。このオプションは、デフォルトで選択されています。この値は Adobe Target のドメインサーバーに対応し、値 /m2 が続きます。例：tt.omtrdc.net/m2。<br /> こ <a href="../../integrations/using/configuring-the-integration-with-adobe-target.md">の節を参照してください</a>。<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">TNT_TenantName</span> <br /> </td> 
   <td> Adobe Target 組織名。この値は Adobe Target のクライアント名に対応します。<br /> こ <a href="../../integrations/using/configuring-the-integration-with-adobe-target.md">の節を参照してください</a>。<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">AAM_DataSourceId</span> <br /> </td> 
   <td> Adobeオーディエンスマネージャーとの統合に使用するオプション。<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">AAM_DestinationId</span> <br /> </td> 
   <td> Adobeオーディエンスマネージャーとの統合に使用するオプション。<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">WdbcCapabilities_Teradata</span> <br /> </td> 
   <td> Teradata コネクタオプション.<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">WdbcCapabilities_Hive</span> <br /> </td> 
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
   <td> <span class="uicontrol">NmsCoupons_MaxPerTransac</span> <br /> </td> 
   <td> SQLトランザクションごとに更新されたクーポン数。<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">NmsInteraction_LastPropositionSynchControl_</span> <br /> </td> 
   <td> '+ [提案のスキーマ] + "_" + extAccountSource.@executionInstanceId + [提案のスキーマ] + "_" + vars.executionInstanceIdFilter<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">NmsInteraction_LastPropositionSynchExec_</span> <br /> </td> 
   <td> '+ [提案のスキーマ] + "_" + extAccountSource.@executionInstanceId + "_" + extAccountTarget。@executionInstanceId<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">NmsInteraction_SynchWorkflowIds</span> <br /> </td> 
   <td> 同期ワークフローのトラッキング。<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">NmsInteraction_UseDaemon</span> <br /> </td> 
   <td> Enable/disable asynchronous proposition writing ("0" to disable, "1" to enable).<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">NmsModule_CouponsEnabled</span> <br /> </td> 
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
   <td> <span class="uicontrol">NmsExecutionInstanceId</span> <br /> </td> 
   <td> 実行インスタンスの識別子.<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">NmsServer_CustomerId</span> <br /> </td> 
   <td> 請求レポートの送信時に使用する顧客識別子.<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">NmsServer_IntranetURL</span> <br /> </td> 
   <td> アプリケーションサーバーにアクセスするための内部ベース URL.<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">NmsServer_LastPostUpgrade</span> <br /> </td> 
   <td> 前回のアップグレード前のACインスタンスのビルド番号。<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">NmsServer_URL</span> <br /> </td> 
   <td> パブリック Web アプリケーションサーバーのベース URL.<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">XtkPassUnknownSQLFunctionsToRDBMS</span> <br /> </td> 
   <td> 移行後も、古い宣言されていないSQL関数を引き続き使用できます。 セキュリティ上のリスクが伴うので、このオプションの使用を強くお勧めしません。<br /> </td> 
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
   <td> <span class="uicontrol">NmsTracking_Available</span> <br /> </td> 
   <td> トラッキングをアクティブにするオプション。<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">NmsTracking_ClickFormula</span> <br /> </td> 
   <td> トラッキングする URL の計算スクリプト.<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">NmsTracking_ExtAccount</span> <br /> </td> 
   <td> トラッキングサーバーの外部アカウントを定義できます。<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">NmsTracking_Instance</span> <br /> </td> 
   <td> トラッキングサーバー上でインスタンス名を定義できます。<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">NmsTracking_LastConsolidation</span> <br /> </td> 
   <td> 前回、トラッキング情報が新しいデータと統合された時刻。<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">NmsTracking_OpenFormula</span> <br /> </td> 
   <td> URL 計算スクリプトを開く.<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">NmsTracking_Password</span> <br /> </td> 
   <td> トラッキングサーバーのパスワード<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">NmsTracking_Pointer</span> <br /> </td> 
   <td> ポインターは、IDと日付を通じて処理された最後のメッセージイベントを追跡します。<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">NmsTracking_SecureServerUrl</span> <br /> </td> 
   <td> フロントトラッキングサーバーのセキュア URL.<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">NmsTracking_ServerUrl</span> <br /> </td> 
   <td> フロントトラッキングサーバーの URL.<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">NmsTracking_ServerUrlList</span> <br /> </td> 
   <td> トラッキングサーバーに接続するために使用される URL のリスト.<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">NmsTracking_UserAgentRules</span> <br /> </td> 
   <td> ブラウザー識別ルールセット.<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">NmsTracking_WebFormula</span> <br /> </td> 
   <td> Web トラッキングタグの処理に使用するスクリプト.<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">NmsTracking_WebTrackingDelivery</span> <br /> </td> 
   <td> Web トラッキング管理向けの仮想配信の名前。<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">NmsTracking_WebTrackingMode</span> <br /> </td> 
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
   <td> <span class="uicontrol">Privacy_Request_ConfirmDeletePending</span> <br /> </td> 
   <td> オプション1を選択した場合は、2番目の手順で、インターフェイスで手動で削除を確認する必要があります。 そうしないと、データは確認なしで削除されます。<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">Privacy_Request_ConfirmDeletePendingDelay</span> <br /> </td> 
   <td> 削除の確認待ちのリクエストとリクエストのキャンセルの間の遅延。<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">Privacy_Request_MaxErrorAllowed</span> <br /> </td> 
   <td> プライバシーリクエストの処理中 / 削除中に許可されるエラーの最大数。<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">Privacy_Request_PurgeDelay</span> <br /> </td> 
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
   <td> <span class="uicontrol">XtkLdap_Active</span> <br /> </td> 
   <td> LDAP サーバーをユーザーの認証とユーザーへの権限の付与に使用できるようにする.<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">XtkLdap_AppLogin</span> <br /> </td> 
   <td> 様々な検索を目的としてサーバーに接続するためのアプリケーションログイン.<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">XtkLdap_AppPassword</span> <br /> </td> 
   <td> アプリケーションログイン用の暗号化されたパスワード.<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">XtkLdap_AutoOperator</span> <br /> </td> 
   <td> Adobe Campaign でオペレーターと権限の自動作成を有効にする.<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">XtkLdap_DN</span> <br /> </td> 
   <td> ログインに基づく LDAP DN の計算式.<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">XtkLdap_DNSearch</span> <br /> </td> 
   <td> ディレクトリの DN 検索を有効にする.<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">XtkLdap_DNSearchBase</span> <br /> </td> 
   <td> 検索ベース.<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">XtkLdap_DNSearchFilter</span> <br /> </td> 
   <td> DN 検索フィルター.<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">XtkLdap_DNSearchScope</span> <br /> </td> 
   <td> 検索範囲.<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">XtkLdap_Mechanism</span> <br /> </td> 
   <td> LDAP サーバーへの接続に使用される認証タイプ (plain、md5、lds、ntlm、dpa).<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">XtkLdap_Rights</span> <br /> </td> 
   <td> LDAP ディレクトリから Adobe Campaign のネームド権限への認証およびグループの同期を有効にします.<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">XtkLdap_RightsAttr</span> <br /> </td> 
   <td> 認証名を含む LDAP 属性.<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">XtkLdap_RightsBase</span> <br /> </td> 
   <td> 検索ベース.<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">XtkLdap_RightsFilter</span> <br /> </td> 
   <td> ユーザー認証用の検索フィルター.<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">XtkLdap_RightsMask</span> <br /> </td> 
   <td> LDAP 認証から Adobe Campaign 権限の名前を抽出するための式です.<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">XtkLdap_RightsScope</span> <br /> </td> 
   <td> 検索範囲.<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">XtkLdap_Server</span> <br /> </td> 
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
   <td> <span class="uicontrol">XtkUseScrollBar</span> <br /> </td> 
   <td> 値を1に設定すると、詳細フォームにスクロールバーを追加できます。<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">XtkWebForm_Instance</span> <br /> </td> 
   <td> 「その他のサーバー」モードで Web フォームの無効化用に使用されるインスタンス<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">XtkWebForm_Password</span> <br /> </td> 
   <td> 「その他のサーバー」モードで Web フォームの無効化に使用するインスタンスのパスワード。<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">XtkWebForm_ServersMode</span> <br /> </td> 
   <td> Web フォームの無効化モードを指定できるオプション : デフォルトではローカルです。「トラッキング」オプションの場合はトラッキングサーバーを使用し、「その他のサーバー」オプションの場合はパーソナライズされたリストを使用します。<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">XtkWebForm_ServersURLs</span> <br /> </td> 
   <td> Web フォームの無効化のために連絡されるサーバーのパーソナライズ済みアドレスリスト (「その他のサーバー」モード)。<br /> </td> 
  </tr> 
 </tbody> 
</table>

