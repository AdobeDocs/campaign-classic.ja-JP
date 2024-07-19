---
product: campaign
title: Linux での Campaign インストールの前提条件
description: Linux での キャンペーン インストールの前提条件
feature: Installation, Instance Settings
badge-v7-prem: label="オンプレミス／ハイブリッドのみ" type="Caution" url="https://experienceleague.adobe.com/docs/campaign-classic/using/installing-campaign-classic/architecture-and-hosting-models/hosting-models-lp/hosting-models.html?lang=ja" tooltip="オンプレミスデプロイメントとハイブリッドデプロイメントにのみ適用されます"
audience: installation
content-type: reference
topic-tags: installing-campaign-in-linux-
exl-id: acbd2873-7b1c-4d81-bc62-cb1246c330af
source-git-commit: f032ed3bdc0b402c8281bc34e6cb29f3c575aaf9
workflow-type: tm+mt
source-wordcount: '829'
ht-degree: 3%

---

# Linux に Campaign をインストールするための前提条件{#prerequisites-of-campaign-installation-in-linux}

## ソフトウェアの前提条件 {#software-prerequisites}

この節では、Adobe Campaignをインストールする前に必要な事前設定手順について説明します。

Adobe Campaignのインストールに必要な技術的およびソフトウェア設定について詳しくは、[ 互換性マトリックス ](../../rn/using/compatibility-matrix.md) を参照してください。

次のコンポーネントをインストールし、正しく設定する必要があります。

