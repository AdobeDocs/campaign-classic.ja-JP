---
product: campaign
title: Campaign Classic の非推奨（廃止予定）および削除された機能
description: このページには、Adobe Campaign Classic の非推奨および削除された機能が表示されます
feature: Release Notes
role: User
level: Beginner
exl-id: d60d67de-6618-4f3b-be4a-ad7633ab5645
source-git-commit: 84e6b2fad97f0ca5d6621cff4648e0be0bef7521
workflow-type: ht
source-wordcount: '1652'
ht-degree: 100%

---

# 非推奨（廃止予定）および削除された機能 {#deprecated-and-removed-features}



アドビは、製品の機能を評価し続けて、より新しい代替手段に置き換えるべき旧機能を特定し、全体的な顧客の価値を向上させ、常に後方互換性を慎重に考慮します。Adobe Campaign Classic はサードパーティ製ツールと連携しており、サポート対象バージョンのみに対応するために、定期的に互換性が更新されています。Adobe Campaign Classic と互換性がなくなったバージョンを、以下および[互換性マトリックス](../../rn/using/compatibility-matrix.md)に示します。

Campaign Classic 機能の差し迫った削除／置換を伝達するため、次の規則が適用されます。

* まず、廃止予定のお知らせが来ます。非推奨（廃止予定）の機能は引き続き既存のユーザーに提供できサポートされますが、それ以上の機能強化やドキュメント化はおこなわれません。
* 非推奨（廃止予定）の機能は、以下のリリースで最も早く削除されます。実際の削除予定日は、このページで発表されます。

このプロセスにより、顧客は、実際に削除する前に、新しいバージョンや非推奨（廃止予定）の機能の後継バージョンに実装を適応させるために、少なくとも 1 つのリリースサイクルを提供できます。

>[!NOTE]
>Adobe Campaign リリースと新機能は、[リリースノート](../../rn/using/latest-release.md)に一覧表示されています。

## 非推奨（廃止予定）の機能 {#deprecated-features}

この節では、最新の Campaign Classic リリースで非推奨（廃止予定）となった機能の一覧を示します。

一般に、将来のリリースで削除される予定の機能は、まず非推奨に設定されます。これらの機能は、新しい Campaign Classic の顧客は利用できなくなるか、新しい実装には使用するべきではないものです。また、製品ドキュメントからも削除されます。

顧客は現在のデプロイメントで機能を利用しているかどうかを確認し、実装を変更する計画を立てるようお勧めします。削除予定日を参照し、それに応じて環境やプロジェクトの更新を計画してください。

<table> 
 <tbody> 
   <tr>
   <td><strong>機能</strong></td>
   <td><strong>詳細</strong></td>
  </tr>
  <tr>
 <td>Campaign（Neolane）レガシー SDK</td>
 <td><p>モバイルアプリケーション用 Campaign（Neolane）SDK は非推奨（廃止予定）になりました。代わりに、データ収集 UI で Adobe Campaign 拡張機能を設定して、Adobe Experience Platform Mobile SDK を使用します。Adobe Experience Platform Mobile SDK は、モバイルアプリでアドビの Experience Cloud のソリューションとサービスを強化するのに役立ちます。SDK の設定はデータ収集 UI を通じて管理され、柔軟な設定と拡張可能なルールベースの統合を実現します。モバイルアプリチャネルを設定する方法については、<a href="https://experienceleague.adobe.com/ja/docs/campaign/campaign-v8/send/push/push-settings">Campaign v8 ドキュメント</a>を参照してください。</p>
<p>削除予定日：2025年7月31日（PT） </p>
</td>
</tr>
<tr>
 <td>Facebook でのソーシャルマーケティング</td>
 <td><p>Facebook を使用したソーシャルマーケティングは非推奨（廃止予定）になりました。X（旧 Twitter）統合を使用してソーシャルメディアに投稿したり、アドビと連携してカスタムチャネルを作成したりできます。</p>
  <!--p>Target removal date: End of 2023</p-->
  </td>
</tr>
<tr>
 <td>ACS コネクタ</td>
 <td><p>ACS コネクタ（プライムオファー）は非推奨（廃止予定）となりました。 Campaign のエクスポート／インポート機能を使用して、両方の製品のデータを抽出および挿入できます。</p>
  <!--p>Target removal date: End of 2023</p-->
  </td>
