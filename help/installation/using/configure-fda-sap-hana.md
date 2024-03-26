---
product: campaign
title: SAP HANA へのアクセスを設定する
description: FDA でSAP HANAへのアクセスを設定する方法
feature: Installation, Federated Data Access
badge-v7-only: label="v7" type="Informative" tooltip="Campaign Classic v7 にのみ適用されます"
audience: platform
content-type: reference
topic-tags: connectors
exl-id: 39bfe775-e182-4a0b-ad3c-b7a901297c90
source-git-commit: 3a9b21d626b60754789c3f594ba798309f62a553
workflow-type: tm+mt
source-wordcount: '279'
ht-degree: 71%

---

# SAP HANA へのアクセスを設定する {#configure-access-to-sap-hana}



キャンペーンを使用 [Federated Data Access](../../installation/using/about-fda.md) (FDA) 外部データベースに保存されている情報を処理するオプション。 次の手順に従って、SAP HANAへのアクセスを設定します。

1. 設定 [SAP HANAデータベース](#sap-config)
1. SAP HANA [外部アカウント](#sap-external) Campaign 内

## SAP HANAドライバ {#sap-config}

FDA で SAP HANA 外部データベースに接続するには、Adobe Campaign サーバーで追加の設定が必要になります。

1. 使用するオペレーティングシステムに応じて、SAP HANA 用の ODBC ドライバーをインストールします。

   * **hdb_client_linux.tgz（Linux 用）：**&#x200B;解凍後、hdbinst コマンドを開始し、指示に従ってドライバーのインストールを完了します。
   * **hdb_client_windows.zip（Windows 用）：**&#x200B;ファイルを解凍し、実行可能ファイル **hdbinst.exe** を起動します。ウィザードの手順に従ってドライバーのインストールを完了します。

1. ODBC ドライバーを設定します。設定は、標準のファイル（一般的なパラメーターは /etc/odbc.ini、ドライバーの宣言は /etc/odbcinst.ini）でおこなえます。

   * **/etc/odbc.ini**

     ```
     [ODBC]
     InstallDir=/etc/
     
     [HDB]
     Driver=HDBODBC
     servernode=localhost:39013 (this value depend of your server)
     User:SYSTEM
     ```

     「InstallDir」は、**odbcinst.ini** ファイルの保存場所です。

   * **/etc/odbcinst.ini**

     ```
     [HDBODBC]
     Description = "SmartCloudPT HANA"
     Driver = /usr/sap/hdbclient/libodbcHDB.so
     ```

1. Adobe Campaign サーバーの環境変数を指定します。

   * **LD_LIBRARY_PATH**：SAP HANA クライアントへのリンク（デフォルトでは /usr/sap/hdbclient/libodbcHDB.so）を含める必要があります。
   * **ODBCINI**：odbc.ini ファイルの保存場所（例：/etc/odbc.ini）。

## SAP HANA外部アカウント{#sap-external}

SAP HANA外部アカウントを使用すれば、Campaign インスタンスをSAP HANA外部データベースに接続できます。

1. キャンペーンから **[!UICONTROL エクスプローラ]**&#x200B;をクリックし、 **[!UICONTROL 管理]** &#39;>&#39; **[!UICONTROL Platform]** &#39;>&#39; **[!UICONTROL 外部アカウント]**.

1. 「**[!UICONTROL 新規]**」をクリックし、「**[!UICONTROL タイプ]**」として「**[!UICONTROL 外部データベース]**」を選択します。

1. **[!UICONTROL SAP Hana]** 外部アカウントを設定するには、次を指定する必要があります。

   * **[!UICONTROL タイプ]**：SAP Hana

   * **[!UICONTROL サーバー]**：SAP Hana サーバーの URL

   * **[!UICONTROL アカウント]**：ユーザーの名前

   * **[!UICONTROL パスワード]**：ユーザーアカウントのパスワード
