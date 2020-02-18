---
title: LinuxでのCampaignのインストールの前提条件
seo-title: LinuxでのCampaignのインストールの前提条件
description: LinuxでのCampaignのインストールの前提条件
seo-description: null
page-status-flag: never-activated
uuid: 65c7af3f-ca1d-4255-b54a-6a3c83af40ae
contentOwner: sauviat
products: SG_CAMPAIGN/CLASSIC
audience: installation
content-type: reference
topic-tags: installing-campaign-in-linux-
discoiquuid: 3e2ccb70-6c0c-435f-9c06-f3e5e40367bb
index: y
internal: n
snippet: y
translation-type: tm+mt
source-git-commit: de04b5d3ceb883a571ee665f630be931a68a5a3e

---


# LinuxでのCampaignのインストールの前提条件{#prerequisites-of-campaign-installation-in-linux}

## ソフトウェアの前提条件 {#software-prerequisites}

ここでは、Adobe Campaignをインストールする前に必要な設定の準備手順について説明します。

Adobe Campaignのインストールに必要な技術的およびソフトウェアの設定について詳しくは、互換性マトリック [スを参照してくださ](https://helpx.adobe.com/campaign/kb/compatibility-matrix.html)い。

注意：次のコンポーネントをインストールし、正しく設定する必要があります。

* Apache、『互換表 [』を参照](https://helpx.adobe.com/campaign/kb/compatibility-matrix.html)、
* Java JDKとOpenJDK、『 [Java開発キット — JDK](../../installation/using/application-server.md#java-development-kit---jdk)、
* ライブラリについては、 [Libraries](#libraries)、
* データベース・アクセス・レイヤー、「 [Database access layers](#database-access-layers)」を参照
* LibreOffice、『LibreOffice for Debianのインス [トール](#installing-libreoffice-for-debian) 』および『LibreOffice for CentOS [のインストール](#installing-libreoffice-for-centos)』を参照してください。
* フォントについては、「MTA統計用 [のフォント」および](#fonts-for-mta-statistics) 「日本語イン [スタンス用のフォント」を参照してください](#fonts-for-japanese-instances)。

>[!NOTE]
>
>CentOS 7およびDebian 8プラットフォームに8709以下のビルドをインストールするには、apache access_compatモジュールを有効にする必要があります。

### ライブラリ {#libraries}

LinuxにAdobe Campaignをインストールするには、必要なライブラリがあることを確認してください。

* ライブラリCは、TLS（スレッドローカルストレージ）モードをサポートできる必要があります。 このモードは、Xenのサポートが無効になっている一部のカーネルを除き、ほとんどの場合アクティブです。

   これを確認するには、 **uname -a| grep xen** （例：）

   コマンドが何も返さない（空行）場合は、設定が正しいことを意味します。

* OpenSSLのバー **ジョン0.9.8** または **1.0** が必要です。

   RHEL 7配布の場合は、OpenSSLのバージョン1.0が必要です。

* Adobe Campaignを使用するには、libicuライブラリをインストール **する** 必要があります。

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

使用する場合は、SELinuxモジュールを正しく設定する必要があります。

これを行うには、rootとしてログオンし、次のコマンドを入力します。

```
echo 0 >/selinux/enforce
```

さらに、 **** /etc/sysconfig/httpdファイルに、Adobe Campaign環境設定スクリプトを参照するために次の行が追加されました。

```
. ~neolane/nl6/env.sh
```

RHELおよびCentOSでは、SELinuxを有効にすると、データベースのクライアント層との互換性の問題が記録されていました。 Adobe Campaignが正しく動作することを確認するために、SELinuxを無効にすることをお勧めします。

**次のプロセスを適用します。**

* /etc/selinux/config **ファイルを編集します。**

* SELINUX行を次のように変更します。

```
SELINUX=disabled
```

### MTA統計用のフォント {#fonts-for-mta-statistics}

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

日本語のインスタンスでは、レポートをPDF形式に書き出すために、特定の文字のフォントが必要です。

Debianで、次のコマンドを追加します。

```
aptitude install fonts-ipafont
```

Red hatで、次のコマンドを追加します。

```
yum install ipa-gothic-fonts ipa-mincho-fonts
```

### LibreOffice for Debianのインストール {#installing-libreoffice-for-debian}

Debianの場合、次の設定が必要です。

1. 次の標準パッケージをインストールします。

   ```
   apt-get install libreoffice-writer libreoffice-calc libreoffice-java-common
   ```

1. 次のフォントをインストールします（オプションですが、日本語インスタンスには強くお勧めします）。

   ```
   apt-get install fonts-ipafont
   ```

### LibreOffice for CentOSのインストール {#installing-libreoffice-for-centos}

CentOSでは、次の設定が必要です。

1. 次の標準パッケージをインストールします。

   ```
   yum install libreoffice-headless libreoffice-writer libreoffice-calc
   ```

1. 次のフォントをインストールします（オプションですが、日本語インスタンスに強くお勧めします）。

   ```
   yum install ipa-gothic-fonts ipa-mincho-fonts
   ```

## データベース・アクセス・レイヤー {#database-access-layers}

使用するデータベースエンジンのアクセスレイヤーは、サーバーにインストールし、Adobe Campaignアカウントを使用してアクセスできる必要があります。 バージョンとインストールモードは、使用するデータベースエンジンによって異なる場合があります。

サポートされているパイロットバージョンは、[互換性マトリックス](https://helpx.adobe.com/campaign/kb/compatibility-matrix.html)に詳述されています。

また、「一般的なデータベース」セクション [も確認し](../../installation/using/database.md) ます。

### PostgreSQL {#postgresql}

Adobe Campaignは、バージョン7.2のPostgreSQLクライアントライブラリのすべてのバージョンをサポートしています。(**libpq.so.5**, **libpq.so.4**, libpq.so.3.2 **,** libpq.3.1 **** so.

Adobe CampaignでPostgreSQLを使用するには、対応する **pgcryptoライブラリをインストールする必要があります** 。

### Oracle {#oracle}

64ビットDebianのライブラリバージョンを取得します。例： **libclntsh.so**、 **libclntsh.so.11.1** 、 **libclntsh.so.10.1**。

Linux RPMパッケージは、Oracle Technology Networkから入手できます。

>[!NOTE]
>
>Oracleクライアントを既にインストールしているが、グローバル環境(例：/etc/profile)が正しく設定されていない場合は、nl6/customer.sh **scriptに足りない情報を追加できます。詳しくは、** Environment variablesを参照してください [](../../installation/using/installing-packages-with-linux.md#environment-variables)。

**トラブルシューティングとベストプラクティス**

問題は、Oracleクライアントまたはサーバーの更新後、バージョンの変更後、またはインスタンスの最初のインストール時に発生する可能性があります。

ログ、ワークフローの最後の処理、次の処理などに予期しない時間の遅延（1時間以上）がクライアントコンソールで発生している場合は、OracleクライアントのライブラリとOracle Serverの間で問題が発生する可能性があります。 そのような問題を避けるには

1. 完全なクライアントを必ず使 **用してください**。

   Oracle Instant clientバージョンを使用する際に、様々な問題が特定されました。 さらに、インスタントクライアントでTimezoneファイルを変更することはできません。

1. クライアントのバージョン **とデータベース** ・サーバーのバー **ジョンが同じであることを確** 認します ****。

   Oracleの互換性マトリックスに関係なく複数のバージョンを混在させ、クライアントとサーバーのバージョンを一致させることがわかっている。

   また、ORACLE_HOMEの値をチェックして、期待されるクライアント・バージョン（マシンに複数のバージョンがインストールされている場合）を指していることを確認します。

1. クライアントとサーバーが同じタイムゾーンファイルを使用しているこ **とを確認しま**&#x200B;す。

### DB2 {#db2}

サポートされるライブラリ **のバージョンはlibdb2.soです**。

## 実装の手順 {#implementation-steps}

Linux版Adobe Campaignのインストールは、次の順序で実行する必要があります。サーバーのインストール後にインスタンスの設定を行います。

この章では、インストールプロセスについて説明します。 インストール手順は次のとおりです。

* 手順1:アプリケーションサーバーのインストールについては、 [Installing packages with Linuxを参照してください](../../installation/using/installing-packages-with-linux.md)。
* 手順2:Webサーバーとの統合（デプロイされているコンポーネントに応じてオプション）。

インストール手順が完了したら、インスタンス、データベース、およびサーバーを設定する必要があります。 For more on this, refer to [About initial configuration](../../installation/using/about-initial-configuration.md).
