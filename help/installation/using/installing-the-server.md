---
product: campaign
title: サーバーのインストール
description: サーバーのインストール
audience: installation
content-type: reference
topic-tags: installing-campaign-in-windows-
exl-id: c0cb4efa-cae9-4312-88fb-738857a89595
source-git-commit: 20509f44c5b8e0827a09f44dffdf2ec9d11652a1
workflow-type: tm+mt
source-wordcount: '421'
ht-degree: 3%

---

# サーバーのインストール{#installing-the-server}

![](../../assets/v7-only.svg)

## インストールプログラムの実行 {#executing-the-installation-program}

Windows 32 ビットプラットフォームの場合、Adobe Campaign 32 ビットをインストールします。 Windows 64 ビットプラットフォームの場合、Adobe Campaign 64 ビットをインストールします。

Adobe Campaignサーバーのインストール手順は次のとおりです。

1. ファイルを実行します **setup.exe**.

   ![](assets/s_ncs_install_installer_01.png)

1. インストールタイプを選択します。

   ![](assets/s_ncs_install_installer_01a.png)

   次のインストールタイプを使用できます。

   * **[!UICONTROL アプリケーションサーバーのインストール]** :Adobe Campaignアプリケーションサーバーとクライアントコンソールをインストールします。
   * **[!UICONTROL 最小インストール（ネットワーク）]** :ネットワークからのクライアントコンピューターのインストール。 必要に応じて、限られた数の DLL のみがコンピュータにインストールされ、その他のすべてのコンポーネントはネットワークドライブから使用されます。
   * **[!UICONTROL クライアントのインストール]** :Adobe Campaignクライアントに必要なコンポーネントのインストール。
   * **[!UICONTROL カスタムインストール]** :ユーザーは、インストールする要素を選択します。

   選択 **アプリケーションサーバーのインストール**&#x200B;を開き、次に示す様々な手順を実行します。

   ![](assets/s_ncs_install_installer_02.png)

1. インストールディレクトリを選択します。

   ![](assets/s_ncs_install_installer_03.png)

1. クリック **[!UICONTROL 完了]** インストールを開始するには：

   ![](assets/s_ncs_install_installer_04.png)

   プログレスバーには、インストールの範囲が表示されます。

   ![](assets/s_ncs_install_installer_05.png)

   インストールが完了すると、次の情報を示すメッセージが表示されます。

   ![](assets/s_ncs_install_installer_06.png)

   >[!NOTE]
   >
   >サーバーのインストールが完了したら、ネットワークの問題を回避するために、サーバーを再起動する必要があります。

   インストールが完了したら、Adobe Campaignを起動して設定ファイルを作成します。 参照： [サーバーの最初の起動](#first-start-up-of-the-server).

## インストールテストの概要 {#summary-installation-testing}

次のコマンドを使用して、初期インストールをテストできます。

```
nlserver pdump
```

Adobe Campaignが起動していない場合の応答は次のようになります。

```
No task
```

## サーバーの最初の起動 {#first-start-up-of-the-server}

インストールテストが完了したら、 **[!UICONTROL スタート/プログラム/Adobe Campaign]** メニューを開き、次のコマンドを入力します。

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

押す **Ctrl+C** プロセスを停止するには、次のコマンドを入力します。

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

Adobe Campaignサーバーは、 **内部** すべてのインスタンスに対するすべての権限を持つ インストール直後に、ログインにパスワードが含まれていません。 定義する必要があります。

詳しくは、[この節](../../installation/using/configuring-campaign-server.md#internal-identifier)を参照してください。

## Adobe Campaign Services の開始 {#starting-adobe-campaign-services}

Adobe Campaignサービスを開始するには、サービスマネージャーを使用するか、（適切な権限を持つ）コマンドラインで次のように入力します。

```
net start nlserver6
```

後でAdobe Campaignプロセスを停止する必要がある場合は、次のコマンドを使用します。

```
net stop nlserver6
```

## LibreOffice のインストール {#installing-libreoffice}

LibreOffice をダウンロード（例： ） [https://www.libreoffice.org/download/libreoffice-fresh/](https://www.libreoffice.org/download/libreoffice-fresh/) をクリックし、通常のインストール手順に従います。

次の環境変数を追加します。

```
OOO_BASIS_INSTALL_DIR="C:\Program Files (x86)\LibreOffice 6\"
```