</tr>
 </tbody> 
</table>

## 削除された機能 {#removed-features}

この節には、Campaign Classic から削除された機能が記載されています。

<table> 
 <tbody>
  <tr> 
   <td><strong>機能</strong></td>
   <td><strong>詳細</strong></td>
  <tr>  
      <tr>
  <td>Adobe Analytics Data Connector<br></td>
   <td><p>Adobe Analytics Data Connector は、2022年8月17日（PT）に削除されました。 Campaign 21.1.3 リリースで非推奨（廃止予定）となりました。</p>
   <p>このコネクタを使用する場合は、それに応じて実装を適応させる必要があります。<a href="../../integrations/using/gs-aa.md">詳細情報</a></p>
  </td>
 </tr>
    <tr>
  <td>配信品質の技術的監視レポート<br></td>
   <td><p>配信品質の技術的監視レポートは使用できなくなりました。 Campaign 21.1.3 リリースで非推奨（廃止予定）となりました。</p>
   <!--p>If needed, you can receive this report daily by email until the feature removal date. To request it, open a specific <a href="https://helpx.adobe.com/jp/enterprise/admin-guide.html/enterprise/using/support-for-experience-cloud.ug.html">Support Case</a> and specify the name of the instance and the email address(es) to send the report to.</p--> 
  </td>
 </tr>
  <tr>
  <td>OAuth 認証（OAuth および JWT）<br></td>
  <td><p> トリガー統合認証（当初はパイプラインにアクセスするための OAuth 認証設定に基づいていた）が変更され、Adobe I/O に移動しました。この認証モードは、Campaign 20.3 リリースで非推奨となりました。<p>
  <p>トリガー統合を使用している場合は、<a href="../../integrations/using/about-triggers.md#implement">このページ</a>で実装の適応方法を確認してください。</p> 
  <p>OAuth 認証の廃止予定について詳しくは、この<a href="https://github.com/AdobeDocs/analytics-1.4-apis/blob/master/docs/APIEOL.md">ページ</a>を参照してください。</p> 
  <!--p><em>Target removal date: October 20, 2021. Hosted environments benefit from an extension until May 25, 2022. </em></p-->
  </td>
  </tr>
   <td>レポート<br></td>
   <td><p>Adobe Flash Player の提供終了に伴い、ゲージレポートとグラフレンダリングエンジンは使用できなくなりました。 <a href="../../reporting/using/creating-a-new-report.md">詳細情報</a></p>
  </tr>
  <tr>  
   <td>FAX チャネル<br></td>
   <td><p>Campaign 21.1.3 リリース以降、FAX チャネルは使用できなくなりました。<a href="../../delivery/using/steps-about-delivery-creation-steps.md">詳細情報</a></p>
  </tr>
  <tr>
  <td>Demdex ドメイン<br></td>
  <td><p> Campaign 21.1.3 リリース以降、Adobe Experience Cloud へのオーディエンスの読み込みおよび書き出しに demdex ドメインを使用できなくなりました。<a href="../../integrations/using/configuring-shared-audiences-integration-in-adobe-campaign.md">詳細情報</a></p> 
  </td>
  </tr>
   <tr> 
   <td>Windows NT 認証<br></td>
   <td><p>Campaign 20.3 リリースより、Microsoft SQL Server で新しいデータベースを設定する際の使用可能な認証方法から Windows NT 認証が削除されました。<a href="../../installation/using/creating-and-configuring-the-database.md#step-1---selecting-the-database-engine">詳細情報</a></p></td>
  </tr>
   <tr> 
   <td>ファイルベースのメールのアーカイブ<br></td>
   <td><p>Campaign 20.2 リリースより、ファイルベースのメールのアーカイブは使用できなくなりました。メールアーカイブは、専用の BCC メールアドレスを通じて使用できるようになりました。<a href="../../installation/using/email-archiving.md">詳細情報</a></p></td>
  </tr> 
   <tr> 
   <td>リード管理</td>
   <td><p>Campaign 20.2 リリースより、リード管理パッケージは使用できなくなりました。他のネイティブワークフローアクティビティやデータモデルの変更を介しても、同様の機能を実装できます。</p></td>
   </tr>
   <tr>
   <td>Campaign API ドキュメント - jsapi.chm ファイル</td>
   <td>Campaign 19.1 リリースより、Campaign Classic API は専用ページで利用できます。従来の jsapi.chm ファイルを使用していた場合は、<a href="https://experienceleague.adobe.com/developer/campaign-api/api/index.html?lang=ja">新しいオンラインバージョン</a>を参照する必要があります。</td>
  </tr> 
  <tr> 
   <td>キャンペーンオーケストレーション - 予測マーケティング</td>
   <td>Campaign 18.10 リリースより、予測マーケティング機能は使用できなくなりました。</td>
  </tr> 
  <tr> 
   <td>web アプリケーション - マイクロサイト</td>
   <td>Campaign 18.10 リリース以降、マイクロサイトは使用できなくなりました。Adobe Campaign 設定ファイルの専用ドメインのみにアクセスを制限することでセキュリティを向上させ、DNS エイリアスを使用して Campaign でパーソナライズされた URL を使用することができます。</td>
  </tr> 
  <tr> 
   <td>プッシュ通知 - iOS バイナリコネクタ</td>
   <td>Campaign 18.10 リリースより、Apple のレコメンデーションに従って、従来の iOS バイナリコネクタを削除しました。HTTP/2 ベースのコネクタは、より高機能でより効率的です。</td>
  </tr> 
  <tr> 
   <td>decryptString API</td>
   <td><p>Campaign 18.6 リリースより、セキュリティ上の理由から、<em>decryptString</em> API は、新しいインストールではデフォルトで使用できなくなりました。</p> 
   <p>18.6（以降）へのアップグレード後、この API は有効化されなくなり、<em>decryptPassword</em> 関数に置き換えられます。<a href="https://experienceleague.adobe.com/developer/campaign-api/api/f-decryptPassword.html?lang=ja&hl=decrypt">詳細情報</a></p></td>
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

