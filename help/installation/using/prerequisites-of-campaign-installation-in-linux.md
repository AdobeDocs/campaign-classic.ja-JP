---
product: campaign
title: Linux での Campaign インストールの前提条件
description: Linux での Campaign インストールの前提条件
feature: Installation, Instance Settings
badge-v7-prem: label="オンプレミスおよびハイブリッド" type="Caution" url="https://experienceleague.adobe.com/docs/campaign-classic/using/installing-campaign-classic/architecture-and-hosting-models/hosting-models-lp/hosting-models.html?lang=ja" tooltip="オンプレミスデプロイメントとハイブリッドデプロイメントにのみ適用されます"
audience: installation
content-type: reference
topic-tags: installing-campaign-in-linux-
exl-id: acbd2873-7b1c-4d81-bc62-cb1246c330af
source-git-commit: b666535f7f82d1b8c2da4fbce1bc25cf8d39d187
workflow-type: tm+mt
source-wordcount: '916'
ht-degree: 2%

---

# Linux に Campaign をインストールするための前提条件{#prerequisites-of-campaign-installation-in-linux}



## ソフトウェアの前提条件 {#software-prerequisites}

この節では、Adobe Campaignをインストールする前に必要な事前設定手順について説明します。

Adobe Campaignのインストールに必要な技術的およびソフトウェア設定について詳しくは、を参照してください。 [互換性マトリックス](../../rn/using/compatibility-matrix.md).

次のコンポーネントをインストールし、正しく設定する必要があります。

