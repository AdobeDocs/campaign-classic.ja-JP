---
product: campaign
title: Adobe Campaign Classic data model description
description: このドキュメントでは、Adobe Campaignデータモデルについて説明します。
audience: configuration
content-type: reference
topic-tags: schema-reference
exl-id: fc0fd23c-f9ea-4e30-b47b-a84143d882ca
source-git-commit: 20509f44c5b8e0827a09f44dffdf2ec9d11652a1
workflow-type: tm+mt
source-wordcount: '2379'
ht-degree: 4%

---

# Campaignデータモデルの説明{#data-model-description}

![](../../assets/v7-only.svg)

Adobe Campaign には、事前定義済みのデータモデルが付属しています。ここでは、Adobe Campaign データモデルの組み込みテーブルとそのインタラクションについて詳しく説明します。

各テーブルの記述にアクセスするには、**[!UICONTROL 管理／設定／データスキーマ]**&#x200B;に移動し、リストからリソースを選択して「**[!UICONTROL ドキュメント]**」タブをクリックします。

![](assets/data-model_documentation-tab.png)

>[!NOTE]
>
>アプリケーションに格納されるデータの物理的および論理的構造は、XML で記述されます。スキーマと呼ばれる Adobe Campaign 特有の文法に従います。Adobe Campaignスキーマについて詳しくは、[この節](../../configuration/using/about-schema-reference.md)を参照してください。

## メインテーブルの説明 {#description-main-tables}

Adobe Campaignは、互いにリンクされたテーブルを含むリレーショナルデータベースに依存します。

次の図は、Adobe Campaignデータモデルのメインビジネステーブルと各メインフィールドとの結合を示しています。

<!--![](assets/data-model_diagram.png)-->

![](assets/data-model_simplified-diagram.png)

事前定義済みのAdobe Campaignデータモデルには、次の主なテーブルが含まれています。

### NmsRecipient {#NmsRecipient}

このテーブルは、**nms:recipient**&#x200B;スキーマと一致します。

これは、配信&#x200B;**の**&#x200B;受信者に使用されるデフォルトのテーブルです。 その結果、様々なチャネルを介した配信に必要な情報が含まれます。

* sEmail:電子メールアドレス。
* iEmailFormat:電子メールの推奨される形式（テキストの場合は1、HTMLの場合は2、定義されていない場合は0）。
* sAddress1、sAddress2、sAddress3、sAddress4、sZipCode、sCityは、郵送先住所の作成に使用されます（1997年5月のXPZ 10-011 AFNOR標準に準拠）。
* sPhone、sMobilePhone、sFaxには、それぞれ電話番号、携帯電話番号、およびFAX番号が含まれます。
* iBlackListは、プロファイルに使用されるデフォルトのオプトアウトフラグです（1は「購読解除」を意味し、それ以外の場合は0を意味します）。

