---
product: campaign
title: 最新リリース
description: 最新の Campaign Classic リリース注意
feature: 概要
role: Business Practitioner
level: Beginner
exl-id: d65869ca-a785-4327-8e8d-791c28e4696c
source-git-commit: 28083eb0271c8c148955fa33978479dc3683eaed
workflow-type: tm+mt
source-wordcount: '1953'
ht-degree: 53%

---

# 最新リリース{#latest-release}

このページには、**最新の Campaign Classic リリース候補バージョン**&#x200B;に加えられた新機能、改善点、および修正点が記載されています。

>[!NOTE]
>
>Campaign **一般公開（GA）ビルド**&#x200B;は次のとおりです。[[!DNL Gold Standard]  11 リリース](../../rn/using/gold-standard.md#gs-11)と [Campaign 20.2.5 リリース](../../rn/using/release--20-2.md)。

## ![](assets/do-not-localize/blue_2.png) リリース 21.1.3 - ビルド 9330 {#release-21-1-3-build-9330}

_2021年6月6日_

**新機能**

<table>
<thead>
<tr>
<th><strong>AdobeJourney Orchestration</strong><br/></th>
</tr>
</thead>
<tbody>
<tr>
<td>
<p>Adobe Campaign ClassicとJourney Orchestrationの統合は現在GAです。 Adobe Campaign Classicのトランザクションメッセージ機能を使用して、Journey OrchestrationがEメール、プッシュ通知、SMSを送信できます。</p>
<p>Journey Orchestration インスタンスと Campaign Classic インスタンスとの接続は、プロビジョニング時にアドビによって設定されます。</p>
<p>詳しくは、<a href="https://experienceleague.adobe.com/docs/journeys/using/action-journeys/acc-action.html">Journey Orchestrationのドキュメント</a>を参照してください。 この<a href="https://experienceleague.adobe.com/docs/journeys/using/use-cases-journeys/campaign-classic-use-case.html">節</a>では、ステップバイステップの使用例を示します。</p>
</td>
</tr>
</tbody>
</table>

<table> 
<thead>
<tr> 
<th> <strong>LINEチャネルの強化</strong><br /> </th> 
</tr> 
</thead> 
<tbody> 
<tr> 
<td> <p>LINEチャネルに次の機能が追加されました。
</p>
<ul> 
<li><p>LINEビデオメッセージタイプのサポート</p></li>
<li><p>LINEパートナー登録APIのサポート</p></li>
<li><p>LINEサーバー側エラーまたはネットワークタイムアウトの場合にメッセージ送信の再試行をサポート</p></li>
</ul>
<p>詳しくは、<a href="../../delivery/using/line-channel.md">詳細ドキュメント</a>を参照してください。</p>
</td> 
</tr> 
</tbody> 
</table>

<table> 
<thead>
<tr> 
<th> <strong>Vertica FDAコネクタ</strong><br/> </th> 
</tr> 
</thead> 
<tbody> 
<tr> 
<td> <p>これで、Adobe Campaign ClassicインスタンスをVertica外部データベースに接続できます。 この接続は、新しい外部アカウントで管理されます。</p>
<p>詳しくは、<a href="../../installation/using/configure-fda-vertica.md">詳細ドキュメント</a>を参照してください。</p>
</td> 
</tr> 
</tbody> 
</table>

<table> 
<thead>
<tr> 
<th> <strong>Google Big Query FDAコネクタ</strong><br /> </th> 
</tr> 
</thead> 
<tbody> 
<tr> 
<td> <p>これで、Adobe Campaign ClassicインスタンスをGoogle Big Query外部データベースに接続できます。 この接続は、新しい外部アカウントで管理されます。
</p>
<p>詳しくは、<a href="../../installation/using/configure-fda-google-big-query.md">詳細ドキュメント</a>を参照してください。</p>
</td> 
</tr> 
</tbody> 
</table>

**セキュリティの機能強化**

* データベース接続の詳細をすべて返す&#x200B;**xtk:session#GetCnxInfo** APIメソッドへのアクセスが、管理者ユーザーのみに制限されるようになりました。 （NEO-27779）
* 非推奨（廃止予定）のdecryptString関数は、CRM関連のJavaScriptファイルのdecryptPasswordに置き換えられました。
* トラッキング署名機能が改善され、サードパーティツール（Eメールクライアント、インターネットブラウザー、安全なリンクセキュリティツール）がトラッキング対象リンクを変更した場合のリダイレクトエラーの追跡リスクが軽減されました。
* 大文字を含めるとトラッキングされるURLが機能しない場合がある問題を修正しました。 トラッキングされるURLの署名メカニズムでは大文字と小文字が区別されるようになりました。 （NEO-28414）

