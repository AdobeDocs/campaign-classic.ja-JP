---
title: Adobe Campaign Classicデータモデルの説明
description: このドキュメントでは、Adobe Campaign Classicデータモデルについて説明します。
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
source-git-commit: 707e16e9e493e175c70af606bf4568a9127cedb2

---


# キャンペーンデータモデルの説明{#data-model-description}

Adobe Campaignには、事前定義されたデータモデルが付属しています。 この節では、Adobe Campaignデータモデルの組み込みの表とそのインタラクションについて詳しく説明します。

各表の説明にアクセスするには、に進み、リソ **[!UICONTROL Admin > Configuration > Data schemas]**&#x200B;ースをリストから選択し、タブをクリック **[!UICONTROL Documentation]** します。

![](assets/data-model_documentation-tab.png)

>[!NOTE]
>
>アプリケーションに格納されるデータの物理的および論理的構造は、XML で記述されます。スキーマと呼ばれる Adobe Campaign 特有の文法に従います。For more on Adobe Campaign schemas, read out this [section](../../configuration/using/about-schema-reference.md).

## メインテーブルの説明 {#description-main-tables}

Adobe Campaignは、相互にリンクされたテーブルを含むリレーショナルデータベースに依存しています。

次の図に、Adobe Campaignデータモデルのメインビジネステーブルと各メインフィールドの結合を示します。

<!--![](assets/data-model_diagram.png)-->

![](assets/data-model_simplified-diagram.png)

事前定義のAdobe Campaignデータモデルには、次に示す主な表が含まれています。

### NmsRecipient {#NmsRecipient}

この表は、 **nms:受信者** スキーマと一致

これは、デフォルトのテーブルで、 **受信者の配信**。 その結果、様々な情報を介した配信に必要な情報が含まれます。

* sEmail:電子メールアドレス。
* iEmailFormat:電子メールの推奨される形式（テキストの場合は1、HTMLの場合は2、未定義の場合は0）。
* sAddress1、sAddress2、sAddress3、sAddress4、sZipCode、sCityは、（1997年5月のXPZ 10-011 AFNOR標準に従って）住所の作成に使用されます。
* sPhone、sMobilePhone、sFaxには、それぞれ電話番号、携帯電話番号およびFAX番号が含まれます。
* iBlackListは、プロファイルに使用されるデフォルトのオプトアウトフラグです（1は「登録解除」を意味し、0はそれ以外の場合）。

