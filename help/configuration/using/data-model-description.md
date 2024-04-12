---
product: campaign
title: Adobe Campaign Classic データモデルの説明
description: このドキュメントでは、Adobe Campaign データモデルについて説明します
feature: Data Model
role: Data Engineer, Developer
exl-id: fc0fd23c-f9ea-4e30-b47b-a84143d882ca
source-git-commit: b666535f7f82d1b8c2da4fbce1bc25cf8d39d187
workflow-type: tm+mt
source-wordcount: '2404'
ht-degree: 2%

---

# Campaign データモデルの説明{#data-model-description}


Adobe Campaign には、事前定義済みのデータモデルが付属しています。ここでは、Adobe Campaign データモデルのビルトインテーブルとそのインタラクションについて詳しく説明します。

各テーブルの記述にアクセスするには、**[!UICONTROL 管理／設定／データスキーマ]**&#x200B;に移動し、リストからリソースを選択して「**[!UICONTROL ドキュメント]**」タブをクリックします。

![](assets/data-model_documentation-tab.png)

>[!NOTE]
>
>アプリケーションに格納されるデータの物理的および論理的構造は、XML で記述されます。スキーマと呼ばれる Adobe Campaign 特有の文法に従います。Adobe Campaign スキーマについて詳しくは、以下を参照してください [この節](../../configuration/using/about-schema-reference.md).

## メインテーブルの説明 {#description-main-tables}

Adobe Campaignは、相互にリンクされたテーブルを含んだリレーショナルデータベースに基づいています。

次の図は、Adobe Campaign データモデルの主要なビジネステーブルと、それぞれの主要なフィールドの間の結合を示しています。

<!--![](assets/data-model_diagram.png)-->

![](assets/data-model_simplified-diagram.png)

事前定義済みのAdobe Campaign データモデルには、以下に示すメインテーブルが含まれています。

### NmsRecipient {#NmsRecipient}

このテーブルはと一致します **nms:recipient** スキーマ。

次に使用するのはデフォルトのテーブルです **配信の受信者**. その結果、様々なチャネルを介した配信に必要な情報が含まれます。

* sEmail：メールアドレス。
* iEmailFormat：メールの推奨フォーマット（テキストの場合は 1、HTMLの場合は 2、未定義の場合は 0）。
* sAddress1、sAddress2、sAddress3、sAddress4、sZipCode、sCity は、住所の作成に使用されます（1997 年 5 月の XPZ 10-011 AFNOR 標準に準拠）。
* sPhone、sMobilePhone、sFax には、それぞれ電話番号、携帯電話番号、FAX 番号が含まれています。
* iBlackList は、プロファイルに使用されるデフォルトのオプトアウトフラグです（1 は「購読解除」を意味し、それ以外は 0 を意味します）。

