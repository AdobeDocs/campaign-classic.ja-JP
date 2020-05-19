---
title: Campaign Classicの廃止/削除された機能
description: このページリストは、Adobe Campaignクラシックの廃止および削除された機能です
page-status-flag: never-activated
uuid: null
contentOwner: simonetn
products: SG_CAMPAIGN/CLASSIC
audience: rn
content-type: reference
topic-tags: campaign-classic-deprecated-features
discoiquuid: null
internal: n
snippet: y
translation-type: tm+mt
source-git-commit: be148d7cd55097b9014d2f4d3b095c65a5ca8c54
workflow-type: tm+mt
source-wordcount: '1389'
ht-degree: 14%

---


# 廃止および削除された機能 {#deprecated-and-removed-features}

アドビは、製品の機能を評価し続けて、より新しい代替手段に置き換えるべき旧機能を特定し、全体的なお客様の価値を向上させ、常に下位互換性を慎重に考慮します。 Adobe Campaignクラシックはサードパーティのツールと連携するので、サポートされているバージョンのみを実装するため、互換性は定期的に更新されます。 Adobe Campaignクラシックと互換性がなくなったバージョンを次に示します。

Campaign Classic機能の差し迫った取り外し/交換を伝えるため、次の規則が適用されます。

* 廃止のお知らせが先に来ます。 非推奨の機能は引き続き既存のユーザーに提供できますが、それ以上の拡張やドキュメント化は行われません。
* 非推奨の機能は、以下のリリースで最も早く削除されます。 削除の実際のターゲット日は、このページで発表されています。

このプロセスにより、お客様は、実際に削除する前に、新しいバージョンや廃止された機能の後継バージョンに導入を適応させるために、少なくとも1つのリリースサイクルを提供できます。

>[!NOTE]
>Adobe Campaignリリースと新機能については、 [リリースノート](../../rn/using/latest-release.md)。


## Deprecated features {#deprecated-features}

この節では、最新のCampaign Classicリリースで非推奨とマークされている機能と機能についてリストします。

一般に、将来のリリースで削除される予定の機能は、非推奨となる最初のものに設定されます。代わりの機能も提供されます。 これらの機能は、新しいCampaign Classicのお客様はご利用いただけなくなるか、新しい実装には使用しないでください。 また、製品ドキュメントからも削除されます。

お客様は、現在の導入で機能を利用しているかどうかを確認し、提供される代替機能を使用するように導入を変更する計画を立てるようお勧めします。 ターゲットの削除日を参照して、環境とプロジェクトの更新を計画してください。

### Adobe Campaign18.6リリース {#ac-18-6-release}

<table> 
 <tbody> 
  <tr> 
   <td><strong>領域</strong></td>
   <td><strong>機能</strong></td> 
   <td><strong>置き換え</strong></td> 
  </tr> 
   <tr> 
   <td>Javascript SDK セキュリティ<br> </td>
   <td>decryptString<br> </td>
   <td><p>セキュリティ上の理由から、 <em>decryptString</em> APIは、新しいインストールではデフォルトで使用できなくなりました。</p> 
   <p>In the context of a postupgrade to 18.6 (and later), this API is no longer activated, and has been replaced by the <em>decryptPassword</em> function.</p><br> </td>
  </tr> 
 </tbody> 
</table>

### Adobe Campaign18.4リリース {#ac-18-4-release}

<table> 
 <tbody> 
  <tr> 
   <td><strong>領域</strong></td>
   <td><strong>機能</strong></td> 
   <td><strong>置き換え</strong></td> 
  </tr> 
   <tr> 
   <td>E メールのアーカイブ<br> </td>
   <td>ファイル・ベースのアーカイブ<br> </td>
   <td><p>E メールアーカイブは、専用の BCC E メールアドレスを通じて使用できるようになりました。<a href="../../installation/using/email-archiving.md">詳細情報</a></p> 
   <p><em>ターゲットの削除日： キャンペーン20.2リリース — 2020年6月</em></p><br> </td>
  </tr> 
   <tr> 
   <td>リード管理<br> </td>
   <td>リード<br> </td>
   <td><p>Adobe Campaignクラシックのリード管理パッケージは、リード管理ライフサイクル全体の構築と維持のプロセスを簡略化しました。 他のネイティブワークフローアクティビティやデータモデルの変更を介しても、同様の機能を実装できます。</p> 
   <p><em>ターゲットの削除日： キャンペーン20.2リリース — 2020年6月</em></p><br> </td>
  </tr> 
 </tbody> 
</table>


## 非推奨の互換性 {#deprecated-compatibility}

### Adobe Campaign20.1リリース {#compat-20-1-release}

2 月リリース の 20.1 より、Campaign Classic は次のシステムへの対応を廃止します。互換性は20.2リリース（2020年6月）で終了します。

<table> 
 <tbody> 
  <tr> 
   <td><strong>領域</strong></td>
   <td><strong>置き換え</strong></td> 
  </tr> 
   <tr> 
   <td>Campaign Classic クライアントコンソール 32 ビット<br> </td>
   <td><p>Campaign Classic クライアントコンソール 64 ビット</p><br> </td>
  </tr> 
 </tbody> 
