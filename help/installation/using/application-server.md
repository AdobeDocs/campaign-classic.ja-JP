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
source-git-commit: 0ed70b3c57714ad6c3926181334f57ed3b409d98
workflow-type: tm+mt
source-wordcount: '649'
ht-degree: 2%

---

# アプリケーションサーバー{#application-server}

必要なデータベースアクセスレイヤーは、サーバーにインストールされ、Adobe Campaign アカウントからアクセスできる必要があります。

## Java Development Kit - JDK {#jdk}

Java Development Kit、または JDK は、ソフトウェア開発キットです。 これは、Java アプリケーションと Java アプレットの開発を可能にする基盤コンポーネントです。

動的 Web ページジェネレーターでは JSP テクノロジーを使用します。 このために、（Apache からの） Tomcat エンジンがアプリケーションに含まれています。 これには、Adobe Campaign アプリケーションがインストールされているすべてのサーバーにインストールされている Java Development Kit （JDK）が必要です。

最初に、Adobe Campaign アプリケーションサーバー（**nlserver web** プロセス）を実行するコンピューターに JDK をインストールする必要があります。これは、このプロセスが、動的 web ページ（レポート、web フォームなど）の生成に使用される、サーブレットコンテナである Apache Tomcat を組み込んでいるからです。

oracleが開発した Java Development Kit （JDK）と、**OpenJDK** の使用が承認されています。

サポートされているバージョンについて詳しくは、Campaign[&#x200B; 互換性マトリックス &#x200B;](../../rn/using/compatibility-matrix.md) を参照してください。


>[!AVAILABILITY]
>
>* v7.4.1 以降、Campaign には **Java JDK 11** 以降が必要です。 Campaign サーバーが Windows 環境にインストールされている場合、Java ランタイム（JRE）は自動的には検出されなくなります。 JRE_HOME 環境変数は、Campaign が `bin/server/jvm.dll` ファイルを検索できるフォルダーに設定されている必要があります。 例えば、JDK 11 が `C:\Program Files\Java\jdk-11` フォルダーの下にインストールされている場合、JRE_HOME は `C:\Program Files\Java\jdk-11` である必要があります。
>
>* v7.4.1 以降、Tomcat 10.1 がデフォルトバージョンです。
>

### 推奨事項

Java 開発キットをインストールしてアップグレードする際は、次の推奨事項を適用してください。

* Java Development Kit は、マシン上の他のアプリケーションですでに使用されている適切な JDK バージョンを使用してインストールできます。

* JDK をインストールする場合、web ブラウザーとの統合は必要ありません。

* 配信エージェント（**nlserver mta** プロセス）またはワークフローサーバー（**nlserver wfserver** プロセス）のみを実行するマシンでは、JDK をインストールする必要はありません。

* Java バージョンをアップグレードする場合、まず以前のバージョンをアンインストールする必要があります。 同じマシンにインストールされた両方のバージョンの Java は、競合を引き起こす可能性があります。

  オンプレミス環境のお客様は、`LD_LIBRARY_PATH` [&#x200B; 環境変数 &#x200B;](installing-packages-with-linux.md#environment-variables) が最新バージョンに設定されていることを確認できます（例： java11）。 以前のバージョンに設定されている場合（例： Java8）を使用する場合は、更新する必要があります。 JDK 11 の場合、JDK ライブラリを見つけるパスは `/usr/lib/jvm/java-11-openjdk-amd64/lib` です。


### インストール手順

Java 開発キットはプラットフォーム固有であり、オペレーティングシステムごとに個別のインストーラーが必要です。

JDK をダウンロードするには、[Oracle web サイト &#x200B;](https://www.oracle.com/technetwork/java/javase/downloads/index.html){target="_blank"} に接続します。

>[!CAUTION]
>
> Java ランタイム環境（JRE）ではなく、Java Development Kit （JDK）をダウンロードします。


Linux 環境に JDSL をインストールする場合、Adobeではパッケージマネージャーを使用することをお勧めします。

Debian の場合は、次のコマンドを使用します。

```sql
apt install openjdk-11-jdk-headless
```

RHEL の場合は、次のコマンドを使用します。

```sql
dnf install java-11-openjdk-headless
```



## レポートを書き出し {#exporting-reports}

Adobe Campaignを使用すると、レポートをMicrosoft Excel およびAdobe PDFに書き出すことができます。

* Microsoft Excel 形式の場合、Adobe Campaignは **LibreOffice** に依存します。

* Adobe PDF形式の場合、Adobe Campaignは **PhantomJS** コンバーターを使用します。 PhantomJs はファクトリパッケージに含まれており、Adobe Campaign アプリケーションサーバーを実行するマシン（**nlserver web** プロセス）に LibreOffice をインストールする必要があります。

>[!NOTE]
>
>Linux の場合、フォントを追加する必要があります。 詳しくは、[MTA 統計のフォント &#x200B;](../../installation/using/prerequisites-of-campaign-installation-in-linux.md#fonts-for-mta-statistics) を参照してください。

## SpamAssassin {#spamassassin}

SpamAssassin を使用すると、受信で使用されるスパム対策ツールでメッセージが望ましくないと見なされるリスクがあるかどうかを判断するために、メールにスコアを割り当てることができます。 インストールはオプションです。

SpamAssassin によって望ましくないものとしてメールが選定されるかどうかは、完全にフィルタリングおよびスコアルールに基づいています。 したがって、SpamAssassin のインストールとAdobe Campaignへの統合が完全に機能し、送信前に配信に割り当てられたスコアの関連性を保証するには、これらのルールを 1 日に 1 回以上更新する必要があります。 この更新は、SpamAssassin をホストするサーバー管理者の責任です。

サポートされている最小バージョンは **3.4** です。

SpamAssassin には HTTP インターネットアクセス （tcp/80）が必要です。

SpamAssassin のインストール段階と設定段階については、[SpamAssassin の設定 &#x200B;](../../installation/using/configuring-spamassassin.md) を参照してください。
