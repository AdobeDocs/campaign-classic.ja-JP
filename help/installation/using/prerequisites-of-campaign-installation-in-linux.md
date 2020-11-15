---
title: Linux での Campaign のインストールの前提条件
description: Linux での Campaign のインストールの前提条件
page-status-flag: never-activated
uuid: 65c7af3f-ca1d-4255-b54a-6a3c83af40ae
contentOwner: sauviat
products: SG_CAMPAIGN/CLASSIC
audience: installation
content-type: reference
topic-tags: installing-campaign-in-linux-
discoiquuid: 3e2ccb70-6c0c-435f-9c06-f3e5e40367bb
translation-type: tm+mt
source-git-commit: 99d766cb6234347ea2975f3c08a6ac0496619b41
workflow-type: tm+mt
source-wordcount: '896'
ht-degree: 3%

---


# Linux での Campaign のインストールの前提条件{#prerequisites-of-campaign-installation-in-linux}

## ソフトウェアの前提条件 {#software-prerequisites}

このセクションでは、Adobe Campaignをインストールする前に必要な設定の暫定手順について説明します。

Adobe Campaignのインストールに必要な技術的およびソフトウェアの設定については、 [互換表を参照してください](../../rn/using/compatibility-matrix.md)。

注意：次のコンポーネントをインストールし、正しく設定する必要があります。

