---
title: サーバーのインストール
seo-title: サーバーのインストール
description: サーバーのインストール
seo-description: null
page-status-flag: never-activated
uuid: 02534211-c267-490d-b9c1-78f56f1284e1
contentOwner: sauviat
products: SG_CAMPAIGN/CLASSIC
audience: installation
content-type: reference
topic-tags: installing-campaign-in-windows-
discoiquuid: d1510fd9-995b-46c6-8d57-e1fe3999235e
translation-type: tm+mt
source-git-commit: 70b143445b2e77128b9404e35d96b39694d55335
workflow-type: tm+mt
source-wordcount: '423'
ht-degree: 2%

---


# サーバーのインストール{#installing-the-server}

## インストールプログラムの実行 {#executing-the-installation-program}

Windows 32ビットプラットフォームの場合は、Adobe Campaign32ビットをインストールします。 Windows 64ビットプラットフォームの場合は、Adobe Campaign64ビットをインストールします。

Adobe Campaignサーバーのインストール手順は次のとおりです。

1. ファイル **setup.exeを実行します**。

   ![](assets/s_ncs_install_installer_01.png)

1. インストールの種類を選択します。

   ![](assets/s_ncs_install_installer_01a.png)

   次のインストールタイプを使用できます。

   * **[!UICONTROL アプリケーションサーバーのインストール]** :Adobe Campaignアプリケーションサーバーとクライアントコンソールをインストールします。
   * **[!UICONTROL 最小インストール（ネットワーク）]** :ネットワークからのクライアントコンピューターのインストール。 必要に応じて、限られた数のDLLだけがコンピュータにインストールされ、その他のコンポーネントはすべてネットワークドライブから使用されます。
   * **[!UICONTROL クライアントのインストール]** :Adobe Campaignクライアントに必要なコンポーネントのインストール。
   * **[!UICONTROL カスタムインストール]** :ユーザーは、インストールする要素を選択します。

   「 **Installation of an application server**」を選択し、次に示す別の手順に従います。

   ![](assets/s_ncs_install_installer_02.png)

1. インストールディレクトリを選択します。

   ![](assets/s_ncs_install_installer_03.png)

1. Click **[!UICONTROL Finish]** to start the installation:

   ![](assets/s_ncs_install_installer_04.png)

   進行状況バーには、インストールの範囲が表示されます。

   ![](assets/s_ncs_install_installer_05.png)

   インストールが完了すると、次のことを知らせるメッセージが表示されます。

   ![](assets/s_ncs_install_installer_06.png)

   >[!NOTE]
   >
   >サーバのインストールが完了したら、ネットワークの問題を回避するために、サーバの再起動が必要です。

   インストールが完了したら、開始Adobe Campaignを使用して設定ファイルを作成します。 「サーバの [最初の開始アップ](#first-start-up-of-the-server)」を参照してください。

## インストールの概要テスト {#summary-installation-testing}

次のコマンドを使用して、初期インストールをテストできます。

```
nlserver pdump
```

Adobe Campaignが開始されていない場合、応答は次のようになります。

```
No task
```

## サーバーの最初の開始アップ {#first-start-up-of-the-server}

インストールテストが完了したら、 **[!UICONTROL 開始/プログラム/Adobe Campaign]** メニューでコマンドプロンプトを開き、次のコマンドを入力します。

```
nlserver web
```

![](assets/s_ncs_install_cmd_nlserverweb.png)

インストールディレクトリ内のファイルは、Adobe Campaignサーバーモジュールの設定に使用されます。

次の情報が表示されます。

```
15:30:12 >   Application server for Adobe Campaign Classic (7.X YY.R build XXX@SHA1) of DD/MM/YYYY
15:30:12 >   Web server start (pid=664, tid=4188)...
15:30:12 >   Creation of server configuration file '[INSTALL]bin..confserverConf.xml' server via '[INSTALL]bin..conffraserverConf.xml.sample
15:30:12 >   Creation of server configuration file '[INSTALL]bin..confconfig-default.xml' server via '[INSTALL]bin..confmodelsconfig-default.xml
15:30:12 >   Server started
15:30:12 >   Stop requested (pid=664)
15:30:12 >   Web server stop (pid=664, tid=4188)...
```

Ctrl **** +Cを押して処理を停止し、次のコマンドを入力します。

```
nlserver start web
```

次の情報が表示されます。

```
12:17:21 >   Application server for Adobe Campaign Classic (7.X YY.R build XXX@SHA1) of DD/MM/YYYY
12:17:21 >   Start of the 'web@default' ('nlserver web -tracefile:web@default -instance:default -detach -tomcat -autorepair') task in a new process 
12:17:21 >   Application server for Adobe Campaign Classic (7.X YY.R build XXX@SHA1) of DD/MM/YYYY
12:17:21 >   Web server start (pid=29188, tid=-1224824320)...
12:17:21 >   Generation of configuration changes '[INSTALL]bin..confserverConf.xml.diff' between '[INSTALL]bin..confserverConf.xml' and '[INSTALL]bin..conffraserverConf.xml.sample'
12:17:22 >   Tomcat started
12:17:22 >   Server started
```

停止するには、次のように入力します。

```
nlserver stop web
```

次の情報が表示されます。

```
12:18:31 >   Application server for Adobe Campaign Classic (7.X YY.R build XXX@SHA1) of DD/MM/YYYY
12:18:31 >   Stop requested for 'web@default' ('nlserver web -tracefile:web@default -instance:default -detach -tomcat -autorepair', pid=29188, tid=-1224824320)...
12:18:31 >   Stop requested (pid=29188)
12:18:31 >   Web server stopped (pid=29188, tid=-1224824320)...
```

## 内部識別子のパスワード {#password-for-the-internal-identifier}

Adobe Campaignサーバは、すべてのインスタンスに対してすべての権限を持つ **internal** という技術的なログインを定義します。 インストール直後は、ログインにパスワードがありません。 定義する必要があります。

「 [内部識別子](../../installation/using/campaign-server-configuration.md#internal-identifier)」を参照してください。

## Starting Adobe Campaign services {#starting-adobe-campaign-services}

Adobe Campaignサービスを開始するには、サービスマネージャを使用するか、コマンドラインで次のように入力します（適切な権限を持ちます）。

```
net start nlserver6
```

後でAdobe Campaignプロセスを停止する必要がある場合は、次のコマンドを使用します。

```
net stop nlserver6
```

## LibreOfficeのインストール {#installing-libreoffice}

例えば、https://www.libreoffice.org/download/libreoffice-fresh/ [からLibreOfficeをダウンロードし](https://www.libreoffice.org/download/libreoffice-fresh/) 、通常のインストール手順に従います。

追加次の環境変数：

```
OOO_BASIS_INSTALL_DIR="C:\Program Files (x86)\LibreOffice 6\"
```

