---
product: campaign
title: LinuxでのCampaign インストールの前提条件
description: LinuxでのCampaign インストールの前提条件
feature: Installation, Instance Settings
badge-v7-prem: label="オンプレミス／ハイブリッドのみ" type="Caution" url="https://experienceleague.adobe.com/docs/campaign-classic/using/installing-campaign-classic/architecture-and-hosting-models/hosting-models-lp/hosting-models.html?lang=ja" tooltip="オンプレミスデプロイメントとハイブリッドデプロイメントにのみ適用されます"
audience: installation
content-type: reference
topic-tags: installing-campaign-in-linux-
exl-id: acbd2873-7b1c-4d81-bc62-cb1246c330af
TQID: https://experienceleague.adobe.com/SFdh5L8-oHjpH7rIhDxOQZqw7AukXtkv3lJHZu2oTHQ
product_v2:
  - id: dfc56824-e8b9-499e-85d4-21aedb507314
topic_v2:
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
  - id: c1579802-ddd4-4214-8a91-97b2066abe11
feature_v2: []
subfeature_v2: []
source-git-commit: bb41e9407ab5853b0194bb325bbf3f17bc3ea232
workflow-type: tm+mt
source-wordcount: 854
ht-degree: 5%

---

# LinuxにCampaignをインストールするための前提条件{#prerequisites-of-campaign-installation-in-linux}

## ソフトウェアの前提条件 {#software-prerequisites}

この節では、Adobe Campaignをインストールする前に必要な事前設定の手順について詳しく説明します。

