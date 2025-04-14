---
product: campaign
title: Campaign Classic の互換性マトリックス
description: Campaign Classic 互換性マトリックス
feature: Release Notes
role: User
level: Beginner
exl-id: b8c1f287-06f4-4c34-8cca-b0c7676abbc2
source-git-commit: b8a6a0db27826309456c285c08d4f1d85de70283
workflow-type: ht
source-wordcount: '846'
ht-degree: 100%

---

# 互換性マトリックス {#compatibility-matrix}

Adobe Campaign Classic v7 の[最新ビルド](../../rn/using/latest-release.md)は、このページに記載されているすべてのシステムおよびツールと互換性があります。これらのサードパーティ製システムおよびツールの特定のバージョンが、それぞれの作成者による提供が終了した（EOL）場合、Adobe Campaign はこれらのバージョンとの互換性を失います。これらは以降の製品リリースで互換表から削除されます。問題を回避するため、この互換性マトリックスに記載されているサポート対象バージョンのシステムをご使用ください。非推奨の項目の詳細については、[このページ](../../rn/using/deprecated-features.md)を参照してください。

特に明記されていない限り、マイナーリリースはすべてサポートされています。

>[!CAUTION]
>
>このマトリックスは、新しいサポート対象システムやツールの追加、非推奨システムとツールの削除など、定期的に更新されます。

## オペレーティングシステム {#OperatingSystems}

オンプレミス／ハイブリッド環境のお客様は、次のオペレーティングシステムのいずれかに Adobe Campaign をインストールする必要があります。Campaign Classic v7 のインストール手順について詳しくは、[このページ](../../installation/using/application-server.md)を参照してください。

<table> 
<tbody> 
<td><strong>オペレーティングシステム</strong></td>
<td><strong>オペレーティングシステムのバージョン</strong></td>
<td><strong>最小 Campaign バージョン</strong></td>
<tr>
<td>
<p>Debian</p>
</td>
<td>
<p>11</p>
</td>
<td>
<p>v7.3</p>
<p></p>
</td>
</tr>
<tr>
<td>
<p>Red Hat Enterprise Linux（RHEL）</p>
</td>
<td>
<p>9.x</p>
<p>8.x</p>
<p>7.x</p>
</td>
<td>
<p>v7.4</p>
<p></p>
<p></p>
</td>
</tr>
<tr>
<td>
<p>Windows Server</p>
</td>
<td>
<p>2022</p>
<p>2019</p>
<p>2016</p>
</td>
<td>
<p>v7.4</p>
<p>v7.2</p>
<p></p>
</td>
</tr>
</tbody>
</table>

