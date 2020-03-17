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
source-git-commit: 8d6e3118dc498096283d54713725071e0906aba3

---


# 最新リリース{#latest-release}

[アップグレードの構築](https://helpx.adobe.com/campaign/kb/acc-build-upgrade.html) )|コント [ロールパネルのリリース](https://docs.adobe.com/content/help/en/control-panel/using/release-notes.html) |ドキュメ [ントの更新](../../rn/using/documentation-updates.md) |以 [前のリリース](../../rn/using/release--19-2.md) |非推 [奨の機能](https://helpx.adobe.com/campaign/kb/deprecated-and-removed-features.html)

<table> 
 <tbody> 
  <tr> 
   <td><img src="assets/green3.png"/><strong>一般公開</strong></td>
   <td><img src="assets/blue3.png"/><strong>候補をリリース</strong></td> 
   <td><img src="assets/orange3.png"/><strong>使用できなくなりました</strong></td> 
   <td><img src="assets/red3.png"/><strong>廃止</strong></td> 
  </tr> 
   <tr> 
   <td>最新の安定したビルドが利用可能です。 ビルドは実稼働環境で検証されました。<br> </td>
   <td>ビルドはアドビによって検証されます。 製品の校正を待っています。<br> </td>
   <td>新しいビルドにバグ修正が加えられました。 更新が必要です。<br> </td>
   <td>既知の回帰が含まれます。 更新は必須です。<br> </td>
  </tr> 
 </tbody> 
</table>

最後 **の安定ビルドは** 9032 (205c981c3)です。 Click [here](../../rn/using/release--19-1.md#release-19-1-4-build-9032)

## ![](assets/blue_2.png) リリース20.1.2 — ビルド9123 {#release-20-1-2-build-9123}

_2020年3月13日_

* Red Hat 7サーバーでバージョンをデプロイできない問題を修正しました。 （NEO-23332）

## ![](assets/orange_2.png) リリース20.1 — ビルド9122 {#release-20-1-build-9122}

_2020年2月17日_

**新機能?**

<table> 
 <thead> 
  <tr> 
   <th> <strong>雪片FDAコネクタ</strong><br /> </th> 
  </tr> 
 </thead> 
 <tbody> 
  <tr> 
   <td> <p>雪片は完全に管理されたクラウドデータウェアハウスで、ストレージとコンピュータの両方のレベルで拡張可能に設計されています。 この新しいコネクターを使用すると、Adobe Campaignはスノーフレークの機能を活用して、ビッグデータセグメント化を実行できます。 このコネクタは、アドビがホストする顧客を含む、すべての顧客が利用できます。</p>
    <p>For more information, refer to the <a href="../../platform/using/specific-configuration-database.md#configure-access-to-snowflake">detailed documentation</a> and <a href="https://docs.adobe.com/content/help/en/campaign-learn/campaign-classic-tutorials/administrating/fda/big-data-segmentation-on-snowflake.html">tutorial video</a>.</p>
   </td> 
  </tr> 
 </tbody> 
</table>

<table> 
 <thead> 
  <tr> 
   <th> <strong>Hadoop FDAコネクタの機能強化</strong><br /> </th> 
  </tr> 
 </thead> 
 <tbody> 
  <tr> 
   <td> <p>Hadoop FDAコネクタが、Clouderaと同様にHadoop 3.0をサポートするように改善されました。</p>
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

* プッシュ通知機能（nms:addressおよびnms:appSubscriptionRcp）で使用されるテーブルの検疫管理とクリーンアップを改善。 iOS（HTTP2コネクタのみ）の場合、無効なトークンは、Androidと同じ方法で処理されるようになりました。 NmsAppSubscriptionRcpテーブルにdisableフラグが設定されました。 [詳細を表示](../../production/using/database-cleanup-workflow.md#subscription-cleanup--nmac-)

* タイムアウト期間を定義する新しいオプションが **JavaScriptコード** 、 **** JavaScriptコードワークフローアクティビティに追加されました。 これにより、JavaScriptの実行段階が長時間続くのを防ぎます。 タイムアウト期間が経過すると、ワークフローは停止します。 デフォルトのタイムアウトは1時間です。 [詳細を表示](../../workflow/using/sql-code-and-javascript-code.md)

* 一致する親和性がミッドソーシングサーバーで見つからない場合に、対応するエラーメッセージが表示され、配信分析が停止されるようになりました。

* Postgresのデータベースのフェイルオーバーがサポートされるようになりました。データベースサーバーがクラッシュし、再起動した場合、Campaignは自動的に再接続されるようになりました。

* 「 **Start Pending** 」表示が、管理/監査/ワークフローステータスノードに追加されました。 これにより、operationMgtプロセスで開始されるのを待機しているインスタンス上のすべてのワークフローを監視 **できま** す。 この表示には、マーケティングキャンペーンパッケージが含まれています。 [詳細を表示](../../workflow/using/monitoring-workflow-execution.md#filtering-workflows-status)

**その他の変更**

* Linuxでは、nlserverサービスの起動時に、/etc/init.d/nlserver6スクリプトの代わりにシステム単位が使用されるようになりました。 新しいスタートアップスキームへの移行は、20.1パッケージのインストール時に自動的に実行されます。 /etc/init.d/nlserver6は引き続き提供されますが、nlserverサービス（start、restart、stopなど）との対話用に、systemctlコマンドを直接使用することをお勧めします。

* 最も多く使用されるカスタムテーブルは、xtkNewIdシーケンスから **専用のシーケンス** に移動されました。 [詳細を表示](https://helpx.adobe.com/campaign/kb/sequence_auto_generation.html#Switchtoadedicatedsequence)

* 不要なデータベース接続の影響を受ける可能性のあるクエリのパフォーマンスを改善。

* データベース更新ウィザードのパフォーマンスを改善しました。

* データベースレコードの管理が強化されました。

* 接続プールの堅牢性が向上し、予期しない接続障害が頻繁に発生するのを防ぐ可能性があります。

* ソフトエラーが発生した場合に検疫するアドレスを送信する電子メールアドレスの検証ルールが強化されました。 [詳細を表示](../../delivery/using/understanding-quarantine-management.md#soft-error-management)

* Debianの場合、CampaignではシステムPCREライブラリが使用可能なときに使用されるようになりました。

* Campaignで、より新しいシステムODBCライブラリを使用できるようになりました。

* リッチイメージを読み込むための接続を開く際に、LINEサーブレットにタイムアウトが追加されました。 イメージの読み込みに時間がかかりすぎる場合は、ボトルネックを回避するためにサーブレットが接続を停止します。

**パッチ**

* Hadoopコネクタを使用する際のアカウントキーの暗号化の問題を修正しました。

* SSL証明書の実装によるWindowsサーバーでのユーザー接続の失敗に起因する問題が修正されました。 （NEO-20629）

* 除外ワークフローIDの場合の増分クエリアクティビティの問題を修正しました。 （NEO-19779）

* Netezza FDAコネクタを介してクエリを実行する場合のエンコーディングの問題を修正しました。 （NEO-19594）

* **** WebダウンロードワークフローイベントアクティビティでPOSTメソッドを使用するとエラーが発生する問題を修正しました。

* オファーの提案の生成に関する問題を修正しました。 （NEO-18176）

* ダウンロード計測用Webフォームテンプレートを使用する際のフッター表示の問題を修正しました。

* 連続配信のコンテンツ内のURLを解析する際に、URLがクラッシュする可能性がある問題を修正しました。 （NEO-16910）

* 新しいキャンペーンを作成する **際に** 、「開始 **日」と「終了日** 」フィールドが計算されない問題を修正しました。

* URLを使用する場合の「ファイルのダウ **ンロード** 」ワークフローアクティビティの問題を修正しました。

* レポートのクエリアクティビティでインポートしたリストをプレビューする際の問題を修正しました。 （NEO-13119）

* 電子メールエディターで「 **Powered by Campaign** 」パーソナライゼーションブロックを選択すると古い画像が表示される問題を修正しました。

* クライアントとサーバー間のネットワーク通信が改善されました。

* 同じキャンペーンで作成されたワークフローが多すぎる場合の問題を修正しました。 現在は、28を超えるワークフローを作成することはできません。 警告が表示されます。

* **Union****** Workflowアクティビティで「列の選択」調整オプションを使用する際の問題を修正しました。

* ワークフローで破損したエンリッチメントリストを使用すると発生する可能性があるコンソールのクラッシュの問題を修正しました。 （NEO-18096）

* ワークフローで発生する可能性がある様々なコンソールクラッシュの問題を修正しました。(NEO-18010、NEO-18032)

* 外部シグナルワークフローアクティビティが無効になっ **ている場合でも** 、実行できる問題を修正しました。 （NEO-17524）

* 新しいスキーマを作成する際の問題を修正しました。

* SMSメッセージを送信する際の追跡の問題を修正しました。 （NEO-19595）

* 配信インジケーターに誤ったターゲットオーディエンス番号が表示される問題を修正しました。

* ワークフローアクティビティを介して説明レポートを生成すると、誤った割合が表示される問題を修正しました。 （NEO-14314）

* 配信スループットレポートで、時間表示パラメーターの値が異なる場合に表示される問題を修正しました。 （NEO-11783）

* トランザクションメッセージ追跡インジケーターが追跡ワークフローで更新されない問題を修正しました。 （NEO-17770）

* SOAPを使用してオファーをリクエストすると、Webプロセスがクラッシュして再起動する問題が修正されました。 （NEO-19482）

* アップロードディレクトリがリモート共有場所の場合に、データをパブリックリソースにアップロードできない問題を修正しました。 （NEO-19361）

* Adobe Experience Cloud技術ワークフローからの **オーディエンスの読み込みが** 、常に失敗する問題を修正しました。 （NEO-18463）

* Experience Managerからインポートしたテンプレートを使用する場合に、配信が送信されない問題を修正しました。 （NEO-17540）

* ビルド9032にアップグレードし、インスタンスがSSLプロトコルを使用してFTPサーバーに接続できない問題を修正しました。 （NEO-20498）

* FDAスキーマをターゲットディメンションとして使用して、ワークフローで **Update data** （更新データ）アクティビティを使用して大量のデータを削除、挿入、または更新する際に発生していた問題を修正しました。 （NEO-13280）

* タグの外で「if」ステートメントを使用すると電子メールが送信されない問題を修正し `body` ました。

* 送信されたメッセージの配信ログからミラーページを表示しようとすると発生していた問題を修正しました。 （NEO-17976）

* 配信で「HTMLを読み込み」をクリックした後に、「 **Link to mirror page** personalization block」が「 **Text content** (テキストコンテンツ **)」タブに表示さ** れない問題を修正しました。 （NEO-17568）

* 期限切れのミラーページへのリンクをクリックしたときに表示されるエラーメッセージが明確になりました。 （NEO-17340）

* データ配布の作成画面で一部のボタンが使用できない **問題を修正** しました。

* Asia/Kolkataをタイムゾーンとして使用して、インスタンスで配信アクティビティをスケジュールする際に発生していた問題を修正しました。 （NEO-20001）

* 配信に親和性の設定の問題がある場合にエラーが表示されるようになりました。

* バージョン情報メニューに誤ったバージョンタグ番号が表示される問題を修 **正し** ました。

* ワークフローで定期的な配信のプロパティからルーティングアカウントを更新しようとすると発生していた問題を修正しました。 （NEO-18684）

* リダイレクトモジュールを使用してインスタンスに接続する際に、接続を閉じると接続が正しくクリーニングされない問題を修正しました。
