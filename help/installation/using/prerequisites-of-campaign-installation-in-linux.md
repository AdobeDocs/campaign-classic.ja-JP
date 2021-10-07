---
product: campaign
title: Linux での Campaign のインストールの前提条件
description: Linux での Campaign のインストールの前提条件
audience: installation
content-type: reference
topic-tags: installing-campaign-in-linux-
exl-id: acbd2873-7b1c-4d81-bc62-cb1246c330af
source-git-commit: bd9f035db1cbad883e1f27fe901e34dfbc9c1229
workflow-type: tm+mt
source-wordcount: '896'
ht-degree: 3%

---

# Linux に Campaign をインストールするための前提条件{#prerequisites-of-campaign-installation-in-linux}

![](../../assets/v7-only.svg)

## ソフトウェアの前提条件 {#software-prerequisites}

この節では、Adobe Campaignをインストールする前に必要な事前設定手順を説明します。

Adobe Campaignのインストールに必要な技術的およびソフトウェアの設定について詳しくは、互換性マトリックス [ を参照してください。](../../rn/using/compatibility-matrix.md)

次のコンポーネントをインストールし、正しく設定する必要があります。

* Apache（[ 互換性マトリックス ](../../rn/using/compatibility-matrix.md) を参照）
* Java JDK および OpenJDK（[Java Development Kit - JDK](../../installation/using/application-server.md#java-development-kit---jdk) を参照）
* ライブラリ（[ ライブラリ ](#libraries) を参照）
* データベース・アクセス・レイヤー（[ データベース・アクセス・レイヤー ](#database-access-layers) を参照）
* LibreOffice については、「 [LibreOffice for Debian のインストール ](#installing-libreoffice-for-debian) 」および「 [LibreOffice for CentOS のインストール ](#installing-libreoffice-for-centos) 」を参照してください。
* フォントについては、[MTA 統計用のフォント ](#fonts-for-mta-statistics) および [ 日本語インスタンス用のフォント ](#fonts-for-japanese-instances) を参照してください。

>[!NOTE]
>
>CentOS 7 および Debian 8 プラットフォームに 8709 以下のビルドをインストールするには、apache access_compat モジュールを有効にする必要があります。

### ライブラリ {#libraries}

Linux にAdobe Campaignをインストールするには、必要なライブラリがあることを確認してください。

* ライブラリ C は、TLS（スレッドローカルストレージ）モードをサポートできる必要があります。 このモードは、Xen のサポートが無効になっている一部のカーネルを除いて、ほとんどの場合、アクティブです。

   これを確認するには、**uname -a | grep xen** コマンドの例

   コマンドが何も返さない場合（空行）は、設定が正しいことを意味します。

* OpenSSL の **バージョン 0.9.8** または **1.0** が必要です。

   RHEL 7 ディストリビューションの場合、OpenSSL のバージョン 1.0 が必要です。

* Adobe Campaignを使用するには、**libicu** ライブラリをインストールする必要があります。

   **libicu** の次のバージョンがサポートされています（32 ビットまたは 64 ビット）。

   * RHEL 7、CentOS 7:libicu50
   * Debian 8:libicu52
   * Debian 9:libicu57

   Adobe Campaignを使用するには、libc-ares ライブラリをインストールする必要があります。 RHEL/CentOS で、次のコマンドを実行します。

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

これに加えて、 **/etc/sysconfig/httpd** ファイルで、Adobe Campaign環境設定スクリプトを参照する次の行が追加されました。

```
. ~neolane/nl6/env.sh
```

RHEL および CentOS では、SELinux を有効にした際に、データベースのクライアント層との互換性の問題が指摘されました。 Adobe Campaignが正しく動作できるように、SELinux を無効にすることをお勧めします。

**次の手順に従います。**

* ファイル **/etc/selinux/config** を編集します。

* SELINUX 行を次のように変更します。

```
SELINUX=disabled
```

### MTA 統計のフォント {#fonts-for-mta-statistics}

MTA 統計 (nms/fra/jsp/stat.jsp) に関するレポートを正しく表示するには、フォントを追加します。

Debian で、次のコマンドを追加します。

```
aptitude install xfonts-base xfonts-75dpi ttf-bitstream-vera ttf-dejavu
```

Redhat では、次のコマンドを使用します。

```
yum install xorg-x11-fonts-base xorg-x11-fonts-75dpi bitstream-vera-fonts dejavu-lgc-fonts
```

### 日本語インスタンス用のフォント {#fonts-for-japanese-instances}

日本語インスタンスでは、レポートをPDF形式で書き出すために特定の文字のフォントが必要です。

Debian で、次のコマンドを追加します。

```
aptitude install fonts-ipafont
```

Red Hat で、次のコマンドを追加します。

```
yum install ipa-gothic-fonts ipa-mincho-fonts
```

### LibreOffice for Debian のインストール {#installing-libreoffice-for-debian}

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

CentOS では、次の設定が必要です。

1. 次の標準パッケージをインストールします。

   ```
   yum install libreoffice-headless libreoffice-writer libreoffice-calc
   ```

1. 次のフォントをインストールします（オプションですが、日本語インスタンスの場合は強く推奨します）。

   ```
   yum install ipa-gothic-fonts ipa-mincho-fonts
   ```

## データベースアクセスレイヤー {#database-access-layers}

使用するデータベースエンジンのアクセスレイヤーは、サーバーにインストールされ、Adobe Campaignアカウント経由でアクセスできる必要があります。 バージョンとインストールモードは、使用するデータベースエンジンによって異なる場合があります。

サポートされているパイロットバージョンは、[互換性マトリックス](../../rn/using/compatibility-matrix.md)に詳述されています。

また、[ データベース ](../../installation/using/database.md) の一般的なセクションも確認してください。

### PostgreSQL {#postgresql}

Adobe Campaignは、バージョン 7.2 の PostgreSQL クライアントライブラリのすべてのバージョンをサポートしています。（**libpq.so.5**、**libpq.so.4**、**libpq.so.3.2** および **libpq.so.3.1**）。

PostgreSQL をAdobe Campaignと共に使用する場合は、対応する **pgcrypto** ライブラリをインストールする必要もあります。

### Oracle {#oracle}

64 ビット Debian のライブラリバージョンを取得します。例：**libclntsh.so**、**libclntsh.so.11.1** および **libclntsh.so.10.1**。

Linux RPM パッケージは、Linux Technology Network から入手できます。Oracle

>[!NOTE]
>
>既にOracleクライアントをインストールしていて、グローバル環境をインストールしている場合 ( 例：/etc/profile) が正しく設定されていない場合は、**nl6/customer.sh** スクリプトに不足している情報を追加できます。詳しくは、[ 環境変数 ](../../installation/using/installing-packages-with-linux.md#environment-variables) を参照してください。

**トラブルシューティングとベストプラクティス**

問題は、Oracleクライアントまたはサーバーの更新後、バージョンの変更後、またはインスタンスの最初のインストール時に発生する可能性があります。

クライアントコンソールで、ログ、ワークフローの最後の処理、次の処理などに予期しない時間遅れ（1 時間以上）があることに気がついた場合は、OracleクライアントのライブラリとOracleサーバーの間で問題が発生する可能性があります。 そのような問題を回避するには

1. 必ず **完全なクライアント** を使用してください。

   Instant Client バージョンを使用する際に、様々なOracleが見つかりました。 また、インスタントクライアントで Timezone ファイルを変更することは不可能です。

1. **クライアントのバージョン** と **データベースのサーバーのバージョン** が **同じ** であることを確認します。

   oracleの互換性マトリックスにもかかわらず、バージョンを混在させ、クライアントとサーバーのバージョンを一致させることをお勧めします。

   また、ORACLE_HOME の値をチェックして、期待されるクライアントのバージョンを指していることを確認します（複数のバージョンがマシンにインストールされている場合）。

1. クライアントとサーバーが同じ **タイムゾーンファイル** を使用していることを確認します。

### DB2 {#db2}

サポートされるライブラリのバージョンは **libdb2.so** です。

## 実装手順 {#implementation-steps}

Adobe Campaign版 Linux のインストールは、次の順序で実行する必要があります。サーバーのインストール後にインスタンスの設定が続きます。

この章では、インストールプロセスについて説明します。 インストール手順は次のとおりです。

* 手順 1:アプリケーションサーバーのインストールについては、[Linux でのパッケージのインストール ](../../installation/using/installing-packages-with-linux.md) を参照してください。
* 手順 2:Web サーバーとの統合（デプロイされたコンポーネントに応じてオプション）。

インストール手順が完了したら、インスタンス、データベース、サーバーを設定する必要があります。 詳しくは、[ 初期設定について ](../../installation/using/about-initial-configuration.md) を参照してください。
