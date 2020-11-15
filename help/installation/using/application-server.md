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
translation-type: tm+mt
source-git-commit: 99d766cb6234347ea2975f3c08a6ac0496619b41
workflow-type: tm+mt
source-wordcount: '500'
ht-degree: 2%

---


# アプリケーションサーバー{#application-server}

必要なデータベースアクセスレイヤーをサーバーにインストールし、Adobe Campaignアカウントからアクセスできる必要があります。

## Java Development Kit - JDK {#java-development-kit---jdk}

Dynamic Webページジェネレーターは、JSP 1.2テクノロジーを使用します。 この場合、（Apacheの）Tomcatエンジンがアプリケーションに含まれます。 Java開発キット(JDK)が必要です。JDKは、Adobe Campaignアプリケーションがインストールされているすべてのサーバーにインストールされます。

JDKは、動的なWebページ(レポート、Web フォームなど)の生成に使用するサーブレットコンテナApache Tomcatを組み込んでいるので、Adobe Campaignアプリケーションサーバー(**nlserver web** process)を実行するコンピューターに最初にインストールする必要があります。

The application has been approved for the Java Development Kit (JDK) developed by Oracle as well as for **OpenJDK**.

The supported versions are detailed in Campaign [Compatibility matrix](../../rn/using/compatibility-matrix.md).

>[!NOTE]
>
>マシン上の他のアプリケーションで既に使用されている適切なJDKバージョンを使用してインストールできます。
>  
>をインストールする場合、ウェブブラウザとの統合を実行する必要はありません。
>
>配信エージェント(**nlserver mta** process)またはワークフローサーバー(nlserver wfserver **** process)のみを実行するマシンでは、JDKをインストールする必要はありません。

Java JDKをダウンロードするには、次に接続します。 [https://www.oracle.com/technetwork/java/javase/downloads/index.html](https://www.oracle.com/technetwork/java/javase/downloads/index.html).

**警告：JREではなくJDKをダウンロードする必要があります。**

>[!CAUTION]
>
>プラットフォームの動作パフォーマンスを維持し、インストールされているバージョンとの互換性を確保するには、WindowsおよびLinuxで自動JDK更新機能を無効にする必要があります。

JDSLをLinux環境にインストールするには、パッケージマネージャーを使用することをお勧めします。

Debian 8および9では、次のコマンドを使用します。

```
aptitude install openjdk-8-jdk
```

RHEL 7の場合は、次のコマンドを使用します。

```
yum install java-1.8.0-openjdk
```

## OpenSSL {#openssl}

Linuxでは、OpenSSLをインストールする必要があります。 Adobe CampaignでサポートされているバージョンはOpenSSL **1.0.1** と **OpenSSL 0.9.8**&#x200B;です。 0.9.8g ～ 0.9.8oのサブバージョンも使用できます。

## レポートのエクスポート {#exporting-reports}

Adobe Campaignを使用すると、プラットフォームレポートをMicrosoft ExcelおよびAdobe PDF形式でエクスポートできます。 Microsoft Excel形式の場合、Adobe CampaignではLibreOffice **を使用します**。 Adobe PDF形式の場合、Adobe CampaignはPhantomJS **** コンバーターを使用します。 PhantomJsはファクトリパッケージに含まれ、LibreOfficeは、Adobe Campaignアプリケーションサーバーが実行されるコンピューター(**nlserver web** process)にインストールする必要があります。

>[!NOTE]
>
>Linuxの場合は、フォントを追加する必要があります。 詳しくは、「MTA統計用の [フォント](../../installation/using/prerequisites-of-campaign-installation-in-linux.md#fonts-for-mta-statistics)」を参照してください。

## SpamAssassin {#spamassassin}

SpamAssicinを使用すると、受信時に使用されるスパム対策ツールでメッセージが望ましくないと見なされる危険性があるかどうかを判断するために、電子メールにスコアを割り当てることができます。 インストールはオプションです。

SpamAssicinが望ましくない電子メールの認定は、完全にフィルターとスコアリングルールに基づいています。 したがって、SpamAssicinのインストールとAdobe Campaignへの統合が完全に機能し、送信前に配信に割り当てられたスコアの関連性を保証するために、これらのルールを少なくとも1日に1回更新する必要があります。 この更新は、SpamAssinをホストするサーバー管理者の責任です。

サポートされる最小バージョンは次のとおりです。 **3.4**

SpamAssinにはHTTPインターネットアクセス(tcp/80)が必要です。

SpamAssinのインストールおよび設定ステージは、SpamAssinの [設定で説明しています](../../installation/using/configuring-spamassassin.md)。
