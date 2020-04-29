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
source-git-commit: eab67029d477044bc853f2a5c2de06ace70ebbee

---


# 最新リリース{#latest-release}

[ビルドアップグレード](https://helpx.adobe.com/jp/campaign/kb/acc-build-upgrade.html) | [コントロールパネルのリリース](https://docs.adobe.com/content/help/ja-JP/control-panel/using/release-notes.html) | [ドキュメントの更新](../../rn/using/documentation-updates.md) | [以前のリリース](../../rn/using/release--19-2.md) | [廃止された機能](https://helpx.adobe.com/jp/campaign/kb/deprecated-and-removed-features.html)

<table> 
 <tbody> 
  <tr> 
   <td><img src="assets/do-not-localize/green3.png"/><strong>一般公開（GA）</strong></td>
   <td><img src="assets/do-not-localize/blue3.png"/><strong>リリース候補</strong></td> 
   <td><img src="assets/do-not-localize/orange3.png"/><strong>公開停止</strong></td> 
   <td><img src="assets/do-not-localize/red3.png"/><strong>廃止済み</strong></td> 
  </tr> 
   <tr> 
   <td>最新の安定したビルド。ビルドは本番環境で検証済みです。<br></td>
   <td>アドビが検証済みのビルド。本番環境での検証待ちです。<br></td>
   <td>バグ修正を含む、新しいビルドがあります。更新が必要です。<br></td>
   <td>新たな不具合を含むことがわかっています。必ず更新が必要です。<br></td>
  </tr> 
 </tbody> 
</table>

最後 **の安定ビルドは** 9032 (3a9dc9c)です。 Click [here](../../rn/using/release--19-1.md#release-19-1-4-build-9032)

## ![](assets/do-not-localize/blue_2.png) リリース 20.1.2 - ビルド 9123 {#release-20-1-2-build-9123}

_2020年3月13日_

* Red Hat 7サーバーでバージョンをデプロイできない問題を修正しました。 （NEO-23332）

## ![](assets/do-not-localize/orange_2.png) リリース 20.1 - ビルド 9122 {#release-20-1-build-9122}

_2020年2月17日_

**新機能?**

<table> 
 <thead> 
  <tr> 
   <th> <strong>雪片FDA接続</strong><br /> </th> 
  </tr> 
 </thead> 
 <tbody> 
  <tr> 
   <td> <p>雪片は完全に管理されたクラウドデータウェアハウスで、ストレージと計算の両方のレベルで拡張できます。 この新しいコネクタを使うと、Adobe Campaignは雪片の力を活用してビッグデータセグメント化を行うことができます。 このコネクタは、アドビがホストする顧客を含む、すべての顧客が利用できます。</p>
    <p>For more information, refer to the <a href="../../platform/using/specific-configuration-database.md#configure-access-to-snowflake">detailed documentation</a> and <a href="https://docs.adobe.com/content/help/en/campaign-learn/campaign-classic-tutorials/administrating/fda/big-data-segmentation-on-snowflake.html">tutorial video</a>.</p>
   </td> 
  </tr> 
 </tbody> 
</table>

<table> 
 <thead> 
  <tr> 
   <th> <strong>HadoopFDAコネクタの強化</strong><br /> </th> 
  </tr> 
 </thead> 
 <tbody> 
  <tr> 
   <td> <p>HadoopFDAコネクタが、Clouderaと同様にHadoop 3.0をサポートするように改善されました。</p>
    <p>詳しくは、<a href="../../platform/using/specific-configuration-database.md#configure-access-to-hadoop-3">詳細ドキュメント</a>を参照してください。</p>
   </td> 
  </tr> 
 </tbody> 
</table>

**セキュリティの機能強化**

* レポート設定のセキュリティを改善し、クリックジャックから保護しました。 これは、新しいレポートに適用されます。 古いレポートの場合は、変更を適用するには再公開する必要があります。 （NEO-13282）

* cryptStringの小さなメモリの問題を修正しました。 （NEO-20071）

* 内部IP開示を修正するために、モニタJSPを改善。 （NEO-16821）

* スタックトレース情報が管理者以外のユーザーに表示される問題を修正しました。 （NEO-12388）

* 以前のセッションのキャッシュデータの管理を改善。 （NEO-17039）

* logins.logファイルで、IMSを使用したログインの成功試行を記録できない問題を修正しました。 （NEO-11004）

**強化点**

* iOS 13がHTTP2コネクタでサポートされるようになりました。

* 強制隔離の管理と、プッシュ通知機能（nms:addressおよびnms:appSubscriptionRcp）で使用されるテーブルのクリーンアップが改善されました。 iOS（HTTP2コネクタのみ）の場合、無効なトークンは、Androidと同じ方法で処理されるようになりました。 NmsAppSubscriptionRcpテーブルにdisableフラグが設定されました。 [詳細を表示](../../production/using/database-cleanup-workflow.md#subscription-cleanup--nmac-)

* タイムアウト期間を定義する新しいオプションが **JavaScriptコードと****** JavaScriptコードワークフローアクティビティに追加されました。 これにより、JavaScriptの実行段階が長時間続くのを防ぎます。 タイムアウト期間が経過すると、ワークフローは停止します。 デフォルトのタイムアウトは1時間です。 [詳細を表示](../../workflow/using/sql-code-and-javascript-code.md)

* 配信分析は、対応するアフィニティがミッドソーシングサーバーで見つからない場合に停止し、対応するエラーメッセージが表示されるようになりました。

* Postgresのデータベースのフェイルオーバーがサポートされるようになりました。データベース・サーバがクラッシュし、再起動した場合、キャンペーンは自動的に再接続されるようになりました。

* 「 **開始保留** 」表示が、管理/監査/ワークフローステータスノードに追加されました。 これにより、 **operationMgtプロセスで開始を待機しているインスタンス上のすべてのワークフローを監視で** きます。 この表示には、マーケティングキャンペーンパッケージが付属します。 [詳細を表示](../../workflow/using/monitoring-workflow-execution.md#filtering-workflows-status)

**その他の変更**

* Linuxでは、nlserverサービスの起動時に、/etc/init.d/nlserver6スクリプトの代わりにシステム単位が使用されるようになりました。 新しいスタートアップスキームへの移行は、20.1パッケージのインストール時に自動的に実行されます。 /etc/init.d/nlserver6は引き続き提供されますが、nlserverサービス(開始、再起動、停止など)との対話用に、systemctlコマンドを直接使用することをお勧めします。

* 最も多く使用されるカスタムテーブルは、xtkNewIdシーケンスから **専用のシーケンス** に移動されました。 [詳細を表示](https://helpx.adobe.com/jp/campaign/kb/sequence_auto_generation.html#Switchtoadedicatedsequence)

* 不要なクエリ接続の影響を受ける可能性があるデータベースのパフォーマンスを改善。

* データベース更新ウィザードのパフォーマンスを改善しました。

* データベースレコードの管理が強化されました。

* 接続プールの堅牢性が向上し、予期しない接続障害が頻繁に発生するのを防ぐ可能性があります。

* ソフトエラーが発生した場合に強制隔離にアドレスを送信するための電子メールアドレスの検証ルールが強化されました。 [詳細を表示](../../delivery/using/understanding-quarantine-management.md#soft-error-management)

* Debianの場合、キャンペーンは、システムPCREライブラリが使用可能なときに使用されるようになりました。

* キャンペーンで、より新しいシステムODBCライブラリを使用できるようになりました。

* リッチイメージを読み込むための接続を開く際に、LINEサーブレットにタイムアウトが追加されました。 イメージの読み込みに時間がかかりすぎる場合は、ボトルネックを回避するためにサーブレットが接続を停止します。

**パッチ**

* Hadoopコネクタを使用する際のアカウントキーの暗号化の問題を修正しました。

* SSL証明書の実装によるWindowsサーバーでのユーザー接続の失敗に起因する問題が修正されました。 （NEO-20629）

* 除外ワークフローIDの場合の増分クエリアクティビティの問題を修正しました。 （NEO-19779）

* NetezzaFDAコネクタを介してクエリを実行する場合のエンコーディングの問題を修正。 （NEO-19594）

* 「 **** Webダウンロードワークフロー」アクティビティのPOSTメソッドを使用するとエラーが発生する問題を修正しました。

* 生成の問題を修正しました。オファーの提案の生成 （NEO-18176）

* ダウンロード計測用Webフォームテンプレートを使用する際のフッター表示の問題を修正しました。

* 連続した配信のコンテンツ内のURLを解析する際に、URLがクラッシュする可能性がある問題を修正しました。 （NEO-16910）

* 新しいキャンペーンを作成する際に ******、** 開始と終了(End)フィールドが計算されない問題を修正しました。

* URLを使用する場合の「ファイルのダウ **ンロード** 」ワークフローアクティビティの問題を修正しました。

* インポートしたリストをレポートのクエリアクティビティでプレビューする際の問題を修正。 （NEO-13119）

* 電子メールエディターで「電源指定」のキャンペーンパーソナライゼーショ **ンブロックを選択する** と、古い画像が表示される問題を修正しました。

* クライアントとサーバー間のネットワーク通信が改善されました。

* 同じキャンペーンで作成されたワークフローが多すぎる問題を修正しました。 現在は、28個を超えるワークフローを作成できません。 警告が表示されます。

* 「列の選択」調整オプションを **和集合ワークフローアクティビティで使用すると** 、問題が修正 **されました** 。

* ワークフローで破損したワークフローを使用する場合に発生する可能性があるエンリッチメントリストのクラッシュの問題を修正しました。 （NEO-18096）

* ワークフローで発生する可能性がある様々なコンソールクラッシュの問題を修正しました。(NEO-18010、NEO-18032)

* 外部シグナルワークフローワークフローが無効になっ **ている場合でも** 、アクティビティを実行できる問題を修正しました。 （NEO-17524）

* 新しいフォルダーを作成する際の問題を修正しました。スキーマ

* SMSメッセージを送信する際の追跡の問題を修正しました。 （NEO-19595）

* ターゲットオーディエンス番号が正しく表示されない問題を修正しました。

* ワークフローワークフローを使用して説明レポートを生成すると、誤った割合が表示される問題を修正しました。アクティビティ （NEO-14314）

* 時間スループットレポートで、配信パラメーターの値が異なる場合に表示スループットレポートが表示される問題を修正しました。 （NEO-11783）

* 追跡ワークフローで、トランザクションメッセージ追跡インジケーターが更新されない問題を修正しました。 （NEO-17770）

* SOAPを使用してオファーを要求すると、Webプロセスがクラッシュして再起動する問題を修正しました。 （NEO-19482）

* アップロードディレクトリがリモート共有の場所である場合に、パブリックリソースにデータをアップロードできない問題を修正しました。 （NEO-19361）

* Adobe Experience Cloudの技術ワークフローから **のオーディエンスの読み込みが** 、常に失敗する問題を修正しました。 （NEO-18463）

* Experience Managerから読み込んだ配信を使用する場合に、テンプレートが送信されない問題を修正しました。 （NEO-17540）

* ビルド9032にアップグレードし、インスタンスがSSLプロトコルを使用してFTPサーバーに接続できない問題を修正しました。 （NEO-20498）

* FDAスキーマをターゲティングディメンションとして使用して、ワークフローの「データを更新」アクティビティを使用して大量のデータを削除、挿入 **** 、または更新する際に発生していた問題を修正しました。 （NEO-13280）

* タグの外で「if」ステートメントを使用すると電子メールが送信されない問題を修正し `body` ました。

* 送信されたメッセージのメッセージを表示しようとするとミラーページが配信ログする問題を修正しました。 （NEO-17976）

* ミラーページで「HTMLを読み込み」をクリ **ックした後に、配信** のパーソナライゼーションブロックへのリンクが「 **Text** content **（テキストコンテンツ）」タブに表示さ** れない問題を修正しました。 （NEO-17568）

* 期限切れのメッセージへのリンクをクリックしたときに表示されるミラーページのエラーメッセージが明確になりました。 （NEO-17340）

* データ配布の作成画面で一部のボタンが使用できない **問題を修正** しました。

* Asia/Kolkataをタイムゾーンとして使用し、配信アクティビティをスケジュールする際に発生していた問題を修正しました。 （NEO-20001）

* エラーが表示されるようになりました。配信の設定に問題がある場合にアフィニティが発生します。

* バージョン情報メニューに誤ったバージョンタグ番号が表示される問題を修 **正し** ました。

* ワークフローで定期的な配信のプロパティからルーティングアカウントを更新しようとすると発生していた問題を修正しました。 （NEO-18684）

* リダイレクトモジュールを使用してインスタンスに接続する際に、接続を閉じると接続が正しくクリーニングされない問題を修正しました。