* Apache、[ 互換性マトリックス ](../../rn/using/compatibility-matrix.md) を参照してください。
* Java JDK および OpenJDK については、[Java Development Kit - JDK](../../installation/using/application-server.md#jdk) を参照してください。
* ライブラリについては、[ ライブラリ ](#libraries) を参照してください。
* データベースアクセスレイヤーについては、[ データベースアクセスレイヤー ](#database-access-layers) を参照してください。
* LibreOffice。[Debian 用 LibreOffice のインストール ](#installing-libreoffice-for-debian) および [CentOS 用 LibreOffice のインストール ](#installing-libreoffice-for-centos) を参照してください。
* フォントについては、[MTA 統計のフォント ](#fonts-for-mta-statistics) および [ 日本語インスタンスのフォント ](#fonts-for-japanese-instances) を参照してください。


### ライブラリ {#libraries}

LinuxにAdobe Campaignをインストールするには、必要なライブラリがあることを確認してください。

* Library C は TLS (スレッドローカルストレージ) モードをサポートできなければなりません。 このモードは、Xen サポートが無効になっている一部のカーネルを除いて、ほとんどの場合アクティブです。

  これを確認するには、例えば **uname -a | grep xen** コマンドを使用します。

  コマンドが空行を返さない場合は、設定が正しいことを意味します。

* OpenSSL バージョン **1.0.2** 以降が必要です。

  RHEL ディストリビューションの場合、OpenSSL のバージョン 1.0 が必要です。

* Adobe Campaignを使用するには、**libicu** ライブラリがインストールされている必要があります。

### SELinux {#selinux}

使用する場合は、SELinux モジュールを適切に設定する必要があります。

これを行うには、root としてログオンし、次のコマンドを入力します。

```
echo 0 >/selinux/enforce
```

これに加えて、**/etc/sysconfig/httpd** ファイルで、Adobe Campaign環境設定スクリプトを参照するために、次の行が追加されました。

```
. ~neolane/nl6/env.sh
```

RHEL および CentOS では、SELinux が有効な場合、データベースのクライアントレイヤーの互換性の問題が見られました。 Adobe Campaignを正しく動作させるには、SELinux を無効にすることをお勧めします。

**次のプロセスを適用します。**

* ファイル **/etc/selinux/config** を編集します。

* SELINUX 行を次のように変更します。

```
SELINUX=disabled
```

### MTA 統計のフォント {#fonts-for-mta-statistics}

MTA 統計（nms/fra/jsp/stat.jsp）に関するレポートを正しく表示するには、フォントを追加します。

Debian で、次のコマンドを追加します。

```
apt install xfonts-base xfonts-75dpi ttf-bitstream-vera ttf-dejavu
```

RHEL に次のコマンドを使用します。

```
dnf install xorg-x11-fonts-misc xorg-x11-fonts-75dpi dejavu-lgc-sans-fonts  dejavu-sans-fonts dejavu-sans-mono-fonts dejavu-serif-fonts
```

### 日本語インスタンス用のフォント {#fonts-for-japanese-instances}

レポートを PDF 形式にエクスポートするには、日本語インスタンスで特定の文字フォント必要があります。

Debian で次のコマンドを追加します:

```
apt install fonts-ipafont
```

RHEL の場合は、次のコマンドを追加します。

```
dnf install epel-release # if required
dnf install vlgothic-fonts
```

### LibreOffice for Debian のインストール {#installing-libreoffice-for-debian}

Debian の場合、次の設定が必要です。

1. 次の標準パッケージをインストールします。

   ```
   apt-get install libreoffice-writer libreoffice-calc libreoffice-java-common
   ```

1. 次のフォントをインストールします(オプションですが、日本語インスタンスの場合は強く推奨します)。

   ```
   apt-get install fonts-ipafont
   ```

### LibreOffice for CentOS のインストール {#installing-libreoffice-for-centos}

CentOS を使用する場合は、以下の設定が必要です。

```
yum install libreoffice-headless libreoffice-writer libreoffice-calc
```

## データベース アクセス層 {#database-access-layers}

使用するデータベース エンジンのアクセス レイヤーは、サーバーにインストールされ、Adobe Campaign アカウントからアクセスできる必要があります。 バージョンとインストールモードは、使用するデータベースエンジンによって異なる場合があります。

サポートされているパイロットバージョンは、[互換性マトリックス](../../rn/using/compatibility-matrix.md)に詳述されています。

また、一般的な [ データベース ](../../installation/using/database.md) セクションも確認してください。

### PostgreSQL {#postgresql}

Adobe Campaignは、バージョン 9.6 以降の PostgreSQL クライアントライブラリのすべてのバージョン（**libpq.so.5**）をサポートします。

Adobe Campaignで PostgreSQL を使用するには、対応する **pgcrypto** ライブラリもインストールする必要があります。

### Oracle {#oracle}

64 ビット Debian 用の ライブラリ バージョン、すなわち **libclntsh.so**、 **libclntsh.so.19.1**、 **libclntsh.so.18.1**、 **libclntsh.so.12.1**、 **libclntsh.so.11.1** または **libclntsh.so.10.1** を取得します。

Linux RPM パッケージは、Oracle Technology Network から入手できます。

>[!NOTE]
>
>Oracle クライアントを既にインストールしているが、グローバル環境(インスタンス の場合:/etc/プロファイル)が正しく設定されていない場合は、不足している情報を **nl6/顧客.sh** スクリプトに追加できます。 詳しくは、 [環境変数を参照してください](../../installation/using/installing-packages-with-linux.md#environment-variables)。

**トラブルシューティングとベストプラクティス**

問題は、Oracleクライアントまたはサーバーのアップデート、バージョンの変更の後、またはインスタンスの初回インストール時に発生する場合があります。

クライアントコンソールでログ、ワークフローの最終処理、次回の処理などに予期しないタイムラグ（1 時間以上）があることに気付いた場合は、OracleクライアントのライブラリとOracleサーバーの間で問題が発生している可能性があります。 このような問題を回避するには

1. 必ず **full client** を使用してください。

   Oracle インスタントクライアントバージョンの使用時に様々な問題が特定されています。 さらに、インスタントクライアントでタイムゾーンファイルを変更することはできません。

1. **クライアントのバージョン**&#x200B;と&#x200B;**データベースサーバーのバージョン**&#x200B;が&#x200B;**同じ**&#x200B;であることを確認します。

   oracleの互換表に反してバージョンを混在させ、クライアントとサーバのバージョンを整合させることを推奨すると、問題が発生することが知られています。

   また、ORACLE_HOME の値をチェックして、期待されるクライアントバージョンを指していることを確認します（マシンに複数のバージョンがインストールされている場合）。

1. クライアントとサーバーで同じ **タイムゾーンファイル** が使用されていることを確認します。

## 実装手順 {#implementation-steps}

Linux 用のAdobe Campaignのインストールは、サーバーのインストールに続いてインスタンスの設定の順序で実行する必要があります。

インストールプロセスについては、この章で説明します。 インストール手順は次のとおりです。

* 手順 1：アプリケーションサーバーのインストール。[Linux でのパッケージのインストール ](../../installation/using/installing-packages-with-linux.md) を参照してください。
* 手順 2:web サーバーとの統合（デプロイされているコンポーネントに応じてオプションで使用可能）

インストール手順が完了したら、インスタンス、データベース、サーバーを設定する必要があります。 詳しくは、[ 初期設定について ](../../installation/using/about-initial-configuration.md) を参照してください。
