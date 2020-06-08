---
title: Campaign Classic の非推奨（廃止予定）および削除された機能
description: このページリストは、Adobe Campaign Classic の非推奨（廃止予定）および削除された機能です
page-status-flag: never-activated
uuid: null
contentOwner: simonetn
products: SG_CAMPAIGN/CLASSIC
audience: rn
content-type: reference
topic-tags: campaign-classic-deprecated-features
internal: n
snippet: y
translation-type: tm+mt
source-git-commit: e46325ab8f68a0b71198aee9cf04f2b1eb97fdd3
workflow-type: tm+mt
source-wordcount: '1468'
ht-degree: 66%

---


# 非推奨（廃止予定）および削除された機能 {#deprecated-and-removed-features}

アドビは、製品の機能を評価し続けて、より新しい代替手段に置き換えるべき旧機能を特定し、全体的な顧客の価値を向上させ、常に後方互換性を慎重に考慮します。Adobe Campaign Classic はサードパーティ製ツールと連携しており、サポート対象バージョンのみに対応するために、定期的に互換性が更新されています。Adobe Campaignクラシックと互換性がなくなったバージョンを、次と [互換表に示します](https://helpx.adobe.com/jp/campaign/kb/compatibility-matrix.html)。

Campaign Classic 機能の差し迫った削除／置換を伝達するため、次の規則が適用されます。

* まず、廃止予定のお知らせが来ます。非推奨の機能は引き続き既存のユーザーに対して使用でき、サポートされますが、それ以上の拡張やドキュメント化は行われません。
* 非推奨（廃止予定）の機能は、以下のリリースで最も早く削除されます。削除の実際のターゲット日は、このページで発表されます。

このプロセスにより、顧客は、実際に削除する前に、新しいバージョンや非推奨（廃止予定）の機能の後継バージョンに実装を適応させるために、少なくとも 1 つのリリースサイクルを提供できます。

>[!NOTE]
>Adobe Campaign リリースと新機能は、[リリースノート](../../rn/using/latest-release.md)に一覧表示されています。

## 非推奨（廃止予定）の機能 {#deprecated-features}

この節では、最新の Campaign Classic リリースで非推奨とマークされている機能を一覧化します。

一般に、将来のリリースで削除される予定の機能は、非推奨になる前に設定されます。 これらの機能は、新しいCampaign Classicのお客様はご利用いただけなくなるか、新しい実装には使用しないでください。 また、製品ドキュメントからも削除されます。

お客様は、現在の導入で機能を利用しているかどうかを確認し、導入を変更する計画を立てることをお勧めします。 削除の目標期日を参照し、それに応じて環境やプロジェクトの更新を計画してください。

<table> 
 <tbody> 
   <tr>
   <td><strong>機能</strong></td>
   <td><strong>置き換え</strong></td> 
  </tr>
   <tr>
  <td>SMSコネクタ<br></td>
  <td><p> 20.2リリース以降、次のSMSコネクタは非推奨となります。<p>
   <ul>
   <li>NetSize</li>
   <li>汎用SMPP（バイナリモードをサポートするSMPPバージョン3.4）</li>
   <li>Sybase365 (SAP SMS 365)</li>
   <li>CLX通信</li>
   <li>Tele2</li>
   <li>O2</li>
   <li>iOS</li>
   </ul>
  <p>これらのコネクタの1つを使用する場合は、それに応じて実装を適応させる必要があります。 <a href="../../delivery/using/sms-channel.md">詳細情報</a>。</p> 
  <p>このテクノノテートでレガシーコネクターを移行する方法 <a href="https://helpx.adobe.com/campaign/kb/sms-connector.html">を説明します</a>。</p>
  <p><em>ターゲットの削除日： 2021</em></p>
  </td> 
 </tr>
  <tr>  
   <td>FAX チャネル<br></td>
   <td><p>20.2リリース以降、Faxチャネルは非推奨となります。</p> 
   <p>このチャネルを使用する場合は、それに応じて実装を適応させる必要があります。 <a href="../../delivery/using/communication-channels.md">キャンペーンチャネルの詳細</a> 。</p>
   <p><em>ターゲットの削除日： 2021</em></p></td>
  </tr>
 </tbody> 
</table>

## 削除された機能 {#removed-features}

このセクションでは、Campaign Classicから削除された機能に関するリストを説明します。

<table> 
 <tbody> 
  <tr> 
   <td><strong>領域 - 機能</strong></td>
   <td><strong>置き換え</strong></td> 
  </tr> 
   <tr> 
   <td>ファイル・ベースの電子メール・アーカイブ<br></td>
   <td><p>キャンペーン20.2以降のリリースでは、ファイルベースの電子メールアーカイブは使用できなくなりました。 E メールアーカイブは、専用の BCC E メールアドレスを通じて使用できるようになりました。<a href="../../installation/using/email-archiving.md">詳細情報</a>。</p></td>
  </tr> 
   <tr> 
   <td>リード管理</td>
   <td><p>キャンペーン20.2リリース以降、Leads Managementパッケージは使用できなくなりました。 他のネイティブワークフローアクティビティやデータモデルの変更を介しても、同様の機能を実装できます。</p></td>
   </tr>
   <tr>
   <td>キャンペーンAPIドキュメント — jsapi.chmファイル</td>
   <td>キャンペーン19.1リリース以降、Campaign ClassicAPIは専用ページで利用できます。 If you were using the legacy jsapi.chm file, you should now refer to <a href="https://docs.adobe.com/content/help/en/campaign-classic/technicalresources/api/index.html">the new online version</a>.</td>
  </tr> 
  <tr> 
   <td>キャンペーンオーケストレーション - 予測マーケティング</td>
   <td>キャンペーン18.10のリリース以降、予測マーケティング機能は使用できなくなりました。</td>
  </tr> 
  <tr> 
   <td>Web アプリケーション - マイクロサイト</td>
   <td>キャンペーン18.10のリリース以降、Micrositesはご利用いただけません。 Adobe Campaign構成ファイル上の専用ドメインへのアクセスのみを制限し、DNSエイリアスを使用してパーソナライズされたURLをキャンペーンで使用することで、セキュリティを向上できます。 <a href="https://helpx.adobe.com/jp/campaign/kb/domain-name-delegation.html">詳細情報</a>。</td>
  </tr> 
  <tr> 
   <td>プッシュ通知 — iOSバイナリコネクタ</td>
   <td>アドビでは、Appleの推奨に従って、レガシーのiOS Binary Connectorのキャンペーン18.10リリースからを削除しました。 HTTP/2 ベースのコネクタは、より高機能でより効率的です。</td>
  </tr> 
  <tr> 
   <td>decryptString API</td>
   <td><p>Starting Campaign 18.6 release, for security reasons, <em>decryptString</em> API is no longer available by default for new installations.</p> 
   <p>18.6（以降）へのアップグレード後、この API は有効化されなくなり、<em>decryptPassword</em> 関数に置き換えられます。<a href="https://docs.adobe.com/content/help/en/campaign-classic/technicalresources/api/f-decryptPassword.html?hl=decrypt">詳細情報</a>。</p></td>
  </tr> 
   <tr> 
   <td>モバイルチャネル- MMS および WAP プッシュメッセージ</td>
   <td>キャンペーン18.4リリース以降、MMSとWapのプッシュチャネルは使用できなくなりました。 代わりに、<a href="../../delivery/using/sms-channel.md">SMS</a> および<a href="../../delivery/using/about-mobile-app-channel.md">プッシュ</a>配信を利用できます。</td>
  </tr> 
   <tr> 
   <td>モバイルチャネル - LINE v1</td>
   <td>キャンペーン18.4リリースから、LINE Connectパッケージは使用できなくなりました。 新しいLINEチャネルパッケージを置き換える場合は、 <a href="../../delivery/using/line-channel.md">詳細情報</a>。</td>
  </tr> 
 </tbody> 
</table>

## 非推奨（廃止予定）の互換性 {#deprecated-compatibility}

次のCampaign Classicシステムは廃止されました。 Please refer to the [Compatibility matrix](https://helpx.adobe.com/jp/campaign/kb/compatibility-matrix.html) to upgrade to a newer version or move to a new system before the compatibility ends.

### Adobe Campaign 20.2 リリース {#compat-20-2-release}

20.2リリース以降、次のCampaign Classicは推奨されません。 互換性は20.3リリース（2020年9月）で終了します。

* クライアントコンソール： Windows 7
* 従来のSMSコネクタ（以下の非推奨機能の節を参照）

### Adobe Campaign 19.2 リリース {#compat-19-2-release}

19.2リリース以降、次のオペレーティングシステムはCampaign Classicに使用されなくなりました。 2020 年末で互換性の維持の取り組みを終了します。

* Webサーバー： Apache 2.2。
* オペレーティングシステム：CentOS 6。

[互換性マトリックス](https://helpx.adobe.com/jp/campaign/kb/compatibility-matrix.html)を参照し、新しいバージョンにアップグレードするか、新しいシステムに移行してください。

## 互換性の終了 {#end-of-compatibility}

>[!CAUTION]
>
>Adobe Campaign Classic は、[互換性マトリックス](https://helpx.adobe.com/jp/campaign/kb/compatibility-matrix.html)に記載されているすべてのシステムおよびツールと互換性があります。これらのサードパーティ製システムおよびツールの特定のバージョンが、それぞれの作成者による提供が終了した（EOL）場合、Adobe Campaign はこれらのバージョンとの互換性を失います。これらは非推奨と発表された後、以降の製品リリースで互換表から削除されます。問題を回避するため、互換性マトリックスに記載されているシステムのサポート対象バージョンを使用していることを確認してください。

### クライアントコンソール {#client-console-eol}

Adobe Campaign Classic クライアントコンソールは、次のシステムでは実行できなくなりました。エディターで非推奨になっています。Campaign クライアントコンソールをこれらのバージョンのいずれかで実行している場合は、削除のターゲット日より前に最新バージョンにアップグレードする必要があります。[互換性マトリックス](https://helpx.adobe.com/jp/campaign/kb/compatibility-matrix.html)を参照してください。

* Windows Server 2003、2008、2008 R2
* Windows XP、Vista

>[!NOTE]
>キャンペーン20.1リリース以降、Campaign Classicクライアントコンソールの32ビットはキャンペーンの最新バージョンとの互換性がなくなりました。 64ビットのクライアントコンソールを使用する必要があります。


### オペレーティングシステム {#o-s-eol}

19.1 リリースより、Adobe Campaign は次のオペレーティングシステムへの対応を終了します。

* Debian 7。[詳細情報](https://wiki.debian.org/DebianReleases)。
* RHEL 6.x. [Learn more](https://access.redhat.com/ja/support/policy/updates/errata)
* Windows Server 2008。[詳細情報](https://support.microsoft.com/ja-jp/lifecycle/search/1163)。
* SLES 11。[詳細情報](https://www.suse.com/lifecycle)。

### Web サーバー {#web-server-eol}

19.1 Spring リリースより、Adobe Campaign は次の WEB サーバーへの対応を終了します。

* Microsoft IIS 7。[詳細情報](https://support.microsoft.com/ja-jp/lifecycle/search/810)。

### ツール {#tools-eol}

19.1 Spring リリースより、Adobe Campaign は次のツールへの対応を終了します。

* Java JDK 7。[詳細情報](http://www.oracle.com/technetwork/java/javase/eol-135779.html)。
* Libre Office 3.5／4.3／5.x（他のツールに埋め込まれた場合を除く）。[詳細情報](https://wiki.documentfoundation.org/ReleasePlan/Archive#End-of-Life_Releases)。

### データベースエンジン {#dbe-eol}

次のデータベースエンジンはエディターによって非推奨となったので、アドビではサポートしません。これらのバージョンを使用する顧客は、最新バージョンにアップグレードするか、別のバージョンに移行する必要があります。

互換性のあるバージョンのリストにアクセスするには、[Campaign Classic 互換性マトリックス](https://helpx.adobe.com/jp/campaign/kb/compatibility-matrix.html)を参照してください。

**Federated Data Access（FDA）**

19.1 Spring リリースより、Adobe Campaign は次の FDA サーバーへの対応を終了します。

* PostgreSQL 9.3. [Learn more](https://www.postgresql.org/support/versioning)
* MySQL 5.5。 [詳細情報](http://www.fromdual.com/support-for-mysql-from-oracle)
* DB2 9.5. [Learn more](http://www-01.ibm.com/support/docview.wss?uid=swg21168270)
* Teradata 14 – 14.1. [Learn more](https://community.teradata.com/t5/Database/Teradata-Database-Product-Life-Cycle/td-p/35068)

Campaign Classic は、Federated Data Access（FDA）の次のサーバーと互換性がありません。

* DB2 UDB 9.5、9.7。より新しいバージョンの DB2 は、Federated Data Access（FDA）を通じてサポートされます。[詳細情報](http://www-01.ibm.com/support/docview.wss?uid=swg21168270)。
* Oracle 9i、10G R2。より新しいバージョンの Oracle は、Federated Data Access（FDA）を通じてサポートされます。[詳細情報](http://www.oracle.com/us/support/library/lifetime-support-technology-069183.pdf)。
* PostgreSQL 8.3、8.4、9.0、9.1、9.2。より新しいバージョンの PostgreSQL は、Federated Data Access（FDA）を通じてサポートされます。[詳細情報](https://www.postgresql.org/support/versioning)。
* MSSQL 2000、2005、2008 R2。より新しいバージョンの SQL Server は、Federated Data Access（FDA）を通じてサポートされます。[詳細情報](https://support.microsoft.com/ja-jp/lifecycle/search/1044)。
* MySQL 5.1。より新しいバージョンの MySQL は、Federated Data Access（FDA）を通じてサポートされます。[詳細情報](https://en.wikipedia.org/wiki/InfiniDB)。
* InfiniDB は提供が終了しました（EOL）。[詳細情報](https://www.mysql.com/jp/support/)。
* Teradata 13、13.1。より新しいバージョンの Teradata は、Federated Data Access（FDA）を通じてサポートされます。[詳細情報](https://www.info.teradata.com/download.cfm?ItemID=1007255)。
* Netezza 6.02、7.0。Netezza は提供が終了しました（EOL）。[詳細情報](https://en.wikipedia.org/wiki/Netezza)。
* AsterData 5.0。AsterData は提供が終了しました（EOL）。[詳細情報](https://en.wikipedia.org/wiki/Aster_Data_Systems)。
* Sybase IQ 15.2、15.4、15.5、Sybase ASE 15.0。より新しいバージョンの Sybase は、Federated Data Access（FDA）を通じてサポートされます。[詳細情報](https://sites.google.com/site/dbatipsandtricks/time-tracker)。
* HiveSQL 経由の Hadoop：Hadoop 2.7.3、HiveSQL 1.2.1。Adobe Campaign Classic は、Federated Data Access（FDA）を通じて、HiveSQL 経由の Hadoop の一覧に示されたバージョンを引き続きサポートしますが、これらのバージョンは、HortonWorks（HDP 2.4.X、2.5.x、2.6.x）および HDInsight 3.4（HDP 2.4）、3.5（HDP 2.5）、3.6（HDP 2.6）と統合されます。

**RDBMS サーバー**

Adobe Campaign は、次の RDBMS サーバーと互換性がありません。
* Oracle 10GR2
* PostgreSQL 9.0 ～ 9.3
* SQL Server 2005
* MySQL 5.1
* DB2 UDB 9.7
