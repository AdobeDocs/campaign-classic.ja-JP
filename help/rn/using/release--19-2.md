---
product: campaign
title: リリース 19.2
description: Campaign 19.2 のリリースノート
exl-id: 3c529e4e-8787-41d2-b85d-3feaa5432196
source-git-commit: 32f55d02920b0104198f809b1be0a91306a4d9e4
workflow-type: tm+mt
source-wordcount: '1537'
ht-degree: 100%

---

# リリース 19.2{#release-19-2}

![](../../assets/v7-only.svg)

## ![](assets/do-not-localize/limited_2.png) リリース 19.2.4 - ビルド 9082 {#release-19-2-4-build-9082}

_2021 年 4 月 15 日_

* IMS 接続画面で永続的なエラーメッセージが発生する原因となっていたクライアントコンソールの不具合を修正しました。 （NEO-34821）

**コンソールのアップグレードのみ必須です。サーバーのアップグレードは必要ありません。**

>[!NOTE]
>
> [アドビのソフトウェア配布](https://experience.adobe.com/#/downloads/content/software-distribution/en/campaign.html)に接続して、新しいバージョンをダウンロードします。 [このページ](../../installation/using/client-console-availability-for-windows.md)では、すべてのエンドユーザーに対してコンソールの更新を提案する方法について説明します。

_2021 年 3 月 22 日_

* 配信での日付選択や画像管理など、コンソールの一部のコンポーネントを使用できないリグレッションを修正しました。 （NEO-31453、NEO-31454）

**コンソールのアップグレードのみ必須です。サーバーのアップグレードは必要ありません。**

>[!NOTE]
>
> [アドビのソフトウェア配布](https://experience.adobe.com/#/downloads/content/software-distribution/en/campaign.html)に接続して、新しいバージョンをダウンロードします。 [このページ](../../installation/using/client-console-availability-for-windows.md)では、すべてのエンドユーザーに対してコンソールの更新を提案する方法について説明します。

_2020 年 12 月 23 日_

>[!CAUTION]
>
> * このリリースには、新しい接続プロトコルが付属しています。Adobe ID サービス（IMS）を通じて Campaign に接続している場合、**2021 年 6 月 30 日（PT）**&#x200B;以降も Campaign サーバーとクライアントコンソールの両方が Campaign に接続できるようにするには、アップグレードする必要があります。[詳細情報](../../technotes/using/ims-updates.md)
>
> * このリリースには、[セキュリティ修正](https://helpx.adobe.com/jp/security/products/campaign/apsb21-04.html)が含まれています。環境のセキュリティを強化するには、アップグレードが必要です。



* 接続プロトコルは、新しい IMS 認証メカニズムに従うように更新されました。
* サーバーサイドリクエストフォージェリ（SSRF）問題に対する保護を強化するために、セキュリティ問題を修正しました。（NEO-27777）

## ![](assets/do-not-localize/red_2.png) リリース 19.2.3 - ビルド 9081 {#release-19-2-3-build-9081}

_2020 年 2 月 7 日_

**改善点**

* Windows サーバーでユーザーの接続が失敗する原因となった SSL 証明書の実装による新たな問題を修正しました。（NEO-20629）
* **バージョン情報**&#x200B;メニューに誤ったバージョンタグ番号が表示される問題を修正しました。

## ![](assets/do-not-localize/red_2.png) リリース 19.2 - ビルド 9080 {#release-19-2-build-9080}

_2019 年 12 月 2 日_

**新機能**

<table> 
 <thead> 
  <tr> 
   <th> <strong>カリフォルニア州消費者プライバシー法（CCPA）</strong><br /> </th> 
  </tr> 
 </thead> 
 <tbody> 
  <tr> 
   <td> <p>CCPA は、2020 年 1 月 1 日より米国カリフォルニア州にて新しく施行されるプライバシー保護法律で、データ保護要件を現代の状況に合わせて整合化させることを目的としています。CCPA は、カリフォルニア州に居住しているデータ主体のデータを保有している Adobe Campaign の顧客に適用されます。</p>
    <p> Adobe Campaign は、既に利用可能なプライバシー機能（同意管理、データ保持設定、ユーザー役割を含む）に加えて、CCPA への対応準備を容易にします。</p>
    <ul>
      <li>アクセス権と削除権：GDPR 用に追加された機能を活用します。<a href="https://helpx.adobe.com/jp/campaign/kb/acc-privacy.html#righttoaccess">詳細を表示</a></li>
      <li>顧客が個人情報の販売からオプトアウトしたかどうかを追跡できます。そのためには、プロファイルテーブルを拡張して「<strong>CCPA のオプトアウト</strong>」フィールドを追加する必要があります。<a href="https://helpx.adobe.com/jp/campaign/kb/acc-privacy.html#ccpa">詳細を表示</a></li></td> 
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
   <td> <p>事前定義されたビューを使用し、インスタンス上のすべてのワークフローの実行ステータスを監視できるようになりました。</p>
   <p>詳しくは、<a href="../../workflow/using/monitoring-workflow-execution.md#filtering-workflows-status">詳細ドキュメント</a>を参照してください。</p></td> 
  </tr> 
 </tbody> 
</table>


<table> 
 <thead> 
  <tr> 
   <th> <strong>AMP を使用したインタラクティブコンテンツ</strong><br /> </th> 
  </tr> 
 </thead> 
 <tbody> 
  <tr> 
<td> <p>Adobe Campaign では、新しいインタラクティブ <a href="https://amp.dev/about/email/">AMP for Email</a> フォーマットを試すことができます。このフォーマットでは、マーケターは、メッセージ内に AMP コンポーネントを含め、メッセージ内で直接アクション可能な、リッチで動的なインタラクティブコンテンツを使用して E メールエクスペリエンスを強化できます。</p>
   <p> この機能はパブリックベータ版としてリリースされています。</p>
   <p>詳しくは、<a href="../../delivery/using/defining-interactive-content.md">詳細ドキュメント</a>および<a href="https://experienceleague.adobe.com/docs/campaign-classic-learn/tutorials/sending-messages/email-channel/defining-interactive-email-content-with-amp.html?lang=ja">チュートリアルビデオ</a>を参照してください。</p><br /></td> 
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
<td> <p>拡張された汎用 SMPP コネクタでセキュア SMS がサポートされるようになりました。これにより、プロバイダーへの接続を暗号化できます。</p> <p><strong>警告</strong> この機能を使用するには、すべてのサーバーで最新の証明書が必要です。無効な証明書、失効した証明書または期限切れの証明書ではエラーが発生し、SMS 送信機能全体に影響を与えます。</p><p>詳しくは、<a href="https://helpx.adobe.com/jp/campaign/kb/sms-connector-protocol-and-settings.html">詳細ドキュメント</a>を参照してください。 </p> </td> 
  </tr> 
 </tbody> 
</table>

**セキュリティの機能強化**

* Campaign インターフェイスの格納型クロスサイトスクリプティングの脆弱性を修正しました（入力データ検証および出力エンコーディング）。（NEO-16810）
* ログイン制限ポリシーを強化して、権限のないデータへのアクセスを許可する可能性がある、プロファイル認証のセキュリティ問題を修正しました。（NEO-14445）

**改善点**

* プッシュ通知のメモリ消費の最適化。
* パフォーマンスとストレージを最適化するため、**logins.log** ファイルの処理が強化されました。このログファイルは複数のファイルに分割されるようになり、1 日に 1 つのファイルとなり、最大 365 個のファイルが保持されます。[詳細を表示](../../production/using/log-files.md)
* Microsoft Dynamics CRM 外部アカウントは、パスワード資格情報（パスワード + ユーザー名）または証明書（秘密鍵）を使用して設定できるようになりました。[詳細を表示](../../installation/using/external-accounts.md#microsoft-dynamics-crm-external-account)
* Hadoop FDA コネクタに強化機能がいくつか追加され、信頼性が向上しました。
* サーバー上の公開リソースのアップロードを許可する前にディスク領域を確認する、特別なガードレールが追加されました。
* 新しい[キャンペーンオプション](../../installation/using/configuring-campaign-options.md)が追加されました。
   * 「**WdbcKillSessionPolicy**」構成オプションを使用すると、すべてのワークフローと PostgreSQL データベースクエリに対して&#x200B;**無条件停止**&#x200B;の動作をさせることができます。
   * 「**NmsOperation_DeliveryPreparationWindow**」オプションを使用すると、ステータスの一貫しない配信が、実行中の配信の数から除外される日数を定義できます。
   * 「**WdbcOptions_TempDbName**」オプションを使用すると、Microsoft SQL Server 上で、作業用テーブル向けに別のデータベースを構成できます。これにより、バックアップとレプリケーションを最適化できます。[詳細を表示](../../production/using/rdbms-specific-recommendations.md#microsoft-sql-server)
   * PostgreSQL の「**XtkCleanup_NoStats**」オプションが強化され、データベースクリーンアップワークフローのストレージ最適化手順の動作をより適切に制御できるようになりました。[詳細を表示](../../production/using/database-cleanup-workflow.md#statistics-update)
* アカウントのロックアウトメカニズムが **logon()** API に追加されました。このメカニズムでは、特定の期間内に一定回数以上連続してログインに失敗すると、それ以降のログイン試行が阻止されます。
* 配信プロパティの新しいオプション「**最長パーソナライゼーション実行時間**」を使用すると、パーソナライゼーションの実行時間のタイムアウト期間を定義して、過度に長い間パーソナライゼーションフェーズが実行されないようにすることができます。[詳細を表示](../../delivery/using/personalization-fields.md#timing-out-personalization)
* 「**FTP プロトコル**」オプションが追加され、SFTP 接続でプロキシ設定を使用できるようになりました。[詳細を表示](../../installation/using/file-res-management.md)
* オンプレミス環境で、SFTP 外部サーバーへのプロキシアクセスを新しくサポートするようになりました。
* Campaign インスタンスと互換性のないパッケージのインストールを防ぐ、特別なガードレールが追加されました。[詳細を表示](../../installation/using/installing-campaign-standard-packages.md)

_非推奨（廃止予定）のシステム_

Campaign Classic 実装では、次のシステムが[非推奨（廃止予定）](deprecated-features.md)となりました。
* Apache 2.2
* Centos 6

最新の Campaign 互換性マトリックスに記載されているサポート対象バージョンのシステムを使用していることを確認してください。[詳細を表示](https://helpx.adobe.com/jp/campaign/kb/compatibility-matrix.html)

_Campaign モバイル SDK_

iOS SDK のビルド 1.0.26 が利用できるようになりました。この新しいビルドには、iOS 13 のサポートが追加されました。この新しいバージョンでは、通知の優先順位および iOS 13 プッシュ通知用の新しい登録トークン管理プロセスがサポートされるようになりました。以前のバージョンの SDK でアプリケーションを実行している場合は、新しい SDK でアプリケーションを再コンパイルする必要があります。SDK を入手するには、[アドビカスタマーケア](https://helpx.adobe.com/jp/enterprise/admin-guide.html/enterprise/using/support-for-experience-cloud.ug.html)にお問い合わせください。

**パッチ**

* **データ読み込み (RDBMS)** ワークフローアクティビティで、「**リンクされたテーブルを追加**」フィールドが空の場合に、クラッシュが発生する問題を修正しました。（NEO-12213）
* ミッドソーシングサーバーで特定のメッセージが処理されない可能性がある問題を修正しました。（NEO-12395）
* Teradata で query banding オプションを使用する際のデータベースクリーンアップワークフローの問題を修正しました。（NEO-12399）
* ne.jp ドメインを含むタイポロジルールを使用した配信分析に影響する問題を修正しました。（NEO-12609）
* より制限的な証明書ポリシーを必要とする TLS による SMS の更新に関連する問題を修正しました。これらの更新により、古い証明書が使用されている場合、マーケティングサーバーとミッドソーシングサーバー間の接続に失敗する可能性があります。（NEO-17698）
* Vault 認証を使用するミッドソーシング環境において、外部アカウントの「**接続をテスト**」ボタンを使用する際の問題を修正しました。（NEO-12722）
* FDA Hadoop 接続で日付関数を使用するクエリの問題を修正しました。（NEO-12847）
* E メールエディターで画像を置き換える際の問題を修正しました。（NEO-13098）
* 削除されたか別の場所に移動されたフォルダーにおいて、アップグレード後にエラーが発生することのある問題を修正しました。（NEO-13118）
* LINE メッセージで「**デバイスの画面サイズごとに画像を定義**」オプションを使用する際の、画像の表示に関する問題を修正しました。（NEO-13228）
* 「**配信中に重複アドレスを除外**」オプションが選択されていない場合の配信準備の問題を修正しました。（NEO-13240）
* ワークフローで&#x200B;**ファイル転送**&#x200B;アクティビティを使用し、「**転送後にソースファイルを削除**」オプションを使って名前にスペース文字が含まれるファイルをダウンロードする際に発生した問題を修正しました。（NEO-13411）
* Tomcat キャッシュのクリーンアップでメモリの問題が発生する問題を修正しました。（NEO-13456）
* Microsoft SQL 2017 で稼動している既存のコントロールインスタンスに、**実行インスタンスによるオファーエンジンのコントロール**&#x200B;組み込みパッケージをインストールする際の問題を修正しました。（NEO-13539）
* 初期化されていない変数が原因で、「**テキストコンテンツ**」タブから E メール内のトラッキングされる URL をチェック解除すると、コンソールクラッシュが発生する可能性がある問題を修正しました。（NEO-13545）
* 中国語の送信者名のエンコードの問題を修正しました。（NEO-13837）
* エクスプローラーからの調査回答データを表示すると発生することのあるエラーを修正しました。（NEO-14590）
* 配信ログの分類と強制隔離テーブルの間で不一致が生じる可能性がある問題を修正しました。（NEO-16547）
* E メールに埋め込まれなかった DKIM キーの問題を修正しました。（NEO-16804）
* イベントをトリガーするために API 呼び出しのコンテキストで無効なセッショントークンが使用された際、誤ったエラーコードが表示された問題を修正しました。エラーコードが「HTTP 403 Forbidden」ではなく「HTTP 200 OK」でした。（NEO-16826）
* web アクセスを介して配信レポートを表示する際の問題を修正しました。（NEO-17015）
* Adobe Campaign にログインする際の IMS 認証の問題を修正しました。（NEO-17312）
* プライバシー管理プロセスで強制隔離済みの E メールを削除できなかった問題を修正しました。（NEO-17314）
* SQL データベースで 9031 にアップグレードした後のスループットの問題を修正しました。（NEO-17558）
* Salesforce の CRM コネクタに影響を及ぼしていた問題を修正しました。（NEO-17712）
* 外部 SFTP からデータをインポートする際のタイムアウトの問題を修正しました。（NEO-19723）
* 予測モデルにアクセスする際の問題を修正しました。（NEO-19713）
* Hadoop FDA データベースを使用した&#x200B;**分割**&#x200B;ワークフローアクティビティでのランダムサンプリングに影響する問題を修正しました。（NEO-16636）
* ポストアップグレード後に一部の関数が無効と見なされる、Oracle の問題を修正しました。（NEO-12759）
