---
product: campaign
title: Campaign Classic 2018 リリース
description: Campaign Classic 2018 リリースの詳細
exl-id: f70fceba-4bbf-4f33-8746-e4405a1cdae6
source-git-commit: f4513834cf721f6d962c7c02c6c64b2171059352
workflow-type: ht
source-wordcount: '5423'
ht-degree: 100%

---

# 2018 リリース{#release-2018}

![](../../assets/v7-only.svg)

## リリース 18.10

### リリース 18.10.6 - ビルド 8985{#release-18-10-6-build-8985}

2019 年 7 月 12 日

**強化点**

* ワークフローをインポートする際に Microsoft Dynamics で作成されたダミーレコードを削除できるようになりました。
* ファイルコレクターワークフローアクティビティで、ファイルへのアクセスが拒否された場合にエラーがループして記録される問題を修正しました。（NEO-12085）
* ユーザーアクティビティと、開封数配信指標のトラッキングレポートの間で、レポートに違いが発生していた問題を修正しました。（NEO-11742）
* 内部アカウントを使用する際にセキュリティゾーンパッケージを実行するための権限が改善されました。
* mtachild ログでエラーが発生する原因となっていた問題を修正しました。（NEO-8978）

### リリース 18.10.5 - ビルド 8984{#release-18-10-5-build-8984}

2019 年 4 月 23 日

**強化点**

* 同時分析／送信をおこなうと（同時に 2 つの配信を分析した場合）配信分析が失敗していた SQL デッドロックの問題を修正しました。（NEO-13026）
* データが失われる問題を修正するため、ワークフローヒートマップの 10,000 レコードの制限を削除しました。（NEO-12329）
* エンリッチメントワークフローアクティビティで「メインセットからのすべての追加データを維持」オプションを使用した際の問題を修正しました。（NEO-13291）

### リリース 18.10.4 - ビルド 8983{#release-18-10-4-build-8983}

2019 年 4 月 15 日

**強化点**

* トランザクションメッセージに対するトラッキング指標の計算プロセスの問題を修正しました。（NEO-12529、NEO-12581）
* すべてのコールバックが終了するまで HTTPRequest API が待機しなかった問題を修正しました。（NEO-12628）
* クーポン一時テーブルにインデックスを追加し、配信の送信を最適化しました。（NEO-12437）
* 日本語（.JP）ドメインの受信者をターゲットとしたメッセージを分析する際の問題を修正しました。（NEO-12246）
* Analytics 統合で、% 文字を使用した AAM セグメントデータを取得できるようになりました。（NEO-12025）
* HTTP2 を使用して通知を送信する際に Tomcat がクラッシュする問題を修正しました。（NEO-12701）

### リリース 18.10.3 - ビルド 8981{#release-18-10-3-build-8981}

2019 年 1 月 29 日

