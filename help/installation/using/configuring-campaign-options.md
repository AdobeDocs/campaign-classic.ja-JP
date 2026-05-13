---
product: campaign
title: Campaign オプションの設定
description: Campaign オプションの設定方法について説明します
feature: Installation, Application Settings
audience: installation
content-type: reference
topic-tags: appendices
exl-id: a979cd99-afa7-4ce6-ba0f-9495089cba08
TQID: https://experienceleague.adobe.com/ZyGxEznt4l0SbCiUySGjKwJwqSUCKJ-TjwGHltVWIzE
product_v2:
  - id: dfc56824-e8b9-499e-85d4-21aedb507314
feature_v2:
  - id: b82389f8-9b5e-4083-8e3b-3cef299fb8b9
  - id: c5474392-5419-4296-9e41-f6f4ce4f6e9b
subfeature_v2:
  - id: cebd7cfa-b9fa-4d9f-a2ab-fce31f32c4a3
  - id: cfc95e9b-b035-4403-a6a9-b27a8a053a37
  - id: eff19c99-440a-4318-b319-444edc4d8d8f
topic_v2:
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
  - id: d095671a-1355-40aa-8b5f-06c33c68080b
  - id: eddd9b14-83bd-4ff4-9072-54a4a484abb7
  - id: f4e6943a-c91a-4134-a2c7-f4f20cfff2f0
source-git-commit: 4c295c0dabae8aba298390a3da2422a3fa1219f9
workflow-type: tm+mt
source-wordcount: 3901
ht-degree: 3%

---

# Campaign Classicのオプション一覧{#configuring-campaign-options}

**[!UICONTROL Administration / Platform / Options]** ノードでは、Adobe Campaign オプションを設定できます。 Campaignをインストールする際に組み込まれるものもあれば、必要に応じて手動で追加できるものもあります。 使用可能なオプションは、インスタンスにインストールされているパッケージによって異なります。


>[!CAUTION]
>
>* このページに記載されていないオプションは内部のみであり、**を変更することはできません**。
>
>* Adobe Campaign オプションの変更や更新は、エキスパートユーザーのみが実行できます。

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
   <td> 配信品質インスタンスから最後に取得したbroadLogMsgの日付。<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">Deliverability_LastBroadLogMsgSent</span> <br /> </td> 
   <td> 配信品質インスタンスに送信された最後のbroadLogMsgの日付。<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">DmRendering_cuid</span> <br /> </td> 
   <td> 配信レポートのID。 サポートに連絡してIDを取得してください。<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">DmRendering_SeedTargets</span> <br /> </td> 
   <td> インボックスレンダリングにテストアドレスを使用するスキーマのリスト。 （要素名はコンマで区切られます）例：custom_nms_recipient.<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">EMTA_BCC_ADDRESS</span> </td> 
   <td> 強化MTAが送信されたメールの生コピーを送信するBCC メールアドレス。<br /> </td> 
  </tr>
  <tr> 
   <td> <span class="uicontrol">NMS_ActivateOwnerConfirmation</span> <br /> </td> 
   <td><p> 配信のプロパティで配信を開始するために特定のオペレーターまたはオペレーターのグループが指定されている場合、配信を担当するオペレーターに送信を確認することを許可できます。</p><p> これを行うには、値として「1」を入力してオプションをアクティブにします。 このオプションを無効にするには、「0」と入力します。</p><p> すると、送信確認プロセスがデフォルトとして機能します。つまり、配信プロパティで送信用に指定されたオペレーターまたはオペレーターのグループ（または管理者）のみが、送信を確認し、実行できるようになります。 詳しくは、<a href="https://experienceleague.adobe.com/docs/campaign/automation/campaign-orchestration/marketing-campaign-deliveries.html?lang=ja#start-a-delivery" target="_blank">この節</a>を参照してください。</p> </td>

