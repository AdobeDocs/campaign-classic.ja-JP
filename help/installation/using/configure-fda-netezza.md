---
product: campaign
title: Netezza へのアクセスの設定
description: FDAでNetezzaへのアクセスを設定する方法について説明します
feature: Installation, Federated Data Access
audience: platform
content-type: reference
topic-tags: connectors
exl-id: b148d34b-4060-4c54-9cb2-9e712a7c17d7
TQID: https://experienceleague.adobe.com/HiTQ6eoYcjp8pLqNmqLhiDTNhplE4ipnYlWuRFOZvog
product_v2:
  - id: dfc56824-e8b9-499e-85d4-21aedb507314
feature_v2:
  - id: b82389f8-9b5e-4083-8e3b-3cef299fb8b9
subfeature_v2:
  - id: cfc95e9b-b035-4403-a6a9-b27a8a053a37
topic_v2:
  - id: eddd9b14-83bd-4ff4-9072-54a4a484abb7
source-git-commit: 4c295c0dabae8aba298390a3da2422a3fa1219f9
workflow-type: tm+mt
source-wordcount: 391
ht-degree: 82%

---

# Netezza へのアクセスの設定 {#configure-access-to-netezza}



外部データベースに保存されている情報を処理するには、Campaign [Federated Data Access](../../installation/using/about-fda.md) （FDA）オプションを使用します。 Netezzaへのアクセスを設定するには、次の手順に従います。

1. [Netezza ドライバー](#netezza-config)をインストールして設定します
1. CampaignでNetezza [外部アカウント &#x200B;](#netezza-external)を設定する

## Netezza設定 {#netezza-config}

FDA で Netezza 外部データベースに接続するには、Adobe Campaign サーバーで追加の設定が必要になります。

1. 使用するオペレーティングシステムに応じて、Netezza 用の ODBC ドライバーをインストールします。

   * **Linux の場合は、nz-linuxclient-v7.2.0.0.tar.gz です。** オペレーティングシステムに対応するフォルダー（linux または linux64）を選択し、解凍コマンドを開始します。 インストール先はデフォルトで提示されるリポジトリ、「/usr/local/nz」のままでかまいません。
   * **Windows の場合は、nz-winclient-v7.2.0.0.zip です。** ファイルを解凍し、オペレーティングシステムに対応する実行可能スクリプト（nzodbcsetup.exe または nzodbcsetup64.exe）を開始します。 アシスタントの指示に従って、ドライバーのインストールを完了します。

1. ODBC ドライバーを設定します。 設定は、標準のファイル（一般的なパラメーターは **/etc/odbc.ini**、ドライバーの宣言は **/etc/odbcinst.ini**）でおこなえます。

   * **/etc/odbc.ini**

     ```
     [ODBC]
     InstallDir=/etc/
     ```

     「InstallDir」は、odbcinst.ini ファイルの保存場所です。

   * **/etc/odbcinst.ini**

     ```
     [ODBC Drivers]
     NetezzaSQL = Installed
     
     [NetezzaSQL]
     Driver           = /usr/local/nz/lib/libnzsqlodbc3.so
     Setup            = /usr/local/nz/lib/libnzsqlodbc3.so
     APILevel         = 1
     ConnectFunctions = YYN
     Description      = Netezza ODBC driver
     DriverODBCVer    = 03.51
     DebugLogging     = false
     LogPath          = /tmp
     UnicodeTranslationOption = utf8
     CharacterTranslationOption = all
     PreFetch         = 256
     Socket           = 16384
     ```

1. Adobe Campaign サーバーの環境変数を指定します。

   * **LD_LIBRARY_PATH**：/usr/local/nz/lib および /usr/local/nz/lib64。 「/usr/local/nz」は、ドライバーのインストール時にデフォルトで提示されるインストールリポジトリです。 インストール先として選択したリポジトリを指定する必要があります。
   * **ODBCINI**：odbc.ini ファイルの保存場所（例：/etc/odbc.ini）。
   * **NZ_ODBC_INI_PATH**：odbc.ini ファイルの保存場所。 Netezza で odbc.ini ファイルを使用するには、この 2 番目の変数も必要になります。

## Netezza外部アカウント {#netezza-external}

Netezza 外部アカウントを使用すれば、Campaign インスタンスを Netezza 外部データベースに接続できます。

1. キャンペーン **[!UICONTROL エクスプローラー]**&#x200B;から、**[!UICONTROL 管理]** &#39;>&#39; **[!UICONTROL プラットフォーム]** &#39;>&#39; **[!UICONTROL 外部アカウント]**&#x200B;をクリックします。

1. 「**[!UICONTROL 新規]**」をクリックし、「**[!UICONTROL タイプ]**」として「**[!UICONTROL 外部データベース]**」を選択します。

1. **[!UICONTROL Netezza]** 外部アカウントを設定するには、次を指定する必要があります。

   * **[!UICONTROL タイプ]**：Netezza

   * **[!UICONTROL サーバー]**：Netezza サーバーの URL

   * **[!UICONTROL アカウント]**：ユーザーの名前

   * **[!UICONTROL パスワード]**：ユーザーアカウントのパスワード

   * **[!UICONTROL データベース]**：データベースの名前

>[!NOTE]
>
>自動で生成されるプライマリキーを含むスキーマの操作は考慮されません。
>
>テーブルでは、スキーマで定義された最初のインデックスに対して **Organize on** 句が使用されます。 Netezza では、この句が 1～4 列に制限されるので、このインデックスに 4 列までしか格納できません。
