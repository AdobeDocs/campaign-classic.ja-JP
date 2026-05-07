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
source-wordcount: '677'
ht-degree: 5%

---

# アプリケーションサーバー{#application-server}

必要なデータベースアクセスレイヤーは、サーバーにインストールされ、Adobe Campaign アカウントからアクセスできる必要があります。

## Java開発キット - JDK {#jdk}

Java Development KitまたはJDKは、ソフトウェア開発キットです。 これは、Java アプリケーションとJava アプレット開発を可能にする基本コンポーネントです。

動的なWeb ページジェネレーターは、JSP テクノロジーを使用します。 このために、（Apacheからの） Tomcat エンジンがアプリケーションに含まれています。 Adobe Campaign アプリケーションがインストールされているすべてのサーバーにJava Development Kit （JDK）がインストールされている必要があります。

まず、動的なWeb ページ（レポート、Web フォームなど）の生成に使用されるサーブレットコンテナ Apache Tomcatが組み込まれているため、Adobe Campaign アプリケーションサーバー（**nlserver web** プロセス）を実行するコンピューターにJDKをインストールする必要があります。

このアプリケーションは、Oracleによって開発されたJava Development Kit （JDK）および&#x200B;**OpenJDK**&#x200B;に対して承認されています。

サポートされているバージョンについて詳しくは、キャンペーン [互換性マトリックス ](../../rn/using/compatibility-matrix.md)を参照してください。


>[!AVAILABILITY]
>
>* v7.4.1以降、Campaignには少なくとも&#x200B;**Java JDK 11**&#x200B;が必要です。 Campaign サーバーがWindows環境にインストールされている場合、Java ランタイム（JRE）が自動的に検出されなくなります。 JRE_HOME環境変数は、Campaignが`bin/server/jvm.dll` ファイルを検索できるフォルダーに設定する必要があります。 例えば、JDK 11が`C:\Program Files\Java\jdk-11` フォルダーにインストールされている場合、JRE_HOMEは`C:\Program Files\Java\jdk-11`である必要があります。
>
>* v7.4.1以降、Tomcat 10.1はデフォルトバージョンです。
>

### 推奨事項

Java開発キットをインストールおよびアップグレードする場合は、次の推奨事項を適用してください。

* Java Development Kitは、マシン上の他のアプリケーションで既に使用されている適切なJDK バージョンを使用してインストールできます。

* JDKをインストールする場合、Web ブラウザーとの統合は必要ありません。

* 配信エージェント（**nlserver mta** プロセス）またはワークフローサーバー（**nlserver wfserver** プロセス）のみを実行するマシンでは、JDKのインストールは必要ありません。

* Java バージョンをアップグレードする場合は、まず以前のバージョンをアンインストールする必要があります。 同じマシンにインストールされているJavaの両方のバージョンで競合が発生する可能性があります。

  オンプレミスのお客様は、`LD_LIBRARY_PATH` [環境変数](installing-packages-with-linux.md#environment-variables)が最新バージョンに設定されていることを確認できます（例：）。 java11）。 以前のバージョンに設定されている場合（例： Java8）の場合は、更新する必要があります。 JDK 11の場合、JDK ライブラリを検索するパスは`/usr/lib/jvm/java-11-openjdk-amd64/lib`です。


### インストール手順

Java Development Kitはプラットフォーム固有です。各オペレーティングシステムには個別のインストーラーが必要です。

JDKをダウンロードするには、[Oracle web サイト ](https://www.oracle.com/technetwork/java/javase/downloads/index.html){target="_blank"}に接続します。

>[!CAUTION]
>
> Java ランタイム環境（JRE）ではなく、Java開発キット（JDK）をダウンロードしてください。


Linux環境にJDSLをインストールするには、Adobeでパッケージマネージャーを使用することをお勧めします。

Debianの場合は、次のコマンドを使用します。

```sql
apt install openjdk-11-jdk-headless
```

RHELの場合は、次のコマンドを使用します。

```sql
dnf install java-11-openjdk-headless
```



## レポートの書き出し {#exporting-reports}

Adobe Campaignを使用して、レポートをMicrosoft ExcelおよびAdobe PDFに書き出すことができます。

* Microsoft Excel形式の場合、Adobe Campaignは&#x200B;**LibreOffice**&#x200B;に依存しています。

* Adobe PDF形式の場合、Adobe Campaignは&#x200B;**PhantomJS** コンバータを使用します。 PhantomJsはファクトリパッケージに含まれており、LibreOfficeはAdobe Campaign アプリケーションサーバーが実行されるコンピューター（**nlserver web** プロセス）にインストールされている必要があります。

>[!NOTE]
>
>Linuxの場合は、フォントを追加する必要があります。 詳しくは、[MTA統計のフォント ](../../installation/using/prerequisites-of-campaign-installation-in-linux.md#fonts-for-mta-statistics)を参照してください。

## SpamAssassin {#spamassassin}

SpamAssassinを使用すると、メッセージが受信に使用される迷惑メール対策ツールによって望ましくないと見なされるリスクがあるかどうかを判断するために、メールにスコアを割り当てることができます。 インストールはオプションです。

SpamAssassinによる望ましくないメールの選定は、フィルタリングとスコアリングのルールにもとづいています。 したがって、SpamAssassinのインストールとAdobe Campaignへの統合が完全に機能し、送信する前に配信に割り当てられたスコアの関連性を保証するために、これらのルールを少なくとも1日1回更新する必要があります。 このアップデートは、SpamAssassinをホストするサーバー管理者の責任です。

サポートされている最小バージョンは&#x200B;**3.4**&#x200B;です

SpamAssassinにはHTTP インターネットアクセス （tcp/80）が必要です。

SpamAssassinのインストールと設定の段階については、[SpamAssassinの設定](../../installation/using/configuring-spamassassin.md)を参照してください。
