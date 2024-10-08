---
product: campaign
title: Campaign オプションの設定
description: Campaign オプションの設定方法を学ぶ
feature: Installation, Application Settings
audience: installation
content-type: reference
topic-tags: appendices
exl-id: a979cd99-afa7-4ce6-ba0f-9495089cba08
source-git-commit: 0fba6a2ad4ffa864e2f726f241aa9d7cd39072a6
workflow-type: tm+mt
source-wordcount: '3834'
ht-degree: 1%

---

# Campaign Classicオプションのリスト{#configuring-campaign-options}

**[!UICONTROL 管理/プラットフォーム/オプション]** ノードでは、Adobe Campaign オプションを設定できます。 Campaign のインストール時に組み込まれるものもあれば、必要に応じて手動で追加できるものもあります。 使用できるオプションは、インスタンスと共にインストールされるパッケージによって異なります。


>[!CAUTION]
>
>* このページにリストされていないオプションは内部のみです **変更しないでください**。
>
>* Adobe Campaignのオプションの変更や更新は、エキスパートユーザーのみが実行できます。

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
   <td> 配信品質インスタンスから取得された最後の broadLogMsg の日付。<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">Deliverability_LastBroadLogMsgSent</span> <br /> </td> 
   <td> 配信品質インスタンスに最後に送信された broadLogMsg の日付。<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">DmRendering_cuid</span> <br /> </td> 
   <td> 配信レポートの識別子。 ID を取得するには、サポートにお問い合わせください。<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">DmRendering_SeedTargets</span> <br /> </td> 
   <td> 受信ボックスレンダリングにテストアドレスを使用するスキーマのリスト。 （要素名はコンマで区切ります）例：custom_nms_recipient.<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">EMTA_BCC_ADDRESS</span> </td> 
   <td> Enhanced MTA が送信済みメールの生のコピーを送信する BCC メールアドレス。<br /> </td> 
  </tr>
  <tr> 
   <td> <span class="uicontrol">NMS_ActivateOwnerConfirmation</span> <br /> </td> 
   <td><p> 配信のプロパティで配信の開始を特定のオペレーターまたはオペレーターグループに指定されている場合に、配信を担当するオペレーターが送信を確認できるようにします。</p><p> これを行うには、値として「1」と入力してオプションを有効にします。 このオプションを無効にするには、「0」と入力します。</p><p> 送信の確認プロセスがデフォルトとして機能します。配信プロパティで送信用に指定されたオペレーターまたはオペレーターのグループ（または管理者）のみが、送信を確認して実行できます。 詳しくは、<a href="../../campaign/using/marketing-campaign-deliveries.md#starting-an-online-delivery">この節</a>を参照してください。</p> </td> 
   <tr> 
   <td> <span class="uicontrol">Nms_DefaultRcpSchema</span> <br /> </td> 
   <td> Adobe Campaignは、「Nms_DefaultRcpSchema」グローバル変数を使用して、デフォルトの受信者データベース（nms:recipient）とのダイアログを行います。<br /> オプションの値は、外部受信者テーブルに一致するスキーマの名前に対応している必要があります。<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">NmsBilling_MainActionThreshold</span> <br /> </td> 
   <td> 配信を請求レポートでメインの配信と見なすための最小受信者数。<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">NmsBroadcast_DefaultProvider</span> <br /> </td> 
   <td> 新しいテンプレートの既定のルーティング サービス プロバイダー <br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">NmsBroadcast_LogsPerTransac</span> <br /> </td> 
   <td> 配信準備中の broadLogs 挿入の最小バッチサイズ （行数）。<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">NmsBroadcast_MaxDelayPerTransac</span> <br /> </td> 
   <td> 配信準備中に broadLogs 挿入のバッチサイズを 2 倍にするバッチ期間しきい値（ミリ秒単位）。<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">NmsBroadcast_MidAnalyzeBatchSize</span> <br /> </td> 
   <td> ミッドソーシング配信を分析する際の配信部分のグループ化サイズ。<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">NmsBroadcast_MsgValidityDuration</span> <br /> </td> 
   <td> 配信のデフォルトの配信期間（秒単位）。<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">NmsBroadcast_RegexRules</span> <br /> </td> 
   <td> 配信メッセージを標準化するための正規表現。<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">NmsBroadcast_RemoveBlackList</span> <br /> </td> 
   <td> 値として「1」を入力すると、連絡を希望しない受信者を除外できます。<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">NmsBroadcast_RemoveDuplicatesRecipients</span> <br /> </td> 
   <td> 値として「1」と入力すると、重複を自動的に無視できます。<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">NmsDelivery_ErrorAddressMasks</span> <br /> </td> 
   <td> メッセージへの返信時に使用するエラーアドレスの構文を定義できます。<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">NmsDelivery_FromAddressMasks</span> <br /> </td> 
   <td> メッセージの送信時に使用する送信元アドレスの構文を定義できます。<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">NmsDelivery_ImageServerTimeout</span> <br /> </td> 
   <td> パーソナライズされた URL からダウンロードしてメールに添付した画像を取得する際に、サーバーから応答を取得するためのタイムアウト制限（秒単位）を定義できます。 この値を超えると、メッセージを送信できなくなります。 デフォルト値は 60 秒です。<br /> </td> 
  </tr> 
 <tr> 
   <td> <span class="uicontrol">NmsDelivery_MaxDownloadedImageSize</span> <br /> </td> 
   <td> パーソナライズされた URL からダウンロードしてメールに添付する画像の最大サイズ（バイト単位）を定義できます。 デフォルト値は 100,000 バイト（100 KB）です。 配達確認を送信し、メールを処理するために画像をダウンロードする際に、画像のサイズがこの値を超えている場合や、ダウンロードに関する問題がある場合は、配信ログにエラーが表示され、配達確認の配信が失敗します。<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">NmsDelivery_MaxRecommendedAttachments</span> <br /> </td> 
   <td> メールまたはトランザクションメールテンプレートの最大添付ファイル数を設定できます。 この値を超えると、配信分析ログまたはトランザクションメールテンプレートの公開時に警告が表示されます。 デフォルト値は「1 attachment」です。<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">NmsDelivery_MaxRetry</span> <br /> </td> 
   <td> 分析中の再試行の最大数。<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">NmsDelivery_PublishingScript</span> <br /> </td> 
   <td> 公開スクリプト。<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">NmsDelivery_NoCountBroadLogMsgPush</span> <br /> </td> 
   <td> プッシュメッセージの broadLogMsg 数を無効にします。<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">NmsDeliveryWizard_ShowDeliveryWeight</span> <br /> </td> 
   <td> 配信アシスタントにメッセージの重み付けを表示します。<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">NmsEmail_DefaultErrorAddr</span> <br /> </td> 
   <td> ユーザーが空のままにした場合のメール配信に使用される、インスタンスレベルのデフォルトの「エラー」メールアドレス。<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">NmsEmail_DefaultFromAddr</span> <br /> </td> 
   <td> ユーザーが空のままにした場合のメール配信に使用される、インスタンスレベルでのデフォルトの「送信元」メールアドレス <br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">NmsEmail_DefaultReplyToAddr</span> <br /> </td> 
   <td> ユーザーが空のままにした場合のメール配信に使用される、インスタンスレベルのデフォルトの「返信先」メールアドレス。<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">NmsEmail_ExpOrganization</span> <br /> </td> 
   <td> 顧客の共通名。 受信者に表示される一部の警告メッセージで使用されます。<br /> 「このメッセージが表示されるのは、『組織』または関連会社と連絡を取ったことがあるからです。 「組織」からのメッセージを受信しなくするには <br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">NmsEmail_FromName</span> <br /> </td> 
   <td> ユーザーが空のままにした場合に電子メール配信に使用される、インスタンスレベルのデフォルトの「送信元」電子メールラベル。<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">NmsEmail_ReplyToName</span> <br /> </td> 
   <td> ユーザーが空のままにした場合に、メール配信に使用されるインスタンスレベルのデフォルトの「返信先」電子メールラベル。<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">NmsEmail_RetryCount</span> <br /> </td> 
   <td> メールメッセージの 2 回の再試行の間の時間（秒）。<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">NmsEmail_RetryPeriod</span> <br /> </td> 
   <td> 電子メールメッセージの再試行期間。<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">NmsForecast_MsgWeightFormula</span> <br /> </td> 
   <td> 暫定配信用のメッセージの重み付けの計算に使用される数式。<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">NmsInmail_AllowlistEmails</span> <br /> </td> 
   <td> 許可された転送先メールアドレスのリスト （受信メール処理モジュールから）。 アドレスはコンマで区切る必要があります（すべて許可する場合は「*」）。 例：xyz@abc.com,pqr@abc.com.<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">NmsLine_AESKey</span> <br /> </td> 
   <td> URL をエンコードするために「lineImage」サーブレットで使用される AES キー（LINE チャネル）。<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">NmsNPAI_EmailMaxError</span> <br /> </td> 
   <td> チャネル「メール」上（デフォルトで使用）：受信者を強制隔離する前に、送信中のソフトエラーに対して許可されるエラーの最大数 <br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">NmsNPAI_EmailSignificantErrorDelay</span> <br /> </td> 
   <td> チャネル「電子メール」で（デフォルトで使用）：新しいソフトエラーを考慮に入れる前に、前に参照されたソフトエラー以降に費やされた最小期間 <br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">NmsNPAI_MobileMaxError</span> <br /> </td> 
   <td> チャネル「モバイル」で：送信中のソフトエラーに対して、受信者を強制隔離する前に受け入れられるエラーの最大数 <br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">NmsNPAI_MobileSignificantErrorDelay</span> <br /> </td> 
   <td> チャネル「モバイル」で：新しいソフトエラーを考慮に入れるまでの、前回の参照ソフトエラー以降に費やされた最小期間。<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">NmsMidSourcing_LogsPeriodHour</span> <br /> </td>
   <td> 同期ワークフローが実行されるたびにリカバリされる broadlog の数を制限するように、最大期間（時間単位）を指定できます。</a>.<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">NmsMidSourcing_PrepareFlow</span> <br /> </td> 
   <td> MidSourcing セッションでの呼び出しの最大数。並行して実行できます（デフォルトでは 3）。<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">NmsMTA_Alert_Delay</span> <br /> </td> 
   <td> 配信が「遅延」と見なされるまでのカスタムの遅延（分）。デフォルトは 30 分です。<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">NmsOperation_DeliveryPreparationWindow</span> <br /> </td> 
   <td><p>このオプションは、実行中の配信数をカウントする際に <span class="uicontrol"><a href="../../workflow/using/about-technical-workflows.md">operationMgt</a></span> テクニカルワークフローで使用されます。</p>これを使用すると、一貫性のないステータスの配信が実行中の配信数から除外される日数を定義できます。</p><p>デフォルトでは、値は「7」に設定されています。つまり、7 日より古い一貫性のない配信は除外されます。</p></td> 
  </tr>
  <tr> 
   <td> <span class="uicontrol">NmsPaper_SenderLine1</span> <br /> </td> 
   <td> 送信者のアドレスの 1 行目。<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">NmsPaper_SenderLine3</span> <br /> </td> 
   <td> 送信者のアドレスの 3 行目。<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">NmsPaper_SenderLine4</span> <br /> </td> 
   <td> 送信者のアドレスの 4 行目。<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">NmsPaper_SenderLine6</span> <br /> </td> 
   <td> 送信者のアドレスの 6 行目。<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">NmsPaper_SenderLine7</span> <br /> </td> 
   <td> 送信者のアドレスの 7 行目。<br /> </td> 
  </tr>
  <tr> 
   <td> <span class="uicontrol">NmsServer_MirrorPageUrl</span> <br /> </td> 
   <td> ミラーページサーバーの URL （デフォルトでは、NmsTracking_ServerUrl と同じである必要があります）。<br /> URL がルーティング定義で指定されていない場合のメール配信のデフォルト値です。<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">NmsSMS_Priority</span> <br /> </td> 
   <td> 送信済み SMS メッセージのパラメーター：メッセージの優先度を示すために SMS ゲートウェイに送信される情報 <br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">NmsSMS_RetryCount</span> <br /> </td> 
   <td> SMS メッセージの送信時の再試行回数。<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">NmsSMS_RetryPeriod</span> <br /> </td> 
   <td> SMS メッセージの再試行が実行される期間。<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">NmsUserAgentStats_LastConsolidation</span> <br /> </td> 
   <td> <span class="uicontrol">NmsUserAgent</span> 統計の最終統合日 <br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">NmsWebSegments_LastStates</span> <br /> </td> 
   <td> Web セグメントとその状態を含むオプションの名前 <br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">XtkBarcode_SpecialChar</span> <br /> </td> 
   <td> Code128.<br /> の特殊文字のサポートを有効/無効にする </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">XtkEmail_Characters</span> <br /> </td> 
   <td> E メール アドレスに対して有効な文字。<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">XtkSecurity_Restrict_EditXML</span> </td> 
   <td> このオプションを「0」値で追加して、配信の XML コードの編集を無効にします（右クリック/<span class="uicontrol">XML ソースを編集 </span> または <span class="uicontrol">Ctrl + F4</span> ショートカット）。<br /> </td> 
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
   <td> <span class="uicontrol">NcmRessourcesDir</span> <br /> </td> 
   <td> Adobe Campaign クライアントコンソールで公開するリソースの場所。 <a href="../../delivery/using/formatting.md#image-referencing">この節</a>を参照してください。<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">NcmRessourcesDirPreview</span> <br /> </td> 
   <td> Adobe Campaign クライアントコンソールでプレビューするリソースの場所。 <a href="../../delivery/using/formatting.md#image-referencing">この節</a>を参照してください。<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">NmsDelivery_DefaultIgnoredImage</span> <br /> </td> 
   <td> アップロード時にスキップされる画像の URL マスクのリスト。<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">NmsDelivery_ImagePublishing</span> </td> 
   <td> 画像アップロードの設定。 値は、なし/ トラッキング / スクリプト / リストにすることができます（オペレーターのオプション設定で上書きできます）。 </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">NmsDelivery_ImageSubDirectory</span> <br /> </td> 
   <td> サーバー上の画像を保存するフォルダー。<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">NmsServer_LogoPath</span> <br /> </td> 
   <td> ロゴを表示するスペース。<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">NcmPublishingDir</span> <br /> </td> 
   <td> パブリケーションのルートフォルダー。<br />HTMLとテキストコンテンツの生成について詳しくは、<a href="../../delivery/using/using-a-content-template.md"> この節 </a> を参照してください。<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">XtkImageUrl</span> <br /> </td> 
   <td> 配信で使用される画像を保存するサーバーを定義して、ブラウザーが取得できるようにします。<br /> ビルドバージョン 5098 未満の場合、インスタンスにアップロードされた画像の URL を使用します。<br /> ビルドバージョン 5098 以上の場合、代わりに、配信のパブリック URL または <span class="uicontrol">XtkFileRes_Public_URL</span> オプションの URL を使用します。<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">NmsDelivery_MediaInstance</span> <br /> </td> 
   <td> 画像をアップロードするためのインスタンス名を設定できます。<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">NmsDelivery_MediaPassword</span> <br /> </td> 
   <td> 画像をアップロードするためのパスワードを設定できます。<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">NmsDelivery_MediaServers</span> <br /> </td> 
   <td> 画像をアップロードするメディア URL を設定できます。<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">NmsBroadcast_MsgWebValidityDuration</span> <br /> </td> 
   <td> 配信のオンラインリソースのデフォルトの有効期間（秒単位）。<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">XtkFileRes_Public_URL</span> <br /> </td> 
   <td> パブリックリソースファイルの新しい URL。<br /> </td> 
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
   <td> この月数のマーケティング履歴が表示されます。<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">NmsOperation_Duration</span> <br /> </td> 
   <td> キャンペーンのデフォルトの有効期間（秒単位）。<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">NmsOperation_LimitConcurrency</span> <br /> </td> 
   <td> operationMgt ワークフローによって開始された、一度に処理できる配信/ワークフロー/仮説/シミュレーションジョブの最大数 <br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">NmsOperation_OperationMgtDebug</span> <br /> </td> 
   <td> <a href="../../workflow/using/about-technical-workflows.md">operationMgt</a> テクニカルワークフローの実行を監視できます。 有効（値「1」）にすると、実行情報がワークフローの監査ログに記録されます。<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">NmsOperation_TimeRange</span> <br /> </td> 
   <td> スケジュールされたモードでのターゲティングおよび抽出条件の期間。<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">Workflow_AnalysisThreshold</span> <br /> </td> 
   <td> 影響を受けるレコードの数。この数を超えると、テーブルの統計が自動的に再計算されます。<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">XtkReport_Logo</span> <br /> </td> 
   <td> エクスポートされた報告書の右上隅に表示されるロゴ。<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">NmsServer_PausedWorkflowPeriod</span> <br /> </td> 
   <td> 一時停止したワークフローのチェック間の待機日数。<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">NmsCampaign_Activate_OwnerConfirmation</span> <br /> </td> 
   <td> 値として「1」を入力して、操作の所有者による配信の検証を有効にします。 このオプションを非アクティブにするには、「0」と入力します。<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">NmsAsset_JavascriptExt</span> <br /> </td> 
   <td> ワークフローのアクティビティ「マーケティングリソース通知」に読み込む追加の JS ライブラリ。<br /> </td> 
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
   <td> <span class="uicontrol">RestrictEditingOOTBchema</span> <br /> </td> 
   <td> （21.1.3 リリース以降） 1 を選択した場合（デフォルト値）、このオプションはビルトインスキーマの編集を無効にします。<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">RestrictEditingOOTBJavascript</span> <br /> </td> 
   <td> （21.1.3 リリース以降） 1 を選択した場合（デフォルト値）、このオプションは組み込みJavaScript コードの編集を無効にします。<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">XtkAcceptOldPasswords</span> <br /> </td> 
   <td> （互換性モードをインストール：build&gt;6000）有効にすると（値「1」）、外部アカウントまたはインスタンスへの接続のために、データベースに保存されている古いパスワードを使用できます。<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">XtkKey</span> <br /> </td> 
   <td> このキーは、データベース内のほとんどのパスワードの暗号化に使用されます。 （外部アカウント、LDAP パスワード…）.<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">XtkSecurity_Allow_PrivilegeEscalation</span> <br /> </td> 
   <td> 1 を選択した場合、JavaScriptで privilegeEscalation を許可します。<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">XtkSecurity_Disable_ControlsOnFileDownload</span> <br /> </td> 
   <td> 1 を選択すると、このオプションは、ファイルのダウンロード中に（fileDownload.jsp 経由で） ACL コントロールを無効にします <br />。 </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">XtkSecurity_Disable_JSFileSandboxing</span> <br /> </td> 
   <td> 1 が選択されている場合、このオプションは Javascript.<br /> 内のファイルのサンドボックスを無効にします </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">XtkSecurity_SaveOptions_AllowNonAdmin</span> <br /> </td> 
   <td> 「true」に設定した場合、管理者以外のオペレーターは、デプロイメントウィザードを使用して xtkOption 値を更新できるように許可されました。<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">XtkSecurity_Unsafe_DecryptString</span> <br /> </td> 
   <td> 1 が選択されている場合、このオプションを使用すると、decryptString を使用して一部のパスワードを復号化できます。<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">XtkTraceDeleteLogin</span> <br /> </td> 
   <td> 「1」の値を入力して、レコードの削除前に「変更者」フィールドを変更することで、mData 内の監査記録情報を含む要素の削除をトレースします。<br /> </td> 
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
   <td> <span class="uicontrol">MC_EnrichmentCustomJs</span> <br /> </td> 
   <td> イベントを充実させるためにパーソナライズされるJavaScript ライブラリ。 次の 2 つの関数の実装を含める必要があります。<br /> 
    <ul> 
     <li> <p> <span class="uicontrol">enrichRtEvents （aiEventId）;</span>：イベントをデータベースにエンリッチメントして保存します（<span class="uicontrol">aiEventId</span> は、処理されたリアルタイムイベントのテーブルに対応します）。</p> </li> 
     <li> <p> <span class="uicontrol">enrichBatchEvents （aiEventId）;</span>：イベントをデータベースにエンリッチメントして保存します（<span class="uicontrol">aiEventId</span> は、処理されたバッチイベントの ID テーブルに対応します）。</p> </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">MC_LastUpdateFromBL</span> <br /> </td> 
   <td> 配信ログを使用してイベントステータスを最後に更新した日付。<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">MC_RoutingCustomJs</span> <br /> </td> 
   <td> ルーティングイベント用にパーソナライズするJavaScript ライブラリ。 次の 2 つの関数の実装を含める必要があります。<br /> 
    <ul> 
     <li> <p> <span class="uicontrol">dispatchRtEvent （iEventId）;</span>：リアルタイムイベントを処理するために選択されたトランザクションメッセージの内部名を返します（<span class="uicontrol">iEventId</span> は、処理されるリアルタイムイベントの ID に対応します）。</p> </li> 
     <li> <p> <span class="uicontrol">dispatchBatchEvent （iEventId）;</span>：バッチイベントを処理するために選択されたトランザクションメッセージの内部名を返します（<span class="uicontrol">iEventId</span> は、処理されるバッチイベントの ID に対応します）。</p> </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">MC_RtEventAvgDeliveryTimeAlert</span> <br /> </td> 
   <td> リアルタイムイベントの平均送信時間のアラートしきい値。<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">MC_RtEventAvgDeliveryTimeWarning</span> <br /> </td> 
   <td> リアルタイムイベントの平均送信時間を警告する際のしきい値。<br /> </td> 
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
   <td> リアルタイムイベントの平均キュー格納時間のアラートしきい値。<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">MC_RtEventAvgQueueTimeWarning</span> <br /> </td> 
   <td> リアルタイムイベントの平均キュー格納時間を警告する際のしきい値。<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">MC_RtEventAvgQueueWarning</span> <br /> </td> 
   <td> キュー内にあるリアルタイムイベントの平均数を警告する際のしきい値。<br /> </td> 
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
   <td> キュー内にあるリアルタイムイベントの最大数を警告する際のしきい値。<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">MC_RtEventMinQueueAlert</span> <br /> </td> 
   <td> 待機中リアルタイムイベントの最小数のアラートしきい値。<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">MC_RtEventMinQueueWarning</span> <br /> </td> 
   <td> キュー内にあるリアルタイムイベントの最小数を警告する際のしきい値。<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">MC_RtEventQueueAlert</span> <br /> </td> 
   <td> 保留中リアルタイムイベントのキューのアラートしきい値。<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">MC_RtEventQueueWarning</span> <br /> </td> 
   <td> 保留中リアルタイムイベントのキューを警告する前のしきい値。<br /> </td> 
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
   <td> イベント ルーティング用の再グループ化のサイズ。<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">MC_LastRtEventStat</span> <br /> </td> 
   <td> RtEvent ステータスのポインターを更新します（データが取得された最後の日付まで）。<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">NmsLine_MessageCenterURL</span> <br /> </td> 
   <td> ウェルカムメッセージ（LINE チャネル）を送信するために使用される Message Center サーバーの URL です。<br /> </td> 
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
   <td> クリーンアッププロセスが最後に実行された時刻を定義します。<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">NmsCleanup_BroadLogPurgeDelay</span> <br /> </td> 
   <td> <p>ブロードログがデータベースから消去されるまでの遅延時間を定義できます。</p><p>このオプションは、インターフェイス内で遅延が変更されると、自動的に作成されます。 オプションリストの値を変更する場合は、秒単位で指定する必要があります。</p><br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">NmsCleanup_EventHistoPurgeDelay</span> <br /> </td> 
   <td><p> イベント履歴がデータベースから消去されるまでの遅延時間を定義できます。</p><p>
   このオプションは、インターフェイス内で遅延が変更されると、自動的に作成されます。 オプションリストの値を変更する場合は、秒単位で指定する必要があります。</p><br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">NmsCleanup_EventPurgeDelay</span> <br /> </td> 
   <td><p> イベントがデータベースから消去されるまでの遅延時間を定義できます。</p><p>このオプションは、インターフェイス内で遅延が変更されると、自動的に作成されます。 オプションリストの値を変更する場合は、秒単位で指定する必要があります。</p><br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">NmsCleanup_EventStatPurgeDelay</span> <br /> </td> 
   <td><p> イベント統計がデータベースから消去されるまでの遅延時間を定義できます。</p><p>このオプションは、インターフェイス内で遅延が変更されると、自動的に作成されます。 オプションリストの値を変更する場合は、秒単位で指定する必要があります。</p><br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">NmsCleanup_PropositionPurgeDelay</span> <br /> </td> 
   <td><p> 提案がデータベースから消去されるまでの遅延時間を定義できます。</p><p> このオプションは、インターフェイス内で遅延が変更されると、自動的に作成されます。 オプションリストの値を変更する場合は、秒単位で指定する必要があります。</p><br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">NmsCleanup_QuarantineMailboxFull</span> <br /> </td> 
   <td> <p>強制隔離がデータベースから消去されるまでの遅延時間を定義できます。</p><p> このオプションは、インターフェイス内で遅延が変更されると、自動的に作成されます。 オプションリストの値を変更する場合は、秒単位で指定する必要があります。</p><br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">NmsCleanup_RecycledDeliveryPurgeDelay</span> <br /> </td> 
   <td> <p>リサイクルされた配信がデータベースから消去されるまでの遅延時間を定義できます。</p><p> このオプションは、インターフェイス内で遅延が変更されると、自動的に作成されます。 オプションリストの値を変更する場合は、秒単位で指定する必要があります。</p><br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">NmsCleanup_RejectsPurgeDelay</span> <br /> </td> 
   <td> <p>却下がデータベースから消去されるまでの遅延時間を定義できます。</p><p>このオプションは、インターフェイス内で遅延が変更されると、自動的に作成されます。 オプションリストの値を変更する場合は、秒単位で指定する必要があります。</p><br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">NmsCleanup_TrackingLogPurgeDelay</span> <br /> </td> 
   <td> <p>トラッキングログがデータベースから消去されるまでの遅延時間を定義できます。</p><p>このオプションは、インターフェイス内で遅延が変更されると、自動的に作成されます。 オプションリストの値を変更する場合は、秒単位で指定する必要があります。</p><br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">NmsCleanup_TrackingStatPurgeDelay</span> <br /> </td> 
   <td><p> トラッキング統計がデータベースから消去されるまでの遅延時間を定義できます。</p><p> このオプションは、インターフェイス内で遅延が変更されると、自動的に作成されます。 オプションリストの値を変更する場合は、秒単位で指定する必要があります。</p><br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">NmsCleanup_VisitorPurgeDelay</span> <br /> </td> 
   <td> <p>訪問者がデータベースから消去されるまでの遅延時間を定義できます。</p><p> このオプションは、インターフェイス内で遅延が変更されると、自動的に作成されます。 オプションリストの値を変更する場合は、秒単位で指定する必要があります。</p><br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">NmsCleanup_WorkflowResultPurgeDelay</span> <br /> </td> 
   <td> <p>ワークフローの結果がデータベースから消去されるまでの遅延時間を定義できます。</p><p> このオプションは、インターフェイス内で遅延が変更されると、自動的に作成されます。 オプションリストの値を変更する場合は、秒単位で指定する必要があります。</p><br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">WdbcCapabilities_AzureDw</span> <br /> </td> 
   <td> Azure SQL Datawarehouse コネクタオプション。<br /> </td> 
  </tr>
   <tr> 
   <td> <span class="uicontrol">WdbcKillSessionPolicy</span> <br /> </td> 
   <td>すべてのワークフローおよび PostgreSQL データベースクエリに対して、次の値に従って無条件停止動作を有効にできます。<ul>
    <li><p>0 - デフォルト：ワークフロープロセスを停止します。データベースには影響しません<p></li>
    <li><p>1 - pg_cancel_backend：ワークフロープロセスを停止し、データベース内のクエリをキャンセルします<p></li>
    <li><p>2 - pg_terminate_backend：ワークフロープロセスを停止し、データベース内のクエリを終了します<p></li></ul></td> 
  </tr>  
    <tr> 
   <td> <span class="uicontrol">WdbcOptions_TableSpaceUser</span> <br /> </td> 
   <td> Adobe Campaign ootb 表のデータを格納する表領域の名前。<br /> データベースの作成および構成 <a href="../../installation/using/creating-and-configuring-the-database.md"> を参照してください </a>。</td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">WdbcOptions_TableSpaceIndex</span> <br /> </td> 
   <td> Adobe Campaign ootb 表の索引を格納する表領域の名前。<br /> データベースの作成および構成 <a href="../../installation/using/creating-and-configuring-the-database.md"> を参照してください </a>。</td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">WdbcOptions_TableSpaceWork</span> <br /> </td> 
   <td> Adobe Campaign作業用テーブルのデータを格納するためのテーブル領域の名前。<br /> データベースの作成および構成 <a href="../../installation/using/creating-and-configuring-the-database.md"> を参照してください </a>。</td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">WdbcOptions_TableSpaceWorkIndex</span> <br /> </td> 
   <td> Adobe Campaign作業用テーブルのインデックスを格納するためのテーブル領域の名前。<br /> データベースの作成および構成 <a href="../../installation/using/creating-and-configuring-the-database.md"> を参照してください </a>。</td> 
  </tr> 
    <tr> 
   <td> <span class="uicontrol">WdbcOptions_TempDbName</span> <br /> </td> 
   <td> バックアップとレプリケーションを最適化するために、Microsoft SQL Server 上のワークテーブルに対して個別のデータベースを設定できます。 オプションは一時データベースの名前に対応します。ワークテーブルは、指定された場合、このデータベースに書き込まれます。 例：'tempdb.dbo.' （名前の末尾はドットにする必要があります）。 <a href="../../production/using/rdbms-specific-recommendations.md#microsoft-sql-server"> 詳細を表示 </a><br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">WdbcTimeZone</span> <br /> </td> 
   <td> Adobe Campaign インスタンスのタイムゾーン。 <a href="../../installation/using/time-zone-management.md#configuration" target="_blank"> 設定 </a> を参照してください。<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">WdbcUseNChar</span> <br /> </td> 
   <td> データベースの文字列フィールドは NChar で定義されていますか？<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">WdbcUseTimeStampWithTZ</span> <br /> </td> 
   <td> データベースの「datetime」フィールドにタイムゾーン情報が格納されていますか？<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">XtkDatabaseId</span> <br /> </td> 
   <td> データベースの ID。 Unicode データベースの'u'で始まる。<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">XtkInstancePrefix</span> <br /> </td> 
   <td> 自動生成された内部名に追加されるプレフィックス。<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">XtkQuery_Schema_LineCount</span> <br /> </td> 
   <td> xtk:schema および xtk:srcSchema.<br /> のクエリによって返される結果の最大数 </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">XtkSequence_AutoGeneration</span> <br /> </td> 
   <td> この日以降に作成され、属性「pkSequence」を持たない autopk="true"を持つすべてのカスタマイズされたスキーマは、自動生成されたシーケンス「auto_」を取得します 
    &lt;schemanamespace&gt; 
     &lt; スキーマ名 &gt;
       _seq. 
   </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">NlMigration_KeepFolderStructure</span> <br /> </td> 
   <td> 移行中、ツリー構造は新しいバージョン標準に基づいて自動的に再編成されます。<br /> このオプションを使用すると、ナビゲーションツリーの自動移行を無効にできます。 これを使用すると、移行後に古いフォルダーを削除し、新しいフォルダーを追加して、必要なチェックをすべて実行する必要があります。<br /> 
    <ul> 
     <li> <p> <span class="uicontrol"> データタイプ：</span> 整数</p> </li> 
     <li> <p> <span class="uicontrol"> 値（テキスト） </span>:1 </p> </li> 
    </ul> このオプションは、標準のナビゲーションツリーに加えられた変更が多すぎる場合にのみ使用してください。<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">NmsLastErrorStatCoalesce</span> <br /> </td> 
   <td> <span class="uicontrol">NmsEmailErrorStat</span> テーブルのクリーンアップの最終処理日。<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">PostUpgradeLastError</span> <br /> </td> 
   <td> アップグレード後に発生したエラーに関する情報で、次の構文を使用します。<br /> <strong>{Build number}:{mode: pre/post/...}:{ エラーが発生した場所+ サブステップの'lessThan'/'greaterOrEquelThan'}</strong> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">XtkCleanup_NoStats</span> <br /> </td> 
   <td> 「1」の値を入力して、クリーンアップワークフローで統計の更新が実行されないようにします。<br /> </td> 
  </tr> 
 </tbody> 