**互換性の更新**

Campaign で次のシステムがサポートされるようになりました。
* Google Big Query FDAコネクタ
* Vertica FDAコネクタ
* PostgreSQL 13

詳しくは、[Campaign 互換性マトリックス](../../rn/using/compatibility-matrix.md)を参照してください。

**非推奨（廃止予定）の機能**

* Campaign 21.1リリースより、Adobe Analytics Data Connectorは非推奨（廃止予定）となります。 このコネクタを使用する場合は、新しいコネクタAdobe Analytics Connectorに応じて実装を適応させる必要があります。
詳しくは、[詳細ドキュメント](../../platform/using/adobe-analytics-connector.md)を参照してください。
* Debian 8のサポートは非推奨（廃止予定）となりました。
* 20.3でのOracleCRMの廃止に続いて、関連する外部アカウントがインターフェイスから削除されました。

詳しくは、[非推奨（廃止予定）の機能と削除された機能のページ](../../rn/using/deprecated-features.md)を参照してください。

**改善点**

* ワークフローの保存時に、アクティビティ名が一意で、トランジションが常に「 」アクティビティに続くことを確認する追加のチェックが追加されました。
* **請求（請求）**&#x200B;テクニカルワークフローに、削除された&#x200B;**アクティブな請求プロファイルの数**(billingActiveContactCount)ワークフローによって元々実行されたタスクが含まれるようになりました。 ワークフローによって毎月送信される電子メールレポートに、インスタンス上のアクティブなプロファイルの数に関する情報が表示されるようになりました。 [詳細情報](../../workflow/using/about-technical-workflows.md)。
* 新しい&#x200B;**_keyOnMData**&#x200B;属性が追加され、メモデータの操作にキーを使用できるようになりました。

**その他の変更**

* Windows用opensslサードパーティをバージョン1.1.1hに更新しました。
* Debianパッケージの説明で、nlserverがAdobe Campaign Classicサーバーに変更されました。

**パッチ**

* セッションタイムアウトを編集して、ユーザーが設定時間の後もログインし続けた特定の時間が経過した後にユーザーをログアウトする問題を修正しました。
* 配信が読み取り専用として表示されるが、配信プロパティで編集可能なままになっていた問題を修正しました。
* Webアプリケーションのデザイン時に編集ツールバーが表示されないエラーを修正しました。
* Eメールにリンクを追加する際に、Adobe Campaign Classicヘッダー付きのEメールのテキストバージョンが表示されるエラーを修正しました。 (NEO-29211)
* HTTP接続でFDAを使用する場合、**ミッドソーシング（配信ログ）**(defaultMidSourcingLog)ワークフローが、**NmsMidSourcing_LogsPeriodHour**&#x200B;オプションで設定された時間枠で停止していました。 これにより、この設定期間後に発生したデータでレコードが更新されなくなります。 （NEO-30833）
* message centerの同期ワークフローを実行した後に発生する問題を修正しました。 配信オブジェクトフォルダーがカスタムフォルダーに移動されるたびに、ワークフローによって配信が汎用の&#x200B;**トランザクションメッセージ履歴**&#x200B;フォルダーに戻されます。 （NEO-27445）
* **ブロードキャスト統計**、**トラッキング指標**、**共有アクティビティの統計**&#x200B;レポートを表示しようとするとエラーメッセージが表示される問題を修正しました。
* **Oracleオンデマンド**&#x200B;ワークフローアクティビティは、OracleCRMコネクタの廃止に続いて、インターフェイスから削除されました。
* ワークフローサーバー(wfserver)モジュールの毎日の再起動後に処理ワークフローの実行が停止する問題を修正しました。 （NEO-30047）
* MX管理ドキュメントが更新されず、IPレピュテーションに悪影響を与える可能性がある問題を修正しました。 （NEO-29897）
* SOAP呼び出しを受け取るとWebプロセスがクラッシュする問題を修正しました。 (NEO-28796)(NEO-29600)
* SAP HANAFDAインデックスの作成に失敗する問題を修正しました。 （NEO-29664）
* ヘッダーを含むSOAP呼び出しを実行する際に、トランザクションメッセージが&#x200B;**待機**&#x200B;状態のままになる可能性がある問題を修正しました。 （NEO-28737）
* teradataFDAコネクタを使用する際に発生していた問題を修正しました。すべての一時テーブルは、クラスタの1つのノードで作成され、スプール領域全体を消費し、Teradataがクラッシュする可能性があります。 一時テーブルが多くのノードで生成されるようになりました。 （NEO-28230）
* Webアプリケーションを使用する際に、トラッキングタグの&#x200B;**nms:trackingURL**&#x200B;スキーマに間違ったプライマリキーが生成される問題を修正しました。 （NEO-27931）
* ODBC 3.xとの互換性が強化され、エラーメッセージの正確性が確保されました。
* Eメール配信でカスタムコンテンツテンプレートが使用されるとコンソールがクラッシュする可能性がある問題を修正しました。 （NEO-31547）
* 接続が遅い、または応答サイズが大きいためにTomcatが有効な応答を送信できない問題を修正しました。
* PostgreSQLデータベースからUUIDを読み取る際に発生する可能性がある問題を修正しました。
* オファーにリンクされた提案データを検索する際に、パフォーマンスの問題が発生する可能性がある問題を修正しました。 （NEO-27554）
* IMSサービスがアクティブ化されても応答しない場合にWebプロセスが応答しなくなる問題を修正しました。
* 特定の結合メカニズムが配信のパーソナライゼーションに失敗したため、配達確認のグループを含む配信を送信できなかった問題を修正しました。 （NEO-14391）
* 配信テーブルをターゲットとするクエリとエンリッチメントアクティビティの場合に、アラートアクティビティでアラートを送信できなかった問題を修正しました。 （NEO-25157）

