---
product: campaign
title: Adobe Campaign Classic データモデルの説明
description: このドキュメントでは、Adobe Campaign データモデルについて説明します
feature: Data Model
role: Data Engineer, Developer
exl-id: fc0fd23c-f9ea-4e30-b47b-a84143d882ca
source-git-commit: ad6f3f2cf242d28de9e6da5cec100e096c5cbec2
workflow-type: tm+mt
source-wordcount: '2359'
ht-degree: 2%

---

# Campaign データモデルの説明{#data-model-description}


Adobe Campaign には、事前定義済みのデータモデルが付属しています。ここでは、Adobe Campaign データモデルのビルトインテーブルとそのインタラクションについて詳しく説明します。

各テーブルの記述にアクセスするには、**[!UICONTROL 管理／設定／データスキーマ]**&#x200B;に移動し、リストからリソースを選択して「**[!UICONTROL ドキュメント]**」タブをクリックします。

![](assets/data-model_documentation-tab.png)

>[!NOTE]
>
>アプリケーションに格納されるデータの物理的および論理的構造は、XML で記述されます。スキーマと呼ばれる Adobe Campaign 特有の文法に従います。Adobe Campaign スキーマについて詳しくは、[&#x200B; この節 &#x200B;](../../configuration/using/about-schema-reference.md) を参照してください。

## メインテーブルの説明 {#description-main-tables}

Adobe Campaignは、相互にリンクされたテーブルを含んだリレーショナルデータベースに基づいています。

次の図は、Adobe Campaign データモデルの主要なビジネステーブルと、それぞれの主要なフィールドの間の結合を示しています。

<!--![](assets/data-model_diagram.png)-->

![](assets/data-model_simplified-diagram.png)

事前定義済みのAdobe Campaign データモデルには、以下に示すメインテーブルが含まれています。

### NmsRecipient {#NmsRecipient}

このテーブルは **nms:recipient** スキーマに一致します。

これは、（配信の受信者 **に使用されるデフォルトのテーブル** す。 その結果、様々なチャネルを介した配信に必要な情報が含まれます。

* sEmail：メールアドレス。
* iEmailFormat：メールの推奨フォーマット（テキストの場合は 1、HTMLの場合は 2、未定義の場合は 0）。
* sAddress1、sAddress2、sAddress3、sAddress4、sZipCode、sCity は、住所の作成に使用されます（1997 年 5 月の XPZ 10-011 AFNOR 標準に準拠）。
* sPhone、sMobilePhone、sFax には、それぞれ電話番号、携帯電話番号、FAX 番号が含まれています。
* iBlackList は、プロファイルに使用されるデフォルトのオプトアウトフラグです（1 は「購読解除」を意味し、それ以外は 0 を意味します）。

iFolderId フィールドは、受信者を実行フォルダーにリンクする外部キーです。 詳しくは、[XtkFolder](#XtkFolder) を参照してください。

sCountryCode フィールドは、受信者に関連付けられている国の 3166-1 Alpha 2 ISO コード（2 文字）です。 このフィールドは、実際には国参照テーブル（NmsCountry）の外部キーであり、国ラベルとその他の国コードデータが含まれています。 国が入力されていない場合、値「XX」が保存されます（ゼロ ID レコードの代わりに使用されます）。

受信者テーブルの詳細については、[&#x200B; この節 &#x200B;](../../configuration/using/about-data-model.md#default-recipient-table) を参照してください。

### NmsGroup {#NmsGroup}

このテーブルは **nms:group** スキーマに一致します。

これにより、**静的な受信者グループ** を作成できます。 受信者とグループの間には多対多の関係があります。 例えば、1 人の受信者が複数のグループに属し、1 つのグループに複数の受信者を含めることができます。 グループは、読み込みまたは配信ターゲティングを使用して手動で作成できます。 グループは多くの場合、配信ターゲットとして使用されます。 sName グループの内部名を表す一意のインデックスがフィールドにあります。 グループはフォルダーにリンクされています（キーは iFolderId です）。 詳しくは、[XtkFolder](#XtkFolder)）を参照してください。

### NmsRcpGrpRel {#NmsRcpGrpRel}

NmsRcpGrpRel 関係テーブルには、iRecipientId および iGroupId リンク テーブルの識別子に対応する 2 つのフィールドのみが含まれています。

### NmsService {#NmsService}

このテーブルは **nms:service** スキーマに一致します。

Adobe Campaignでは、情報サービス（トピック）の購読を作成および管理できます。 NmsService テーブルには、受信者に購読を提供する情報サービス（トピック） （ニュースレターなど）の定義が格納されます。

サービスは、より多くの情報を循環し、フォームを介して購読と購読解除を簡単に管理できることを除いて、グループ（静的な受信者のグループ化）に似たエンティティです。

sName サービスの内部名を表す一意のインデックスがフィールドにあります。 サービスはフォルダーにリンクされています（キーは iFolderId です）。 詳しくは、[XtkFolder](#XtkFolder)）を参照してください。 最後に、iType フィールドには、このサービスの配信チャネルを指定します（メールの場合は 0、SMS の場合は 1、電話の場合は 2、ダイレクトメールの場合は 3、FAX の場合は 4）。

### NmsSubscription {#NmsSubscription}

このテーブルは **nms:subscription** スキーマに一致します。

これにより、情報サービスに対する受信者の購読を管理できます。

### NmsSubHito {#NmsSubHisto}

このテーブルは **nms:subHisto** スキーマに一致します。

購読が web フォームまたはアプリケーションのインターフェイスを使用して管理されている場合、すべての購読と購読解除は NmsSubHisto テーブルで履歴化されます。 iAction フィールドは、tsDate フィールドに格納された日付に実行されるアクション（購読解除の場合は 0 で購読の場合は 1 で）を指定します。

### NmsDelivery {#NmsDelivery}

このテーブルは **nms:delivery** スキーマに一致します。

このテーブルの各レコードは、**配信アクション** または **配信テンプレート** を表します。 配信の実行に必要なすべてのパラメーター（ターゲット、コンテンツなど）が含まれます。 配信（ブロードキャスト）ログ（NmsBroadLog）と関連するトラッキング URL （NmsTrackingUrl）は、分析フェーズで作成されます（これらのテーブルについて詳しくは、両方のテーブルを参照してください）。

sInternalName 配信またはシナリオの内部名を表す一意のインデックスがフィールドにあります。 配信は実行フォルダーにリンクされています（外部キーは iFolderProcessId です）。 詳しくは、[XtkFolder](#XtkFolder)）を参照してください。

### XtkFolder {#XtkFolder}

**ツリー内のすべてのフォルダー** がコンソールの **ナビゲーション** タブに表示されます。

フォルダーには次のタイプを入力します。sModel フィールドの値は、フォルダーに含めることができるデータのタイプを指定します。 また、このフィールドを使用すると、クライアントコンソールで対応するフォームと共にデータを正しく表示できます。 このフィールドに指定可能な値は、navTree で定義されます。

ツリーは、iParentId および iChildCount フィールドで管理されます。 sFullName フィールドには、ツリー内のフォルダーの完全パスが表示されます。 最後に、sName フォルダーの内部名を表す一意のインデックスがフィールドに表示されます。

## 配信とトラッキング {#delivery-and-tracking}

この一連のテーブルは **配信** モジュールとリンクしており、メッセージの送信時に発生する配信と最終的な問題を監視できます。 詳しくは、[&#x200B; 配信の監視 &#x200B;](../../delivery/using/about-delivery-monitoring.md) を参照してください。 トラッキングについて詳しくは、[&#x200B; トラッキングメッセージ &#x200B;](../../delivery/using/about-message-tracking.md) を参照してください。

![](assets/data-model_delivery.png)

**NmsBroadLogMsg**：このテーブルは **nms:broadLogMsg** スキーマに一致します。 これは、配信ログテーブルの拡張です。

## キャンペーン管理 {#campaign-management}

このテーブルのセットは、コミュニケーションおよびマーケティングキャンペーンを定義、最適化、実行および分析できる **マーケティングキャンペーン** モジュールにリンクされています。 詳しくは、[Campaign v8 ドキュメント &#x200B;](https://experienceleague.adobe.com/docs/campaign/campaign-v8/campaigns/campaigns.html?lang=ja){target=_blank} を参照してください。

![](assets/data-model_campaign.png)

* **NmsOperation**：このテーブルは **nms:operation** スキーマと一致します。 マーケティングキャンペーンのデータが含まれます。
* **NmsDeliveryOutline**：このテーブルは **nms:deliveryOutline** スキーマと一致します。 配信の拡張プロパティ（配信の概要）が含まれます。
* **NmsDlvOutlineItem**：このテーブルは **nms:dlvOutlineItem** スキーマと一致します。 配信の概要の記事が含まれます。
* **NmsDeliveryCustomization**：このテーブルは、**nms:deliveryCustomization** スキーマと一致します。 配信のパーソナライゼーションフィールドが含まれます。
* **NmsBudget**：このテーブルは **nms:budget** スキーマと一致します。 キャンペーン、プラン、プログラム、タスクおよび/または配信の予算のデータが含まれます。
* **NmsDocument**：このテーブルは **nms:document** スキーマと一致します。 ファイル（画像、Excel ファイル、Word ファイルなど）の形式でキャンペーンのマーケティングドキュメントが含まれます。
* **XtkWorkflow**：このテーブルは **xtk:workflow** スキーマに一致します。 キャンペーンのターゲティングが含まれます。
* **NmsTask**：このテーブルは **nms:task** スキーマと一致します。 マーケティングタスクの定義が含まれます。
* **NmsAsset**：このテーブルは **nms:asset** スキーマと一致します。 マーケティングリソースの定義が含まれます。

## 通信の整合性 {#communication-consistency}

この一連のテーブルは、**キャンペーンの最適化** モジュールにリンクされており、配信の送信を制御、フィルタリングおよび監視できます。 [Campaign v8 ドキュメント &#x200B;](https://experienceleague.adobe.com/docs/campaign/automation/campaign-optimization/campaign-typologies.html?lang=ja){target="_blank"} を参照してください。


![](assets/data-model_typology.png)

* **NmsTypologyRule**：このテーブルは **nms:typologyRule** スキーマと一致します。 タイポロジに応じて配信に適用されるルールが含まれます。
* **NmsTypology**：このテーブルは **nms:typology** スキーマと一致します。 タイポロジに一致する配信に適用される一連のルールが含まれます。
* **NmsTypologyRuleRel**：このテーブルは **nms:typologyRuleRel** スキーマと一致します。 タイポロジとそのルールの関係が含まれます。
* **NmsVolumeLine**：このテーブルは **nms:volumeLine** スキーマと一致します。 処理能力ルールの稼動ラインのセットが含まれます。
* **NmsVolumeConsumed**：このテーブルは **nms:volumeConsumed** スキーマと一致します。 処理能力ルールのすべての消費ラインが含まれます。

## 応答管理 {#response-management}

この一連のテーブルは、**応答マネージャー** モジュールにリンクされており、マーケティングキャンペーンの成功や収益性を測定したり、すべての通信チャネルに対して提案を行ったりできます。 詳しくは、[Response Manager について &#x200B;](../../response/using/about-response-manager.md) を参照してください。

![](assets/data-model_response.png)

### NmsRema 仮説 {#NmsRemaHypothesis}

このテーブルは、**nms:remaHypothesis** スキーマと一致します。 測定仮説の定義が含まれます。

このテーブルには、XML に格納された次のような重要な情報が含まれます。

**実行コンテキスト（XML に保存される情報）**

実行コンテキストでは、測定計算に考慮するテーブルとフィールドに値を設定します。つまり、
* nms:remaMatchRcp 反応ログのストレージスキーマ。
* トランザクションテーブルスキーマ（購入など）。
* クエリスキーマ（仮説の条件の開始テーブルを定義できます）
* 個人へのリンク。クエリスキーマに基づいて個人を識別できます。
* トランザクションの日付。 このフィールドは必須ではありませんが、計算範囲を制限するために使用することをお勧めします。
* 取引金額：売上高指標を自動計算するためのオプションのフィールドです。

**仮説の境界（XML に保存される情報）**

仮説の境界は、クエリスキーマのテーブルに基づく仮説のフィルタリングで構成されます。

**仮説オーバーロードスクリプト（XML に保存される情報）**

仮説オーバーロードスクリプトは、実行中に仮説のコンテンツをオーバーロードできるJavaScript コードです。

**測定指標**

仮説の実行中に、次の指標が自動的に更新されます。

* 反応数：**iTransaction**。 反応ログテーブルのライン数。
* コンタクト数：**iContactReacted**。 仮説のターゲット連絡先のユニーク数。
* コントロール母集団の数：**iProofReacted**。 仮説でのターゲットコントロールグループのユニーク連絡先の数。
* 反応率：**dContactReactedRate**。 仮説のターゲットとなる連絡先の応答率。
* コントロール母集団の応答速度：**dProofReactedRate**。 仮説コントロールグループの応答率。
* コンタクト済み母集団の合計売上高：**dContactReactedTotalAmount**. 仮説のターゲット連絡先の合計売上高。
* コントロール母集団の平均売上高：**dContactReactedAvgAmount**. 仮説のターゲットコントロールグループ連絡先の平均売上高。
* コントロール母集団の合計売上高：**dProofReactedTotalAmount**。 仮説コントロールグループの合計売上高。
* コントロール母集団の平均売上高：**dProofReactedAvgAmount**。 仮説コントロールグループの平均売上高。
* コンタクト先ごとの合計利益：**dContactReactedTotalMargin**. 仮説のコンタクト先ごとの合計マージン。
* コンタクト先ごとの平均マージン：**dContactReactedAvgMargin**. 仮説のコンタクト先あたりの平均マージン。
* コントロール母集団の合計利益：**dProofReactedTotalMargin**。 仮説でターゲティングしたコントロールグループの合計利益。
* コントロール母集団の平均マージン：**dProofReactedAvgMargin**。 仮説でターゲティングしたコントロールグループの平均利益。
* 追加の売上高：**dAdditionnalAmount**. （コンタクト先の平均売上高 – コントロール母集団の平均売上高） * コンタクト先数。
* 追加の余白：**dAdditionnalMargin**. （コンタクト先の平均利益 – コントロール母集団の平均利益）/ コンタクト先数。
* コンタクト先ごとの平均コスト （SQL 式）。 配信の計算コスト /連絡された数。
* ROI （SQL 式）。 配信の計算コスト / コンタクト済みの合計利益。
* 実効 ROI （SQL 式） 配信の計算コスト /追加マージン。
* 重要度：**iSignificativy** （SQL 式）。 キャンペーンの重要性に応じて 0 ～ 3 の値が含まれます。

### NmsRemaMatchRcp {#NmsRemaMatchRcp}

このテーブルは **nms:remaMatchRcp** スキーマに一致します。

特定の仮説に対する個人の反応を表すレコードが含まれます。 これらのレコードは、仮説の実行中に作成されました。

## シミュレーションと配信 {#simulation-and-delivery}

この一連のテーブルは **シミュレーション** モジュールにリンクしており、提案を受信者に送信する前に、カテゴリまたは環境に属するオファーの配布をテストできます。 詳しくは、[&#x200B; オファーシミュレーションについて &#x200B;](../../interaction/using/about-offers-simulation.md) を参照してください。

![](assets/data-model_simulation.png)

* **NmsSimulation**：このテーブルは **nms:simulation** スキーマと一致します。 特定の母集団に対する一連の配信またはオファーのシミュレーションを表します。
* **NmsDlvSimulationRel**：このテーブルは **nms:dlvSimulationRel** スキーマと一致します。 シミュレーションで考慮される配信のリストが含まれます。 シミュレーションの範囲は、XML に保存されます。
* **NmsOfferSimulationRel**：このテーブルは **nms:offerSimulationRel** スキーマと一致します。 シミュレーションとオファーをリンクできます。

## インタラクションモジュール {#interaction-module}

この一連のテーブルは、**インタラクション** モジュールにリンクしており、特定の連絡先とのインタラクション中に、1 つまたは複数の適合するオファーを提供することで、リアルタイムに応答できます。 詳しくは、[&#x200B; インタラクションとオファー管理 &#x200B;](../../interaction/using/interaction-and-offer-management.md) を参照してください。

* **NmsOffer**：このテーブルは **nms:offer** スキーマと一致します。 各マーケティングオファーの定義が含まれます。
* **NmsPropositionRcp**：このテーブルは **nms:propositionRcp** スキーマに一致します。 各個人に送信されたマーケティング提案のクロスチャネルログが含まれます。 レコードは、提案が準備されたときや、個人に対して効果的に提案されたときに作成されます。
* **NmsOfferSpace**：このテーブルは **nms:offerSpace** スキーマと一致します。 これには、提案が行われる場所の定義が含まれています。
* **NmsOfferContext**：このテーブルは **nms:offerContext** スキーマと一致します。 これには、提案の適用可能性に関する追加の条件と、重み付け計算式の定義が含まれています。
* **NmsOfferView**：このテーブルは **nms:offerView** と一致します。 これには、オファー表示域が含まれます。
* **NmsOfferCategory**：このテーブルは **nms:offerCategory** と一致します。 オファーカテゴリが含まれます。
* **NmsOfferEnv**：このテーブルは **nms:offerEnv** と一致します。 これには、オファー環境が含まれます。

## Message Center モジュール {#message-center-module}

以下の一連のテーブルは、**トランザクションメッセージ** （Message Center）モジュールにリンクしています。このモジュールでは、情報システムからトリガーされるイベントから生成され、ユーザーに送信される個別および一意の通信を管理できます。 詳しくは、[&#x200B; トランザクションメッセージについて &#x200B;](../../message-center/using/about-transactional-messaging.md) を参照してください。

### NmsRtEvent {#NmsRtEvent}

![](assets/data-model_message-center_rt.png)

このテーブルは **nms:rtEvent** スキーマに一致します。 リアルタイムイベントの定義が含まれています。

### NmsBatchEvent {#NmsBatchEvent}

![](assets/data-model_message-center_batch.png)

このテーブルは **nms:batchEvent** スキーマに一致します。 バッチ別のイベントの定義が含まれます。

<!--## Microsites Module {#microsites-module}

This set of tables is linked to the **Web applications** functionality, which allows to create and publish dynamic and interactive web applications with data from the database and content adapted to the rights of the connected user. For more on this, see [About web applications](../../web/using/about-web-applications.md).

![](assets/data-model_microsites.png)

* **NmsTrackingUrl**: This table matches the **nms:trackingUrl** schema.

* **NmsPurl**: This table matches the **nms:purl** schema.-->

## NMAC モジュール {#nmac-module}

この一連のテーブルは、**モバイルアプリチャネル** にリンクされており、アプリを介してiOSおよびAndroid端末にパーソナライズされた通知を送信できます。 詳しくは、[&#x200B; モバイルアプリチャネルについて &#x200B;](../../delivery/using/about-mobile-app-channel.md) を参照してください。

* **NmsMobileApp**：このテーブルは **nms:mobileApp** スキーマと一致します。 これには、Adobe Campaignで定義されたモバイルアプリケーションが含まれます。
* **NmsAppSubscription**：このテーブルは **nms:appSubscription** スキーマと一致します。 1 つ以上のアプリケーションに関するサブスクライバー情報が含まれます。
* **NmsAppSubscriptionRcp**：このテーブルは **nms:appSubscriptionRcp** スキーマと一致します。 これにより、アプリケーションを購読している訪問者を受信者テーブルにリンクできます。
* **NmsExcludeLogAppSubRcp**：このテーブルは **nms:excludeLogAppSubRcp** スキーマと一致します。
* **NmsTrackingLogAppSubRcp**：このテーブルは **nms:trackingLogAppSubRcp** スキーマと一致します。
* **NmsBroadLogAppSubRcp**：このテーブルは **nms:broadLogAppSubRcp** スキーマと一致します。

## ソーシャルマーケティングモジュール {#social-marketing-module}

この一連のテーブルは、**ソーシャルネットワーク管理** モジュールにリンクされています。このモジュールを使用すると、Facebook および X （旧称 Twitter）を介して顧客や見込み客とやり取りできます。 詳しくは、[&#x200B; ソーシャルマーケティングについて &#x200B;](../../social/using/about-social-marketing.md) を参照してください。

![](assets/data-model_social.png)

* **NmsVisitor**：このテーブルは **nms:visitor** スキーマと一致します。 訪問者に関する情報が含まれます。
* **NmsVisitorSub**：このテーブルは **nms:visitorSub** スキーマと一致します。 これにより、訪問者を、その訪問者が購読しているサービス（X または Facebook）にリンクできます。
* **NmsFriendShipRel**：このテーブルは **nms:friendshipRel** スキーマと一致します。 これにより、Facebook サービスのコンテキスト内で、訪問者を友人とリンクできます。
* **NmsVisitorInterestRel**：このテーブルは **nms:visitorInterestRel** スキーマと一致します。 これにより、訪問者とその興味をリンクさせることができます。
* **NmsInterest**：このテーブルは **nms:interest** スキーマと一致します。 各訪問者の興味のリストが含まれます。