>[!IMPORTANT]
>
>RHEL を使用する場合は、[SELinux](../../installation/using/prerequisites-of-campaign-installation-in-linux.md#selinux) を無効にするか、アーキテクトにカスタム SELinux ルールを記述させ、有効にされた SELinux が Campaign 操作で問題を引き起こしていないことを確認する必要があります。

## web サーバー {#WebServers}

オンプレミス／ハイブリッド環境のお客様は、オペレーティングシステムに応じて、以下に示す web サーバーのいずれかと Campaign を統合する必要があります。Web サーバーの設定手順について詳しくは、[このページ](../../installation/using/integration-into-a-web-server-for-windows.md)（Windows の場合）と[このページ](../../installation/using/integration-into-a-web-server-for-linux.md)（Linux の場合）を参照してください。

<table>
<tbody>
<td><strong>Web サーバー</strong></td>
<td><strong>Web サーバーバージョン</strong></td>
<tr>
<td>
<p>Microsoft IIS</p>
</td>
<td>
<p>10.0</p>
</td>
</tr>
<tr>
<td>
<p>Apache</p>
</td>
<td>
<p>2.4</p>
</td>
</tr>
</tbody>
</table>

## ツール {#Tools}

オンプレミス／ハイブリッド環境のお客様は、以下に示すツールをインストールして設定する必要があります。[詳細情報](../../installation/using/application-server.md)。

<table>
<tbody>
<td><strong>ツール</strong></td>
<td><strong>バージョン</strong></td>
<td><strong>最小 Campaign バージョン</strong></td>
<tr>
<td><p>Java Development Kit（JDK）</p>
<p>詳しくは、<a href="../../installation/using/application-server.md#jdk" target="_blank">このページ</a>を参照してください。</p>
</td>
<td>
<p>17</p>
<p>11</p>
<p>9</p>
<p>8</p>
<p></p>
</td>
<td>
<p>v7.4.1 以降で必須</p>
<p>v7.4.1 以降で必須</p>
<p>v7.4.1 まで</p>
<p>v7.4.1 まで</p>
</tr>
<tr>
<td><p>Libre Office</p></td>
<td>
<p>7（お使いのシステムに埋め込まれている場合は以前のバージョン）</p>
</td>
<td>
<p></p>
</td>
</tr>
<tr>
<td><p>SpamAssassin</p></td>
<td>
<p>3.4.x</p>
</td>
<td>
<p></p>
</td>
</tbody>
</table>

## 関係データベース管理システム（RDBMS） {#RDBMSservers}

オンプレミス／ハイブリッド環境のお客様は、次のデータベースのいずれかをインストールして設定する必要があります。[詳細情報](../../installation/using/creating-and-configuring-the-database.md)。


<table>
<tbody>
<td><strong>データベースシステム</strong></td>
<td><strong>データベースのバージョン</strong></td>
<td><strong>最小 Campaign バージョン</strong></td>
<tr>
<td>
<p>Oracle</p>
</td>
<td>
<p>23c</p>
<p>21c</p>
<p>19c</p>
<p>18c</p>
<p>12c</p>
<p>11g R2</p>
</td>
<td>
<p>v7.4</p>
<p></p>
<p></p>
<p></p>
<p></p>
</td>
</tr>
<tr>
<td>
<p>PostgreSQL</p>
</td>
<td>
<p>14.x</p>
<p>13.x</p>
<p>12.x</p>
<p>11.x</p>
</td>
<td>
<p>v7.3.2</p>
<p></p>
<p></p>
<p></p>
</td>
</tr>
<tr>
<td>
<p>Microsoft SQL Server</p>
</td>
<td>
<p>2022</p>
<p>2019</p>
<p>2017</p>
<p>2016</p>
<p>2014</p>
</td>
<td>
<p>v7.4</p>
<p></p>
<p></p>
<p></p>
<p></p>
</td>
</tr>
</tbody>
</table>

>[!NOTE]
>
>* RDBMS ドライバは RDBMS サーバーのバージョンと一致する必要があります。
>
>* Linux で Campaign サーバーを実行している場合、プライマリデータベースとしての Microsoft SQL Server の使用はサポートされません。[詳細情報](../../installation/using/prerequisites-of-campaign-installation-in-linux.md#database-access-layers)。
>
>* 上記のバージョンで Amazon RDS for PostgreSQL を使用することもできます。
>
>* PostgreSQL はホスト／Managed Cloud Services 環境の RDBMS です。


## CRM コネクタ {#CRMconnectors}

Adobe Campaign と互換性のある顧客関係管理（CRM）システムを次に示します。 Campaign CRM コネクタの[詳細](../../platform/using/crm-connectors.md)を説明します。

<table>
<tbody>
<tr>
<td>
<p>Salesforce コネクタ API</p>
</td>
<td>
<p>API バージョン 49</p>
</td>
</tr>
<tr>
<td>
<p>Microsoft Dynamics コネクタ</p>
</td>
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
<td><strong>最小 Campaign バージョン</strong></td>
<tr>
<td>Amazon Redshift</td>
<td><p> </p>
<td>v7.0 19.1.4</td>
</td>
</tr>
<tr>
<td>Google BigQuery</td>
<td> </td>
<td>v7.2</td>
</tr>
<tr>
<td>PostgreSQL</td>
<td>
<p>14.x</p>
<p>13.x</p>
<p>12.x</p>
<p>11.x</p>
</td>
<td>v7.0 19.1.4</td>
</tr>
<tr>
<td>Snowflake</td>
<td> </td>
<td>v7.2</td>
</tr>
<tr>
<td>Vertica Analytics</td>
<td> </td>
<td>v7.0 19.1.4 </td>
</tr>
</tbody>
</table>

さらに、**ハイブリッド**&#x200B;環境および&#x200B;**オンプレミス**&#x200B;環境では、Campaign を次の外部データベースシステムとも接続できます。これらのシステムは Campaign **Managed Services**（ホスト）環境と&#x200B;**互換性がありません**。

<table>
<tbody>
<td><strong>データベースシステム</strong></td>
<td><strong>データベースのバージョン</strong></td>
<td><strong>最小 Campaign バージョン</strong></td>
<tr>
<td>Microsoft Azure Synapse Analytics</td>
<td> </td>
<td></td>
</tr>
<tr><td>MySQL</td>
<td>
<p>8</p>
<p>5.7</p>
</td>
<td>
<p>v7.3</p>
<p></p>
</td>
</tr>
<tr>
<td>Netezza</td>
<td>
<p>v7.2</p>
</td>
<td></td>
</tr>
<tr>
<td>Oracle</td>
<td>
<p>23c</p>
<p>21c</p>
<p>19c</p>
<p>18c</p>
<p>12c</p>
<p>11g</p>
</td>
<td>
<p>v7.4</p>
<p></p>
<p></p>
<p></p>
<p></p>
</td>
</tr>
<tr>
<td>SAP HANA</td>
<td>
<p>バージョン 1 SPS 12</p>
</td>
<td></td>
</tr>
<tr><td>SQL Server</td>
<td>
<p>2022（Campaign v7.4 以降）</p>
<p>2019</p>
<p>2017</p>
<p>2016</p>
<p>2014</p>
<p>2012 SP1 および SP2</p>
</td>
<td></td>
</tr>
<tr>
<td>Sybase</td>
<td>
<p>IQ 16</p>
<p>ASE 15.7</p>
</td>
<td></td>
</tr>
<tr>
<td>Teradata</td>
<td>
<p>17.x</p>
<p>16.x（最新バージョン）</p>
</td>
<td></td>
</tr>
<tr><td>HiveSQL による Hadoop</td>
<td>
<p>HortonWorks HDP 2.4.x、2.5.x、2.6.x</p>
<p>HDInsight 3.4（HDP 2.4）、3.5（HDP 2.5）、3.6（HDP 2.6）</p>
<p>Cloudera CDH6.x</p>
</td>
<td></td>
</tr>
</tbody>
</table>


## クライアントコンソール {#ClientOS}

[Campaign クライアントコンソール](../../installation/using/installing-the-client-console.md)を使用するには、次のオペレーティングシステムとブラウザーが&#x200B;**必要**&#x200B;です。

### オペレーティングシステム

<table>
<tbody>
<td><strong>システム</strong></td>
<td><strong>OS バージョン</strong></td>
<td><strong>最小 Campaign バージョン</strong></td>
<tr>
<td>Microsoft Windows</td>
<td>
<p>11</p>
<p>10</p>
</td>
<td>
<p>v7.3</p>
<p></p>
<p></p>
</tr>
<tr>
<td>Microsoft Windows Server</td>
<td>
<p>2022</p>
<p>2019</p>
<p>2016</p>
</td>
<td>
<p>v7.4.1</p>
<p>v7.2.1</p>
<p></p>
</tbody>
</table>

### Microsoft WebView2 ランタイム {#webview}

Microsoft Edge WebView2 ランタイムの最新バージョンは、Campaign クライアントコンソールに必須です。

[Microsoft Developer サイト](https://www.adobe.com/go/acc-ms-webview2-runtime-download_jp)から Microsoft Edge WebView2 をダウンロードします。


## Mobile SDK {#MobileSDK}

データ収集 UI で Adobe Campaign 拡張機能を設定することで、Adobe Experience Platform Mobile SDK 経由で Campaign を使用して[プッシュ通知を送信](../../delivery/using/about-mobile-app-channel.md)できます。

Campaign SDK は、Campaign v7.4 以降では[非推奨（廃止予定）](deprecated-features.md)となります。既存の実装を AEP Mobile SDK にスムーズに移行するために、以下のオペレーティングシステムでも引き続き使用できます<!--, using the associated [mobile SDK](../../delivery/using/integrating-campaign-sdk-into-the-mobile-application.md)-->。


<table>
<tbody>
<tr>
<td>Google Android</td>
<td>
<p>7～14</p>
<p>Mobile SDK ビルド 1.1.1 のサポート。</p>
<p>Android 13 および 14 は Campaign v7.4 以降でサポートされています。</p>
<p>Android 12 は Campaign v7.3 以降でサポートされています。</p>
</td>
</tr>
<tr>
<td>Apple iOS</td>
<td>
<p>iOS 9～17</p>
<p>Mobile SDK ビルド 1.0.26 のサポート。</p>
<p>Apple iOS 15 は Campaign v7.3 以降でサポートされています。 </p>
<p>Apple iOS 16 および 17 は Campaign v7.4 以降でサポートされています。</p>
</td>
</tr>
</tbody>
</table>

## ブラウザー {#Browsers}

最新バージョンの次のブラウザーは Campaign for [Web Access](../../campaign/using/accessing-marketing-campaigns.md#using-the-web-interface-) と互換性があります。

* Google Chrome
* Microsoft Edge
* Mozilla Firefox
* Safari



>[!MORELIKETHIS]
>
>* [Campaign Classic リリースノート](../../rn/using/latest-release.md)
>* [Campaign の一般的なアーキテクチャ](../../installation/using/general-architecture.md)
>* [ハードウェアサイズについての推奨事項](../../technotes/using/hardware-sizing.md)
>* [非推奨（廃止予定）になった機能およびシステム](../../rn/using/deprecated-features.md)
>* [ビルドアップグレード手順](../../production/using/build-upgrade.md)
