---
product: campaign
title: SAP HANA へのアクセスを設定する
description: FDAでSAP HANAへのアクセスを設定する方法について説明します
feature: Installation, Federated Data Access
audience: platform
content-type: reference
topic-tags: connectors
exl-id: 39bfe775-e182-4a0b-ad3c-b7a901297c90
TQID: https://experienceleague.adobe.com/m2ibPllvRz-0vRS80bsktgY2qKdxL-fH9UEmHDgokT8
product_v2:
  - id: dfc56824-e8b9-499e-85d4-21aedb507314
topic_v2:
  - id: eddd9b14-83bd-4ff4-9072-54a4a484abb7
source-git-commit: 4c295c0dabae8aba298390a3da2422a3fa1219f9
workflow-type: tm+mt
source-wordcount: 272
ht-degree: 73%

---

# SAP HANA へのアクセスを設定する {#configure-access-to-sap-hana}



外部データベースに保存されている情報を処理するには、Campaign [Federated Data Access](../../installation/using/about-fda.md) （FDA）オプションを使用します。 SAP HANAへのアクセスを設定するには、次の手順に従います。

1. [SAP HANA データベース &#x200B;](#sap-config)を設定
1. CampaignでSAP HANA [外部アカウント &#x200B;](#sap-external)を設定する

## SAP HANA ドライバー {#sap-config}

FDA で SAP HANA 外部データベースに接続するには、Adobe Campaign サーバーで追加の設定が必要になります。

1. 使用するオペレーティングシステムに応じて、SAP HANA 用の ODBC ドライバーをインストールします。

   * **hdb_client_linux.tgz（Linux 用）：** 解凍後、hdbinst コマンドを開始し、指示に従ってドライバーのインストールを完了します。
   * **hdb_client_windows.zip（Windows 用）：** ファイルを解凍し、実行可能ファイル **hdbinst.exe** を起動します。 アシスタントの指示に従って、ドライバーのインストールを完了します。

1. ODBC ドライバーを設定します。 設定は、標準のファイル（一般的なパラメーターは /etc/odbc.ini、ドライバーの宣言は /etc/odbcinst.ini）でおこなえます。

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

SAP HANA 外部アカウントを使用すれば、Campaign インスタンスを SAP HANA 外部データベースに接続できます。

1. キャンペーン **[!UICONTROL エクスプローラー]**&#x200B;から、**[!UICONTROL 管理]** &#39;>&#39; **[!UICONTROL プラットフォーム]** &#39;>&#39; **[!UICONTROL 外部アカウント]**&#x200B;をクリックします。

1. 「**[!UICONTROL 新規]**」をクリックし、「**[!UICONTROL タイプ]**」として「**[!UICONTROL 外部データベース]**」を選択します。

1. **[!UICONTROL SAP Hana]** 外部アカウントを設定するには、次を指定する必要があります。

   * **[!UICONTROL タイプ]**：SAP Hana

   * **[!UICONTROL サーバー]**：SAP Hana サーバーの URL

   * **[!UICONTROL アカウント]**：ユーザーの名前

   * **[!UICONTROL パスワード]**：ユーザーアカウントのパスワード