## ![](assets/do-not-localize/red_2.png) リリース 21.1.2 - ビルド 9282 {#release-21-1-2-build-9282}

_2021 年 4 月 15 日_

* パスワード管理が向上し、セキュリティが最適化されました。 
* MTA がクラッシュする可能性がある問題を修正しました。

## ![](assets/do-not-localize/red_2.png) リリース 21.1.1 - ビルド 9277 {#release-21-1-1-build-9277}

_2021 年 2 月 22 日_

**セキュリティの機能強化**

* コンソール認証メカニズムが強化され、セキュリティが最適化されました。（NEO-26944）
* サーバーサイドリクエストフォージェリ（SSRF）問題に対する保護を強化するために、セキュリティ問題を修正しました。（NEO-28532）

**互換性の更新**

Campaign で次のシステムがサポートされるようになりました。

* Salesforce CRM 外部アカウントの使用時に、Salesforce API バージョン 49 がサポートされるようになりました。

**非推奨（廃止予定）の機能**

**配信品質の技術的監視**&#x200B;レポートは非推奨となりました。

詳しくは、[非推奨（廃止予定）の機能と削除された機能のページ](../../rn/using/deprecated-features.md)を参照してください。

**改善点**

**E メールフィードバックサービス（EFS）**&#x200B;は、拡張 MTA から直接フィードバックを取り込み、レポートの正確性を向上させる、スケーラブルなサービスです。この機能はプライベートベータ版としてリリースされており、今後のリリースですべての顧客が段階的に利用できるようになります。

* フィードバックのすべてのカテゴリが収集され、完全で正確なレポートが可能になりました。
* 配信済み指標の計算は、精度と反応性を向上させるために、拡張 MTA からのリアルタイムフィードバックに基づいておこなわれるようになりました。
* EFS は、同期ソフトバウンスレポートの遅延の問題を解決します。

