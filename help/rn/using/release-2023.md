---
product: campaign
title: Campaign Classic 2023 リリース
description: Campaign Classic 2023 リリースの詳細
feature: Release Notes
role: User
level: Beginner
exl-id: 8ed11e96-9f23-4e2e-bae2-25c51cfb549a
source-git-commit: 728848eab059fc669c241346a2ff1feebd79222c
workflow-type: ht
source-wordcount: '2337'
ht-degree: 100%

---

# 2023 リリース{#release-2023}

## リリース 7.3.5 - ビルド 9368 {#release-7-3-5}

[!BADGE 限定提供（LA）]{type=Informative url="https://experienceleague.adobe.com/docs/campaign-classic/using/release-notes/rn-overview.html?lang=ja#rn-statuses" tooltip="限定提供（LA）"}

_2023年12月5日（PT）_

### セキュリティの機能強化 {#release-7-3-5-security}


* Campaign Classic v7.3.5 では、認証プロセスが改善され、セキュリティが強化されました。テクニカルオペレーターは、Adobe Identity Management System（IMS）を使用して Campaign に接続する必要があります。既存のテクニカルアカウントを移行する方法については、[このテクニカルノート](../../technotes/using/ims-migration.md)を参照してください。

* また、セキュリティと認証プロセスを強化する取り組みの一環として、Adobe Campaign では、エンドユーザー認証モードをログイン／パスワードのネイティブ認証から Adobe Identity Management System（IMS）に移行することを強く推奨しています。オペレーターを移行する方法については、[このテクニカルノート](../../technotes/using/migrate-users-to-ims.md)を参照してください。

* 現在、Web フォームのステータスが&#x200B;**保留中の公開**&#x200B;になっている場合、自動的にライブにならなくなります。セキュリティの問題を防ぐには、**オンライン**&#x200B;になる前に公開し、Web ブラウザーの Web フォーム URL からアクセスする必要があります。[詳細情報](../../web/using/publishing-a-web-form.md#life-cycle-of-a-form)

### その他の機能強化 {#release-7-3-5-other}

このリリース以降も、既に送信済みのメールのトラッキングリンクは、アップグレード中も引き続き機能します。[詳細情報](../../platform/using/faq-build-upgrade.md)

### パッチ {#release-7-3-5-patches}

* Google Big Query データベースのデータを使用し、Oracle データベースのデータを更新する際の問題を修正しました。ワークフロー一時テーブルですべてのキーを `0` に設定しました。（NEO-65091）
* Google Big Query データベース上の 2 つのクエリを&#x200B;**和集合**&#x200B;ワークフローアクティビティで組み合わせると、ワークフローの実行が失敗する原因となっていた問題を修正しました。（NEO-63705）
* キャンペーンレポートで `Back` ボタンをクリックした際に、ユーザーに再認証をリクエストしていた問題を修正しました。（NEO-65087）
* 配達確認の前に配信を削除した際に発生していた、データベースクリーンアップワークフローのエラーを修正しました。（NEO-48114）
* クライアントコンソールへの接続時に、TLS 検証に関する最近の更新により、接続エラーが発生していた問題を修正しました。（NEO-50488）
* Campaign の 7.3.1 へのアップグレード後の HTTP プロキシ認証に関する問題を修正しました。Campaign ワークフローの HTTP リクエストが `error 407 – proxy auth required is returned` で失敗していました。（NEO-49624）
* **スクリプト**&#x200B;ワークフローアクティビティにおける、GPG 復号化での断続的なエラーを修正しました。関連するエラーメッセージは `gpg: decryption failed: No secret key` でした。（NEO-50257）
  <!--* Workflow temporary tables now have a primary index in Teradata with a Federated Data Access (FDA) connection. (NEO-62575)-->




## リリース 7.3.4 - ビルド 9364 {#release-7-3-4}

[!BADGE 限定提供（LA）]{type=Informative url="https://experienceleague.adobe.com/docs/campaign-classic/using/release-notes/rn-overview.html?lang=ja#rn-statuses" tooltip="限定提供（LA）"}


>[!CAUTION]
>
>コンソールのアップグレードは必須です。クライアントコンソールのアップグレード方法について詳しくは、こちらの[ページ](../../installation/using/installing-the-client-console.md)を参照してください。
>
>[Campaign - Microsoft Dynamics CRM コネクタ](../../platform/using/crm-connectors.md)を使用している場合は、マーケティングサーバーとミッドソーシングサーバーの両方をこの新しいビルドでアップグレードする必要があります。

