---
title: Adobe Campaignクラシックデータモデルの説明
description: このドキュメントでは、Adobe Campaignクラシックデータモデルについて説明します。
page-status-flag: never-activated
uuid: faddde15-59a1-4d2c-8303-5b3e470a0c51
contentOwner: sauviat
products: SG_CAMPAIGN/CLASSIC
audience: configuration
content-type: reference
topic-tags: schema-reference
discoiquuid: 5957b39e-c2c6-40a2-b81a-656e9ff7989c
index: y
internal: n
snippet: y
translation-type: tm+mt
source-git-commit: 15581517df8d2f397285bbadebd83b7f4539dfd7
workflow-type: tm+mt
source-wordcount: '2380'
ht-degree: 1%

---


# キャンペーンデータモデルの説明{#data-model-description}

Adobe Campaignには、事前定義済みのデータモデルが付属しています。 この節では、Adobe Campaignデータモデルの組み込みの表とその操作について詳しく説明します。

各テーブルの説明にアクセスするには、 **[!UICONTROL 管理者/設定/データスキーマ]**&#x200B;に移動し、リストからリソースを選択して、「 **[!UICONTROL ドキュメント]** 」タブをクリックします。

![](assets/data-model_documentation-tab.png)

>[!NOTE]
>
>アプリケーションに格納されるデータの物理的および論理的構造は、XML で記述されます。スキーマと呼ばれる Adobe Campaign 特有の文法に従います。For more on Adobe Campaign schemas, read out [this section](../../configuration/using/about-schema-reference.md).

## メインテーブルの説明 {#description-main-tables}

Adobe Campaignは、相互にリンクされたテーブルを含むリレーショナルデータベースに依存しています。

次の図に、Adobe Campaignデータモデルのメインビジネステーブルと各データのメインフィールドとの結合を示します。

<!--![](assets/data-model_diagram.png)-->

![](assets/data-model_simplified-diagram.png)

事前定義済みのAdobe Campaignデータモデルには、次に示す主なテーブルが含まれます。

### NmsRecipient {#NmsRecipient}

このテーブルは、 **nms:受信者** スキーマと一致します。

これは、配信の **受信者に使用されるデフォルトのテーブルです**。 その結果、様々なチャネルを介した配信に必要な情報が含まれます。

* sEmail: 電子メールアドレス。
* iEmailFormat: 電子メールに適した形式（テキストには1、HTMLには2、未定義の場合は0）。
* 住所1、sAddress2、sAddress3、sAddress4、sZipCode、sCityを使用して、住所を作成します（1997年5月のXPZ 10-011 AFNOR標準に準拠）。
* sPhone、sMobilePhone、sFaxには、それぞれ電話番号、携帯電話番号、FAX番号が含まれます。
* iBlackListは、プロファイルに使用されるデフォルトのオプトアウトフラグです（1は「登録解除」、0はそれ以外）。