<tr> 
   <td> <span class="uicontrol">Nms_DefaultRcpSchema</span> <br /> </td> 
   <td> Adobe Campaignは、「Nms_DefaultRcpSchema」グローバル変数を使用して、デフォルトの受信者データベース （nms:recipient）と対話します。<br /> オプションの値は、外部受信者テーブルと一致するスキーマの名前に対応している必要があります。<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">NmsBilling_MainActionThreshold</span> <br /> </td> 
   <td> 支払いレポートで配信をメインの配信と見なすための最小受信者数。<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">NmsBroadcast_DefaultProvider</span> <br /> </td> 
   <td> 新しいテンプレートの既定のルーティング サービス プロバイダー。<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">NmsBroadcast_LogsPerTransac</span> <br /> </td> 
   <td> 配信準備中にbroadLogsを挿入するための最小バッチサイズ （行数）。<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">NmsBroadcast_MaxDelayPerTransac</span> <br /> </td> 
   <td> 配信準備中にbroadLogsの挿入のバッチサイズが2倍になるバッチ期間しきい値（ミリ秒数）。<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">NmsBroadcast_MidAnalyzeBatchSize</span> <br /> </td> 
   <td> ミッドソーシング配信を分析する際の配信パーツのグループ化サイズ。<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">NmsBroadcast_MsgValidityDuration</span> <br /> </td> 
   <td> 配信の既定の配信期間（秒単位）。<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">NmsBroadcast_RegexRules</span> <br /> </td> 
   <td> 配信メッセージを正規化するための正規表現。<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">NmsBroadcast_RemoveBlackList</span> <br /> </td> 
   <td> 値として「1」を入力すると、連絡を取りたくない受信者を除外できます。<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">NmsBroadcast_RemoveDuplicatesRecipients</span> <br /> </td> 
   <td> 値として「1」を入力すると、倍数を自動的に無視できます。<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">NmsDelivery_ErrorAddressMasks</span> <br /> </td> 
   <td> メッセージへの返信に使用するエラーアドレスの構文を定義できます。<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">NmsDelivery_FromAddressMasks</span> <br /> </td> 
   <td> メッセージの送信時に使用される差出人アドレスの構文を定義できます。<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">NmsDelivery_ImageServerTimeout</span> <br /> </td> 
   <td> パーソナライズされたURLからダウンロードされ、メールに添付された画像を取得する際に、サーバーから応答を取得するためのタイムアウト制限（秒単位）を定義できます。 この値を超えると、メッセージを送信できません。 デフォルト値は60秒です。<br /> </td> 
  </tr> 
 <tr> 
   <td> <span class="uicontrol">NmsDelivery_MaxDownloadedImageSize</span> <br /> </td> 
   <td> パーソナライズされたURLからダウンロードされ、メールに添付された画像に許可される最大サイズ（バイト単位）を定義できます。 デフォルト値は100,000 バイト（100 KB）です。 プルーフを送信し、画像をダウンロードして電子メールを処理する場合、画像のサイズがこの値を超えた場合、またはダウンロードの問題がある場合、配信ログにエラーが表示され、プルーフ配信が失敗します。<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">NmsDelivery_MaxRecommendedAttachments</span> <br /> </td> 
   <td> 電子メールまたはトランザクションメールテンプレートの添付ファイルの最大数を設定できます。 この値を超えると、配信分析ログまたはトランザクションメールテンプレートの公開時に警告が表示されます。 デフォルト値は1個の添付ファイルです。<br /> </td> 
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
   <td> プッシュメッセージのbroadLogMsg カウントを無効にします。<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">NmsDeliveryWizard_ShowDeliveryWeight</span> <br /> </td> 
   <td> 配信アシスタントにメッセージの重み付けを表示します。<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">NmsEmail_DefaultErrorAddr</span> <br /> </td> 
   <td> ユーザーが空のままにした場合、メール配信に使用されるインスタンスレベルのデフォルトの「エラー」電子メールアドレス。<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">NmsEmail_DefaultFromAddr</span> <br /> </td> 
   <td> ユーザーが空のままにした場合、メール配信に使用されるインスタンスレベルでのデフォルトの「差出人」電子メールアドレス。<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">NmsEmail_DefaultReplyToAddr</span> <br /> </td> 
   <td> ユーザーが空のままにした場合、メール配信に使用されるインスタンスレベルのデフォルトの「返信先」電子メールアドレス。<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">NmsEmail_ExpOrganization</span> <br /> </td> 
   <td> 顧客の共通の名前。 受信者に表示される一部の警告メッセージで使用されます。<br /> 「このメッセージは、「組織」または関連会社と連絡を取ったために受け取ります。 '組織'<br />からメッセージを受信しない </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">NmsEmail_FromName</span> <br /> </td> 
   <td> ユーザーが空のままにした場合、メール配信に使用されるインスタンスレベルでのデフォルトの「差出人」電子メールラベル。<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">NmsEmail_ReplyToName</span> <br /> </td> 
   <td> ユーザーが空のままにした場合、メール配信に使用されるインスタンスレベルのデフォルトの「返信先」電子メールラベル。<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">NmsEmail_RetryCount</span> <br /> </td> 
   <td> 電子メール メッセージの2回の再試行の間隔（秒単位）。<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">NmsEmail_RetryPeriod</span> <br /> </td> 
   <td> メールメッセージの再試行期間。<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">NmsForecast_MsgWeightFormula</span> <br /> </td> 
   <td> 暫定配信のメッセージの重み付けを計算するために使用される数式。<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">NmsInmail_AllowlistEmails</span> <br /> </td> 
   <td> 許可された転送メールアドレスのリスト（受信メール処理モジュールから）。 アドレスはコンマで区切る必要があります（またはすべてを許可するには*）。 E.g. xyz@abc.com,pqr@abc.com.<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">NmsLine_AESKey</span> <br /> </td> 
   <td> URL （LINE チャネル）をエンコードするために'lineImage' サーブレットで使用されるAES キー。<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">NmsNPAI_EmailMaxError</span> <br /> </td> 
   <td> チャネル「電子メール」（デフォルトとして使用）：受信者を強制隔離する前の送信中のソフトエラーについて、許可されるエラーの最大数。<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">NmsNPAI_EmailSignificantErrorDelay</span> <br /> </td> 
   <td> チャネル「電子メール」（デフォルトとして使用）：新しいソフトエラーを考慮に入れる前に、前回の参照元ソフトエラーから費やす最小限の期間。<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">NmsNPAI_MobileMaxError</span> <br /> </td> 
   <td> チャネル「モバイル」：受信者を強制隔離に入れる前の送信中のソフトエラーについて、受け入れられるエラーの最大数。<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">NmsNPAI_MobileSignificantErrorDelay</span> <br /> </td> 
   <td> チャネル「モバイル」：新しいソフトエラーを考慮に入れる前に、前に参照したソフトエラーから費やす最小限の期間。<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">NmsMidSourcing_LogsPeriodHour</span> <br /> </td>
   <td> 同期ワークフローが実行されるたびに回復されるブロードログの数を制限するように、最大期間（時間で表される）を指定できます。</a>.<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">NmsMidSourcing_PrepareFlow</span> <br /> </td> 
   <td> MidSourcing セッション内の最大呼び出し数。並行して実行できます（デフォルトでは3つ）。<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">NmsMTA_Alert_Delay</span> <br /> </td> 
   <td> 配信が「遅延」と見なされるまでのカスタム遅延（分単位）。デフォルトは30分です。<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">NmsOperation_DeliveryPreparationWindow</span> <br /> </td> 
   <td><p>このオプションは、実行中の配信の数をカウントする際に、<span class="uicontrol"><a href="https://experienceleague.adobe.com/docs/campaign/automation/workflows/introduction/wf-type/technical-workflows.html?lang=ja" target="_blank">operationMgt</a></span>のテクニカルワークフローで使用されます。</p>これにより、ステータスが一貫しない配信を実行中の配信の数から除外する日数を定義できます。</p><p>デフォルトでは、値は「7」に設定されています。つまり、7日を超える一貫性のない配信は除外されます。</p></td> 
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
   <td> ミラーページ サーバーのURL （既定では、NmsTracking_ServerUrlと同じである必要があります）。<br /> URLがルーティング定義で指定されていない場合、これはメール配信のデフォルト値です。<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">NmsSMS_Priority</span> <br /> </td> 
   <td> 送信されたSMS メッセージのパラメーター：メッセージの優先順位を示すためにSMS ゲートウェイに送信される情報。<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">NmsSMS_RetryCount</span> <br /> </td> 
   <td> SMS メッセージ送信時の再試行回数。<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">NmsSMS_RetryPeriod</span> <br /> </td> 
   <td> SMS メッセージの再試行が実行される期間。<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">NmsUserAgentStats_LastConsolidation</span> <br /> </td> 
   <td> <span class="uicontrol">NmsUserAgent</span>統計の最終統合日。<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">NmsWebSegments_LastStates</span> <br /> </td> 
   <td> Web セグメントとその状態を含むオプションの名前。<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">XtkBarcode_SpecialChar</span> <br /> </td> 
   <td> Code128の特殊文字のサポートを有効/無効にします。<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">XtkEmail_Characters</span> <br /> </td> 
   <td> 電子メールアドレスの有効な文字。<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">XtkSecurity_Restrict_EditXML</span> </td> 
   <td> 配信のXML コードの編集を無効にするには、このオプションを「0」値で追加します（右クリック / <span class="uicontrol">XML ソースの編集</span>または<span class="uicontrol">CTRL + F4</span> ショートカット）。<br /> </td> 
  </tr>  
 </tbody> 