>[!CAUTION]
>
>このビルドはリコールされました。[最新のビルド](../../production/using/build-upgrade.md)にアップグレードするか、[アドビカスタマーケア](https://helpx.adobe.com/jp/enterprise/admin-guide.html/enterprise/using/support-for-experience-cloud.ug.html)にお問い合わせください。

**強化点**

* s3 ファイル転送ワークフローアクティビティの問題を修正しました。（NEO-12473）
* トラッキングワークフローが失敗することがあった問題を修正しました。（NEO-12520）
* IMS ログインの問題を修正しました。
* 大きなオファー ID を使用した際に、トランザクションメッセージにプレビューとコンテンツの承認で発生していた問題を修正しました。
* ミッドソーシング（配信カウンター）ワークフローの問題を修正しました。
* データベース構造を更新すると NmsRecipient 上にある新しいインデックスがドロップされていた問題を修正しました。
* 配信のメインターゲット用に「外部ファイルで定義」オプションを使用した際、コンソールのクラッシュが発生することがあった問題を修正しました。（NEO-12349）
* 複数の InMail クラッシュを修正しました。
* データを更新ワークフローアクティビティを使用して、FDA Teradata データベースに格納されているレコードを削除する際の問題を修正しました。
* 秘密鍵管理の不一致の問題を修正しました。
* フィールドに「xml=true and calculated=true」と入力したときのエンリッチメントアクティビティの問題を修正しました。
* モバイルアプリケーションでプッシュ通知を送信する際に文字がエスケープされる問題を修正しました。
* ミッドソーシング外部アカウントで FDA から SOAP 同期メソッドに切り替えることができない問題を修正しました。

### リリース 18.10.2 - ビルド 8978{#release-18-10-2-build-8978}

2018 年 12 月 6 日

>[!CAUTION]
>
>このビルドはリコールされました。[最新のビルド](../../production/using/build-upgrade.md)にアップグレードするか、[アドビスタマーケア](https://helpx.adobe.com/jp/enterprise/admin-guide.html/enterprise/using/support-for-experience-cloud.ug.html)にお問い合わせください。

**強化点**

* FDA で MySQL を使用してワークフローを実行する際に発生していた様々な問題を修正しました。（NEO-11652）
* プッシュ通知を送信する際のパフォーマンスの問題を修正しました。（NEO-11787）
* 配信でシードアドレスを使用する際に ID が枯渇していた問題を修正しました。（NEO-11842）
* 複雑なワークフローを使用する際にクライアントがフリーズすることがあった問題を修正しました。（NEO-11847）
* 1:N リンクを含む値の配分を使用する際に発生していた表示の問題を修正しました。（NEO-11820）
* ワークフローヒートマップでの Oracle エラーを修正しました。
* エンリッチメントアクティビティでオファーの提案を追加する際に発生していた権利の問題を修正しました。
* SQL データ管理接続の問題を修正しました。
* 負の ID の場合に一時的なワークフローテーブル名の生成で発生していた問題を修正しました。
* ワークフローヒートマップのワークフロー持続期間の計算で発生していた問題を修正しました。


### リリース 18.10.1 - ビルド 8977{#release-18-10-build-8977}

2018 年 11 月 5 日

>[!CAUTION]
>
>このビルドはリコールされました。[最新のビルド](../../production/using/build-upgrade.md)にアップグレードするか、[アドビカスタマーケア](https://helpx.adobe.com/jp/enterprise/admin-guide.html/enterprise/using/support-for-experience-cloud.ug.html)にお問い合わせください。

**新機能**

<table> 
 <thead> 
  <tr> 
   <th> 機能<br /> </th> 
   <th> 説明<br /> </th> 
  </tr> 
 </thead> 
 <tbody> 
  <tr> 
   <td> プッシュ通知の強化点<br /> </td> 
   <td> プッシュ通知に関する以下の様々な機能強化を Adobe Campaign に実装しました。<br /> 
    <ul> 
     <li> <p>iOS でのサイレント通知のトラッキング </p> </li> 
     <li> <p>iOS での登録呼び出しに関するフィードバックの実装</p> </li> 
     <li> <p>iOS 配信準備の時間の短縮</p> </li> 
    </ul> <p>Google の GCM 廃止予定に伴い、Android V2 コネクタは FCM サーバーにのみ接続可能になりました。</p><p>詳しくは、<a href="../../delivery/using/integrating-campaign-sdk-into-the-mobile-application.md">詳細ドキュメント</a>を参照してください。</p> </td> 
  </tr> 
  <tr> 
   <td> SQL データ管理アクティビティ<br /> </td> 
   <td> <p>新しいデータ管理ワークフローアクティビティが追加されました。<strong>SQL データ管理</strong>アクティビティでは、ワークテーブルを作成および設定する独自の SQL クエリを記述できます。 </p> <p>詳しくは、<a href="../../workflow/using/sql-data-management.md">詳細ドキュメント</a>を参照してください。</p></td> 
  </tr> 
  <tr> 
   <td> ワークフロー監視<br /> </td> 
   <td> <p>新しい Adobe Campaign Workflow HeatMap では、プラットフォーム管理者はすべての並列ワークフローをグラフィカルにすばやく確認できるので、インスタンスの負荷を監視し、それに応じてワークフローを計画することができます。</p> <p>詳しくは、<a href="../../workflow/using/heatmap.md">詳細ドキュメント</a>を参照してください。</p> <p>8977 より前のビルド（開始ビルド 8700）について、ワークフローヒートマップパッケージもオンデマンドで使用できます。リクエストおよびインストールについて詳しくは、<a href="https://helpx.adobe.com/jp/campaign/kb/install-workflow-heatmap-package.html">このページ</a>を参照してください。</p> </td> 
  </tr> 
 </tbody> 
</table>

**セキュリティの機能強化**

* SSRF（サーバーサイドリクエストフォージェリ）攻撃や DoS（サービス拒否）攻撃に対する脆弱性につながるセキュリティ上の問題を修正しました。（NEO-11453）
* X-Robots-Tag（nocache ヘッダー）を使用した場合に、Campaign からコンテンツ（トラッキングリダイレクト、ミラーページ、調査など）が提供されるようになりました。これにより、インターネット検索エンジンによるコンテンツのインデックス作成を防ぎます。（NEO-11101）
* 購読 API（nms:subscription:Unsubscribe および nms:subscription:Subscribe）の XTK 挿入の問題を修正しました。
* 購読解除 Web アプリケーションの XTK 挿入の問題を修正しました。
* 一部の SMS ログで不用意に表示されていたパスワードを削除しました。

**強化点**

* Campaign Classic API を[専用ページ](https://experienceleague.adobe.com/developer/campaign-api/api/index.html?lang=ja)から入手できるようになりました。jsapi.chm ファイルを使用していた場合は、新しいオンラインバージョンを参照する必要があります。
* PostgreSQL 10、Debian 9 および Teradata 16.20 がサポートされるようになりました。[互換性マトリックス](https://helpx.adobe.com/jp/campaign/kb/compatibility-matrix.html)を参照してください。
* SFTP 接続を作成する際、プロキシ認証を使用できるようになりました。詳しくは、[詳細ドキュメント](../../installation/using/file-res-management.md)を参照してください。（NEO-9868）
* ダイレクトメール配信テンプレートを使用して単一の配信を作成する際、配信プロパティで「**日付計算式**」オプションを使用できるようになりました。（NEO-9792）
* Cookie のトラッキングと Web アプリケーションで、ドメイン名管理が強化されました。詳しくは、以下の「技術面の変更点」の節を参照してください。
* 配信やランディングページでの Adobe Experience Cloud の共有アセットのインポートがセキュリティとパフォーマンスの面で強化されました。
* モバイルチャネルの外部アカウントで、ログファイルの詳細 SMPP トレースを有効にする新しいチェックボックスが使用可能になりました。これにより、Adobe Campaign インターフェイスから直接この出力にアクセスできます。
* broadLog で、接続の最大数と 1 時間あたりのメッセージの最大数が区別されるようになりました。限界値に達した場合、スループットが制限される理由を判別できます。これまでは、どちらの場合にも同じメッセージ（「割り当てに達しました」）が表示されていました。
* プールから接続を取得する際に実行する SQL スクリプトを指定できるようになりました。このスクリプトはデフォルトのスキーマを設定するために使用できます。このスクリプトは Query Banding の後に適用されます。（NEO-11256）
* PII（個人識別情報）の規制遵守のため、Campaign SDK ではユーザー ID を保存しなくなりました。データはハッシュとして保存されるようになりました。
* パッケージのエクスポート XML ファイルをインポートする際、ファイル内でエンコードが明確に宣言されていても、ファイル内に存在する BOM がサポートされるようになりました。

**技術面の変更点**

クライアントおよびサーバーのアップグレード

>[!CAUTION]
>
>サーバーを既に 18.10 に更新済みの場合、サーバーにアクセスするには 18.10 クライアントを使用する必要があります。18.10 クライアントは前のバージョンのサーバーにも接続できます。

ドメイン名管理

Cookie のトラッキングと Web アプリケーションで、ドメイン名管理が強化されました。

2 文字のセカンドレベルドメイン名（例：.aa.com）がデフォルトでサポートされるようになりました。より複雑なドメイン名（.com.au のような 3 文字のセカンドレベルドメイン名）の場合は、serverConf の **cookieDomains** オプション（リダイレクトタグ内）に追加する必要があります。次に例を示します。

```
<redirection cookiedomain="http://toureiffel.paris">
```

インデックスの機能強化

NmsRecipient のインデックスが修正されました。これにより、このテーブルを使用するクエリのパフォーマンスが向上します。NmsRecipient の拡張を既に実施している場合、新しいインデックスとの重複がないか確認することをお勧めします（データベースサーバー上のスペース使用量を最小化するため）。（NEO-8228）

PostgreSql で UTF-8 照合順序を使用する際、「LIKE &#39;string%’」（または「starts with」）の演算を最適化するインデックスを作成できるようになりました。同じ列に対して他の演算（order by や join など）を実行する場合は、別の標準的なインデックスが必要になります。スキーマにおいては、これはインデックス定義に「indexOption=&quot;searchFromStart&quot;」を追加することで可能になります（標準的な btree インデックスの代わりに varchar_pattern_ops インデックスが作成されます）。次に例を示します（NmsRecipient の場合）。

```
<dbindex name="email2"> <!-- optimize order by/join (and startWith if not PostgreSql with an UTF-8 collation) operations -->
  <keyfield xpath="@email"/>
</dbindex>
<dbindex name="email3" indexOption="searchFromStart"><!-- optimize startsWith operation on PostgreSql when a UTF-8 collation is used; create no index in other cases-->
  <keyfield xpath="@email" />
</dbindex>
```

（「スケジュール済み」列で）NmsRtEvent および NmsEventHisto に新しいインデックスが追加されました。これにより、対応するフォームの表示時間が短縮されます。（NEO-11738）

これらのインデックスの変更により、アップグレード後のタスクの実行に時間がかかる場合があります。

**パッチ**

* **Web ダウンロード**&#x200B;ワークフローアクティビティからファイルをダウンロードできないエラーを修正しました。（NEO-11105）
* **指標とキャンペーン属性の送信**&#x200B;ワークフローが時折、失敗状態のままになるエラーを修正しました。（NEO-10820）
* ワークフローでリスト更新アクティビティを実行した後に作成された受信者リストが削除される問題を修正しました。（NEO-11696）
* （日本語インスタンスの）キャンペーンカレンダーでキャンペーンが誤って 1 ヶ月先に表示される問題を修正しました。（NEO-11445）
* 配信プロパティの「Web 分析」タブで分析設定の表示を妨げていた問題を修正しました。（NEO-11619）
* nms:delivery 入力フォームを編集および保存しようとするときに表示されていたエラーを修正しました。（NEO-10973）
* ファイル転送アクティビティを含むワークフローを実行しているときに発生していた外部アカウント設定の問題を修正しました。（NEO-11012）
* データの読み込みアクティビティで zcat 関数を使用してファイルを読み込むと空行が返されていた問題を修正しました。（NEO-11273）
* 配信の分析中に配信ログが重複して生成されていた問題を修正しました。（NEO-11360）
* ワークフローでエンリッチメントアクティビティを実行した後、外部リンクキーの欠如が原因で配信が失敗する問題を修正しました。（NEO-11537）
* Adobe Campaign のインストールパスに GB18030 の特定の中国語文字が含まれている場合に、インストールや修正を正常に実行できなかった問題を修正しました。
* 一部のトラッキングログを誤った配信にリンクしていた問題を修正しました。（NEO-11412）
* 配信ログの一部が通常よりも長く保留中ステータスのままになることがある問題を修正しました。（NEO-11336）
* クエリを編集して配信にクーポンを追加する際に発生していたエラーを修正しました。（NEO-11037）
* どの集計演算子を選択しても、グラフでは常に値の合計が計算されるというレポートの問題を修正しました。（NEO-10913）
* 「request.scheme」関数は廃止されたので、JSAPI ドキュメントから削除されました。（NEO-10828）
* 特定のタイムゾーン設定を使用している一部のユーザーが Adobe Campaign にログインできない問題を修正しました。（NEO-10712）
* 拡張された汎用 SMPP コネクタを使用してモバイルチャネルの外部アカウントを設定する際に起きていた問題を修正しました（受信者に対して別のパラメーターを使用するよう指定した場合、トランスミッターがそれ自体のパラメーターではなく指定したパラメーターを誤って使用してしまうという問題）。
* 最初の判別後、配信は常に再計算されるので、頻度ルールに頻度を設定すると、スケジュールされた配信が失敗してしまう問題を修正しました。（NEO-10016）
* アプリケーションプールのリサイクルプロセス（nlsrvmod.dll ライブラリ内）中に IIS Web サーバーがクラッシュしてしまう問題を修正しました。（NEO-10862）
* **プロファイルとターゲット**&#x200B;画面で受信者を検索できない場合がある問題を修正しました。（NEO-8228）
* レコード数が多い場合、イベント履歴フォルダーにアクセスするとタイムアウトエラーが生じることがある問題を修正しました。（NEO-11738）
* LINE 配信受信者が誤って「未到達」と返される場合がある問題を修正しました。（NEO-10833）
* Oracle で列を追加してワークフロークエリを実行する際の問題を修正しました。（NEO-11615）
* 閉じられた接続が接続プールに長時間保持されないようにするための機能強化が実施されました。（NEO-11392）
* （テーブル名、フィールド名などに）UTF8 文字を含み、システムによって生成されたデフォルトの制限名を持つプライマリキー制限も含む外部の Oracle テーブルに FDA 経由で接続されたターゲティングワークフローアクティビティ（クエリ、データ読み込み（RDBMS）など）を使用する際の問題を修正しました。（NEO-10714）
* 配信の HTML コンテンツを削除できない場合がある問題を修正しました。（NEO-11327）
* キャンペーンの実行後、ダイレクトメール内の XML および CSV ファイルのプレビューの問題を修正しました。（NEO-11290）
* エンリッチメントワークフローアクティビティでデータを並べ替える際の問題を修正しました。（NEO-11394）
* カスタムレポートでデータを並べ替える際の問題を修正しました。（NEO-10896）
* Teradata で useVault 設定を使用したときにエラーが起きる問題を修正しました。（NEO-11399）
* 複数のクエリ行を削除すると、Adobe Campaign クライアントコンソールがクラッシュする問題を修正しました。（NEO-10744）
* ダイレクトメールを配信する際に頻度ルールが適用されないことがある問題を修正しました。（NEO-9004）
* データの読み込みアクティビティを使用して「時刻」データタイプの列をインポートする際に発生する、時間区切り記号を削除してもリセットされる問題を修正しました。（NEO-10743）
* 繰り返し配信を編集するときに配信プロパティの実行フォルダーリストから配信フォルダーを表示できない問題を修正しました。（NEO-11094）
* 母集団を表示ウィンドウで、ワークフロー内のクエリアクティビティの結果のターゲットとして 200 を超えるレコードを表示できない問題を修正しました。（NEO-11195）
* 1000 個を超える要素が選択されている状態で DELETE クエリを実行できない問題を修正しました。（NEO-11171）
* Android プッシュ通知配信の追加パラメーターで URL がトラッキングされる URL としてエンコードされる問題を修正しました。（NEO-11468）
* パラメーターを「1 日置き」および「開封数」に設定した場合にユーザーアクティビティレポートで発生するスクリプトエラーを修正しました。（NEO-11655）
* ミッドソーシングサーバーに接続するとき、または認証済み Web プロキシ経由で Message Center に接続するときに発生する問題を修正しました。（NEO-11309）
* **SQL ビューに基づいた**&#x200B;特定のスキーマの要素を選択した後に新しい配信コンポジションを保存すると発生する Oracle のエラーを修正しました。（NEO-11682）
* 「解凍」オプションを使用してファイルを読み込みアクティビティ経由で .csv ファイルを含んだ zip ファイルを処理すると、誤検出を含んだ却下ファイルが生成される問題を修正しました。
* xtkjoblog はクリーンアップでパージされるようになりました。

## リリース 18.6

### リリース 18.6.2 - ビルド 8949{#release-18-6-3-build-8949}

2018 年 8 月 22 日

>[!CAUTION]
>
>このビルドはリコールされました。[最新のビルド](../../production/using/build-upgrade.md)にアップグレードするか、[アドビカスタマーケア](https://helpx.adobe.com/jp/enterprise/admin-guide.html/enterprise/using/support-for-experience-cloud.ug.html)にお問い合わせください。

**新機能**

<table> 
 <thead> 
  <tr> 
   <th> 機能<br /> </th> 
   <th> 説明<br /> </th> 
  </tr> 
 </thead> 
 <tbody> 
  <tr> 
   <td> Query Banding<br /> </td> 
   <td> <p>複数のキャンペーンユーザーが同じ FDA Teradata 外部アカウントに接続したときに、各ユーザーに固有の query band（キー/値のペア）を渡すことができるようになりました。Campaign ユーザーが Teradata データベースに対してクエリを実行するたびに、Adobe Campaign はそのユーザーに関連付けられたメタデータを送信できます。これらのデータはキーと値のリストで構成されており、Teradata 管理者が監査目的やアクセス権限の管理などに利用できます。</p><p>詳しくは、<a href="../../installation/using/external-accounts.md">詳細ドキュメント</a>を参照してください。</p> </td>
  </tr> 
 </tbody> 
</table>

**強化点**

* E メールのアーカイブログが強化され、どの E メールが正常に配信されたかまたは BCC アーカイブで失敗したかがより簡単にはっきりと確認できるようになりました。（NEO-10675）
* トラッキングブロードログでカスタマー IP の代わりにロードバランサー IP が表示されてしまうという問題を修正しました。（NEO-11295）
* 配信のプロパティが誤って上書きされるというランダム問題を修正しました。（NEO-11015）
* エンリッチメントアクティビティの結果を並べ替えるときの構文エラーを修正しました。（NEO-11394）
* **[!UICONTROL 調査の回答]**&#x200B;ワークフローアクティビティの計算フィールドを使用した際に発生する問題を修正しました。（NEO-11382）
* Tomcat は脆弱性の悪用を避けるために更新されました。（NEO-11503）
* PostgreSQL データベースへの FDA 接続を使用した際に LATIN1 エンコードで発生するエラーを修正しました。（NEO-11299）
* 「**[!UICONTROL ワークフローを使用してパーソナライゼーションデータを準備]**」配信オプションを使用したときに発生する問題を修正しました。（NEO-11047）
* 拡張コネクタの使用時に SMS が送信されることを妨げるポストアップグレードの問題を修正しました。
* パッケージのインポート/エクスポートを改善しました（ログと領域がインターフェイスに追加されました）。
* **[!UICONTROL 調査の回答]**&#x200B;ワークフローアクティビティが完全に設定されていないときに、ポストアップグレードログに役に立たないエラーが表示されるという問題を修正しました。

**技術面の変更点**

Query Banding

Teradata ユーザーまたは役割を Campaign ユーザーに関連付けるには、固有のキー（PROXYUSER または PROXYROLE）を使用します。このプロキシユーザーや役割を使用できる新しい権限が追加されました。GRANT CONNECT THROUGH アクセス権をデータベースアカウント（Teradata 外部アカウントで定義されたもの）に追加する必要があります。

Teradata 外部アカウントに新しいタブが追加されました。「**[!UICONTROL Query Banding]**」タブには以下のオプションがあります。

* **[!UICONTROL アクティブ]**：このボックスをオンにすると、この機能が有効になります。
* **[!UICONTROL デフォルト]**：ユーザーに関連付けられている Query Banding がない場合に使用する、デフォルトの Query Banding を入力します。デフォルトの Query Banding が定義されていないと、Query Banding が関連付けられていないユーザーは Teradata を使用できません。
* **[!UICONTROL ユーザー]**：ユーザーごとに、Query Banding を指定します。キーと値のペアを必要な数だけ追加できます。例：‘priority=1;workload=high;’

Query Banding について詳しくは、以下の記事を参照してください。

* [https://docs.teradata.com/reader/cY5B~oeEUFWjgN2kBnH3Vw/a5G1iz~ve68yTMa24kVjVw](https://docs.teradata.com/reader/cY5B%7EoeEUFWjgN2kBnH3Vw/a5G1iz%7Eve68yTMa24kVjVw)
* [https://docs.teradata.com/reader/rgAb27O_xRmMVc_aQq2VGw/qVNfdszBssrZ7ttrE7AtmQ](https://docs.teradata.com/reader/rgAb27O_xRmMVc_aQq2VGw/qVNfdszBssrZ7ttrE7AtmQ)

### リリース 18.6.1 - ビルド 8947{#release-18-6-build-8947}

2018 年 6 月 25 日

>[!CAUTION]
>
>このビルドはリコールされました。[最新ビルドにアップグレードする](../../production/using/build-upgrade.md)か、[テクニカルサポート](https://helpx.adobe.com/jp/enterprise/admin-guide.html/enterprise/using/support-for-experience-cloud.ug.html)にお問い合わせください。

**新機能?**

<table> 
 <thead> 
  <tr> 
   <th> 機能<br /> </th> 
   <th> 説明<br /> </th> 
  </tr> 
 </thead> 
 <tbody> 
  <tr> 
   <td> セキュリティの強化<br /> </td> 
   <td> Campaign Classic に対して一連のセキュリティ強化が追加されました。機能強化および修正点を次に示します。<br /> </td> 
  </tr> 
  <tr> 
   <td> Windows Server 2016 のサポート<br /> </td> 
   <td> Adobe Campaign は現在、Windows Server 2016 に対応しています。<a href="https://helpx.adobe.com/jp/campaign/kb/compatibility-matrix.html">Campaign Classic の互換性マトリックス</a>を参照してください。<br /> </td> 
  </tr> 
 </tbody> 
</table>

**セキュリティの機能強化**

decryptString

**decryptString** 関数は廃止される予定です。[廃止される機能および削除された機能](deprecated-features.md)についての記事を参照してください。

新規のお客様は、ランディングページで受信者の暗号化 ID を復号化する際にのみ、この関数を使用します。外部アカウントに保管されているパスワードを復号化するには、新しい **decryptPassword** 関数を使用します。

既存のお客様にとっては、この関数の動作は変わりませんが、**decryptString** の代わりに **decryptPassword** を使用することをお勧めします。この関数を引き続き使用できるように、**XtkSecurity_Unsafe_DecryptString** 互換性オプションがアップグレード後に追加されて、デフォルトで有効になります。**decryptString** を無効にする場合は、このオプションを無効にします。

decryptPassword

**decryptPassword** 関数が追加されました。この関数を使用して、外部アカウントに格納されたパスワードを復号化できます。詳しくは、[JSAPI](https://helpx.adobe.com/jp/campaign/kb/compatibility-matrix.html) ドキュメントを参照してください。

ファイル API

新規インストールでは、ファイル API を介したフォルダーアクセスが、Adobe Campaign の **var**、**sftp**、一時フォルダーに限定されます。

既存のお客様は、ファイル API で Adobe Campaign の **conf** フォルダーにアクセスできなくなりました。他のフォルダーにアクセスできるように、**XtkSecurity_Disable_JSFileSandboxing** 互換性オプションがアップグレード後に追加されて、デフォルトで有効になります。アクセスを Adobe Campaign の **var**、**sftp**、一時フォルダーに限定する場合は、このオプションを無効にします。

**パッチ**

* SMS トランザクションメッセージのパフォーマンスを低下させる可能性のある問題を修正しました。（NEO-9812）

## リリース 18.4

### リリース 18.4.5 - ビルド 8937{#release-18-4-5-build-8937}

2018 年 11 月 21 日

**強化点**

* FDA で MySQL を使用してワークフローを実行する際に発生していた様々な問題を修正しました。（NEO-11652）
* 特定の事例で、配信母集団の一部が保留中状態のままになっていた問題を修正しました。（NEO-11336）
* SMS 自動応答で発生していた断続的な問題を修正しました。（NEO-11811）
* 配信でシードアドレスを使用する際に ID が枯渇していた問題を修正しました。（NEO-11842）
* エンリッチメントワークフローアクティビティで並べ替えを実行する際の構文エラーを修正しました。（NEO-11394）
* IIS を再起動すると Web サーバーがクラッシュしていた問題を修正しました。（NEO-10862）
* ビルドをアップグレード（FDA - SQL）した後でトラッキングワークフローが失敗していた問題を修正しました。（NEO-11635）
* ワークフローリストデータが消失していた問題を修正しました。（NEO-11696）
* プッシュ通知を送信する際のパフォーマンスの問題を修正しました。（NEO-11787）
* 「com.au」ドメインに Web トラッキングが機能しなかった問題を修正しました。
* 複雑なワークフローを使用する際にクライアントがフリーズすることがあった問題を修正しました。（NEO-11847）
* 特定のスキーマの要素を選択した後で新しい配信を保存すると発生していた Oracle のエラーを修正しました。（NEO-11682）
* アクセント記号付きの文字を含むフィールドをクエリする際に発生していた問題を修正しました（FDA／Teradata）。外部アカウントで、Teradata ドライバーとの通信に使用するエンコードを変更できるようになりました。（NEO-11818）
* トラッキングで、プッシュ通知の追加の変数に URL を渡す際に、誤った形式または正しくないデータがモバイルアプリケーションで受信されていた問題を修正しました。（NEO-11468、NEO-11960）
* 1:N リンクを含む値の配分を使用する際に発生していた表示の問題を修正しました。（NEO-11820）
* 一括読み込みが Teradata 16 で機能しなかった問題を修正しました。
* 15.10 ドライバーでのバインディングの問題を避けるために、Teradata 上のタイムスタンプのバッファーサイズを増やしました。
* ポストアップグレード時の問題の原因となっていた長い名前のインデックスの管理を改善しました。
* 子プロセスが無効の際に使用できる共有メモリを改善しました（MTA）。
* Apache で発生する可能性のあるデッドロックの問題を修正しました（トラッキング）。


### リリース 18.4.4 - ビルド 8936{#release-18-4-4-build-8936}

2018 年 8 月 1 日

**強化点**

* E メールのアーカイブログが強化され、どの E メールが正常に配信されたかまたは BCC アーカイブで失敗したかがより簡単にはっきりと確認できるようになりました。（NEO-10675）
* トラッキングブロードログでカスタマー IP の代わりにロードバランサー IP が表示されてしまうという問題を修正しました。（NEO-11295）
* PostgreSQL データベースへの FDA 接続を使用した際に LATIN1 エンコードで発生するエラーを修正しました。（NEO-11299）
* 「**[!UICONTROL ワークフローを使用してパーソナライゼーションデータを準備]**」配信オプションを使用したときに発生する問題を修正しました。（NEO-11047、NEO-11301）
* 配信のプロパティが誤って上書きされるというランダム問題を修正しました。（NEO-11015）
* **[!UICONTROL 調査の回答]**&#x200B;ワークフローアクティビティの計算フィールドを使用した際に発生する問題を修正しました。（NEO-11382）
* **[!UICONTROL 調査の回答]**&#x200B;ワークフローアクティビティで、XML 形式で格納されているデータを使用した際に発生する問題を修正しました。（NEO-10816）
* ビルド 8935 でサーバーアップグレードを実行するときに発生する問題を修正しました。
* **[!UICONTROL 調査の回答]**&#x200B;ワークフローアクティビティが完全に設定されていないときに、ポストアップグレードログに役に立たないエラーが表示されるという問題を修正しました。
* FDA Teradata：SQL テーブルの自動増分フィールドとインデックスで発生する問題を修正しました。

### リリース 18.4.3 - ビルド 8935{#release-18-4-3-build-8935}

2018 年 6 月 22 日

**強化点**

* Microsoft Edge および Internet Explorer で発生していたエンコードのトラッキングの問題を修正しました。（NEO-11257）
* LINE 配信での画像リンクのパーソナライゼーションに伴う問題を修正しました。（NEO-11077）
* ID シーケンス生成メカニズムが正常に機能しない問題を修正しました。（NEO-11115）
* カスタム名前空間で integer タイプの紐付けキーを使用する場合に、プライバシー（GDPR）要求が機能しない問題を修正しました。（NEO-11123）
* **[!UICONTROL クエリ]**&#x200B;ワークフローアクティビティで「**[!UICONTROL 値の配分]**」オプションを使用する場合に発生することがあったエラーを修正しました。（NEO-10958）
* マーケティングインスタンスからインタラクションインスタンスにオファースペースを同期する際の問題を修正しました。（NEO-11162）
* ポストアップグレード時の長い名前のインデックスの管理を強化しました。

### リリース 18.4.2 - ビルド 8932{#release-18-4-2-build-8932}

2018 年 5 月 22 日

**強化点**

* Windows Server Update が正常に機能しない問題を修正しました。
* XML 形式で格納されているデータを使用する際の&#x200B;**[!UICONTROL 調査結果]**&#x200B;アクティビティに関する問題を修正しました。レポートが正しく表示されませんでした。（NEO-10816）
* バウンスメールサーバーを使用する際に inMail プロセスで発生することがあった、パフォーマンスの問題を修正しました。（NEO-10641）
* 1000 を超えるスキーマをアップグレードする際に発生することがあった、データベースアップグレードの問題を修正しました。

### リリース 18.4.1 - ビルド 8931{#release-18-4-build-8931}

2018 年 4 月 24 日

**新機能?**

<table> 
 <thead> 
  <tr> 
   <th> 機能<br /> </th> 
   <th> 説明<br /> </th> 
  </tr> 
 </thead> 
 <tbody> 
  <tr> 
   <td> EU 一般データ保護規則（GDPR）<br /> </td> 
   <td> <p>GDPR は 2018 年 5 月 25 日より欧州連合（EU）にて新しく施行されるプライバシー保護法律で、データ保護要件を現代の状況に合わせて整合化させることを目的としています。GDPR は、EU に居住しているデータ主体のデータを保有している Adobe Campaign の顧客に適用されます。</p> <p>Adobe Campaign には既にプライバシー機能（同意管理、データ保持設定、ユーザーの役割など）が用意されていますが、これを機会にデータ管理者としてお客様自身が特定の GDPR 要件に対応できるようにする機能を導入しました。</p> 
    <ul> 
     <li> <p>アクセス権限：データ主体は、データ管理者により取得された自分の個人データのコピーを受け取ることができます。これには Adobe Campaign に保存されているデータも含まれている場合があります。</p> </li> 
     <li> <p>削除権限：データ主体は、データ管理者により取得された自分の個人データを消去させることができます。これには Adobe Campaign に保存されているデータも含まれている場合があります。</p> </li> 
    </ul> 詳しくは、<a href="https://helpx.adobe.com/jp/campaign/kb/acc-privacy.html">詳細ドキュメント</a>を参照してください。<br /> </td> 
  </tr> 
  <tr> 
   <td> アクティブなプロファイル<br /> </td> 
   <td> <p>Adobe Campaign では、アクティブなプロファイルのリストの提供と、専用ワークフローによるそのリストの月次更新がおこなわれるようになりました。</p> <p>詳しくは、<a href="../../platform/using/about-profiles.md#active-profiles">詳細ドキュメント</a>を参照してください。</p> </td> 
  </tr> 
  <tr> 
   <td> Android プッシュコネクタの機能強化<br /> </td> 
   <td> <p>Android コネクタが高スループットに対応するように強化されました。 </p> <p>詳しくは、<a href="../../delivery/using/configuring-the-mobile-application.md">詳細ドキュメント</a>を参照してください。</p> </td> 
  </tr> 
 </tbody> 
</table>

**セキュリティの機能強化**

* 認証されていないユーザーからの潜在的な攻撃を防ぐために、外部エンティティの拡張が無効になりました。（NEO-10173）
* 標準ユーザーがアプリケーションアクセス URL、LDAP 設定などのインスタンス設定パラメーターを変更するのを防ぐために、権限が堅牢化されました。（NEO-10171）
* スタックトレース経由で機密情報が漏洩する可能性がある問題を修正しました。外部ネットワークからアクセスできない場所にエラー詳細がバックエンドで記録されるようになりました。（NEO-10176）
* 管理者がアップロードしたドキュメントやエクスポートしたパッケージを標準ユーザーが表示するのを防ぐために、権限が堅牢化されました。（NEO-10170）

**強化点**

* **LINE チャネル - アーキテクチャ機能強化**：Adobe Campaign のその他すべてのチャネルと同じように、LINE チャネルがすべてのデプロイメントタイプ（ホスト、ハイブリッド、オンプレミス）でサポートされるようになりました。
* **シーケンス自動生成**：ID 生成メカニズムが強化され、オブジェクトが大量にあるキャンペーンインスタンスの存続期間が長くなりました。

**その他の変更**

* コマンドラインを使ってパッケージをインポートする新しいモードが使用可能になり、循環依存関係（サイズの大きいパッケージでは推奨されません）に対応できるようになりました。詳しくは、「技術面の変更点」の節を参照してください。（NEO-8979）
* Teradata で大量のデータを読み込む際のパフォーマンスが向上し、処理されたデータの適切な値がログに表示されない問題が解決されました。（NEO-10429）
* Audience Manager からのオーディエンスのインポートが分割ファイルで正しく機能するようになりました。これまでは、importSharedAudience テクニカルワークフローによってセグメントの最後のファイルのみがインポートされていました。（NEO-10156）
* Windows で、Campaign サーバーのデフォルトインストールパスが変更されました。64 ビットバージョンのセットアップを起動する際、デフォルトのインストールパスが次のようになりました。**C:\Program Files\Adobe\Adobe Campaign Classic v7**（以前のパスは **C:\Program Files (x86)\Adobe\Adobe Campaign Classic v7**）
* デフォルトの MX ルールが強化され、含まれるドメイン数が増えると共にスループットが最適化されています。
* デプロイウィザードの SOAP 呼び出しに対する強制的なアクセス制限（xtk:serverOptions#SaveOptions）。
* 古い weka.jar ライブラリが削除され、OpenSSL ライブラリがセキュリティの最適化のために更新されました。
* インスタンスのパフォーマンス確保のために請求のテクニカルワークフローが改良されました。
* 管理者が任意のオペレーターのパスワードを設定またはリセットできる機能が復元されました。そのためには、オペレーターを右クリックし、**[!UICONTROL アクション]**／**[!UICONTROL パスワードをリセット]**&#x200B;を選択して、そのオペレーターの新しいパスワードを設定します。オペレーターが最初の再接続時にパスワードを変更することをお勧めします。詳しくは、[詳細ドキュメント](../../production/using/lost-password.md)を参照してください。
* 新しいマルチテナンシー機能を Adobe Target でサポートするために、Target との統合のためのオプションおよび外部アカウントの設定時に、新しい「at_property」パラメーターを URL に追加できるようになりました。このパラメーターに使用する値は、Adobe Target で参照でき、Target の呼び出し時に Campaign で使用されます。詳しくは、[詳細ドキュメント](../../integrations/using/inserting-a-dynamic-image.md)を参照してください。
* Adobe Target によって提供される画像をクリックしたときに開くデフォルトのランディングページを指定できるようになりました。これまでは、この画像をクリックすると、電子メールの作成時に設定したデフォルト画像が表示されました。詳しくは、[詳細ドキュメント](../../integrations/using/inserting-a-dynamic-image.md)を参照してください。
* トレース出力を強制的におこなうための「**SMPP トレースを有効にする**」チェックボックスが外部アカウントに追加されました。詳しくは、[詳細ドキュメント](../../delivery/using/sms-set-up.md#creating-an-smpp-external-account)を参照してください。

**技術面の変更点**

queryDef

queryDef に対して「orderBy」句に関する変更がおこなわれました。変更前は、クエリ対象テーブルのプライマリキーが暗黙的に「orderBy」句に追加されていました。一部のデータベースエンジン（postgresql など）では、このためにインデックスが使用できなくなります（orderBy 句のすべてのフィールドが同じインデックスでカバーされる必要があります）。これまでこの挙動を利用していた場合は、「orderBy」句にプライマリキーを明示的に追加する必要があります。

例えば、次のクエリがあるとします。

```
<queryDef operation="select" schema="xtk:job" startPath="/" xtkschema="xtk:queryDef">
  <select>
     <node expr="@id"/>
   </select>
   <orderBy>
     <node expr="@logDate"/>
   </orderBy>
</queryDef>`
```

このクエリは暗黙的に次のように渡されていました（18.4 の変更前の場合）：

```
<queryDef operation="select" schema="xtk:job" startPath="/" xtkschema="xtk:queryDef">
  <select>
     <node expr="@id"/>
   </select>
   <orderBy>
      <node expr="@logDate"/>
      <node expr="@id"/> <!-- implicitly added before 18.4, you can add it manually on your query, if you relied on this implicit order clauses --!>
   </orderBy>
</queryDef>
```

urlEncode 関数

JavaScript の &#39;urlEncode&#39; 関数は、非 ASCII 文字に対して適切に機能していませんでした。この点が是正され、すべての Unicode 文字（日本語の文字を含む）で機能するようになりました。これまで非 ASCII 文字に対する &#39;urlEncode&#39; の挙動を利用していた場合は、コードの変更が必要になります。

パッケージインポートの新しいモード

コマンドラインを使ってパッケージをインポートする新しいモードが使用可能になり、循環依存関係（サイズの大きいパッケージでは推奨されません）に対応できるようになりました。既存の機能は維持されています。循環依存関係があるパッケージのために、新しいフラグ **-usejs** がコマンドラインのパッケージインポートに追加されました。実行時には、パッケージインポートがインターフェイスから実行されたときと同様に JSEngine が使用されます。

```
nlserver package -instance:fresh -import:sup-packInstallTest.xml -verbose -usejs
```

**パッチ**

* 配信およびトラッキングログを Adobe Campaign 標準版から Adobe Campaign Classic にレプリケートする際の同期の問題を修正しました。（NEO-10023）
* 高速読み込み操作でのエラー発生後に ETL ワークフローが再開されたときの Teradata でのエラーおよびログテーブルの処理に関する問題を修正しました。ワークフローを再開するたびにエラーおよびログテーブルが適切に削除されるようになりました。（NEO-10672）
* FDA パッケージがインストールされている場合の Hive パッケージ（Hadoop で必要）の自動インストールに関するポストアップグレードの問題を修正しました。（NEO-10592）
* 無効なドメインを&#x200B;**未定義**&#x200B;エラーとして処理していたエラーを修正しました。（NEO-10248）
* Android プッシュ配信を送信する際の deliveryLogStats テーブルでの重複ログの問題を修正しました。（NEO-10234）
* 特定のバーコード形式をバーコードスキャナーで読み取れなくなる可能性がある問題を修正しました。（NEO-10125）
* JavaScript の &#39;urlEncode&#39; 関数で非 ASCII 文字を使用したときの問題を修正しました。詳しくは、「技術面の変更点」の節を参照してください。（NEO-10123）
* sha256 関数を含むクエリを Teradata データベースに対して実行したときの問題を修正しました。（NEO-10119）
* 大規模な SalesForce テーブルの使用時に SalesForce アクティビティで発生するおそれがあるワークフローメモリーエラーを修正しました。（NEO-9900）
* FDA 使用時のワークフローアクティビティのターゲティングにおける「**補集合を生成**」オプションの問題を修正しました。（NEO-9878）
* ミッドソーシング使用時にマーケティングインスタンスで「**処理済み**」および「**成功**」の指標が更新されなくなる可能性がある問題を修正しました。（NEO-9454）
* プラットフォーム内のオファーが 10,000 件を超える場合のインタラクションの再提案なしルールを修正しました（NEO-9352）
* XML 外部ファイルの使用時に配信のターゲットを指定できなくなる可能性がある問題を修正しました。（NEO-9312）
* オファーに対する仮説の実行や提案のステータス更新をおこなう際のワークフローエラーにつながるおそれがある問題を修正しました。（NEO-9304）
* Android 配信マッピングの属性に基づく頻度ルールを使用した場合の配信分析中に発生するエラーを修正しました。（NEO-9202）
* パフォーマンスの問題を引き起こす可能性がある、受信者リストの列を並べ替える際の問題を修正しました。queryDef の変更について詳しくは、以下の「技術面の変更点」の節を参照してください。（NEO-9042）
* 特に Federated ID ログインタイプの使用時に、承認電子メールのリンクが誤ったログイン URL を指している問題を修正しました。（NEO-9011）
* 特定のタイムゾーンのレポートの日付選択で間違った日付が表示される可能性がある問題を修正しました。（NEO-9007）
* FDA SQL データベースの使用時にアウトバウンドのターゲットを表示できなかった問題を修正しました。（NEO-8924）
* 月初の 7 日間に Microsoft の Dynamics CRM コネクタでデータをプルできない問題を修正しました。（NEO-8803）
* ユーザーが国際文字を含めることができない Analytics 統合に関するエラーを修正しました。（NEO-8719）
* 適切な権限がなくてもワークフロー編集が可能になる場合がある問題を修正しました。（NEO-8708）
* ハイブリッドアーキテクチャで Message Center を使用した場合に、HTTP 経由の FDA で接続が中断したり切断（タイムアウト）する問題を修正しました。（NEO-8438）
* 負の ID に対する増分処理クエリアクティビティで発生するワークフローエラーを修正しました。（NEO-8229）
* 特定の画面にスクロールバーが 2 本表示される場合がある問題を修正しました。（NEO-8208）
* 最新のデータベース構造ウィザードの実行時にエラーメッセージが表示される問題を修正しました。ポストアップグレードは、名前の長さが 30 を超えるインデックスの名前を変更します。大規模なテーブルでは、インデックスの置換に時間がかかることに注意してください。（NEO-7983）
* インスタンスを制御するための Message Center 実行インスタンスから適切な同期がおこなわれないログのトラッキングに関する問題を修正しました。（NEO-7286）
* オファーのエンリッチメントアクティビティに関するパフォーマンスの問題を修正しました。（NEO-7263）
* FDA によって Redshift データベースに対するクエリを実行したときに DaysAgo 関数を使用できなくなる問題を修正しました。（NEO-7099）
* エンリッチメントのようなワークフローアクティビティ上でインデックス作成ができなくなるデータ管理の回帰を修正しました。
* タイトル @id による外部リソースの作成時に発生する可能性がある問題を修正しました。
* zip 圧縮済みファイルを FTP サーバー経由でアップロードする場合や、ファイル名にワイルドカードを使用してファイルをアップロードする場合に発生する可能性がある問題を修正しました。
* Campaign 標準版内で作成された外部カスタムリソースでの長いベースタイプ列挙に関する問題を修正しました。
* プロバイダーとの接続が失敗して SMS が失われた場合でも SMS が送信される可能性がある問題を修正しました。
* SMTP 接続がいつまで経っても動作しなくなるエラーを修正しました。
* LINE マッピングを使用している場合に、またはフィルタリングスキーマとターゲティングスキーマが異なる場合に、メッセージの準備段階で発生していた頻度ルールの問題を修正しました。
