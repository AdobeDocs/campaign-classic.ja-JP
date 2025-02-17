---
product: campaign
title: Campaign Classic 2021 リリース
description: Campaign Classic 2021 リリースの詳細
feature: Release Notes
role: User
level: Beginner
hidefromtoc: true
exl-id: 0cd6bf20-da72-4cf0-9f5d-d4e8acdd324d
source-git-commit: a1dbef3e1feca1e3347de013db8bd7809d315016
workflow-type: tm+mt
source-wordcount: '2586'
ht-degree: 100%

---

# 2021 リリース{#release-2021}

## リリース 7.1（21.1）

>[!CAUTION]
>**[!UICONTROL ヘルプ／バージョン情報…]**&#x200B;メニューを使用し、Adobe Campaign の[バージョンおよびビルド番号](../../platform/using/launching-adobe-campaign.md#getting-your-campaign-version)を確認します。 ただし、このページに記載されている 9277～9343 のすべてのビルドでは、バージョン番号は 7.1 ではなく 7.0 と表示されています。
> 

### リリース 21.1.4 - ビルド 9343 {#release-21-1-4-build-9343}

[!BADGE 非推奨（廃止予定）]{type=negative url="https://experienceleague.adobe.com/docs/campaign-classic/using/release-notes/rn-overview.html?lang=ja#rn-statuses" tooltip="非推奨（廃止予定）"}

_2021年10月8日（PT）_

**パッチ**

* ビルド 9342 で利用可能な請求ワークフローの修正を改善しました。この修正を適用するには、ワークフローを手動で再開する必要があります。これで、アップグレード後に、ワークフローが自動的に再開されます。

* **インタラクション**&#x200B;モジュールを[パワーブースター](../../installation/using/power-booster-and-power-cluster.md)オプションとともに使用すると、適切なオファー管理ができなくなる可能性がある問題を修正しました。 （NEO-39263）

* 複数のミッドソーシングインスタンスで複数の IP アフィニティを使用する場合に、配信の送信時に発生する可能性がある「ipaffinity xxx がミッドサーバー xxx に見つかりません」というエラーを修正しました。 （NEO-37514）

### リリース 21.1.4 - ビルド 9342 {#release-21-1-4-build-9342}

[!BADGE 非推奨（廃止予定）]{type=negative url="https://experienceleague.adobe.com/docs/campaign-classic/using/release-notes/rn-overview.html?lang=ja#rn-statuses" tooltip="非推奨（廃止予定）"}

_2021 年 9 月 7 日_（PT）

**セキュリティの強化**

* セキュリティ上の問題を修正して、ディレクトリトラバーサル攻撃に対する保護を強化しました。（NEO-28547）

**改善点**

* Flash は、提供終了後、関連するすべての Campaign 機能およびコンポーネントから削除され、HTML5 に置き換えられました。**ゲージ**&#x200B;タイプのグラフが削除されました。（NEO-30330）[詳細情報](../../reporting/using/creating-a-chart.md)
* Windows にクライアントコンソールをインストールする際、インストーラーは親レジストリノードがあるかどうかを確認し、ない場合は作成するようになりました。これにより、コンソールの起動時に発生する可能性のある問題を防止できます。（NEO-34854）
* 署名トラッキング機能が改善され、サードパーティツール（メールクライアント、インターネットブラウザーなど）による特殊文字の処理方法に関連するエラーを防止できるようになりました。URL パラメーターがエンコードされるようになりました。

**その他の変更**