</table>

<!--
<tr> 
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
   <td> Adobe Campaign クライアントコンソールでの公開用のリソースの場所。 <a href="../../delivery/using/formatting.md#image-referencing">この節</a>を参照してください。<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">NcmRessourcesDirPreview</span> <br /> </td> 
   <td> Adobe Campaign クライアントコンソールでプレビューするリソースの場所。 <a href="../../delivery/using/formatting.md#image-referencing">この節</a>を参照してください。<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">NmsDelivery_DefaultIgnoredImage</span> <br /> </td> 
   <td> アップロード中にスキップされた画像のURL マスクのリスト。<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">NmsDelivery_ImagePublishing</span> </td> 
   <td> 画像アップロードの設定。 値はnone / tracking / script / listにすることができます（オペレーターのオプション設定で上書きできます）。 </td> 
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
   <td> パブリケーションのルート フォルダー。<br /> HTMLとテキストによるコンテンツの生成について詳しくは、<a href="../../delivery/using/using-a-content-template.md">この節</a>を参照してください。<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">XtkImageUrl</span> <br /> </td> 
   <td> 配信で使用される画像を保存するサーバーを定義して、ブラウザーが画像を取得できるようにします。<br /> ビルドバージョン &lt;= 5098の場合、インスタンスにアップロードされた画像のURLを使用します。<br /> ビルド バージョンが5098を超える場合は、代わりに配信のパブリック URLまたは<span class="uicontrol">XtkFileRes_Public_URL</span> オプションのURLを使用します。<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">NmsDelivery_MediaInstance</span> <br /> </td> 
   <td> 画像のアップロード用にインスタンス名を設定できます。<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">NmsDelivery_MediaPassword</span> <br /> </td> 
   <td> 画像をアップロードするためのパスワードを設定できます。<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">NmsDelivery_MediaServers</span> <br /> </td> 
   <td> 画像のアップロード用にメディア URLを設定できます。<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">NmsBroadcast_MsgWebValidityDuration</span> <br /> </td> 
   <td> 配信のオンライン リソースの既定の有効期間（秒単位）。<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">XtkFileRes_Public_URL</span> <br /> </td> 
   <td> パブリック リソース ファイルの新しいURL。<br /> </td> 
  </tr> 
 </tbody> 
</table>