</table>

### Adobe Campaign19.2リリース  {#compat-19-2-release}

19.2 Fall リリースより、Adobe Campaign は次のオペレーティングシステムへの対応を廃止します。2020 年末で互換性の維持の取り組みを終了します。

* Webサーバー： Apache 2.2。 [詳細](https://wiki.centos.org/About/Product)
* オペレーティングシステム： CentOS 6. [さらに詳しく](https://wiki.centos.org/About/Product)

[互換性マトリックス](https://helpx.adobe.com/jp/campaign/kb/compatibility-matrix.html)を参照し、新しいバージョンにアップグレードするか、新しいシステムに移行してください。

## 削除された機能 {#removed-features}

このセクションでは、Campaign Classicから削除された機能に関するリストを説明します。

<table> 
 <tbody> 
  <tr> 
   <td><strong>エリア — 機能</strong></td>
   <td><strong>置き換え</strong></td> 
   <td><strong>バージョン</strong></td> 
  </tr> 
   <tr> 
   <td>キャンペーンAPIドキュメント — jsapi.chmファイル<br> </td>
   <td>Campaign Classic API を専用ページから入手できるようになりました。If you were using the jsapi.chm file, you should now refer to <a href="https://docs.adobe.com/content/help/en/campaign-classic/technicalresources/api/index.html">the new online version</a>.</td>
   <td>19.1</td>
  </tr> 
  <tr> 
   <td>キャンペーンオーケストレーション — 予測マーケティング</td>
   <td>Adobe Campaignクラシックの予測マーケティング機能の大部分は、予測モデルの使用です。 予測マーケティングワークフローのアクティビティは今後のバージョンで削除されますが、Adobe Campaignは、他のワークフローアクティビティを介した外部ソースからの予測モデルの消費と使用を引き続きサポートします。</td>
   <td>18.10</td>
  </tr> 
  <tr> 
   <td>Web アプリケーション — マイクロサイト</td>
   <td>Adobe Campaign構成ファイル上の専用ドメインへのアクセスのみを制限することで、セキュリティを向上させます。 DNSエイリアスを使用して、パーソナライズされたURLをキャンペーンで引き続き使用できます。 <a href="https://helpx.adobe.com/jp/campaign/kb/domain-name-delegation.html">詳細情報</a></td>
   <td>18.10</td>
  </tr> 
  <tr> 
   <td>プッシュ通知 — iOSバイナリコネクタ<br> </td>
   <td>アドビは、Appleの推奨に従って、レガシーのiOS Binary Connectorを削除します。 HTTP/2ベースのコネクタは、より高機能でより効率的です。</td>
   <td>18.10</td>
  </tr> 
   <tr> 
   <td>モバイルチャネル- MMSおよびWAPのプッシュメッセージ</td>
   <td>MMSおよびWapのプッシュチャネルは使用できなくなりました。 代わりに、 <a href="../../delivery/using/sms-channel.md">SMS</a> / <a href="../../delivery/using/about-mobile-app-channel.md">プッシュ</a> 配信を利用できます。</td>
   <td>18.4</td>
  </tr> 
   <tr> 
   <td>モバイルチャネル- LINE v1</td>
   <td>LINE Connectパッケージは、Adobe Campaignクラシックではインストールできなくなりました。 アドビでは、新しいLINEチャネルパッケージを使用してLINEメッセージを送信することをお勧めします。 <a href="../../delivery/using/line-channel.md">詳細情報</a></td>
   <td>18.4</td>
  </tr> 
 </tbody> 
</table>

## 互換性の終了 {#end-of-compatibility}

>[!CAUTION]
>
>Adobe Campaignクラシックは、 [互換表に記載されているすべてのシステムおよびツールと互換性があります](https://helpx.adobe.com/jp/campaign/kb/compatibility-matrix.html)。 これらのサードパーティ製システムおよびツールの特定のバージョンが、それぞれの作成者と共に提供終了(EOL)に達した場合、Adobe Campaignはこれらのバージョンとの互換性を失います。 非推奨と発表された後、以降の製品リリースで互換表から削除されます。 問題を回避するため、互換表に記載されているシステムのサポート対象バージョンを使用していることを確認してください。

### クライアントコンソール {#client-console-eol}

Adobe Campaignクラシッククライアントコンソールは、次のシステムでは実行できなくなりました。エディターで非推奨になっています。 キャンペーンクライアントコンソールをこれらのバージョンのいずれかで実行している場合は、ターゲットを削除する前に最新バージョンにアップグレードする必要があります。 [互換性マトリックス](https://helpx.adobe.com/jp/campaign/kb/compatibility-matrix.html)を参照してください。

* Windows Server 2003、2008、2008 R2
* Windows XP、Vista

### オペレーティングシステム {#o-s-eol}

19.1リリース以降、Adobe Campaignは次のオペレーティングシステムとの互換性がなくなりました。

* デビアン7. [詳細情報](https://wiki.debian.org/DebianReleases)
* RHEL 6.x [詳細情報](https://access.redhat.com/support/policy/updates/errata)。
* Windows Server 2008 [詳細情報](https://support.microsoft.com/en-us/lifecycle/search/1163)
* SLES 11。 [詳細情報](https://www.suse.com/lifecycle)

### Webサーバー {#web-server-eol}

19.1 Springリリース以降、Adobe Campaignは次のWebサーバーとの互換性がなくなりました。

* Microsoft IIS 7 [詳細情報](https://support.microsoft.com/en-us/lifecycle/search/810)

### ツール {#tools-eol}

19.1 Springリリース以降、Adobe Campaignは次のツールとの互換性がなくなりました。

* Java JDK 7。 [詳細情報](http://www.oracle.com/technetwork/java/javase/eol-135779.html)
* Libre Office 3.5 / 4.3 / 5.x（他のツールに埋め込まれた場合を除く） [詳細情報](https://wiki.documentfoundation.org/ReleasePlan/Archive#End-of-Life_Releases)

### データベースエンジン {#dbe-eol}

次のデータベースエンジンはエディターによって非推奨となったので、アドビではサポートしていません。 これらのバージョンを使用するお客様は、最新バージョンにアップグレードするか、別のバージョンに移行する必要があります。

互換性のあるバージョンのリストにアクセスするには、 [Campaign Classic互換表](https://helpx.adobe.com/jp/campaign/kb/compatibility-matrix.html) （英語）を参照してください。

**FEDERATED DATA ACCESS(FDA)**

19.1 Springリリース以降、Adobe Campaignは次のFDAサーバーとの互換性がなくなりました。

* Oracle 11G. [詳細情報](http://www.oracle.com/us/support/library/lifetime-support-technology-069183.pdf)
* PostgreSQL 9.3. [詳細](https://www.postgresql.org/support/versioning)。
* MySQL 5.5. &lt;[さらに詳しく](http://www.fromdual.com/support-for-mysql-from-oracle).
* DB2 9.5。 [詳細情報](http://www-01.ibm.com/support/docview.wss?uid=swg21168270)。
* Teradata 14 - 14.1。 [詳細を表示します](https://community.teradata.com/t5/Database/Teradata-Database-Product-Life-Cycle/td-p/35068)。

Campaign Classicは、Federated Data Access(FDA)の次のサーバーと互換性がありません。

* DB2 UDB 9.5、9.7。DB2の最新バージョンは、Federated Data Access(FDA)を通じてサポートされます。 [詳細情報](http://www-01.ibm.com/support/docview.wss?uid=swg21168270)
* Oracle 9i、10G R2。 Federated Data Access(FDA)を通じて、Oracleの最新バージョンがサポートされます。 [詳細情報](http://www.oracle.com/us/support/library/lifetime-support-technology-069183.pdf)
* PostgreSQL 8.3, 8.4, 9.0, 9.1, 9.2。Federated Data Access(FDA)を通じて、より新しいバージョンのPostgreSQLがサポートされています。 [詳細情報](https://www.postgresql.org/support/versioning)
* MSSQL 2000、2005、2008 R2。 Federated Data Access(FDA)を通じて、より新しいバージョンのSQL Serverがサポートされます。 [詳細情報](https://support.microsoft.com/en-us/lifecycle/search/1044)
* MySQL 5.1。MySQLの最新バージョンは、Federated Data Access(FDA)を通じてサポートされます。 [詳細情報](https://en.wikipedia.org/wiki/InfiniDB)
* InfiniDBは提供終了に達しました。 [詳細情報](https://www.mysql.com/support)
* Teradata 13, 13.1。Teradataの最新バージョンは、Federated Data Access(FDA)を通じてサポートされます。 [詳細情報](https://www.info.teradata.com/download.cfm?ItemID=1007255)
* ネテッザは6.02、7.0。ネテッザは終焉を迎えた。 [詳細情報](https://en.wikipedia.org/wiki/Netezza)
* AsterData 5.0. AsterDataは提供終了に達しました。 [詳細情報](https://en.wikipedia.org/wiki/Aster_Data_Systems)
* Sybase IQ 15.2、15.4、15.5、Sybase ASE 15.0。Sybaseの最新バージョンは、Federated Data Access(FDA)を通じてサポートされます。 [詳細情報](https://sites.google.com/site/dbatipsandtricks/time-tracker)
* HiveSQL経由のHadoop: Hadoop 2.7.3、HiveSQL 1.2.1。Adobe Campaignクラシックは、Federated Data Access(FDA)を介してHiveSQLを介してHadoopの一覧に示されたバージョンを引き続きサポートしますが、これらのバージョンは次のバージョンと統合されます。 HortonWorks(HDP 2.4.X、2.5.x、2.6.x)およびHDInsight 3.4(HDP 2.4)、3.5(HDP 2.5)、3.6(HDP 2.6)

**RDBMSサーバ**

Adobe Campaignは、次のRDBMSサーバーと互換性がありません：
* Oracle 10GR2、11G
* PostgreSQL 9.0 ～ 9.3
* SQL Server 2005
* MySQL 5.1
* DB2 UDB 9.7
