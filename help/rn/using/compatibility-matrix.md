---
title: 互換性マトリックス
description: 互換性マトリックス
page-status-flag: never-activated
uuid: 269d590c-5a6d-40b9-a879-02f5033863fc
contentOwner: sauviat
products: SG_CAMPAIGN/CLASSIC
audience: rns
content-type: reference
topic-tags: latest-release-notes
discoiquuid: 5df34f55-135a-4ea8-afc2-f9427ce5ae7b
index: y
internal: n
snippet: y
translation-type: tm+mt
source-git-commit: 5e8598fd445f6e2ebd891af1e15c07eb836cd647
workflow-type: tm+mt
source-wordcount: '621'
ht-degree: 40%

---


# 互換性マトリックス{#compatibility-matrix}

This document lists all systems and components supported for the latest build of **Adobe Campaign Classic (v6.11 and v7)**. このリストに含まれていない製品とバージョンは、Adobe Campaign とは互換性がありません。

## 重要な注意事項{#important-notes}

このマトリックスは、追加された新しいサポートアイテムおよび削除された非推奨アイテムを定期的に更新します。

特に断りのない限り、すべてのマイナーリリースがサポートされます。

Adobe Campaignクラシックは、このページに表示されるすべてのシステムおよびツールと互換性があります。 これらのサードパーティ製システムおよびツールの特定のバージョンは、それぞれの作成者と共に提供終了(EOL)に達すると、Adobe Campaignはこれらのバージョンとの互換性がなくなり、以降の製品リリースで互換表から削除されます。 問題を回避するため、互換性マトリックスに記載されているシステムのサポート対象バージョンを使用していることを確認してください。

非推奨の項目の詳細については、 [このページを参照してください](../../rn/using/deprecated-features.md)。

## オペレーティングシステム{#OperatingSystems}

<table> 
<tbody> 
<tr> 
<td>CentOs</td>
<td>
<p>7.x（64 ビット）</p>
</td>
</tr>
<tr>
<td>Debian</td>
<td>
<p>8（64 ビット）</p>
<p>9（64 ビット）</p>
<p>10（64 ビット）</p>
</td>
</tr>
<tr>
<td>RHEL</td>
<td>
<p>7.x（64 ビット）</p>
<p><strong>重要：</strong> RHELを使用する場合は、SELinuxを無効にするか、有効にしたSELinuxがキャンペーン操作の問題を引き起こしていないかを設計者にカスタムSELinuxルールを書かせる必要があります。</p>
</td>
</tr>
<tr>
<td>Windows Server</td>
<td>
<p>2012</p>
<p>2012 R2</p>
<p>2016</p>
</td>
</tr>
</tbody>
</table>

## Web Servers{#WebServers}

<table>
<tbody>
<tr>
<td>Microsoft IIS</td>
<td>
<p>8.0(Windows Server 2012、Windows 8)</p>
<p>8.5(Windows Server 2012 R2)</p>
<p>Windows Server 2016では10.0</p>
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
<td>Java開発キット(JDK)</td>
<td>
<p>8</p>
<p>9</p>
<p>このアプリケーションは、Oracleが開発したJava Development Kit(JDK)およびOpenJDKに対して承認されています。</p>
</td>
</tr>
<tr>
<td>図書館</td>
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

## RDBMSドライバ{#RDBMSdrivers}

次のRDBMSドライバがサポートされています。

* Oracle SQL*Net 11

* Oracle SQL*Net 12

* PostgreSQL（libpq）

* SQLServer

* DB2 （ODBCドライバ）


>[!NOTE]
>
>RDBMSドライバはRDBMSサーバーのバージョンと一致する必要があります。

## RDBMSサーバー{#RDBMSservers}

<table>
<tbody>
<tr>
<td>Oracle</td>
<td>
<p>11g R2</p>
<p>12c</p>
<p>18c</p>
<p>19c</p>
</td>
</tr>
<tr>
<td>PostgreSQL</td>
<td>
<p>9.4.x</p>
<p>9.5.x</p>
<p>9.6.x</p>
<p>10.x</p>
<p>11.x</p>
<p>注意： 上記のバージョンでAmazon RDS for PostgreSQLを使用することもできます。</p>
</td>
</tr>
<tr>
<td>SQL Server</td>
<td>
<p>2012 - SP1 および SP2</p>
<p>2014</p>
<p>2016</p>
<p>2017</p>
<p>警告： Linuxでキャンペーンサーバーを実行している場合、Microsoft SQL Serverはプライマリデータベースとしてサポートされません。 Refer to the <a href="https://docs.campaign.adobe.com/doc/AC/en/INS_Prerequisites_and_recommendations__Database.html#Microsoft_SQL_Server">Installation guide</a>.</p>
</td>
</tr>
</tbody>
</table>

>[!NOTE]
>
>PostgreSQL は、ホスト環境のデフォルトのデータベースサーバーです。

