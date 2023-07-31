---
product: campaign
title: キャンペーンオプションの設定
description: Campaign オプションの設定方法を説明します
feature: Installation, Application Settings
badge-v7-only: label="v7" type="Informative" tooltip="Campaign Classicv7 にのみ適用"
audience: installation
content-type: reference
topic-tags: appendices
exl-id: a979cd99-afa7-4ce6-ba0f-9495089cba08
source-git-commit: 3a9b21d626b60754789c3f594ba798309f62a553
workflow-type: tm+mt
source-wordcount: '4015'
ht-degree: 24%

---

# Campaign Classic のオプションのリスト{#configuring-campaign-options}

The **[!UICONTROL 管理/プラットフォーム/オプション]** ノードでは、Adobe Campaignオプションを設定できます。 Campaign のインストール時に組み込まれるものもあれば、必要に応じて手動で追加できるものもあります。 使用可能なオプションは、インスタンスと共にインストールされているパッケージによって異なります。


>[!CAUTION]
>
>* このページに記載されていないオプションは内部のみで、 **は変更できません**.
>
>* Adobe Campaignオプションの変更または更新は、エキスパートユーザーのみが実行できます。

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
   <td> 配信品質インスタンスから取得した最後の broadLogMsg の日付。<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">Deliverability_LastBroadLogMsgSent</span> <br /> </td> 
   <td> 配信品質インスタンスに送信された最後の broadLogMsg の日付。<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">DmRendering_cuid</span> <br /> </td> 
   <td> 配信レポート識別子。識別子を取得するには、サポートにお問い合わせください。<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">DmRendering_SeedTargets</span> <br /> </td> 
   <td> 受信ボックスレンダリングのテストアドレスを使用するスキーマのリスト。
