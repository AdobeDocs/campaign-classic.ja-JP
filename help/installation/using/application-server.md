---
title: アプリケーションサーバー
seo-title: アプリケーションサーバー
description: アプリケーションサーバー
seo-description: null
page-status-flag: never-activated
uuid: 837c6a5c-53a4-4d1b-a084-9cf77e7a0eee
contentOwner: sauviat
products: SG_CAMPAIGN/CLASSIC
audience: installation
content-type: reference
topic-tags: prerequisites-and-recommendations-
discoiquuid: 7a9e028c-255d-4aad-9827-d19f9a7897b2
index: y
internal: n
snippet: y
translation-type: tm+mt
source-git-commit: 46f5bfb41bfe9c938ac0ffa767ead3e47a32047d

---


# Application server{#application-server}

必要なデータベースアクセスレイヤーがサーバーにインストールされ、Adobe Campaignアカウントからアクセスできる必要があります。

## Java開発キット — JDK {#java-development-kit---jdk}

動的WebページジェネレーターはJSP 1.2テクノロジーを使用します。 この場合、（Apacheからの）Tomcatエンジンがアプリケーションに含まれます。 Adobe CampaignアプリケーションがインストールされているすべてのサーバーにJava開発キット(JDK)がインストールされている必要があります。

動的なWebページ（レポート、Webフォームなど）の生成に使用するサーブレットコンテナApache tomcatが組み込まれているので、Adobe Campaignアプリケーションサーバー(**nlserver webプロセス** )を実行するコンピューターにJDKをインストールする必要があります。

アプリケーションは、Oracleが開発したJava開発キット(JDK)および **OpenJDKに対して承認されています**。

The supported versions are detailed in the [Compatibility matrix](https://helpx.adobe.com/campaign/kb/compatibility-matrix.html).

>[!NOTE]
>
>マシン上の他のアプリケーションで既に使用されている適切なJDKバージョンを使用してインストールできます。
>  
>インストール時に、ウェブブラウザとの統合を実行する必要はありません。
>
>配信エージェント(**nlserver mta** process)またはワークフローサーバー(nlserver wfserver **** process)のみを実行するマシンでは、JDKをインストールする必要はありません。

Java JDKをダウンロードするには、次に接続します。https://www.oracle.com/technetwork/java/javase/downloads/index.html [](https://www.oracle.com/technetwork/java/javase/downloads/index.html).

**警告：jreではなくJDKをダウンロードする必要があります。**

>[!CAUTION]
>
>プラットフォームの動作パフォーマンスを維持し、インストールされているバージョンとの互換性を確保するには、WindowsおよびLinuxで自動JDK更新機能を無効にする必要があります。

Linux環境にJDSLをインストールするには、パッケージマネージャーを使用することをお勧めします。

Debian 7および8では、次のコマンドを使用します。

```
aptitude install openjdk-7-jdk
```

RHEL 6の場合は、次のコマンドを使用します。

```
yum install java-1.8.0-openjdk
```

RHEL 7の場合は、次のコマンドを使用します。

```
yum install java-1.8.0-openjdk
```

## OpenSSL {#openssl}

Linuxでは、OpenSSLをインストールする必要があります。 Adobe Campaignでサポートされているバー **ジョンはOpenSSL 1.0.1** 、 **OpenSSL 0.9.8です**。 サブバージョン0.9.8g ～ 0.9.8oも使用できます。

>[!NOTE]
>
>RHEL 6およびCentOS 6の場合は、openSSL 1.0が必要です。

## レポートのエクスポート {#exporting-reports}

Adobe Campaignを使用すると、プラットフォームレポートをMicrosoft excelおよびAdobe PDF形式でエクスポートできます。 Microsoft excel形式の場合、Adobe CampaignではLibreOfficeが使用さ **れます**。 Adobe PDF形式の場合、Adobe Campaignは **PhantomJS** Converterを使用します。 PhantomJsはファクトリパッケージに含まれ、Adobe Campaignアプリケーションサーバーが実行されるコンピューター(**nlserver webプロセス** )にLibreOfficeがインストールされている必要があります。

>[!NOTE]
>
>Linuxの場合は、フォントを追加する必要があります。 詳しくは、「MTA統計用のフォン [ト」を参照してください](../../installation/using/prerequisites-of-campaign-installation-in-linux.md#fonts-for-mta-statistics)。

## SpamAssassin {#spamassassin}

SpamAssacinを使用すると、受信時に使用するスパム対策ツールによってメッセージのリスクが望ましくないと見なされるかどうかを判断するために、電子メールにスコアを割り当てることができます。 インストールはオプションです。

SpamAssacsinが望ましくない電子メールの資格は、完全にフィルタリングとスコアリングルールに基づいています。 したがって、SpamAssacsinのインストールとAdobe Campaignへの統合が完全に機能し、送信前に配信に割り当てられたスコアの関連性を保証するには、これらのルールを少なくとも1日に1回更新する必要があります。 この更新は、SpamAssacinをホストするサーバー管理者の責任です。

サポートされる最小バージョンは次のとおりです。 **3.2.5** と **3.3.2**。

SpamAssacinにはHTTPインターネットアクセス(tcp/80)が必要です。

SpamAssacsinのインストールおよび設定ステージは、SpamAssinの設定に [記載されています](../../installation/using/configuring-spamassassin.md)。
