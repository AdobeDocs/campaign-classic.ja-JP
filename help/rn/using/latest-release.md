---
title: 最新リリース
description: 最新リリース
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
source-git-commit: cb55216e75559e1ce7eefa24d2302fe2c2224d40
workflow-type: tm+mt
source-wordcount: '1739'
ht-degree: 14%

---


# 最新リリース{#latest-release}

[ビルドアップグレード](https://helpx.adobe.com/jp/campaign/kb/acc-build-upgrade.html) | [コントロールパネルのリリース](https://docs.adobe.com/content/help/ja-JP/control-panel/using/release-notes.html) | [ドキュメントの更新](../../rn/using/documentation-updates.md) | [以前のリリース](../../rn/using/release--20-1.md) | [非推奨（廃止予定）の機能](../../rn/using/deprecated-features.md)

<table> 
 <tbody> 
  <tr> 
   <td><img src="assets/do-not-localize/green3.png"/><strong>一般公開（GA）</strong></td>
   <td><img src="assets/do-not-localize/blue3.png"/><strong>リリース候補</strong></td> 
   <td><img src="assets/do-not-localize/orange3.png"/><strong>公開停止</strong></td> 
   <td><img src="assets/do-not-localize/red3.png"/><strong>非推奨（廃止予定）</strong></td> 
  </tr> 
   <tr> 
   <td>最新の安定したビルド。ビルドは本番環境で検証済みです。<br></td>
   <td>アドビが検証済みのビルド。本番環境での検証待ちです。<br></td>
   <td>バグ修正を含む、新しいビルドがあります。更新が必要です。<br></td>
   <td>新たな不具合を含むことがわかっています。必ず更新が必要です。<br></td>
  </tr> 
 </tbody> 
</table>

**最新の安定したビルド**&#x200B;は 9032（3a9dc9c）です。[ここ](../../rn/using/release--19-1.md#release-19-1-4-build-9032)をクリックしてください

## ![](assets/do-not-localize/blue_2.png) リリース 20.2.1 - ビルド 9178 {#release-20-2-1-build-9178}

_2020年6月8日_

**新機能**

<table> 
 <thead> 
  <tr> 
   <th> <strong>顔文字のサポート</strong><br /> </th> 
  </tr> 
 </thead> 
 <tbody> 
  <tr> 
   <td> <p>キャンペーンでメッセージをデザインする場合、専用のボタンを使用して、メッセージの本文に簡単に顔文字を挿入できるようになりました。 電子メールの件名行に追加することもできます。 インターフェイスで使用可能な顔文字のリストをカスタマイズできます。</p>
    <p>顔文字の追加について詳しくは、 <a href="../../delivery/using/defining-the-email-content.md#inserting-emoticons">詳細なドキュメントを参照してください</a>。 このセクションでは、絵文字のリストをカスタマイズ <a href="../../delivery/using/customizing-emoticon-list.md">する方法を説明します</a>。</p>
   </td> 
  </tr> 
 </tbody> 
</table>

<table> 
 <thead> 
  <tr> 
   <th> <strong>Azure SynapseFDAコネクタ</strong><br /> </th> 
  </tr> 
 </thead> 
 <tbody> 
  <tr> 
   <td> <p>これで、キャンペーンインスタンスをAzure Synapse外部データベースに接続できます。 この接続は、新しい外部アカウントで管理されます。</p>
    <p>Azure Synapseは、ハイブリッドおよびオンプレミスの環境でのみ使用できます。 詳しくは、<a href="../../platform/using/specific-configuration-database.md#configure-access-to-azure-synapse">詳細ドキュメント</a>を参照してください。</p>
   </td> 
  </tr> 
 </tbody> 
</table>

<table> 
 <thead> 
  <tr> 
   <th> <strong>タイとブラジルのプライバシーに関する法律</strong><br /> </th> 
  </tr> 
 </thead> 
 <tbody> 
  <tr> 
   <td> <p>タイの個人データ保護法(PDPA)は、タイのデータ保護要件を調和・最新化する新しいプライバシー法です。 </p>
   <p>ブラジルのゲラル・デ・プロテサレウ・デ・ダドス(LGPD)は、8月16日から、ブラジルで個人データを収集し、処理するすべての会社に対して有効となる。</p>
   <p>本規則は、これらの国に居住するデータ・サブジェクトのデータを保持するAdobe Campaignのお客様に適用されます。 キャンペーンで既に利用可能なプライバシー機能（同意管理、データ保持設定、ユーザーの役割など）に加え、PDPAおよびLGPDの準備を容易にするための追加機能を追加する予定です。</p>
   <ul> 
     <li><p>アクセス権と削除権： GDPRとCCPAに追加された機能を活用しています。 <a href="https://helpx.adobe.com/jp/campaign/kb/acc-privacy.html">詳細を表示</a></p></li> 
     <li> <p>キャンペーンインターフェイスまたはAPIを使用してプライバシーリクエストを作成する場合、「 <strong>規則</strong> 」タイプを選択できるようになりました。 PDPA、LGPD、GDPR、CCPA。 <a href="https://helpx.adobe.com/campaign/kb/acc-privacy.html#ManagingPrivacyRequests">詳細を表示</a>。</p></li>
    </ul>
   </td> 
  </tr> 
 </tbody> 
</table>

**セキュリティの機能強化**

* 電子メール内のリンクの追跡に関するセキュリティが改善され、すべての顧客に対してデフォルトで有効になっています。 さらに、強化されたセキュリティ機能が利用できます。この機能はカスタマーケアにご連絡いただくと有効にできます。これを非ホスト型顧客が有効にするための手順と機能の詳細については、[セキュリティおよびプライバシーチェックリスト](https://helpx.adobe.com/jp/campaign/kb/acc-security.html)を参照してください。（NEO-24232）

* セキュリティを最適化するため、ファイル名の生成に使用するMD5ハッシュアルゴリズムは、パブリックファイルのアップロード用にsha256で強化されました。 （NEO-17044）

* XSS攻撃に対するセキュリティを強化するために、ミラーページの実行時にクライアント側のスクリプトが無効になります。 （NEO-17987）

* プライ **バシー要求のクリーンアップ** (Privacy Request Cleanup)テクニカルワークフローで調整データを削除できない問題を修正しました。 （NEO-25168、NEO-21004）

* SFTP キーに基づく認証が Debian 9 で動作しない&#x200B;**ファイル転送**&#x200B;アクティビティの問題を修正しました。（NEO-23183）

**互換性の強化**

キャンペーンで次のシステムがサポートされるようになりました。
* オペレーティングシステム： Debian 10
* RDBMS: Oracle 18cおよびOracle 19c
* FDA: Azure Synapse Analytics

詳しくは、 [キャンペーン互換表を参照してください](https://helpx.adobe.com/jp/campaign/kb/compatibility-matrix.html)。

**強化点**

* トランザクションメッセージングが改善され、ユーザーエクスペリエンスが向上しました。 実行インスタンスを非公開にして、トランザクションメッセージテンプレートをから削除できるようになりました。 [詳細情報](../../message-center/using/template-unpublication.md)。

* 画像や添付ファイルを含む電子メールの送信時に制限を設定する新しいオプションが追加されました。 これらのガードレールは、パフォーマンスの問題を回避できます。これは、トランザクションメッセージングで特に役立ちます。 [詳細を表示](../../installation/using/configuring-campaign-options.md#delivery)

* 新しい「 **Prepare the database parts in the database** 」オプションを使用すると、配信の準備をデータベース内で直接実行でき、分析を大幅に高速化できます。 このオプションは、特定の設定でのみ使用できます。 [詳細情報](../../delivery/using/steps-validating-the-delivery.md#improving-delivery-analysis)。（NEO-23886）

* Microsoft Dynamics用 [CRMコネクタアクティビティ](../../workflow/using/crm-connector.md) のパフォーマンスが向上しました。 （NEO-13303、NEO-12710）

* 共有メモリのバージョンが増加しました。

   >[!WARNING]
   >
   >この改善には、アップグレードの実行後に追加の手順が必要です。 以下の「 **技術的な発展** 」の項を参照してください。

* クリーンアップワークフローが強化されました。 すべての削除済みワークフローの親なし作業テーブルも、クリーンアップワークフローによって自動的に削除されるようになりました。 [詳細情報](../../production/using/database-cleanup-workflow.md#cleanup-of-workflow-instances)。

* iOS HTTP2コネクターを使用するiOSモバイルアプリケーション用の証明書は、プッシュ通知を送信する前に検証されるようになりました。したがって、証明書の期限が切れているため配信が失敗するのを防ぐことができます。

* HTTPプロキシ接続の管理が改善されました。 [詳細情報](../../installation/using/configuring-campaign-server.md#proxy-connection-configuration)。

**その他の変更**

* 従来のSMSコネクタは廃止されました。 非 [推奨機能のページを参照してください](../../rn/using/deprecated-features.md)。

* 独自のLitmusアカウントを使用して、Adobe Campaignでのインボックスレンダリングのプロビジョニングと使用を行うことはできなくなりました。 [詳細情報](../../delivery/using/inbox-rendering.md)。

* フォルダと表示の区別を改善するために、表示名の色を濃い青から濃いシアンに変更しました。 [詳細を表示](../../platform/using/access-management.md#about-views)

* Campaign Classicは、英国、インドおよびカナダの地域でホストされるMicrosoft Dynamics CRMアカウントに接続できるようになりました。 これは、Office 365およびオンプレミス(Dynamics 2015)の展開の種類に適用されます。

* キャンペーンは、TLS検証を実行して、指定した証明書のホスト名とサーバーのホスト名が一致しているかどうかを確認できるようになりました。

* 配信と追跡の統計テーブルに、SMSチャネルの配信ごとに1つのエントリが表示され、配信受信者ごとに1つのエントリが表示されるようになりました。

* ダウンロードしたファイルがディスク領域より大きい場合に警告を表示するエラーメッセージをログファイルに追加しました。

* 雪片コネクタに次の機能が使用できるようになりました。 MonthsAgo、DaysAgoInt、ToDateTime、YearsAgo。

**技術面の変更点**

この新しいビルドは共有メモリを更新し、アップグレードを実行するために追加の手順が必要です。 キャンペーン管理者は、メモリセグメントを削除する必要があります。 これらの手順は必須です。古いセグメントによりnlserver/nlsrvmodの起動が妨げられるためです。

Windowsでは、システムを再起動する必要があります。

Debian/CentOsでは、共有メモリの削除が必要です。 次の手順を実行します。

アップグレードの前に、次の手順に従う必要があります。

1. Apache2（CentOSではhttp2）サービスが実行中の場合は停止します。
1. nlserver （古いビルドの場合はnlserver6）サービスが実行中の場合は停止します。

アップグレード後：

1. バージョンが現在のバージョンより古い場合は、 **ipcrm** コマンドを使用して共有メモリを削除します。
1. nlserverサービスが実行されていた場合に開始します。
1. apache2サービスが実行されていた場合に開始します。

Debianのコマンドラインを次に示します。

```
/etc/init.d/nlserver* stop
/etc/init.d/apache2 stop
```

```
for i in `ipcs -s | awk '/www-data/
{print $2}'`; do (ipcrm -s $i); done
```

```
for i in `ipcs -m | awk '/www-data/ {print $2}
'`; do (ipcrm shm $i); done
```

```
for i in `ipcs -m | awk '/neolane/
{print $2}'`; do (ipcrm shm $i); done
```

```
for i in `ipcs -s | awk '/neolane/ {print $2}
'`; do (ipcrm -s $i); done
```

```
/etc/init.d/apache2 restart
/etc/init.d/nlserver* start
```

Linuxの例はこの [ページで紹介している](../../configuration/using/additional-parameters.md#redirection-server-configuration)。

**パッチ**

* クリーンアップワークフローログの軽度の問題を修正しました。
* WSDLファイルを解析する際のワークフロー **読み込み(SOAP)** アクティビティの問題を修正しました。
* 多数のワークフローを効率的に処理するために **調査** アクティビティを使用して多数のワークフローをアップグレードする場合にエラーが発生する問題を修正しました。
* 拡張MTAからのinMailメッセージの処理中に接続が断続的に発生する問題を修正しました。 （NEO-20380）
* HTMLで画像が100%の幅で表示されている場合に、ホットクリックの割合が正しく表示されない問題を修正しました。 （NEO-23203）
* 配信の条件付きコンテンツがホットクリック数レポートに完全に表示されない問題を修正しました。 （NEO-18729）
* ワークフローを定期的に送信するためにターゲットの再開時にワークフローの承認手順がスキップされる問題を修正しました。 （NEO-18166）
* ワークフロー内のエラーを修正した後に、 **「再開」配信の準備** (Restart)ボタンがメッセージを再開できない問題を修正しました。 （NEO-13488）
* ターゲットに日本語E メールフォーマットとの受信者が含まれるランプアップフェーズで、ミッドソーシングモードで配信が失敗する可能性がある問題を修正しました。 （NEO-23846）
* 雪片コネクタ(NEO-20105)のタイムゾーン変換の問題を修正しました。
* FTP over SSL を使用する外部アカウントの問題を修正しました。（NEO-20498）
* 行配信に画像が表示されない可能性がある問題を修正しました。 （NEO-23207）
* オファーの公開時にエラーが発生する問題を修正しました。 （NEO-23312）
* 証明書の有効期限が切れている場合でも、モバイルアプリケーションでテスト接続が機能するプッシュ通知の問題が修正されました。 （NEO-22991）
* 高い頻度で送信された場合にプッシュ通知に影響を与える可能性がある問題を修正しました。 （NEO-20516）
* トラッキングログが含めていない場合でも、追跡データに重複が含まれる問題を修正しました。 （NEO-20040）
* トラッキングサーバーの通信エラーが修正された後、重複トランザクション電子メールが送信される問題を修正しました。 （NEO-23640）
* 追跡URLからリダイレクトする際にエンコーディングパラメーターの値が削除される問題を修正しました。 （NEO-25637）
* 浮動小数点数の比較時にクエリが機能しない可能性がある問題を修正しました。 （NEO-23243）
* ワークフローを再開した後に、 **変更者** 列のコンテンツが表示されない可能性がある問題を修正しました。 （NEO-23035）
* 2つ目のコンテナからログをダウンロードする場合に、トラッキング技術ワークフローが失敗する問題を修正しました。 （NEO-23159）
* **エンリッチメント** アクティビティの実行時にワークフローが失敗する可能性がある問題を修正しました。 （NEO-17338）
* nullまたは負の値を入力しないように、 **重複にチェックマークが追加され** 、 **** 重複排除 - 重複ワークフローアクティビティのフィールドを保持するようになりました。
* 時間と分の指定を避けるために、 **** スケジューラーキャンペーンを定期的なから削除しました。 日付のみが考慮されます。
* スクリプトワークフローアクティビティの「スクリプトによって **計算される****** 」オプションを使用して配信を作成する場合に、追加のストレージフィールドが発生する問題を修正しました。 （NEO-20609）
* データベースのクリーンアップタスク内でゴーストワークフローが削除されない問題を修正しました。
* 「 **請求(アクティブなプロファイル)** 」技術ワークフローが失敗する問題を修正しました。 （NEO-19777）
* acsDefaultAccount外部アカウントの接続をテストする際の問題を修正しました。 （NEO-23433）
* Hadoopテーブルを含む複数の列を持つ主キーにスキーマ拡張を作成できない問題を修正しました。 （NEO-17390）
* WSDLファイルがURLから読み込まれない可能性がある **読み込み(SOAP)** アクティビティの問題を修正しました。 （NEO-16924）
* 複数のアクティブなワークフローサーバーが負荷分散されている場合に、 **無条件停止** （コンソールを使用）を実行できない問題を修正しました。 （NEO-19556）
* クリーンアップワークフローがクラッシュする原因となる問題を修正しました。
* 実行インスタンスにテンプレートを公開する際に発生する可能性がある問題を修正しました。
* collectPrivacyRequestsテクニカルワークフローが実行されない可能性がある問題を修正しました。 （NEO-20513、NEO-25169）
* 9080の構築のアップグレード後にオーディエンスマネージャーに接続しようとすると発生する可能性がある問題を修正しました。 （NEO-20511、NEO-25167）
* PDF形式またはXLS形式でレポートを書き出す際に発生する可能性がある問題を修正しました。 (NEO-20982、NEO-23493、NEO-23348)
* 配信が送信された後、配信リストで2回を表示する可能性がある問題を修正しました。
* ミッドソーシング経由で配信を送信するようにルーティング設定が設定されている場合に発生する可能性がある配信の準備に関する問題が修正されました。
* 行メッセージ内のWebアプリケーションのリンクをクリックするとエラーメッセージが表示される問題を修正しました。
* Microsoft Dynamics CRMがすべてのエンティティを取得できない可能性がある問題を修正しました。 （NEO-24528）
* クリーンアップワークフローを実行した後に **増分処理クエリ** アクティビティの履歴が削除される問題を修正しました。
* ミッドソーシング外部アカウントを作成する際に、NmsMidSourcing_LastBroadLog_&lt;InternalName>オプションがない問題を修正しました
