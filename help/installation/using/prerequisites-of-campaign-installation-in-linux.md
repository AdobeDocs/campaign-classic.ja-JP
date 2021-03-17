---
solution: Campaign Classic
product: campaign
title: Linux での Campaign のインストールの前提条件
description: Linux での Campaign のインストールの前提条件
audience: installation
content-type: reference
topic-tags: installing-campaign-in-linux-
translation-type: tm+mt
source-git-commit: ae4b2ba6db140cdfb9ec4a38231fcc3e54b1478c
workflow-type: tm+mt
source-wordcount: '896'
ht-degree: 3%

---


# Linuxにキャンペーンをインストールするための前提条件{#prerequisites-of-campaign-installation-in-linux}

## ソフトウェアの前提条件{#software-prerequisites}

このセクションでは、Adobe Campaignをインストールする前に必要な設定の暫定手順について説明します。

Adobe Campaignのインストールに必要な技術的およびソフトウェアの設定については、[互換表](../../rn/using/compatibility-matrix.md)を参照してください。

注意：次のコンポーネントをインストールし、正しく設定する必要があります。

* Apache、[互換表](../../rn/using/compatibility-matrix.md)を参照。
* Java JDKとOpenJDK、『Java Development Kit - JDK](../../installation/using/application-server.md#java-development-kit---jdk),[
* ライブラリ， [ライブラリ](#libraries)を参照，
* データベース・アクセス・レイヤー。[データベース・アクセス・レイヤー](#database-access-layers)を参照してください。
* LibreOffice、[LibreOffice for Debianのインストール](#installing-libreoffice-for-debian)および[LibreOffice for CentOSのインストール](#installing-libreoffice-for-centos)を参照してください。
* フォントについては、[MTA統計用のフォント](#fonts-for-mta-statistics)および[日本語インスタンス用のフォント](#fonts-for-japanese-instances)を参照してください。

>[!NOTE]
>
>CentOS 7およびDebian 8プラットフォームに8709以下のビルドをインストールするには、apache access_compatモジュールを有効にする必要があります。

### ライブラリ{#libraries}

LinuxにAdobe Campaignをインストールするには、必要なライブラリがあることを確認してください。

* ライブラリCは、TLS(スレッドローカルストレージ)モードをサポートできる必要があります。 このモードは、Xenのサポートが無効になっているカーネルを除き、ほとんどの場合アクティブです。

   これを確認するには、**uname -a | grep xen**&#x200B;コマンドの例を示します。

   コマンドが何も返さない（空行）場合は、設定が正しいことを意味します。

* OpenSSLの&#x200B;**バージョン0.9.8**&#x200B;または&#x200B;**1.0**&#x200B;が必要です。

   RHEL 7ディストリビューションの場合は、OpenSSLのバージョン1.0が必要です。

* Adobe Campaignを使用するには、**libicu**&#x200B;ライブラリをインストールする必要があります。

   **libicu**&#x200B;の次のバージョンがサポートされています（32bitまたは64bit）。

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

これに加えて、**/etc/sysconfig/httpd**&#x200B;ファイルには、Adobe Campaign環境設定スクリプトを参照する次の行が追加されています。

```
. ~neolane/nl6/env.sh
```

RHELおよびCentOSでは、SELinuxを有効にすると、データベースのクライアント層との互換性の問題が報告されていました。 Adobe Campaignが正しく動作するように、SELinuxを無効にすることをお勧めします。

**次のプロセスを適用します。**

* ファイル&#x200B;**/etc/selinux/config**&#x200B;を編集します。

* SELINUX行を次のように変更します。

```
SELINUX=disabled
```

### MTA統計用フォント{#fonts-for-mta-statistics}

MTA統計(nms/fra/jsp/stat.jsp)のレポートを正しく表示するには、フォントを追加します。

Debianで、次のコマンドを追加します。

```
aptitude install xfonts-base xfonts-75dpi ttf-bitstream-vera ttf-dejavu
```

Redhatで、次のコマンドを使用します。

```
yum install xorg-x11-fonts-base xorg-x11-fonts-75dpi bitstream-vera-fonts dejavu-lgc-fonts
```

### 日本語インスタンスのフォント{#fonts-for-japanese-instances}

レポートをPDF形式に書き出すには、日本のインスタンスで特定の文字のフォントが必要です。

Debianで、次のコマンドを追加します。

```
aptitude install fonts-ipafont
```

Red Hatで、次のコマンドを追加します。

```
yum install ipa-gothic-fonts ipa-mincho-fonts
```

### LibreOffice for Debianのインストール{#installing-libreoffice-for-debian}

Debianの場合、次の設定が必要です。

1. 次の標準パッケージをインストールします。

   ```
   apt-get install libreoffice-writer libreoffice-calc libreoffice-java-common
   ```

1. 次のフォントをインストールします（オプションですが、日本語インスタンスの場合は強くお勧めします）。

   ```
   apt-get install fonts-ipafont
   ```

### LibreOffice for CentOSのインストール{#installing-libreoffice-for-centos}

CentOSでは、次の設定が必要です。

1. 次の標準パッケージをインストールします。

   ```
   yum install libreoffice-headless libreoffice-writer libreoffice-calc
   ```

1. 次のフォントをインストールします（オプションですが、日本語インスタンスの場合は強くお勧めします）。

   ```
   yum install ipa-gothic-fonts ipa-mincho-fonts
   ```

## データベースアクセス層{#database-access-layers}

使用するデータベースエンジンのアクセス層は、サーバーにインストールされ、Adobe Campaignアカウントを介してアクセスできる必要があります。 バージョンとインストールモードは、使用するデータベースエンジンによって異なる場合があります。

サポートされているパイロットバージョンは、[互換性マトリックス](../../rn/using/compatibility-matrix.md)に詳述されています。

[データベース](../../installation/using/database.md)の一般セクションも確認します。

### PostgreSQL {#postgresql}

Adobe Campaignは、バージョン7.2のPostgreSQLクライアントライブラリの全バージョンをサポートしています。(**libpq.so.5**、**libpq.so.4**、**libpq.so.3.2**、**libpq.so.3.1**)。

Adobe CampaignでPostgreSQLを使用するには、対応する&#x200B;**pgcrypto**&#x200B;ライブラリをインストールする必要もあります。

### Oracle {#oracle}

64ビットDebianのライブラリバージョンを取得します。例：**libclntsh.so**、**libclntsh.so.11.1**、**libclntsh.so.10.1**。

Linux RPMパッケージは、Oracleテクノロジーネットワークから入手できます。

>[!NOTE]
>
>oracleクライアントを既にインストールしているが、グローバル環境(例：/etc/プロファイル)が正しく設定されていない場合は、**nl6/customer.sh**&#x200B;スクリプトに、足りない情報を追加できます。詳しくは、[環境変数](../../installation/using/installing-packages-with-linux.md#environment-variables)を参照してください。

**トラブルシューティングとベストプラクティス**

問題は、Oracleクライアントまたはサーバーの更新、バージョンの変更の後、またはインスタンスの最初のインストール時に発生する可能性があります。

ログ、ワークフローの最後の処理、次の処理などに予期しない時間の遅れ（1時間以上）がクライアントコンソールで認識された場合は、OracleクライアントのライブラリとOracleサーバーの間で問題が発生する可能性があります。 そのような問題を回避するには

1. **完全なクライアント**&#x200B;を必ず使用してください。

   oracleインスタントクライアントのバージョンを使用する際に、様々な問題が見つかりました。 さらに、インスタントクライアントでTimezoneファイルを変更することはできません。

1. **クライアントバージョン**&#x200B;と&#x200B;**データベースサーバーバージョン**&#x200B;が&#x200B;**同じ**&#x200B;であることを確認してください。

   oracleの互換表にもかかわらず、バージョンを混在させ、クライアントとサーバーのバージョンを一致させるための推奨事項を示すことが、問題の原因として知られています。

   また、ORACLE_HOMEの値をチェックして、期待されるクライアントのバージョン（マシンに複数のバージョンがインストールされている場合）を指しているかどうかを確認します。

1. クライアントとサーバーが同じ&#x200B;**タイムゾーンファイル**&#x200B;を使用していることを確認します。

### DB2 {#db2}

サポートされているライブラリのバージョンは&#x200B;**libdb2.so**&#x200B;です。

## 実装手順 {#implementation-steps}

Linux用のAdobe Campaignのインストールは、次の順序で行う必要があります。サーバーのインストール後にインスタンスの設定が続きます。

この章では、インストールプロセスについて説明します。 インストール手順は次のとおりです。

* 手順1:アプリケーションサーバーのインストールについては、[Installing packages with Linux](../../installation/using/installing-packages-with-linux.md)を参照してください。
* 手順2:Webサーバーとの統合（デプロイされているコンポーネントに応じてオプション）。

インストール手順が完了したら、インスタンス、データベース、およびサーバーを設定する必要があります。 詳しくは、[初期設定](../../installation/using/about-initial-configuration.md)についてを参照してください。
