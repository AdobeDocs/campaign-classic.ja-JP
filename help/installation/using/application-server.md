---
product: campaign
title: アプリケーションサーバー
description: アプリケーションサーバー
feature: Installation
badge-v7-prem: label="オンプレミス／ハイブリッドのみ" type="Caution" url="https://experienceleague.adobe.com/docs/campaign-classic/using/installing-campaign-classic/architecture-and-hosting-models/hosting-models-lp/hosting-models.html?lang=ja" tooltip="オンプレミスデプロイメントとハイブリッドデプロイメントにのみ適用されます"
audience: installation
content-type: reference
topic-tags: prerequisites-and-recommendations-
exl-id: 87103c31-1530-4f8d-ab3a-6ff73093b80c
source-git-commit: 7e1c3b256cf43232e49d9daa0bf44d1e114b565b
workflow-type: tm+mt
source-wordcount: '622'
ht-degree: 3%

---

# アプリケーションサーバー{#application-server}

必要なデータベースアクセスレイヤーは、サーバーにインストールされ、Adobe Campaign アカウントからアクセスできる必要があります。

## Java Development Kit - JDK {#java-development-kit---jdk}

Java Development Kit、または JDK は、ソフトウェア開発キットです。 これは、Java アプリケーションと Java アプレットの開発を可能にする基盤コンポーネントです。

動的 Web ページジェネレーターでは、JSP 1.2 テクノロジーを使用します。 このために、（Apache からの） Tomcat エンジンがアプリケーションに含まれています。 これには、Adobe Campaign アプリケーションがインストールされているすべてのサーバーにインストールされている Java Development Kit （JDK）が必要です。

最初に、Adobe Campaign Application Server （**nlserver web** プロセス）を使用する必要があります。これには、動的な web ページ（レポート、web フォームなど）の生成に使用されるサーブレットコンテナ Apache Tomcat が組み込まれています。

このアプリケーションは、Oracleで開発された Java Development Kit （JDK）および **OpenJDK**.

サポートされているバージョンについて詳しくは、Campaign を参照してください。 [互換性マトリックス](../../rn/using/compatibility-matrix.md).


### 推奨事項

Java 開発キットをインストールしてアップグレードする際は、次の推奨事項を適用してください。

* Java Development Kit は、マシン上の他のアプリケーションですでに使用されている適切な JDK バージョンを使用してインストールできます。

* JDK をインストールする場合、web ブラウザーとの統合は必要ありません。

* 配信エージェントのみを実行するマシン（**nlserver mta** プロセス）またはワークフローサーバー（**nlserver wfserver** プロセス）を選択する場合は、JDK のインストールは必要ありません。

* プラットフォームの操作パフォーマンスを維持し、インストールされているバージョンとの互換性を確保するには、Windows と Linux で JDK の自動アップデート機能を無効にする必要があります。

* Java バージョンをアップグレードする場合、まず以前のバージョンをアンインストールする必要があります。 同じマシンにインストールされた両方のバージョンの Java は、競合を引き起こす可能性があります。

  オンプレミス環境のお客様は、 `LD_LIBRARY_PATH` [環境変数](installing-packages-with-linux.md#environment-variables) は最新バージョンに設定されています（例： java11）。 以前のバージョンに設定されている場合（例： Java8）を使用する場合は、更新する必要があります。 JDK 11 の場合、JDK ライブラリを探すパスはです。 `/usr/lib/jvm/java-11-openjdk-amd64/lib`.


### インストール手順

Java 開発キットはプラットフォーム固有であり、オペレーティングシステムごとに個別のインストーラーが必要です。

JDK をダウンロードするには、に接続します。 [Oracleの web サイト](https://www.oracle.com/technetwork/java/javase/downloads/index.html){target="_blank"}.

>[!CAUTION]
>
> Java ランタイム環境（JRE）ではなく、Java Development Kit （JDK）をダウンロードします。


Linux 環境に JDSL をインストールする場合、Adobeではパッケージマネージャーを使用することをお勧めします。

Debian の場合は、次のコマンドを使用します。

```sql
aptitude install openjdk-8-jdk
```

RHEL の場合は、次のコマンドを使用します。

```sql
yum install java-1.8.0-openjdk
```


## OpenSSL {#openssl}

Linux では、OpenSSL をインストールする必要があります。 Adobe Campaignは、OpenSSL バージョン 1.0.2 以降をサポートしています。

## レポートを書き出し {#exporting-reports}

Adobe Campaignを使用すると、レポートをMicrosoft Excel およびAdobe PDFに書き出すことができます。

* Microsoft Excel 形式の場合、Adobe Campaignはを利用します **LibreOffice**.

* Adobe PDF形式の場合、Adobe Campaignは次を使用します **PhantomJS** コンバータ。 PhantomJs はファクトリパッケージに含まれており、Adobe Campaign アプリケーションサーバーを実行する（**nlserver web** プロセス）。

>[!NOTE]
>
>Linux の場合、フォントを追加する必要があります。 詳しくは、次を参照してください [MTA 統計のフォント](../../installation/using/prerequisites-of-campaign-installation-in-linux.md#fonts-for-mta-statistics).

## SpamAssassin {#spamassassin}

SpamAssassin を使用すると、受信で使用されるスパム対策ツールでメッセージが望ましくないと見なされるリスクがあるかどうかを判断するために、メールにスコアを割り当てることができます。 インストールはオプションです。

SpamAssassin によって望ましくないものとしてメールが選定されるかどうかは、完全にフィルタリングおよびスコアルールに基づいています。 したがって、SpamAssassin のインストールとAdobe Campaignへの統合が完全に機能し、送信前に配信に割り当てられたスコアの関連性を保証するには、これらのルールを 1 日に 1 回以上更新する必要があります。 この更新は、SpamAssassin をホストするサーバー管理者の責任です。

サポートされている最小バージョンは次のとおりです。 **3.4**

SpamAssassin には HTTP インターネットアクセス （tcp/80）が必要です。

SpamAssassin のインストール段階と設定段階については、以下を参照してください。 [SpamAssassin の設定](../../installation/using/configuring-spamassassin.md).
