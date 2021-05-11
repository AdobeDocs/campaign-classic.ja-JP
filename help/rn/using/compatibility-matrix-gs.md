---
solution: Campaign Classic
product: campaign
title: Campaign  [!DNL Gold Standard] の互換性マトリックス
description: Campaign Classic 互換性マトリックス（ [!DNL Gold Standard] リリース）
feature: 概要
role: Business Practitioner
level: Beginner
exl-id: 5c0ccaf6-7f82-4e4b-9247-261dbd0f127c
translation-type: tm+mt
source-git-commit: 69f6fcd21b27f095781bca4a62153086382f3d7f
workflow-type: tm+mt
source-wordcount: '538'
ht-degree: 92%

---

# [!DNL Gold Standard] 互換性マトリックス{#compatibility-matrix-gs}

このドキュメントでは、**Adobe Campaign Classic[!DNL Gold Standard]** のビルド 19.1 でサポートされているすべてのシステムとコンポーネントを示します。このリストに含まれていない製品とバージョンは、このバージョンの Adobe Campaign とは互換性がありません。

## 重要な注意事項{#important-notes-gs}

特に断りのない限り、すべてのマイナーリリースがサポートされます。

Adobe Campaign Classic は、このページに記載されているすべてのシステムおよびツールと互換性があります。これらのサードパーティ製システムおよびツールの特定のバージョンが、それぞれの作成者による提供が終了した（EOL）場合、Adobe Campaign はこれらのバージョンとの互換性を失います。これらは以降の製品リリースで互換表から削除されます。問題を回避するため、互換性マトリックスに記載されているシステムのサポート対象バージョンを使用していることを確認してください。

## オペレーティングシステム{#OperatingSystems-gs}

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

## web サーバー{#WebServers-gs}

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

## ツール{#Tools-gs}

<table>
<tbody>
<tr>
<td>Java 開発キット（JDK）</td>
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

## RDBMS サーバー{#RDBMSservers-gs}

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
<p>警告：Linux で Campaign サーバーを実行している場合、Microsoft SQL Server はプライマリデータベースとしてサポートされません。<a href="https://docs.adobe.com/content/help/ja-JP/campaign-classic/using/installing-campaign-classic/prerequisites-and-recommendations-/database.html#Microsoft_SQL_Server">詳細情報</a>。</p>
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

## CRM コネクタ{#CRMconnectors-gs}

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
<tr><td>Oracle オンデマンド API</td>
<td>
<p>Web サービス v1.0 API</p>
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

## Federated Data Access (FDA){#FederatedDataAccessFDA-gs}

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


## クライアントコンソール {#ClientConsoleoperatingsystems}

:warning:キャンペーンクライアントコンソールを使用するには、次のオペレーティングシステムとブラウザーが必要です。

### オペレーティングシステム

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

## モバイル SDK{#MobileSDK}

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
<p>モバイル SDK ビルド 1.0.26 のサポート。32 および 64 ビットバージョンとの互換性。</p>
</td>
</tr>
</tbody>
</table>

## ブラウザー{#Browsers}

次のブラウザーは、Web Accessのキャンペーンーと互換性があります。

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

## その他の関連ヘルプ{#Morelikethis-gs}

* [Campaign Classic リリースノート](../../rn/using/latest-release.md)
* [インストールガイド](../../installation/using/general-architecture.md)
* [非推奨（廃止予定）になった機能およびシステム](../../rn/using/deprecated-features.md)
* [ビルドアップグレード手順](https://helpx.adobe.com/jp/campaign/kb/acc-build-upgrade.html)
