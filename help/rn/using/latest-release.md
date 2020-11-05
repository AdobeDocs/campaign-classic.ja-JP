---
title: 最新リリース
description: 最新の Campaign Classic リリース メモ
page-status-flag: never-activated
uuid: 269d590c-5a6d-40b9-a879-02f5033863fc
contentOwner: sauviat
products: SG_CAMPAIGN/CLASSIC
audience: rns
content-type: reference
topic-tags: latest-release-notes
discoiquuid: 5df34f55-135a-4ea8-afc2-f9427ce5ae7b
translation-type: tm+mt
source-git-commit: 48acf8cbc52a54a2dd08f0b8f29be57d4e5e006f
workflow-type: tm+mt
source-wordcount: '1824'
ht-degree: 4%

---


# 最新リリース{#latest-release}

このページでは、 **最新のCampaign Classicリリース候補バージョンに関する新機能、改善点、および修正点をリスト**&#x200B;します。

Campaign Classicゴールド標準バージョン（最新のGAビルド）については、このページ [を参照してください](../../rn/using/gold-standard.md)。

## ![](assets/do-not-localize/blue_2.png) リリース 20.3.1 - ビルド 9228 {#release-20-3-1-build-9228}

_2020年10月27日_

**新機能**

<table> 
<thead>
<tr> 
<th> <strong>iOSのプッシュ通知の機能強化</strong><br /> </th> 
</tr> 
</thead> 
<tbody> 
<tr> 
<td> <p>モバイルアプリをキャンペーンと統合する場合は、Apple Push Notification Service(APNs)との通信をセキュリティで保護する必要があります。 証明書ベースまたはトークンベースの認証を使用できます。
</p>
<p>次の2つの認証モードが、Campaign ClassicのiOSモバイルアプリで使用できるようになりました。
</p>
<ul> 
<li><p>トークンベースの認証（推奨）:この認証モードは.p8ファイルに基づいています。 この認証モードは、APNsへの各要求にトークンが含まれるたびに高速になります。 <a href="https://developer.apple.com/documentation/usernotifications/setting_up_a_remote_notification_server/establishing_a_token-based_connection_to_apns">詳細情報</a></p></li>
<li><p>証明書ベースの認証：この認証モードは.p12ファイルに基づいています。 各アプリに対して、別々の証明書が必要です。 この証明書は、Appleによって開発者アカウント経由で配信されます。 <a href="https://developer.apple.com/documentation/usernotifications/setting_up_a_remote_notification_server/establishing_a_certificate-based_connection_to_apns">詳細情報</a></p></li> 
</ul>
<p>詳細なドキュメントで、キャンペーンで認証モードを選択する方法について説明し <a href="../../delivery/using/configuring-the-mobile-application.md">ます</a>。</p>
</td> 
</tr> 
</tbody> 
</table>

<table> 
<thead>
<tr> 
<th> <strong>Androidのプッシュ通知の機能強化</strong><br /> </th> 
</tr> 
</thead> 
<tbody> 
<tr> 
<td> <p>Androidのプッシュ通知が強化され、Androidのプッシュチャネル認証用のFCM HTTP v1 APIがサポートされるようになりました。 </p>
<p>サポートされる新しいAPIバージョンで、強化されたリッチプッシュメッセージ機能を提供するFCM通知メッセージを送信できるようになりました。 <a href="https://firebase.google.com/docs/cloud-messaging/migrate-v1">詳細情報</a></p> 
<p>この節では、Android用のFCM HTTP v1 APIをAdobe Campaignして設定する方法につ <a href="../../delivery/using/configuring-the-mobile-application-android.md">いて説明します</a> 。</p>
</td> 
</tr> 
</tbody> 
</table>

**セキュリティの機能強化**