## キャンペーンとワークフロー管理 {#campaign-e-workflow-management}

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
   <td> キャンペーンの既定の有効期間（秒単位）。<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">NmsOperation_LimitConcurrency</span> <br /> </td> 
   <td> operationMgt ワークフローによって開始された、一度に処理できる配信/ワークフロー/仮説/シミュレーション ジョブの最大数。<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">NmsOperation_OperationMgtDebug</span> <br /> </td> 
   <td> <a href="https://experienceleague.adobe.com/docs/campaign/automation/workflows/introduction/wf-type/technical-workflows.html?lang=ja" target="_blank">operationMgt</a> テクニカルワークフローの実行を監視できます。 アクティブ化すると（値「1」）、実行情報がワークフロー監査ログに記録されます。<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">NmsOperation_TimeRange</span> <br /> </td> 
   <td> スケジュール モードでのターゲティング条件と抽出条件の期間。<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">Workflow_AnalysisThreshold</span> <br /> </td> 
   <td> テーブル統計が自動的に再計算されるまでに影響を受けるレコードの数。<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">XtkReport_Logo</span> <br /> </td> 
   <td> 書き出されたレポートの右上隅に表示されるロゴ。<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">NmsServer_PausedWorkflowPeriod</span> <br /> </td> 
   <td> 一時停止したワークフローのチェック間の待機日数。<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">NmsCampaign_Activate_OwnerConfirmation</span> <br /> </td> 
   <td> 値として「1」を入力して、操作の所有者による配信の検証をアクティブ化します。 このオプションを無効にするには、「0」と入力します。<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">NmsAsset_JavascriptExt</span> <br /> </td> 
   <td> ワークフローのアクティビティ「マーケティングリソース通知」に読み込む追加のJS ライブラリ。<br /> </td> 
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
   <td> （21.1.3 リリース以降） 1が選択されている場合（デフォルト値）、このオプションはビルトインスキーマのエディションを無効にします。<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">RestrictEditingOOTBJavascript</span> <br /> </td> 
   <td> （21.1.3 リリース以降） 1が選択されている場合（デフォルト値）、ビルトイン JavaScript コードのエディションは無効になります。<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">XtkAcceptOldPasswords</span> <br /> </td> 
   <td> （インストール互換モード：build&gt;6000）有効にすると（値「1」）、このオプションを使用すると、データベースに保存されている古いパスワードを外部アカウントまたはインスタンスに接続できます。<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">XtkKey</span> <br /> </td> 
   <td> このキーは、データベース内のほとんどのパスワードを暗号化するために使用されます。 （外部アカウント、LDAP パスワード…）。<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">XtkSecurity_Allow_PrivilegeEscalation</span> <br /> </td> 
   <td> 1が選択されている場合、このオプションを使用すると、JavaScriptでprivilegeEscalationを許可できます。<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">XtkSecurity_Disable_ControlsOnFileDownload</span> <br /> </td> 
   <td> 1が選択されている場合、このオプションは、（fileDownload.jspを介して）ファイルのダウンロード中にACL コントロールを無効にします。<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">XtkSecurity_Disable_JSFileSandboxing</span> <br /> </td> 
   <td> 1を選択した場合、このオプションはJavascript内のファイル サンドボックスを無効にします。<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">XtkSecurity_SaveOptions_AllowNonAdmin</span> <br /> </td> 
   <td> 'true'に設定されている場合、管理者以外のオペレーターがデプロイメントウィザードを使用してxtkOption値を更新することを許可しました。<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">XtkSecurity_Unsafe_DecryptString</span> <br /> </td> 
   <td> 1が選択されている場合、このオプションを使用すると、一部のパスワードを復号化するためにdecryptStringを使用できます。<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">XtkTraceDeleteLogin</span> <br /> </td> 
   <td> 「1」値を入力して、レコードの削除前に「変更者」フィールドを変更して、mDataの監査証跡情報を使用して要素の削除を追跡します。<br /> </td> 
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
   <td> イベントを充実させるためにパーソナライズされるJavaScriptライブラリ。 次の2つの関数の実装を含める必要があります：<br /> 
    <ul> 
     <li> <p> <span class="uicontrol">enrichRtEvents （aiEventId）;</span>：データベース内のイベントをエンリッチおよび保存します（ここで、<span class="uicontrol">aiEventId</span>は、処理されたリアルタイムイベントのテーブルに対応します）。</p> </li> 
     <li> <p> <span class="uicontrol">enrichBatchEvents （aiEventId）;</span>：データベース内のイベントをエンリッチおよび保存します（ここで、<span class="uicontrol">aiEventId</span>は、処理されたバッチイベントのID テーブルに対応します）。</p> </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">MC_LastUpdateFromBL</span> <br /> </td> 
   <td> 配信ログを介した最後のイベント ステータス更新日。<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">MC_RoutingCustomJs</span> <br /> </td> 
   <td> ルーティングイベント用にパーソナライズされるJavaScriptライブラリ。 次の2つの関数の実装を含める必要があります：<br /> 
    <ul> 
     <li> <p> <span class="uicontrol">dispatchRtEvent （iEventId）;</span>：リアルタイムイベントを処理するために選択されたトランザクションメッセージの内部名を返します（ここで、<span class="uicontrol">iEventId</span>は、処理されたリアルタイムイベントのIDに対応します）。</p> </li> 
     <li> <p> <span class="uicontrol">dispatchBatchEvent （iEventId）;</span>：バッチイベントを処理するために選択されたトランザクションメッセージの内部名を返します（ここで、<span class="uicontrol">iEventId</span>は、処理されたバッチイベントのIDに対応します）。</p> </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">MC_RtEventAvgDeliveryTimeAlert</span> <br /> </td> 
   <td> リアルタイム イベントの平均送信時間のアラートしきい値。<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">MC_RtEventAvgDeliveryTimeWarning</span> <br /> </td> 
   <td> リアルタイム イベントの平均送信時間の警告しきい値。<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">MC_RtEventAvgProcessTimeAlert</span> <br /> </td> 
   <td> リアルタイム イベントの平均処理時間に対するアラートのしきい値。<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">MC_RtEventAvgProcessTimeWarning</span> <br /> </td> 
   <td> リアルタイム イベントの平均処理時間の警告しきい値。<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">MC_RtEventAvgQueueAlert</span> <br /> </td> 
   <td> キューに入れられたリアルタイム イベントの平均数のアラートしきい値。<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">MC_RtEventAvgQueueTimeAlert</span> <br /> </td> 
   <td> リアルタイム イベントの平均キュー時間のアラートしきい値。<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">MC_RtEventAvgQueueTimeWarning</span> <br /> </td> 
   <td> リアルタイム イベントの平均キュー時間の警告しきい値。<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">MC_RtEventAvgQueueWarning</span> <br /> </td> 
   <td> キューに入れられたリアルタイム イベントの平均数の警告しきい値。<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">MC_RtEventErrorAlert</span> <br /> </td> 
   <td> リアルタイムイベントの処理エラーに対するアラートしきい値。<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">MC_RtEventErrorWarning</span> <br /> </td> 
   <td> リアルタイムイベントの処理エラーに対する警告しきい値。<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">MC_RtEventMaxQueueAlert</span> <br /> </td> 
   <td> キューに入れられたリアルタイム イベントの最大数に対するアラートしきい値。<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">MC_RtEventMaxQueueWarning</span> <br /> </td> 
   <td> キューに入れられたリアルタイム イベントの最大数に対する警告しきい値。<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">MC_RtEventMinQueueAlert</span> <br /> </td> 
   <td> キューに追加されたリアルタイム イベントの最小数に関するアラートしきい値。<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">MC_RtEventMinQueueWarning</span> <br /> </td> 
   <td> キューに追加されたリアルタイム イベントの最小数に対する警告しきい値。<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">MC_RtEventQueueAlert</span> <br /> </td> 
   <td> 保留中のリアルタイム イベントのキューのクリティカルな条件の前のしきい値。<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">MC_RtEventQueueWarning</span> <br /> </td> 
   <td> 保留中のリアルタイム イベントのキューに対する警告の前のしきい値。<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">MC_RtEventThroughputAlert</span> <br /> </td> 
   <td> リアルタイム イベント スループットのアラートしきい値。<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">MC_RtEventThroughputWarning</span> <br /> </td> 
   <td> リアルタイム イベント スループットの警告しきい値。<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">NmsMessageCenter_RoutingBatchSize</span> <br /> </td> 
   <td> イベント ルーティングの再グループ化のサイズ。<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">MC_LastRtEventStat</span> <br /> </td> 
   <td> RtEvent ステータスのポインターを更新します（データが取得されるまでの最終日）。<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">NmsLine_MessageCenterURL</span> <br /> </td> 
   <td> ウェルカムメッセージの送信に使用されるMessage Center サーバーのURL （LINE チャネル）。<br /> </td> 
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
   <td> クリーンアップ プロセスが最後に実行された時刻を定義します。<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">NmsCleanup_BroadLogPurgeDelay</span> <br /> </td> 
   <td> <p>ブロードログをデータベースから消去するまでの遅延を定義できます。</p><p>このオプションは、遅延がインターフェイス内で変更されると自動的に作成されます。 オプションリストから値を変更する場合は、秒単位で表す必要があります。</p><br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">NmsCleanup_EventHistoPurgeDelay</span> <br /> </td> 
   <td><p> イベント履歴がデータベースから消去されるまでの遅延を定義できます。</p><p>
   このオプションは、遅延がインターフェイス内で変更されると自動的に作成されます。 オプションリストから値を変更する場合は、秒単位で表す必要があります。</p><br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">NmsCleanup_EventPurgeDelay</span> <br /> </td> 
   <td><p> イベントがデータベースから消去されるまでの遅延を定義できます。</p><p>このオプションは、遅延がインターフェイス内で変更されると自動的に作成されます。 オプションリストから値を変更する場合は、秒単位で表す必要があります。</p><br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">NmsCleanup_EventStatPurgeDelay</span> <br /> </td> 
   <td><p> イベント統計をデータベースから消去するまでの遅延を定義できます。</p><p>このオプションは、遅延がインターフェイス内で変更されると自動的に作成されます。 オプションリストから値を変更する場合は、秒単位で表す必要があります。</p><br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">NmsCleanup_PropositionPurgeDelay</span> <br /> </td> 
   <td><p> 提案をデータベースから消去するまでの遅延時間を定義できます。</p><p> このオプションは、遅延がインターフェイス内で変更されると自動的に作成されます。 オプションリストから値を変更する場合は、秒単位で表す必要があります。</p><br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">NmsCleanup_QuarantineMailboxFull</span> <br /> </td> 
   <td> <p>強制隔離がデータベースから消去されるまでの遅延を定義できます。</p><p> このオプションは、遅延がインターフェイス内で変更されると自動的に作成されます。 オプションリストから値を変更する場合は、秒単位で表す必要があります。</p><br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">NmsCleanup_RecycledDeliveryPurgeDelay</span> <br /> </td> 
   <td> <p>リサイクルされた配信がデータベースから消去されるまでの遅延を定義できます。</p><p> このオプションは、遅延がインターフェイス内で変更されると自動的に作成されます。 オプションリストから値を変更する場合は、秒単位で表す必要があります。</p><br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">NmsCleanup_RejectsPurgeDelay</span> <br /> </td> 
   <td> <p>拒否がデータベースから消去されるまでの遅延を定義できます。</p><p>このオプションは、遅延がインターフェイス内で変更されると自動的に作成されます。 オプションリストから値を変更する場合は、秒単位で表す必要があります。</p><br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">NmsCleanup_TrackingLogPurgeDelay</span> <br /> </td> 
   <td> <p>トラッキングログをデータベースから消去するまでの遅延を定義できます。</p><p>このオプションは、遅延がインターフェイス内で変更されると自動的に作成されます。 オプションリストから値を変更する場合は、秒単位で表す必要があります。</p><br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">NmsCleanup_TrackingStatPurgeDelay</span> <br /> </td> 
   <td><p> データベースからトラッキング統計を消去するまでの遅延時間を定義します。</p><p> このオプションは、遅延がインターフェイス内で変更されると自動的に作成されます。 オプションリストから値を変更する場合は、秒単位で表す必要があります。</p><br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">NmsCleanup_VisitorPurgeDelay</span> <br /> </td> 
   <td> <p>データベースから訪問者を消去するまでの遅延を定義できます。</p><p> このオプションは、遅延がインターフェイス内で変更されると自動的に作成されます。 オプションリストから値を変更する場合は、秒単位で表す必要があります。</p><br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">NmsCleanup_WorkflowResultPurgeDelay</span> <br /> </td> 
   <td> <p>ワークフロー結果をデータベースから消去するまでの遅延を定義できます。</p><p> このオプションは、遅延がインターフェイス内で変更されると自動的に作成されます。 オプションリストから値を変更する場合は、秒単位で表す必要があります。</p><br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">WdbcCapabilities_AzureDw</span> <br /> </td> 
   <td> Azure SQL Datawarehouse コネクタのオプション。<br /> </td> 
  </tr>
   <tr> 
   <td> <span class="uicontrol">WdbcKillSessionPolicy</span> <br /> </td> 
   <td>すべてのワークフローおよびPostgreSQL データベースクエリに対して、次の潜在的な値に従って無条件停止動作に影響を与えることができます。<ul>
    <li><p>0 - デフォルト：ワークフロープロセスを停止し、データベースに影響を与えない<p></li>
    <li><p>1 - pg_cancel_backend: ワークフロー処理を停止し、データベース内のクエリをキャンセルします<p></li>
    <li><p>2 - pg_terminate_backend: ワークフロープロセスを停止し、データベース内のクエリを終了します<p></li></ul></td> 
  </tr>  
    <tr> 
   <td> <span class="uicontrol">WdbcOptions_TableSpaceUser</span> <br /> </td> 
   <td> Adobe Campaign Otb テーブルのデータを格納する表領域の名前。<br />詳しくは、<a href="../../installation/using/creating-and-configuring-the-database.md"> データベースの作成と設定</a>を参照してください。</td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">WdbcOptions_TableSpaceIndex</span> <br /> </td> 
   <td> Adobe Campaign Otb テーブルのインデックスを含めるテーブル空間の名前。<br />詳しくは、<a href="../../installation/using/creating-and-configuring-the-database.md"> データベースの作成と設定</a>を参照してください。</td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">WdbcOptions_TableSpaceWork</span> <br /> </td> 
   <td> Adobe Campaignのワークテーブルのデータを格納するテーブルスペースの名前。<br />詳しくは、<a href="../../installation/using/creating-and-configuring-the-database.md"> データベースの作成と設定</a>を参照してください。</td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">WdbcOptions_TableSpaceWorkIndex</span> <br /> </td> 
   <td> Adobe Campaignのワークテーブルのインデックスを格納するテーブルスペースの名前。<br />詳しくは、<a href="../../installation/using/creating-and-configuring-the-database.md"> データベースの作成と設定</a>を参照してください。</td> 
  </tr> 
    <tr> 
   <td> <span class="uicontrol">WdbcOptions_TempDbName</span> <br /> </td> 
   <td> バックアップとレプリケーションを最適化するために、Microsoft SQL Server上のテーブルを操作するための個別のデータベースを設定できます。 このオプションは、一時データベースの名前に対応します。作業用テーブルは、指定した場合にこのデータベースに書き込まれます。 例：'tempdb.dbo.' （名前はドットで終わる必要があります）。 <a href="../../production/using/rdbms-specific-recommendations.md#microsoft-sql-server">詳細を読む</a> <br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">WdbcTimeZone</span> <br /> </td> 
   <td> Adobe Campaign インスタンスのタイムゾーン。 <a href="../../installation/using/time-zone-management.md#configuration" target="_blank">設定</a>を参照してください。<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">WdbcUseNChar</span> <br /> </td> 
   <td> データベースの文字列フィールドはNCharで定義されていますか？<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">WdbcUseTimeStampWithTZ</span> <br /> </td> 
   <td> データベースの「datetime」フィールドにはタイムゾーン情報が格納されますか？<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">XtkDatabaseId</span> <br /> </td> 
   <td> データベースのID。 Unicode DataBaseの'u'で始まります。<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">XtkInstancePrefix</span> <br /> </td> 
   <td> 自動的に生成される内部名にプレフィックスが追加されました。<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">XtkQuery_Schema_LineCount</span> <br /> </td> 
   <td> xtk:schemaおよびxtk:srcSchemaのクエリによって返される結果の最大数。<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">XtkSequence_AutoGeneration</span> <br /> </td> 
   <td> この後にautopk="true"で作成され、属性"pkSequence"なしで作成されたすべてのカスタマイズされたスキーマは、自動生成されたシーケンス "auto_を取得します 
    &lt;schemanamespace&gt; 
     &lt;schemaname&gt;
       _seq。 
   </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">NlMigration_KeepFolderStructure</span> <br /> </td> 
   <td> 移行時に、新しいバージョン標準に基づいて、ツリー構造が自動的に再編成されます。<br /> このオプションを使用すると、ナビゲーションツリーの自動移行を無効にできます。 これを使用する場合、移行後に古いフォルダーを削除し、新しいフォルダーを追加して、必要なすべてのチェックを実行する必要があります。<br /> 
    <ul> 
     <li> <p> <span class="uicontrol"> データ型：</span>整数</p> </li> 
     <li> <p> <span class="uicontrol">値（テキスト） </span> : 1 </p> </li> 
    </ul> このオプションは、標準搭載のナビゲーションツリーが変更された回数が多すぎる場合にのみ使用してください。<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">NmsLastErrorStatCoalesce</span> <br /> </td> 
   <td> <span class="uicontrol">NmsEmailErrorStat</span> テーブル クリーンアップの最終処理日。<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">PostUpgradeLastError</span> <br /> </td> 
   <td> 以下の構文に従って、Postupgradeで発生したエラーに関する情報：<br /> <strong>{ ビルド番号}:{mode: pre/post/...}:{ エラーが発生した+ サブステップ }</strong>の「lessThan」/「greaterOrEquelThan」 </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">XtkCleanup_NoStats</span> <br /> </td> 
   <td> 統計の更新がクリーンアップワークフローを通じて実行されないように、「1」値を入力します。<br /> </td> 
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
   <td> Adobe Campaignで使用できるAEM リソースの種類。 値はコンマで区切る必要があります。<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">nmsPipeline_config</span> <br /> </td> 
   <td> トリガーを設定できます。 データタイプは「long text」で、JSON形式である必要があります。 <a class="anchorLink" href="https://helpx.adobe.com/campaign/kb/triggers-and-campaign.html#PipelineoptionNmsPipelineConfig" target="_blank">Adobe Campaign ClassicでのExperience Cloud トリガーの使用方法</a>を参照してください。<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">LASTIMPORT_&lt;%=instance.internalName%&gt;_&lt;%=activityName%&gt;</span> <br /> </td> 
   <td> このオプションは、CRM コネクタを介してサードパーティシステムからデータを読み込む場合に使用します。 このオプションを有効にすると、前回の読み込み以降に変更されたオブジェクトのみを収集できます。 このオプションは、次のように手動で作成して入力する必要があります。 
    <ul> 
     <li> <p> <span class="uicontrol">内部名</span> : LASTIMPORT_&lt;%=instance.internalName%&gt;_&lt;%=activityName%&gt;</p> </li> 
     <li> <p> <span class="uicontrol">値（フィールド） </span> :yyyy/MM/dd hh:mm:ss形式の前回のインポートの日付。 </p> </li> 
    </ul><br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">TNT_EdgeServer</span> <br /> </td> 
   <td> 統合に使用されるAdobe Target サーバー。 このオプションは、デフォルトで選択されています。 この値は、Adobe Target Domain Serverに対応し、その後に/m2という値が続きます。 例：tt.omtrdc.net/m2.<br /> <a href="../../integrations/using/configuring-the-integration-with-adobe-target.md">この節</a>を参照してください。<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">TNT_TenantName</span> <br /> </td> 
   <td> Adobe Target組織名。 この値は、Adobe Target クライアントの名前に対応します。<br /> <a href="../../integrations/using/configuring-the-integration-with-adobe-target.md">この節</a>を参照してください。<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">AAM_DataSourceId</span> <br /> </td> 
   <td> Adobe Audience Managerとの統合に使用されるオプション。<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">AAM_DestinationId</span> <br /> </td> 
   <td> Adobe Audience Managerとの統合に使用されるオプション。<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">WdbcCapabilities_Teradata</span> <br /> </td> 
   <td> Teradata コネクタのオプション。<br /> </td> 
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
   <td> '+ [提案のスキーマ ] + "_" + extAccountSource.@executionInstanceId + [提案のスキーマ ] + "_" + vars.executionInstanceIdFilter<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">NmsInteraction_LastPropositionSynchExec_</span> <br /> </td> 
   <td> '+ [ proposition's schema] + "_" + extAccountSource.@executionInstanceId + "_" + extAccountTarget.@executionInstanceId<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">NmsInteraction_SynchWorkflowIds</span> <br /> </td> 
   <td> 同期ワークフローの追跡。<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">NmsInteraction_UseDaemon</span> <br /> </td> 
   <td> 非同期の提案の書き込みを有効または無効にします（「0」を無効にする場合は「1」を有効にする場合）。<br /> </td> 
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
   <td> 実行インスタンス ID。<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">NmsServer_CustomerId</span> <br /> </td> 
   <td> 請求レポートの送信時に使用される顧客識別子。<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">NmsServer_IntranetURL</span> <br /> </td> 
   <td> アプリケーションサーバーにアクセスするための内部ベース URL。<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">NmsServer_LastPostUpgrade</span> <br /> </td> 
   <td> 最後のアップグレードの前にAC インスタンスのビルド番号を指定します。<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">NmsServer_URL</span> <br /> </td> 
   <td> パブリック Web アプリケーション サーバーのベース URL。<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">XtkPassUnknownSQLFunctionsToRDBMS</span> <br /> </td> 
   <td> 移行後も、古い未宣言のSQL関数を引き続き使用できます。 セキュリティ上のリスクがあるため、このオプションを使用しないことを強くお勧めします。<br /> </td> 
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
   <td> トラッキングを有効にするオプション。<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">NmsTracking_ClickFormula</span> <br /> </td> 
   <td> トラッキングされたURL計算スクリプト。<br /> </td> 
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
   <td> 前回、トラッキング情報が新しいデータと統合されました。<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">NmsTracking_OpenFormula</span> <br /> </td> 
   <td> URL計算スクリプトを開きます。<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">NmsTracking_Password</span> <br /> </td> 
   <td> トラッキングサーバー<br />のパスワード </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">NmsTracking_Pointer</span> <br /> </td> 
   <td> ポインターは、IDと日付を通じて処理された最後のメッセージイベントを追跡します。<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">NmsTracking_SecureServerUrl</span> <br /> </td> 
   <td> 正面追跡サーバーの安全なURL。<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">NmsTracking_ServerUrl</span> <br /> </td> 
   <td> フロント追跡サーバーのURL。<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">NmsTracking_ServerUrlList</span> <br /> </td> 
   <td> トラッキングサーバーへの接続に使用されるURLのリスト。<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">NmsTracking_UserAgentRules</span> <br /> </td> 
   <td> ブラウザー識別ルール セット。<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">NmsTracking_WebFormula</span> <br /> </td> 
   <td> Web トラッキングタグの計算に使用されるスクリプト。<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">NmsTracking_WebTrackingDelivery</span> <br /> </td> 
   <td> Web トラッキング管理用に設計された仮想配信の名前。<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">NmsTracking_WebTrackingMode</span> <br /> </td> 
   <td> Web トラッキング モードを定義できます。<br /> </td> 
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
   <td> オプション 1が選択されている場合は、2番目の手順でインターフェイスの削除を手動で確認する必要があります。 それ以外の場合は、確認せずにデータが削除されます。<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">Privacy_Request_ConfirmDeletePendingDelay</span> <br /> </td> 
   <td> 確認を削除するためのリクエスト待ち時間とリクエストのキャンセル時間の間の遅延です。<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">Privacy_Request_MaxErrorAllowed</span> <br /> </td> 
   <td> プライバシーリクエストの処理または削除時に許可されるエラーの最大数。<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">Privacy_Request_PurgeDelay</span> <br /> </td> 
   <td> リクエストがキューに作成され、リクエストデータが削除されるまでの遅延が発生しました。<br /> </td> 
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
   <td> LDAP サーバーを有効にして、ユーザーを認証し、ユーザーに承認を提供します。<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">XtkLdap_AppLogin</span> <br /> </td> 
   <td> 様々な検索のためにサーバーに接続するためのアプリケーション ログイン。<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">XtkLdap_AppPassword</span> <br /> </td> 
   <td> アプリケーションのログイン用に暗号化されたパスワード。<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">XtkLdap_AutoOperator</span> <br /> </td> 
   <td> Adobe Campaignで演算子と権限の自動作成を有効にします。<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">XtkLdap_DN</span> <br /> </td> 
   <td> ログインに基づくLDAP DNの計算式。<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">XtkLdap_DNSearch</span> <br /> </td> 
   <td> ディレクトリのDN検索を有効にします。<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">XtkLdap_DNSearchBase</span> <br /> </td> 
   <td> 検索ベース：<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">XtkLdap_DNSearchFilter</span> <br /> </td> 
   <td> DN検索フィルター。<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">XtkLdap_DNSearchScope</span> <br /> </td> 
   <td> 検索範囲：<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">XtkLdap_Mechanism</span> <br /> </td> 
   <td> LDAP サーバー（plain、md5、lds、ntlm、dpa）への接続に使用される認証タイプ。<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">XtkLdap_Rights</span> <br /> </td> 
   <td> LDAP ディレクトリからAdobe Campaignの名前付き権限への認証とグループの同期を有効にします。<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">XtkLdap_RightsAttr</span> <br /> </td> 
   <td> 承認名を含むLDAP属性。<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">XtkLdap_RightsBase</span> <br /> </td> 
   <td> 検索ベース：<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">XtkLdap_RightsFilter</span> <br /> </td> 
   <td> ユーザー認証の検索フィルター。<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">XtkLdap_RightsMask</span> <br /> </td> 
   <td> LDAP認証からAdobe Campaign権限の名前を抽出する式。<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">XtkLdap_RightsScope</span> <br /> </td> 
   <td> 検索範囲：<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">XtkLdap_Server</span> <br /> </td> 
   <td> LDAP サーバーアドレス （区切り記号として「:」を指定してポートを指定できます）。<br /> </td> 
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
   <td> 'other server （s）' モードでのweb フォームの無効化に使用するインスタンス。<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">XtkWebForm_Password</span> <br /> </td> 
   <td> 「その他のサーバー」モードでweb フォームの無効化に使用されるインスタンスのパスワード。<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">XtkWebForm_ServersMode</span> <br /> </td> 
   <td> Web フォームの無効化モードを指定できるオプションです。デフォルトではローカルで、オプションが「トラッキング」の場合はトラッキングサーバーを使用し、「その他のサーバー」オプションを含むパーソナライズされたリストを使用します。<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">XtkWebForm_ServersURL</span> <br /> </td> 
   <td> Web フォームの無効化のために連絡を取るサーバーのパーソナライズされたアドレス リスト （「他のサーバー」モード）。<br /> </td> 
  </tr> 
 </tbody> 
</table>
