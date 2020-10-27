---
title: 互換性マトリックス
description: Campaign Classic 互換性マトリックス
page-status-flag: never-activated
uuid: 269d590c-5a6d-40b9-a879-02f5033863fc
contentOwner: sauviat
products: SG_CAMPAIGN/CLASSIC
audience: rns
content-type: reference
topic-tags: latest-release-notes
discoiquuid: 5df34f55-135a-4ea8-afc2-f9427ce5ae7b
translation-type: tm+mt
source-git-commit: 9cff35424b389d0cc6adb8ce0ec81d3258ffb6ba
workflow-type: tm+mt
source-wordcount: '549'
ht-degree: 87%

---


# 互換性マトリックス{#compatibility-matrix}

This document lists all systems and components supported for [the latest build](../../rn/using/latest-release.md) of **Adobe Campaign Classic**. このリストに含まれていない製品とバージョンは、Adobe Campaign とは互換性がありません。

ゴールド・スタンダードのユーザーの場合は、 [ゴールド・スタンダード互換表を参照](../../rn/using/compatibility-matrix-gs.md)。

## 重要な注意事項{#important-notes}

特に断りのない限り、すべてのマイナーリリースがサポートされます。

In its [latest build](../../rn/using/latest-release.md), Adobe Campaign Classic is compatible with all the systems and tools listed in this page. これらのサードパーティ製システムおよびツールの特定のバージョンが、それぞれの作成者による提供が終了した（EOL）場合、Adobe Campaign はこれらのバージョンとの互換性を失います。これらは以降の製品リリースで互換表から削除されます。問題を回避するため、互換性マトリックスに記載されているシステムのサポート対象バージョンを使用していることを確認してください。

非推奨の項目の詳細については、[このページ](../../rn/using/deprecated-features.md)を参照してください。

>[!CAUTION]
>
>このマトリックスは、追加された新しいサポートアイテムおよび削除された非推奨アイテムを定期的に更新します。

## オペレーティングシステム{#OperatingSystems}

<table> 
<tbody> 
<tr> 
<td>CentOs</td>
<td>
<p>8.x（64 ビット）</p>
<p>7.x（64 ビット）</p>
</td>
</tr>
<tr>
<td>Debian</td>
<td>
<p>10（64 ビット）</p>
<p>9（64 ビット）</p>
<p>8（64 ビット）</p>
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
<p>2016</p>
<p>2012 R2</p>
<p>2012</p>
</td>
</tr>
</tbody>
</table>

## Web サーバー{#WebServers}

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
</td>
</tr>
</tbody>
</table>

## ツール{#Tools}

<table>
<tbody>
<tr>
<td>Java 開発キット（JDK）</td>
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

## RDBMS サーバー{#RDBMSservers}

>[!NOTE]
>
>RDBMS ドライバーは RDBMS サーバーのバージョンと一致する必要があります。

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
<p>12.x</p>
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
<p>31 日</p>
<p>2017</p>
<p>2016</p>
<p>2014</p>
<p>2012 - SP1 および SP2</p>
<p>警告：Linux で Campaign サーバーを実行している場合、Microsoft SQL Server はプライマリデータベースとしてサポートされません。<a href="https://docs.adobe.com/content/help/ja-JP/campaign-classic/using/installing-campaign-classic/prerequisites-and-recommendations-/database.html#Microsoft_SQL_Server">詳細情報</a>。</p>
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
<tr><td>Oracle On Demand API</td>
<td>
<p>Web サービス v1.0 API</p>
</td>
</tr>
<tr>
<td>MS Dynamics</td>
<td>
<p>SOAP API - オンプレミス：2007、2015、2016</p>
<p>SOAP API - オンライン：2015、2016</p>
<p>Web API - オンプレミスおよびオンライン：365、2016、2016 Update 1</p>
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
<p>18c</p>
<p>12c</p>
<p>11g</p>
</td>
</tr>
<tr>
<td>PostgreSQL</td>
<td>
<p>12.x</p>
<p>11.x</p>
<p>10.x</p>
<p>9.6.x</p>
<p>9.5.x</p>
<p>9.4.x</p>
</td>
</tr>
<tr><td>SQL Server</td>
<td>
<p>31 日</p>
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
<p>バージョン 1 SP12 以降</p>
</td>
</tr>
<tr><td>HiveSQL による Hadoop</td>
<td>
<p>HortonWorks HDP 2.4.x、2.5.x、2.6.x</p>
<p>HDInsight 3.4（HDP 2.4）、3.5（HDP 2.5）、3.6（HDP 2.6）</p>
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
<p>2016</p>
<p>2012</p>
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
<p>7.x, 8.x, 9.0</p>
<p>モバイル SDK ビルド 1.0.27 のサポート。</p>
</td>
</tr>
<tr>
<td>iOS</td>
<td>
<p>iOS 9 - 14</p>
<p>モバイル SDK ビルド 1.0.26 のサポート。32 および 64 ビットバージョンとの互換性。</p>
</td>
</tr>
</tbody>
</table>

## ブラウザー{#Browsers}

次のブラウザーでは、最新バージョンがサポートされています。Microsoft Edge、Mozilla Firefox、Google Chrome、Safari。

Internet Explorer 11がサポートされます。

## その他の関連ヘルプ{#Morelikethis}

* [Campaign Classic リリースノート](../../rn/using/latest-release.md)
* [インストールガイド](../../installation/using/general-architecture.md)
* [廃止された機能およびシステム](../../rn/using/deprecated-features.md)
* [ビルドアップグレード手順](https://helpx.adobe.com/jp/campaign/kb/acc-build-upgrade.html)
