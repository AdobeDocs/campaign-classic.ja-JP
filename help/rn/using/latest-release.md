---
title: 最新リリース
description: 最新の Campaign Classic リリース注意
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
ht-degree: 100%

---


# 最新リリース{#latest-release}

このページには、**最新の Campaign Classic リリース候補バージョン**&#x200B;に加えられた新機能、改善点、および修正点が記載されています。

Campaign Classic Gold Standard バージョン（最新の GA ビルド）については、[このページを参照してください](../../rn/using/gold-standard.md)。

## ![](assets/do-not-localize/blue_2.png) リリース 20.3.1 - ビルド 9228 {#release-20-3-1-build-9228}

_2020 年 10 月 27 日_

**新機能**

<table> 
<thead>
<tr> 
<th> <strong>iOS のプッシュ通知の改善点</strong><br /> </th> 
</tr> 
</thead> 
<tbody> 
<tr> 
<td> <p>モバイルアプリを Campaign と統合する場合は、Apple Push Notification service（APNs）との通信をセキュリティで保護する必要があります。証明書ベースまたはトークンベースの認証を使用できます。
</p>
<p>Campaign Classic では次の 2 つの認証モードが iOS モバイルアプリで使用できるようになりました。
</p>
<ul> 
<li><p>トークンベースの認証（推奨）：この認証モードは .p8 ファイルに基づいています。この認証モードは、APNs への各リクエストにトークンが含まれるのでより高速です。<a href="https://developer.apple.com/documentation/usernotifications/setting_up_a_remote_notification_server/establishing_a_token-based_connection_to_apns">詳細情報</a></p></li>
<li><p>証明書ベースの認証：この認証モードは .p12 ファイルに基づいています。各アプリに対して別々の証明書が必要です。この証明書は、Apple によって開発者アカウント経由で配信されます。<a href="https://developer.apple.com/documentation/usernotifications/setting_up_a_remote_notification_server/establishing_a_certificate-based_connection_to_apns">詳細情報</a></p></li> 
</ul>
<p>Campaign で認証モードを選択する方法については、この<a href="../../delivery/using/configuring-the-mobile-application.md">詳細なドキュメント</a>を参照してください。</p>
</td> 
</tr> 
</tbody> 
</table>

<table> 
<thead>
<tr> 
<th> <strong>Android のプッシュ通知の改善点</strong><br /> </th> 
</tr> 
</thead> 
<tbody> 
<tr> 
<td> <p>Android のプッシュ通知が改善され、Android のプッシュチャネル認証用の FCM HTTP v1 API がサポートされるようになりました。 </p>
<p>サポートされる新しい API バージョンでは、強化されたリッチなプッシュメッセージ機能を備えた FCM 通知メッセージを送信できるようになりました。<a href="https://firebase.google.com/docs/cloud-messaging/migrate-v1">詳細情報</a></p> 
<p>Adobe Campaign で Android 用の FCM HTTP v1 API 設定する方法については、<a href="../../delivery/using/configuring-the-mobile-application-android.md">この節</a>を参照してください。</p>
</td> 
</tr> 
</tbody> 
</table>

**セキュリティの機能強化**