* ライブラリの安全な読み込み：DLLのプリロード攻撃から保護するため、キャンペーンは、キャンペーンクライアント(nlclient)の読み込み中に、Windowsの既定のシステムDLLパスからのみWindows DLLを読み込むようになりました。 [詳細情報](https://support.microsoft.com/en-us/help/2389418/secure-loading-of-libraries-to-prevent-dll-preloading-attacks) (NEO-24147)
* サーバー側要求偽造(SSRF)攻撃に対する保護を強化するセキュリティの問題を修正しました。 （NEO-25661）
* 受信者テーブルとの第2レベルの関係を持つカスタムテーブルからレコードを削除できないGDPRプライバシー要求を処理する際に発生していた問題を修正しました。 （NEO-25967）
* 管理者以外のユーザーがAdobe Experience Managerテンプレートを同期しようとした場合に行うAPI呼び出しを使用するセキュリティの問題を修正しました。 （NEO-23487）

**互換性の更新**

Campaign で次のシステムがサポートされるようになりました。
* iOS 14
* PostgreSQL 12
* CentOS / RedHat 8
* MSSQL2019

Learn more in the [Campaign Compatibility matrix](../../rn/using/compatibility-matrix.md).

**非推奨（廃止予定）の機能**

20.3では、次の機能が廃止されました。

* オーディエンスのAdobe Experience Cloudへの読み込みと書き出しに使用するdemdexドメインは非推奨です。 インポート/エクスポート外部アカウントにdemdexドメインを使用する場合は、それに応じて実装を適応させる必要があります。 [詳細情報](../../integrations/using/configuring-shared-audiences-integration-in-adobe-campaign.md)
* 元々oAUTH認証設定に基づいて統合認証をトリガーし、パイプラインにアクセスするための認証が変更され、AdobeI/Oに移動されました。 [詳細情報](../../integrations/using/configuring-adobe-io.md)

詳しくは、 [廃止/削除された機能ページを参照してください](../../rn/using/deprecated-features.md)。

**強化点**

* ク **ライアントコンソールには、次の機能がいくつか強化されました**。
   * 一部のインターネットセキュリティGPO規則の制限との非互換性を防ぐため、キャンペーンクライアントコンソールのログオン画面は組み込みの標準Windowsフォームに置き換えられました。
   * 64ビットのクライアントコンソールを使用したワークフローで、アクティビティのコピー/貼り付けを行うときの問題を修正しました。 （NEO-27635）
   * [ **バージョン情報** ]メニューには、64ビットと32ビットのコンソールを区別する情報が追加されています。
* ワークフローを再開する際に、ワークフロー識別子がログに表示されるようになりました。これにより、どのワークフローが再開されたかをより適切に識別できます。
* 新しい永久的なCookieが導入されました。nllastdelid。 このcookie（UUID230以外）は、deliveryIdを格納します。 セッションcookieが存在しない場合、ブロードログ情報は、このcookieに存在するdeliveryIdから取得されます。
この変更により、ブラウザーセッションの終了時に発生した問題が修正されました。deliveryIdとbroadlogIdを含むセッションcookieが削除されました。 deliveryIdがない場合、ブロードローグ情報が見つからず、永続的な追跡(最後の配信)の場合に追跡テーブル情報が見つからない問題を修正しました。
Learn more about cookies in [this section](../../platform/using/privacy-and-recommendations.md#cookies).
* 配信送信前にMTAプロセスを再起動し、配信品質サーバでの高ボリューム配信スループットパフォーマンスを改善。

**その他の変更**

* SFTPに相対パスを使用する場合、文字が自動的に追加されることはなく `~/` なりました。 必要に応じて、手動でパスに `~/` 文字を追加できますが、Adobeでは **絶対パスの使用をお勧めします**。
* Microsoft SQL Serverで新しいデータベースを構成する際に、使用可能な認証方法からWindows NT認証が削除されました。 [詳細を表示](../../installation/using/creating-and-configuring-the-database.md#step-1---selecting-the-database-engine)
* パフォーマンスを向上させるために、データベースのクリーンアップワークフローがTeradata用に最適化されました。 （NEO-19959）
* Adobe Targetからのイメージの挿入時に表示されるエラーメッセージを改善し、外部アカウントでテナント名が空であった問題を修正しました。
* 配信のプロパティで、「電子メールを **[!UICONTROL アーカイブ]** 」オプションの名前が「 **[!UICONTROL 電子メールBCC]**」に変更されました。
* 堅牢性を向上するために、selectAllクエリ（無効なノードを含む）は拒否されるようになりました。 チェックを無効にして前の動作に戻る必要がある場合は、XtkSecurity_Disable_QueryCheckを0に設定します。

**技術面の変更点**

Tomcatは、バージョン7(7.0.103)からバージョン8(8.5.57)に更新されました。

ディレクトリ `tomcat-7` は、ディレクトリに置き換えら `tomcat-8` れます。

Windowsでは、 _iis_neolane_setup.vbs_ と _apache_neolane.conf_ が( `conf``tomcat-7/conf` 以前ではなく)ディレクトリにインストールされるようになりました。

Linuxでは、 _apache_neolane.conf_`conf` がディレクトリにインストールされました。

**パッチ**

* 配信統計が再計算されない可能性がある問題を修正しました。
* 古いビルドを使用してサーバーに接続されたCampaign Classic9080ビルドを使用してCSVファイルをアップロードすると、エラーメッセージが表示される問題を修正しました。 （NEO-23218）
* 外部アカウント用のMicrosoft Dynamics CRMウィザードを構成する際にエラーメッセージが表示される問題を修正しました。 これは、最新のMS Dynamics CRM APIバージョンとの互換性の問題が原因でした。 （NEO-24528）
* ルックアップタイプレコード（他のテーブルに接続された外部キーレコードから成るデータ）をCRMコネクタを使用してCampaign ClassicからMicrosoft Dynamicsにエクスポートできない問題を修正しました。 （NEO-23864）
* CRMコネクタで[ **自動インデックス** ]オプションが有効になっている場合に、Microsoft Dynamicsデータを取得できない問題を修正しました。 （NEO-25981）
* IMS認証で、接続が終了した場合でも接続を開いたままになる可能性がある問題を修正しました。 終了した接続は、接続の蓄積やシステムリソースの消費を避けるため、終了と同時に自動的に閉じられるようになりました。 （NEO-25996）
* 外部アカウントの設定（アカウントまたはパスワードが正しくない）が誤っているために、配信のAdobe Experience Managerコンテンツの同期に失敗した場合にエラーメッセージが表示されない問題を修正しました。 失敗した場合にメッセージが表示され、問題をより簡単に識別できるようになりました。 （NEO-25586）
* 「データを更新 **」** アクティビティで「 **更新** 」操作の種類を選択すると発生していた問題を修正しました。 更新するデータが正しくない場合、ワークフローにエラーが発生し、失敗します。 データが正しくない場合、ワークフローは失敗せず、レコードは **Rejects** Outboundトランジションに保存されます。 （NEO-23794）
* サブワークフローを含むワークフローが機能しない可能性がある問題を修正しました。 （NEO-24036）
* キャンペーンテンプレートの説明を編集する際に、日本語文字などの記号をコピー&amp;ペーストすると **保存** ボタンが表示されない問題を修正しました。 （NEO-27071）
* インスタンス設定ウィザードでトラッキングサーバーを変更できない可能性がある問題を修正しました。
* 「 **保存** 」ボタンをクリックする前にウィンドウの外側をクリックした場合に、キャンペーンまたはキャンペーンテンプレートの説明が保存されない問題を修正しました。 （NEO-27449）
* 「アクティブな請求プロファイルの **数** (billingActiveContactCount)」テクニカルワークフローが機能しない可能性がある問題を修正しました。 これは、スキーマ拡張の計算済みフィールドに対してリンクが実行された場合に発生する可能性があります。 大量のデータが作成されたため、データベースの一時的な領域が不足する可能性があります。 （NEO-24062）
* ファイルの末尾に配置されている場合に、txtファイルやcsvファイルから日本語の文字をインポートできない可能性がある、 **データの読み込み（ファイル）** アクティビティの問題を修正しました。 （NEO-24957）
* 連続配信で、「 **分析開始** 」フィールドと「 **分析完了** 」フィールドが正しく入力されない可能性がある問題を修正しました。 （NEO-20755）
* クエリを **受信者** (nms:受信者)以外のスキーマでプレビューした後にSMSメッセージをメッセージ表示しようとするとエラーメッセージが表示される問題を修正しました。 （NEO-27517）
* SnowflakeFDAコネクタを使用する際の問題を修正しました。 SnowflakeFDAのアクセス名の権限を持つユーザーは、Snowflakeスキーマでクエリを実行できませんでした。 ログに「パスワードが見つかりません」というタイプのエラーが表示されました。 （NEO-23851）
* リンクされたFDAスキーマ名が現在のスキーマのFDA名のサブ文字列である場合に発生する要素コネクタを使用する際の問題を修正しました。 この問題は、例えば、FDAスキーマが「cust」で、受信者スキーマ内の要素の1つが「customer」の場合などに発生していました。 「customer」要素内の列をフェッチし、「cust」FDAスキーマから列を追加する場合、ローカル列の値が欠落していた問題を修正しました。 （NEO-20193）
* 外部データベースからレコードを取得し、キャンペーンデータベースに挿入する際のワークフローの問題を修正しました。 （NEO-26359）
* イベントの **更新ステータス** （テクニカルワークフロー）の問題を修正しました。「 **配信統計** 」アクティビティの受信対応するフィールドのサイズを一致させるために、「配信統計を **更新** 」アクティビティの3つの宛先フィールドのサイズが32ビットから64ビットに変更されました。 (NEO-11557) **更新イベントの状態** ( [更新)の詳細については、](../../workflow/using/message-center--execution-.md)この節を参照してください。
* Message Centerの **イベント履歴** レポートで、フィルターを適用しようとするとスクリプトにエラーが発生し、日付範囲でのフィルターが不可能になる問題を修正しました。 （NEO-23365）
* キャンペーンジョブ **(operationMgt)と** プレビュー **** （予測）テクニカルワークフローの間の干渉の問題を修正しました。 これは、スケジュールされた配信が「ターゲット準備完了」または「配信準備完了」のステータスのままの場合に発生していました。 （NEO-20819）
* xtkOperatorのmdataフィールドにXML識別子が存在しない場合のXML解析の問題を修正しました。 アップグレード後のエラーを引き起こしていました。 （NEO-26113）
* SSLで暗号化されたAzure外部アカウントにリンクされた **File Transfer** アクティビティを使用する場合に、HTTPSではなくHTTPを使用して接続が行われた問題を修正しました。 （NEO-26720）
* MSSQLデータベースで、クリーンアップワークフロー中にup_updatestatsプロシージャでエラーが発生する可能性がある問題を修正しました。
* インタラクション要求がまだ処理中の場合に、Webプロセスのシャットダウン中に発生するクラッシュを修正しました。 （NEO-26447）
* Oracle DBの **NoNull** 関数が、9032のアップグレード後に機能しなくなる問題を修正しました。 （NEO-26488）
* Message CenterパッケージがないLINEV2パッケージがインストールされた場合、アップグレード後にトラッキングワークフローが失敗する問題を修正しました。
* 属性&#39;APP&#39;のデータベース接続文字列が無効な値を取得することになったため、接続プールを必要な接続数まで増やせなかったスケーラビリティの問題を修正しました。 （NEO-25105）
* Windows 10の最新の更新後にAdobe Campaignにログインできなかった、プロキシ設定レベルの問題を修正しました。 （NEO-27813）
* トラッキングリンクを含むHTMLテンプレートをインポートした後、配信された電子メールに不要なURLが表示される問題を修正しました。 （NEO-25909）
* ワークフローの **分割** アクティビティの残りのターゲットデータを表示すると、サーバーがクラッシュする問題を修正しました。
* 式パーサーをクリーニングする際にメモリの破損を防ぐことで、サーバーのクラッシュの問題を修正しました。 （NEO-26856）
* エンリッチメントアクティビティで管理者以外のユーザーがインスタンス変数を定義していた問題を修正しました。 （NEO-25653）