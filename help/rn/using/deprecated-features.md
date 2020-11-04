---
title: Campaign Classic の非推奨（廃止予定）および削除された機能
description: このページリストは、Adobe Campaign Classic の非推奨（廃止予定）および削除された機能です
page-status-flag: never-activated
contentOwner: simonetn
products: SG_CAMPAIGN/CLASSIC
audience: rn
content-type: reference
topic-tags: campaign-classic-deprecated-features
internal: n
snippet: y
translation-type: tm+mt
source-git-commit: 281eb6b0f84e01d25ac9c3542dc2ee950d4879e7
workflow-type: tm+mt
source-wordcount: '1621'
ht-degree: 85%

---


# 非推奨（廃止予定）および削除された機能 {#deprecated-and-removed-features}

アドビは、製品の機能を評価し続けて、より新しい代替手段に置き換えるべき旧機能を特定し、全体的な顧客の価値を向上させ、常に後方互換性を慎重に考慮します。Adobe Campaign Classic はサードパーティ製ツールと連携しており、サポート対象バージョンのみに対応するために、定期的に互換性が更新されています。Adobe Campaign Classic と互換性がなくなったバージョンを、以下および[互換性マトリックス](../../rn/using/compatibility-matrix.md)に示します。

Campaign Classic 機能の差し迫った削除／置換を伝達するため、次の規則が適用されます。

* まず、廃止予定のお知らせが来ます。非推奨（廃止予定）の機能は引き続き既存のユーザーに提供できサポートされますが、それ以上の機能強化やドキュメント化はおこなわれません。
* 非推奨（廃止予定）の機能は、以下のリリースで最も早く削除されます。削除の実際のターゲット日は、このページで発表されます。

このプロセスにより、顧客は、実際に削除する前に、新しいバージョンや非推奨（廃止予定）の機能の後継バージョンに実装を適応させるために、少なくとも 1 つのリリースサイクルを提供できます。

>[!NOTE]
>Adobe Campaign リリースと新機能は、[リリースノート](../../rn/using/latest-release.md)に一覧表示されています。

## 非推奨（廃止予定）の機能 {#deprecated-features}

この節では、最新の Campaign Classic リリースで非推奨とマークされている機能を一覧化します。

一般に、将来のリリースで削除される予定の機能は、まず非推奨に設定されます。これらの機能は、新しい Campaign Classic の顧客は利用できなくなるか、新しい実装には使用するべきではないものです。また、製品ドキュメントからも削除されます。

顧客は現在のデプロイメントで機能を利用しているかどうかを確認し、実装を変更する計画を立てるようお勧めします。削除の目標期日を参照し、それに応じて環境やプロジェクトの更新を計画してください。

