---
product: campaign
title: Linux での Campaign のインストールの前提条件
description: Linux での Campaign のインストールの前提条件
feature: Installation, Instance Settings
badge-v7-only: label="v7" type="Informative" tooltip="Campaign Classic v7 にのみ適用されます"
badge-v7-prem: label="オンプレミスおよびハイブリッド" type="Caution" url="https://experienceleague.adobe.com/docs/campaign-classic/using/installing-campaign-classic/architecture-and-hosting-models/hosting-models-lp/hosting-models.html?lang=ja" tooltip="オンプレミスデプロイメントとハイブリッドデプロイメントにのみ適用されます"
audience: installation
content-type: reference
topic-tags: installing-campaign-in-linux-
exl-id: acbd2873-7b1c-4d81-bc62-cb1246c330af
source-git-commit: 3a9b21d626b60754789c3f594ba798309f62a553
workflow-type: tm+mt
source-wordcount: '914'
ht-degree: 5%

---

# Linux でキャンペーンをインストールするための前提条件{#prerequisites-of-campaign-installation-in-linux}



## ソフトウェアの前提条件 {#software-prerequisites}

ここでは、Adobe Campaign をインストールする前に必要な事前設定手順について説明します。

Adobe Campaignのインストールに必要な技術的およびソフトウェア設定について詳しくは、 [互換性マトリックス](../../rn/using/compatibility-matrix.md).

次のコンポーネントをインストールし、正しく設定する必要があります。