* Apache( [互換表](../../rn/using/compatibility-matrix.md)、
* Java JDKとOpenJDK、『 [Java Development Kit - JDK](../../installation/using/application-server.md#java-development-kit---jdk)』を参照してください。
* ライブラリについては、 [Libraries](#libraries)、
* データベース・アクセス・レイヤ、 [データベース・アクセス・レイヤ](#database-access-layers)、
* LibreOffice、『LibreOffice for Debianの [インストール](#installing-libreoffice-for-debian) 』および『LibreOffice for CentOSの [インストール](#installing-libreoffice-for-centos)』を参照してください。
* フォントについては、「MTA統計用の [フォント](#fonts-for-mta-statistics) 」および「日本語インスタンス用の [フォント](#fonts-for-japanese-instances)」を参照してください。

>[!NOTE]
>
>CentOS 7およびDebian 8プラットフォームに8709以下のビルドをインストールするには、apache access_compatモジュールを有効にする必要があります。

### ライブラリ {#libraries}

LinuxにAdobe Campaignをインストールするには、必要なライブラリがあることを確認してください。

* ライブラリCは、TLS(スレッドローカルストレージ)モードをサポートできる必要があります。 このモードは、Xenのサポートが無効になっているカーネルを除き、ほとんどの場合アクティブです。

   これを確認するには、 **uname -a | grep xen** コマンドの例

   コマンドが何も返さない（空行）場合は、設定が正しいことを意味します。

* OpenSSLの **バージョン0.9.8** または **1.0** が必要です。

   RHEL 7ディストリビューションの場合は、OpenSSLのバージョン1.0が必要です。

* Adobe Campaignを使用するには、 **libicu** libraryをインストールする必要があります。

   次のバージョンの **libicu** （32bitまたは64bit）がサポートされています。

   * RHEL 7、CentOS 7:libicu50
   * Debian 8:libicu52
   * Debian 9:libicu57

   Adobe Campaignを使用するには、libc-aresライブラリをインストールする必要があります。 RHEL/CentOSで、次のコマンドを実行します。

   ```
   yum install c-ares
   ```

   Debianの場合：

   ```
   aptitude install libc-ares2
   ```

### SELinux {#selinux}

使用する場合は、SELinuxモジュールを適切に構成する必要があります。

これを行うには、rootとしてログオンし、次のコマンドを入力します。

```
echo 0 >/selinux/enforce
```

これに加えて、 **/etc/sysconfig/httpd** ファイルには、Adobe Campaign環境設定スクリプトを参照する次の行が追加されています。

```
. ~neolane/nl6/env.sh
```

RHELおよびCentOSでは、SELinuxを有効にすると、データベースのクライアント層との互換性の問題が報告されていました。 Adobe Campaignが正しく動作するように、SELinuxを無効にすることをお勧めします。

**次のプロセスを適用します。**

* /etc/selinux/configファイル **を編集します。**

* SELINUX行を次のように変更します。

```
SELINUX=disabled
```

### MTA統計用フォント {#fonts-for-mta-statistics}

MTA統計(nms/fra/jsp/stat.jsp)のレポートを正しく表示するには、フォントを追加します。

Debianで、次のコマンドを追加します。

```
aptitude install xfonts-base xfonts-75dpi ttf-bitstream-vera ttf-dejavu
```

Redhatで、次のコマンドを使用します。

```
yum install xorg-x11-fonts-base xorg-x11-fonts-75dpi bitstream-vera-fonts dejavu-lgc-fonts
```

### 日本語インスタンス用のフォント {#fonts-for-japanese-instances}

レポートをPDF形式に書き出すには、日本のインスタンスで特定の文字のフォントが必要です。

Debianで、次のコマンドを追加します。

```
aptitude install fonts-ipafont
```

Red Hatで、次のコマンドを追加します。

```
yum install ipa-gothic-fonts ipa-mincho-fonts
```

### LibreOffice for Debianのインストール {#installing-libreoffice-for-debian}

Debianの場合、次の設定が必要です。

1. 次の標準パッケージをインストールします。

   ```
   apt-get install libreoffice-writer libreoffice-calc libreoffice-java-common
   ```

1. 次のフォントをインストールします（オプションですが、日本語インスタンスの場合は強くお勧めします）。

   ```
   apt-get install fonts-ipafont
   ```

### LibreOffice for CentOSのインストール {#installing-libreoffice-for-centos}

CentOSでは、次の設定が必要です。

1. 次の標準パッケージをインストールします。

   ```
   yum install libreoffice-headless libreoffice-writer libreoffice-calc
   ```

1. 次のフォントをインストールします（オプションですが、日本語インスタンスの場合は強くお勧めします）。

   ```
   yum install ipa-gothic-fonts ipa-mincho-fonts
   ```

## データベースアクセスレイヤー {#database-access-layers}

使用するデータベースエンジンのアクセス層は、サーバーにインストールされ、Adobe Campaignアカウントを介してアクセスできる必要があります。 バージョンとインストールモードは、使用するデータベースエンジンによって異なる場合があります。

サポートされているパイロットバージョンは、[互換性マトリックス](../../rn/using/compatibility-matrix.md)に詳述されています。

一般的な [Database](../../installation/using/database.md) セクションも確認します。

### PostgreSQL {#postgresql}

Adobe Campaignは、バージョン7.2のPostgreSQLクライアントライブラリの全バージョンをサポートしています。(**libpq.so.5**, libpq.so.4 **, libpq.so.3.2**, **libpq.so.3.2,** libpq.so.3.1 **** libpq.so.5)

Adobe CampaignでPostgreSQLを使用する場合は、対応する **pgcrypto** ライブラリをインストールする必要もあります。

### Oracle {#oracle}

64ビットDebianのライブラリバージョンを取得します。例： **libclntsh.so**、 **libclntsh.so.11.1** 、 **libclntsh.so.10.1**。

Linux RPMパッケージは、Oracle Technology Networkから入手できます。

>[!NOTE]
>
>Oracleクライアントを既にインストール済みで、グローバル環境(例：/etc/プロファイル)が正しく設定されていない場合は、nl6/customer.sh **scriptに足りない情報を追加できます。詳しくは、** 環境変数を参照してください [](../../installation/using/installing-packages-with-linux.md#environment-variables)。

**トラブルシューティングとベストプラクティス**

問題は、Oracleクライアントまたはサーバーの更新、バージョンの変更、またはインスタンスの最初のインストールの後に発生する可能性があります。

ログ、ワークフローの最後の処理、次の処理などに予期しない時間の遅れ（1時間以上）がクライアントコンソールで確認された場合は、OracleクライアントのライブラリとOracle Serverの間で問題が発生する可能性があります。 そのような問題を回避するには

1. 必ず **フルクライアントを使用してください**。

   Oracle Instant Clientバージョンを使用する場合、様々な問題が特定されています。 さらに、インスタントクライアントでTimezoneファイルを変更することはできません。

1. ク **ライアントのバージョン** と **データベースサーバーのバージョンが** 同じであることを確認します ****。

   Oracleの互換表にもかかわらず、異なるバージョンを混在させ、クライアントとサーバーのバージョンを一致させるための推奨事項が問題を引き起こすことがわかっています。

   また、ORACLE_HOME値をチェックして、期待されるクライアント・バージョン（マシンに複数のバージョンがインストールされている場合）を指していることを確認します。

1. クライアントとサーバーが同じ **タイムゾーンファイルを使用していることを確認します**。

### DB2 {#db2}

サポートされるライブラリのバージョンは **libdb2.so**&#x200B;です。

## 実装の手順 {#implementation-steps}

Linux用のAdobe Campaignのインストールは、次の順序で行う必要があります。サーバーのインストール後にインスタンスの設定が続きます。

この章では、インストールプロセスについて説明します。 インストール手順は次のとおりです。

* 手順1:アプリケーションサーバーのインストールについては、『Installing packages with Linux [](../../installation/using/installing-packages-with-linux.md)』を参照してください。
* 手順2:Webサーバーとの統合（デプロイされているコンポーネントに応じてオプション）。

インストール手順が完了したら、インスタンス、データベース、およびサーバーを設定する必要があります。 For more on this, refer to [About initial configuration](../../installation/using/about-initial-configuration.md).
