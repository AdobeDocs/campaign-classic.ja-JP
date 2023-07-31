---
product: campaign
title: Netezza へのアクセスの設定
description: FDA でNetezzaへのアクセスを設定する方法
feature: Installation, Federated Data Access
badge-v7-only: label="v7" type="Informative" tooltip="Campaign Classicv7 にのみ適用"
audience: platform
content-type: reference
topic-tags: connectors
exl-id: b148d34b-4060-4c54-9cb2-9e712a7c17d7
source-git-commit: 3a9b21d626b60754789c3f594ba798309f62a553
workflow-type: tm+mt
source-wordcount: '396'
ht-degree: 79%

---

# Netezza へのアクセスの設定 {#configure-access-to-netezza}



キャンペーンを使用 [Federated Data Access](../../installation/using/about-fda.md) (FDA) 外部データベースに保存されている情報を処理するオプション。 次の手順に従って、Netezzaへのアクセスを設定します。

1. インストールと設定 [Netezzaドライバ](#netezza-config)
1. netezza [外部アカウント](#netezza-external) Campaign 内

## Netezza設定 {#netezza-config}

FDA で Netezza 外部データベースに接続するには、Adobe Campaign サーバーで追加の設定が必要になります。

1. 使用するオペレーティングシステムに応じて、Netezza 用の ODBC ドライバーをインストールします。

   * **Linux の場合は、nz-linuxclient-v7.2.0.0.tar.gz です。**&#x200B;オペレーティングシステムに対応するフォルダー（linux または linux64）を選択し、解凍コマンドを開始します。インストール先はデフォルトで提示されるリポジトリ、「/usr/local/nz」のままでかまいません。
   * **Windows の場合は、nz-winclient-v7.2.0.0.zip です。**&#x200B;ファイルを解凍し、オペレーティングシステムに対応する実行可能スクリプト（nzodbcsetup.exe または nzodbcsetup64.exe）を開始します。ウィザードの手順に従ってドライバーのインストールを完了します。

1. ODBC ドライバーを設定します。設定は、標準のファイル（一般的なパラメーターは **/etc/odbc.ini**、ドライバーの宣言は **/etc/odbcinst.ini**）でおこなえます。

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

   * **LD_LIBRARY_PATH**：/usr/local/nz/lib および /usr/local/nz/lib64。「/usr/local/nz」は、ドライバーのインストール時にデフォルトで提示されるインストールリポジトリです。インストール先として選択したリポジトリを指定する必要があります。
   * **ODBCINI**：odbc.ini ファイルの保存場所（例：/etc/odbc.ini）。
   * **NZ_ODBC_INI_PATH**：odbc.ini ファイルの保存場所。Netezza で odbc.ini ファイルを使用するには、この 2 番目の変数も必要になります。

## Netezza外部アカウント {#netezza-external}

netezza外部アカウントを使用すれば、Campaign インスタンスをNetezza外部データベースに接続できます。

1. キャンペーンから **[!UICONTROL エクスプローラ]**&#x200B;をクリックし、 **[!UICONTROL 管理]** &#39;>&#39; **[!UICONTROL Platform]** &#39;>&#39; **[!UICONTROL 外部アカウント]**.

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
>テーブルでは、スキーマで定義された最初のインデックスに対して **Organize on** 句が使用されます。Netezza では、この句が 1～4 列に制限されるので、このインデックスに 4 列までしか格納できません。
