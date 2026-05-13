---
product: campaign
title: Sybase IQ へのアクセスを設定する
description: FDAでSybase IQへのアクセスを設定する方法について説明します
feature: Installation, Federated Data Access
audience: platform
content-type: reference
topic-tags: connectors
exl-id: 0fdf8259-5cab-4a9d-adb3-6c55ec5c8851
TQID: https://experienceleague.adobe.com/AnTufHUh2UZrrIqrauxCzPEeua3qKLuHwH5DEz0KqI8
product_v2: id: dfc56824-e8b9-499e-85d4-21aedb507314
topic_v2: id: eddd9b14-83bd-4ff4-9072-54a4a484abb7
source-git-commit: 4c295c0dabae8aba298390a3da2422a3fa1219f9
workflow-type: tm+mt
source-wordcount: 330
ht-degree: 66%

---

# Sybase IQ へのアクセスを設定する {#configure-access-to-sybase-iq}



外部データベースに保存されている情報を処理するには、Campaign **Federated Data Access** （FDA）オプションを使用します。 Sybase IQへのアクセスを設定するには、次の手順に従います。

1. [Sybase IQ データベース ](#configuring-sybase)を設定
1. CampaignでSybase IQ [外部アカウント ](#sybase-external)を設定する

## Sybase IQ設定 {#configuring-sybase}

FDAでSybase IQ外部データベースに接続するには、Adobe Campaign サーバーで以下の追加の設定が必要です。

>[!NOTE]
>
>開始する前に、**unixodbc** パッケージがサーバー上にあることを確認してください。

1. **iq_odbc** をインストールします。 インストールの終了時にエラーが発生することがあります。 このエラーは無視してかまいません。

1. **iq_client_common** をインストールします。 インストールの終了時に Java のエラーが発生することがあります。 このエラーは無視してかまいません。

1. ODBC ドライバーを設定します。 設定は、標準のファイル（一般的なパラメーターは /etc/odbc.ini、ドライバーの宣言は /etc/odbcinst.ini）でおこなえます。

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

1. 新しい libodbc16.so ライブラリのパスを LD_LIBRARY_PATH 変数に追加します。 方法は次のとおりです。

   * customer.sh ファイルを使用してパスを宣言する場合は、パス /opt/sybase/IQ-16_0/lib64 を LD_LIBRARY_PATH 変数に追加します。
   * それ以外の場合は、Unix コマンドを使用します。

## Sybase IQ外部アカウント {#sybase-external}

Sybase IQ外部アカウントを使用すると、Campaign インスタンスをSybase IQ外部データベースに接続できます。

1. キャンペーン **[!UICONTROL エクスプローラー]**&#x200B;から、**[!UICONTROL 管理]** &#39;>&#39; **[!UICONTROL プラットフォーム]** &#39;>&#39; **[!UICONTROL 外部アカウント]**&#x200B;をクリックします。

1. 「**[!UICONTROL 新規]**」をクリックし、「**[!UICONTROL タイプ]**」として「**[!UICONTROL 外部データベース]**」を選択します。

1. **[!UICONTROL Sybase IQ]** 外部アカウントを構成するには、次を指定する必要があります。

   * **[!UICONTROL タイプ]**：ODBC（Sybase ASE、Sybase IQ）

   * **[!UICONTROL サーバー]**：手順 5 で定義した ODBC 接続（`<server_alias>`）に対応します。 必ずしもサーバー自体の名前であるとは限りません。

   * **[!UICONTROL アカウント]**：ユーザーの名前

   * **[!UICONTROL パスワード]**：ユーザーアカウントのパスワード

   * **[!UICONTROL データベース]**：データベースの名前

>[!NOTE]
>
>Windows の場合は、Sybase IQ クライアントを Adobe Campaign サーバーにインストールし、ODBC 接続を作成する必要があります。 Adobe Campaign サーバー（nlserver）を Windows でサービスとして実行しているときに、システムデータソースを作成してください。