(要素名はコンマ区切りで指定)
例 : custom_nms_recipient.<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">EMTA_BCC_ADDRESS</span> </td> 
   <td> Enhanced MTA が送信済み電子メールの生のコピーを送信する BCC 電子メールアドレス。 <br /> </td> 
  </tr>
  <tr> 
   <td> <span class="uicontrol">NMS_ActivateOwnerConfirmation</span> <br /> </td> 
   <td><p> 配信のプロパティで、配信を開始するために特定のオペレーターまたはオペレーターのグループが指定されている場合に、配信を担当するオペレーターが送信を確認できるようにします。</p><p> これをおこなうには、値に「1」を入力して、オプションを有効にします。 このオプションを無効にするには、"0"と入力します。</p><p> すると、送信確認プロセスがデフォルトとして機能します。つまり、配信プロパティで送信用に指定されたオペレーターまたはオペレーターのグループ（または管理者）のみが、送信を確認し、実行できるようになります。詳しくは、<a href="../../campaign/using/marketing-campaign-deliveries.md#starting-an-online-delivery">この節</a>を参照してください。</p> </td> 
   <tr> 
   <td> <span class="uicontrol">Nms_DefaultRcpSchema</span> <br /> </td> 
   <td> Adobe Campaignは、「Nms_DefaultRcpSchema」グローバル変数を使用して、デフォルトの受信者データベース (nms:recipient) とのダイアログを作成します。<br /> オプションの値は、外部の受信者テーブルと一致するスキーマの名前に対応している必要があります。<br /> </td> 
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
   <td> 配信の準備中に broadLogs を挿入するための最小バッチサイズ（行数）。<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">NmsBroadcast_MaxDelayPerTransac</span> <br /> </td> 
   <td> 配信準備中に broadLogs の挿入のバッチサイズが 2 倍になるバッチ期間しきい値（ミリ秒数）。<br /> </td> 
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
   <td> 「1」を値として入力すると、今後連絡を希望しない受信者が除外されます。<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">NmsBroadcast_RemoveDuplicatesRecipients</span> <br /> </td> 
   <td> 値に「1」を入力すると、コピーが自動的に無視されます。<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">NmsDelivery_ErrorAddressMasks</span> <br /> </td> 
   <td> メッセージの返信時に使用するエラーアドレスの構文を定義できます。<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">NmsDelivery_FromAddressMasks</span> <br /> </td> 
   <td> メッセージの送信時に使用される送信者アドレスの構文を定義できます。<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">NmsDelivery_ImageServerTimeout</span> <br /> </td> 
   <td> パーソナライズされた URL からダウンロードされ、E メールに添付された画像を取得する際の、サーバーからの応答取得のタイムアウト制限（秒）を定義できます。 この値を超えると、メッセージは送信されません。 デフォルト値は 60 秒です。<br /> </td> 
  </tr> 
 <tr> 
   <td> <span class="uicontrol">NmsDelivery_MaxDownloadedImageSize</span> <br /> </td> 
   <td> パーソナライズされた URL からダウンロードされ、E メールに添付された画像に許可される最大サイズ（バイト単位）を定義できます。 デフォルト値は 100,000 バイト (100 KB) です。 配達確認を送信し、E メールを処理するために画像をダウンロードする際に、画像のサイズがこの値を超えた場合、またはダウンロードの問題が発生した場合は、配信ログにエラーが表示され、配達確認の配信が失敗します。<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">NmsDelivery_MaxRecommendedAttachments</span> <br /> </td> 
   <td> E メールまたはトランザクション E メールテンプレートの添付ファイルの最大数を設定できます。 この値を超えると、配信分析ログまたはトランザクション E メールテンプレートの公開時に、警告が表示されます。 デフォルト値は 1 の添付ファイルです。<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">NmsDelivery_MaxRetry</span> <br /> </td> 
   <td> 分析中の再試行の最大数.<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">NmsDelivery_PublishingScript</span> <br /> </td> 
   <td> 公開スクリプト.<br /> </td> 
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
   <td> ユーザーが空のままにした場合、インスタンスのレベルで E メールの配信に使用されるデフォルトの「エラー」E メールアドレス。<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">NmsEmail_DefaultFromAddr</span> <br /> </td> 
   <td> ユーザーが空のままにした場合、インスタンスのレベルで E メール配信に使用されるデフォルトの「差出人」E メールアドレス。<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">NmsEmail_DefaultReplyToAddr</span> <br /> </td> 
   <td> ユーザーが空のままにした場合、インスタンスのレベルで E メール配信に使用されるデフォルトの「返信先」E メールアドレス。<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">NmsEmail_ExpOrganization</span> <br /> </td> 
   <td> 顧客の共通名. 一部の警告メッセージで、受信者に表示される際に使用されます。<br /> 「組織や関連会社と連絡を取っていたので、このメッセージを受け取っています。 「組織」からのメッセージを受信しないようにするには<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">NmsEmail_FromName</span> <br /> </td> 
   <td> ユーザーが空のままにした場合に E メール配信に使用されるインスタンスのレベルのデフォルトの「差出人」E メールラベル。<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">NmsEmail_ReplyToName</span> <br /> </td> 
   <td> ユーザーが空のままにした場合に E メール配信に使用されるインスタンスのレベルのデフォルトの「返信先」E メールラベル。<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">NmsEmail_RetryCount</span> <br /> </td> 
   <td> E メールメッセージの 2 回の再試行間の期間（秒）。<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">NmsEmail_RetryPeriod</span> <br /> </td> 
   <td> E メールメッセージの再試行の期間。<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">NmsForecast_MsgWeightFormula</span> <br /> </td> 
   <td> 暫定的な配信メッセージの重み付けを計算するときに使用する数式.<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">NmsInmail_AllowlistEmails</span> <br /> </td> 
   <td> （インバウンドメール処理モジュールから）許可された転送 E メールアドレスのリスト。アドレスはコンマで区切る必要があります（またはすべてを許可する場合は*を使用）。例： xyz@abc.com,pqr@abc.com<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">NmsLine_AESKey</span> <br /> </td> 
   <td> URL をエンコードするために「lineImage」サーブレットで使用される AES キー (LINE チャネル).<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">NmsNPAI_EmailMaxError</span> <br /> </td> 
   <td> チャネル「email」で（デフォルトとして使用） ：送信中に SOFT エラーが発生した場合に受け入れられるエラーの最大数（受信者を強制隔離します）。<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">NmsNPAI_EmailSignificantErrorDelay</span> <br /> </td> 
   <td> チャネル「email」（デフォルトとして使用） ：新しい SOFT エラーを考慮する前に、以前に参照された SOFT エラー以降に費やした最小期間。<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">NmsNPAI_MobileMaxError</span> <br /> </td> 
   <td> チャネル「mobile」上：送信中に受信者を強制隔離する前に発生した SOFT エラーに対して、受け入れられるエラーの最大数。<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">NmsNPAI_MobileSignificantErrorDelay</span> <br /> </td> 
   <td> チャネル「モバイル」上：新しい SOFT エラーを考慮に入れる前に、以前参照した SOFT エラー以降に費やした最小期間。<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">NmsMidSourcing_LogsPeriodHour</span> <br /> </td>
   <td> 同期ワークフローが実行されるたびに復元される broadlog の数を制限するために、最大期間（時間単位）を指定できます。</a>.<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">NmsMidSourcing_PrepareFlow</span> <br /> </td> 
   <td> MidSourcing セッションの最大呼び出し数。同時に実行できます（デフォルトでは 3）。<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">NmsMTA_Alert_Delay</span> <br /> </td> 
   <td> 配信が「遅延」と見なされるまでのカスタムの遅延（分）。デフォルトは 30 分です。<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">NmsOperation_DeliveryPreparationWindow</span> <br /> </td> 
   <td><p>このオプションは、 <span class="uicontrol"><a href="../../workflow/using/about-technical-workflows.md">operationMgt</a></span> 実行中の配信の数をカウントする際のテクニカルワークフロー。</p>このオプションを使用すると、ステータスの一貫しない配信が、実行中の配信の数から除外される日数を定義できます。</p><p>デフォルトでは、値は「7」に設定されています。これは、7 日より古い一貫性のない配信が除外されることを意味します。</p></td> 
  </tr>
  <tr> 
   <td> <span class="uicontrol">NmsPaper_SenderLine1</span> <br /> </td> 
   <td> 送信者のアドレスのライン 1。<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">NmsPaper_SenderLine3</span> <br /> </td> 
   <td> 送信者のアドレスのライン 3。<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">NmsPaper_SenderLine4</span> <br /> </td> 
   <td> 送信者のアドレスのライン 4。<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">NmsPaper_SenderLine6</span> <br /> </td> 
   <td> 送信者のアドレスのライン 6。<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">NmsPaper_SenderLine7</span> <br /> </td> 
   <td> 送信者のアドレスのライン 7。<br /> </td> 
  </tr>
  <tr> 
   <td> <span class="uicontrol">NmsServer_MirrorPageUrl</span> <br /> </td> 
   <td> ミラーページサーバーの URL（デフォルトでは、NmsTracking_ServerUrl と同じである必要があります）。<br /> これは、ルーティング定義で URL が指定されていない場合の E メール配信のデフォルト値です。<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">NmsSMS_Priority</span> <br /> </td> 
   <td> 送信済み SMS メッセージのパラメーター：メッセージの優先度を示すために SMS ゲートウェイに送信される情報。<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">NmsSMS_RetryCount</span> <br /> </td> 
   <td> SMS メッセージの送信時の再試行の回数。<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">NmsSMS_RetryPeriod</span> <br /> </td> 
   <td> SMS メッセージの再試行を実行する期間。<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">NmsUserAgentStats_LastConsolidation</span> <br /> </td> 
   <td> の最終連結日 <span class="uicontrol">NmsUserAgent</span> 統計。<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">NmsWebSegments_LastStates</span> <br /> </td> 
   <td> Web セグメントとその状態を含むオプションの名前。<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">XtkBarcode_SpecialChar</span> <br /> </td> 
   <td> Code128 の特殊文字のサポートを有効/無効にします。<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">XtkEmail_Characters</span> <br /> </td> 
   <td> E メールアドレスで有効な文字.<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">XtkSecurity_Restrict_EditXML</span> </td> 
   <td> 配信の XML コードのエディションを無効にするには、このオプションを「0」値で追加します ( 右クリック/ <span class="uicontrol">XML ソースを編集</span> または <span class="uicontrol">Ctrl + F4</span> ショートカット )。<br /> </td> 
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
   <td> Adobe Campaignクライアントコンソールでのパブリッシュ用リソースの場所。 詳しくは、<a href="../../delivery/using/formatting.md#image-referencing">この節</a>を参照してください。<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">NcmRessourcesDirPreview</span> <br /> </td> 
   <td> Adobe Campaignクライアントコンソールでプレビューするリソースの場所。 詳しくは、<a href="../../delivery/using/formatting.md#image-referencing">この節</a>を参照してください。<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">NmsDelivery_DefaultIgnoredImage</span> <br /> </td> 
   <td> アップロード時にスキップする画像の URL マスクのリスト.<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">NmsDelivery_ImagePublishing</span> </td> 
   <td> 画像のアップロードの設定. 値は、 none / tracking / script / list にすることができます（演算子のオプション設定で上書きできます）。 </td> 
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
   <td> 公開用ルートフォルダー.<br /> HTMLとテキストコンテンツの生成について詳しくは、 <a href="../../delivery/using/using-a-content-template.md">この節</a>.<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">XtkImageUrl</span> <br /> </td> 
   <td> 配信に使用する画像を保存するサーバーを定義して、ブラウザーがそれらを取得できるようにします。<br /> ビルドバージョンが 5098 未満の場合は、インスタンスにアップロードされた画像の URL を使用します。<br /> ビルドバージョンが 5098 より大きい場合、配信のパブリック URL または <span class="uicontrol">XtkFileRes_Public_URL</span> オプションの URL。<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">NmsDelivery_MediaInstance</span> <br /> </td> 
   <td> 画像のアップロード用にインスタンス名を設定できます。<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">NmsDelivery_MediaPassword</span> <br /> </td> 
   <td> 画像のアップロード用のパスワードを設定できます。<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">NmsDelivery_MediaServers</span> <br /> </td> 
   <td> 画像アップロード用のメディア URL を設定できます。<br /> </td> 
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
   <td> operationMgt ワークフローで開始し、一度に処理できる配信/ワークフロー/仮説/シミュレーションジョブの最大数。<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">NmsOperation_OperationMgtDebug</span> <br /> </td> 
   <td> 次の項目を監視できます。 <a href="../../workflow/using/about-technical-workflows.md">operationMgt</a> テクニカルワークフローの実行 有効化すると（値「1」）、実行情報がワークフロー監査ログに記録されます。<br /> </td> 
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
   <td> 一時停止したワークフローのチェック間の待機日数。<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">NmsCampaign_Activate_OwnerConfirmation</span> <br /> </td> 
   <td> 操作の所有者による配信の検証を有効にするには、値に「1」を入力します。 このオプションを無効にするには、"0"と入力します。<br /> </td> 
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
   <td> <span class="uicontrol">RestrictEditingOOTBSchema</span> <br /> </td> 
   <td> （21.1.3 リリース以降）1 が選択されている場合（デフォルト値）、このオプションは組み込みスキーマのエディションを無効にします。<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">RestrictEditingOOTBJavascript</span> <br /> </td> 
   <td> （21.1.3 リリース以降）1 を選択した場合（デフォルト値）、このオプションを選択すると、組み込み JavaScript コードのエディションが無効になります。<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">XtkAcceptOldPasswords</span> <br /> </td> 
   <td> （インストール互換性モード：ビルド &gt; 6000）有効化すると（値"1"）、このオプションを使用して、外部アカウントやインスタンスへの接続に使用するためにデータベースに保存されている古いパスワードを使用できます。<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">XtkKey</span> <br /> </td> 
   <td> このキーは、データベース内のほとんどのパスワードを暗号化するために使用されます。（外部アカウント、LDAP パスワード…）。<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">XtkSecurity_Allow_PrivilegeEscalation</span> <br /> </td> 
   <td> 1 を選択した場合、このオプションを使用して JavaScript で privilegeEscalation を許可します。<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">XtkSecurity_Disable_ControlsOnFileDownload</span> <br /> </td> 
   <td> 1 を選択した場合、このオプションは（fileDownload.jsp を介した）ファイルのダウンロード中に ACL コントロールを無効にします。<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">XtkSecurity_Disable_JSFileSandboxing</span> <br /> </td> 
   <td> 1 を選択した場合、このオプションは JavaScript 内のファイルサンドボックスを無効にします。<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">XtkSecurity_SaveOptions_AllowNonAdmin</span> <br /> </td> 
   <td> 「true」に設定した場合、管理者以外のオペレーターに対し、デプロイウィザードで xtkOption の値を更新することを許可しました。<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">XtkSecurity_Unsafe_DecryptString</span> <br /> </td> 
   <td> 1 を選択した場合、このオプションを使用すると、一部のパスワードを decryptString で復号化できます。<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">XtkTraceDeleteLogin</span> <br /> </td> 
   <td> 「1」の値を入力して、レコードを削除する前に mData の「変更者」フィールドを変更して、監査証跡情報を含む要素の削除をトレースします。<br /> </td> 
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
   <td> イベントをエンリッチメントするためにパーソナライズされる JavaScript ライブラリ。には、次の 2 つの関数の実装を含める必要があります。<br /> 
    <ul> 
     <li> <p> <span class="uicontrol">enrichRtEvents(aiEventId);</span> ：データベース内のイベントをエンリッチメントして保存します ( <span class="uicontrol">aiEventId</span> は、処理されたリアルタイムイベントの表に対応します )。</p> </li> 
     <li> <p> <span class="uicontrol">enrichBatchEvents(aiEventId);</span> ：データベース内のイベントをエンリッチメントして保存します ( <span class="uicontrol">aiEventId</span> は、処理されたバッチイベントの ID テーブルに対応します )。</p> </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">MC_LastUpdateFromBL</span> <br /> </td> 
   <td> 配信ログ経由での前回のイベントステータス更新の日付。<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">MC_RoutingCustomJs</span> <br /> </td> 
   <td> ルーティングイベント用にパーソナライズする JavaScript ライブラリ。には、次の 2 つの関数の実装を含める必要があります。<br /> 
    <ul> 
     <li> <p> <span class="uicontrol">dispatchRtEvent(iEventId);</span> ：リアルタイムイベントの処理に選択したトランザクションメッセージの内部名を戻します ( <span class="uicontrol">iEventId</span> は、処理されたリアルタイムイベントの ID に対応します )。</p> </li> 
     <li> <p> <span class="uicontrol">dispatchBatchEvent(iEventId);</span> ：バッチイベントの処理に選択されたトランザクションメッセージの内部名を戻します ( <span class="uicontrol">iEventId</span> は、処理されたバッチイベントの ID に対応します )。</p> </li> 
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
   <td> RtEvent ステータスのポインター（データが取得されるまでの最終日）を更新します。<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">NmsLine_MessageCenterURL</span> <br /> </td> 
   <td> ようこそメッセージの送信に使用する Message Center サーバー URL (LINE Channel)。<br /> </td> 
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
   <td> <p>データベースから broadlog が消去されるまでの遅延を定義できます。</p><p>このオプションは、インターフェイス内で遅延が変更されると自動的に作成されます。 オプションリストから値を変更する場合は、秒単位で表す必要があります。</p><br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">NmsCleanup_EventHistoPurgeDelay</span> <br /> </td> 
   <td><p> データベースからイベント履歴が消去されるまでの遅延を定義できます。</p><p>
   このオプションは、インターフェイス内で遅延が変更されると自動的に作成されます。 オプションリストから値を変更する場合は、秒単位で表す必要があります。</p><br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">NmsCleanup_EventPurgeDelay</span> <br /> </td> 
   <td><p> データベースからイベントが消去されるまでの遅延を定義できます。</p><p>このオプションは、インターフェイス内で遅延が変更されると自動的に作成されます。 オプションリストから値を変更する場合は、秒単位で表す必要があります。</p><br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">NmsCleanup_EventStatPurgeDelay</span> <br /> </td> 
   <td><p> データベースからイベント統計を消去するまでの遅延を定義できます。</p><p>このオプションは、インターフェイス内で遅延が変更されると自動的に作成されます。 オプションリストから値を変更する場合は、秒単位で表す必要があります。</p><br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">NmsCleanup_PropositionPurgeDelay</span> <br /> </td> 
   <td><p> データベースから提案が消去されるまでの遅延を定義できます。</p><p> このオプションは、インターフェイス内で遅延が変更されると自動的に作成されます。 オプションリストから値を変更する場合は、秒単位で表す必要があります。</p><br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">NmsCleanup_QuarantineMailboxFull</span> <br /> </td> 
   <td> <p>データベースから強制隔離が消去されるまでの遅延を定義できます。</p><p> このオプションは、インターフェイス内で遅延が変更されると自動的に作成されます。 オプションリストから値を変更する場合は、秒単位で表す必要があります。</p><br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">NmsCleanup_RecycledDeliveryPurgeDelay</span> <br /> </td> 
   <td> <p>リサイクルされた配信がデータベースから消去されるまでの遅延を定義できます。</p><p> このオプションは、インターフェイス内で遅延が変更されると自動的に作成されます。 オプションリストから値を変更する場合は、秒単位で表す必要があります。</p><br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">NmsCleanup_RejectsPurgeDelay</span> <br /> </td> 
   <td> <p>データベースから却下が消去されるまでの遅延を定義できます。</p><p>このオプションは、インターフェイス内で遅延が変更されると自動的に作成されます。 オプションリストから値を変更する場合は、秒単位で表す必要があります。</p><br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">NmsCleanup_TrackingLogPurgeDelay</span> <br /> </td> 
   <td> <p>データベースからトラッキングログが消去されるまでの遅延を定義できます。</p><p>このオプションは、インターフェイス内で遅延が変更されると自動的に作成されます。 オプションリストから値を変更する場合は、秒単位で表す必要があります。</p><br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">NmsCleanup_TrackingStatPurgeDelay</span> <br /> </td> 
   <td><p> データベースからトラッキング統計が消去されるまでの遅延を定義できます。</p><p> このオプションは、インターフェイス内で遅延が変更されると自動的に作成されます。 オプションリストから値を変更する場合は、秒単位で表す必要があります。</p><br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">NmsCleanup_VisitorPurgeDelay</span> <br /> </td> 
   <td> <p>データベースから訪問者が消去されるまでの遅延を定義できます。</p><p> このオプションは、インターフェイス内で遅延が変更されると自動的に作成されます。 オプションリストから値を変更する場合は、秒単位で表す必要があります。</p><br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">NmsCleanup_WorkflowResultPurgeDelay</span> <br /> </td> 
   <td> <p>データベースからワークフローの結果が消去されるまでの遅延を定義できます。</p><p> このオプションは、インターフェイス内で遅延が変更されると自動的に作成されます。 オプションリストから値を変更する場合は、秒単位で表す必要があります。</p><br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">WdbcCapabilities_AzureDw</span> <br /> </td> 
   <td> Azure SQL Datawarehouse コネクタオプション.<br /> </td> 
  </tr>
   <tr> 
   <td> <span class="uicontrol">WdbcKillSessionPolicy</span> <br /> </td> 
   <td>次の潜在的な値に従って、すべてのワークフローと PostgreSQL データベースクエリに対して無条件停止の動作をさせることができます。<ul>
    <li><p>0 — デフォルト：ワークフロープロセスを停止し、データベースに影響を与えません。<p></li>
    <li><p>1 - pg_cancel_backend：ワークフロープロセスを停止し、データベース内のクエリをキャンセルします<p></li>
    <li><p>2 - pg_terminate_backend：ワークフロープロセスを停止し、データベース内のクエリを終了します<p></li></ul></td> 
  </tr>  
    <tr> 
   <td> <span class="uicontrol">WdbcOptions_TableSpaceUser</span> <br /> </td> 
   <td> Adobe Campaign Ootb テーブルのデータを格納するテーブル領域の名前。<br />詳しくは、 <a href="../../installation/using/creating-and-configuring-the-database.md">データベースの作成と設定</a>.</td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">WdbcOptions_TableSpaceIndex</span> <br /> </td> 
   <td> Adobe Campaign Ootb テーブルのインデックスを格納するテーブル領域の名前。<br />詳しくは、 <a href="../../installation/using/creating-and-configuring-the-database.md">データベースの作成と設定</a>.</td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">WdbcOptions_TableSpaceWork</span> <br /> </td> 
   <td> Adobe Campaign 作業用テーブルのデータを格納するテーブル領域の名前.<br />詳しくは、 <a href="../../installation/using/creating-and-configuring-the-database.md">データベースの作成と設定</a>.</td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">WdbcOptions_TableSpaceWorkIndex</span> <br /> </td> 
   <td> Adobe Campaign 作業用テーブルのインデックスを含むテーブル領域の名前.<br />詳しくは、 <a href="../../installation/using/creating-and-configuring-the-database.md">データベースの作成と設定</a>.</td> 
  </tr> 
    <tr> 
   <td> <span class="uicontrol">WdbcOptions_TempDbName</span> <br /> </td> 
   <td> Microsoft SQL Server 上の作業用テーブルに対して別のデータベースを設定し、バックアップとレプリケーションを最適化できます。 このオプションは、一時データベースの名前に対応します。指定した場合、作業用テーブルがこのデータベースに書き込まれます。 例： 'tempdb.dbo.' （名前の末尾はドットにする必要があります）。 <a href="../../production/using/rdbms-specific-recommendations.md#microsoft-sql-server">詳細情報</a> <br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">WdbcTimeZone</span> <br /> </td> 
   <td> Adobe Campaignインスタンスのタイムゾーン。 詳しくは、 <a href="../../installation/using/time-zone-management.md#configuration" target="_blank">設定</a>.<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">WdbcUseNChar</span> <br /> </td> 
   <td> データベースの文字列フィールドは NChar で定義されていますか？<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">WdbcUseTimeStampWithTZ</span> <br /> </td> 
   <td> データベースの「datetime」フィールドにタイムゾーン情報が格納されますか。<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">XtkDatabaseId</span> <br /> </td> 
   <td> データベースの ID。 Unicode DataBase の場合は、「u」で始まります。<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">XtkInstancePrefix</span> <br /> </td> 
   <td> 自動生成された内部名に追加されるプレフィックス.<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">XtkQuery_Schema_LineCount</span> <br /> </td> 
   <td> 結果の最大数は、xtk:schema および xtk:srcSchema のクエリによって返されます。<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">XtkSequence_AutoGeneration</span> <br /> </td> 
   <td> autopk="true"を使用し、属性"pkSequence"を使用しない、今後作成されたすべてのカスタマイズ済みスキーマは、自動生成されたシーケンス"auto_ 
    &lt;schemanamespace&gt; 
     &lt;schemaname&gt;
       _seq 
   </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">NlMigration_KeepFolderStructure</span> <br /> </td> 
   <td> 移行中、ツリー構造は新しいバージョン標準に基づいて自動的に再編成されます。<br /> このオプションを使用すると、ナビゲーションツリーの自動移行を無効にできます。 これを使用する場合、移行後に古いフォルダーを削除する必要があります。新しいフォルダーを追加し、必要なチェックをすべて実行します。<br /> 
    <ul> 
     <li> <p> <span class="uicontrol">データタイプ：</span> 整数</p> </li> 
     <li> <p> <span class="uicontrol">値（テキスト）</span> : 1 </p> </li> 
    </ul> このオプションは、標準のナビゲーションツリーに対して多くの変更が加えられている場合にのみ使用してください。<br /> 詳しくは、 <a href="../../migration/using/configuring-your-platform.md#specific-configurations-in-v5-11">この節</a>.<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">NmsLastErrorStatCoalesce</span> <br /> </td> 
   <td> の最終処理日 <span class="uicontrol">NmsEmailErrorStat</span> テーブルのクリーンアップ。<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">PostUpgradeLastError</span> <br /> </td> 
   <td> 以下の構文に従う、ポストアップグレードで発生したエラーに関する情報です。<br /> <strong>{ ビルド番号 }:{mode: pre/post/..}:{ エラーが発生した「lessThan」/「greaterOrEquelThan」+サブステップ }</strong> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">XtkCleanup_NoStats</span> <br /> </td> 
   <td> 「1」の値を入力して、クリーンアップワークフローを通じて統計の更新が実行されないようにします。<br /> </td> 
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
   <td> Adobe Campaignで使用できるAEMリソースのタイプ。 値はコンマで区切る必要があります。<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">nmsPipeline_config</span> <br /> </td> 
   <td> Experience Cloudトリガー データタイプは「長いテキスト」で、JSON 形式である必要があります。 詳しくは、 <a class="anchorLink" href="https://helpx.adobe.com/campaign/kb/triggers-and-campaign.html#PipelineoptionNmsPipelineConfig" target="_blank">Adobe Campaign ClassicでのExperience Cloudトリガーの使用方法</a>.<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">LASTIMPORT_&lt;%=instance.internalName%&gt;_&lt;%=activityName%&gt;</span> <br /> </td> 
   <td> このオプションは、CRM コネクタを通じてサードパーティのシステムからデータをインポートする際に使用します。 「 」オプションを有効にすると、最後のインポート以降に変更されたオブジェクトのみを収集できます。 このオプションは、手動で作成し、以下のように設定する必要があります。 
    <ul> 
     <li> <p> <span class="uicontrol">内部名</span> : LASTIMPORT_&lt;%=instance.internalName%&gt;_&lt;%=activityName%&gt;</p> </li> 
     <li> <p> <span class="uicontrol">値（フィールド）</span> ：最後のインポートの日付 (yyyy/MM/dd hh):mm:ss 形式。 </p> </li> 
    </ul><br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">TNT_EdgeServer</span> <br /> </td> 
   <td> 統合に使用される Adobe Target サーバー。このオプションは、デフォルトで選択されています。この値は Adobe Target のドメインサーバーに対応し、値 /m2 が続きます。例：tt.omtrdc.net/m2。<br /> 詳しくは、 <a href="../../integrations/using/configuring-the-integration-with-adobe-target.md">この節</a>.<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">TNT_TenantName</span> <br /> </td> 
   <td> Adobe Target 組織名。この値は Adobe Target のクライアント名に対応します。<br /> 詳しくは、 <a href="../../integrations/using/configuring-the-integration-with-adobe-target.md">この節</a>.<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">AAM_DataSourceId</span> <br /> </td> 
   <td> Adobe Audience Managerとの統合に使用するオプション。<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">AAM_DestinationId</span> <br /> </td> 
   <td> Adobe Audience Managerとの統合に使用するオプション。<br /> </td> 
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
   <td> SQL トランザクションごとに更新されるクーポンの数。<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">NmsInteraction_LastPropositionSynchControl_</span> <br /> </td> 
   <td> '+ [proposition's schema] + "_" + extAccountSource。@executionInstanceId + [proposition's schema] + "_" + vars.executionInstanceIdFilter<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">NmsInteraction_LastPropositionSynchExec_</span> <br /> </td> 
   <td> '+ [ 提案のスキーマ ] + "_" + extAccountSource。@executionInstanceId + "_" + extAccountTarget。@executionInstanceId<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">NmsInteraction_SynchWorkflowIds</span> <br /> </td> 
   <td> 同期ワークフローのトラッキング。<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">NmsInteraction_UseDaemon</span> <br /> </td> 
   <td> 非同期提案の書き込みを有効化/無効化します（無効にするには「0」、有効にするには「1」）。<br /> </td> 
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
   <td> 前回のアップグレード前の AC インスタンスのビルド番号。<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">NmsServer_URL</span> <br /> </td> 
   <td> パブリック Web アプリケーションサーバーのベース URL.<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">XtkPassUnknownSQLFunctionsToRDBMS</span> <br /> </td> 
   <td> 移行後も、古い宣言されていない SQL 関数を引き続き使用できます。 セキュリティ上のリスクがあるので、このオプションは使用しないことを強くお勧めします。<br /> </td> 
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
   <td> トラッキングを有効化するためのオプション。<br /> </td> 
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
   <td> トラッキングサーバーでインスタンス名を定義できます。<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">NmsTracking_LastConsolidation</span> <br /> </td> 
   <td> 前回、トラッキング情報が新しいデータと統合された時点。<br /> </td> 
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
   <td> ポインターは、ID と日付を通じて処理された最後のメッセージイベントを追跡します。<br /> </td> 
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
   <td> オプション 1 を選択した場合は、2 番目の手順で、インターフェイスで手動で削除を確定する必要があります。 そうしないと、データは確認なしで削除されます。<br /> </td> 
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
   <td> 値を 1 に設定すると、詳細フォームにスクロールバーを追加できます。<br /> </td> 
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