iFolderIdフィールドは、実行フォルダーに受信者をリンクする外部キーです。 For more on this, see [XtkFolder](#XtkFolder).

sCountryCodeフィールドは、受信者に関連付けられた国の3166-1アルファ2 ISOコード（2文字）です。 このフィールドは、実際には国参照テーブル(NmsCountry)の外部キーで、国ラベルと他の国コードデータが含まれています。 国が入力されていない場合は、値「XX」が保存されます（ゼロのIDレコードの代わりに使用されます）。

受信者表について詳しくは、この節を参照して [ください](../../configuration/using/about-data-model.md#default-recipient-table)。

### NmsGroup {#NmsGroup}

このテーブルは、 **nms:group** スキーマと一致します。

これにより、統計的な **受信者のグループ**。 グループとグループには多対多の関係が受信者にある。 例えば、1人の受信者が複数のグループに属し、1人のグループが複数の受信者を含む場合、 グループは、読み込みまたは配信のターゲット設定を使用して、手動で作成できます。 グループは多くの場合、配信ターゲットです。 sNameグループの内部名を表す一意のインデックスがフィールドに存在します。 グループがフォルダーにリンクされている(キーはiFolderId。 For more on this, see [XtkFolder](#XtkFolder)).

### NmsRcpGrpRel {#NmsRcpGrpRel}

NmsRcpGrpRel関係テーブルには、iRecipientIdとiGroupIdのリンクテーブルの識別子に対応する2つのフィールドのみが含まれます。

### NmsService {#NmsService}

この表は、 **nms:service** スキーマと一致

サービスとは、より多くの情報が流通し、フォームを介して購読や購読解除を簡単に管理できる点を除き、グループ(静的な受信者グループ)に似たエンティティです。

sNameサービスの内部名を表すフィールドに一意のインデックスがあります。 サービスがフォルダーにリンクされている(キーはiFolderId。 For more on this, see [XtkFolder](#XtkFolder)). 最後に、iTypeフィールドで、このサービスの配信チャネルを指定します（電子メールの場合は0、SMSの場合は1、電話の場合は2、ダイレクトメールの場合は3、FAXの場合は4）。

### NmsSubscription {#NmsSubscription}

この表は、 **nms:購読** スキーマと一致

これにより、ユーザーに対する受信者購読を管理できます。

### NmsSubHisto {#NmsSubHisto}

このテーブルは、 **nms:subHistoスキーマと一致します** 。

購読がWebフォームまたはアプリケーションのインターフェイスを使用して管理されている場合、すべての購読と購読解除がNmsSubHistoテーブルに履歴化されます。 iActionフィールドは、tsDateフィールドに格納された日付に対して実行される購読解除(購読の場合は0、アクションの場合は1)を指定します。

### NmsDelivery {#NmsDelivery}

この表は、 **nms:配信** スキーマと一致

この表の各レコードは、1つの **配信アクション** 、または **配信テンプレート**。 配信(ターゲット、コンテンツなど)を実行するために必要なすべてのパラメーターが含まれます。 配信（ブロードキャスト）ログ(NmsBroadLog)と関連する追跡URL(NmsTrackingUrl)は、分析段階で作成されます（これらの両方の表の詳細については、以下を参照）。

sInternalNameシナリオまたはシナリオの内部名を表す一意のインデックスがフィールドに配信されます。 配信は実行フォルダーにリンクされています（外部キーはiFolderProcessIdです）。 For more on this, see [XtkFolder](#XtkFolder)).

### XtkFolder {#XtkFolder}

コンソール **の「ナビゲーション」タブに表示されるツリー** 内のすべ **てのフォルダが含まれます** 。

次のフォルダーが入力されます。smodelフィールドの値は、フォルダに含めることができるデータのタイプを指定します。 また、このフィールドを使用すると、クライアントコンソールで対応するフォームと共にデータを正しく表示できます。 このフィールドに指定できる値は、navTreeで定義されます。

ツリーは、iParentIdフィールドとiChildCountフィールドで管理されます。 [sFullName]フィールドは、ツリー内のフォルダのフルパスを示します。 最後に、sNameフォルダーの内部名を表す一意のインデックスがフィールドに表示されます。

## 配信と追跡 {#delivery-and-tracking}

この一連のテーブルは **配信** ・モジュールにリンクされているので、配信やメッセージの送信時に発生する最終的な問題を監視できます。 For more on this, see [Monitoring deliveries](../../delivery/using/monitoring-a-delivery.md). 追跡について詳しくは、メッセージの追跡を参 [照してくださ](../../delivery/using/about-message-tracking.md)い。

![](assets/data-model_delivery.png)

**NmsBroadLogMsg**:このテーブルは、 **nms:broadLogMsgスキーマと一致します** 。 これは、配信ログテーブルの拡張です。

## Campaign management {#campaign-management}

この一連の表はマーケティングキャンペーンモジュ **ールにリンクされ** 、コミュニケーションやマーケティングキャンペーンを定義、最適化、実行、分析できます。 For more on this, see [About marketing campaigns](../../campaign/using/designing-marketing-campaigns.md).

![](assets/data-model_campaign.png)

* **NmsOperation**:このテーブルは、 **nms:operation** スキーマと一致 マーケティングキャンペーンのデータ。
* **NmsDeliveryOutline**:この表は、 **nms:deliveryOutlineスキーマと一致します** 。 配信(配信の概要)の拡張プロパティ。
* **NmsDlvOutlineItem**:次の表は、 **nms:dlvOutlineItemスキーマと一致します** 。 記事が含まれます。配信の概要
* **NmsDeliveryCustomization**:この表は、 **nms:deliveryCustomizationスキーマと一致します** 。 この変数には、パーソナライゼーションフィールドの配信が含まれます。
* **NmsBudget**:この表は、 **nms:budget** スキーマと一致 キャンペーン、計画、プログラム、タスク、配信の予算のデータが含まれます。
* **NmsDocument**:この表は、 **nms:ドキュメント** スキーマと一致 キャンペーンのマーケティングドキュメントがファイル（画像、Excel、Wordファイルなど）の形式で含まれます。
* **XtkWorkflow**:次の表は、 **xtk:workflow** スキーマと一致 これには、キャンペーンのターゲット設定が含まれます。
* **NmsTask**:この表は、 **nms:タスク** スキーマと一致 マーケティングタスクの定義。
* **NmsAsset**:この表は、 **nms:asset** スキーマと この変数には、定義のマーケティングリソースが含まれます。

## 通信の一貫性 {#communication-consistency}

この一連のテーブルは **キャンペーンの最適化** ・モジュールにリンクされ、配信の送信を制御、フィルタリング、監視できます。 For more on this, see [About campaign typologies](../../campaign/using/about-campaign-typologies.md).

![](assets/data-model_typology.png)

* **NmsTypologyRule**:この表は、 **nms:typologyRuleスキーマと一致します** 。 タイポロジに応じて配信に適用されるルールが含まれます。
* **NmsTypology**:この表は、 **nms:typologyのスキーマと一致します** 。 タイポロジに一致するルールに適用される配信のセットが含まれます。
* **NmsTypologyRuleRel**:この表は、 **nms:typologyRuleRelスキーマと一致します** 。 タイポロジとルールの関係が含まれます。
* **NmsVolumeLine**:このテーブルは、 **nms:volumeLineスキーマと一致します** 。 容量ルールの可用性行のセットが含まれます。
* **NmsVolumeConsumed**:この表は、 **nms:volumeConsumedスキーマと一致します** 。 容量ルールのすべての消費ラインが含まれます。

## 応答管理 {#response-management}

この一連のテーブルは **Response Manager** ・モジュールにリンクされており、すべての通信チャネルのマーケティング・キャンペーンまたはオファーの提案の成功と収益性を測定できます。 For more on this, see [About response manager](../../campaign/using/about-response-manager.md).

![](assets/data-model_response.png)

### NmsRema仮説 {#NmsRemaHypothesis}

このテーブルは、nms:rema仮説 **スキーマと一致します** 。 測定仮説の定義。

この表には、次のような重要な情報がXMLに保存されています。

**実行コンテキスト（XMLに保存される情報）**

実行コンテキストは、測定の計算に考慮されるテーブルとフィールド、すなわち次の値を設定します。
* nms:remaMatchRcp反応ログのストレージスキーマ。
* トランザクションテーブルスキーマ（購入など）。
* クエリースキーマ。これにより、開始条件の仮説表を定義できます。
* 個人へのリンク。クエリーのスキーマに基づいて個人を識別できます。
* 取引日。 このフィールドは必須ではありませんが、このフィールドを使用して計算の枠を制限することをお勧めします。
* 取引金額：これは、売上高指標を自動的に計算するオプションのフィールドです。

**仮説の周長（XMLに保存された情報）**

仮説の周長は、クエリー仮説のテーブルに基づいたスキーマのフィルタリングで構成されます。

**仮説オーバーロードスクリプト（XMLに保存された情報）**

仮説オーバーロードスクリプトは、実行中に仮説の内容をオーバーロードできるJavaScriptコードです。

**測定指標**

次のインジケーターは、仮説の実行中に自動的に更新されます。

* 反応数： **iTransaction**。 反応ログテーブルの行数。
* 連絡数： **iContactRecoled**. ターゲットとなる連絡先の個別仮説数。
* コントロール母集団数： **iProofReacod**. ターゲットコントロール母集団の連絡先の個別数。
* 連絡済み回答率： **dContactRecoledRate**。 ターゲットとなる連絡先の仮説率。
* Response rate of the control group: **dProofReactedRate**. 応答率(仮説コントロール母集団)
* Total revenue of population contacted: **dContactReactedTotalAmount**. ターゲットとなる連絡先の合計売上高が仮説内です。
* Average revenue of control group: **dContactReactedAvgAmount**. ターゲットコントロール母集団の連絡先の平均売上高。
* Total revenue of the control group: **dProofReactedTotalAmount**. 仮説コントロール母集団の合計売上高.
* Average revenue of control group: **dProofReactedAvgAmount**. 仮説コントロール母集団の平均売上高
* Total margin per contact: **dContactReactedTotalMargin**. 仮説のコンタクト先あたりの合計マージン.
* Average margin per contact: **dContactReactedAvgMargin**. 連絡先ごとの平均利益率(仮説内)。
* Total margin of control group: **dProofReactedTotalMargin**. 仮説内でターゲット設定されたコントロール母集団の合計利益。
* Average margin of control group: **dProofReactedAvgMargin**. ターゲット設定されたコントロール母集団の平均利益率です。仮説。
* 追加の売上高： **dAdditionalAmount**。 (連絡先の平均売上高 —コントロール母集団の平均売上高) *連絡先の数。
* 追加の利益幅： **AdditionalMargin**。 (連絡の平均利益率 —コントロール母集団の平均利益率)/連絡数。
* 連絡1件あたりの平均コスト(SQL式)。 計算された配信のコスト/連絡数。
* ROI (SQL式) 計算された配信のコスト/連絡の合計利益。
* 効果的なROI(SQL式) 計算された配信/追加利益幅。
* 有意性：重要 **な** (SQL式) キャンペーンの有意性に応じて0 ～ 3の値を含みます。

### NmsRemaMatchRcp {#NmsRemaMatchRcp}

この表は、 **nms:remaMatchRcpスキーマと一致します** 。

特定の仮説に対する個人の反応を表すレコードが含まれます。 これらのレコードは、仮説の実行中に作成されました。

## シミュレーションと配信 {#simulation-and-delivery}

この一連のテーブルは **シミュレーション** ・モジュールにリンクされています。これにより、提案を受信者に送信する前に、カテゴリまたは環境に属するオファーの分布をテストできます。 For more on this, see [About offers simulation](../../interaction/using/about-offers-simulation.md).

![](assets/data-model_simulation.png)

* **NmsSimulation**:この表は、 **nms:シミュレーション** スキーマと一致 特定の母集団のシミュレーションまたは配信のセットを表します。
* **NmsDlvSimulationRel**:この表は、 **nms:dlvSimulationRelスキーマと一致します** 。 この変数には、配信で考慮されるシミュレーションのリストが含まれます。 スコープはXMLで保存されます。シミュレーションのスコープはXMLで保存されます。
* **NmsOfferSimulationRel**:この表は、 **nms:offerSimulationRelスキーマと一致します** 。 これにより、シミュレーションとオファーを

## インタラクションモジュール {#interaction-module}

この一連のテーブルは **Interaction** モジュールにリンクされており、このモジュールを使用すると、1つまたは複数の適合オファーにすることで、特定の接触とのインタラクション中にリアルタイムで応答できます。 詳しくは、インタラクションと [オファー管理を参照](../../interaction/using/interaction-and-offer-management.md)。

* **NmsOffer**:この表は、 **nms:オファー** スキーマと一致 各マーケティングオファーの定義。
* **NmsPropositionRcp**:この表は、 **nms:propositionRcpのスキーマと一致します** 。 各個人に送信されるマーケティング提案のチャネル間ログが含まれます。 レコードは、提案が準備された場合、または個人に対して効果的に作成された場合に作成されます。
* **NmsOfferSpace**:この表は、 **nms:offerSpaceスキーマと一致します** 。 提案を行う場所の定義が含まれます。
* **NmsOfferContext**:この表は、 **nms:offerContextスキーマと一致します** 。 提案の適用性に関する追加の条件と、重み付けの計算式の定義が含まれます。
* **NmsOfferView**:この表は、 **nms:offerViewと一致します**。 これには、オファー表示域が含まれます。
* **NmsOfferCategory**:この表は、 **nms:offerCategoryと一致します**。 これにはオファーカテゴリが含まれます。
* **NmsOfferEnv**:この表は、 **nms:offerEnvと一致します**。 これにはオファー環境が含まれます。

## Message Centerモジュール {#message-center-module}

次の表は、 **Transactional messaging** (Message Center)モジュールにリンクされています。このモジュールを使用すると、ユーザーに送信され、情報システムからトリガーされたイベントから生成された個々の固有の通信を管理できます。 For more on this, see [About transactional messaging](../../message-center/using/about-transactional-messaging.md).

### NmsRtEvent {#NmsRtEvent}

![](assets/data-model_message-center_rt.png)

この表は、 **nms:rtEvent** スキーマ。 これには、定義が含まれています。リアルタイムイベント

### NmsBatchEvent {#NmsBatchEvent}

![](assets/data-model_message-center_batch.png)

この表は、 **nms:batchEventスキーマと一致します** 。 バッチ別のイベント定義が含まれます。

<!--## Microsites Module {#microsites-module}

This set of tables is linked to the **Web applications** functionality, which allows to create and publish dynamic and interactive web applications with data from the database and content adapted to the rights of the connected user. For more on this, see [About web applications](../../web/using/about-web-applications.md).

![](assets/data-model_microsites.png)

* **NmsTrackingUrl**: This table matches the **nms:trackingUrl** schema.

* **NmsPurl**: This table matches the **nms:purl** schema.-->

## NMACモジュール {#nmac-module}

この表はモバイルアプリチャネルにリンクされ **ているので**、アプリを介してiOSやAndroid端末にパーソナライズされた通知を送信できます。 詳しくは、モバイルアプリの [チャネル](../../delivery/using/about-mobile-app-channel.md)。

* **NmsMobileApp**:この表は、 **** nms:mobileAppのスキーマと一致します。 Adobe Campaignで定義されたモバイルアプリが含まれます。
* **NmsAppSubscription**:この表は、 **nms:appSubscriptionスキーマと一致します** 。 1つ以上のアプリケーションに関するサブスクライバー情報が含まれます。
* **NmsAppSubscriptionRcp**:この表は、 **nms:appSubscriptionRcpスキーマと一致します** 。 このテーブルを使用すると、訪問者を購読しているアプリを受信者表にリンクできます。
* **NmsExcludeLogAppSubRcp**:この表は、 **nms:excludeLogAppSubRcpスキーマと一致します** 。
* **NmsTrackingLogAppSubRcp**:この表は、 **nms:trackingLogAppSubRcpスキーマと一致します** 。
* **NmsBroadLogAppSubRcp**:次の表は、 **nms:broadLogAppSubRcpスキーマと一致します** 。

## Social Marketing Module {#social-marketing-module}

この一連の表は、ソーシャルネットワークの管理モジ **ュールにリンクされています** 。このモジュールを使用すると、FacebookやTwitterを介して顧客や見込み客とやり取りすることができます。 For more on this, see [About social marketing](../../social/using/about-social-marketing.md).

![](assets/data-model_social.png)

* **NmsVisitor**:この表は、 **nms:訪問者** スキーマと一致 これには、訪問者の情報が含まれます。
* **NmsVisitorSub**:この表は、 **nms:visitorSub** スキーマと一致 これにより、訪問者を、登録したサービス（TwitterまたはFacebook）にリンクできます。
* **NmsFriendShipRel**:このテーブルは、 **nms:friendshipRelスキーマと一致します** 。 Facebookサービスのコンテキスト内で訪問者を友人とリンクさせることができます。
* **NmsVisitorInterestRel**:このテーブルは、 **nms:visitorInterestRelスキーマと一致します** 。 これにより、ユーザーとその興味を訪問者にリンクできます。
* **NmsInterest**:このテーブルは、 **nms:interest** スキーマと一致します。 各訪問者の関心のリストが含まれます。