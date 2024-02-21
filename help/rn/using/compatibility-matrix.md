---
product: campaign
title: Campaign Classic の互換性マトリックス
description: Campaign Classic 互換性マトリックス
feature: Release Notes
badge-v7-only: label="v7" type="Informative" tooltip="Campaign Classic v7 にのみ適用されます"
role: User
level: Beginner
exl-id: b8c1f287-06f4-4c34-8cca-b0c7676abbc2
source-git-commit: 668cee663890fafe27f86f2afd3752f7e2ab347a
workflow-type: tm+mt
source-wordcount: '805'
ht-degree: 96%

---

# 互換性マトリックス{#compatibility-matrix}



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
<p>8.x（ハイブリッド環境の場合のみ）</p>
<p>7.x</p>
<p><strong>重要</strong>：RHEL を使用する場合は、SELinux を無効にするか、アーキテクトにカスタム SELinux ルールを記述させ、有効にされた SELinux が Campaign 操作で問題を引き起こしていないことを確認する必要があります。</p>
</td>
</tr>
<tr>
<td>Debian</td>
<td>
<p>11（Campaign v7.3 以降）</p>
<p>10</p>
</td>
</tr>
<tr>
<td>RHEL</td>
<td>
<p>8.x</p>
<p>7.x</p>
<p><strong>重要</strong>：RHEL を使用する場合は、SELinux を無効にするか、アーキテクトにカスタム SELinux ルールを記述させ、有効にされた SELinux が Campaign 操作で問題を引き起こしていないことを確認する必要があります。</p>
</td>
</tr>
<tr>
<td>Windows Server</td>
<td>
<p>2019（Campaign v7.2 以降）</p>
<p>2016</p>
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
<p>Windows Server 2016 および 2019 上の 10.0</p>
</td>
</tr>
<tr>
<td>Apache</td>
<td>
<p>RHEL7 - CentOS 7、Debian 8/9、Windows 向けの 2.4</p>
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
<p>Campaign は、Oracle が開発した Java Development Kit（JDK）と、OpenJDK をサポートしています。</p>
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
<p>14.x（Campaign v7.3.2 以降）</p>
<p>13.x</p>
<p>12.x</p>
<p>11.x</p>
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
<p><strong>重要：</strong>Linux で Campaign サーバーを実行している場合、プライマリデータベースとしての Microsoft SQL Server の使用はサポートされません。<a href="https://experienceleague.adobe.com/docs/campaign-classic/using/installing-campaign-classic/install-campaign-on-prem/installing-campaign-in-linux/prerequisites-of-campaign-installation-in-linux.html#database-access-layers">詳細情報</a>。</p>
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
<td>Amazon Redshift</td>
<td><p> </p>
<td>v7.0 19.1.4 以上</td>
</td>
</tr>
<tr>
<td>Google BigQuery</td>
<td> </td>
<td>7.2 以上</td>
</tr>
<tr>
<td>PostgreSQL</td>
<td>
<p>14.x</p>
<p>13.x</p>
<p>12.x</p>
<p>11.x</p>
</td>
<td>v7.0 19.1.4 以上</td>
</tr>
<tr>
<td>Snowflake</td>
<td> </td>
<td>7.2 以上</td>
</tr>
<tr>
<td>Vertica Analytics</td>
<td> </td>
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
<td>Microsoft Azure Synapse Analytics</td>
<td> </td>
<td>v7.0 19.1.4 以上</td>
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
<td>Netezza</td>
<td>
<p>7.2</p>
</td>
<td>v7.0 以上</td>
</tr>
<tr>
<td>Oracle</td>
<td>
<p>19c</p>
<p>18c</p>
<p>12c</p>
<p>11g</p>
</td>
<td>
<p>v7.0 以上</p>
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
<tr>
<td>Sybase</td>
<td>
<p>IQ 16</p>
<p>ASE 15.7</p>
</td>
<td>v7.0 以上</td>
</tr>
<tr>
<td>Teradata</td>
<td>
<p>17.x</p>
<p>16.x（最新バージョン）</p>
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
<td><strong>システム</strong></td>
<td><strong>OS バージョン</strong></td>
<td><strong>Campaign のバージョン</strong></td>
<tr>
<td>Microsoft Windows</td>
<td>
<p>11</p>
<p>10</p>
</td>
<td>
<p>v7.3 以上</p>
<p></p>
<p></p>
</tr>
<tr>
<td>Microsoft Windows Server</td>
<td>
<p>2019</p>
<p>2016</p>
</td>
<td>
<p>v7.2.1 以上</p>
<p></p>
<p></p>
</tbody>
</table>

### Microsoft WebView2 ランタイム

Microsoft Edge WebView2 ランタイムの最新バージョンは、Campaign クライアントコンソールに必須です。

[Microsoft Developer サイト](https://www.adobe.com/go/acc-ms-webview2-runtime-download_jp)から Microsoft Edge WebView2 をダウンロードします。


## Mobile SDK{#MobileSDK}

以下に示すオペレーティングシステムでは、関連する [Mobile SDK](../../delivery/using/integrating-campaign-sdk-into-the-mobile-application.md) を使用して、Campaign を使用して[プッシュ通知を送信](../../delivery/using/about-mobile-app-channel.md)できます。

データ収集 UI で Adobe Campaign 拡張機能を設定することで、Adobe Experience Platform Mobile SDK を使用することもできます。

<table>
<tbody>
<tr>
<td>Google Android</td>
<td>
<p>12（Campaign v7.3 以降）、9.0、8.x、7.x</p>
<p>（モバイル SDK ビルド 1.1.1 を使用）</p>
</td>
</tr>
<tr>
<td>Apple iOS</td>
<td>
<p>iOS 9～15</p>
<p>（32 ビットおよび 64 ビットバージョンと互換性のあるモバイル SDK ビルド 1.0.26 を使用）iOS 15 は Campaign v7.3 以降でサポートされています</p>
</td>
</tr>
</tbody>
</table>

## ブラウザー{#Browsers}

最新バージョンの次のブラウザーは Campaign for [Web Access](../../campaign/using/accessing-marketing-campaigns.md#using-the-web-interface-) と互換性があります。

* Google Chrome
* Microsoft Edge
* Mozilla Firefox
* Safari



## その他の関連リソース{#Morelikethis}

* [Campaign Classic リリースノート](../../rn/using/latest-release.md)
* [Campaign の一般的なアーキテクチャ](../../installation/using/general-architecture.md)
* [ハードウェアサイズについてのレコメンデーション](../../technotes/using/hardware-sizing.md)
* [非推奨（廃止予定）の機能およびシステム](../../rn/using/deprecated-features.md)
* [ビルドアップグレード手順](../../production/using/build-upgrade.md)
