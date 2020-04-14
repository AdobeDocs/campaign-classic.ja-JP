---
title: Campaign Classicの廃止および削除された機能
description: このページリストは廃止され、Adobe Campaignクラシックの機能は削除されました
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
source-git-commit: 79f8cc179fcbf9d537a1cc889b268a43202d7369

---


# Deprecated and removed features {#deprecated-and-removed-features}

アドビは、製品の機能を評価し続けて、より最新の代替手段に置き換える必要のある旧機能を特定し、全体的な顧客価値を向上させ、常に下位互換性を慎重に考慮します。 Adobe Campaignクラシックはサードパーティのツールと連携するので、サポートされているバージョンのみを実装するために、定期的に互換性が更新されます。 以下に、Version Classicとの互換性がなくなったAdobe Campaignを示します。

差し迫ったCampaign Classic機能の削除/交換を伝えるため、次のルールが適用されます。

* 廃止のお知らせが先に来ます。 非推奨の機能は引き続き既存のユーザーが使用できますが、それ以上の拡張やドキュメント化は行われません。
* 非推奨の機能が削除されるのは、以下のリリースでは早くても可能です。 実際のターゲット削除日は、このページで発表されています。

このプロセスにより、お客様は、実際に削除される前に、新しいバージョンまたは廃止された機能の後継バージョンに実装を適合させるために、少なくとも1つのリリースサイクルを提供します。

>[!NOTE]
>Adobe Campaignリリースと新機能については、リリースノートを参 [照してください](../../rn/using/latest-release.md)。


## 廃止された機能 {#deprecated-features}

この節では、リストの最新リリースで非推奨とマークされている機能についてCampaign Classicします。

一般に、将来のリリースで削除される予定の機能は、代替機能と共に非推奨に設定されます。 これらの機能は、新しいCampaign Standardのお客様は利用できなくなったか、新しい実装には使用しないでください。 また、製品ドキュメントからも削除されます。

お客様は、現在の導入で機能を利用しているかどうかを確認し、提供されている代替機能を使用するように導入を変更する計画を立てることをお勧めします。 ターゲットの削除日を参照して、それに応じて環境とプロジェクトの更新を計画してください。

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
   <td>ファイル・ベースのアーカイブ<br></td>
   <td><p>E メールアーカイブは、専用の BCC E メールアドレスを通じて使用できるようになりました。<a href="../../installation/using/email-archiving.md">詳細情報</a></p> 
   <p><em>ターゲットの削除日：キャンペーン20.2リリース — 2020年6月</em></p><br> </td>
  </tr> 
   <tr> 
   <td>リード管理<br> </td>
   <td>リード<br> </td>
   <td><p>Leads ClassicのLeads Managementパッケージは、Adobe Campaign管理のライフサイクル全体を構築し、維持するプロセスを簡素化しました。 同様の機能は、他のネイティブワークフローアクティビティやデータモデルの変更を介して実装できます。</p> 
   <p><em>ターゲットの削除日：キャンペーン20.2リリース — 2020年6月</em></p><br> </td>
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

### Adobe Campaign19.2リリース {#compat-19-2-release}

19.2 Fall リリースより、Adobe Campaign は次のオペレーティングシステムへの対応を廃止します。2020 年末で互換性の維持の取り組みを終了します。