<!--## Deprecated compatibility {#deprecated-compatibility}

The following systems are deprecated for Campaign Classic. Please refer to the [Compatibility matrix](../../rn/using/compatibility-matrix.md) to upgrade to a newer version or move to a new system before the compatibility ends.-->

## 互換性の終了 {#end-of-compatibility}

>[!CAUTION]
>
>Adobe Campaign Classic は、[互換性マトリックス](../../rn/using/compatibility-matrix.md)に記載されているすべてのシステムおよびツールと互換性があります。これらのサードパーティ製システムおよびツールの特定のバージョンが、それぞれの作成者による提供が終了した（EOL）場合、Adobe Campaign はこれらのバージョンとの互換性を失います。これらは非推奨と発表された後、以降の製品リリースで互換表から削除されます。問題を回避するため、互換性マトリックスに記載されているシステムのサポート対象バージョンを使用していることを確認してください。

### クライアントコンソール {#client-console-eol}

Adobe Campaign Classic クライアントコンソールは、次のシステムでは実行できなくなりました。エディターで非推奨になっています。Campaign クライアントコンソールをこれらのバージョンのいずれかで実行している場合は、削除予定日より前に最新バージョンにアップグレードする必要があります。[互換性マトリックス](../../rn/using/compatibility-matrix.md)を参照してください。

* Windows Server 2003、2008、2008 R2
* Windows 7、XP、Vista

>[!NOTE]
>Campaign 20.1 リリースより、Campaign Classic クライアントコンソール 32 ビットは Campaign の最新バージョンとの互換性がなくなります。64 ビットのクライアントコンソールを使用する必要があります。

### オペレーティングシステム {#o-s-eol}

* 7.3.1 リリースより、Adobe Campaign は Windows 8 および Windows Server 2012 との互換性を失います。