<table> 
 <tbody> 
   <tr>
   <td><strong>機能</strong></td>
   <td><strong>置き換え</strong></td>
  </tr>
  <tr>
  <td>CRM コネクタ<br></td>
   <td><p>キャンペーン20.3リリース以降、次のCRMコネクタは非推奨となりました。</p>
   <ul>
   <li>SOAP API - オンプレミス：2007、2015、2016</li>
   <li>SOAP API - オンライン：2015、2016</li>
   <li>Web API - Microsoft Dynamics CRMオンプレミス：2016, 2016 Update 1</li>
   <li>Web API - Microsoft Dynamics CRM Online:2016, 2016 Update 1</li>
   </ul>
  <p><em>削除予定日：2021 年</em></p>
  </td>
 </tr>
  <tr>
  <td>iOSレガシーバイナリ<br></td>
  <td><p>キャンペーン20.3リリース以降、iOSレガシバイナリコネクタは非推奨となりました。<p>
  <p> このコネクタを使用する場合は、それに応じて実装を適応させる必要があります。
  <a href="https://helpx.adobe.com/campaign/kb/migrate-to-http2.html">詳細情報</a></p>
  <p><em>削除予定日：2021 年</em></p>
  </td>
 </tr>
   <tr>
  <td>Demdexドメイン<br></td>
  <td><p> キャンペーン20.3リリース以降、オーディエンスのAdobe Experience Cloudへの読み込みと書き出しに使用するdemdexドメインは廃止されました。<p>
  <p>インポート/エクスポート外部アカウントにdemdexドメインを使用する場合は、それに応じて実装を適応させる必要があります。 <a href="../../integrations/using/configuring-shared-audiences-integration-in-adobe-campaign.md">詳細情報</a></p> 
  <p><em>削除予定日：2021 年</em></p>
  </td>
  <tr>
  <td>OAuth認証（OAuthおよびJWT）<br></td>
  <td><p> キャンペーン20.3リリース以降、元々はoAUTH認証設定に基づいて統合認証をトリガーし、パイプラインにアクセスするための設定が変更され、AdobeI/Oに移行しました。 <p>
  <p>Triggers統合を使用している場合は、それに応じて実装を適応させる必要があります。 <a href="../../integrations/using/about-triggers.md">詳細情報</a></p> 
  <p>OAuth Authenticationの減価償却の詳細については、この <a href="https://github.com/AdobeDocs/analytics-1.4-apis/blob/master/docs/APIEOL.md">ページを参照してください。</a></p> 
  <p><em>ターゲットの削除日：2021年4月</em></p>
  </td>
  </tr>
  <td>SMS コネクタ<br></td>
  <td><p> Campaign 20.2 リリースより、次の SMS コネクタは非推奨（廃止予定）になります。<p>
   <ul>
   <li>NetSize</li>
   <li>一般的な SMPP（バイナリモードをサポートする SMPP バージョン 3.4）</li>
   <li>Sybase365（SAP SMS 365）</li>
   <li>CLX Communications</li>
   <li>Tele2</li>
   <li>O2</li>
   <li>iOS</li>
   </ul>
  <p>これらのコネクタのいずれかを使用する場合は、それに応じて実装を適応させる必要があります。<a href="../../delivery/using/sms-channel.md">詳細情報</a>。</p> 
  <p>従来のコネクタを移行する方法については、この<a href="https://helpx.adobe.com/jp/campaign/kb/sms-connector.html">テクニカルノート</a>を参照してください。</p>
  <p><em>削除予定日：2021 年</em></p>
  </td> 
 </tr>
  <tr>  
   <td>FAX チャネル<br></td>
   <td><p>Campaign 20.2 リリースより、FAX チャネルは非推奨（廃止予定）になります。</p> 
   <p>このチャネルを使用する場合は、それに応じて実装を適応させる必要があります。Campaign チャネルの<a href="../../delivery/using/steps-about-delivery-creation-steps.md">詳細情報</a>を参照してください。</p>
   <p><em>削除予定日：2021 年</em></p></td>
  </tr>
 </tbody> 
</table>

## 削除された機能 {#removed-features}

この節には、Campaign Standard から削除された機能が記載されています。

<table> 
 <tbody> 
  <tr> 
   <td><strong>領域 - 機能</strong></td>
   <td><strong>置き換え</strong></td> 
  </tr> 
   <tr> 
   <td>Windows NT認証<br></td>
   <td><p>キャンペーン20.3リリースから、Microsoft SQL Serverで新しいデータベースを構成する際に、Windows NT認証が利用可能な認証方法から削除されました。 <a href="../../installation/using/creating-and-configuring-the-database.md#step-1---selecting-the-database-engine">詳細情報</a></p></td>
  </tr>
   <tr> 
   <td>ファイルベースの E メールのアーカイブ<br></td>
   <td><p>Campaign 20.2 リリースより、ファイルベースの E メールのアーカイブは使用できなくなりました。E メールアーカイブは、専用の BCC E メールアドレスを通じて使用できるようになりました。<a href="../../installation/using/email-archiving.md">詳細情報</a></p></td>
  </tr> 
   <tr> 
   <td>リード管理</td>
   <td><p>Campaign 20.2 リリースより、リード管理パッケージは使用できなくなりました。他のネイティブワークフローアクティビティやデータモデルの変更を介しても、同様の機能を実装できます。</p></td>
   </tr>
   <tr>
   <td>Campaign API ドキュメント - jsapi.chm ファイル</td>
   <td>Campaign 19.1 リリースより、Campaign Classic API は専用ページで利用できます。従来の jsapi.chm ファイルを使用していた場合は、<a href="https://docs.adobe.com/content/help/en/campaign-classic/technicalresources/api/index.html">新しいオンラインバージョン</a>を参照する必要があります。</td>
  </tr> 
  <tr> 
   <td>キャンペーンオーケストレーション - 予測マーケティング</td>
   <td>Campaign 18.10 リリースより、予測マーケティング機能は使用できなくなりました。</td>
  </tr> 
  <tr> 
   <td>Web アプリケーション - マイクロサイト</td>
   <td>Campaign 18.10 リリースより、マイクロサイトは使用できなくなりました。Adobe Campaign 構成ファイルの専用ドメインのみにアクセスを制限することでセキュリティを向上させ、DNS エイリアスを使用して Campaign でパーソナライズされた URL を使用することができます。<a href="https://helpx.adobe.com/jp/campaign/kb/domain-name-delegation.html">詳細情報</a>。</td>
  </tr> 
  <tr> 
   <td>プッシュ通知 - iOS バイナリコネクタ</td>
   <td>Campaign 18.10 リリースより、Apple の推奨に従って、従来の iOS バイナリコネクタを削除しました。HTTP/2 ベースのコネクタは、より高機能でより効率的です。</td>
  </tr> 
  <tr> 
   <td>decryptString API</td>
   <td><p>Campaign 18.6 リリースより、セキュリティ上の理由から、<em>decryptString</em> API は、新しいインストールではデフォルトで使用できなくなりました。</p> 
   <p>18.6（以降）へのアップグレード後、この API は有効化されなくなり、<em>decryptPassword</em> 関数に置き換えられます。<a href="https://docs.adobe.com/content/help/en/campaign-classic/technicalresources/api/f-decryptPassword.html?hl=decrypt">詳細情報</a></p></td>
  </tr> 
   <tr> 
   <td>モバイルチャネル- MMS および WAP プッシュメッセージ</td>
   <td>Campaign 18.4 リリースより、MMS と WAP プッシュのチャネルは使用できなくなりました。代わりに、<a href="../../delivery/using/sms-channel.md">SMS</a> および<a href="../../delivery/using/about-mobile-app-channel.md">プッシュ</a>配信を利用できます。</td>
  </tr> 
   <tr> 
   <td>モバイルチャネル - LINE v1</td>
   <td>Campaign 18.4 リリースより、LINE Connect パッケージは使用できなくなりました。代わりに、新しい LINE Channel パッケージを使用することをお勧めします。<a href="../../delivery/using/line-channel.md">詳細情報</a></td>
  </tr> 
 </tbody> 