詳しくは、[詳細ドキュメント](../../delivery/using/sending-with-enhanced-mta.md#efs)を参照してください。このプライベートベータ版への参加を希望される場合は、ご連絡いたしますので、[フォーム](https://forms.office.com/Pages/ResponsePage.aspx?id=Wht7-jR7h0OUrtLBeN7O4Rol2vQGupxItW9_BerXV6VUQTJPN1Q5WUI4OFNTWkYzQjg3WllUSDAxWi4u)にご記入ください。

**その他の変更**

* 圧縮を使用することにより、大きなトラッキングログの転送速度が向上しました。
* 複数のアクティビティでワークフローを実行する場合のタイムアウトを回避するため、ワークフローヒートマップが改善されました。（NEO-27423）
* 終了日が過ぎた場合でもオファーが表示される問題を修正しました。Campaign Classic では、終了日の日付だけでなく、終了日のタイムスタンプ全体が考慮されるようになりました。（NEO-27590）
* Google+ リンクは、**ソーシャルネットワーク共有リンク**&#x200B;のパーソナライゼーションブロックから削除されました。
* 前回のリリースでバグ修正が実装された後の問題を修正しました。SSL/TLS を使用して接続する際に SMS 配信が失敗する原因となっていたホスト名にチェックが追加されました。POP3、SMS、プロキシを使用した HTTP など、ほとんどのプロトコルでホスト名の検証が無効になりました。SMS 外部アカウントの証明書チェックが改善され、3 つの値が追加されました。（NEO-29581）[詳細情報](../../delivery/using/sms-protocol.md#skip-tls)

**パッチ**

* Tab、Enter、Esc キーボードショートカットが新しいログイン画面で動作しない問題を修正しました。
* 新しく作成したワークフローの名前が保存後にデフォルト値に置き換わる問題を修正しました。（NEO-26106）
* **外部ファイル**&#x200B;ターゲットマッピングを使用して、**配信**&#x200B;アクティビティの前に、**エンリッチメント**&#x200B;アクティビティの一部として新しいフィールドをワークフローに追加すると、そのワークフローを実行するときに問題（不要なフィールドが&#x200B;**外部ファイル**&#x200B;ターゲットマッピングに追加される）が発生していました。それを修正しました。（NEO-27687）
* 以前に作成して保存した web アプリケーションを再び開くと、ソースコード内の一部の文字が変更される問題が発生していました。それを修正しました。（NEO-27597）
* リンクをトラッキングするための新しい署名メカニズムを含むビルドに（ビルド 19.1.4 および Campaign 20.2 から）アップグレードする場合に発生する可能性がある問題を修正しました。複数のテンプレートがイベントに関連付けられている場合、アップグレードすると、トランザクションメッセージの送信時に誤ったテンプレートが選択される可能性がありました。（NEO-28326）
* MTA が応答しなくなり、再起動しない限り配信を処理できなくなる問題を修正しました。（NEO-27455）
* 日時型列の一括読み込み操作中のタイムスタンプ管理に関連する MSSQL データベースの問題を修正しました。
* Redshift xtk 関数を使用する場合のワークフロークエリの問題を修正しました。SubDays、SubSeconds、SubMinutes、SubHours が両方の Redshift タイムスタンプ型を受け入れるようになりました。（NEO-24962）
* 匿名アクセスでレポートをプレビューしようとするとスクリプトエラーメッセージが表示される問題を修正しました。（NEO-27081）
* 配信分析を実行する際に、サーバーのメモリ使用量が減少する可能性がある問題を修正しました。
* 特定の複雑なクエリを実行しようとすると、インスタンスが動作しなくなる可能性がある問題を修正しました。
* **Twitter ページを同期する**&#x200B;テクニカルワークフローを実行できない可能性がある問題を修正しました。（NEO-28634）
* **ツイート（twitter）**&#x200B;配信テンプレートを使用して Twitter に投稿しようとすると、decryptPassword 関数に関連するエラーメッセージが表示される可能性がある問題を修正しました。（NEO-28216）
* **JavaScript** アクティビティを使用してワークフロー内で HTTP リクエストをおこなう際に発生していた問題を修正しました。ホスト名にポート番号を定義した後、次のエラーが発生して、呼び出しに失敗していました。（NEO-29146）

```
IOB-090020 Error in SSL library: 'IOB-090013 error:14090086:SSL routines:ssl3_get_server_certificate:certificate verify failed (code 336134278)'
```

* ターゲットデータのパーソナライズ機能を使用した新しい配信が送信されない問題を修正しました（NEO-30323）。
* マーケティングインスタンスで複数のクラッシュが発生し、コアファイルが生成される問題を修正しました。
* 次のエラーが発生して、**トラッキング**&#x200B;ワークフローが失敗する問題を修正しました。（NEO-25206）

```
There is no index on the sourceId field of the 'NmsTrackingLogRcp' table required for the current Web tracking mode. Please add this index.
```

* キャンペーンの「**ターゲティングとワークフロー**」タブ内で配信を作成および保存する際に発生していた問題を修正しました。次のエラーが発生して、プレビューに失敗していました。（NEO-29440）

```
XTK-170024 The temporary 'temp:deliveryEmail-all' schema is not defined in the current context
```

* マーケティングインスタンスと Adobe Campaign Standard インスタンスまたは Campaign Classic ミッドソーシングインスタンスの間で外部アカウントを設定し、「DisableFOH2=1」オプションを使用すると発生していたエラーを修正しました。外部アカウントで「DisableFOH2=1」オプションを使用すると、接続が正しく閉じられないため停滞し、次のエラーが発生していました。（NEO-26258）

```
The maximum number of connections has been reached (50) by connections pool 'nms:extAccount:acsDefaultRelayAccount XXX'. The server is overloaded. Please try again later.
```

* サーバーとプロバイダーの間で接続の問題が発生した場合の SMS のエラーを修正しました。接続は、MTA の子によって自動的に無効にされていました。Adobe Campaign Classic は、新しい子が起動していない限り、この失敗する接続を試行しません。
