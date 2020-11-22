---
solution: Campaign Classic
product: campaign
title: Sybase IQ へのアクセスを設定する
description: FDAでのSybase IQへのアクセスを設定する方法を学びます。
audience: platform
content-type: reference
topic-tags: connectors
translation-type: tm+mt
source-git-commit: 972885c3a38bcd3a260574bacbb3f507e11ae05b
workflow-type: tm+mt
source-wordcount: '335'
ht-degree: 67%

---


# Sybase IQ へのアクセスを設定する {#configure-access-to-sybase-iq}

キャンペーン **Federated Data Access** (FDA)オプションを使用して、外部データベースに保存された情報を処理します。 次の手順に従って、Sybase IQへのアクセスを設定します。

1. [Sybase IQデータベースの設定](#configuring-sybase)
1. キャンペーンでのSybase IQ [外部アカウントの設定](#sybase-external)

## sybase IQ形状 {#configuring-sybase}

FDAでSybase IQの外部データベースに接続するには、Adobe Campaignサーバで以下の追加設定が必要です。

>[!NOTE]
>
>Before starting, make sure the **unixodbc** package is on the server.

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

## sybase IQ外部アカウント {#sybase-external}

sybase IQ外部アカウントを使用すると、キャンペーンインスタンスをSybase IQの外部データベースに接続できます。

1. From Campaign **[!UICONTROL Explorer]**, click **[!UICONTROL Administration]** &#39;>&#39; **[!UICONTROL Platform]** &#39;>&#39; **[!UICONTROL External accounts]**.

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