</table>

## 統合 {#integration}

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
   <td> Adobe Campaignで使用できるAEM リソースのタイプ。 値はコンマで区切る必要があります。<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">nmsPipeline_config</span> <br /> </td> 
   <td> Experience Cloudトリガーを設定できます。 データタイプは「長いテキスト」で、JSON 形式である必要があります。 <a class="anchorLink" href="https://helpx.adobe.com/campaign/kb/triggers-and-campaign.html#PipelineoptionNmsPipelineConfig" target="_blank">Adobe Campaign ClassicでExperience Cloudトリガーを使用する方法 </a> を参照してください。<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">LASTIMPORT_&lt;%=instance.internalName%&gt;_&lt;%=activityName%&gt;</span> <br /> </td> 
   <td> このオプションは、CRM コネクタを使用してサードパーティシステムからデータをインポートする際に使用されます。 このオプションを有効にすると、前回の読み込み以降に変更されたオブジェクトのみを収集できます。 このオプションは、次のように手動で作成して入力する必要があります。 
    <ul> 
     <li> <p> <span class="uicontrol"> 内部名 </span> :LASTIMPORT_&lt;%=instance.internalName%&gt;_&lt;%=activityName%&gt;</p> </li> 
     <li> <p> <span class="uicontrol"> 値（フィールド） </span> :yyyy/MM/dd hh:mm:ss 形式の最後のインポートの日付。 </p> </li> 
    </ul><br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">TNT_EdgeServer</span> <br /> </td> 
   <td> 統合に使用されるAdobe Target サーバー。 このオプションは、デフォルトで選択されています。この値はAdobe Target Domain Server に対応し、続いて/m2 という値が続きます。 例：tt.omtrdc.net/m2<a href="../../integrations/using/configuring-the-integration-with-adobe-target.md"> この節 </a> を参照してくださ <br />。<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">TNT_TenantName</span> <br /> </td> 
   <td> Adobe Targetの組織名。 この値は、Adobe Target クライアントの名前に対応します。<a href="../../integrations/using/configuring-the-integration-with-adobe-target.md"> この節 </a> を参照してくださ <br />。<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">AAM_DataSourceId</span> <br /> </td> 
   <td> Adobe Audience Manager.<br /> との統合に使用するオプション </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">AAM_DestinationId</span> <br /> </td> 
   <td> Adobe Audience Manager.<br /> との統合に使用するオプション </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">WdbcCapabilities_Teradata</span> <br /> </td> 
   <td> Teradataコネクタのオプション。<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">WdbcCapabilities_Hive</span> <br /> </td> 
   <td> Hive コネクタのオプション。<br /> </td> 
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
   <td> SQL トランザクションごとに更新されるクーポンの数。<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">NmsInteraction_LastPropositionSynchControl_</span> <br /> </td> 
   <td> 「+ [ 提案のスキーマ ] + 「_」 + extAccountSource。@executionInstanceId + [ 提案のスキーマ ] + "_" + vars.executionInstanceIdFilter<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">NmsInteraction_LastPropositionSynchExec_</span> <br /> </td> 
   <td> 「+ [ 提案のスキーマ ] + 「_」 + extAccountSource。@executionInstanceId + "_" + extAccountTarget。@executionInstanceId<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">NmsInteraction_SynchWorkflowIds</span> <br /> </td> 
   <td> 同期ワークフローの追跡。<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">NmsInteraction_UseDaemon</span> <br /> </td> 
   <td> 非同期提案書き込みを有効/無効にします（「0」で無効、「1」で有効）。<br /> </td> 
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
   <td> 実行インスタンス識別子。<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">NmsServer_CustomerId</span> <br /> </td> 
   <td> 請求レポートの送信時に使用する顧客識別子。<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">NmsServer_IntranetURL</span> <br /> </td> 
   <td> アプリケーションサーバーにアクセスするための内部ベース URL。<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">NmsServer_LastPostUpgrade</span> <br /> </td> 
   <td> 前回のアップグレードの前の AC インスタンスのビルド番号。<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">NmsServer_URL</span> <br /> </td> 
   <td> 公開 Web アプリケーションサーバーのベース URL。<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">XtkPassUnknownSQLFunctionsToRDBMS</span> <br /> </td> 
   <td> 移行後も古い宣言されていない SQL 関数を引き続き使用できます。 このオプションはセキュリティリスクがあるため、使用しないことを強くお勧めします。<br /> </td> 
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
   <td> トラッキングを有効化できるオプション <br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">NmsTracking_ClickFormula</span> <br /> </td> 
   <td> トラッキングする URL の計算スクリプト。<br /> </td> 
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
   <td> URL 計算スクリプトを開きます。<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">NmsTracking_Password</span> <br /> </td> 
   <td> トラッキングサーバー <br /> パスワード </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">NmsTracking_Pointer</span> <br /> </td> 
   <td> ポインターは、ID と日付を使用して処理された最後のメッセージイベントを追跡します。<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">NmsTracking_SecureServerUrl</span> <br /> </td> 
   <td> フロントトラッキングサーバーのセキュア URL。<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">NmsTracking_ServerUrl</span> <br /> </td> 
   <td> フロントトラッキングサーバーの URL。<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">NmsTracking_ServerUrlList</span> <br /> </td> 
   <td> トラッキングサーバーへの接続に使用する URL のリスト。<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">NmsTracking_UserAgentRules</span> <br /> </td> 
   <td> ブラウザー識別ルールセット <br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">NmsTracking_WebFormula</span> <br /> </td> 
   <td> Web トラッキングタグの計算に使用するスクリプト。<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">NmsTracking_WebTrackingDelivery</span> <br /> </td> 
   <td> Web トラッキング管理用に設計された仮想配信の名前。<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">NmsTracking_WebTrackingMode</span> <br /> </td> 
   <td> Web トラッキングモードを定義できます。<br /> </td> 
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
   <td> オプション 1 を選択した場合、2 番目の手順のインターフェイスで削除を手動で確認する必要があります。 そうでない場合は、確認なしにデータが削除されます。<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">Privacy_Request_ConfirmDeletePendingDelay</span> <br /> </td> 
   <td> 削除の確認待ちのリクエストとリクエストのキャンセルの間の遅延。<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">Privacy_Request_MaxErrorAllowed</span> <br /> </td> 
   <td> プライバシーリクエストの処理中/削除中に許可されるエラーの最大数。<br /> </td> 
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
   <td> LDAP サーバーをユーザーの認証およびユーザーへの認証に使用できるようにします。<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">XtkLdap_AppLogin</span> <br /> </td> 
   <td> サーバーに問い合わせて様々な検索を行うためのアプリケーションログイン。<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">XtkLdap_AppPassword</span> <br /> </td> 
   <td> アプリケーション ログインの暗号化されたパスワード。<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">XtkLdap_AutoOperator</span> <br /> </td> 
   <td> Adobe Campaignでオペレーターと権限の自動作成を有効にします。<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">XtkLdap_DN</span> <br /> </td> 
   <td> ログイン。<br /> に基づく LDAP DN の計算式 </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">XtkLdap_DNSearch</span> <br /> </td> 
   <td> Directory.<br /> で DN 検索を有効にします。 </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">XtkLdap_DNSearchBase</span> <br /> </td> 
   <td> 検索ベース。<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">XtkLdap_DNSearchFilter</span> <br /> </td> 
   <td> DN 検索フィルター。<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">XtkLdap_DNSearchScope</span> <br /> </td> 
   <td> 検索範囲。<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">XtkLdap_Mechanism</span> <br /> </td> 
   <td> LDAP サーバーへの接続に使用する認証タイプ （plain、md5、lds、ntlm、dpa）。<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">XtkLdap_Rights</span> <br /> </td> 
   <td> LDAP ディレクトリにある権限とグループをAdobe Campaign.<br /> のネームド権限に同期できるようにします。 </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">XtkLdap_RightsAttr</span> <br /> </td> 
   <td> 認証名を含む LDAP 属性。<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">XtkLdap_RightsBase</span> <br /> </td> 
   <td> 検索ベース。<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">XtkLdap_RightsFilter</span> <br /> </td> 
   <td> ユーザー認証の検索フィルター。<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">XtkLdap_RightsMask</span> <br /> </td> 
   <td> LDAP 認証からAdobe Campaign権限の名前を抽出する式。<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">XtkLdap_RightsScope</span> <br /> </td> 
   <td> 検索範囲。<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">XtkLdap_Server</span> <br /> </td> 
   <td> LDAP サーバーアドレス （「:」を区切り文字として指定することで、ポートを指定できます）。<br /> </td> 
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
   <td> 値を 1 に設定すると、詳細フォームにスクロールバーを追加できます。<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">XtkWebForm_Instance</span> <br /> </td> 
   <td> 「その他のサーバー」モードでの Web フォーム無効化に使用するインスタンス。<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">XtkWebForm_Password</span> <br /> </td> 
   <td> 「その他のサーバー」モードでの Web フォーム無効化に使用するインスタンスのパスワード。<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">XtkWebForm_ServersMode</span> <br /> </td> 
   <td> Web フォームの無効化モードを指定できるオプション : デフォルトではローカルです。「トラッキング」オプションの場合はトラッキングサーバーを使用し、「その他のサーバー」オプションの場合はパーソナライズされたリストを使用します。<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">XtkWebForm_ServersURLs</span> <br /> </td> 
   <td> Web フォームの無効化のために接続されるサーバーのパーソナライズされたアドレスリスト （「その他のサーバー」モード）。<br /> </td> 
  </tr> 
 </tbody> 
</table>