iFolderIdフィールドは、受信者を実行フォルダーにリンクする外部キーです。 For more on this, see [XtkFolder](#XtkFolder).

sCountryCodeフィールドは、受信者に関連付けられた国の3166-1アルファ2 ISOコード（2文字）です。 このフィールドは、実際には国参照テーブル(NmsCountry)の外部キーで、国ラベルとその他の国コードデータが含まれます。 国が入力されていない場合は、値「XX」が保存されます（IDがゼロのレコードの代わりに使用されます）。

受信者表の詳細については、 [この節を参照してください](../../configuration/using/about-data-model.md#default-recipient-table)。

### NmsGroup {#NmsGroup}

このテーブルは、 **nms:group** スキーマと一致します。

これにより、受信者の **統計的なグループを作成でき**&#x200B;ます。 受信者とグループには多対多の関係がある。 例えば、1人の受信者が複数のグループに属し、1つのグループに複数の受信者を含めることができます。 読み込みまたは配信のターゲット設定を使用して、手動でグループを作成できます。 グループは多くの場合、配信ターゲットとして使用されます。 sNameグループの内部名を表す一意のインデックスがフィールドに存在します。 グループがフォルダーにリンクされている(キーはiFolderIdです。 For more on this, see [XtkFolder](#XtkFolder)).

### NmsRcpGrpRel {#NmsRcpGrpRel}

NmsRcpGrpRel関係テーブルには、iRecipientIdとiGroupIdのリンクテーブルの識別子に対応する2つのフィールドのみが含まれます。

### NmsService {#NmsService}

この表は、 **nms:service** スキーマと一致します。

Adobe Campaignでは、情報サービス（トピック）への購読を作成および管理できます。 NmsServiceテーブルには、受信者が購読するオファー（ニュースレターなど）の情報サービス（トピック）の定義が格納されます。

サービスは、情報が循環し、フォームを介した購読や購読解除の管理が容易になる点を除いて、グループ(静的な受信者グループ)に似たエンティティです。

sNameサービスの内部名を表すフィールドには一意のインデックスがあります。 サービスがフォルダーにリンクされている(キーはiFolderId。 For more on this, see [XtkFolder](#XtkFolder)). 最後に、iTypeフィールドで、このサービスの配信チャネルを指定します（電子メールの場合は0、SMSの場合は1、電話の場合は2、ダイレクトメールの場合は3、FAXの場合は4）。

### NmsSubscription {#NmsSubscription}

このテーブルは、 **nms:購読** スキーマと一致します。

これにより、情報サービスに対する受信者購読を管理できます。

### NmsSubHisto {#NmsSubHisto}

このテーブルは、 **nms:subHisto** スキーマと一致します。

購読がWebフォームまたはアプリケーションのインターフェイスを使用して管理されている場合、すべてのサブスクリプションと購読解除がNmsSubHistoテーブルに履歴化されます。 iActionフィールドは、tsDateフィールドに格納された日付に対して実行されるアクション(購読解除の場合は0、購読の場合は1)を指定します。

### NmsDelivery {#NmsDelivery}

このテーブルは、 **nms:配信** スキーマと一致します。

このテーブルの各レコードは、 **配信アクション** 、または **配信テンプレートを表します**。 配信(ターゲット、コンテンツなど)を実行するために必要なすべてのパラメーターが含まれます。 配信（ブロードキャスト）ログ(NmsBroadLog)および関連するトラッキングURL(NmsTrackingUrl)は、分析段階で作成されます（これらの両方の表の詳細については、以下を参照）。

sInternalName配信またはシナリオの内部名を表すフィールドに一意のインデックスがあります。 配信は実行フォルダーにリンクされています（外部キーはiFolderProcessIdです）。 For more on this, see [XtkFolder](#XtkFolder)).

### XtkFolder {#XtkFolder}

コンソールの「 **ナビゲーション** 」タブに表示されるツリー内の **** すべてのフォルダが含まれます。

フォルダーは次のように入力します。 sModelフィールドの値は、フォルダーに含めることができるデータのタイプを指定します。 また、このフィールドを使用すると、クライアントコンソールで、対応するフォームと共にデータを正しく表示できます。 このフィールドに指定できる値は、navTreeで定義されます。

ツリーは、iParentIdフィールドとiChildCountフィールドで管理されます。 sFullNameフィールドは、ツリー内のフォルダのフルパスを指定します。 最後に、sNameフォルダーの内部名を表すフィールドに一意のインデックスがあります。

## 配信と追跡 {#delivery-and-tracking}

この一連のテーブルは **配信** ・モジュールにリンクされているため、配信を監視したり、メッセージの送信時に発生する最終的な問題を監視できます。 For more on this, see [Monitoring deliveries](../../delivery/using/monitoring-a-delivery.md). 追跡について詳しくは、「 [メッセージの追跡](../../delivery/using/about-message-tracking.md)」を参照してください。

![](assets/data-model_delivery.png)

**NmsBroadLogMsg**: このテーブルは、 **nms:broadLogMsg** スキーマと一致します。 配信ログテーブルの拡張です。

## Campaign management {#campaign-management}

この表は、 **マーケティングキャンペーン** ・モジュールにリンクされています。このモジュールを使用して、コミュニケーションとマーケティング・キャンペーンを定義、最適化、実行、分析できます。 For more on this, see [About marketing campaigns](../../campaign/using/designing-marketing-campaigns.md).

![](assets/data-model_campaign.png)

* **NmsOperation**: このテーブルは、 **nms:operation** スキーマと一致します。 マーケティングキャンペーンのデータが含まれます。
* **NmsDeliveryOutline**: このテーブルは、 **nms:deliveryOutline** スキーマと一致します。 配信(配信の概要)の拡張プロパティが含まれます。
* **NmsDlvOutlineItem**: 次の表は、 **nms:dlvOutlineItem** スキーマと一致します。 配信の概要の記事が含まれます。
* **NmsDeliveryCustomization**: このテーブルは、 **nms:deliveryCustomization** スキーマと一致します。 配信のパーソナライゼーションフィールドが含まれます。
* **NmsBudget**: このテーブルは、 **nms:budget** スキーマと一致します。 キャンペーン、計画、プログラム、タスク、配信に関する予算のデータが含まれます。
* **NmsDocument**: このテーブルは、 **nms:ドキュメント** スキーマと一致します。 キャンペーンのマーケティングドキュメントがファイル（画像、Excelファイル、Wordファイルなど）の形式で含まれます。
* **XtkWorkflow**: 次の表は、 **xtk:workflow** スキーマと一致します。 キャンペーンのターゲット設定が含まれます。
* **NmsTask**: このテーブルは、 **nms:タスク** スキーマと一致します。 マーケティングタスクの定義が含まれます。
* **NmsAsset**: このテーブルは、 **nms:asset** スキーマと一致します。 マーケティングリソースの定義が含まれます。

## 通信の一貫性 {#communication-consistency}

この一連のテーブルは **キャンペーンの最適化** ・モジュールにリンクされており、配信の送信を制御、フィルタリング、監視できます。 For more on this, see [About campaign typologies](../../campaign/using/about-campaign-typologies.md).

![](assets/data-model_typology.png)

* **NmsTypologyRule**: 次の表は、 **nms:typologyRule** スキーマと一致します。 タイポロジに応じた配信に適用されるルールが含まれます。
* **NmsTypology**: 次の表は、 **nms:typology** スキーマと一致します。 タイポロジに一致する配信に適用される一連のルールが含まれます。
* **NmsTypologyRuleRel**: このテーブルは、 **nms:typologyRuleRel** スキーマと一致します。 類型とそのルールの関係が含まれます。
* **NmsVolumeLine**: このテーブルは、 **nms:volumeLine** スキーマと一致します。 キャパシティ・ルールの可用性ラインのセットが含まれます。
* **NmsVolumeConsumed**: この表は、 **nms:volumeConsumed** スキーマと一致します。 キャパシティ・ルールのすべての消費ラインが含まれます。

## 応答管理 {#response-management}

この一連のテーブルは **Response Manager** ・モジュールにリンクされており、これにより、すべての通信チャネルに対するマーケティング・キャンペーンまたはオファーの提案の成功と収益性を測定できます。 For more on this, see [About response manager](../../campaign/using/about-response-manager.md).

![](assets/data-model_response.png)

### NmsRemaPeascim {#NmsRemaHypothesis}

このテーブルは、 **nms:remaPerasom** スキーマと一致します。 測定仮説の定義が含まれます。

この表には、次のような重要な情報がXMLに保存されています。

**実行コンテキスト（XMLに保存される情報）**

実行コンテキストにより、測定の計算に考慮されるテーブルとフィールド、すなわち次の項目が設定されます。
* nms:remaMatchRcpリアクションログストレージスキーマ。
* トランザクションテーブルスキーマ（購入など）。
* クエリースキーマ。仮説条件の開始テーブルを定義できます。
* 個人に対するリンク。クエリスキーマに基づいて個人を識別できます。
* 取引日。 このフィールドは必須ではありませんが、計算の枠を制限するために使用することをお勧めします。
* 取引金額： これは、売上高指標を自動的に計算するためのオプションのフィールドです。

**仮説の境界線（XMLに保存された情報）**

仮説境界は、クエリスキーマのテーブルに基づく仮説のフィルタリングで構成されます。

**仮説オーバーロードスクリプト（XMLに格納された情報）**

仮説オーバーロードスクリプトは、実行中に仮説のコンテンツをオーバーロードできるJavaScriptコードです。

**測定指標**

次のインジケーターは、仮説の実行中に自動的に更新されます。

* 反応数： **iTransaction**。 反応ログテーブル内の行数。
* 連絡数： **iContactReacoded**. 仮説内のターゲットとなる連絡先の個別数。
* コントロール母集団数： **iProofReacoded**. 仮説内のターゲットコントロール母集団連絡先の個別数。
* 連絡回答率： **dContactRecoledRate**. 仮説内のターゲットの連絡先の回答率です。
* Response rate of the control group: **dProofReactedRate**. 仮説コントロール母集団の回答率。
* Total revenue of population contacted: **dContactReactedTotalAmount**. 仮説内のターゲットとなる連絡先の総売上高。
* Average revenue of control group: **dContactReactedAvgAmount**. 仮説内のターゲットコントロール母集団の連絡先の平均売上高。
* Total revenue of the control group: **dProofReactedTotalAmount**. 仮説コントロール母集団の合計売上高.
* Average revenue of control group: **dProofReactedAvgAmount**. 仮説コントロール母集団の平均売上高。
* Total margin per contact: **dContactReactedTotalMargin**. 仮説のコンタクト先あたりの合計マージン.
* Average margin per contact: **dContactReactedAvgMargin**. 仮説内でターゲット設定された、連絡先あたりの平均利益。
* Total margin of control group: **dProofReactedTotalMargin**. 仮説内でターゲット設定されたコントロール母集団の合計マージン。
* Average margin of control group: **dProofReactedAvgMargin**. 仮説でターゲット設定されたコントロール母集団の平均利益。
* 追加の売上高： **AdditionalAmount**. (連絡先の平均売上高 —コントロール母集団の平均売上高) *連絡先の数。
* 追加の余白： **AdditionalMargin**. (平均連絡利益率 —コントロール母集団の平均利益率) /連絡数。
* 連絡先あたりの平均コスト(SQL式)。 配信のコスト/連絡数を計算しました。
* ROI (SQL式) 配信のコスト/連絡の合計利益率が計算されました。
* 効果的なROI (SQL式) 計算された配信のコスト/追加利益。
* 有意性： **重要** (SQL式) キャンペーンの有意性に応じて、0 ～ 3の値が含まれます。

### NmsRemaMatchRcp {#NmsRemaMatchRcp}

このテーブルは、 **nms:remaMatchRcp** スキーマと一致します。

特定の仮説に対する個人の反応を表すレコードが含まれます。 これらのレコードは仮説の実行中に作成されました。

## シミュレーションと配信 {#simulation-and-delivery}

この一連のテーブルは **シミュレーション** ・モジュールにリンクされています。これにより、提案を受信者に送信する前に、カテゴリまたは環境に属するオファーの分布をテストできます。 For more on this, see [About offers simulation](../../interaction/using/about-offers-simulation.md).

![](assets/data-model_simulation.png)

* **NmsSimulation**: このテーブルは、 **nms:シミュレーション** スキーマと一致します。 特定の母集団に対する一連の配信またはオファーのシミュレーションを表します。
* **NmsDlvSimulationRel**: 次の表は、 **nms:dlvSimulationRel** スキーマと一致します。 シミュレーション内で考慮される配信のリストが含まれます。 シミュレーションの範囲はXMLに保存されます。
* **NmsOfferSimulationRel**: このテーブルは、 **nms:offerSimulationRel** スキーマと一致します。 シミュレーションをオファーとリンクできます。

## 対話モジュール {#interaction-module}

この一連のテーブルは **Interaction** モジュールにリンクされており、このモジュールを使用すると、1つまたは複数の適合オファーにすることで、特定の接触との対話中にリアルタイムに応答できます。 詳しくは、インタラク [ションとオファーの管理を参照してください](../../interaction/using/interaction-and-offer-management.md)。

* **NmsOffer**: このテーブルは、 **nms:オファー** スキーマと一致します。 各マーケティングオファーの定義が含まれます。
* **NmsPropositionRcp**: この表は、 **nms:propositionRcp** スキーマと一致します。 各個人に送信されるマーケティング提案のクロスチャネルログが含まれます。 レコードは、提案が準備されたか、または個人に効果的に作成されたときに作成されます。
* **NmsOfferSpace**: このテーブルは、 **nms:offerSpace** スキーマと一致します。 提案が行われる場所の定義が含まれます。
* **NmsOfferContext**: このテーブルは、 **nms:offerContext** スキーマと一致します。 提案の適用性に関する追加の条件と、重み付けの計算式の定義が含まれます。
* **NmsOfferView**: このテーブルは、 **nms:offerView**. オファー表示域が含まれます。
* **NmsOfferCategory**: このテーブルは、 **nms:offerCategory**. オファーカテゴリが含まれます。
* **NmsOfferEnv**: このテーブルは、 **nms:offerEnv**. オファー環境が含まれます。

## Message Centerモジュール {#message-center-module}

次の表は、 **トランザクションメッセージング** (Message Center)モジュールにリンクされています。このモジュールを使用すると、ユーザーに送信され、情報システムからトリガーされたイベントから生成される個別および個別の通信を管理できます。 For more on this, see [About transactional messaging](../../message-center/using/about-transactional-messaging.md).

### NmsRtEvent {#NmsRtEvent}

![](assets/data-model_message-center_rt.png)

このテーブルは、 **nms:rtEvent** スキーマと一致します。 リアルタイムイベントの定義が含まれます。

### NmsBatchEvent {#NmsBatchEvent}

![](assets/data-model_message-center_batch.png)

このテーブルは、 **nms:batchEvent** スキーマと一致します。 バッチ別のイベントの定義が含まれます。

<!--## Microsites Module {#microsites-module}

This set of tables is linked to the **Web applications** functionality, which allows to create and publish dynamic and interactive web applications with data from the database and content adapted to the rights of the connected user. For more on this, see [About web applications](../../web/using/about-web-applications.md).

![](assets/data-model_microsites.png)

* **NmsTrackingUrl**: This table matches the **nms:trackingUrl** schema.

* **NmsPurl**: This table matches the **nms:purl** schema.-->

## NMACモジュール {#nmac-module}

この表は **モバイルアプリチャネルにリンクされています**。モバイルアプリを使用すると、アプリを介してiOS端末とAndroid端末にパーソナライズされた通知を送信できます。 詳しくは、モバイルアプリのチャネル [についてを参照してください](../../delivery/using/about-mobile-app-channel.md)。

* **NmsMobileApp**: この表は、 **nms:mobileApp** スキーマと一致します。 Adobe Campaignで定義されたモバイルアプリケーションが含まれます。
* **NmsAppSubscription**: このテーブルは、 **nms:appSubscription** スキーマと一致します。 1つ以上のアプリケーションに関するサブスクライバー情報が含まれます。
* **NmsAppSubscriptionRcp**: このテーブルは、 **nms:appSubscriptionRcp** スキーマと一致します。 このテーブルを使用すると、受信者に登録した訪問者をアプリケーションテーブルとリンクできます。
* **NmsExcludeLogAppSubRcp**: このテーブルは、 **nms:excludeLogAppSubRcp** スキーマと一致します。
* **NmsTrackingLogAppSubRcp**: この表は、 **nms:trackingLogAppSubRcp** スキーマと一致します。
* **NmsBroadLogAppSubRcp**: この表は、 **nms:broadLogAppSubRcp** スキーマと一致します。

## Social Marketing Module {#social-marketing-module}

この一連の表は、ソーシャルネットワークの **** 管理モジュールにリンクされています。このモジュールでは、FacebookやTwitterを使用して顧客や見込み客とやり取りを行うことができます。 For more on this, see [About social marketing](../../social/using/about-social-marketing.md).

![](assets/data-model_social.png)

* **NmsVisitor**: このテーブルは、 **nms:訪問者** スキーマと一致します。 訪問者に関する情報が含まれます。
* **NmsVisitorSub**: このテーブルは、 **nms:visitorSub** スキーマと一致します。 訪問者を、登録済みのサービス（TwitterまたはFacebook）にリンクできます。
* **NmsFriendShipRel**: このテーブルは、 **nms:friendshipRel** スキーマと一致します。 Facebookサービスのコンテキスト内で、訪問者を友人とリンクさせることができます。
* **NmsVisitorInterestRel**: このテーブルは、 **nms:visitorInterestRel** スキーマと一致します。 訪問者とその興味をリンクできます。
* **NmsInterest**: このテーブルは、 **nms:interest** スキーマと一致します。 各訪問者の興味のリストが含まれます。