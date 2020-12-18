---
solution: Campaign Classic
product: campaign
title: アプリケーションサーバー
description: アプリケーションサーバー
audience: installation
content-type: reference
topic-tags: prerequisites-and-recommendations-
translation-type: tm+mt
source-git-commit: 972885c3a38bcd3a260574bacbb3f507e11ae05b
workflow-type: tm+mt
source-wordcount: '498'
ht-degree: 1%

---


# アプリケーションサーバー{#application-server}

必要なデータベースアクセスレイヤーをサーバーにインストールし、Adobe Campaignアカウントからアクセスできる必要があります。

## Java開発キット — JDK {#java-development-kit---jdk}

Dynamic Webページジェネレーターは、JSP 1.2テクノロジーを使用します。 この場合、（Apacheの）Tomcatエンジンがアプリケーションに含まれます。 Java開発キット(JDK)が必要です。JDKは、Adobe Campaignアプリケーションがインストールされているすべてのサーバーにインストールされます。

動的なWebページ(レポート、Web フォームなど)の生成に使用されるサーブレットコンテナApache Tomcatを組み込むので、Adobe Campaignアプリケーションサーバー（**nlserver web**&#x200B;プロセス）を実行するコンピューターにJDKをインストールする必要があります。

このアプリケーションは、**OpenJDK**&#x200B;と同様に、Oracleが開発したJava Development Kit(JDK)に対して承認されています。

サポートされるバージョンの詳細については、キャンペーン[互換表](../../rn/using/compatibility-matrix.md)を参照してください。

>[!NOTE]
>
>マシン上の他のアプリケーションで既に使用されている適切なJDKバージョンを使用してインストールできます。
>  
>をインストールする場合、ウェブブラウザとの統合を実行する必要はありません。
>
>配信エージェント（**nlserver mta**&#x200B;プロセス）またはワークフローサーバー（**nlserver wfserver**&#x200B;プロセス）のみを実行するマシンでは、JDKをインストールする必要はありません。

Java JDKをダウンロードするには、次に接続します。[https://www.oracle.com/technetwork/java/javase/downloads/index.html](https://www.oracle.com/technetwork/java/javase/downloads/index.html).

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

Linuxでは、OpenSSLをインストールする必要があります。 Adobe Campaignでサポートされるバージョンは、**OpenSSL 1.0.1**&#x200B;および&#x200B;**OpenSSL 0.9.8**&#x200B;です。 0.9.8g ～ 0.9.8oのサブバージョンも使用できます。

## レポートのエクスポート {#exporting-reports}

Adobe Campaignを使用すると、プラットフォームレポートをMicrosoft ExcelおよびAdobe PDF形式でエクスポートできます。 Microsoft Excel形式の場合、Adobe Campaignでは&#x200B;**LibreOffice**&#x200B;を使用します。 Adobe PDF形式の場合、Adobe Campaignは&#x200B;**PhantomJS**&#x200B;コンバーターを使用します。 PhantomJsはファクトリパッケージに含まれ、LibreOfficeは、Adobe Campaignアプリケーションサーバーが実行されるコンピューター（**nlserver web**&#x200B;プロセス）にインストールする必要があります。

>[!NOTE]
>
>Linuxの場合は、フォントを追加する必要があります。 詳しくは、[MTA統計用のフォント](../../installation/using/prerequisites-of-campaign-installation-in-linux.md#fonts-for-mta-statistics)を参照してください。

## SpamAssassin {#spamassassin}

SpamAssicinを使用すると、受信時に使用されるスパム対策ツールでメッセージが望ましくないと見なされる危険性があるかどうかを判断するために、電子メールにスコアを割り当てることができます。 インストールはオプションです。

SpamAssicinが望ましくない電子メールの認定は、完全にフィルターとスコアリングルールに基づいています。 したがって、SpamAssicinのインストールとAdobe Campaignへの統合が完全に機能し、送信前に配信に割り当てられたスコアの関連性を保証するために、これらのルールを少なくとも1日に1回更新する必要があります。 この更新は、SpamAssinをホストするサーバー管理者の責任です。

サポートされる最小バージョンは次のとおりです。**3.4**

SpamAssinにはHTTPインターネットアクセス(tcp/80)が必要です。

SpamAssinのインストールと設定の段階は、[SpamAssinの設定](../../installation/using/configuring-spamassassin.md)に記載されています。