iFolderId フィールドは、受信者を実行フォルダーにリンクする外部キーです。 詳しくは、次を参照してください [XtkFolder](#XtkFolder).

sCountryCode フィールドは、受信者に関連付けられている国の 3166-1Alpha2 の ISO コード（2 文字）です。 このフィールドは、実際には国参照テーブル（NmsCountry）の外部キーであり、国ラベルとその他の国コードデータが含まれています。 国が入力されていない場合、値「XX」が保存されます（ゼロ ID レコードの代わりに使用されます）。

受信者テーブルの詳細については、次を参照してください [この節](../../configuration/using/about-data-model.md#default-recipient-table).

### NmsGroup {#NmsGroup}

このテーブルはと一致します **nms:group** スキーマ。

以下を作成できます **受信者の静的グループ**. 受信者とグループの間には多対多の関係があります。 例えば、1 人の受信者が複数のグループに属し、1 つのグループに複数の受信者を含めることができます。 グループは、読み込みまたは配信ターゲティングを使用して手動で作成できます。 グループは多くの場合、配信ターゲットとして使用されます。 sName グループの内部名を表す一意のインデックスがフィールドにあります。 グループはフォルダーにリンクされています（キーは iFolderId です）。 詳しくは、次を参照してください [XtkFolder](#XtkFolder)）に設定します。

### NmsRcpGrpRel {#NmsRcpGrpRel}

NmsRcpGrpRel 関係テーブルには、iRecipientId および iGroupId リンク テーブルの識別子に対応する 2 つのフィールドのみが含まれています。

### NmsService {#NmsService}

このテーブルはと一致します **nms:service** スキーマ。

Adobe Campaignでは、情報サービス（トピック）の購読を作成および管理できます。 NmsService テーブルには、受信者に購読を提供する情報サービス（トピック） （ニュースレターなど）の定義が格納されます。

サービスは、より多くの情報を循環し、フォームを介して購読と購読解除を簡単に管理できることを除いて、グループ（静的な受信者のグループ化）に似たエンティティです。

sName サービスの内部名を表す一意のインデックスがフィールドにあります。 サービスはフォルダーにリンクされています（キーは iFolderId です）。 詳しくは、次を参照してください [XtkFolder](#XtkFolder)）に設定します。 最後に、iType フィールドには、このサービスの配信チャネルを指定します（メールの場合は 0、SMS の場合は 1、電話の場合は 2、ダイレクトメールの場合は 3、FAX の場合は 4）。

### NmsSubscription {#NmsSubscription}

このテーブルはと一致します **nms:subscription** スキーマ。

これにより、情報サービスに対する受信者の購読を管理できます。

### NmsSubHito {#NmsSubHisto}

このテーブルはと一致します **nms:subHito** スキーマ。

購読が web フォームまたはアプリケーションのインターフェイスを使用して管理されている場合、すべての購読と購読解除は NmsSubHisto テーブルで履歴化されます。 iAction フィールドは、tsDate フィールドに格納された日付に実行されるアクション（購読解除の場合は 0 で購読の場合は 1 で）を指定します。

### NmsDelivery {#NmsDelivery}

このテーブルはと一致します **nms:delivery** スキーマ。

このテーブルの各レコードは、 **配信アクション** または **配信テンプレート**. 配信の実行に必要なすべてのパラメーター（ターゲット、コンテンツなど）が含まれます。 配信（ブロードキャスト）ログ（NmsBroadLog）と関連するトラッキング URL （NmsTrackingUrl）は、分析フェーズで作成されます（これらのテーブルについて詳しくは、両方のテーブルを参照してください）。

sInternalName 配信またはシナリオの内部名を表す一意のインデックスがフィールドにあります。 配信は実行フォルダーにリンクされています（外部キーは iFolderProcessId です）。 詳しくは、次を参照してください [XtkFolder](#XtkFolder)）に設定します。

### XtkFolder {#XtkFolder}

次を含む **ツリー内のすべてのフォルダー** に表示 **ナビゲーション** コンソールのタブ。

フォルダーには次のタイプを入力します。sModel フィールドの値は、フォルダーに含めることができるデータのタイプを指定します。 また、このフィールドを使用すると、クライアントコンソールで対応するフォームと共にデータを正しく表示できます。 このフィールドに指定可能な値は、navTree で定義されます。

ツリーは、iParentId および iChildCount フィールドで管理されます。 sFullName フィールドには、ツリー内のフォルダーの完全パスが表示されます。 最後に、sName フォルダーの内部名を表す一意のインデックスがフィールドに表示されます。

## 配信とトラッキング {#delivery-and-tracking}

このテーブル セットは、にリンクされています **配信** モジュール。メッセージの送信時に発生した配信と最終的な問題を監視できます。 詳しくは、次を参照してください [配信の監視](../../delivery/using/about-delivery-monitoring.md). トラッキングについて詳しくは、を参照してください。 [メッセージのトラッキング](../../delivery/using/about-message-tracking.md).

![](assets/data-model_delivery.png)

**NmsBroadLogMsg**：このテーブルはと一致します。 **nms:broadLogMsg** スキーマ。 これは、配信ログテーブルの拡張です。

## キャンペーン管理 {#campaign-management}

このテーブル セットは、にリンクされています **マーケティングキャンペーン** モジュールを使用すると、コミュニケーションおよびマーケティングキャンペーンを定義、最適化、実行および分析できます。 詳しくは、次を参照してください [マーケティングキャンペーンについて](../../campaign/using/designing-marketing-campaigns.md).

![](assets/data-model_campaign.png)

* **NmsOperation**：このテーブルはと一致します。 **nms:operation** スキーマ。 マーケティングキャンペーンのデータが含まれます。
* **NmsDeliveryOutline**：このテーブルはと一致します。 **nms:deliveryOutline** スキーマ。 配信の拡張プロパティ（配信の概要）が含まれます。
* **NmsDlvOutlineItem**：このテーブルはと一致します。 **nms:dlvOutlineItem** スキーマ。 配信の概要の記事が含まれます。
* **NmsDeliveryCustomization**：このテーブルはと一致します。 **nms:deliveryCustomization** スキーマ。 配信のパーソナライゼーションフィールドが含まれます。
* **NmsBudget**：このテーブルはと一致します。 **nms:budget** スキーマ。 キャンペーン、プラン、プログラム、タスクおよび/または配信の予算のデータが含まれます。
* **NmsDocument**：このテーブルはと一致します。 **nms:document** スキーマ。 ファイル（画像、Excel ファイル、Word ファイルなど）の形式でキャンペーンのマーケティングドキュメントが含まれます。
* **XtkWorkflow**：このテーブルはと一致します。 **xtk:workflow** スキーマ。 キャンペーンのターゲティングが含まれます。
* **NmsTask**：このテーブルはと一致します。 **nms:task** スキーマ。 マーケティングタスクの定義が含まれます。
* **NmsAsset**：このテーブルはと一致します。 **nms:asset** スキーマ。 マーケティングリソースの定義が含まれます。

## 通信の整合性 {#communication-consistency}

このテーブル セットは、にリンクされています **キャンペーンの最適化** モジュール（配信の送信を制御、フィルタリングおよび監視できます）。 詳しくは、次を参照してください [キャンペーンタイポロジについて](../../campaign-opt/using/about-campaign-typologies.md).

![](assets/data-model_typology.png)

* **NmsTypologyRule**：このテーブルはと一致します。 **nms:typologyRule** スキーマ。 タイポロジに応じて配信に適用されるルールが含まれます。
* **NmsTypology**：このテーブルはと一致します。 **nms：タイポロジ** スキーマ。 タイポロジに一致する配信に適用される一連のルールが含まれます。
* **NmsTypologyRuleRel**：このテーブルはと一致します。 **nms:typologyRuleRel** スキーマ。 タイポロジとそのルールの関係が含まれます。
* **NmsVolumeLine**：このテーブルはと一致します。 **nms:volumeLine** スキーマ。 処理能力ルールの稼動ラインのセットが含まれます。
* **NmsVolumeConsumed**：このテーブルはと一致します。 **nms:volumeConsumed** スキーマ。 処理能力ルールのすべての消費ラインが含まれます。

## 応答管理 {#response-management}

このテーブル セットは、にリンクされています **Response Manager** モジュールを使用すると、マーケティングキャンペーンの成功や収益性を測定したり、すべてのコミュニケーションチャネルに対して提案を行ったりできます。 詳しくは、次を参照してください [Response manager について](../../response/using/about-response-manager.md).

![](assets/data-model_response.png)

### NmsRema 仮説 {#NmsRemaHypothesis}

この表は、 **nms:remaHypothesis** スキーマ。 測定仮説の定義が含まれます。

このテーブルには、XML に格納された次のような重要な情報が含まれます。

**実行コンテキスト （XML に保存される情報）**

実行コンテキストでは、測定計算に考慮するテーブルとフィールドに値を設定します。つまり、
* nms:remaMatchRcp 反応ログストレージスキーマ。
* トランザクションテーブルスキーマ（購入など）。
* クエリスキーマ（仮説の条件の開始テーブルを定義できます）
* 個人へのリンク。クエリスキーマに基づいて個人を識別できます。
* トランザクションの日付。 このフィールドは必須ではありませんが、計算範囲を制限するために使用することをお勧めします。
* 取引金額：売上高指標を自動計算するためのオプションのフィールドです。

**仮説の境界（XML に保存された情報）**

仮説の境界は、クエリスキーマのテーブルに基づく仮説のフィルタリングで構成されます。

**仮説オーバーロードスクリプト（XML に保存される情報）**

仮説オーバーロードスクリプトは、実行中に仮説のコンテンツをオーバーロードできる JavaScript コードです。

**測定インジケーター**

仮説の実行中に、次の指標が自動的に更新されます。

* 反応の数： **iTransaction**. 反応ログテーブルのライン数。
* 連絡回数： **iContactReacted**. 仮説のターゲット連絡先のユニーク数。
* コントロール母集団の数： **iProofReacted**. 仮説でのターゲットコントロールグループのユニーク連絡先の数。
* 反応率： **dContactReactRate**. 仮説のターゲットとなる連絡先の応答率。
* コントロール母集団の応答率： **dProofReactedRate**. 仮説コントロールグループの応答率。
* コンタクト済み母集団の合計売上高： **dContactReactedTotalAmount**. 仮説のターゲット連絡先の合計売上高。
* コントロール母集団の平均売上高： **dContactReactAvgAmount**. 仮説のターゲットコントロールグループ連絡先の平均売上高。
* コントロール母集団の合計売上高： **dProofReactedTotalAmount**. 仮説コントロールグループの合計売上高。
* コントロール母集団の平均売上高： **dProofReactedAvgAmount**. 仮説コントロールグループの平均売上高。
* コンタクト先ごとの合計利益： **dContactReactedTotalMargin**. 仮説のコンタクト先ごとの合計マージン。
* コンタクト先ごとの平均利益： **dContactReactedAvgMargin**. 仮説のコンタクト先あたりの平均マージン。
* コントロール母集団の合計利益： **dProofReactedTotalMargin**. 仮説でターゲティングしたコントロールグループの合計利益。
* コントロール母集団の平均利益： **dProofReactedAvgMargin**. 仮説でターゲティングしたコントロールグループの平均利益。
* 追加の売上高： **AdditionnalAmount**. （コンタクト先の平均売上高 – コントロール母集団の平均売上高） * コンタクト先数。
* 追加の利益： **AdditionnalMargin**. （コンタクト先の平均利益 – コントロール母集団の平均利益）/ コンタクト先数。
* コンタクト先ごとの平均コスト （SQL 式）。 配信の計算コスト /連絡された数。
* ROI （SQL 式）。 配信の計算コスト / コンタクト済みの合計利益。
* 実効 ROI （SQL 式） 配信の計算コスト /追加マージン。
* 重要度： **有意性** （SQL 式）。 キャンペーンの重要性に応じて 0 ～ 3 の値が含まれます。

### NmsRemaMatchRcp {#NmsRemaMatchRcp}

このテーブルはと一致します **nms:remaMatchRcp** スキーマ。

特定の仮説に対する個人の反応を表すレコードが含まれます。 これらのレコードは、仮説の実行中に作成されました。

## シミュレーションと配信 {#simulation-and-delivery}

このテーブル セットは、にリンクされています **模擬** モジュール。提案を受信者に送信する前に、カテゴリまたは環境に属するオファーの配布をテストできます。 詳しくは、次を参照してください [オファーシミュレーションについて](../../interaction/using/about-offers-simulation.md).

![](assets/data-model_simulation.png)

* **NmsSimulation**：このテーブルはと一致します。 **nms：シミュレーション** スキーマ。 特定の母集団に対する一連の配信またはオファーのシミュレーションを表します。
* **NmsDlvSimulationRel**：このテーブルはと一致します。 **nms:dlvSimulationRel** スキーマ。 シミュレーションで考慮される配信のリストが含まれます。 シミュレーションの範囲は、XML に保存されます。
* **NmsOfferSimulationRel**：このテーブルはと一致します。 **nms:offerSimulationRel** スキーマ。 シミュレーションとオファーをリンクできます。

## インタラクションモジュール {#interaction-module}

このテーブル セットは、にリンクされています **相互作用** モジュール。特定のコンタクト先とのインタラクション中に、1 つまたは複数の適合するオファーを提供することで、リアルタイムに応答できます。 詳しくは、次を参照してください [インタラクションとオファー管理](../../interaction/using/interaction-and-offer-management.md).

* **NmsOffer**：このテーブルはと一致します。 **nms:offer** スキーマ。 各マーケティングオファーの定義が含まれます。
* **NmsPropositionRcp**：このテーブルはと一致します。 **nms:propositionRcp** スキーマ。 各個人に送信されたマーケティング提案のクロスチャネルログが含まれます。 レコードは、提案が準備されたときや、個人に対して効果的に提案されたときに作成されます。
* **NmsOfferSpace**：このテーブルはと一致します。 **nms:offerSpace** スキーマ。 これには、提案が行われる場所の定義が含まれています。
* **NmsOfferContext**：このテーブルはと一致します。 **nms:offerContext** スキーマ。 これには、提案の適用可能性に関する追加の条件と、重み付け計算式の定義が含まれています。
* **NmsOfferView**：このテーブルはと一致します。 **nms:offerView**. これには、オファー表示域が含まれます。
* **NmsOfferCategory**：このテーブルはと一致します。 **nms:offerCategory**. オファーカテゴリが含まれます。
* **NmsOfferEnv**：このテーブルはと一致します。 **nms:offerEnv**. これには、オファー環境が含まれます。

## Message Center モジュール {#message-center-module}

にリンクされているテーブルは次のとおりです。 **トランザクションメッセージ** （Message Center）モジュール。情報システムからトリガーされるイベントから生成され、ユーザーに送信される個々のコミュニケーションと一意のコミュニケーションを管理できます。 詳しくは、次を参照してください [トランザクションメッセージについて](../../message-center/using/about-transactional-messaging.md).

### NmsRtEvent {#NmsRtEvent}

![](assets/data-model_message-center_rt.png)

このテーブルはと一致します **nms:rtEvent** スキーマ。 リアルタイムイベントの定義が含まれています。

### NmsBatchEvent {#NmsBatchEvent}

![](assets/data-model_message-center_batch.png)

このテーブルはと一致します **nms:batchEvent** スキーマ。 バッチ別のイベントの定義が含まれます。

<!--## Microsites Module {#microsites-module}

This set of tables is linked to the **Web applications** functionality, which allows to create and publish dynamic and interactive web applications with data from the database and content adapted to the rights of the connected user. For more on this, see [About web applications](../../web/using/about-web-applications.md).

![](assets/data-model_microsites.png)

* **NmsTrackingUrl**: This table matches the **nms:trackingUrl** schema.

* **NmsPurl**: This table matches the **nms:purl** schema.-->

## NMAC モジュール {#nmac-module}

このテーブル セットは、にリンクされています **モバイルアプリチャネル**&#x200B;を使用すると、パーソナライズされた通知をアプリを介してiOSおよび Android 端末に送信できます。 詳しくは、次を参照してください [モバイルアプリチャネルについて](../../delivery/using/about-mobile-app-channel.md).

* **NmsMobileApp**：このテーブルはと一致します。 **nms:mobileApp** スキーマ。 これには、Adobe Campaignで定義されたモバイルアプリケーションが含まれます。
* **NmsAppSubscription**：このテーブルはと一致します。 **nms:appSubscription** スキーマ。 1 つ以上のアプリケーションに関するサブスクライバー情報が含まれます。
* **NmsAppSubscriptionRcp**：このテーブルはと一致します。 **nms:appSubscriptionRcp** スキーマ。 これにより、アプリケーションを購読している訪問者を受信者テーブルにリンクできます。
* **NmsExcludeLogAppSubRcp**：このテーブルはと一致します。 **nms:excludeLogAppSubRcp** スキーマ。
* **NmsTrackingLogAppSubRcp**：このテーブルはと一致します。 **nms:trackingLogAppSubRcp** スキーマ。
* **NmsBroadLogAppSubRcp**：このテーブルはと一致します。 **nms:broadLogAppSubRcp** スキーマ。

## ソーシャルマーケティングモジュール {#social-marketing-module}

このテーブル セットは、にリンクされています **ソーシャルネットワーク管理** モジュール。Facebookおよび X （旧称：Twitter）を介して顧客や見込み客とやり取りできます。 詳しくは、次を参照してください [ソーシャルマーケティングについて](../../social/using/about-social-marketing.md).

![](assets/data-model_social.png)

* **NmsVisitor**：このテーブルはと一致します。 **nms:visitor** スキーマ。 訪問者に関する情報が含まれます。
* **NmsVisitorSub**：このテーブルはと一致します。 **nms:visitorSub** スキーマ。 これにより、訪問者を、その訪問者が購読しているサービス（X またはFacebook）にリンクさせることができます。
* **NmsFriendShipRel**：このテーブルはと一致します。 **nms:friendshipRel** スキーマ。 これにより、Facebook サービスのコンテキスト内で、訪問者を友人とリンクできます。
* **NmsVisitorInterestRel**：このテーブルはと一致します。 **nms:visitorInterestRel** スキーマ。 これにより、訪問者とその興味をリンクさせることができます。
* **NmsInterest**：このテーブルはと一致します。 **nms:interest** スキーマ。 各訪問者の興味のリストが含まれます。