* 21.1.3 で導入された、請求ワークフローの新しいガードレールでの不具合を修正しました。請求ワークフローが誤ったインスタンスで実行され、生成されなかった請求レポートを送信しようとしてクラッシュしました。修正を適用するには、手動でワークフローを再開する必要があります。
* 既に非推奨（廃止予定）となっている Microsoft CRM コネクタ（Office 365 およびオンプレミスデプロイメント）がインターフェイスから削除されました。[詳細情報](../../platform/using/crm-ms-dynamics.md#configure-acc-for-microsoft)
* Tomcat 8 への移行後に、IIS セットアップスクリプトが更新されて、IIS 統合の問題が修正されました。（NEO-31019）
* ワークフロートランジションの&#x200B;**母集団を表示**&#x200B;ウィンドウのデータタブとスキーマタブで、データソースの識別が改善されました。
* データベースの更新の問題を防ぐために、欠落していたデータベースインデックスが、xtk:rights、nms:dlvExclusion、nms:seedMember、nms:trackingUrl の各スキーマに追加されました。

**パッチ**

* オファーが配信にリンクされるとホットクリックレポートが機能しなくなる問題を修正しました。（NEO-26295）
* **サブワークフロー**&#x200B;アクティビティを実行しても出力テーブルが生成されなかった問題を修正しました。（NEO-36242）
* **記述的分析**&#x200B;レポートを PDF にエクスポートする際の様々な問題を修正しました。（NEO-25847）
* 外部メール配信を使用すると配信が失敗する可能性がある問題を修正しました。（NEO-37435）
* Web API を使用して Microsoft CRM に接続する際のエラーを修正しました。機能に影響がなかったので、エラーメッセージは削除されました。
* ミッドサーバーがトラッキングサーバーとマーケティングサーバーの間のリレーとして設定された場合のトラッキングログ重複排除の問題を修正しました。（NEO-36285）
* Vault を特定のコードストアとして使用できなかったリグレッションを修正しました。
* 受信トランジションが FDA データソースからのものである場合に「**エンリッチメント**」ワークフローアクティビティで変数を使用できなかった問題を修正しました。
* メールメッセージ内の URL が機能しなくなる可能性がある問題を修正しました。

### リリース 21.1.3 - ビルド 9330 {#release-21-1-3-build-9330}

[!BADGE 非推奨（廃止予定）]{type=negative url="https://experienceleague.adobe.com/docs/campaign-classic/using/release-notes/rn-overview.html?lang=ja#rn-statuses" tooltip="非推奨（廃止予定）"}

_2021 年 6 月 5 日（PT）_

**新機能**


<table>
<thead>
<tr>
<th><strong>新しいワークフローアクティビティ：データソースを変更</strong><br/></th>
</tr>
</thead>
<tbody>
<tr>
<td>
<p>新しい「<b>データソースを変更</b>」ワークフローアクティビティを使用すると、ワークフローのワークテーブルのデータソースを変更できます。これにより、様々なデータソース（FDA およびローカルデータベース）にわたってデータ管理の柔軟性が向上します。</p>
<p>Adobe Campaign ワークフローでは、データは作業用（または一時）テーブルを使用して管理されます。ワークフローの実行時に、ワークテーブルはワークフローアクティビティ間でデータを共有します。デフォルトでは、ワークテーブルは、クエリ対象となるデータのソースと同じデータベースに作成されます。</p>
<p>詳しくは、<a href="../../workflow/using/change-data-source.md">詳細なドキュメント</a>を参照してください。</p>
</td>
</tr>
</tbody>
</table>

<table>
<thead>
<tr>
<th><strong>Adobe Journey Orchestration との統合</strong><br/></th>
</tr>
</thead>
<tbody>
<tr>
<td>
<p>Adobe Campaign Classic と Journey Orchestration の統合が一般提供されるようになりました。Journey Orchestration が Adobe Campaign Classic のトランザクションメッセージ機能を使用して、メール、プッシュ通知、SMS などを送信できるようになります。</p>
<p>Journey Orchestration インスタンスと Campaign Classic インスタンスとの接続は、プロビジョニング時にアドビが設定します。</p>
<p>詳しくは、<a href="https://experienceleague.adobe.com/docs/journeys/using/action-journeys/acc-action.html?lang=ja">Journey Orchestration ドキュメント</a>を参照してください。ステップバイステップのユースケースについては、この<a href="https://experienceleague.adobe.com/docs/journeys/using/use-cases-journeys/campaign-classic-use-case.html?lang=ja">節</a>を参照してください。</p>
</td>
</tr>
</tbody>
</table>

<table> 
<thead>
<tr> 
<th> <strong>LINE チャネルの強化</strong><br /> </th> 
</tr> 
</thead> 
<tbody> 
<tr> 
<td> <p>LINE チャネルに次の改善が追加されました。
</p>
<ul> 
<li><p>LINE ビデオメッセージのサポート</p></li>
<li><p>LINE Partner Registration API のサポート</p></li>
<li><p>LINE のサーバー側のエラーやネットワークタイムアウトが発生した場合、適切な再送信を実施ト</p></li>
</ul>
<p>詳しくは、<a href="../../delivery/using/line-channel.md">詳細ドキュメント</a>を参照してください。</p>
</td> 
</tr> 
</tbody> 
</table>

<table> 
<thead>
<tr> 
<th> <strong>Vertica Analytics FDA コネクタ</strong><br/> </th> 
</tr> 
</thead> 
<tbody> 
<tr> 
<td> <p>Adobe Campaign Classic インスタンスを Vertica 外部データベースに接続できるようになりました。この接続は、新しい外部アカウントで管理します。</p>
<p>詳しくは、<a href="../../installation/using/configure-fda-vertica.md">詳細ドキュメント</a>を参照してください。</p>
</td> 
</tr> 
</tbody> 
</table>

<table> 
<thead>
<tr> 
<th> <strong>Google BigQuery FDA コネクタ</strong><br /> </th> 
</tr> 
</thead> 
<tbody> 
<tr> 
<td> <p>Adobe Campaign Classic インスタンスを Google BigQuery 外部データベースに接続できるようになりました。この接続は、新しい外部アカウントで管理します。
</p>
<p>詳しくは、<a href="../../installation/using/configure-fda-google-big-query.md">詳細ドキュメント</a>を参照してください。</p>
</td> 
</tr> 
</tbody> 
</table>

**セキュリティ機能の強化**

* データベース接続の詳細をすべて返す **xtk:session#GetCnxInfo** API メソッドへのアクセスが、管理者ユーザーのみに制限されるようになりました。（NEO-27779）
* 非推奨の decryptString 関数は、CRM 関連の JavaScript ファイルの decryptPassword に置き換えられました。
* トラッキング署名機能を改善し、トラッキング対象リンクがサードパーティツール（メールクライアント、インターネットブラウザー、安全なリンクセキュリティツールなど）で変更された場合に、トラッキングリダイレクトエラーが発生するリスクを軽減しました。
* トラッキング対象の URL が大文字を含んでいると機能しなくなる場合がある問題を修正しました。トラッキング対象の URL の署名メカニズムで大文字と小文字を区別するようになりました。 （NEO-28414）

**互換性の更新**

Campaign で次のシステムがサポートされるようになりました。
* Google BigQuery FDA コネクタ
* Vertica Analytics FDA コネクタ
* PostgreSQL 13

詳しくは、[Campaign 互換性マトリックス](../../rn/using/compatibility-matrix.md)を参照してください。

**非推奨（廃止予定）の機能**

* Campaign 21.1 リリース以降、Adobe Analytics Connectorは非推奨になりました。このコネクタを使用している場合は、ご利用の実装に新しい Adobe Analytics Connectorを適用する必要があります。
* Debian 8 のサポートは廃止されました。
* 20.3 での Oracle CRM の廃止を受け、関連する外部アカウントがインターフェイスから削除されました。

詳しくは、[非推奨（廃止予定）の機能と削除された機能のページ](../../rn/using/deprecated-features.md)を参照してください。

**改善点**

* ワークフローを保存するときに、アクティビティ名が一意であり、移行の後には必ずアクティビティが続くことを確認するためのチェックを追加しました。
* **請求**&#x200B;テクニカルワークフローに、削除済みの「**アクティブな請求プロファイルの数**（billingActiveContactCount）」ワークフローで元々実行したタスクを含むようになりました。ワークフローで毎月送信するメールレポートで、インスタンス上のアクティブなプロファイルの数に関する情報が提供されるようになりました。[詳細情報](../../workflow/using/about-technical-workflows.md)。
* **_keyOnMData** 属性が新しく追加され、メモデータの操作にキーを使用できるようになりました。

**その他の変更**

* ガードレールが追加されて、マーケティングインスタンス上で[請求テクニカルワークフロー](../../production/using/monitoring-processes.md#billing-report)を実行できるようになりました。
* Windows 用 openssl サードパーティをバージョン 1.1.1h に更新しました。
* Debian パッケージの説明で、nlserver を Adobe Campaign Classic サーバーに変更しました。

**パッチ**

* 一定時間後にユーザーをログアウトするセッションタイムアウトを編集した際、設定時間が過ぎてもユーザーがログインしたままになる問題を修正しました。
* 配信が読み取り専用として表示されているのに、配信プロパティで引き続き編集可能となる問題を修正しました。
* Web アプリケーションを設計する際に、編集ツールバーが表示されないエラーを修正しました。
* メールにリンクを追加する際に、Adobe Campaign Classic ヘッダーが付いたテキストバージョンのメールが表示されるエラーを修正しました。（NEO-29211）
* HTTPS 接続で FDA を使用すると、**ミッドソーシング（配信ログ）**（defaultMidSourcingLog）ワークフローが、**NmsMidSourcing_LogsPeriodHour** オプションで設定した期間にスタックしていました。そのため、この設定期間後に発生したデータを使用してレコードが更新されませんでした。（NEO-30833）
* メッセージセンターの同期ワークフローを実行後に発生する問題を修正しました。配信オブジェクトフォルダーをカスタムフォルダーに移動するたびに、ワークフローによって配信が汎用の&#x200B;**トランザクションメッセージ履歴**&#x200B;フォルダーに戻されていました。 （NEO-27445）
* **ブロードキャスト統計**、**トラッキング指標**、**共有アクティビティ統計**&#x200B;などのレポートを表示しようとするとエラーメッセージが表示される問題を修正しました。
* Oracle CRM コネクタの廃止を受けて、**Oracle オンデマンド**&#x200B;ワークフローアクティビティをインターフェイスから削除しました。
* ワークフローサーバー（wfserver）モジュールを日次で再起動すると、処理ワークフローの実行が停止する問題を修正しました。 （NEO-30047）
* MX 管理ドキュメントが更新されず、IP 評価に悪影響を与える可能性がある問題を修正しました。 （NEO-29897）
* SOAP 呼び出しを受け取ると web プロセスがクラッシュする問題を修正しました。 （NEO-28796、NEO-29600）
* SAP HANA FDA インデックスの作成に失敗する問題を修正しました。 （NEO-29664）
* ヘッダーを含む SOAP 呼び出しを実行する際に、トランザクションメッセージが&#x200B;**待機**&#x200B;状態のままになる場合がある問題を修正しました。（NEO-28737）
* Teradata FDA コネクタを使用する際に発生していた問題を修正しました。すべての一時テーブルがクラスタの 1 つのノードでのみ作成されていたため、スプール領域全体を消費し、Teradata がクラッシュする場合がありました。一時テーブルは、多くのノードで生成されるようになります。 （NEO-28230）
* Web アプリケーションを使用する際に、トラッキングタグが **nms:trackingURL** スキーマに間違ったプライマリキーを生成する問題を修正しました。 （NEO-27931）
* ODBC 3.x との互換性を強化し、エラーメッセージの正確性を確保しました。
* カスタムコンテンツテンプレートをメール配信で使用する際に、コンソールがクラッシュする場合がある問題を修正しました。（NEO-31547）
* 接続が遅い、または応答サイズが大きいことが原因で Tomcat が有効な応答を送信できない問題を修正しました。（NEO-30858）
* PostgreSQL データベースから UUID を読み取る際に発生する場合がある問題を修正しました。
* オファーにリンクされた提案データの検索時に発生する場合がある、パフォーマンスの問題を修正しました。 （NEO-27554）
* IMS サービスをアクティブ化しても応答しなかった場合に、Web プロセスが応答しなくなる問題を修正しました。
* 特定の結合メカニズムが配信のパーソナライズに失敗したことにより、配達確認のグループを含む配信を送信できない問題を修正しました。 （NEO-14391）
* 配信テーブルをターゲットとしてクエリやエンリッチメントアクティビティを実施すると、アラートアクティビティでアラートを送信できない問題を修正しました。 （NEO-25157）

### リリース 21.1.2 - ビルド 9282 {#release-21-1-2-build-9282}

[!BADGE 非推奨（廃止予定）]{type=negative url="https://experienceleague.adobe.com/docs/campaign-classic/using/release-notes/rn-overview.html?lang=ja#rn-statuses" tooltip="非推奨（廃止予定）"}

_2021 年 4 月 15 日_

* パスワード管理が向上し、セキュリティが最適化されました。 
* MTA がクラッシュする可能性がある問題を修正しました。

### リリース 21.1.1 - ビルド 9277 {#release-21-1-1-build-9277}

[!BADGE 非推奨（廃止予定）]{type=negative url="https://experienceleague.adobe.com/docs/campaign-classic/using/release-notes/rn-overview.html?lang=ja#rn-statuses" tooltip="非推奨（廃止予定）"}

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

**メールフィードバックサービス（EFS）**&#x200B;は、拡張 MTA から直接フィードバックを取り込み、レポートの正確性を向上させる、スケーラブルなサービスです。この機能はプライベートベータ版としてリリースされており、今後のリリースですべての顧客が段階的に利用できるようになります。

* フィードバックのすべてのカテゴリが収集され、完全で正確なレポートが可能になりました。
* 配信済み指標の計算は、精度と反応性を向上させるために、拡張 MTA からのリアルタイムフィードバックに基づいておこなわれるようになりました。
* EFS は、同期ソフトバウンスレポートの遅延の問題を解決します。

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
* 日時型列の一括読み込み操作中のタイムゾーン管理に関連する MSSQL データベースの問題を修正しました。（NEO-27375）
* Redshift xtk 関数を使用する場合のワークフロークエリの問題を修正しました。SubDays、SubSeconds、SubMinutes、SubHours が両方の Redshift タイムスタンプ型を受け入れるようになりました。（NEO-24962）
* 匿名アクセスでレポートをプレビューしようとするとスクリプトエラーメッセージが表示される問題を修正しました。（NEO-27081）
* 配信分析を実行する際に、サーバーのメモリ使用量が減少する可能性がある問題を修正しました。
* 特定の複雑なクエリを実行しようとすると、インスタンスが動作しなくなる可能性がある問題を修正しました。
* **Twitter ページを同期する**&#x200B;テクニカルワークフローを実行できない可能性がある問題を修正しました。（NEO-28634）
* **ツイート（Twitter）**&#x200B;配信テンプレートを使用して X（旧 Twitter）に公開しようとすると、decryptPassword 関数に関連するエラーメッセージが表示される可能性がある問題を修正しました。（NEO-28216）
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