_2023年9月7日（PT）_

### セキュリティの機能強化 {#release-7-3-4-security}

* IMS API のセキュリティが向上しました。クライアントの機密情報（アクセストークン）が URL パラメーターから削除されました。これらの資格情報は POST データまたは認証ヘッダーに送信されるようになり、通信プロセスのセキュリティが向上します。（NEO-63045）
* DDOS 攻撃を防ぐために、web アプリのセキュリティが向上しました。（NEO-50757）
* PII データが web ログエラーに公開されないように、セキュリティが強化されました。（NEO-46827）
* セキュリティトークンが Campaign ホームページの URL に含まれないように、セキュリティが最適化されました。（NEO-38519）

### 互換性のアップデート  {#release-7-3-4-compat}

* Tomcat がバージョン 8.5.91 に更新されました
* libexpat ライブラリは、セキュリティを向上させるために 2.5.0 に更新されました。（NEO-51023）

### 改善点 {#release-7-3-4-improvements}

* 配信用のメモリ割り当てを最適化するために、サーバー設定ファイル（serverConf.xml）の MaxWorkingSetMb パラメーターが変更されました。（NEO-49204）
* BigQuery 外部アカウントが強化され、GCloud SDK の設定に使用する新しいオプションが追加されました。（NEO-63879）[詳細情報](../../installation/using/configure-fda-google-big-query.md#google-external)
* 新しい `cusHeader` セクションがサーバー設定ファイル（serverConf.xml）に追加されました。外部サーバーからファイルをアップロードする際に、カスタムヘッダーを追加できます。（NEO-58339）[詳細情報](../../installation/using/the-server-configuration-file.md#cusheaders)。
* トラッキングログ管理が改善され、lastMsgId の負の ID が回避されるようになりました。int32 から int64 に変更されました。（NEO-52290）
* ミッドソーシング（配信統計）ワークフローが標準で追加されました。この新しいワークフローは、配信統計データ（nms:deliveryStat）をミッドインスタンスからマーケティングインスタンスまで同期します。（NEO-36802）

### パッチ {#release-7-3-4-patches}

* サービスリクエスト呼び出しの認証でサービストークンを使用していた場合に、IMS ログイン前にサービスリクエストが行われた際に発生する可能性がある問題を修正しました。（NEO-64903）
* デジタルコンテンツエディターの使用時にスクロールの問題が発生する可能性があるリグレッションの問題を修正しました。（NEO-64671、NEO-59256）
* Excel からデジタルコンテンツエディターにコンテンツをペーストする際のリグレッションの問題を修正しました。（NEO-63287）
* v5 互換性モードで web アプリが正しく表示されない可能性がある問題を修正しました。（NEO-63174）
* 管理者以外のオペレーターが webAnalytics 配信を送信できない問題を修正しました。（NEO-62750）
* 配信で条件付きコンテンツを使用する際に、ブラウザーで余分なスペースを追加できない問題を修正しました。（NEO-62132）
* 複数のログスキーマに関連付けられたターゲットスキーマを使用する際に、請求ワークフローでアクティブな連絡先の計算が正しく機能しないというリグレッションの問題を修正しました。（NEO-61468）
* 配信のコンテンツを編集する際にエラーが発生し、スクロールできなくなる可能性がある問題を修正しました。（NEO-61364）
* メールコンテンツエディターで画像をクリックすると、ポップアップウィンドウが開く問題を修正しました。（NEO-60752）
* 複数のブラウザーで配信の HTML コンテンツ内の特殊文字が誤ってエンコードされる可能性がある問題を修正しました。（NEO-60081）
* inSMS ワークフローアクティビティの使用時に発生する可能性がある同期の問題を修正しました。（NEO-59544）
* タイムスタンプフィールドまたは日時フィールドで Big Query コネクタを使用する際の問題を修正しました。（NEO-59502、NEO-49768）
* 累積配信レポートを使用できない問題を修正しました。（NEO-59211）
* オーディエンスを People コアサービスと共有する際にエラーが発生する可能性がある問題を修正しました。（NEO-58637）
* 配信のミラーページを表示する際の問題を修正しました。（NEO-58325）
* XtkLibrary.Right() xtk 式が機能しない問題を修正しました。（NEO-57870）
* デジタルコンテンツエディターで画像をアップロードする際に、本文タグのスタイル属性が変更される問題を修正しました。（NEO-57697）
* CRM コネクタアクティビティで一括エクスポートを実行する際の特殊文字に関する問題を修正しました。（NEO-54300）
* データの読み込みアクティビティと Big Query コネクタを使用する際に、一括読み込みが「文字列」データタイプで機能しない問題を修正しました。（NEO-53748）
* オファーのレンダリングの問題を引き起こす可能性があるキャッシュのキーの問題を修正しました。（NEO-51516、NEO-49995）
* 承認付きの targetMapping を使用してダイレクトメール配信を送信する際に、検証エラーが発生する可能性がある問題を修正しました。（NEO-50758）
* 配信パフォーマンスに影響を与える可能性があるクエリ管理の問題を修正しました。（NEO-49991）
* キャンペーンワークフローの配信アクティビティで外部アカウントを使用する際に、外部アカウントの設定に関する問題が発生する可能性がある問題を修正しました。（NEO-49959）
* プッシュ通知を送信する際のパフォーマンスの問題を修正しました。（NEO-49953）
レポートのエクスポート時に日本語の文字が正しく表示されないことがある問題を修正しました。（NEO-49308）
* Tomcat エラーレポートに過剰なエラー詳細が表示される原因となった問題を修正しました。（NEO-49029）
* 多数のオファーを使用すると配信エラーが発生することがある問題を修正しました。（NEO-48807）
* **データを更新**&#x200B;ワークフローアクティビティが正しく機能しないことがある問題を修正しました。（NEO-48140）
* メールとは異なる外部アカウントを使用する配信で、クリックの追跡データが同期されないことがある問題を修正しました。（NEO-47277）
* Message Center のマーケティングインスタンスでリアルタイムトラッキングログが同期されなくなることがある問題を修正しました。（NEO-42540）
* Snowflake データベーステーブルのスキーマの検出ウィンドウにワークスペースプレフィックスが表示されない問題を修正しました。（NEO-40297）
* メールコンテンツ内で `<img-amp>` タグが機能しない問題を修正しました。（NEO-38685）
* HTTP リレーの使用時に Message Center のアーカイブワークフローが失敗することがある問題を修正しました。（NEO-33783）
* メールコンテンツエディターでフォント名とサイズのエラーが発生することがある問題を修正しました。（NEO-61342）

## リリース 7.3.3 - ビルド 9359 {#release-7-3-3}

[!BADGE 限定提供（LA）]{type=Informative url="https://experienceleague.adobe.com/docs/campaign-classic/using/release-notes/rn-overview.html?lang=ja#rn-statuses" tooltip="限定提供（LA）"}

>[!AVAILABILITY]
>
>環境に他のパッチが適用されていない場合、このバージョンでは特定の Campaign v7.3.3.IMS パッチアップグレードを使用できます。これにより、[v7.3.5 に伴う Adobe Identity Management System（IMS）セキュリティの更新](#release-7-3-5-security)が既存の v7.3.3 環境に適用されます。


_2023年3月20日（PT）_


### セキュリティの強化 {#release-7-3-3-security}

* Tomcat は、セキュリティを最適化するために、バージョン 8.5.81 から 8.5.85 に更新されました。（NEO-56936）


### 改善点 {#release-7-3-3-improvements}

* 請求ワークフローを改善し、パフォーマンスを最適化しました。（NEO-47658）
* トラッキングワークフローを改善し、配信サイズが大きい場合のパフォーマンスを最適化しました。（NEO-45064）
* トラッキング管理を改善し、URL の動的パラメーターで発生する可能性がある問題を修正しました。トラッキング管理 v3 では、ajax タイプの URL（「#」の後のパラメーターを含む）を処理し、サードパーティツールによるトラッキング URL を変更するのを防ぎます。この変更を適用するには、アドビにお問い合わせください。（NEO-46535）
* このリリース以降も、既に送信済みのメールのトラッキングリンクは、アップグレード中も引き続き機能します。[詳細情報](../../platform/using/faq-build-upgrade.md)

<!--To apply this change, the marketing, tracking and mid servers need to be updated to 7.3.3. To enable the new tracking management mode, set the `emailLinksVersion` parameter to '3' in the configuration file of the marketing server. (NEO-46535)-->

>[!CAUTION]
>
>コンソールのアップグレードは必須です。クライアントコンソールのアップグレード方法について詳しくは、こちらの[ページ](../../installation/using/installing-the-client-console.md)を参照してください。

### パッチ {#release-7-3-3-patches}

* コントロールインスタンス（トランザクションメッセージコンテキスト）から iOS の配達確認のプッシュ通知が送信されない問題を修正しました。（NEO-54713）
* デジタルコンテンツエディター（DCE）の「**編集**」タブでスクロールできない問題を修正しました。（NEO-54474）
* 2 つのエンリッチメントアクティビティがリンクで同じ名前識別子を使用していた場合に、2 つ目のエンリッチメントアクティビティが最初のエンリッチメントアクティビティのリンクを使用する問題を修正しました。（NEO-48851）

## リリース 7.3.2 - ビルド 9356 {#release-7-3-2}

[!BADGE 限定提供（LA）]{type=Informative url="https://experienceleague.adobe.com/docs/campaign-classic/using/release-notes/rn-overview.html?lang=ja#rn-statuses" tooltip="限定提供（LA）"}


>[!AVAILABILITY]
>
>環境に他のパッチが適用されていない場合、このバージョンでは特定の Campaign v7.3.2.IMS パッチアップグレードを使用できます。これにより、[v7.3.5 に伴う Adobe Identity Management System（IMS）セキュリティの更新](#release-7-3-5-security)が既存の v7.3.3 環境に適用されます。

_2022 年 11 月 21 日（PT）_

### 互換性のアップデート {#release-7-3-2-compat}

* Adobe Campaign に、PostgreSQL 14 との互換性が備わりました。詳しくは、この[テクニカルノート](../../technotes/using/tech-stack-upgrade.md)を参照してください。

* Microsoft Internet Explorer 11 のサポート終了に伴い、クライアントコンソールのダッシュボードの HTML レンダリングエンジンは、Edge Chromium を使用するようになりました。（NEO-20741）

詳しくは、[Campaign 互換性マトリックス](../../rn/using/compatibility-matrix.md#RDBMSservers)を参照してください。

>[!CAUTION]
>
>コンソールのアップグレードは必須です。クライアントコンソールのアップグレード方法について詳しくは、こちらの[ページ](../../installation/using/installing-the-client-console.md)を参照してください。

### 改善点 {#release-7-3-2-improvements}

* Google BigQuery コネクタがブール値フィールドを完全にサポートするようになりました。 （NEO-49181）
* serverConf.xml ファイルの `Configuration for the redirection service` セクションで、IMS Cookie の有効期間を設定できるようになりました。これは、次の Cookie（`uuid230`、`nllastdelid` および `AMCV_`）に適用されます（NEO-42541）。
* serverConf.xml ファイルのリダイレクトノードで `showSourceIP` を false に設定することで、「/r/test」リクエストで IP を非表示にできるようになりました。[詳細を表示](../../installation/using/the-server-configuration-file.md#redirection-redirection)（NEO-46656）
* このリリース以降も、既に送信済みのメールのトラッキングリンクは、アップグレード中も引き続き機能します。[詳細情報](../../platform/using/faq-build-upgrade.md)


### 非推奨（廃止予定）の機能  {#release-7-3-2-deprecated}

* Facebook を使用したソーシャルマーケティングは非推奨（廃止予定）になりました。X（旧 Twitter）統合を使用してソーシャルメディアに投稿したり、アドビと連携してカスタムチャネルを作成したりできます。
* ACS コネクタ（プライムオファー）は非推奨（廃止予定）となりました。 Campaign のエクスポート／インポート機能を使用して、両方の製品のデータを抽出および挿入できます。

詳しくは、[非推奨（廃止予定）の機能と削除された機能のページ](deprecated-features.md)を参照してください。

### その他の変更  {#release-7-3-2-other}

<!--* Web logs have been improved: `logonEscalation` warnings are now only displayed for users with admin privileges. (NEO-47167)-->
* エラー回避のために、**ヒートマップサービスのデータを収集**（collectDataHeatMapService）ワークフローはデフォルトで停止しています。 （NEO-33959）
* キャンペーンダッシュボードの CPU 使用率を最適化するために、様々な改善を実装しました。（NEO-46417）
* クラッシュを防ぐために、loadLibraryDebug JS メソッドを削除しました。（NEO-46968）
* log4j ライブラリへの残りの参照は、Windows での Campaign インストールから削除されました。 （NEO-44851）

### パッチ {#release-7-3-2-patches}

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