* ライブラリの安全な読み込み：Campaign では、DLL プリロード攻撃から保護するために、Campaign クライアント（nlclient）の読み込み中に Windows のデフォルトのシステム DLL パスからのみ Windows DLL を読み込むようになりました。[詳細情報](https://support.microsoft.com/ja-jp/help/2389418/secure-loading-of-libraries-to-prevent-dll-preloading-attacks)（NEO-24147）
* サーバーサイドリクエストフォージェリ（SSRF）攻撃に対する保護を強化するために、セキュリティ問題を修正しました。（NEO-25661）
* GDPR プライバシーリクエストを処理する際に発生していた問題を修正しました。この問題は、受信者テーブルとのセカンドレベル関係を持つカスタムテーブルからレコードを削除できなくしていました。（NEO-25967）
* 管理者以外のユーザーが Adobe Experience Manager テンプレートの同期を試みるときに実行する API 呼び出しの使用に関するセキュリティ問題を修正しました。（NEO-23487）

**互換性の更新**

Campaign で次のシステムがサポートされるようになりました。
* iOS 14
* PostgreSQL 12
* CentOS / RedHat 8
* MSSQL2019

詳しくは、[Campaign 互換性マトリックス](../../rn/using/compatibility-matrix.md)を参照してください。

**非推奨（廃止予定）の機能**

20.3 では、次の機能が非推奨（廃止予定）になります。

* Adobe Experience Cloud へのオーディエンスのインポートおよびエクスポートに使用する demdex ドメインは非推奨（廃止予定）になります。インポート/エクスポート外部アカウントに demdex ドメインを使用している場合は、それに応じて実装を適応させる必要があります。[詳細情報](../../integrations/using/configuring-shared-audiences-integration-in-adobe-campaign.md)
* パイプラインにアクセスするために当初は oAUTH 認証設定に基づいていたトリガー統合認証が変更され、Adobe I/O に移動しました。[詳細情報](../../integrations/using/configuring-adobe-io.md)

詳しくは、[非推奨（廃止予定）の機能と削除された機能のページ](../../rn/using/deprecated-features.md)を参照してください。

**改善点**

* **クライアントコンソール**&#x200B;には、次の改善点が追加されました。
   * インターネットセキュリティ GPO ルールの一部の制限との非互換性を防ぐため、Campaign クライアントコンソールのログオン画面は組み込みの標準 Windows フォームに置き換えられました。
   * 64 ビットのクライアントコンソールを使用したワークフローで、アクティビティのコピー/貼り付けを行うときの問題を修正しました。（NEO-27635）
   * **バージョン情報**&#x200B;メニューに、64 ビットと 32 ビットのコンソールを区別するための情報が追加されました。
* ワークフローを再開すると、ワークフロー識別子がログに表示されるようになりました。これにより、再開されたワークフローの識別が簡単になりました。
* 新しい永続的な cookie である nllastdelid が導入されました。この cookie（UUID230 以外）は、deliveryId を格納します。セッション cookie が存在しない場合、broadlog 情報は、この cookie に存在する deliveryId から取得されます。
この変更により、ブラウザーセッションの終了時に deliveryId と broadlogId を含むセッション cookie が削除されて発生する問題が修正されました。deliveryId がないと、broadlog 情報が見つからず、永続的なトラッキング（最後の配信）の場合にトラッキングテーブル情報が欠落します。
Cookie について詳しくは、[この節](../../platform/using/privacy-and-recommendations.md#cookies)を参照してください。
* 配信の送信の前に MTA プロセスを再起動することにより、配信品質サーバーでの高ボリューム配信スループットパフォーマンスを改善しました。

**その他の変更**

* SFTP に相対パスを使用するときに、`~/` 文字が自動的に追加されなくなりました。必要に応じて、パスに `~/` 文字を手動で追加できますが、**絶対パス**&#x200B;を使用することをお勧めします。
* Microsoft SQL Server で新しいデータベースを設定する際の使用可能な認証方法から Windows NT 認証が削除されました。[詳細を表示](../../installation/using/creating-and-configuring-the-database.md#step-1---selecting-the-database-engine)
* パフォーマンスを向上させるために、データベースのクリーンアップワークフローが Teradata 用に最適化されました。（NEO-19959）
* Adobe Target から画像を挿入するときに、外部アカウントでテナント名が空だった場合に表示されるエラーメッセージを改善しました。
* 配信プロパティで、「**[!UICONTROL E メールをアーカイブ]**」オプションが「**[!UICONTROL BCC で E メールを送信]**」に名前変更されました。
* 堅牢性を向上するために、無効なノードでの selectAll クエリは拒否されるようになりました。チェックを無効にして前の動作に戻る必要がある場合は、XtkSecurity_Disable_QueryCheck を 0 に設定します。

**技術面の変更点**

Tomcat は、バージョン 7（7.0.103）からバージョン 8（8.5.57）に更新されました。

`tomcat-7` ディレクトリは、`tomcat-8` ディレクトリに置き換えられています。

Windows では、_iis_neolane_setup.vbs_ と _apache_neolane.conf_ が（以前の `tomcat-7/conf` ではなく） `conf` ディレクトリにインストールされるようになりました。

Linux では、_apache_neolane.conf_ が `conf` ディレクトリにインストールされるようになりました。

**パッチ**

* 配信統計を再計算できない原因となる場合がある問題を修正しました。
* 古いビルドを使用しているサーバーに接続された Campaign Classic 9080 ビルドを使用して CSV ファイルをアップロードするとエラーメッセージが表示される問題を修正しました。（NEO-23218）
* 外部アカウント用に Microsoft Dynamics CRM ウィザードを設定する際にエラーメッセージが表示される場合がある問題を修正しました。この問題は、最新の MS Dynamics CRM API バージョンとの互換性が原因でした。（NEO-24528）
* CRM コネクタを使用して参照タイプレコード（つまり、他のテーブルに接続された外部キーレコードから成るデータ）を Campaign Classic から Microsoft Dynamics にエクスポートできない問題を修正しました。（NEO-23864）
* CRM コネクタで「**自動インデックス**」オプションが有効になっている場合に、Microsoft Dynamics データを取得できない ことがある問題を修正しました。（NEO-25981）
* 接続を終了した場合でも接続が開いたままになる IMS 認証の問題を修正しました。接続の蓄積やシステムリソースの消費を避けるために、切断した接続は、終了と同時に自動的に閉じられるようになりました。（NEO-25996）
* 外部アカウントの設定が誤っている（アカウントまたはパスワードが正しくない）ために、配信する Adobe Experience Manager コンテンツの同期に失敗した場合にエラーメッセージが表示されない問題を修正しました。失敗した場合にメッセージが表示され、問題をより簡単に識別できるようになりました。（NEO-25586）
* 「**データを更新**」アクティビティで「**更新**」操作タイプを選択すると発生していた問題を修正しました。更新するデータが正しくない場合、ワークフローにエラーが発生し、失敗していました。データが正しくない場合、ワークフローは失敗せず、レコードは「**却下**」アウトバウンドトランジションに保存されるようになりました。（NEO-23794）
* サブワークフローを含むワークフローが機能しない原因となることがある問題を修正しました。（NEO-24036）
* キャンペーンテンプレートの説明を編集する際に、日本語文字などの記号のコピー/貼り付けを行うと「**保存**」ボタンが表示されない問題を修正しました。（NEO-27071）
* インスタンス設定ウィザードでトラッキングサーバーを変更できない原因となることのある問題を修正しました。
* 「**保存**」ボタンをクリックする前にウィンドウの外側をクリックした場合に、キャンペーンまたはキャンペーンテンプレートの説明が保存されない問題を修正しました。（NEO-27449）
* 「**アクティブなプロファイルの数（請求）**」（billingActiveContactCount）テクニカルワークフローが機能しないことがある問題を修正しました。この問題は、スキーマ拡張の計算されたフィールドに対してリンクが実行された場合に発生する可能性がありました。大量のデータが作成され、データベースの一時的な領域が不足する場合がありました。（NEO-24062）
* 日本語文字が txt ファイルや csv ファイルの末尾に配置されている場合、日本語文字がインポートできないことがある「**データ読み込み（ファイル）**」アクティビティの問題を修正しました。（NEO-24957）
* 「**分析開始日**」フィールドと「**分析終了日**」フィールドが正しく入力されない連続配信の問題を修正しました。（NEO-20755）
* 「**受信者**」（nms:recipient）以外のスキーマでクエリを行った後、SMS メッセージをプレビューしようとするとエラーメッセージが表示される場合がある問題を修正しました。（NEO-27517）
* Snowflake FDA コネクタを使用する際の問題を修正しました。Snowflake FDA のアクセス名の権限を持つユーザーは、Snowflake スキーマでクエリを実行できませんでした。ログに「パスワードが見つかりません」というタイプのエラーが表示されていました。（NEO-23851）
* リンクされた FDA スキーマ名が現在のスキーマの要素名のサブ文字列である場合に発生する、FDA コネクタを使用する際の問題を修正しました。この問題は、例えば、FDA スキーマが「cust」で、受信者スキーマ内の要素の 1 つが「customer」である場合に発生していました。「customer」要素内の列を取得し、「cust」FDA スキーマから列を追加するときに、ローカルの列の値が欠落していました。（NEO-20193）
* 外部データベースからレコードを取得し、Campaign データベースに挿入する際のワークフローの問題を修正しました。（NEO-26359）
* 「**イベントステータスを更新**」テクニカルワークフローの問題を修正しました。「**配信統計**」アクティビティの対応する受信フィールドのサイズを一致させるために、「**配信の統計値を更新**」アクティビティの 3 つの宛先フィールドのサイズを 32 ビットから 64 ビットに変更しました。（NEO-11557）「**イベントステータスを更新**」ワークフローについて詳しくは、[この節](../../workflow/using/message-center--execution-.md)を参照してください。
* フィルターを適用しようとするとスクリプトにエラーが発生し、日付範囲でフィルターできない「**Message Center のイベント履歴**」の問題を修正しました。（NEO-23365）
* 「**キャンペーンのジョブ**」（operationMgt）テクニカルワークフローと「**プレビュー**」（forecasting）テクニカルワークフローの間の干渉の問題を修正しました。この問題は、スケジュール済みの配信が「ターゲット準備完了」ステータスまたは「配信準備完了」ステータスのままの場合に発生していました。（NEO-20819）
* xtkOperator の mdata フィールドに XML 識別子が存在しない場合の XML 解析の問題を修正しました。この問題は、アップグレード後のエラーを引き起こしていました。（NEO-26113）
* 接続確立に HTTPS ではなく HTTP を使用して SSL で暗号化された Azure 外部アカウントにリンクされている「**ファイル転送**」アクティビティを使用する際の問題を修正しました。（NEO-26720）
* クリーンアップワークフロー中に up_updatestats プロシージャでエラーが発生する可能性がある MSSQL データベースの問題を修正しました。
* インタラクションリクエストがまだ処理中の場合、Web プロセスのシャットダウン中に発生するクラッシュを修正しました。（NEO-26447）
* 9032 にアップグレードした後、Oracle データベースの **NoNull** 関数が機能しなくなる問題を修正しました。（NEO-26488）
* Message Center パッケージなしで、LINEV2 パッケージがインストールされた場合、9171 にアップグレードした後、トラッキングワークフローが失敗する問題を修正しました。
* 属性「APP」のデータベース接続文字列が最終的に無効な値を取得するため、接続プールを必要な接続数まで増やせなかったスケーラビリティの問題を修正しました。（NEO-25105）
* Windows 10 の最新の更新後に Adobe Campaign にログインできなくなるプロキシ設定レベルの問題を修正しました。（NEO-27813）
* トラッキングリンクを含む HTML テンプレートをインポートした後、配信された E メールに不要な URL が表示される問題を修正しました。（NEO-25909）
* ワークフローの「**分割**」アクティビティの残りのターゲットデータを表示すると、サーバーがクラッシュする原因となった問題を修正しました。
* 式パーサーをクリーニングする際にメモリの破損を防ぐことで、サーバーのクラッシュの問題を修正しました。（NEO-26856）
* 管理者以外のユーザーがインスタンス変数を定義しているエンリッチメントアクティビティの問題を修正しました。（NEO-25653）