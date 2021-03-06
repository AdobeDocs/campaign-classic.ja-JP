---
product: campaign
title: Campaign Classic の互換性マトリックス
description: Campaign Classic 互換性マトリックス
feature: Overview
role: User
level: Beginner
exl-id: b8c1f287-06f4-4c34-8cca-b0c7676abbc2
source-git-commit: 7f24c8be599d6dece41de848d64feb8079b10ff3
workflow-type: ht
source-wordcount: '768'
ht-degree: 100%

---

# 互換性マトリックス{#compatibility-matrix}

![](../../assets/v7-only.svg)

このドキュメントでは、**Adobe Campaign Classic v7** の[最新ビルド](../../rn/using/latest-release.md)でサポートされているすべてのシステムとコンポーネントを示します。このリストに含まれていない製品とバージョンは、Adobe Campaign とは互換性がありません。

[!DNL Gold Standard] ユーザーの場合は、[[!DNL Gold Standard]  互換性マトリックス](../../rn/using/gold-standard.md#compatibility-matrix-gs)を参照してください。

## 重要な注意事項{#important-notes}

特に断りのない限り、すべてのマイナーリリースがサポートされます。

Adobe Campaign Classic の[最新ビルド](../../rn/using/latest-release.md)は、このページに記載されているすべてのシステムおよびツールと互換性があります。これらのサードパーティ製システムおよびツールの特定のバージョンが、それぞれの作成者による提供が終了した（EOL）場合、Adobe Campaign はこれらのバージョンとの互換性を失います。これらは以降の製品リリースで互換表から削除されます。問題を回避するため、互換性マトリックスに記載されているシステムのサポート対象バージョンを使用していることを確認してください。

非推奨の項目の詳細については、[このページ](../../rn/using/deprecated-features.md)を参照してください。

>[!CAUTION]
>
>このマトリックスは、新しいサポート対象項目の追加および非推奨項目の削除により定期的に更新されます。

## オペレーティングシステム{#OperatingSystems}

<table> 
<tbody> 
<tr> 
<td>CentOS</td>
<td>
<p>8.x（64 ビット） </br><strong>重要：</strong> CentOS Linux 8 は、2021年12月31日（PT）に提供終了（EOL）となります。 詳しくは、<a href="../../rn/using/deprecated-features.md">非推奨（廃止予定）の機能</a>ページを参照してください。</p>
<p>7.x（64 ビット）</p>
<p><strong>重要</strong>：RHEL を使用する場合は、SELinux を無効にするか、アーキテクトにカスタム SELinux ルールを記述させ、有効にされた SELinux が Campaign 操作で問題を引き起こしていないことを確認する必要があります。</p>
</td>
</tr>
<tr>
<td>Debian</td>
<td>
<p>11（64 ビット）</p>
<p>10（64 ビット）</p>
<p>9（64 ビット）</p>
</td>
</tr>
<tr>
<td>RHEL</td>
<td>
<p>8.x（64 ビット）</p>
<p>7.x（64 ビット）</p>
<p><strong>重要</strong>：RHEL を使用する場合は、SELinux を無効にするか、アーキテクトにカスタム SELinux ルールを記述させ、有効にされた SELinux が Campaign 操作で問題を引き起こしていないことを確認する必要があります。</p>
</td>
</tr>
<tr>
<td>Windows Server</td>
<td>
<p>2019（7.2.1 リリース以降）</p>
<p>2016</p>
<p>2012 R2</p>
<p>2012</p>
</td>
</tr>
</tbody>
</table>

## web サーバー{#WebServers}

<table>
<tbody>
<tr>
<td>Microsoft IIS</td>
<td>
<p>10.0（Windows Server 2016）および 2019</p>
<p>8.5（Windows Server 2012 R2）</p>
<p>8.0（Windows Server 2012 - Windows 8）</p>
</td>
</tr>
<tr>
<td>Apache</td>
<td>
<p>RHEL7 - CentOS 7、Debian 8/9、Windows（64 ビット）向けの 2.4</p>
</td>
</tr>
</tbody>
</table>

## ツール{#Tools}

<table>
<tbody>
<tr>
<td>Java Development Kit（JDK）</td>
<td>
<p>11</p>
<p>9</p>
<p>8</p>
<p>このアプリケーションは、Oracle が開発した Java Development Kit（JDK）および OpenJDK に対して承認されています。</p>
</td>
</tr>
<tr>
<td>Libre Office</td>
<td>
<p>7（お使いのシステムに埋め込まれている場合は以前のバージョン）</p>
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

## 関係データベース管理システム（RDBMS）{#RDBMSservers}

<table>
<tbody>
<tr>
<td>Oracle</td>
<td>
<p>19c</p>
<p>18c</p>
<p>12c</p>
<p>11g R2</p>
</td>
</tr>
<tr>
<td>PostgreSQL</td>
<td>
<p>13.x</p>
<p>12.x</p>
<p>11.x</p>
<p>10.x</p>
<p><strong>注意：</strong>上記のバージョンで Amazon RDS for PostgreSQL を使用することもできます。</p>
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
<p><strong>警告：</strong>Linux で Campaign サーバーを実行している場合、プライマリデータベースとしての Microsoft SQL Server の使用はサポートされません。<a href="../../installation/using/prerequisites-of-campaign-installation-in-linux.md#database-access-layers">詳細情報</a>。</p>
</td>
</tr>
</tbody>
</table>

>[!NOTE]
>
>* RDBMS ドライバは RDBMS サーバーのバージョンと一致する必要があります。
>
>* PostgreSQL はホスト環境の RDBMS です。


## CRM コネクタ{#CRMconnectors}

Adobe Campaign と互換性のある顧客関係管理（CRM）システムを次に示します。 Campaign CRM コネクタの[詳細](../../platform/using/crm-connectors.md)を説明します。

<table>
<tbody>
<tr>
<td>Salesforce コネクタ API</td>
<td>
<p>API バージョン 49</p>
</td>
</tr>
<tr>
<td>Microsoft Dynamics コネクタ</td>
<td>
<p>Web API</p>
</td>
</tr>
</tbody>
</table>

## Federated Data Access（FDA）{#FederatedDataAccessFDA}

Adobe Campaign [Federated Data Access モジュール](../../installation/using/about-fda.md)と互換性のある外部データベースを以下に示します。互換性は[ホスティングモデル](../../installation/using/hosting-models.md)に依存します。

**Managed Services**（ホスト）、**ハイブリッド**&#x200B;および&#x200B;**オンプレミス**&#x200B;環境は、Campaign を次の外部データベースシステムと接続できます。

<table>
<tbody>
<td><strong>データベースシステム</strong></td>
<td><strong>データベースのバージョン</strong></td>
<td><strong>Campaign のバージョン</strong></td>
<tr>
<tr>
<td>Snowflake</td>
<td> </td>
<td>7.2.1 以上</td>
</tr>
<tr>
<td>Google BigQuery</td>
<td> </td>
<td>7.2.1 以上</td>
</tr>
<tr>
<td>Amazon Redshift</td>
<td><p> </p>
<td>v7.0 19.1.4 以上</td>
</td>
</tr>
<tr>
<td>PostgreSQL</td>
<td>
<p>13.x</p>
<p>12.x</p>
<p>11.x</p>
<p>10.x</p>
</td>
<td>v7.0 19.1.4 以上</td>
</tr>
</tbody>
</table>

さらに、**ハイブリッド**&#x200B;環境および&#x200B;**オンプレミス**&#x200B;環境では、Campaign を次の外部データベースシステムとも接続できます。これらのシステムは Campaign **Managed Services**（ホスト）環境と&#x200B;**互換性がありません**。

<table>
<tbody>
<td><strong>データベースシステム</strong></td>
<td><strong>データベースのバージョン</strong></td>
<td><strong>Campaign のバージョン</strong></td>
<tr>
<td>Vertica</td>
<td> </td>
<td>v7.0 19.1.4 以上</td>
</tr>
<tr>
<td>Microsoft Azure Synapse Analytics</td>
<td> </td>
<td>v7.0 19.1.4 以上</td>
</tr>
<tr>
<td>Oracle</td>
<td>
<p>19c</p>
<p>18c</p>
<p>12c</p>
<p>11g</p>
</td>
<td>v7.0 以上</td>
</tr>
<tr><td>SQL Server</td>
<td>
<p>2019</p>
<p>2017</p>
<p>2016</p>
<p>2014</p>
<p>2012 SP1 および SP2</p>
</td>
<td>v7.0 以上</td>
</tr>
<tr><td>MySQL</td>
<td>
<p>8</p>
<p>5.7</p>
</td>
<td>
<p>v7.3 以上</p>
<p>v7.0 以上</p>
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
<td>v7.0 以上</td>
</tr>
<tr>
<td>Netezza</td>
<td>
<p>7.2</p>
</td>
<td>v7.0 以上</td>
</tr>
<tr>
<td>Sybase</td>
<td>
<p>IQ 16</p>
<p>ASE 15.7</p>
</td>
<td>v7.0 以上</td>
</tr>
<tr>
<td>SAP HANA</td>
<td>
<p>バージョン 1 SPS 12</p>
</td>
<td>v7.0 以上</td>
</tr>
<tr><td>HiveSQL による Hadoop</td>
<td>
<p>HortonWorks HDP 2.4.x、2.5.x、2.6.x</p>
<p>HDInsight 3.4（HDP 2.4）、3.5（HDP 2.5）、3.6（HDP 2.6）</p>
<p>Cloudera CDH6.x</p>
</td>
<td>v7.0 以上</td>
</tr>
</tbody>
</table>





## クライアントコンソール {#ClientConsoleoperatingsystems}

[Campaign クライアントコンソール](../../installation/using/installing-the-client-console.md)を使用するには、次のオペレーティングシステムとブラウザーが&#x200B;**必要**&#x200B;です。

### オペレーティングシステム

<table>
<tbody>
<tr>
<td>Microsoft Windows Server</td>
<td>
<p>2019（7.2.1 リリース以降）</p>
<p>2016</p>
<p>2012</p>
</td>
</tr>
<tr>
<td>Microsoft Windows</td>
<td>
<p>11（Campaign v7.3 以降）</p>
<p>10（日本語インスタンスの場合に推奨）</p>
<p>8</p>
</td>
</tr>
</tbody>
</table>

### ブラウザー

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

### Microsoft WebView2 ランタイム

<table>
<tbody>
<tr>
<td>
<p>Microsoft Edge WebView2 ランタイム
</p>
</td>
<td>
<p>最新バージョン</p>
</td>
<td>
<p><a href="http://www.adobe.com/go/acc-ms-webview2-runtime-download_jp">Microsoft Developer web サイトからダウンロード</a></p>
</td>
</tr>
</tbody>
</table>

## Mobile SDK{#MobileSDK}

以下に示すオペレーティングシステムでは、関連する [Mobile SDK](../../delivery/using/integrating-campaign-sdk-into-the-mobile-application.md) を使用して、Campaign を使用して[プッシュ通知を送信](../../delivery/using/about-mobile-app-channel.md)できます。

<table>
<tbody>
<tr>
<td>Android</td>
<td>
<p>12（Campaign v7.3 以降）、9.0、8.x、7.x</p>
<p>（モバイル SDK ビルド 1.1.1 を使用）</p>
</td>
</tr>
<tr>
<td>iOS</td>
<td>
<p>iOS 9～15</p>
<p>（32 ビットおよび 64 ビットバージョンと互換性のあるモバイル SDK ビルド 1.0.26 を使用）iOS 15 は Campaign v7.3 以降でサポートされています</p>
</td>
</tr>
</tbody>
</table>

## ブラウザー{#Browsers}

次のブラウザーは Campaign for [Web Access](../../campaign/using/accessing-marketing-campaigns.md#using-the-web-interface-) と互換性があります。

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

</tr>
</tbody>
</table>


## その他の関連リソース{#Morelikethis}

* [Campaign Classic リリースノート](../../rn/using/latest-release.md)
* [Campaign の一般的なアーキテクチャ](../../installation/using/general-architecture.md)
* [ハードウェアサイズについての推奨事項](../../technotes/using/hardware-sizing.md)
* [非推奨（廃止予定）の機能およびシステム](../../rn/using/deprecated-features.md)
* [ビルドアップグレード手順](../../production/using/build-upgrade.md)