Adobe Campaignのインストールに必要な技術的な設定とソフトウェアの設定については、[互換性マトリックス &#x200B;](../../rn/using/compatibility-matrix.md)で詳しく説明しています。

リマインダーとして、次のコンポーネントをインストールして正しく設定する必要があります。

* Apacheについては、[互換性マトリックス &#x200B;](../../rn/using/compatibility-matrix.md)を参照してください。
* Java JDKおよびOpenJDKについては、[Java Development Kit - JDK](../../installation/using/application-server.md#jdk)を参照してください。
* ライブラリ：[&#x200B; ライブラリ &#x200B;](#libraries)を参照してください。
* データベースアクセスレイヤーについては、[&#x200B; データベースアクセスレイヤー](#database-access-layers)を参照してください。
* LibreOfficeについては、[Debian向けLibreOfficeのインストール &#x200B;](#installing-libreoffice-for-debian)および[CentOS向けLibreOfficeのインストール &#x200B;](#installing-libreoffice-for-centos)を参照してください。
* フォントについては、[MTA統計のフォント &#x200B;](#fonts-for-mta-statistics)および日本語インスタンスのフォント [を参照してください。](#fonts-for-japanese-instances)


### ライブラリ {#libraries}

LinuxにAdobe Campaignをインストールするには、必要なライブラリがあることを確認してください。

* ライブラリ Cは、TLS （Thread Local Storage）モードをサポートできる必要があります。 このモードは、Xen サポートが無効になっている一部のカーネルを除いて、ほとんどの場合にアクティブです。

  これを確認するには、例えば、**uname -a | grep xen** コマンドを使用します。

  コマンドが空の行を返さない場合は、設定が正しいことを意味します。

* OpenSSL バージョン **1.0.2**&#x200B;以降が必要です。

  RHEL ディストリビューションの場合は、バージョン 1.0のOpenSSLが必要です。

* Adobe Campaignを使用するには、**libicu** ライブラリがインストールされている必要があります。

### SELinux {#selinux}

SELinux モジュールを使用する場合は、適切に設定する必要があります。

これを行うには、rootとしてログオンし、次のコマンドを入力します。

```
echo 0 >/selinux/enforce
```

これに加えて、**/etc/sysconfig/httpd** ファイルで、Adobe Campaign環境設定スクリプトを参照するために次の行が追加されました。

```
. ~neolane/nl6/env.sh
```

RHELおよびCentOSでは、SELinuxが有効になっている場合に、データベースのクライアントレイヤーに関する互換性の問題が記録されました。 Adobe Campaignが正しく動作することを確認するには、SELinuxを無効にすることをお勧めします。

**次のプロセスを適用します：**

* ファイル **/etc/selinux/config**&#x200B;を編集

* SELINUX行を次のように変更します。

```
SELINUX=disabled
```

### MTA統計用フォント {#fonts-for-mta-statistics}

MTA統計（nms/fra/jsp/stat.jsp）に関するレポートを正しく表示するには、フォントを追加します。

Debianで、次のコマンドを追加します。

```
apt install xfonts-base xfonts-75dpi ttf-bitstream-vera ttf-dejavu
```

RHELには次のコマンドを使用します。

```
dnf install xorg-x11-fonts-misc xorg-x11-fonts-75dpi dejavu-lgc-sans-fonts  dejavu-sans-fonts dejavu-sans-mono-fonts dejavu-serif-fonts
```

### 日本語インスタンス用フォント {#fonts-for-japanese-instances}

レポートをPDF形式に書き出すには、日本語インスタンスで特定の文字のフォントが必要です。

Debianで、次のコマンドを追加します。

```
apt install fonts-ipafont
```

RHELの場合は、次のコマンドを追加します。

```
dnf install epel-release # if required
dnf install vlgothic-fonts
```

### Debian用LibreOfficeのインストール {#installing-libreoffice-for-debian}

Debianの場合、以下の設定が必要です。

1. 次の標準パッケージをインストールします。

   ```
   apt-get install libreoffice-writer libreoffice-calc libreoffice-java-common
   ```

1. 次のフォントをインストールします（オプションですが、日本語の場合は強くお勧めします）。

   ```
   apt-get install fonts-ipafont
   ```

### CentOS用LibreOfficeのインストール {#installing-libreoffice-for-centos}

CentOSでは、次の設定が必要です。

```
yum install libreoffice-headless libreoffice-writer libreoffice-calc
```

## データベースアクセスレイヤー {#database-access-layers}

使用しているデータベースエンジンのアクセスレイヤーは、サーバーにインストールされ、Adobe Campaign アカウントからアクセスできる必要があります。 バージョンとインストールモードは、使用するデータベースエンジンによって異なります。

サポートされているパイロットバージョンは、[互換性マトリックス](../../rn/using/compatibility-matrix.md)に詳述されています。

一般[&#x200B; データベース &#x200B;](../../installation/using/database.md) セクションも確認してください。

### PostgreSQL {#postgresql}

Adobe Campaignは、バージョン 9.6のすべてのバージョン（**libpq.so.5**）のPostgreSQL クライアントライブラリをサポートしています。

Adobe CampaignでPostgreSQLを使用するには、対応する&#x200B;**pgcrypto** ライブラリもインストールする必要があります。

### Oracle {#oracle}

64 ビット Debianのライブラリバージョン （例：**libclntsh.so**、**libclntsh.so.19.1**、**libclntsh.so.18.1**、**libclntsh.so.12.1**、**libclntsh.so.11.1**&#x200B;または&#x200B;**libclntsh.so.10.1**）を取得します。

Linux RPM パッケージは、Oracle Technology Networkから入手できます。

>[!NOTE]
>
>既にOracle クライアントをインストールしたが、グローバル環境（例：/etc/profile）が正しく設定されていない場合は、**nl6/customer.sh** スクリプトに不足している情報を追加できます。詳しくは、[環境変数](../../installation/using/installing-packages-with-linux.md#environment-variables)を参照してください。

**トラブルシューティングとベストプラクティス**

問題は、Oracle クライアントまたはサーバーのアップデート、バージョンの変更、またはインスタンスの最初のインストール後に発生する可能性があります。

クライアントコンソールで、ログ、ワークフローの最終処理、次の処理などで予期しないタイムラグ（1時間以上）が発生していることに気づいた場合は、Oracle クライアントのライブラリとOracle Serverの間に問題が発生する可能性があります。 このような問題を回避するには

1. **完全なクライアント**&#x200B;を使用してください。

   Oracle Instant Client バージョンを使用する際に、様々な問題が特定されています。 さらに、インスタントクライアントでタイムゾーンファイルを変更することは不可能です。

1. **クライアントバージョン**&#x200B;と&#x200B;**データベースサーバーバージョン**&#x200B;が&#x200B;**同一**&#x200B;であることを確認してください。

   Oracleの互換性マトリックスと、クライアントとサーバーのバージョンを調整するための推奨事項にもかかわらず、バージョンを混在させると問題が発生することが分かっています。

   また、ORACLE_HOMEの値を確認して、想定されるクライアントバージョンを指していることを確認します（コンピューターに複数のバージョンがインストールされている場合）。

1. クライアントとサーバーが同じ&#x200B;**タイムゾーンファイル**&#x200B;を使用していることを確認してください。

## 実装手順 {#implementation-steps}

Linux用のAdobe Campaignのインストールは、サーバーインストールの後にインスタンス設定を行う必要があります。

インストールプロセスについては、この章で説明します。 インストール手順は次のとおりです。

* 手順1: アプリケーションサーバーのインストールについては、[Linuxでのパッケージのインストール &#x200B;](../../installation/using/installing-packages-with-linux.md)を参照してください。
* 手順2:Web サーバーとの統合（デプロイされたコンポーネントに応じてオプション）。

インストール手順が完了したら、インスタンス、データベース、サーバーを設定する必要があります。 詳しくは、[初期設定について](../../installation/using/about-initial-configuration.md)を参照してください。
