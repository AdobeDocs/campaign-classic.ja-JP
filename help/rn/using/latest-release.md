---
product: campaign
title: 最新リリース
description: 最新の Campaign Classic v7 リリースノート
badge-v7-only: label="v7" type="Informative" tooltip="Applies to Campaign Classic v7 only"
feature: Overview
role: User
level: Beginner
exl-id: d65869ca-a785-4327-8e8d-791c28e4696c
source-git-commit: f2dc0947a3b1ed17cbc3d88176e7921e80ca1bb5
workflow-type: tm+mt
source-wordcount: '986'
ht-degree: 99%

---

# 最新リリース{#latest-release}

このページには、**最新の Campaign Classic v7 リリース**&#x200B;の新機能、改善点および修正点が記載されています。新しいビルドごとに、色分けされたステータスが表示されます。Campaign Classic v7 のビルドステータスについて詳しくは、[このページ](rn-overview.md)を参照してください。

## リリース 7.3.3 - ビルド 9359 {#release-7-3-3}

[!BADGE 一般公開（GA）]{type=Informative url="https://experienceleague.adobe.com/docs/campaign-classic/using/release-notes/rn-overview.html?lang=ja#rn-statuses" tooltip="一般公開（GA）"}

>[!CAUTION]
>
>コンソールのアップグレードは必須です。クライアントコンソールのアップグレード方法について詳しくは、こちらの[ページ](../../installation/using/installing-the-client-console.md)を参照してください。

_2023年3月20日（PT）_

**セキュリティの強化**

* Tomcat は、セキュリティを最適化するために、バージョン 8.5.81 から 8.5.85 に更新されました。（NEO-56936）

**改善点**

* 請求ワークフローを改善し、パフォーマンスを最適化しました。（NEO-47658）
* トラッキングワークフローを改善し、配信サイズが大きい場合のパフォーマンスを最適化しました。（NEO-45064）
* トラッキング管理を改善し、URL の動的パラメーターで発生する可能性がある問題を修正しました。トラッキング管理 v3 では、ajax タイプの URL（「#」の後のパラメーターを含む）を処理し、サードパーティツールによるトラッキング URL を変更するのを防ぎます。この変更を適用するには、アドビにお問い合わせください。（NEO-46535）

<!--To apply this change, the marketing, tracking and mid servers need to be updated to 7.3.3. To enable the new tracking management mode, set the `emailLinksVersion` parameter to '3' in the configuration file of the marketing server. (NEO-46535)-->

**パッチ**

* コントロールインスタンス（トランザクションメッセージコンテキスト）から iOS の配達確認のプッシュ通知が送信されない問題を修正しました。（NEO-54713）
* デジタルコンテンツエディター（DCE）の「**編集**」タブでスクロールできない問題を修正しました。（NEO-54474）
* 2 つのエンリッチメントアクティビティがリンクで同じ名前識別子を使用していた場合に、2 つ目のエンリッチメントアクティビティが最初のエンリッチメントアクティビティのリンクを使用する問題を修正しました。（NEO-48851）

## リリース 7.3.2 - ビルド 9356 {#release-7-3-2}

[!BADGE 限定的な可用性]{type=Neutral url="https://experienceleague.adobe.com/docs/campaign-classic/using/release-notes/rn-overview.html?lang=ja#rn-statuses" tooltip="限定的な可用性"}

_2022年11月21日（PT）_

>[!CAUTION]
>
>コンソールのアップグレードは必須です。クライアントコンソールのアップグレード方法について詳しくは、こちらの[ページ](../../installation/using/installing-the-client-console.md)を参照してください。

**互換性の更新**

* Adobe Campaign に、PostgreSQL 14 との互換性が備わりました。詳しくは、この[テクニカルノート](../../technotes/using/tech-stack-upgrade.md)を参照してください。

* Microsoft Internet Explorer 11 のサポート終了に伴い、クライアントコンソールのダッシュボードの HTML レンダリングエンジンは、Edge Chromium を使用するようになりました。（NEO-20741）