## CRM コネクタ{#CRMconnectors}

<table>
<tbody>
<tr>
<td>SalesforceコネクタAPI</td>
<td>
<p>APIバージョン37</p>
</td>
</tr>
<tr>
<td>SFDC API</td>
<td>
<p>APIバージョン15</p>
<p>APIバージョン21</p>
</td>
</tr>
<tr><td>Oracle On Demand API</td>
<td>
<p>Web Services v1.0 API</p>
</td>
</tr>
<tr>
<td>MS Dynamics</td>
<td>
<p>SOAP API — オンプレミス： 2007, 2015, 2016</p>
<p>SOAP API — オンライン： 2015, 2016</p>
<p>Web API — オンプレミスおよびオンライン： 365, 2016, 2016 Update 1</p>
</td>
</tr>
</tbody>
</table>

## Federated Data Access (FDA){#FederatedDataAccessFDA}

<table>
<tbody>
<tr>
<td>Microsoft Azure Synapse Analytics</td>
<td> </td>
</tr>
<tr>
<td>Amazon Redshift</td>
<td><p> </p>
</td>
</tr>
<tr>
<td>Oracle</td>
<td>
<p>11g</p>
<p>12c</p>
<p>18c</p>
</td>
</tr>
<tr>
<td>PostgreSQL</td>
<td>
<p>9.4.x</p>
<p>9.5.x</p>
<p>9.6.x</p>
<p>10.x</p>
<p>11.x</p>
</td>
</tr>
<tr><td>SQL Server</td>
<td>
<p>2012 SP1およびSP2</p>
<p>2014</p>
<p>2016</p>
<p>2017</p>
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
<p>15.0</p>
<p>15.10</p>
<p>16</p>
<p>16.20</p>
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
<p>バージョン1 SP12以降</p>
</td>
</tr>
<tr><td>HiveSQLを使用したHadoop</td>
<td>
<p>HortonWorks HDP 2.4.X、2.5.x、2.6.x</p>
<p>HDInsight 3.4 (HDP 2.4)、3.5 (HDP 2.5)、3.6 (HDP 2.6)</p>
<p>Cloudera CDH6.x</p>
</td>
</tr>
<tr>
<td>Snowflake</td>
<td> </td>
</tr>
</tbody>
</table>

## クライアントコンソールのオペレーティングシステム{#ClientConsoleoperatingsystems}

<table>
<tbody>
<tr>
<td>Windows Server</td>
<td>
<p>2012</p>
<p>2016</p>
</td>
</tr>
<tr>
<td>Windows</td>
<td>
<p>8</p>
<p>10（日本語インスタンスの場合に推奨）</p>
</td>
</tr>
</tbody>
</table>

## モバイル SDK{#MobileSDK}

<table>
<tbody>
<tr>
<td>Android</td>
<td>
<p>7.x</p>
<p>8.x</p>
<p>9.0</p>
<p>モバイルSDKビルド1.0.27を使用します。</p>
</td>
</tr>
<tr>
<td>iOS</td>
<td>
<p>iOS 9</p>
<p>iOS 10</p>
<p>iOS 11</p>
<p>iOS 12</p>
<p>iOS 13</p>
<p>モバイルSDKビルド1.0.26（32ビットおよび64ビットバージョンと互換）</p>
</td>
</tr>
</tbody>
</table>

## ブラウザー{#Browsers}

Internet Explorerのバージョン11がサポートされています。

次のブラウザーでは、最新バージョンがサポートされています。

* Microsoft Edge

* Firefox

* クロム

* Safari

## Experience Cloud との統合{#ExperienceCloudintegrations}

For integrations with Adobe solutions, refer to this [section](https://docs.adobe.com/content/help/ja-JP/campaign-classic/using/integrating-with-adobe-experience-cloud/about-campaign-integrations.html#experience-cloud-integrations).

## その他の関連ヘルプ{#Morelikethis}

* [Campaign Classic リリースノート](https://docs.adobe.com/content/help/ja-JP/campaign-classic/using/release-notes/latest-release.html)
* [インストールガイド](https://docs.adobe.com/content/help/ja-JP/campaign-classic/using/installing-campaign-classic/architecture-and-hosting-models/general-architecture.html)
* [非推奨の機能およびシステム](https://helpx.adobe.com/jp/campaign/kb/deprecated-and-removed-features.html)
* [ビルドアップグレード手順](https://helpx.adobe.com/jp/campaign/kb/acc-build-upgrade.html)
* [Campaign Classic 互換性マトリックス（19.0 リリース）](https://helpx.adobe.com/jp/campaign/kb/compatibility-matrix-19-0.html)
* [Campaign Classic 互換性マトリックス（19.1 リリース）](https://helpx.adobe.com/jp/campaign/kb/compatibility-matrix-19-1.html)

