---
product: campaign
title: アプリケーションサーバー
description: アプリケーションサーバー
audience: installation
content-type: reference
topic-tags: prerequisites-and-recommendations-
exl-id: 87103c31-1530-4f8d-ab3a-6ff73093b80c
source-git-commit: 8794464d6fcc8ab648cd6866266855a701538fde
workflow-type: tm+mt
source-wordcount: '489'
ht-degree: 1%

---

# アプリケーションサーバー{#application-server}

![](../../assets/v7-only.svg)

必要なデータベースアクセスレイヤーをサーバーにインストールし、Adobe Campaignアカウントからアクセスできるようにする必要があります。

## Java 開発キット — JDK {#java-development-kit---jdk}

Dynamic Web ページジェネレーターは、JSP 1.2 テクノロジーを使用します。 この場合、（Apache の）Tomcat エンジンがアプリケーションに含まれます。 Java Development Kit(JDK) が必要です。JDK は、Adobe Campaignアプリケーションがインストールされているすべてのサーバーにインストールされています。

まず、Adobe Campaignアプリケーションサーバー (**nlserver web** プロセスを通じて ) を書き込む必要があります。

oracleが開発した Java Development Kit(JDK) および **OpenJDK**.

サポート対象バージョンについて詳しくは、 Campaign を参照してください。 [互換性マトリックス](../../rn/using/compatibility-matrix.md).

>[!NOTE]
>
>マシン上の他のアプリケーションで既に使用されている適切な JDK バージョンを使用してインストールできます。
>  
>インストール時に、Web ブラウザーとの統合を実行する必要はありません。
>
>配信エージェント (**nlserver mta** プロセス ) またはワークフローサーバー (**nlserver wfserver** プロセス )、JDK のインストールは必要ありません。

Java JDK をダウンロードするには、次に接続します。 [https://www.oracle.com/technetwork/java/javase/downloads/index.html](https://www.oracle.com/technetwork/java/javase/downloads/index.html).

**警告：JRE ではなく、JDK をダウンロードする必要があります。**

>[!CAUTION]
>
>プラットフォームの動作パフォーマンスを維持し、インストールされているバージョンとの互換性を確保するには、Windows および Linux で自動 JDK 更新機能を無効にする必要があります。

Linux 環境に JDSL をインストールするには、パッケージマネージャーを使用することをお勧めします。

Debian 8 および 9 で、次のコマンドを使用します。

```
aptitude install openjdk-8-jdk
```

RHEL 7 の場合は、次のコマンドを使用します。

```
yum install java-1.8.0-openjdk
```

## OpenSSL {#openssl}

Linux では、OpenSSL をインストールする必要があります。 Adobe Campaignは、OpenSSL バージョン 1.0.2 以降をサポートしています。

## レポートのエクスポート {#exporting-reports}

Adobe Campaignでは、プラットフォームレポートをMicrosoft Excel およびAdobe PDF形式で書き出すことができます。 Microsoft Excel 形式の場合、Adobe Campaignは **LibreOffice**. Adobe PDF形式の場合、Adobe Campaignは **PhantomJS** コンバータ。 PhantomJs がファクトリパッケージに含まれており、Adobe Campaignアプリケーションサーバーが実行されるマシン ( ) に LibreOffice をインストールする必要があります。**nlserver web** プロセス )。

>[!NOTE]
>
>Linux の場合は、フォントを追加する必要があります。 詳しくは、 [MTA 統計用のフォント](../../installation/using/prerequisites-of-campaign-installation-in-linux.md#fonts-for-mta-statistics).

## SpamAssassin {#spamassassin}

SpamAssassin を使用すると、E メールにスコアを割り当てて、受信時に使用されるスパム対策ツールによって、メッセージが望ましくないと見なされるリスクがあるかどうかを判断できます。 インストールはオプションです。

SpamAssassin によって望ましくない電子メールの選定は、完全にフィルタリングとスコア付けルールに基づいています。 したがって、SpamAssassin のインストールとAdobe Campaignへの統合が完全に機能し、送信前に配信に割り当てられたスコアの関連性を保証するために、これらのルールを少なくとも 1 日に 1 回更新する必要があります。 この更新は、SpamAssassin をホストするサーバー管理者の責任です。

サポートされている最小バージョンは次のとおりです。 **3.4**

SpamAssassin には、HTTP インターネットアクセス (tcp/80) が必要です。

SpamAssassin のインストールおよび設定ステージについては、 [SpamAssassin の設定](../../installation/using/configuring-spamassassin.md).
