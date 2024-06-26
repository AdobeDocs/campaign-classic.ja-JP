---
product: campaign
title: 「[!DNL Gold Standard] リリース」
description: Campaign Classic に関するリリースノートおよび互換性マトリックス [!DNL Gold Standard]
feature: Release Notes
role: User
level: Beginner
hidefromtoc: true
hide: true
exl-id: 9e3a11b1-3070-4d90-91d5-7c559bdd500e
source-git-commit: 8de62db2499449fc9966b6464862748e2514a774
workflow-type: ht
source-wordcount: '1774'
ht-degree: 100%

---

# [!DNL Gold Standard] リリース{#gold-standard}



このページで、[!DNL Gold Standard] リリースのリリースノートと互換性マトリックスを確認できます。

## [!DNL Gold Standard] リリースノート


### [!DNL Gold Standard] 12 リリース{#gs-12}

[!BADGE 非推奨（廃止予定）]{type=negative url="https://experienceleague.adobe.com/docs/campaign-classic/using/release-notes/rn-overview.html?lang=ja#rn-statuses" tooltip="非推奨（廃止予定）"}

_2021 年 9 月 7 日_

ビルド 9032@554dbcd には、以下の修正が含まれています。

* トラッキングを有効にして LINE 配信で web アプリケーションへのリンクを開くと 500 エラーが発生する問題を修正しました。

_2021 年 8 月 27 日_

ビルド 9032@99a3894 には、以下の修正が含まれています。

* 署名トラッキング機能が改善され、サードパーティツール（メールクライアント、インターネットブラウザーなど）による特殊文字の処理方法に関連するエラーを防げるようになりました。URL パラメーターがエンコードされるようになりました。
* コンソールにブロッカーのエラーメッセージが表示される可能性がある日付選択の問題を修正しました。 （NEO-36345）

### [!DNL Gold Standard] 11 リリース{#gs-11}

[!BADGE 非推奨（廃止予定）]{type=negative url="https://experienceleague.adobe.com/docs/campaign-classic/using/release-notes/rn-overview.html?lang=ja#rn-statuses" tooltip="非推奨（廃止予定）"}

_2021 年 4 月 14 日_

ビルド 9032@d030c36 には、以下の修正が含まれています。

* IMS 接続画面で永続的なエラーメッセージが発生する原因となっていたクライアントコンソールの不具合を修正しました。 （NEO-34821）
* このコンソールビルドは、[IMS アクセス](../../technotes/using/ims-updates.md)を維持するために必要です。

**コンソールのアップグレードのみ必須です。サーバーのアップグレードは必要ありません。**