</table>

## 非推奨（廃止予定）の互換性 {#deprecated-compatibility}

Campaign Classic では、次のシステムが非推奨（廃止予定）になっています。[互換性マトリックス](../../rn/using/compatibility-matrix.md)を参照し、互換性がなくなる前に、新しいバージョンにアップグレードするか、新しいシステムに移行してください。

### Adobe Campaign 20.2 リリース {#compat-20-2-release}

20.2リリース以降、レガシーSMSコネクタは非推奨となります。 非 [推奨機能の節を参照してください](#deprecated-features)

## 互換性の終了 {#end-of-compatibility}

>[!CAUTION]
>
>Adobe Campaign Classic は、[互換性マトリックス](../../rn/using/compatibility-matrix.md)に記載されているすべてのシステムおよびツールと互換性があります。これらのサードパーティ製システムおよびツールの特定のバージョンが、それぞれの作成者による提供が終了した（EOL）場合、Adobe Campaign はこれらのバージョンとの互換性を失います。これらは非推奨と発表された後、以降の製品リリースで互換表から削除されます。問題を回避するため、互換性マトリックスに記載されているシステムのサポート対象バージョンを使用していることを確認してください。

### クライアントコンソール {#client-console-eol}

Adobe Campaign Classic クライアントコンソールは、次のシステムでは実行できなくなりました。エディターで非推奨になっています。Campaign クライアントコンソールをこれらのバージョンのいずれかで実行している場合は、削除のターゲット日より前に最新バージョンにアップグレードする必要があります。[互換性マトリックス](../../rn/using/compatibility-matrix.md)を参照してください。

* Windows Server 2003、2008、2008 R2
* Windows 7、XP、Vista

>[!NOTE]
>Campaign 20.1 リリースより、Campaign Classic クライアントコンソール 32 ビットは Campaign の最新バージョンとの互換性がなくなります。64 ビットのクライアントコンソールを使用する必要があります。


### オペレーティングシステム {#o-s-eol}

19.1 リリースより、Adobe Campaign は次のオペレーティングシステムへの対応を終了します。

* CentOS 6 [詳細情報](https://wiki.centos.org/Download)
* Debian 7。[詳細情報](https://wiki.debian.org/DebianReleases)
* RHEL 6.x。[詳細情報](https://access.redhat.com/ja/support/policy/updates/errata)
* Windows Server 2008。[詳細情報](https://support.microsoft.com/ja-jp/lifecycle/search/1163)
* SLES 11。[詳細情報](https://www.suse.com/lifecycle)

### Web サーバー {#web-server-eol}

19.1 Spring リリースより、Adobe Campaign は次の WEB サーバーへの対応を終了します。

* Apache 2.2。 [詳細](https://httpd.apache.org/)
* Microsoft IIS 7。[詳細情報](https://support.microsoft.com/ja-jp/lifecycle/search/810)

### ツール {#tools-eol}

19.1 Spring リリースより、Adobe Campaign は次のツールへの対応を終了します。

* Java JDK 7。[詳細情報](http://www.oracle.com/technetwork/java/javase/eol-135779.html)
* Libre Office 3.5／4.3／5.x（他のツールに埋め込まれた場合を除く）。[詳細情報](https://wiki.documentfoundation.org/ReleasePlan/Archive#End-of-Life_Releases)

### データベースエンジン {#dbe-eol}

次のデータベースエンジンはエディターによって非推奨となったので、アドビではサポートしません。これらのバージョンを使用する顧客は、最新バージョンにアップグレードするか、別のバージョンに移行する必要があります。

互換性のあるバージョンのリストにアクセスするには、[Campaign 互換性マトリックス](../../rn/using/compatibility-matrix.md)を参照してください。

**Federated Data Access（FDA）**

20.2リリース以降、Adobe Campaignは次のFDAサーバーとの互換性がなくなりました。

* DB2 UDB 10.5

19.1 Springリリース以降、Adobe Campaignは次のFDAサーバーとの互換性がなくなりました。

* PostgreSQL 9.3。[詳細情報](https://www.postgresql.org/support/versioning)
* MySQL 5.5。[詳細情報](http://www.fromdual.com/support-for-mysql-from-oracle)
* DB2 9.5。[詳細情報](http://www-01.ibm.com/support/docview.wss?uid=swg21168270)
* Teradata 14 – 14.1。[詳細情報](https://community.teradata.com/t5/Database/Teradata-Database-Product-Life-Cycle/td-p/35068)

Campaign Classic は、Federated Data Access（FDA）の次のサーバーと互換性がありません。

* DB2 UDB 9.5、9.7。より新しいバージョンの DB2 は、Federated Data Access（FDA）を通じてサポートされます。[詳細情報](http://www-01.ibm.com/support/docview.wss?uid=swg21168270)
* Oracle 9i、10G R2。より新しいバージョンの Oracle は、Federated Data Access（FDA）を通じてサポートされます。[詳細情報](http://www.oracle.com/us/support/library/lifetime-support-technology-069183.pdf)
* PostgreSQL 8.3、8.4、9.0、9.1、9.2。より新しいバージョンの PostgreSQL は、Federated Data Access（FDA）を通じてサポートされます。[詳細情報](https://www.postgresql.org/support/versioning)
* MSSQL 2000、2005、2008 R2。より新しいバージョンの SQL Server は、Federated Data Access（FDA）を通じてサポートされます。[詳細情報](https://support.microsoft.com/ja-jp/lifecycle/search/1044)
* MySQL 5.1。より新しいバージョンの MySQL は、Federated Data Access（FDA）を通じてサポートされます。[詳細情報](https://en.wikipedia.org/wiki/InfiniDB)
* InfiniDB は提供が終了しました（EOL）。[詳細情報](https://www.mysql.com/jp/support/)
* Teradata 13、13.1。より新しいバージョンの Teradata は、Federated Data Access（FDA）を通じてサポートされます。[詳細情報](https://www.info.teradata.com/download.cfm?ItemID=1007255)
* Netezza 6.02、7.0。Netezza は提供が終了しました（EOL）。[詳細情報](https://en.wikipedia.org/wiki/Netezza)
* AsterData 5.0。AsterData は提供が終了しました（EOL）。[詳細情報](https://en.wikipedia.org/wiki/Aster_Data_Systems)
* Sybase IQ 15.2、15.4、15.5、Sybase ASE 15.0。より新しいバージョンの Sybase は、Federated Data Access（FDA）を通じてサポートされます。[詳細情報](https://sites.google.com/site/dbatipsandtricks/time-tracker)
* HiveSQL 経由の Hadoop：Hadoop 2.7.3、HiveSQL 1.2.1。Adobe Campaign Classic は、Federated Data Access（FDA）を通じて、HiveSQL 経由の Hadoop の一覧に示されたバージョンを引き続きサポートしますが、これらのバージョンは、HortonWorks（HDP 2.4.X、2.5.x、2.6.x）および HDInsight 3.4（HDP 2.4）、3.5（HDP 2.5）、3.6（HDP 2.6）と統合されます。

**RDBMS サーバー**

Adobe Campaign は、次の RDBMS サーバーと互換性がありません。
* Oracle 10GR2
* PostgreSQL 9.0 ～ 9.3
* SQL Server 2005
* MySQL 5.1
* DB2 UDB 9.7
