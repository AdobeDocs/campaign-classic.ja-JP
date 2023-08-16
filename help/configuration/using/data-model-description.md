---
product: campaign
title: Adobe Campaign Classic data model description
description: このドキュメントでは、Adobe Campaignデータモデルについて説明します
badge-v7-only: label="v7" type="Informative" tooltip="Campaign Classic v7 にのみ適用されます"
feature: Data Model
exl-id: fc0fd23c-f9ea-4e30-b47b-a84143d882ca
source-git-commit: 8debcd3d8fb883b3316cf75187a86bebf15a1d31
workflow-type: tm+mt
source-wordcount: '2386'
ht-degree: 4%

---

# Campaign データモデルの説明{#data-model-description}


Adobe Campaign には、事前定義済みのデータモデルが付属しています。ここでは、Adobe Campaign データモデルのビルトインテーブルとそのインタラクションについて詳しく説明します。

各テーブルの記述にアクセスするには、**[!UICONTROL 管理／設定／データスキーマ]**&#x200B;に移動し、リストからリソースを選択して「**[!UICONTROL ドキュメント]**」タブをクリックします。

![](assets/data-model_documentation-tab.png)

>[!NOTE]
>
>アプリケーションに格納されるデータの物理的および論理的構造は、XML で記述されます。スキーマと呼ばれる Adobe Campaign 特有の文法に従います。Adobe Campaignスキーマについて詳しくは、 [この節](../../configuration/using/about-schema-reference.md).

## メインテーブルの説明 {#description-main-tables}

Adobe Campaignは、互いにリンクされたテーブルを含むリレーショナルデータベースに依存します。

次の図に、Adobe Campaignデータモデルのメインビジネステーブルと各メインフィールドとの結合を示します。

<!--![](assets/data-model_diagram.png)-->

![](assets/data-model_simplified-diagram.png)

事前定義されたAdobe Campaignデータモデルには、次に示す主なテーブルが含まれています。

### NmsRecipient {#NmsRecipient}

このテーブルは、 **nms:recipient** スキーマ。

これは、 **配信の受信者**. その結果、様々なチャネルを介した配信に必要な情報が含まれます。

* sEmail：電子メールアドレス。
* iEmailFormat：電子メールの推奨される形式 ( テキストの場合は 1、HTMLの場合は 2、未定義の場合は 0)。
* 郵送先住所の作成には、sAddress1、sAddress2、sAddress4、sZipCode、sCity を使用します（1997 年 5 月の XPZ 10-011 AFNOR 標準に準拠）。
* sPhone、sMobilePhone、sFax には、それぞれ電話番号、携帯電話番号、FAX 番号が含まれます。
* iBlackList は、プロファイルに使用されるデフォルトのオプトアウトフラグです（1 は「購読解除済み」を意味し、それ以外は 0 を意味します）。