* Apache(互換性マトリックス](../../rn/using/compatibility-matrix.md)を参照してください[。
* Java JDK および OpenJDK については、 [Java Development Kit - JDK](../../installation/using/application-server.md#java-development-kit---jdk) を参照してください。
* ライブラリ( [ライブラリ](#libraries)を参照)
* データベースアクセスレイヤーについては、「データベースアクセスレイヤー](#database-access-layers)」を参照してください[。
* LibreOffice、を参照 [LibreOffice for Debian のインストール](#installing-libreoffice-for-debian) および [LibreOffice for CentOS のインストール](#installing-libreoffice-for-centos),
* フォントについては、を参照してください。 [MTA 統計のフォント](#fonts-for-mta-statistics) および [日本語インスタンス用のフォント](#fonts-for-japanese-instances).

>[!NOTE]
>
>CentOS 7 および Debian 8 プラットフォームに 8709 以前のビルドをインストールするには、apache access_compat モジュールを有効にする必要があります。

### ライブラリ {#libraries}

Linux にAdobe Campaignをインストールするには、必要なライブラリがあることを確認してください。

* Library C は TLS (スレッドローカルストレージ) モードをサポートできなければなりません。 このモードは、Xen サポートが無効になっている一部のカーネルを除いて、ほとんどの場合アクティブです。

  これを確認するには、たとえばuname **-a | grep xen** コマンドを使用できます。

  コマンドが何も返さない（空の行）場合は、設定が正しいことを意味します。

* OpenSSL バージョンが必要です **1.0.2** 以上。

  RHEL 7/8 ディストリビューションの場合、バージョン 1.0 の OpenSSL が必要です。

* Adobe Campaignを使用するには、 **libicu** ライブラリがインストールされました。

  次のバージョンの **libicu** サポートされているビット（32 ビットまたは 64 ビット）:

   * RHEL 7/8、CentOS 7:libicu50
   * Debian 8: libicu52
   * Debian 9: libicu57

  Adobe Campaignを使用するには、libc-ares ライブラリをインストールする必要があります。 RHEL/CentOS 上で、次のコマンドを実行します。

  ```
  yum install c-ares
  ```

  Debian の場合

  ```
  aptitude install libc-ares2
  ```

### Selinux {#selinux}

使用する場合は、SELinux モジュールを適切に設定する必要があります。

これを行うには、root としてログオンし、次のコマンドを入力します。

```
echo 0 >/selinux/enforce
```

これに加えて、 **/etc/sysconfig/httpd** ファイルの次の行が、Adobe Campaign環境設定スクリプトを参照するために追加されました。

```
. ~neolane/nl6/env.sh
```

RHEL および CentOS では、SELinux が有効な場合、データベースのクライアントレイヤーの互換性の問題が見られました。 Adobe Campaignを正しく動作させるには、SELinux を無効にすることをお勧めします。

**次のプロセスを適用します。**

* ファイルを編集します **/etc/selinux/config**

* SELINUX の行を次のように変更します。

```
SELINUX=disabled
```

### MTA 統計のフォント {#fonts-for-mta-statistics}

MTA 統計(nms/fra/jsp/stat.jsp)に関するレポートを正しく表示するには、フォントを追加します。

Debian で次のコマンドを追加します:

```
aptitude install xfonts-base xfonts-75dpi ttf-bitstream-vera ttf-dejavu
```

Redhat で、次のコマンドを使用します。

* CentOS/RHEL 7 の場合：

  ```
  yum install xorg-x11-fonts-base xorg-x11-fonts-75dpi bitstream-vera-fonts dejavu-lgc-fonts
  ```

* RHEL 8 の場合：

  ```
  dnf install xorg-x11-fonts-misc xorg-x11-fonts-75dpi dejavu-lgc-sans-fonts  dejavu-sans-fonts dejavu-sans-mono-fonts dejavu-serif-fonts
  ```

### 日本語インスタンス用のフォント {#fonts-for-japanese-instances}

レポートをPDFフォーマットにエクスポートするには、日本語インスタンスで特定の文字のフォントが必要です。

Debian で、次のコマンドを追加します。

```
aptitude install fonts-ipafont
```

Red Hat で、次のコマンドを追加します。

* RHEL 7 の場合:

  ```
  yum install ipa-gothic-fonts ipa-mincho-fonts
  ```

* RHEL 8 の場合:

  ```
  dnf install vlgothic-fonts
  ```

### LibreOffice for Debian のインストール {#installing-libreoffice-for-debian}

Debian の場合、次の設定が必要です。

1. 次の標準パッケージをインストールします。

   ```
   apt-get install libreoffice-writer libreoffice-calc libreoffice-java-common
   ```

1. 次のフォントをインストールします（オプションですが、日本語インスタンスには強く推奨されます）。

   ```
   apt-get install fonts-ipafont
   ```

### LibreOffice for CentOS のインストール {#installing-libreoffice-for-centos}

CentOS を使用する場合は、以下の設定が必要です。

```
yum install libreoffice-headless libreoffice-writer libreoffice-calc
```

## データベース アクセス層 {#database-access-layers}

使用しているデータベースエンジンのアクセスレイヤーがサーバーにインストールされ、Adobe Campaign アカウントを介してアクセスできる必要があります。 バージョンとインストールモードは、使用するデータベースエンジンによって異なる場合があります。

サポートされているパイロットバージョンは、[互換性マトリックス](../../rn/using/compatibility-matrix.md)に詳述されています。

また、一般も確認してください [データベース](../../installation/using/database.md) セクション。

### PostgreSQL {#postgresql}

Adobe Campaignは、バージョン 7.2 以降の PostgreSQL クライアントライブラリのすべてのバージョンをサポートします。（**libpq.so.5**, **libpq.so.4**, **libpq.so.3.2** および **libpq.so.3.1**）に設定します。

Adobe Campaignで PostgreSQL を使用するには、対応するをインストールする必要があります **pgcrypto** ライブラリ。

### Oracle {#oracle}

64 ビット Debian のライブラリバージョンを取得します。例： **libclntsh.so**, **libclntsh.so.11.1** および **libclntsh.so.10.1**.

Linux RPM パッケージはOracleテクノロジ・ネットワークから入手できます。

>[!NOTE]
>
>既にOracleクライアントをインストールしていて、グローバル環境（例：/etc/profile）が正しく設定されていない場合は、不足している情報を以下に追加できます。 **nl6/customer.sh** スクリプト詳しくは、次を参照してください。 [環境変数](../../installation/using/installing-packages-with-linux.md#environment-variables).

**トラブルシューティングとベストプラクティス**

問題は、Oracleクライアントまたはサーバーの更新、バージョンの変更後、またはインスタンスの最初のインストール時に発生する可能性があります。

クライアント・コンソールで、ログ、ワークフロー最後の処理、次の処理などに予期しないタイム・ラグ (1 時間以上) があることに気付いた場合は、Oracle クライアントのライブラリと Oracle サーバーの間に問題がある可能性があります。 このような問題を回避するために

1. 必ず完全なクライアント&#x200B;**を使用してください**。

   oracleインスタントクライアントバージョンを使用する際の様々な問題が特定されています。 さらに、インスタントクライアントでタイムゾーンファイルを変更することは不可能です。

1. 次のことを確認します **クライアントバージョン** および **データベース・サーバのバージョン** はです **同じ**.

   oracleの互換表に反してバージョンを混在させ、クライアントとサーバのバージョンを整合させることを推奨すると、問題が発生することが知られています。

   またORACLE_HOME値をチェックして、予想されるクライアントバージョンを指していることを確認します(複数のバージョンがマシンにインストールされている場合)。

1. クライアントとサーバーが同じ **タイムゾーンファイル**&#x200B;を使用していることを確認します。

### DB2 {#db2}

サポートされているライブラリバージョンは **libdb2.so** です。

## 実装手順 {#implementation-steps}

Linux 用のAdobe Campaignのインストールは、サーバーのインストールに続いてインスタンスの設定の順序で実行する必要があります。

インストールプロセスについては、この章で説明します。 インストール手順は次のとおりです。

* 手順 1：アプリケーションサーバーのインストールについては、を参照してください。 [Linux でのパッケージのインストール](../../installation/using/installing-packages-with-linux.md).
* 手順 2:web サーバーとの統合（デプロイされているコンポーネントに応じてオプションで使用可能）

インストール手順が完了したら、インスタンス、データベース、サーバーを設定する必要があります。 詳しくは、次を参照してください [初期設定について](../../installation/using/about-initial-configuration.md).
