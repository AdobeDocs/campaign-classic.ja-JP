---
title: Oracle へのアクセスの設定
description: FDAでのOracleへのアクセスの設定方法
page-status-flag: never-activated
uuid: b84359b9-c584-431d-80d5-71146d9b6854
contentOwner: sauviat
products: SG_CAMPAIGN/CLASSIC
audience: platform
content-type: reference
topic-tags: connectors
discoiquuid: dd3d14cc-5153-428d-a98a-32b46f0fe811
translation-type: tm+mt
source-git-commit: 9bbde65aea6735e30e95e75c2b6ae5445d4a2bdd
workflow-type: tm+mt
source-wordcount: '368'
ht-degree: 73%

---


# Oracle へのアクセスの設定 {#configure-access-to-oracle}

キャンペーン [Federated Data Access](../../installation/using/about-fda.md) (FDA)オプションを使用して、外部データベースに保存された情報を処理します。 次の手順に従って、Oracleへのアクセスを設定します。

1. [Linux](#oracle-linux) または [WindowsでのOracleの設定](#azure-windows)
1. キャンペーンでのOracle [外部アカウントの設定](#oracle-external)

## Oracle（Linux） {#oracle-linux}

FDA で Oracle 外部データベースに接続するには、Adobe Campaign サーバーで追加の設定が必要になります。

1. お使いのバージョンの Oracle に対応した Oracle フルクライアントをインストールします。
1. インストールに TNS の定義を追加します。これは、/etc/oracle リポジトリの「**tnsnames.ora**」ファイルで指定します。このリポジトリが存在しない場合は作成します。

   その後、TNS_ADMIN 環境変数を新規に作成し、TNS_ADMIN=/etc/oracle をエクスポートしてマシンを再起動します。

1. Oracle を Adobe Campaign サーバー（nlserver）に統合します。そのためには、Adobe Campaign サーバーツリー構造の「nl6」フォルダーに「**customer.sh**」ファイルがあり、そのファイルに Oracle ライブラリへのリンクが含まれていることを確認します。T

   クライアントのバージョンが 11.2 の場合の例を次に示します。

   ```
   export ORACLE_HOME=/usr/lib/oracle/11.2
   export TNS_ADMIN=/etc/oracle
   export LD_LIBRARY_PATH=$ORACLE_HOME/client64/lib:$LD_LIBRARY_PATH
   ```

   >[!NOTE]
   >
   >これらの値（特に ORACLE_HOME）はインストールリポジトリによって異なります。これらの値を参照する前に、ツリー構造を確認してください。

1. Oracle に必要なライブラリをインストールします。

   * **libclntsh.so**

      ```
      cd /usr/lib/oracle/<version>/client<architecture>/lib
      ln -s libclntsh.so.<version> libclntsh.so
      ```

   * **libaio1**

      ```
      aptitude install libaio1
      or
      yum install libaio1
      ```

1. Campaign Classic では、[!DNL Oracle] 外部アカウントを設定できます。For more on how to configure your external account, refer to [this section](#oracle-external).

## Oracle（Windows） {#oracle-windows}

FDA で Oracle 外部データベースに接続するには、Adobe Campaign サーバーで追加の設定が必要になります。

1. Oracle クライアントをインストールします。

1. C:\Oracle フォルダーに、TNS の定義を含む **tnsnames.ora** ファイルを作成します。

1. TNS_ADMIN 環境変数を追加して値を C:\Oracle に設定し、マシンを再起動します。

1. Campaign Classic では、[!DNL Oracle] 外部アカウントを設定できます。For more on how to configure your external account, refer to [this section](#oracle-external).

## Oracle 外部アカウント {#oracle-external}

The [!DNL Oracle] external account allows you to connect your Campaign instance to your Oracle external database.

1. From Campaign **[!UICONTROL Explorer]**, select **[!UICONTROL Administration]** &#39;>&#39; **[!UICONTROL Platform]** &#39;>&#39; **[!UICONTROL External accounts]**.

1. 「 **[!UICONTROL 新規]**」を選択します。

1. 外部アカウント&#x200B;**[!UICONTROL タイプ]**&#x200B;として、「**[!UICONTROL 外部データベース]**」を選択します。

1. **[!UICONTROL Oracle]** 外部アカウントを設定するには、次を指定する必要があります。

   * **[!UICONTROL タイプ]**：Oracle

   * **[!UICONTROL サーバー]**：DNS の名前

   * **[!UICONTROL アカウント]**：ユーザーの名前

   * **[!UICONTROL パスワード]**：ユーザーアカウントのパスワード

   * **[!UICONTROL タイムゾーン]**：サーバーのタイムゾーン

   ![](assets/oracle_config.png)

