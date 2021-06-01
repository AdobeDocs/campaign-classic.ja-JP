---
product: campaign
title: アプリケーションサーバー
description: アプリケーションサーバー
audience: installation
content-type: reference
topic-tags: prerequisites-and-recommendations-
exl-id: 87103c31-1530-4f8d-ab3a-6ff73093b80c
source-git-commit: 98d646919fedc66ee9145522ad0c5f15b25dbf2e
workflow-type: tm+mt
source-wordcount: '498'
ht-degree: 1%

---

# アプリケーションサーバー{#application-server}

必要なデータベースアクセスレイヤーをサーバーにインストールし、Adobe Campaignアカウントからアクセスできるようにする必要があります。

## Java開発キット — JDK {#java-development-kit---jdk}

Dynamic Webページジェネレーターは、JSP 1.2テクノロジーを使用します。 このため、（Apacheの）Tomcatエンジンがアプリケーションに含まれます。 Adobe CampaignアプリケーションがインストールされているすべてのサーバーにJava開発キット(JDK)がインストールされている必要があります。

Adobe Campaignアプリケーションサーバー（**nlserver web**&#x200B;プロセス）を実行するコンピューターにJDKをインストールする必要があります。これは、動的Webページ（レポート、Webフォームなど）の生成に使用するサーブレットコンテナApache Tomcatが組み込まれているからです。

oracleが開発したJava Development Kit(JDK)と&#x200B;**OpenJDK**&#x200B;に対して、アプリケーションが承認されました。

サポートされるバージョンについて詳しくは、Campaign [互換性マトリックス](../../rn/using/compatibility-matrix.md)を参照してください。

>[!NOTE]
>
>マシン上の他のアプリケーションで既に使用されている適切なJDKバージョンを使用してインストールできます。
>  
>インストール時に、Webブラウザーとの統合を実行する必要はありません。
>
>配信エージェント（**nlserver mta**&#x200B;プロセス）またはワークフローサーバー（**nlserver wfserver**&#x200B;プロセス）のみを実行するマシンでは、JDKをインストールする必要はありません。

Java JDKをダウンロードするには、次のURLに接続します。[https://www.oracle.com/technetwork/java/javase/downloads/index.html](https://www.oracle.com/technetwork/java/javase/downloads/index.html).

**警告：JREではなく、JDKをダウンロードする必要があります。**

>[!CAUTION]
>
>プラットフォームの動作パフォーマンスを維持し、インストールされたバージョンとの互換性を確保するには、WindowsおよびLinuxで自動JDK更新機能を無効にする必要があります。

Linux環境にJDSLをインストールするには、パッケージマネージャーを使用することをお勧めします。

Debian 8および9では、次のコマンドを使用します。

```
aptitude install openjdk-8-jdk
```

RHEL 7の場合は、次のコマンドを使用します。

```
yum install java-1.8.0-openjdk
```

## OpenSSL {#openssl}

Linuxでは、OpenSSLをインストールする必要があります。 Adobe Campaignでサポートされているバージョンは&#x200B;**OpenSSL 1.0.1**&#x200B;と&#x200B;**OpenSSL 0.9.8**&#x200B;です。 サブバージョン0.9.8g～0.9.8oが受け入れられます。

## レポートのエクスポート {#exporting-reports}

Adobe Campaignでは、プラットフォームレポートをMicrosoft ExcelおよびAdobe PDF形式で書き出すことができます。 Microsoft Excel形式の場合、Adobe Campaignは&#x200B;**LibreOffice**&#x200B;を使用します。 Adobe PDF形式の場合、Adobe Campaignは&#x200B;**PhantomJS**&#x200B;コンバーターを使用します。 PhantomJsはファクトリパッケージに含まれ、Adobe Campaignアプリケーションサーバーが実行されるマシン（**nlserver web**&#x200B;プロセス）にLibreOfficeをインストールする必要があります。

>[!NOTE]
>
>Linuxの場合は、フォントを追加する必要があります。 詳しくは、[MTA統計のフォント](../../installation/using/prerequisites-of-campaign-installation-in-linux.md#fonts-for-mta-statistics)を参照してください。

## SpamAssassin {#spamassassin}

SpamAssassinを使用すると、受信時に使用されるスパム対策ツールによってメッセージのリスクが望ましくないと見なされるかどうかを判断するために、Eメールにスコアを割り当てることができます。 インストールはオプションです。

SpamAssassinによって望ましくないEメールの認定は、完全にフィルタリングとスコアルールに基づいています。 したがって、SpamAssassinのインストールとAdobe Campaignへの統合が完全に機能し、送信前に配信に割り当てられたスコアの関連性を保証するために、これらのルールを少なくとも1日に1回更新する必要があります。 この更新は、SpamAssassinをホストするサーバー管理者の責任です。

サポートされている最小バージョンは次のとおりです。**3.4**

SpamAssassinにはHTTPインターネットアクセス(tcp/80)が必要です。

SpamAssassinのインストールおよび設定ステージについては、[SpamAssassinの設定](../../installation/using/configuring-spamassassin.md)で説明しています。