* Apache（を参照） [互換性マトリックス](../../rn/using/compatibility-matrix.md),
* Java JDK と OpenJDK（を参照） [Java 開発キット — JDK](../../installation/using/application-server.md#java-development-kit---jdk),
* ライブラリ（を参照） [ライブラリ](#libraries),
* データベースアクセスレイヤー（を参照） [データベースアクセスレイヤー](#database-access-layers),
* LibreOffice（を参照） [Debian 用 LibreOffice のインストール](#installing-libreoffice-for-debian) および [CentOS 用 LibreOffice のインストール](#installing-libreoffice-for-centos),
* フォント（を参照） [MTA 統計用のフォント](#fonts-for-mta-statistics) および [日本語インスタンス用のフォント](#fonts-for-japanese-instances).

>[!NOTE]
>
>CentOS 7 および Debian 8 プラットフォームに 8709 以下のビルドをインストールするには、apache access_compat モジュールを有効にする必要があります。

### ライブラリ {#libraries}

Linux にAdobe Campaignをインストールするには、必要なライブラリがあることを確認してください。

* Library C は、TLS (スレッドローカルストレージ) モードをサポートできる必要があります。 このモードは、ほとんどの場合、Xen のサポートが無効になっている一部のカーネルを除き、アクティブになります。

  これを確認するには、例として uname-a | grep xen **コマンドを使用** します。

  コマンドが何も返さない（空行）場合は、設定が正しいことを意味します。

* OpenSSL バージョンが必要です **1.0.2** 以上

  RHEL 7/8 ディストリビューションの場合、OpenSSL のバージョン 1.0 が必要です。

* Adobe Campaign を使用するには、libicu **ライブラリインストールされている** 必要があります。

  Libicu **の** 次のバージョンがサポートされています (32 ビットまたは64ビット)。

   * RHEL 7/8、CentOS 7: libicu50
   * Debian 8: libicu52
   * Debian 9: libicu57

  Adobe Campaign を使用するには、libc-アレスライブラリがインストールされている必要があります。 RHEL/CentOS で、次のコマンドを実行します。

  ```
  yum install c-ares
  ```

  Debian の場合：

  ```
  aptitude install libc-ares2
  ```

### SELinux {#selinux}

使用する場合は、SELinux モジュールを適切に設定する必要があります。

これをおこなうには、root としてログオンし、次のコマンドを入力します。

```
echo 0 >/selinux/enforce
```

これに加えて、 **/etc/sysconfig/httpd** ファイルの下に、Adobe Campaign環境設定スクリプトを参照する次の行が追加されました。

```
. ~neolane/nl6/env.sh
```

RHEL および CentOS では、SELinux を有効にする際に、データベースのクライアント層との互換性の問題が指摘されました。 Adobe Campaignが正しく動作できるように、SELinux を無効にすることをお勧めします。

**次の手順に従います。**

* ファイルを編集します **/etc/selinux/config**

* SELINUX 行を次のように変更します。

```
SELINUX=disabled
```

### MTA 統計用のフォント {#fonts-for-mta-statistics}

MTA 統計 (nms/fra/jsp/stat) のレポートが正しく表示されるようにするには、フォントを追加します。

Debian で、次のコマンドを追加します。

```
aptitude install xfonts-base xfonts-75dpi ttf-bitstream-vera ttf-dejavu
```

Redhat では、次のコマンドを使用します。

* CentOS/RHEL 7 の場合：

  ```
  yum install xorg-x11-fonts-base xorg-x11-fonts-75dpi bitstream-vera-fonts dejavu-lgc-fonts
  ```

* RHEL 8 の場合：

  ```
  dnf install xorg-x11-fonts-misc xorg-x11-fonts-75dpi dejavu-lgc-sans-fonts  dejavu-sans-fonts dejavu-sans-mono-fonts dejavu-serif-fonts
  ```

### 日本語インスタンスのフォント {#fonts-for-japanese-instances}

日本語インスタンスでは、レポートをPDF形式で書き出すために、特定の文字のフォントが必要です。

Debian で、次のコマンドを追加します。

```
aptitude install fonts-ipafont
```

Red Hat で、次のコマンドを追加します。

* RHEL 7 の場合：

  ```
  yum install ipa-gothic-fonts ipa-mincho-fonts
  ```

* RHEL 8 の場合：

  ```
  dnf install vlgothic-fonts
  ```

### Debian 用 LibreOffice のインストール {#installing-libreoffice-for-debian}

Debian の場合、次の設定が必要です。

1. 次の標準パッケージをインストールします。

   ```
   apt-get install libreoffice-writer libreoffice-calc libreoffice-java-common
   ```

1. 次のフォントをインストールします（オプションですが、日本語インスタンスの場合は強く推奨します）。

   ```
   apt-get install fonts-ipafont
   ```

### CentOS 用 LibreOffice のインストール {#installing-libreoffice-for-centos}

CentOS には、次の設定が必要です。

```
yum install libreoffice-headless libreoffice-writer libreoffice-calc
```

## データベースアクセス層 {#database-access-layers}

使用しているデータベースエンジンのアクセスレイヤーは、サーバーにインストールされ、Adobe Campaignアカウント経由でアクセスできる必要があります。 バージョンとインストールモードは、使用するデータベースエンジンによって異なる場合があります。

サポートされているパイロットバージョンは、[互換性マトリックス](../../rn/using/compatibility-matrix.md)に詳述されています。

また、一般 [データベース](../../installation/using/database.md) 」セクションに入力します。

### PostgreSQL {#postgresql}

Adobe Campaign では、バージョン7.2 からのすべてのバージョンの PostgreSQL クライアントライブラリをサポートしています。 **** **** つまり、libpq、libpq、libpq、libpq **など** **** です。

Adobe Campaign で PostgreSQL を使用する場合も、対応する **pgcrypto** ライブラリをインストールする必要があります。

### Oracle {#oracle}

64ビット Debian のライブラリのバージョンを取得します。例: libclntsh.so, libclntsh **** . so、libclntsh. so **.** ****

Oracle テクノロジーのネットワークから Linux RPM パッケージを入手できます。

>[!NOTE]
>
>既にOracleクライアントをインストールしているが、グローバル環境（例：/etc/profile）が正しく設定されていない場合は、見つからない情報を **nl6/customer.sh** スクリプトについて詳しくは、 [環境変数](../../installation/using/installing-packages-with-linux.md#environment-variables).

**トラブルシューティングとベストプラクティス**

問題は、Oracleクライアントまたはサーバーの更新後、バージョンの変更後、またはインスタンスの最初のインストール時に発生する可能性があります。

ログ、Oracleの最後の処理、次の処理などに予期しない時間ラグ（1 時間以上）があることがクライアントコンソールでわかった場合は、ワークフロークライアントのライブラリとOracleサーバーの間に問題が発生する可能性があります。 こうした問題を回避するには

1. 必ず **フルクライアント**.

   Instant Client バージョンを使用する際に、様々なOracleが見つかりました。 また、インスタントクライアントで Timezone ファイルを変更することはできません。

1. 次を確認します。 **クライアントバージョン** そして **データベースサーバーのバージョン** は **同じ**.

   oracleの互換表にもかかわらず、バージョンを混在させ、クライアントとサーバーのバージョンを一致させることを推奨することで、問題が発生することがわかっています。

   また、ORACLE_HOME の値をチェックして、期待されるクライアントバージョンを指していることを確認します（複数のバージョンがマシンにインストールされている場合）。

1. クライアントとサーバーが同じものを使用していることを確認します。 **タイムゾーンファイル**.

### DB2 {#db2}

サポートされているライブラリバージョンは **libdb2.so** です。

## 実装手順 {#implementation-steps}

Adobe Campaign installations for Linux は、次のシーケンスで実行する必要があります。サーバーのインストール、その後のインスタンスの設定。

この章では、インストールプロセスについて説明します。 インストール手順は次のとおりです。

* 手順 1: アプリケーションサーバーのインストールについては、『 Linux ](../../installation/using/installing-packages-with-linux.md) でのパッケージのインストールを [ 参照してください。
* 手順 2: Web サーバーとの統合 (オプション。デプロイされているコンポーネントによって異なります)。

インストール手順が完了したら、インスタンス、データベースおよびサーバーを設定する必要があります。 詳しくは、初期設定 ](../../installation/using/about-initial-configuration.md) を [ 参照してください。