* Webサーバー：Apache 2.2。詳 [細](https://wiki.centos.org/About/Product)
* オペレーティングシステム：CentOS 6. [さらに詳しく](https://wiki.centos.org/About/Product)

[互換性マトリックス](https://helpx.adobe.com/jp/campaign/kb/compatibility-matrix.html)を参照し、新しいバージョンにアップグレードするか、新しいシステムに移行してください。

## 削除された機能 {#removed-features}

この節では、リストから削除された機能に関するCampaign Standardを示します。

<table> 
 <tbody> 
  <tr> 
   <td><strong>エリア — 機能</strong></td>
   <td><strong>置き換え</strong></td> 
   <td><strong>バージョン</strong></td> 
  </tr> 
   <tr> 
   <td>キャンペーンAPIドキュメント — jsapi.chmファイル<br></td>
   <td>Campaign Classic API を専用ページから入手できるようになりました。If you were using the jsapi.chm file, you should now refer to <a href="https://docs.adobe.com/content/help/en/campaign-classic/technicalresources/api/index.html">the new online version</a>.</td>
   <td>19.1</td>
  </tr> 
  <tr> 
   <td>キャンペーンオーケストレーション — 予測マーケティング</td>
   <td>Predictive Classicの予測マーケティング機能の大部分は、Adobe Campaignモデルの消費です。 予測マーケティングワークフローのアクティビティは今後のバージョンでは削除されますが、Adobe Campaignは、他のワークフローアクティビティを通じて、外部ソースからの予測モデルの消費と使用を引き続きサポートします。</td>
   <td>18.10</td>
  </tr> 
  <tr> 
   <td>Web アプリケーション — マイクロサイト</td>
   <td>セキュリティを強化するため、ドメイン設定ファイル上の専用ドメインへのアクセスのみをAdobe Campaignに制限する必要があります。 DNSエイリアスを使用して、パーソナライズされたURLをキャンペーンで引き続き使用できます。 <a href="https://helpx.adobe.com/jp/campaign/kb/domain-name-delegation.html">詳細情報</a></td>
   <td>18.10</td>
  </tr> 
  <tr> 
   <td>プッシュ通知 — iOS Binary Connector<br></td>
   <td>アドビは、Appleの推奨に従って、レガシーのiOS Binary Connectorを削除します。 より高機能でより効率的なHTTP/2ベースのコネクタが既に用意されています。</td>
   <td>18.10</td>
  </tr> 
   <tr> 
   <td>モバイルチャネル- MMSおよびWAPのプッシュメッセージ</td>
   <td>MMSおよびWapのプッシュチャネルは使用できなくなりました。 代わりに、 <a href="../../delivery/using/sms-channel.md">SMSとプッシュ</a> 配信を利用 <a href="../../delivery/using/about-mobile-app-channel.md">できます</a> 。</td>
   <td>18.4</td>
  </tr> 
   <tr> 
   <td>モバイルチャネル- LINE v1</td>
   <td>LINE Connectパッケージは、Linux Classicでのインストールには使用できなくなりました。Adobe Campaign アドビでは、新しいLINEメッセージパッケージを使用してLINEチャネルを送信することをお勧めします。 <a href="../../delivery/using/line-channel.md">詳細情報</a></td>
   <td>18.4</td>
  </tr> 
 </tbody> 
</table>

## 互換性の終了 {#end-of-compatibility}

>[!CAUTION]
>
>Adobe Campaignクラシックは、互換性マトリックスに記載されているすべてのシステムおよびツールと [互換性がありま](https://helpx.adobe.com/jp/campaign/kb/compatibility-matrix.html)す。 これらのサードパーティ製システムおよびツールの特定のバージョンが、それぞれの作成者と共に提供終了(EOL)に達した場合、Adobe Campaignはこれらのバージョンと互換性がなくなります。非推奨と発表され、その後の製品リリースで互換性マトリックスから削除されます。 問題を回避するため、互換性マトリックスに記載されているシステムのサポート対象バージョンを使用していることを確認してください。

### クライアントコンソール {#client-console-eol}

Adobe Campaignクラシッククライアントコンソールは、次のシステムでは実行できなくなりました。エディターで非推奨になったシステムです。 これらのバージョンの1つでキャンペーンクライアントコンソールを実行しているお客様は、ターゲットの削除日の前に最新バージョンにアップグレードする必要があります。 [互換性マトリックス](https://helpx.adobe.com/jp/campaign/kb/compatibility-matrix.html)を参照してください。

* Windows Server 2003、2008、2008 R2
* Windows XP、Vista

### オペレーティングシステム {#o-s-eol}

19.1リリース以降、Adobe Campaignは次のオペレーティングシステムと互換性がなくなりました。

* Debian 7. [詳細情報](https://wiki.debian.org/DebianReleases)
* RHEL 6.x詳 [細](https://access.redhat.com/support/policy/updates/errata)。
* Windows Server 2008。 [詳細情報](https://support.microsoft.com/en-us/lifecycle/search/1163)
* SLES 11. [詳細情報](https://www.suse.com/lifecycle)

### Webサーバー {#web-server-eol}

19.1 Springリリース以降、Adobe Campaignは次のWebサーバーと互換性がなくなりました。

* Microsoft IIS 7。 [詳細情報](https://support.microsoft.com/en-us/lifecycle/search/810)

### ツール {#tools-eol}

19.1 Springリリース以降、Adobe Campaignは次のツールと互換性がなくなりました。

* Java JDK 7。 [詳細情報](http://www.oracle.com/technetwork/java/javase/eol-135779.html)
* Office 3.5 / 4.3 / 5.xライブラリ（別のツールに埋め込まれた場合を除く）。 [詳細情報](https://wiki.documentfoundation.org/ReleasePlan/Archive#End-of-Life_Releases)

### データベースエンジン {#dbe-eol}

アドビでは、次のデータベースエンジンはエディターで非推奨となっているので、サポートしていません。 これらのバージョンを使用しているお客様は、最新バージョンにアップグレードするか、別のバージョンに移行する必要があります。

互換性のあるバージ [ョンのリストにアクセスするには、『](https://helpx.adobe.com/jp/campaign/kb/compatibility-matrix.html) Campaign Classic互換性マトリックス』を参照してください。

**FEDERATED DATA ACCESS(FDA)**

19.1 Springリリース以降、Adobe Campaignは次のFDAサーバーとの互換性がなくなりました。

* Oracle 11G [詳細情報](http://www.oracle.com/us/support/library/lifetime-support-technology-069183.pdf)
* PostgreSQL 9.3.詳 [細](https://www.postgresql.org/support/versioning)。
* MySQL 5.5. &lt;[さらに詳しく](http://www.fromdual.com/support-for-mysql-from-oracle).
* DB2 9.5.詳 [細](http://www-01.ibm.com/support/docview.wss?uid=swg21168270)。
* Teradata 14 - 14.1詳 [細](https://community.teradata.com/t5/Database/Teradata-Database-Product-Life-Cycle/td-p/35068)。

Campaign Classicは、Federated Data Access(FDA)内の次のサーバーと互換性がありません。

* DB2 UDB 9.5、9.7。DB2のより新しいバージョンは、Federated Data Access(FDA)を通じてサポートされます。 [詳細情報](http://www-01.ibm.com/support/docview.wss?uid=swg21168270)
* Oracle 9i、10G R2。 Oracleの最新バージョンは、Federated Data Access(FDA)を通じてサポートされます。 [詳細情報](http://www.oracle.com/us/support/library/lifetime-support-technology-069183.pdf)
* PostgreSQL 8.3、8.4、9.0、9.1、9.2。PostgreSQLのより新しいバージョンは、Federated Data Access(FDA)を通じてサポートされます。 [詳細情報](https://www.postgresql.org/support/versioning)
* MSSQL 2000、2005、2008 R2。 SQL Serverの最新バージョンは、Federated Data Access(FDA)を通じてサポートされます。 [詳細情報](https://support.microsoft.com/en-us/lifecycle/search/1044)
* MySQL 5.1.MySQLの最新バージョンは、Federated Data Access(FDA)を通じてサポートされます。 [詳細情報](https://en.wikipedia.org/wiki/InfiniDB)
* InfiniDBは提供終了に達しました。 [詳細情報](https://www.mysql.com/support)
* Teradata 13, 13.1.最新バージョンのTeradataは、Federated Data Access(FDA)を通じてサポートされます。 [詳細情報](https://www.info.teradata.com/download.cfm?ItemID=1007255)
* Netezza 6.02、7.0。ネテッツァは終焉を迎えた。 [詳細情報](https://en.wikipedia.org/wiki/Netezza)
* AsterData 5.0を参照してください。AsterDataが提供終了に達しました。 [詳細情報](https://en.wikipedia.org/wiki/Aster_Data_Systems)
* Sybase IQ 15.2、15.4、15.5、Sybase ASE 15.0。Sybaseの最新バージョンは、Federated Data Access(FDA)を通じてサポートされます。 [詳細情報](https://sites.google.com/site/dbatipsandtricks/time-tracker)
* HiveSQL経由のHadoop:Hadoop 2.7.3、HiveSQL 1.2.1。Adobe Campaignクラシックは、Federated Data Access(FDA)を通じてHiveSQLを介してHadoopの一覧に記載されているバージョンを引き続きサポートしますが、これらのバージョンは次のバージョンと統合されます。HortonWorks(HDP 2.4.X、2.5.x、2.6.x)およびHDInsight 3.4(HDP 2.4)、3.5(HDP 2.5)、3.6(HDP 2.6)

**RDBMSサーバ**

Adobe Campaignは、次のRDBMSサーバーと互換性がありません：
* Oracle 10GR2、11G
* PostgreSQL 9.0 ～ 9.3
* SQL Server 2005
* MySQL 5.1
* DB2 UDB 9.7