iFolderIdフィールドは、受信者を実行フォルダーにリンクする外部キーです。 詳しくは、[XtkFolder](#XtkFolder)を参照してください。

sCountryCodeフィールドは、受信者に関連付けられた国の3166-1 Alpha 2 ISOコード（2文字）です。 このフィールドは、実際には国参照テーブル(NmsCountry)の外部キーで、国ラベルと他の国コードデータが含まれます。 国が入力されていない場合、値「XX」が保存されます（ゼロのIDレコードの代わりに使用されます）。

 受信者テーブルの詳細については、[この節](../../configuration/using/about-data-model.md#default-recipient-table)を参照してください。

### NmsGroup {#NmsGroup}

このテーブルは、**nms:group**&#x200B;スキーマと一致します。

これにより、**受信者の統計的なグループ**&#x200B;を作成できます。 受信者とグループには多対多の関係があります。 例えば、1人の受信者が複数のグループに属し、1つのグループに複数の受信者を含めることができます。 グループは、インポートまたは配信のターゲティングを使用して、手動で作成できます。 グループは、多くの場合、配信ターゲットとして使用されます。 sNameグループの内部名を表すフィールドに一意のインデックスが存在します。 グループはフォルダーにリンクされています（キーはiFolderIdです）。 詳しくは、[XtkFolder](#XtkFolder)を参照してください。

### NmsRcpGrpRel {#NmsRcpGrpRel}

NmsRcpGrpRelリレーションシップテーブルには、iRecipientIdとiGroupIdのリンクされたテーブルの識別子に対応する2つのフィールドのみが含まれます。

### NmsService {#NmsService}

このテーブルは、**nms:service**&#x200B;スキーマと一致します。

Adobe Campaignでは、情報サービス（トピック）の購読を作成および管理できます。 NmsServiceテーブルには、受信者に購読登録を申し込む情報サービス（トピック）の定義（例えばニュースレター）が格納されます。

サービスは、グループ（静的な受信者グループ）に似たエンティティですが、循環する情報が多く、フォームを介して購読と購読解除を簡単に管理できる点が異なります。

sNameサービスの内部名を表すフィールドに一意のインデックスが存在します。 サービスはフォルダーにリンクされています（キーはiFolderIdです）。 詳しくは、[XtkFolder](#XtkFolder)を参照してください。 最後に、このサービスの配信チャネルを「iType」フィールドで指定します（Eメールの場合は0、SMSの場合は1、電話の場合は2、ダイレクトメールの場合は3、FAXの場合は4）。

### NmsSubscription {#NmsSubscription}

このテーブルは、**nms:subscription**&#x200B;スキーマと一致します。

情報サービスに対する受信者の購読を管理できます。

### NmsSubHisto {#NmsSubHisto}

このテーブルは、**nms:subHisto**&#x200B;スキーマと一致します。

購読がWebフォームまたはアプリケーションのインターフェイスを使用して管理されている場合、すべての購読と購読解除がNmsSubHistoテーブルに履歴化されます。 「 iAction 」フィールドで、「 tsDate 」フィールドに格納された日付に対して実行されるアクション（購読解除は0、購読は1）を指定します。

### NmsDelivery {#NmsDelivery}

このテーブルは、**nms:delivery**&#x200B;スキーマと一致します。

このテーブルの各レコードは、**配信アクション**&#x200B;または&#x200B;**配信テンプレート**&#x200B;を表します。 配信を実行するために必要なすべてのパラメーター（ターゲット、コンテンツなど）が含まれています。 配信（ブロードキャスト）ログ(NmsBroadLog)と関連するトラッキングURL(NmsTrackingUrl)は、分析フェーズで作成されます（これらの両方のテーブルについて詳しくは、以下を参照してください）。

sInternalName配信またはシナリオの内部名を表すフィールドに一意のインデックスがあります。 配信は実行フォルダーにリンクされます（外部キーはiFolderProcessIdです）。 詳しくは、[XtkFolder](#XtkFolder)を参照してください。

### XtkFolder {#XtkFolder}

コンソールの「**ナビゲーション**」タブに表示される、ツリー&#x200B;**内の**&#x200B;すべてのフォルダーが含まれます。

フォルダーのタイプは次のとおりです。「 sModel 」フィールドの値は、フォルダーに格納できるデータのタイプを指定します。 また、このフィールドを使用すると、クライアントコンソールで、対応するフォームと共にデータを正しく表示できます。 このフィールドで指定可能な値は、 navTreeで定義されます。

ツリーは、 iParentIdフィールドとiChildCountフィールドで管理されます。 sFullNameフィールドは、ツリー内のフォルダーのフルパスを示します。 最後に、sNameフォルダーの内部名を表すフィールドに一意のインデックスが存在します。

## 配信とトラッキング {#delivery-and-tracking}

このテーブルは&#x200B;**配信**&#x200B;モジュールにリンクされています。このモジュールを使用すると、配信と、メッセージの送信時に結果として発生する問題を監視できます。 詳しくは、[配信の監視](../../delivery/using/about-delivery-monitoring.md)を参照してください。 トラッキングについて詳しくは、[メッセージのトラッキング](../../delivery/using/about-message-tracking.md)を参照してください。

![](assets/data-model_delivery.png)

**NmsBroadLogMsg**:このテーブルは、 **nms:** broadLogMsgschemaと一致します。配信ログテーブルの拡張です。

## キャンペーン管理 {#campaign-management}

この表は、**マーケティングキャンペーン**&#x200B;モジュールにリンクされています。このモジュールを使用して、コミュニケーションおよびマーケティングキャンペーンを定義、最適化、実行および分析できます。 詳しくは、[マーケティングキャンペーンについて](../../campaign/using/designing-marketing-campaigns.md)を参照してください。

![](assets/data-model_campaign.png)

* **NmsOperation**:このテーブルは、 **nms:** operationschemaと一致します。マーケティングキャンペーンのデータが含まれます。
* **NmsDeliveryOutline**:このテーブルは、 **nms:** deliveryOutlineschemaと一致します。配信の拡張プロパティ（配信の概要）が含まれます。
* **NmsDlvOutlineItem**:次の表は、  **nms:** dlvOutlineItemsスキーマと一致します。配信の概要の記事が含まれます。
* **NmsDeliveryCustomization**:このテーブルは、 **nms:** deliveryCustomizationschemaと一致します。配信のパーソナライゼーションフィールドが含まれます。
* **NmsBudget**:次の表は、 **nms:** budgetschemaと一致します。キャンペーン、プラン、プログラム、タスク、配信に関する予算のデータが含まれます。
* **NmsDocument**:次の表は、 **nms:**  documentschemaと一致します。キャンペーンのマーケティングドキュメントが、
* **XtkWorkflow**:次の表は、「 **xtk:** workflowschema」と一致します。キャンペーンのターゲティングが含まれます。
* **NmsTask**:このテーブルは **nms:** taskschemaと一致します。マーケティングタスクの定義が含まれます。
* **NmsAsset**:このテーブルは、 **nms:** assetschemaと一致します。マーケティングリソースの定義が含まれます。

## 通信の一貫性 {#communication-consistency}

このテーブルセットは、**キャンペーンの最適化**&#x200B;モジュールにリンクされています。このモジュールを使用して、配信の送信を制御、フィルタリングおよび監視できます。 詳しくは、[キャンペーンタイポロジについて](../../campaign-opt/using/about-campaign-typologies.md)を参照してください。

![](assets/data-model_typology.png)

* **NmsTypologyRule**:次の表は、 **nms:** typologyRuleschemaと一致します。タイポロジに応じた配信に適用されるルールが含まれています。
* **NmsTypology**:次の表は、 **nms:** タイポロジスキーマと一致します。タイポロジに一致する配信に適用される一連のルールが含まれます。
* **NmsTypologyRuleRel**:この表は、nms: **typologyRuleRelschemaと一** 致します。タイポロジとそのルールの関係が含まれます。
* **NmsVolumeLine**:このテーブルは、 **nms:** volumeLineschemaと一致します。容量ルールの稼動ラインのセットが含まれます。
* **NmsVolumeConsumed**:このテーブルは、 **nms:** volumeConsumedschemaと一致します。処理能力ルールの消費ラインがすべて含まれます。

## 応答管理 {#response-management}

この表のセットは、**Response Manager**&#x200B;モジュールにリンクされています。このモジュールを使用して、マーケティングキャンペーンの成功と収益性を測定したり、すべてのコミュニケーションチャネルのオファーの提案を測定したりできます。 詳しくは、[Response manager](../../response/using/about-response-manager.md)についてを参照してください。

![](assets/data-model_response.png)

### NmsRemaHypothesis {#NmsRemaHypothesis}

このテーブルは、**nms:remaHypothesis**&#x200B;スキーマと一致します。 測定の仮説の定義が含まれます。

この表には、次のようなXMLに格納される重要な情報が含まれます。

**実行コンテキスト（XML形式で格納された情報）**

実行コンテキストによって、測定の計算に考慮するテーブルとフィールドが設定されます。つまり、
* nms:remaMatchRcp反応ログストレージスキーマ。
* トランザクションテーブルスキーマ（購入など）。
* 条件スキーマ。仮説条件の開始テーブルを定義できます。
* 個人へのリンク。クエリスキーマに基づいて個人を識別できます。
* トランザクション日。 このフィールドは必須ではありませんが、このフィールドを使用して計算の境界を制限することをお勧めします。
* トランザクション金額：売上高指標を自動的に計算するオプションのフィールドです。

**仮説ペリメーター（XML形式で格納された情報）**

仮説ペリメーターは、クエリスキーマのテーブルに基づく仮説のフィルタリングで構成されます。

**仮説オーバーロードスクリプト（XML形式で保存された情報）**

仮説オーバーロードスクリプトは、実行中に仮説の内容をオーバーロードできるJavaScriptコードです。

**測定指標**

仮説の実行中、次の指標が自動的に更新されます。

* 反応数：**iTransaction**&#x200B;です。 反応ログテーブルの行数。
* 連絡数：**iContactRecomed**. 仮説のターゲットとなる連絡先の個別数。
* コントロール母集団の数：**iProofRecoped**. 仮説に含まれるターゲットコントロール母集団のコンタクト先の数。
* 連絡回答率：**dContactRecodedRate**&#x200B;です。 仮説のターゲット連絡先の回答率。
* コントロール母集団の応答率：**dProofRecopedRate**&#x200B;です。 仮説コントロール母集団の回答率。
* コンタクト済み母集団の合計売上高：**dContactReacodedTotalAmount**。 仮説のターゲットとなる連絡先の合計売上高。
* コントロール母集団の平均売上高：**dContactReactedAvgAmount**。 仮説のターゲットコントロール母集団のコンタクト先の平均売上高。
* コントロール母集団の合計売上高：**dProofReacedTotalAmount**。 仮説コントロールグループの合計売上高.
* コントロール母集団の平均売上高：**dProofRecovedAvgAmount**。 仮説コントロール母集団の平均売上高。
* コンタクト先ごとの合計利益：**dContactReacodedTotalMargin**。 仮説のコンタクト先あたりの合計マージン.
* コンタクト先ごとの平均利益：**dContactRecodedAvgMargin**。 仮説でターゲットとしたコンタクト先ごとの平均利益。
* コントロール母集団の合計利益：**dProofReacodedTotalMargin**。 仮説でターゲットにしたコントロール母集団の合計利益。
* コントロール母集団の平均利益：**dProofRecovedAvgMargin**. 仮説でターゲットにしたコントロール母集団の平均利益。
* 追加の売上高：**dAdditionnalAmount**。 （コンタクト先の平均売上高 — コントロール母集団の平均売上高） *コンタクト先数。
* 余白：**dAdditionnalMargin**。 （コンタクト先の平均利益 — コントロール母集団の平均利益） /コンタクト先数
* コンタクト先ごとの平均コスト（SQL式）。 配信の計算されたコスト/コンタクト先数。
* ROI （SQL式） 配信の計算されたコスト/コンタクト先の合計利益。
* 効果的なROI（SQL式） 配信の計算されたコスト/追加利益。
* 重要度：**iPhanitivy** （SQL式）。 キャンペーンの重要度に応じて0 ～ 3の値が含まれます。

### NmsRemaMatchRcp {#NmsRemaMatchRcp}

このテーブルは、**nms:remaMatchRcp**&#x200B;スキーマと一致します。

特定の仮説に対する個人の反応を表すレコードが含まれます。 これらのレコードは仮説の実行中に作成されました。

## シミュレーションと配信 {#simulation-and-delivery}

このテーブルセットは、**シミュレーション**&#x200B;モジュールにリンクされています。このモジュールを使用すると、提案を受信者に送信する前に、カテゴリまたは環境に属するオファーの配分をテストできます。 詳しくは、[オファーのシミュレーション](../../interaction/using/about-offers-simulation.md)についてを参照してください。

![](assets/data-model_simulation.png)

* **NmsSimulation**:このテーブルは、 **nms:** シミュレーションスキーマと一致します。これは、特定の母集団に対する一連の配信またはオファーのシミュレーションを表します。
* **NmsDlvSimulationRel**:次の表は、  **nms:** dlvSimulationRelschemaと一致します。シミュレーションで考慮される配信のリストが含まれます。 シミュレーションの範囲はXML形式で保存されます。
* **NmsOfferSimulationRel**:この表は、 **nms:** offerSimulationRelschemaと一致します。シミュレーションをオファーにリンクできます。

## インタラクションモジュール {#interaction-module}

このテーブルセットは、**インタラクション**&#x200B;モジュールにリンクされており、1つまたは複数の適応済みオファーを作成することで、特定のコンタクト先とのインタラクション中にリアルタイムで応答できます。 詳しくは、[インタラクションとオファーの管理](../../interaction/using/interaction-and-offer-management.md)を参照してください。

* **NmsOffer**:このテーブルは、 **nms:** offerschemaと一致します。各マーケティングオファーの定義が含まれます。
* **NmsPropositionRcp**:次の表は、 **nms:** propositionRcpschemaと一致します。各個人に送信されたマーケティング提案のクロスチャネルログが含まれます。 レコードは、提案が準備された場合、または個人に対して効果的に作成された場合に作成されます。
* **NmsOfferSpace**:このテーブルは、 **nms:** offerSpaceschemaと一致します。提案がおこなわれる場所の定義が含まれます。
* **NmsOfferContext**:このテーブルは、 **nms:** offerContextschemaと一致します。提案の適用性に関する追加の基準と、重み付け計算式の定義が含まれます。
* **NmsOfferView**:このテーブルは **nms:offerView**&#x200B;と一致します。オファー表示域が含まれます。
* **NmsOfferCategory**:このテーブルは **nms:offerCategory**&#x200B;と一致します。オファーカテゴリが含まれます。
* **NmsOfferEnv**:この表は、 **nms:offerEnv**&#x200B;と一致します。オファー環境が含まれます。

## Message Centerモジュール {#message-center-module}

次の表は、**トランザクションメッセージ**(Message Center)モジュールにリンクされています。このモジュールでは、ユーザーに送信され、情報システムからトリガーされるイベントから生成される個別の通信と個別の通信を管理できます。 詳しくは、[トランザクションメッセージ](../../message-center/using/about-transactional-messaging.md)についてを参照してください。

### NmsRtEvent {#NmsRtEvent}

![](assets/data-model_message-center_rt.png)

このテーブルは、**nms:rtEvent**&#x200B;スキーマと一致します。 リアルタイムイベントの定義が含まれます。

### NmsBatchEvent {#NmsBatchEvent}

![](assets/data-model_message-center_batch.png)

このテーブルは、**nms:batchEvent**&#x200B;スキーマと一致します。 バッチ別のイベントの定義が含まれます。

<!--## Microsites Module {#microsites-module}

This set of tables is linked to the **Web applications** functionality, which allows to create and publish dynamic and interactive web applications with data from the database and content adapted to the rights of the connected user. For more on this, see [About web applications](../../web/using/about-web-applications.md).

![](assets/data-model_microsites.png)

* **NmsTrackingUrl**: This table matches the **nms:trackingUrl** schema.

* **NmsPurl**: This table matches the **nms:purl** schema.-->

## NMACモジュール {#nmac-module}

この表は、**モバイルアプリチャネル**&#x200B;にリンクされています。このチャネルを使用して、iOSおよびAndroidの端末にアプリを介してパーソナライズされた通知を送信できます。 詳しくは、[モバイルアプリチャネル](../../delivery/using/about-mobile-app-channel.md)についてを参照してください。

* **NmsMobileApp**:この表は、 **nms:** mobileAppschemaと一致します。Adobe Campaignで定義されたモバイルアプリケーションが含まれます。
* **NmsAppSubscription**:このテーブルは、 **nms:** appSubscriptionschemaと一致します。1つ以上のアプリケーションに関する購読者情報が含まれます。
* **NmsAppSubscriptionRcp**:このテーブルは、 **nms:** appSubscriptionRcpschemaと一致します。これにより、アプリを購読している訪問者を受信者テーブルにリンクできます。
* **NmsExcludeLogAppSubRcp**:このテーブルは、 **nms:** excludeLogAppSubRcpschemaと一致します。
* **NmsTrackingLogAppSubRcp**:このテーブルは、 **nms:** trackingLogAppSubRcpschemaと一致します。
* **NmsBroadLogAppSubRcp**:このテーブルは、 **nms:** broadLogAppSubRcpschemaと一致します。

## ソーシャルマーケティングモジュール {#social-marketing-module}

この表は、**ソーシャルネットワークの管理**&#x200B;モジュールにリンクされています。このモジュールを使用すると、FacebookとTwitterを介して顧客や見込み客とやり取りできます。 詳しくは、[ソーシャルマーケティングについて](../../social/using/about-social-marketing.md)を参照してください。

![](assets/data-model_social.png)

* **NmsVisitor**:次の表は、 **nms:** visitorschemaと一致します。訪問者に関する情報が含まれます。
* **NmsVisitorSub**:このテーブルは、 **nms:** visitorSubschemaと一致します。これにより、訪問者を、購読したサービス(TwitterまたはFacebook)にリンクできます。
* **NmsFriendShipRel**:このテーブルは **nms:** friendshipRelschemaと一致します。これにより、Facebookサービスのコンテキスト内で訪問者と友達をリンクさせることができます。
* **NmsVisitorInterestRel**:このテーブルは、 **nms:** visitorInterestRelschemaと一致します。これにより、訪問者とその関心をリンクさせることができます。
* **NmsInterest**:このテーブルは、 **nms:**  interestschemaと一致します。各訪問者の興味のリストが含まれます。
