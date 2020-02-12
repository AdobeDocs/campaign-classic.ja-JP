---
title: 最新リリース
description: Campaign Classic 19.2リリースノート
page-status-flag: never-activated
uuid: 269d590c-5a6d-40b9-a879-02f5033863fc
contentOwner: sauviat
products: SG_CAMPAIGN/CLASSIC
audience: rns
content-type: reference
topic-tags: latest-release-notes
discoiquuid: 5df34f55-135a-4ea8-afc2-f9427ce5ae7b
index: y
internal: n
snippet: y
translation-type: tm+mt
source-git-commit: 03cba38dc2c9e10396feddc38cca6a6073e932d5

---


# 最新リリース{#latest-release}

[アップグレードの構築](https://helpx.adobe.com/campaign/kb/acc-build-upgrade.html) |コント [ロールパネルのリリース](https://docs.adobe.com/content/help/en/control-panel/using/release-notes.html) |ドキュメ [ントの更新](../../rn/using/documentation-updates.md) |以 [前のリリース](../../rn/using/release--19-1.md) |非推 [奨の機能](https://helpx.adobe.com/campaign/kb/deprecated-and-removed-features.html)

<table> 
 <tbody> 
  <tr> 
   <td><img src="assets/green3.png"/><strong>一般公開</strong></td>
   <td><img src="assets/blue3.png"/><strong>リリース候補</strong></td> 
   <td><img src="assets/orange3.png"/><strong>使用できなくなりました</strong></td> 
   <td><img src="assets/red3.png"/><strong>廃止</strong></td> 
  </tr> 
   <tr> 
   <td>最新の安定したビルドが利用可能です。 <br>ビルドは実稼働環境で検証されました。 </td>
   <td>ビルドはアドビによって検証されます。 <br>製品の校正を待っています。 </td>
   <td>新しいビルドにバグ修正が加えられました。 <br>更新が必要です。 </td>
   <td>既知の回帰を含みます。 <br>更新は必須です。 </td>
  </tr> 
 </tbody> 
</table>

ここをク [リックし](../../rn/using/release--19-1.md#release-19-1-4-build-9032) 、最後の安 **定ビルド** (GA)を表示します。

## ![](assets/orange2.png) リリース19.2.2 — ビルド9081 {#release-19-2-2-build-9081}

2020年2月7日_

**強化点**

* SSL証明書の導入によるWindowsサーバーでのユーザー接続の失敗による問題を修正しました。 （NEO-20629）
* バージョン情報メニューに誤ったバージョンタグ番号が表示される問題を修 **正し** ました。

## ![](assets/orange2.png) リリース19.2 — ビルド9080 {#release-19-2-build-9080}

_2019年12月2日_

**新機能?**

<table> 
 <thead> 
  <tr> 
   <th> <strong>カリフォルニア消費者プライバシー法(CCPA)</strong><br /> </th> 
  </tr> 
 </thead> 
 <tbody> 
  <tr> 
   <td> <p>CCPAは、2020年1月1日に施行されるデータ保護要件を調和させ、最新化するカリフォルニア州の新しいプライバシー法です。 CCPAは、カリフォルニアに居住するデータサブジェクトのデータを保持するAdobe Campaignのお客様に適用されます。</p>
    <p> Adobe Campaignは、既に利用可能なプライバシー機能（同意管理、データ保持設定、ユーザーの役割を含む）に加えて、CCPAの準備を容易にします。</p>
    <ul>
      <li>アクセス権と削除権：GDPR用に追加された機能を活用しています。 <a href="https://helpx.adobe.com/campaign/kb/acc-privacy.html#righttoaccess">詳細を表示</a></li>
      <li>顧客が個人情報の販売をオプトアウトしたかどうかを追跡できます。 この場合は、プロファイルテーブルを拡張し、CCPAのオプトアウトフィ <strong>ールドを追加する必要があります</strong> 。 <a href="https://helpx.adobe.com/campaign/kb/acc-privacy.html#ccpa">詳細を表示</a></li></td> 
  </tr> 
 </tbody> 
</table>

<table> 
 <thead> 
  <tr> 
   <th> <strong>ワークフローライブ監視</strong><br /> </th> 
  </tr> 
 </thead> 
 <tbody> 
  <tr> 
   <td> <p>事前定義されたビューを使用して、インスタンス上のすべてのワークフローの実行ステータスを監視できるようになりました。</p>
   <p>詳しくは、<a href="../../workflow/using/monitoring-workflow-execution.md#filtering-workflows-status">詳細ドキュメント</a>を参照してください。</p></td> 
  </tr> 
 </tbody> 
</table>


<table> 
 <thead> 
  <tr> 
   <th> <strong>AMPを使用したインタラクティブコンテンツ</strong><br /> </th> 
  </tr> 
 </thead> 
 <tbody> 
  <tr> 
<td> <p>Adobe Campaignでは、新しいEmail <a href="https://amp.dev/about/email/">Formatのインタラクティブ</a> AMPを試すことができます。これにより、マーケターは、メッセージ内にAMPコンポーネントを含め、メッセージ自体に直接アクション可能なリッチで動的なインタラクティブなコンテンツを使用して、電子メールエクスペリエンスを強化できます。</p>
   <p> この機能はパブリックベータ版としてリリースされています。</p>
   <p>For more information, refer to the <a href="../../delivery/using/defining-interactive-content.md">detailed documentation</a> and the <a href="https://docs.adobe.com/content/help/en/campaign-learn/campaign-classic-tutorials/sending-messages/email-channel/defining-interactive-email-content-with-amp.html">tutorial video</a>.</p><br /></td> 
  </tr> 
 </tbody> 
</table>


<table> 
 <thead> 
  <tr> 
   <th> <strong>セキュア SMS メッセージ（TLS）</strong><br /> </th> 
  </tr> 
 </thead> 
 <tbody> 
  <tr> 
<td> <p>拡張された汎用 SMPP コネクタでセキュア SMS がサポートされるようになりました。これにより、プロバイダーへの接続を暗号化できます。</p> <p><strong>警告</strong> この機能を使用するには、すべてのサーバーで最新の証明書が必要です。 無効な証明書、失効した証明書、または期限切れの証明書は、SMS送信機能全体に影響を与えるエラーを生成します。</p><p>詳しくは、<a href="https://helpx.adobe.com/campaign/kb/sms-connector-protocol-and-settings.html">詳細ドキュメント</a>を参照してください。 </p> </td> 
  </tr> 
 </tbody> 
</table>

**セキュリティの機能強化**

* キャンペーンインターフェイスのストアドクロスサイトスクリプティングの脆弱性（入力データの検証と出力エンコーディング）を修正。 （NEO-16810）
* ログイン制限ポリシーを強化して、権限のないデータへのアクセスを許可する可能性がある、プロファイル承認のセキュリティの問題を修正しました。 （NEO-14445）

**強化点**

* プッシュ通知のメモリ消費の最適化を参照してください。
* パフォーマンスとストレージの最適化のために、 **logins.logファイルの処理が強化され** 、 現在は、ファイルは複数のファイルに分割され、1日に1つ、最大365個のファイルが保持されます。 [詳細を表示](../../production/using/log-files.md)
* Microsoft Dynamics CRM外部アカウントは、パスワード資格情報（パスワード+ユーザー名）または証明書（秘密キー）を使用して構成できるようになりました。 [詳細を表示](../../platform/using/external-accounts.md#microsoft-dynamics-crm-external-account)
* Hadoop FDAコネクターに、信頼性を向上させるための機能がいくつか強化されました
* サーバー上のパブリックリソースのアップロードを許可する前に、ディスク領域を確認するために、特定のガードレールが追加されました。
* 新しいキ [ャンペーンオプション](../../installation/using/configuring-campaign-options.md) が追加されました。
   * WdbcKillSessionPolicy構成オ **プションを使用すると** 、すべてのワークフローとPostgreSQLデータベースクエリに対し **** て無条件停止動作に影響を与えることができます。
   * NmsOperation_ **DeliveryPreparationWindowオプションを使用すると** 、ステータスが一貫しない配信が実行中の配信の数から除外される日数を定義できます。
   * WdbcOptions_ **TempDbName** オプションを使用すると、Microsoft SQL server上でテーブルを作業するための別のデータベースを構成できます。 これにより、バックアップとレプリケーションが最適化されます。 [詳細を表示](../../production/using/rdbms-specific-recommendations.md#microsoft-sql-server)
   * PostgreSQLの **** XtkCleanup_NoStatsオプションが強化され、データベースクリーンアップワークフローのストレージ最適化手順の動作をより適切に制御できるようになりました。 [詳細を表示](../../production/using/database-cleanup-workflow.md#statistics-update)
* アカウントのロックアウトメカニズムが **logon()** APIに追加されました。 特定の期間内に連続してログインに失敗した回数が経過した場合、それ以降のログインは試行されません。
* 配信プロパティの新しい **「** Maximum personalization run time」オプションを使用すると、パーソナライゼーションの実行時間のタイムアウト期間を定義して、パーソナライゼーションフェーズが長時間実行されないようにすることができます。 [詳細を表示](../../delivery/using/personalization-fields.md#timing-out-personalization)
* SFTP接 **** 続にプロキシ設定を使用できるように、ftpプロトコルオプションが追加されました。 [詳細を表示](../../installation/using/configuring-campaign-server.md#proxy-connection-configuration)
* オンプレミス環境でのSFTP外部サーバーへのプロキシアクセスの新しいサポート。
* 特定のガードレールが追加され、Campaignインスタンスと互換性のないパッケージのインストールを防止しました。 [詳細を表示](../../installation/using/installing-campaign-standard-packages.md)

_廃止されたシステム_

Campaign Classicの導入では、次のシステムが廃 [止され](https://helpx.adobe.com/campaign/kb/deprecated-and-removed-features.html) ました。
* Apache 2.2
* セントス6

最新のキャンペーン互換性マトリックスに記載されているシステムのサポート対象バージョンを使用していることを確認してください。 [詳細を表示](https://helpx.adobe.com/campaign/kb/compatibility-matrix.html)

_Campaign Mobile SDK_

iOS SDKのビルド1.0.26が利用できるようになりました。 この新しいビルドでは、iOS 13のサポートが追加されました。 この新しいバージョンでは、通知の優先順位と、iOS 13プッシュ通知用の新しい登録トークン管理プロセスがサポートされるようになりました。 以前のバージョンのSDKでアプリケーションを実行している場合は、新しいSDKでアプリケーションを再コンパイルする必要があります。 SDKを入手するには、アドビカスタマーケアにお問い合わせください。

**パッチ**

* データ読み込み(RDBMS)ワークフローアクティビティで空のリンクテーブルを追加すると発生する **可能性があるコンソールのクラッシュを修正** しました。 （NEO-12213）
* 中間ソーシングサーバーで処理されない特定のメッセージが発生する可能性がある問題を修正しました。 （NEO-12395）
* Teradataでクエリバンディングオプションを使用する場合の、データベースクリーンアップワークフローの問題を修正しました。 （NEO-12399）
* ne.jpドメインを含むタイポロジルールを使用した配信分析に影響する問題を修正しました。 （NEO-12609）
* TLS上でのSMSの更新に関連する問題が修正され、より制限的な証明書ポリシーが必要になる問題を修正しました。 これらの更新により、古い証明書が使用されている場合に、マーケティングサーバーと中間ソーシングサーバーの間の接続に失敗する可能性があります。 （NEO-17698）
* Vault認証を使用する中間ソーシング環境で **外部アカウントで** 「接続のテスト」ボタンを使用する際に発生していた問題を修正しました。 （NEO-12722）
* FDA Hadoop接続で日付関数を使用するクエリに関する問題を修正しました。 （NEO-12847）
* 電子メールエディターで画像を置き換える際の問題を修正しました。 （NEO-13098）
* 削除されたか別の場所に移動されたフォルダーのアップグレード後のエラーが発生する可能性がある問題を修正しました。 （NEO-13118）
* LINEメッセージで「デバイスの画面サイズごとに画像を定義 **」オプションを使用すると** 、画像の表示に関する問題を修正しました。 （NEO-13228）
* 「配信中に重複した住所を除外」オプションが選択さ **れていない場合の配信準備の問題** を修正しました。 （NEO-13240）
* 「転送後にソースファイルを削除」オプションを使用して **File転送アクティビティを使用し** 、 **Delete the source files after transfer** （転送後ソースファイルを削除）オプションを使用してファイルをダウンロードする場合のワークフローで、名前にスペース文字が含まれていた問題を修正しました。 （NEO-13411）
* Tomcatキャッシュのクリーンアップでメモリの問題が発生する問題を修正しました。 （NEO-13456）
* Microsoft SQL 2017で実行中の既存のコントロールインスタンスに、実行インスタンス **（組み込みパッケージ）を含むオファーエンジンのコントロール(** Control)をインストールする際の問題を修正しました。 （NEO-13539）
* 電子メール内の追跡対象URLを「テキストコンテンツ」タブからチェック解除すると発生する可能性があるコンソール **のクラッシュを修正** 。 （NEO-13545）
* 中国語の送信者名のエンコードの問題を修正しました。 （NEO-13837）
* エクスプローラーから調査回答データを表示すると発生する可能性があるエラーを修正しました。 （NEO-14590）
* 配信ログの分類と検疫テーブルの間で不一致が生じる可能性がある問題を修正しました。 （NEO-16547）
* 電子メールに埋め込まれなかったDKIMキーの問題を修正しました。 （NEO-16804）
* API呼び出しのコンテキストで無効なセッショントークンが使用されてイベントをトリガーする場合に、誤ったエラーコードが表示される問題を修正しました。 エラーコードが「HTTP 403 Forbidden」ではなく「HTTP 200 OK」でした。 （NEO-16826）
* Webアクセスを介して配信レポートを表示する際の問題を修正しました。 （NEO-17015）
* Adobe Campaignにログインする際のIMS認証の問題を修正しました。 （NEO-17312）
* 検疫済みの電子メールがプライバシー管理プロセスで削除されない問題を修正しました。 （NEO-17314）
* SQLデータベースを使用して9031にアップグレードした後のスループットの問題を修正。 （NEO-17558）
* Salesforceを使用したCRM Connectorに影響を与えていた問題を修正しました。 （NEO-17712）
* 外部SFTPからデータをインポートする際のタイムアウトの問題を修正しました。 （NEO-19723）
* 予測モデルにアクセスする際の問題を修正しました。 （NEO-19713）
* Hadoop FDAデータベースを使用した **Split** workflowアクティビティでのランダムサンプリングに影響する問題を修正しました。 （NEO-16636）

