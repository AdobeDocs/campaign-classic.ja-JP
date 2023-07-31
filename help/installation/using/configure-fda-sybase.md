---
product: campaign
title: Sybase IQ へのアクセスを設定する
description: FDA でのSybase IQへのアクセスの設定方法を説明します
feature: Installation, Federated Data Access
badge-v7-only: label="v7" type="Informative" tooltip="Campaign Classicv7 にのみ適用"
audience: platform
content-type: reference
topic-tags: connectors
exl-id: 0fdf8259-5cab-4a9d-adb3-6c55ec5c8851
source-git-commit: 3a9b21d626b60754789c3f594ba798309f62a553
workflow-type: tm+mt
source-wordcount: '342'
ht-degree: 66%

---

# Sybase IQ へのアクセスを設定する {#configure-access-to-sybase-iq}



キャンペーンを使用 **Federated Data Access** (FDA) 外部データベースに保存されている情報を処理するオプション。 次の手順に従って、Sybase IQへのアクセスを設定します。

1. 設定 [Sybase IQデータベース](#configuring-sybase)
1. sybase IQの設定 [外部アカウント](#sybase-external) Campaign 内

## Sybase IQ設定 {#configuring-sybase}

FDA で外部Sybase IQベースに接続するには、Adobe Campaignサーバーで追加の設定が必要になります。

>[!NOTE]
>
>開始する前に、 **unixodbc** パッケージはサーバー上にあります。

1. **iq_odbc** をインストールします。インストールの終了時にエラーが発生することがあります。このエラーは無視してかまいません。

1. **iq_client_common** をインストールします。インストールの終了時に Java のエラーが発生することがあります。このエラーは無視してかまいません。

1. ODBC ドライバーを設定します。設定は、標準のファイル（一般的なパラメーターは /etc/odbc.ini、ドライバーの宣言は /etc/odbcinst.ini）でおこなえます。

   * **/etc/odbc.ini**（「`<server_alias>`」などの部分は独自の値に置き換えてください）：

     ```
     [ODBC Data Sources]
     <server_alias>=libdbodbc.so
     
     [<server_alias>]
     Driver=/opt/sybase/IQ-16_0/lib64/libdbodbc16.so
     Description=<description>
     Username=<username>
     Password=<password>
     ServerName=<server_name>
     CommLinks=tcpip(host=<host>)
     ```

   * **/etc/odbcinst.ini**

     ```
     [ODBC DRIVERS]
     SAP SybaseIQ=Installed
     
     [SAP SybaseIQ]
     Driver=/opt/sybase/IQ-16_0/lib64/libdbodbc16.so
     ```

1. 新しい libodbc16.so ライブラリのパスを LD_LIBRARY_PATH 変数に追加します。方法は次のとおりです。

   * customer.sh ファイルを使用してパスを宣言する場合は、パス /opt/sybase/IQ-16_0/lib64 を LD_LIBRARY_PATH 変数に追加します。
   * それ以外の場合は、Unix コマンドを使用します。

## Sybase IQ外部アカウント {#sybase-external}

sybase IQ外部アカウントを使用すれば、Campaign インスタンスをSybase IQ外部データベースに接続することができます。

1. キャンペーンから **[!UICONTROL エクスプローラ]**&#x200B;をクリックし、 **[!UICONTROL 管理]** &#39;>&#39; **[!UICONTROL Platform]** &#39;>&#39; **[!UICONTROL 外部アカウント]**.

1. 「**[!UICONTROL 新規]**」をクリックし、「**[!UICONTROL タイプ]**」として「**[!UICONTROL 外部データベース]**」を選択します。

1. **[!UICONTROL Sybase IQ]** 外部アカウントを構成するには、次を指定する必要があります。

   * **[!UICONTROL タイプ]**：ODBC（Sybase ASE、Sybase IQ）

   * **[!UICONTROL サーバー]**：手順 5 で定義した ODBC 接続（`<server_alias>`）に対応します。必ずしもサーバー自体の名前であるとは限りません。

   * **[!UICONTROL アカウント]**：ユーザーの名前

   * **[!UICONTROL パスワード]**：ユーザーアカウントのパスワード

   * **[!UICONTROL データベース]**：データベースの名前

>[!NOTE]
>
>Windows の場合は、Sybase IQ クライアントを Adobe Campaign サーバーにインストールし、ODBC 接続を作成する必要があります。Adobe Campaign サーバー（nlserver）を Windows でサービスとして実行しているときに、システムデータソースを作成してください。