>[!CAUTION]
>
> * Adobe Identity Management サービス（IMS）を使用して Adobe ID で Campaign に接続する場合、**2021 年 6 月 30 日**（PT）以降も Campaign に接続できるようにするには、Campaign サーバーとクライアントコンソールの両方をアップグレードする必要があります。[詳細情報](../../technotes/using/ims-updates.md)
> * このリリースには、[セキュリティ修正](https://helpx.adobe.com/jp/security/products/campaign/apsb21-04.html)が含まれています。環境のセキュリティを強化するには、アップグレードが必要です。
> * OAuth 認証を通じた Experience Cloud トリガー統合を使用する場合は、[こちらのページ](../../integrations/using/about-triggers.md#implement)の説明に従って Adobe I/O に移行する必要があります。Campaign の従来の OAuth 認証モードは、[2021年9月](https://experienceleaguecommunities.adobe.com/t5/adobe-analytics-discussions/adobe-analytics-legacy-api-end-of-life-notice/td-p/385411?profile.language=ja)に&#x200B;**廃止されました**。ホスト環境では、**2022年2月23日（PT）**&#x200B;まで延長サポートを受けられます。オンプレミス環境またはハイブリッド環境のお客様は、アドビカスタマーケアに連絡してサポートを 2022年2月まで延長してください。[OAuth アプリケーションの AppID](../../integrations/using/configuring-pipeline.md#step-optional) をアドビに伝える必要があります。
>
>詳しくは、この[[!DNL Gold Standard] 節](../../rn/using/gold-standard.md)を参照してください。

_2021 年 3 月 2 日_

ビルド 9032@10c2709 には、以下の修正が含まれています。

* 配信での日付選択や画像管理など、コンソールの一部のコンポーネントを使用できないリグレッションを修正しました。 （NEO-31453、NEO-31454）

**コンソールのアップグレードのみ必須です。サーバーのアップグレードは必要ありません。**

>[!NOTE]
>
> [アドビのソフトウェア配布](https://experience.adobe.com/#/downloads/content/software-distribution/en/campaign.html)に接続して、新しいバージョンをダウンロードします。 [このページ](../../installation/using/client-console-availability-for-windows.md)では、すべてのエンドユーザーに対してコンソールの更新を提案する方法について説明します。

_2020 年 12 月 22 日_

ビルド 9032@d3b452f には、次の機能強化および修正が含まれています。

* 接続プロトコルは、新しい IMS 認証メカニズムに従うように更新されました。

* パイプラインにアクセスするために当初は oAUTH 認証設定に基づいていた Triggers 統合認証が変更され、Adobe I/O に移動しました。[詳細情報](../../integrations/using/about-triggers.md#implement)

* [iOS APN レガシーバイナリプロトコルのサポート終了](https://developer.apple.com/news/?id=c88acm2b)後は、このプロトコルを使用するすべてのインスタンスがアップグレード後に HTTP/2 プロトコルに更新されます。

* サーバーサイドリクエストフォージェリ（SSRF）問題に対する保護を強化するために、セキュリティ問題を修正しました。（NEO-27777）

* **エンリッチメント**&#x200B;アクティビティの実行時にワークフローが失敗する可能性がある問題を修正しました。（NEO-17338）

### [!DNL Gold Standard] 10 リリース{#gs-10}

[!BADGE 非推奨（廃止予定）]{type=negative url="https://experienceleague.adobe.com/docs/campaign-classic/using/release-notes/rn-overview.html?lang=ja#rn-statuses" tooltip="非推奨（廃止予定）"}

_2020 年 7 月 7 日_

ビルド 9032@efd8a94 には、以下の修正が含まれています。

署名機能が無効な場合にトラッキングが機能しない問題を修正しました。（NEO-26411）

>[!CAUTION]
>
>クライアントコンソールをこのリリースに含まれるものにアップグレードすることをお勧めします。[このページ](../../installation/using/installing-the-client-console.md)を参照してください。

### [!DNL Gold Standard] 9 リリース{#gs-9}

[!BADGE 非推奨（廃止予定）]{type=negative url="https://experienceleague.adobe.com/docs/campaign-classic/using/release-notes/rn-overview.html?lang=ja#rn-statuses" tooltip="非推奨（廃止予定）"}

_2020 年 6 月 22 日_

ビルド（9032@800be2e）には、以下の修正が含まれています。

* iOS HTTP2 コネクタが強化されました（サードパーティのアップデートおよびエラー管理）。（NEO-25904、NEO-25903、NEO-25799）

以下はトラッキングリンクのセキュリティメカニズムに関する修正です（詳しくは、[セキュリティとプライバシーのチェックリスト](https://helpx.adobe.com/jp/campaign/kb/acc-security.html#signature-mechanism)を参照してください）。

* 「通知クリック数」のトラッキングが機能しない問題を修正しました（iOS および Android のプッシュ通知）。（NEO-25965）
* 一部のレガシーバージョンの Outlook を使用する場合に、トラッキング URL を開いたりクリックしたりできない問題を修正しました。（NEO-25688）
* パーソナライゼーションパラメーター（シャープ記号の付いたアンカータグ）のフラグメントを使用した URL のトラッキングが機能しなかった問題を修正しました。（NEO-25774）
* フィッシング詐欺対策サービスの問題を修正しました。（NEO-25283）
* 特定のカスタムトラッキング式を使用する場合のトラッキングの問題を修正しました。（NEO-25277）

### [!DNL Gold Standard] 8 リリース{#gs-8}

[!BADGE 非推奨（廃止予定）]{type=negative url="https://experienceleague.adobe.com/docs/campaign-classic/using/release-notes/rn-overview.html?lang=ja#rn-statuses" tooltip="非推奨（廃止予定）"}

_2020 年 4 月 29 日_

ビルド（9032@3a9dc9c）には、以下の修正が含まれています。

* メール内のリンクの追跡に関するセキュリティを改善。これは、あらゆる顧客に対してデフォルトで有効です。さらに、強化されたセキュリティ機能が利用できます。この機能はカスタマーケアにご連絡いただくと有効にできます。これを非ホスト型顧客が有効にするための手順と機能の詳細については、[セキュリティおよびプライバシーチェックリスト](https://helpx.adobe.com/jp/campaign/kb/acc-security.html#signature-mechanism)を参照してください。

>[!CAUTION]
>
>トラッキングリンクを使用したプッシュ通知、またはアンカータグを使用した配信で問題が発生した場合は、トラッキングリンク用の新しい署名メカニズムを無効にすることをお勧めします。手順について詳しくは、[このページ](https://helpx.adobe.com/jp/campaign/kb/acc-security.html#signature-mechanism)を参照してください。

* LINE 配信に画像が表示されない可能性がある問題を修正しました。（NEO-23207）
* SFTP キーに基づく認証が Debian 9 で動作しない&#x200B;**ファイル転送**&#x200B;アクティビティの問題を修正しました。（NEO-23183）
* 高い頻度で送信されたときにプッシュ通知に影響を与える可能性がある問題を修正しました。（NEO-20516）
* Web サーバーのクラッシュを引き起こす可能性があるオファー応答管理の問題を修正しました。（NEO-19482）
* LibreOffice 管理で、レポートをエクスポートできなかったエラーを修正しました。（NEO-20982）
* 調査アクティビティを使用して多数のワークフローをアップグレードする場合にエラーが発生する問題を修正しました。
* .odt ファイルを含むメールプレビューでエラーが発生しないように、LibreOffice の管理を改善しました。
* Apache 接続の管理を改善し、Web サービスでの待ち時間を回避しました。
* **バージョン情報**&#x200B;メニューでのバージョンタグ（7 桁）の表示を改善しました。
* リスト管理でオファーが公開されない問題を修正しました。
* クリーンアップワークフローがクラッシュする原因となる問題を修正しました。
* クリーンアップワークフローログの軽度の問題を修正しました。

### [!DNL Gold Standard] 6 リリース{#gs-6}

[!BADGE 非推奨（廃止予定）]{type=negative url="https://experienceleague.adobe.com/docs/campaign-classic/using/release-notes/rn-overview.html?lang=ja#rn-statuses" tooltip="非推奨（廃止予定）"}

_2020 年 3 月 9 日_

ビルド（9032@19f73c5）には、以下の修正が含まれています。

* FTP over SSL を使用する外部アカウントの問題を修正しました。（NEO-20498）

### [!DNL Gold Standard] 5 リリース{#gs-5}

[!BADGE 非推奨（廃止予定）]{type=negative url="https://experienceleague.adobe.com/docs/campaign-classic/using/release-notes/rn-overview.html?lang=ja#rn-statuses" tooltip="非推奨（廃止予定）"}

_2019 年 12 月 17 日_

ビルド（9032@d6b8062）には、以下の修正が含まれています。

* モバイル（SMS、MMS）、プッシュ（iOS、Android）およびソーシャルネットワーク（Facebook、X - 旧 Twitter）の各通信チャネルでのトラッキングの問題を修正しました。（NEO-19595）

### [!DNL Gold Standard] 4 リリース{#gs-4}

[!BADGE 非推奨（廃止予定）]{type=negative url="https://experienceleague.adobe.com/docs/campaign-classic/using/release-notes/rn-overview.html?lang=ja#rn-statuses" tooltip="非推奨（廃止予定）"}

_2019 年 12 月 11 日_

ビルド（9032@bc4a935）には、以下の修正が含まれています。

* MSSQL データベースでメッセージを送信する際のパフォーマンスの問題を修正しました。（NEO-17558）

### [!DNL Gold Standard] 3 リリース{#gs-3}

[!BADGE 非推奨（廃止予定）]{type=negative url="https://experienceleague.adobe.com/docs/campaign-classic/using/release-notes/rn-overview.html?lang=ja#rn-statuses" tooltip="非推奨（廃止予定）"}

_2019 年 11 月 20 日_

ビルド（9032@3468c7b）には、以下の修正が含まれています。

* IMS 認証を使用したログインの問題を修正しました。（NEO-17312）
* 複数の配信に関する累積レポートを表示する際の問題を修正しました。（NEO-18165）
* Web サーバーがブロックまたはクラッシュする可能性がある問題を修正しました。

### [!DNL Gold Standard] 2 リリース{#gs-2}

[!BADGE 非推奨（廃止予定）]{type=negative url="https://experienceleague.adobe.com/docs/campaign-classic/using/release-notes/rn-overview.html?lang=ja#rn-statuses" tooltip="非推奨（廃止予定）"}

_2019 年 9 月 19 日_

ビルド（9032@cee805c）には、以下の修正が含まれています。

* Salesforce 用 CRM コネクタを使用する際の問題を修正しました。（NEO-17712）
* トランザクションメッセージの送信時にパフォーマンスの問題を引き起こす可能性があるインデックスの問題を修正しました。

### リリース 19.1.4 - ビルド 9032{#release-19-1-4-build-9032}

[!BADGE 非推奨（廃止予定）]{type=negative url="https://experienceleague.adobe.com/docs/campaign-classic/using/release-notes/rn-overview.html?lang=ja#rn-statuses" tooltip="非推奨（廃止予定）"}

_2019 年 8 月 13 日_

初期の 19.1.4 ビルドには以下の修正が含まれています。

* スケジューラーアクティビティで、ウィザード設定時に望ましくないエラーメッセージが生成される問題を修正しました。NEO-11662 から、更新を元に戻します。（NEO-17097）
* テストアクティビティが 2 回実行された際にワークフローが停止する、NEO-12727 が原因の回帰を修正しました。（NEO-16835）
* 無効な、または期限切れのセッショントークンが API 呼び出しで使用されると、間違った HTTP コード（HTTP 403 Forbidden ではなく HTTP 200 OK）が返される問題を修正しました。（NEO-16826）
* DKIM キーがメールに埋め込まれなくなった結果、配信品質が低下していた問題を修正しました。（NEO-16804）
* スケジューリングワークフローの様々な問題を修正しました。ワークフローは、スケジューラー設定を考慮することなく、1 日 1 回実行されるようにスケジュールされていました。（NEO-16619、NEO-16426）


## [!DNL Gold Standard] 互換性マトリックス{#compatibility-matrix-gs}

この節では、**Adobe Campaign Classic[!DNL Gold Standard]** のビルド 19.1 でサポートされているすべてのシステムとコンポーネントを示します。このリストに含まれていない製品とバージョンは、このバージョンの Adobe Campaign とは互換性がありません。

>[!CAUTION]
>特に明記されていない限り、マイナーリリースはすべてサポートされています。
>
>Adobe Campaign Classic は、このページに記載されているすべてのシステムおよびツールと互換性があります。これらのサードパーティ製システムおよびツールの特定のバージョンが、それぞれの作成者による提供が終了した（EOL）場合、Adobe Campaign はこれらのバージョンとの互換性を失います。これらは以降の製品リリースで互換表から削除されます。問題を回避するため、互換性マトリックスに記載されているシステムのサポート対象バージョンを使用していることを確認してください。
>

### オペレーティングシステム{#OperatingSystems-gs}

<table> 
<tbody> 
<tr> 
<td>CentOS</td>
<td>
<p>8.x（64 ビット）</p>
<p>7.x（64 ビット）</p>
</td>
</tr>
<tr>
<td>Debian</td>
<td>
<p>9（64 ビット）</p>
<p>8（64 ビット）</p>
</td>
</tr>
<tr>
<td>RHEL</td>
<td>
<p>7.x（64 ビット）</p>
<p><strong>重要</strong>：RHEL を使用する場合は、SELinux を無効にするか、アーキテクトにカスタム SELinux ルールを記述させ、有効にされた SELinux が Campaign 操作で問題を引き起こしていないことを確認する必要があります。</p>
</td>
</tr>
<tr>
<td>Windows Server</td>
<td>
<p>2016</p>
<p>2012 R2</p>
<p>2012</p>
</td>
</tr>
</tbody>
</table>

### web サーバー{#WebServers-gs}

<table>
<tbody>
<tr>
<td>Microsoft IIS</td>
<td>
<p>10.0（Windows Server 2016）</p>
<p>8.5（Windows Server 2012 R2）</p>
<p>8.0（Windows Server 2012 - Windows 8）</p>
</td>
</tr>
<tr>
<td>Apache</td>
<td>
<p>RHEL7 - CentOS 7、Debian 8/9、Windows（64 ビット）向けの 2.4</p>
<p>RHEL6 - CentOS 6（64 ビット）のみ向けの 2.2</p>
</td>
</tr>
</tbody>
</table>

### ツール{#Tools-gs}

<table>
<tbody>
<tr>
<td>Java Development Kit（JDK）</td>
<td>
<p>8</p>
<p>このアプリケーションは、Oracle が開発した Java Development Kit（JDK）および OpenJDK に対して承認されています。</p>
</td>
</tr>
<tr>
<td>Libre Office</td>
<td>
<p>6（お使いのシステムに埋め込まれている場合は以前のバージョン）</p>
</td>
</tr>
<tr>
<td>SpamAssassin</td>
<td>
<p>3.4.x</p>
</td>
</tr>
</tbody>
</table>

### RDBMS サーバー{#RDBMSservers-gs}

>[!NOTE]
>
>RDBMS ドライバーは RDBMS サーバーのバージョンと一致する必要があります。

<table>
<tbody>
<tr>
<td>Oracle</td>
<td>
<p>18c</p>
<p>12c</p>
<p>11g R2</p>
</td>
</tr>
<tr>
<td>PostgreSQL</td>
<td>
<p>11.x</p>
<p>10.x</p>
<p>9.6.x</p>
<p>9.5.x</p>
<p>9.4.x</p>
<p>注意：上記のバージョンで Amazon RDS for PostgreSQL を使用することもできます。</p>
</td>
</tr>
<tr>
<td>SQL Server</td>
<td>
<p>2019</p>
<p>2017</p>
<p>2016</p>
<p>2014</p>
<p>2012 - SP1 および SP2</p>
<p>警告：Linux で Campaign サーバーを実行している場合、Microsoft SQL Server はプライマリデータベースとしてサポートされません。</p>
</td>
</tr>
<tr>
<td>DB2 UDB</td>
<td>
<p>9.7</p>
<p>警告：DB2 UDB は新規インストールでは使用できません。</p>
</td>
</tr>
</tbody>
</table>

>[!NOTE]
>
>PostgreSQL は、ホスト環境のデフォルトのデータベースサーバーです。

### CRM コネクタ{#CRMconnectors-gs}

<table>
<tbody>
<tr>
<td>Salesforce コネクタ API</td>
<td>
<p>API バージョン 37</p>
</td>
</tr>
<tr>
<td>SFDC API</td>
<td>
<p>API バージョン 21</p>
<p>API バージョン 15</p>
</td>
</tr>
<tr>
<td>Microsoft Dynamics</td>
<td>
<p>SOAP API - オンプレミス：2007、2015、2016</p>
<p>SOAP API - オンライン：2015、2016</p>
<p>Web API - オンプレミスおよびオンライン：365、2016、2016 Update 1</p>
</td>
</tr>
</tbody>
</table>

### Federated Data Access（FDA）{#FederatedDataAccessFDA-gs}

<table>
<tbody>
<tr>
<td>Amazon Redshift</td>
<td><p> </p>
</td>
</tr>
<tr>
<td>Oracle</td>
<td>
<p>12c</p>
<p>11g</p>
</td>
</tr>
<tr>
<td>PostgreSQL</td>
<td>
<p>11.x</p>
<p>10.x</p>
<p>9.6.x</p>
<p>9.4.x</p>
</td>
</tr>
<tr><td>SQL Server</td>
<td>
<p>2019</p>
<p>2017</p>
<p>2016</p>
<p>2014</p>
<p>2012 SP1 および SP2</p>
</td>
</tr>
<tr><td>MySQL</td>
<td>
<p>5.7</p>
</td>
</tr>
<tr>
<td>Teradata</td>
<td>
<p>16.20</p>
<p>16</p>
<p>15.10</p>
<p>15.0</p>
</td>
</tr>
<tr>
<td>Netezza</td>
<td>
<p>7.2</p>
</td>
</tr>
<tr>
<td>Sybase</td>
<td>
<p>IQ 16</p>
<p>ASE 15.7</p>
</td>
</tr>
<tr>
<td>SAP HANA</td>
<td>
<p>バージョン 1 SPS 12</p>
</td>
</tr>
<tr><td>HiveSQL による Hadoop</td>
<td>
<p>HortonWorks HDP 2.4.x、2.5.x、2.6.x</p>
<p>HDInsight 3.4（HDP 2.4）、3.5（HDP 2.5）、3.6（HDP 2.6）</p>
</td>
</tr>
</tbody>
</table>

### クライアントコンソール {#ClientConsoleoperatingsystems}

`:warning:` Campaign クライアントコンソールを使用するには、次のオペレーティングシステムとブラウザーが必要です。

#### オペレーティングシステム

<table>
<tbody>
<tr>
<td>Microsoft Windows Server</td>
<td>
<p>2016</p>
<p>2012</p>
</td>
</tr>
<tr>
<td>Microsoft Windows</td>
<td>
<p>8</p>
<p>10（日本語インスタンスの場合に推奨）</p>
</td>
</tr>
</tbody>
</table>

#### ブラウザー

<table>
<tbody>
<tr>
<td>
<p>Microsoft Internet Explorer</p>
</td>
<td>
<p>11</p>
</td>
</tr>
</tbody>
</table>

### Mobile SDK{#MobileSDK}

<table>
<tbody>
<tr>
<td>Android</td>
<td>
<p>7.x、8.x、9.0</p>
<p>モバイル SDK ビルド 1.0.27 のサポート。</p>
</td>
</tr>
<tr>
<td>iOS</td>
<td>
<p>iOS 9 ～ 14</p>
<p>モバイル SDK ビルド 1.0.26 付き（32 ビットおよび 64 ビットバージョンと互換）</p>
</td>
</tr>
</tbody>
</table>

### ブラウザー{#Browsers}

次のブラウザーは Campaign for Web Access と互換性があります。

<table>
<tbody>
<tr>
<td>
<p>Microsoft Edge</p>
</td>
<td>
<p>最新バージョン</p>
</td>
</tr>
<tr>
<td>
<p>Mozilla Firefox</p>
</td>
<td>
<p>最新バージョン</p>
</td>
</tr>
<tr>
<td>
<p>Google Chrome</p>
</td>
<td>
<p>最新バージョン</p>
</td>
</tr>
<tr>
<td>
<p>Safari</p>
</td>
<td>
<p>最新バージョン</p>
</td>
</tr>
<tr>
<td>
<p>Microsoft Internet Explorer</p>
</td>
<td>
<p>11</p>
</td>
</tr>
</tbody>
</table>