iFolderId フィールドは、受信者を実行フォルダーにリンクする外部キーです。 詳しくは、 [XtkFolder](#XtkFolder).

sCountryCode フィールドは、受信者に関連付けられた国の 3166-1 Alpha 2 ISO コード（2 文字）です。 このフィールドは、実際には国参照テーブル (NmsCountry) の外部キーで、国ラベルと他の国コードデータが含まれます。 国が入力されていない場合、値「XX」が保存されます（ゼロの ID レコードの代わりに使用されます）。

 受信者テーブルの詳細については、[この節](../../configuration/using/about-data-model.md#default-recipient-table)を参照してください。

### NmsGroup {#NmsGroup}

このテーブルは、 **nms:group** スキーマ。

これにより、 **受信者の統計的なグループ**. 受信者とグループには多対多の関係があります。 例えば、1 人の受信者が複数のグループに属し、1 つのグループに複数の受信者を含めることができます。 グループは、インポートまたは配信のターゲティングを使用して、手動で作成できます。 グループは、多くの場合、配信ターゲットとして使用されます。 sName グループの内部名を表す一意のインデックスがフィールドに存在します。 グループはフォルダーにリンクされています（キーは iFolderId です）。 詳しくは、 [XtkFolder](#XtkFolder)) をクリックします。

### NmsRcpGrpRel {#NmsRcpGrpRel}

NmsRcpGrpRel 関係テーブルには、iRecipientId と iGroupId のリンクされたテーブルの識別子に対応する 2 つのフィールドのみが含まれます。

### NmsService {#NmsService}

このテーブルは、 **nms:service** スキーマ。

Adobe Campaignでは、情報サービス（トピック）の購読を作成および管理できます。 NmsService テーブルには、受信者に購読登録を申し込む情報サービス（トピック）の定義が格納されます（例えば、ニュースレター）。

サービスは、グループ（静的な受信者グループ）に似たエンティティですが、情報が循環し、フォームを介した購読と購読解除の管理が容易になる点が異なります。

sName サービスの内部名を表すフィールドには一意のインデックスがあります。 サービスはフォルダーにリンクされています（キーは iFolderId です）。 詳しくは、 [XtkFolder](#XtkFolder)) をクリックします。 最後に、このサービスの配信チャネルを「 iType 」フィールドで指定します（E メールの場合は 0、SMS の場合は 1、電話の場合は 2、ダイレクトメールの場合は 3、FAX の場合は 4）。

### NmsSubscription {#NmsSubscription}

このテーブルは、 **nms:subscription** スキーマ。

情報サービスに対する受信者の購読を管理できます。

### NmsSubHisto {#NmsSubHisto}

このテーブルは、 **nms:subHisto** スキーマ。

購読が Web フォームまたはアプリケーションのインターフェイスを使用して管理されている場合、すべての購読と購読解除が NmsSubHisto テーブルに履歴化されます。 「 iAction 」フィールドで、「 tsDate 」フィールドに格納された日に実行されるアクション（購読解除の場合は 0、購読の場合は 1）を指定します。

### NmsDelivery {#NmsDelivery}

このテーブルは、 **nms:delivery** スキーマ。

このテーブルの各レコードは、 **配信アクション** または **配信テンプレート**. 配信を実行するために必要なすべてのパラメーター（ターゲット、コンテンツなど）が含まれています。 配信（ブロードキャスト）ログ (NmsBroadLog) と関連するトラッキング URL(NmsTrackingUrl) は、分析フェーズで作成されます（これらの両方のテーブルについて詳しくは、以下を参照してください）。

sInternalName 配信またはシナリオの内部名を表すフィールドに一意のインデックスがあります。 この配信は実行フォルダーにリンクされます（外部キーは iFolderProcessId です）。 詳しくは、 [XtkFolder](#XtkFolder)) をクリックします。

### XtkFolder {#XtkFolder}

次を含む **ツリー内のすべてのフォルダ** 次の場所に表示： **ナビゲーション** コンソールの「 」タブをクリックします。

フォルダーの種類： sModel フィールドの値は、フォルダーに含めることができるデータのタイプを指定します。 また、このフィールドを使用すると、クライアントコンソールで、対応するフォームと共にデータを正しく表示できます。 このフィールドで指定可能な値は、 navTree で定義されます。

このツリーは、 iParentId フィールドと iChildCount フィールドで管理されます。 「sFullName」フィールドには、ツリー内のフォルダーのフルパスが入力されます。 最後に、sName フォルダーの内部名を表すフィールドに一意のインデックスが存在します。

## 配信とトラッキング {#delivery-and-tracking}

この一連のテーブルは、 **配信** モジュール：配信と、メッセージの送信時に結果として起こる問題を監視できます。 詳しくは、 [配信の監視](../../delivery/using/about-delivery-monitoring.md). トラッキングについて詳しくは、 [メッセージのトラッキング](../../delivery/using/about-message-tracking.md).

![](assets/data-model_delivery.png)

**NmsBroadLogMsg**：このテーブルは、 **nms:broadLogMsg** スキーマ。 これは、配信ログテーブルの拡張です。

## キャンペーン管理 {#campaign-management}

この一連のテーブルは、 **マーケティングキャンペーン** モジュール：コミュニケーションおよびマーケティングキャンペーンを定義、最適化、実行および分析できます。 詳しくは、 [マーケティングキャンペーンについて](../../campaign/using/designing-marketing-campaigns.md).

![](assets/data-model_campaign.png)

* **NmsOperation**：このテーブルは、 **nms:operation** スキーマ。 マーケティングキャンペーンのデータが含まれます。
* **NmsDeliveryOutline**：このテーブルは、 **nms:deliveryOutline** スキーマ。 配信の拡張プロパティ（配信の概要）が含まれます。
* **NmsDlvOutlineItem**：このテーブルは、 **nms:dlvOutlineItem** スキーマ。 配信の概要の記事が含まれます。
* **NmsDeliveryCustomization**：このテーブルは、 **nms:deliveryCustomization** スキーマ。 配信のパーソナライゼーションフィールドが含まれます。
* **NmsBudget**：このテーブルは、 **nms:budget** スキーマ。 キャンペーン、プラン、プログラム、タスク、配信に関する予算のデータが含まれます。
* **NmsDocument**：このテーブルは、 **nms:document** スキーマ。 このテンプレートには、キャンペーンのマーケティングドキュメントがファイル（画像、Excel、Word ファイルなど）の形式で含まれます。
* **XtkWorkflow**：このテーブルは、 **xtk:workflow** スキーマ。 キャンペーンのターゲティングが含まれます。
* **NmsTask**：このテーブルは、 **nms:task** スキーマ。 マーケティングタスクの定義が含まれます。
* **NmsAsset**：このテーブルは、 **nms:asset** スキーマ。 マーケティングリソースの定義が含まれます。

## 通信の一貫性 {#communication-consistency}

この一連のテーブルは、 **キャンペーンの最適化** モジュール：配信を制御、フィルタリングおよび監視できます。 詳しくは、 [キャンペーンタイポロジについて](../../campaign-opt/using/about-campaign-typologies.md).

![](assets/data-model_typology.png)

* **NmsTypologyRule**：このテーブルは、 **nms:typologyRule** スキーマ。 タイポロジに応じて配信に適用されるルールが含まれています。
* **NmsTypology**：このテーブルは、 **nms:typology** スキーマ。 タイポロジに一致する配信に適用される一連のルールが含まれます。
* **NmsTypologyRuleRel**：このテーブルは、 **nms:typologyRuleRel** スキーマ。 タイポロジとそのルールの関係が含まれます。
* **NmsVolumeLine**：このテーブルは、 **nms:volumeLine** スキーマ。 処理能力ルールの稼動ラインのセットが含まれます。
* **NmsVolumeConsumed**：このテーブルは、 **nms:volumeConsumed** スキーマ。 処理能力ルールのすべての消費ラインが含まれます。

## 応答管理 {#response-management}

この一連のテーブルは、 **Response Manager** モジュール：すべての通信チャネルに対するマーケティングキャンペーンまたはオファーの提案の成功と収益性を測定できます。 詳しくは、 [Response Manager について](../../response/using/about-response-manager.md).

![](assets/data-model_response.png)

### NmsRemaHypothesis {#NmsRemaHypothesis}

このテーブルは、 **nms:remaHypothesis** スキーマ。 測定仮説の定義が含まれます。

この表には、次のような XML に格納された重要な情報が含まれます。

**実行コンテキスト（XML 形式で格納された情報）**

実行コンテキストによって、測定の計算に考慮するテーブルとフィールドが設定されます。つまり、
* nms:remaMatchRcp 反応ログストレージスキーマ。
* トランザクションテーブルスキーマ（購入など）。
* 条件スキーマ。仮説の条件の開始テーブルを定義できます。
* 個人へのリンク。クエリスキーマに基づいて個人を識別できます。
* トランザクションの日付。 このフィールドは必須ではありませんが、このフィールドを使用して計算境界を制限することをお勧めします。
* トランザクション金額：売上高指標を自動的に計算するオプションのフィールドです。

**仮説ペリメーター（XML 形式で保存された情報）**

仮説ペリメーターは、条件スキーマのテーブルに基づく仮説のフィルタリングで構成されます。

**仮説オーバーロードスクリプト（XML 形式で保存された情報）**

仮説オーバーロードスクリプトは、実行中に仮説の内容をオーバーロードできる JavaScript コードです。

**測定指標**

次の指標は、仮説の実行中に自動的に更新されます。

* 反応数： **iTransaction**. 反応ログテーブルの行数。
* 連絡数： **iContactReacted**. 仮説でのターゲットとなる連絡先のユニーク数。
* コントロール母集団の数： **iProofReacted**. 仮説でのターゲットコントロール母集団のユニーク連絡先数。
* 連絡済み応答率： **dContactRecodedRate**. 仮説のターゲットとなる連絡先の回答率。
* コントロール母集団の応答率： **dProofReactedRate**. 仮説コントロール母集団の応答率。
* コンタクト済み母集団の合計売上高： **dContactRecolatedTotalAmount**. 仮説のターゲットとなる連絡先の合計売上高。
* コントロール母集団の平均売上高： **dContactReactedAvgAmount**. 仮説でのターゲットコントロール母集団の連絡先の平均売上高。
* コントロール母集団の合計売上高： **dProofReactedTotalAmount**. 仮説コントロールグループの合計売上高.
* コントロール母集団の平均売上高： **dProofReactedAvgAmount**. 仮説コントロールグループの平均売上高。
* 連絡先ごとの合計利益： **dContactRecolatedTotalMargin**. 仮説のコンタクト先あたりの合計マージン.
* コンタクト先ごとの平均利益： **dContactReactedAvgMargin**. 仮説でターゲティングしたコンタクト先ごとの平均利益。
* コントロール母集団の合計利益： **dProofReactedTotalMargin**. 仮説でターゲティングしたコントロール母集団の利益の合計。
* コントロール母集団の平均利益： **dProofReacedAvgMargin**. 仮説でターゲティングしたコントロール母集団の平均利益。
* その他の売上高： **dAdditionalAmount**. （コンタクト先の平均売上高 — コントロール母集団の平均売上高） *コンタクト先の数。
* 追加の利益： **dAdditionalMargin**. （コンタクト先の平均利益 — コントロール母集団の平均利益） /コンタクト先数
* 連絡先あたりの平均コスト（SQL 式）。 配信の計算されたコスト/コンタクト先の数。
* ROI （SQL 式）。 配信の計算されたコスト/コンタクト先の合計利益。
* 効果的な ROI （SQL 式）。 配信の計算されたコスト/追加の利益。
* 重要度： **重要** （SQL 式）。 キャンペーンの重要度に応じて 0 ～ 3 の値が含まれます。

### NmsRemaMatchRcp {#NmsRemaMatchRcp}

このテーブルは、 **nms:remaMatchRcp** スキーマ。

特定の仮説に対する個人の反応を表すレコードが含まれます。 これらのレコードは仮説の実行中に作成されました。

## シミュレーションと配信 {#simulation-and-delivery}

この一連のテーブルは、 **シミュレーション** モジュール：提案を受信者に送信する前に、1 つのカテゴリまたは環境に属するオファーの配分をテストできます。 詳しくは、 [オファーのシミュレーションについて](../../interaction/using/about-offers-simulation.md).

![](assets/data-model_simulation.png)

* **NmsSimulation**：このテーブルは、 **nms:simulation** スキーマ。 これは、特定の母集団に関する一連の配信またはオファーのシミュレーションを表します。
* **NmsDlvSimulationRel**：このテーブルは、 **nms:dlvSimulationRel** スキーマ。 このリストには、シミュレーションで考慮された配信のリストが含まれます。 シミュレーションの範囲は XML 形式で保存されます。
* **NmsOfferSimulationRel**：このテーブルは、 **nms:offerSimulationRel** スキーマ。 シミュレーションをオファーにリンクできます。

## インタラクションモジュール {#interaction-module}

この一連のテーブルは、 **インタラクション** モジュール：特定の連絡先とのインタラクション中に、1 つまたは複数の適応したオファーを作成して、リアルタイムで応答できるようにします。 詳しくは、 [インタラクションとオファーの管理](../../interaction/using/interaction-and-offer-management.md).

* **NmsOffer**：このテーブルは、 **nms:offer** スキーマ。 各マーケティングオファーの定義が含まれます。
* **NmsPropositionRcp**：このテーブルは、 **nms:propositionRcp** スキーマ。 各個人に送信されるマーケティング提案のクロスチャネルログが含まれます。 レコードは、提案が準備されたとき、または個人に対して効果的に提案されたときに作成されます。
* **NmsOfferSpace**：このテーブルは、 **nms:offerSpace** スキーマ。 提案がおこなわれる場所の定義が含まれます。
* **NmsOfferContext**：このテーブルは、 **nms:offerContext** スキーマ。 提案の適用性に関する追加の基準と、重み付け計算式の定義が含まれます。
* **NmsOfferView**：このテーブルは、 **nms:offerView**. オファー表示域が含まれます。
* **NmsOfferCategory**：このテーブルは、 **nms:offerCategory**. オファーカテゴリが含まれます。
* **NmsOfferEnv**：このテーブルは、 **nms:offerEnv**. オファー環境が含まれます。

## Message Center モジュール {#message-center-module}

次の一連のテーブルは、 **トランザクションメッセージ** (Message Center) モジュール。ユーザーに送信され、情報システムからトリガーされるイベントから生成される、個別および個別の通信を管理できます。 詳しくは、 [トランザクションメッセージについて](../../message-center/using/about-transactional-messaging.md).

### NmsRtEvent {#NmsRtEvent}

![](assets/data-model_message-center_rt.png)

このテーブルは、 **nms:rtEvent** スキーマ。 リアルタイムイベントの定義が含まれます。

### NmsBatchEvent {#NmsBatchEvent}

![](assets/data-model_message-center_batch.png)

このテーブルは、 **nms:batchEvent** スキーマ。 バッチ別のイベントの定義が含まれます。

<!--## Microsites Module {#microsites-module}

This set of tables is linked to the **Web applications** functionality, which allows to create and publish dynamic and interactive web applications with data from the database and content adapted to the rights of the connected user. For more on this, see [About web applications](../../web/using/about-web-applications.md).

![](assets/data-model_microsites.png)

* **NmsTrackingUrl**: This table matches the **nms:trackingUrl** schema.

* **NmsPurl**: This table matches the **nms:purl** schema.-->

## NMAC モジュール {#nmac-module}

この一連のテーブルは、 **モバイルアプリチャネル**：アプリを介してiOSおよび Android の端末にパーソナライズされた通知を送信できます。 詳しくは、 [モバイルアプリチャネルについて](../../delivery/using/about-mobile-app-channel.md).

* **NmsMobileApp**：このテーブルは、 **nms:mobileApp** スキーマ。 これには、Adobe Campaignで定義されたモバイルアプリケーションが含まれます。
* **NmsAppSubscription**：このテーブルは、 **nms:appSubscription** スキーマ。 これには、1 つ以上のアプリケーションに関する購読者情報が含まれます。
* **NmsAppSubscriptionRcp**：このテーブルは、 **nms:appSubscriptionRcp** スキーマ。 これにより、アプリを購読している訪問者を受信者テーブルとリンクすることができます。
* **NmsExcludeLogAppSubRcp**：このテーブルは、 **nms:excludeLogAppSubRcp** スキーマ。
* **NmsTrackingLogAppSubRcp**：このテーブルは、 **nms:trackingLogAppSubRcp** スキーマ。
* **NmsBroadLogAppSubRcp**：このテーブルは、 **nms:broadLogAppSubRcp** スキーマ。

## ソーシャルマーケティングモジュール {#social-marketing-module}

この一連のテーブルは、 **ソーシャルネットワークの管理** モジュール：FacebookとTwitterを使用して、顧客や見込み客とやり取りできるようにします。 詳しくは、 [ソーシャルマーケティングについて](../../social/using/about-social-marketing.md).

![](assets/data-model_social.png)

* **NmsVisitor**：このテーブルは、 **nms:visitor** スキーマ。 訪問者に関する情報が含まれます。
* **NmsVisitorSub**：このテーブルは、 **nms:visitorSub** スキーマ。 これにより、訪問者が購読したサービス (TwitterまたはFacebook) に訪問者をリンクすることができます。
* **NmsFriendShipRel**：このテーブルは、 **nms:friendshipRel** スキーマ。 これにより、Facebookサービスのコンテキスト内で、訪問者を友人とリンクすることができます。
* **NmsVisitorInterestRel**：このテーブルは、 **nms:visitorInterestRel** スキーマ。 これにより、訪問者とその興味を関連付けることができます。
* **NmsInterest**：このテーブルは、 **nms:interest** スキーマ。 各訪問者の興味のリストが含まれます。
