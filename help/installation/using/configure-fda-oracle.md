---
product: campaign
title: Oracle へのアクセスの設定
description: FDAでOracleへのアクセスを設定する方法について説明します
feature: Installation, Federated Data Access
audience: platform
content-type: reference
topic-tags: connectors
exl-id: 320bfbb4-533b-4c45-a46f-c3c8dd68221f
TQID: https://experienceleague.adobe.com/PbyBdgy6uFZNOmZ2GFrntS4XSJoJj41uFXLWOF4eWyA
product_v2:
  - id: dfc56824-e8b9-499e-85d4-21aedb507314
topic_v2:
  - id: eddd9b14-83bd-4ff4-9072-54a4a484abb7
source-git-commit: 4c295c0dabae8aba298390a3da2422a3fa1219f9
workflow-type: tm+mt
source-wordcount: 363
ht-degree: 63%

---

# Oracle へのアクセスの設定 {#configure-access-to-oracle}



外部データベースに保存されている情報を処理するには、Campaign [Federated Data Access](../../installation/using/about-fda.md) （FDA）オプションを使用します。 Oracleへのアクセスを設定するには、次の手順に従います。

1. [Linux](#oracle-linux)または[Windows](#azure-windows)でOracleを構成する
1. CampaignでOracle [外部アカウント &#x200B;](#oracle-external)を設定する

## Linux版Oracle {#oracle-linux}

FDA で Oracle 外部データベースに接続するには、Adobe Campaign サーバーで追加の設定が必要になります。

1. お使いのバージョンの Oracle に対応した Oracle フルクライアントをインストールします。
1. インストールに TNS の定義を追加します。 これは、/etc/oracle リポジトリの「**tnsnames.ora**」ファイルで指定します。 このリポジトリが存在しない場合は作成します。

   その後、TNS_ADMIN 環境変数を新規に作成し、TNS_ADMIN=/etc/oracle をエクスポートしてマシンを再起動します。

1. Oracle を Adobe Campaign サーバー（nlserver）に統合します。 そのためには、Adobe Campaign サーバーツリー構造の「nl6」フォルダーに「**customer.sh**」ファイルがあり、そのファイルに Oracle ライブラリへのリンクが含まれていることを確認します。T

   クライアントのバージョンが 11.2 の場合の例を次に示します。

   ```
   export ORACLE_HOME=/usr/lib/oracle/11.2
   export TNS_ADMIN=/etc/oracle
   export LD_LIBRARY_PATH=$ORACLE_HOME/client64/lib:$LD_LIBRARY_PATH
   ```

   >[!NOTE]
   >
   >これらの値（特に ORACLE_HOME）はインストールリポジトリによって異なります。 これらの値を参照する前に、ツリー構造を確認してください。

1. Oracle に必要なライブラリをインストールします。

   * **libclntsh.so**

     ```
     cd /usr/lib/oracle/<version>/client<architecture>/lib
     ln -s libclntsh.so.<version> libclntsh.so
     ```

   * **libaio1**

     ```
     apt install libaio1
     or
     yum install libaio1
     ```

1. Campaign Classic では、[!DNL Oracle] 外部アカウントを設定できます。 外部アカウントの設定方法について詳しくは、[この節](#oracle-external)を参照してください。

## Windows版Oracle {#oracle-windows}

FDA で Oracle 外部データベースに接続するには、Adobe Campaign サーバーで追加の設定が必要になります。

1. Oracle クライアントをインストールします。

1. C:Oracle フォルダーに、TNS定義を含む&#x200B;**tnsnames.ora** ファイルを作成します。

1. 値としてC:Oracleを持つTNS_ADMIN環境変数を追加し、コンピューターを再起動します。

1. Campaign Classic では、[!DNL Oracle] 外部アカウントを設定できます。 外部アカウントの設定方法について詳しくは、[この節](#oracle-external)を参照してください。

## Oracle外部アカウント {#oracle-external}

[!DNL Oracle]外部アカウントを使用すると、Campaign インスタンスをOracle外部データベースに接続できます。

1. キャンペーン **[!UICONTROL エクスプローラー]**&#x200B;から、**[!UICONTROL 管理]** &#39;>&#39; **[!UICONTROL プラットフォーム]** &#39;>&#39; **[!UICONTROL 外部アカウント]**&#x200B;を選択します。

1. **[!UICONTROL 新規]**&#x200B;を選択します。

1. 外部アカウント&#x200B;**[!UICONTROL タイプ]**&#x200B;として、「**[!UICONTROL 外部データベース]**」を選択します。

1. **[!UICONTROL Oracle]** 外部アカウントを設定するには、次を指定する必要があります。

   * **[!UICONTROL タイプ]**：Oracle

   * **[!UICONTROL サーバー]**：DNS の名前

   * **[!UICONTROL アカウント]**：ユーザーの名前

   * **[!UICONTROL パスワード]**：ユーザーアカウントのパスワード

   * **[!UICONTROL タイムゾーン]**：サーバーのタイムゾーン

   ![](assets/oracle_config.png)