詳しくは、[Campaign 互換性マトリックス](../../rn/using/compatibility-matrix.md#RDBMSservers)を参照してください。

**改善点**

* Google BigQuery コネクタがブール値フィールドを完全にサポートするようになりました。 （NEO-49181）
* serverConf.xml ファイルの `Configuration for the redirection service` セクションで、IMS Cookie の有効期間を設定できるようになりました。これは、次の Cookie（`uuid230`、`nllastdelid` および `AMCV_`）に適用されます（NEO-42541）。
* serverConf.xml ファイルのリダイレクトノードで `showSourceIP` を false に設定することで、「/r/test」リクエストで IP を非表示にできるようになりました。[詳細を表示](../../installation/using/the-server-configuration-file.md#redirection-redirection)（NEO-46656）

**非推奨（廃止予定）の機能**

* Facebook を使用したソーシャルマーケティングは非推奨（廃止予定）になりました。Twitter 統合を使用してソーシャルメディアに投稿したり、アドビと連携してカスタムチャネルを作成したりできます。
* ACS コネクタ（プライムオファー）は非推奨（廃止予定）となりました。 Campaign のエクスポート／インポート機能を使用して、両方の製品のデータを抽出および挿入できます。

詳しくは、[非推奨（廃止予定）の機能と削除された機能のページ](deprecated-features.md)を参照してください。

**その他の変更**

* Web ログが改善されました。`logonEscalation` 警告は、管理者権限を持つユーザーに対してのみ表示されるようになりました。 （NEO-47167）
* エラー回避のために、**ヒートマップサービスのデータを収集**（collectDataHeatMapService）ワークフローはデフォルトで停止しています。 （NEO-33959）
* キャンペーンダッシュボードの CPU 使用率を最適化するために、様々な改善を実装しました。（NEO-46417）
* クラッシュを防ぐために、loadLibraryDebug JS メソッドを削除しました。（NEO-46968）
* log4j ライブラリへの残りの参照は、Windows での Campaign インストールから削除されました。 （NEO-44851）

**パッチ**

* **選択した行を結合**&#x200B;ワークフローオプションを使用できない問題を修正しました。（NEO-48488）
* Adobe Campaign Enhanced MTA を使用する場合に、**成功**&#x200B;の配信達成度が正しく更新されない問題を修正しました。（NEO-50462）
* メール配信でコンテンツの承認をリセットすると、再承認できなくなる問題を修正しました。（NEO-44259）
* 「**配信承認**」ボタンが表示されない場合がある問題を修正しました。（NEO-47547）
* 配信の「HTML」タブで、大きな HTML コードで発生する可能性があるパフォーマンスの問題を修正しました。 （NEO-47440）
* `FeatureFlag_GZIP_Compression` オプションが有効になっている場合に MID インスタンスで配信ログのステータス更新に影響を及ぼす問題を修正しました。（NEO-49183）
* トークンベースの認証を使用している場合に、実行インスタンスから iOS モバイルアプリ通知を送信できない問題を修正しました。 （NEO-45961）
* **配信品質の更新**&#x200B;ワークフロー（deliverabilityUpdate）で、同期する broadLog が多すぎるとスタックする問題を修正しました。（NEO-48287）
* **Message Center の同期**（mcSynch）ワークフローをブロックするイベントタイプの問題を修正しました。
* **クエリ**&#x200B;ワークフローアクティビティの追加データに&#x200B;**開封した受信者**（estimatedRecipientOpen）インジケーターを追加すると、エラーが発生する場合がある問題を修正しました。（NEO-46665）
* **請求**&#x200B;ワークフローで Message Center のコントロールおよび実行パッケージを同じインスタンスにインストールすると失敗する問題を修正しました。（NEO-47674）
* **請求**&#x200B;ワークフローで、プライマリキーが整数ではなく文字列として定義されたテーブルがあると失敗する問題を修正しました。（NEO-46254）
* ワークフロー名が長すぎる場合のヒートマップフィルターの問題を修正しました。 （NEO-46301）
* Snowflake FDA コネクタの 7.3.1 で発生した問題を修正しました。エンリッチメント中に「0 または 1 の基数単純結合」を使用すると、レコードが削除されていました。 （NEO-48737）
* **分割**&#x200B;ワークフローアクティビティで並べ替えパラメーターを使用する場合の、Snowflake FFDA の問題を修正しました。 （NEO-45899）
* 外部アカウント設定を保存できない問題を修正しました。 外部アカウントはパーサー機能（Snowflake と Google BigQuery）を備えたコネクタの場合、接続テスト後に自動保存されるようになりました。（NEO-47636）
* MSSQL の&#x200B;**データ更新**&#x200B;ワークフローアクティビティに時間データタイプを挿入できない問題を修正しました。（NEO-47763）
* エンジンのタイムゾーンが設定されていない場合（MSSQL に固有）に、MTA プロセスがクラッシュする問題を修正しました。 （NEO-46619）
* 画像ノード（img）にパーソナライゼーションフィールドを含む URL が含まれている場合の HTML ファイルの読み込みに関する問題を修正しました。 （NEO-48396）
* `limit` ノードが serverConf.xml ファイルで設定されていないインスタンスに接続しようとした際の HTTP 500 エラーを修正しました。
* NChar が有効になっていない Oracle Unicode データベースで `to_nclob` などの特定の関数を使用すると、「文字セットの不一致」エラーが発生する場合がある問題を修正しました。（NEO-49361）
* nmsDeliveryMapping フォルダーの読み取りアクセス権を持つユーザーがキャンペーンまたはワークフローを実行しようとするとエラーが発生する問題を修正しました。 （NEO-48230）
* `JSPContext.sqlExecWithOneParam` 関数が機能しない問題を修正しました。（NEO-50066）
* 様々なリダイレクトエラーを修正しました。 （NEO-50030）