* 22.1 リリースより、Adobe Campaign は CentOs 8.x（64 ビット）との互換性を失います。CentOS Linux 8 は、2021年12月31日（PT）に提供終了（EOL）となります。[詳細情報](https://www.centos.org/centos-linux-eol/)。

  このオペレーティングシステムを使用していた場合は、それに応じて実装を適応させます。CentOS 7.x（64 ビット）と RHEL 8.x/7.x（64 ビット）は引き続きサポートされます。

* 21.1.3 リリース以降、Adobe Campaign は Debian 8 との互換性がなくなります。

* 19.1 リリース以降、Adobe Campaign は次のオペレーティングシステムへの対応を終了します。

   * CentOS 6。[詳細情報](https://wiki.centos.org/Download)
   * Debian 7。[詳細情報](https://wiki.debian.org/DebianReleases)
   * RHEL 6.x。[詳細情報](https://access.redhat.com/ja/support/policy/updates/errata)
   * Windows Server 2008。[詳細情報](https://support.microsoft.com/ja-jp/lifecycle/search/1163)
   * SLES 11。[詳細情報](https://www.suse.com/lifecycle)

### Web サーバー {#web-server-eol}

19.1 Spring リリース以降、Adobe Campaign は下記の web サーバーに対応しなくなります。

* Apache 2.2。[詳細情報](https://httpd.apache.org/)
* Microsoft IIS 7。[詳細情報](https://support.microsoft.com/en-us/lifecycle/search/810)

### ツール {#tools-eol}

19.1 Spring リリースより、Adobe Campaign は次のツールへの対応を終了します。

* Java JDK 7。[詳細情報](https://www.oracle.com/technetwork/java/javase/eol-135779.html)
* Libre Office 3.5／4.3／5.x（他のツールに埋め込まれた場合を除く）。[詳細情報](https://wiki.documentfoundation.org/ReleasePlan/Archive#End-of-Life_Releases)

### データベースエンジン {#dbe-eol}

次のデータベースエンジンはエディターによって非推奨となったので、アドビではサポートしません。これらのバージョンを使用する顧客は、最新バージョンにアップグレードするか、別のバージョンに移行する必要があります。

互換性のあるバージョンのリストにアクセスするには、[Campaign 互換性マトリックス](../../rn/using/compatibility-matrix.md)を参照してください。

**Federated Data Access（FDA）**

20.2 リリースより、Adobe Campaign は次の FDA サーバーへの対応を終了します。

* DB2 UDB 10.5

19.1 Spring リリースより、Adobe Campaign は次の FDA サーバーへの対応を終了します。

* PostgreSQL 9.3.
* MySQL 5.5。
* DB2 9.5。
* Teradata 14 – 14.1。

Campaign Classic は、Federated Data Access（FDA）の次のサーバーと互換性がありません。より新しいバージョンまたはシステムを使用してください。

* DB2 UDB 9.5、9.7。
* Oracle 9i、10G R2。
* PostgreSQL の 9.6 までのバージョンは、提供が終了しました。
* MSSQL 2000、2005、2008 R2。
* MySQL 5.1。
* InfiniDB は提供が終了しました（EOL）。
* Teradata 13、13.1。
* Netezza 6.02、7.0。Netezza は提供が終了しました（EOL）。
* AsterData 5.0。AsterData は提供が終了しました（EOL）。
* Sybase IQ 15.2、15.4、15.5 および Sybase ASE 15.0。
* HiveSQL 経由の Hadoop：Hadoop 2.7.3、HiveSQL 1.2.1。Adobe Campaign Classic は、Federated Data Access（FDA）を通じて、HiveSQL 経由の Hadoop の一覧に示されたバージョンを引き続きサポートしますが、これらのバージョンは、HortonWorks（HDP 2.4.X、2.5.x、2.6.x）および HDInsight 3.4（HDP 2.4）、3.5（HDP 2.5）、3.6（HDP 2.6）と統合されます。

**RDBMS サーバー**

19.1 Spring リリースより、Adobe Campaign は次の RDBMS サーバーへの対応を終了します。

* Oracle 10GR2
* PostgreSQL 9.0 ～ 9.3
* SQL Server 2005
* MySQL 5.1
* DB2 UDB 9.7

PostgreSQL の 9.6 までのバージョンは、提供が終了しました。したがって、これらは Adobe Campaign ではサポートされません。

### SMS コネクタ {#sms-eol}

20.2 リリースより、レガシー SMS コネクタは非推奨（廃止予定）になります。Adobe Campaign は次と互換性がありません。

* 一般的な SMPP（バイナリモードをサポートする SMPP バージョン 3.4）
* Sybase365（SAP SMS 365）
* CLX Communications
* Tele2
* O2
* iOS

### CRM コネクタ {#crm-connectors}

Campaign 21.1 リリース以降、次の CRM コネクタは Campaign との互換性がなくなりました。

* SOAP API - オンプレミス：2007、2015、2016
* SOAP API - オンライン：2015、2016
* Web API - Microsoft Dynamics CRM 2016
* Web API - Microsoft Dynamics CRM 2016 Update 1
* Oracle On Demand API
