---
product: campaign
title: サーバーのインストール
description: サーバーのインストール
feature: Installation, Instance Settings
badge-v7-prem: label="オンプレミス／ハイブリッドのみ" type="Caution" url="https://experienceleague.adobe.com/docs/campaign-classic/using/installing-campaign-classic/architecture-and-hosting-models/hosting-models-lp/hosting-models.html?lang=ja" tooltip="オンプレミスデプロイメントとハイブリッドデプロイメントにのみ適用されます"
audience: installation
content-type: reference
topic-tags: installing-campaign-in-windows-
exl-id: c0cb4efa-cae9-4312-88fb-738857a89595
source-git-commit: b7dedddc080d1ea8db700fabc9ee03238b3706cc
workflow-type: tm+mt
source-wordcount: '425'
ht-degree: 3%

---

# サーバーのインストール{#installing-the-server}

## インストールプログラムの実行 {#executing-the-installation-program}

Windows 32 ビットプラットフォームの場合は、Adobe Campaign 32 ビットをインストールします。 Windows 64 ビット版のプラットフォームの場合は、Adobe Campaign 64 ビット版をインストールします。

Adobe Campaign サーバーのインストール手順は次のとおりです。

1. ファイルを実行します **setup.exe**.

   ![](assets/s_ncs_install_installer_01.png)

1. インストールの種類を選択します。

   ![](assets/s_ncs_install_installer_01a.png)

   次の複数のインストールタイプを使用できます。

   * **[!UICONTROL アプリケーションサーバーのインストール]** :Adobe Campaign アプリケーションサーバーとクライアントコンソールをインストールします。
   * **[!UICONTROL 最小インストール（ネットワーク）]** ：ネットワークからのクライアントコンピューターのインストール。 必要に応じて、限られた数の DLL のみがコンピュータにインストールされ、他のすべてのコンポーネントはネットワークドライブから使用されます。
   * **[!UICONTROL クライアントのインストール]** :Adobe Campaign クライアントに必要なコンポーネントのインストール。
   * **[!UICONTROL カスタムインストール]** ：インストールする要素をユーザーが選択します。

   を選択 **アプリケーションサーバーのインストール**&#x200B;をクリックし、次に示すように様々な手順を実行します。

   ![](assets/s_ncs_install_installer_02.png)

1. インストール ディレクトリの選択：

   ![](assets/s_ncs_install_installer_03.png)

1. クリック **[!UICONTROL 終了]** インストールを開始するには：

   ![](assets/s_ncs_install_installer_04.png)

   進行状況バーに、インストールの進行状況が表示されます。

   ![](assets/s_ncs_install_installer_05.png)

   インストールが完了すると、次の内容を知らせるメッセージが表示されます。

   ![](assets/s_ncs_install_installer_06.png)

   >[!NOTE]
   >
   >サーバのインストールが完了したら、ネットワークの問題を回避するためにサーバを再起動する必要があります。

   インストールが完了したら、Adobe Campaignを起動して設定ファイルを作成します。 こちらを参照してください [サーバーの初回起動](#first-start-up-of-the-server).

## 概要インストールテスト {#summary-installation-testing}

最初のインストールをテストするには、次のコマンドを使用します。

```sql
nlserver pdump
```

Adobe Campaignが起動されていない場合は、次のように応答します。

```sql
No task
```

## サーバーの初回起動 {#first-start-up-of-the-server}

インストールテストが完了したら、 **[!UICONTROL スタート/プログラム/Adobe Campaign]** メニューをクリックし、次のコマンドを入力します。

```sql
nlserver web
```

インストールディレクトリ内のファイルは、Adobe Campaign サーバーモジュールの設定に使用されます。

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

```sql
nlserver start web
```

次の情報が表示されます。

```sql
12:17:21 >   Application server for Adobe Campaign Classic (7.X YY.R build XXX@SHA1) of DD/MM/YYYY
12:17:21 >   Start of the 'web@default' ('nlserver web -tracefile:web@default -instance:default -detach -tomcat -autorepair') task in a new process 
12:17:21 >   Application server for Adobe Campaign Classic (7.X YY.R build XXX@SHA1) of DD/MM/YYYY
12:17:21 >   Web server start (pid=29188, tid=-1224824320)...
12:17:21 >   Generation of configuration changes '[INSTALL]bin..confserverConf.xml.diff' between '[INSTALL]bin..confserverConf.xml' and '[INSTALL]bin..conffraserverConf.xml.sample'
12:17:22 >   Tomcat started
12:17:22 >   Server started
```

停止するには、次のように入力します。

```sql
nlserver stop web
```

次の情報が表示されます。

```sql
12:18:31 >   Application server for Adobe Campaign Classic (7.X YY.R build XXX@SHA1) of DD/MM/YYYY
12:18:31 >   Stop requested for 'web@default' ('nlserver web -tracefile:web@default -instance:default -detach -tomcat -autorepair', pid=29188, tid=-1224824320)...
12:18:31 >   Stop requested (pid=29188)
12:18:31 >   Web server stopped (pid=29188, tid=-1224824320)...
```

## 内部識別子のパスワード {#password-for-the-internal-identifier}

Adobe Campaign サーバーは、というテクニカルログインを定義します。 **内部** すべてのインスタンスに対してすべての権限を持っています。 インストール直後は、ログインにパスワードがありません。 定義する必要があります。

詳しくは、[こちら](../../installation/using/configuring-campaign-server.md#internal-identifier)を参照してください。

## Adobe Campaign サービスの開始 {#starting-adobe-campaign-services}

Adobe Campaign サービスを開始するには、サービスマネージャーを使用するか、コマンドラインで適切な権限を持つ以下を入力します。

```sql
net start nlserver6
```

Adobe Campaign プロセスを後で停止する必要がある場合は、次のコマンドを使用します。

```sql
net stop nlserver6
```

## LibreOffice のインストール {#installing-libreoffice}

LibreOffice をダウンロードし、通常のインストール手順に従います。

次の環境変数を追加します。

```sql
OOO_BASIS_INSTALL_DIR="C:\Program Files (x86)\LibreOffice 6\"
```
