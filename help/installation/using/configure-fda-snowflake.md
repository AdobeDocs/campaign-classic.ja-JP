---
product: campaign
title: Snowflake へのアクセスの設定
description: FDA でSnowflakeへのアクセスを設定する方法
feature: Installation, Federated Data Access
badge-v7-only: label="v7" type="Informative" tooltip="Campaign Classic v7 にのみ適用されます"
audience: platform
content-type: reference
topic-tags: connectors
exl-id: bdb5e422-ecfe-42eb-bd15-39fe5ec0ff1d
source-git-commit: 3a9b21d626b60754789c3f594ba798309f62a553
workflow-type: tm+mt
source-wordcount: '545'
ht-degree: 39%

---

# Snowflake へのアクセスの設定 {#configure-access-to-snowflake}



キャンペーンを使用 **Federated Data Access** (FDA) 外部データベースに保存された情報を処理するオプション。 次の手順に従って、へのアクセスを設定します。 [!DNL Snowflake].

1. 設定 [!DNL Snowflake] オン [Linux](#snowflake-linux).
1. を設定します。 [!DNL Snowflake] [外部アカウント](#snowflake-external) Campaign 内

>[!NOTE]
>
>[!DNL Snowflake] コネクタは、ホスト型およびオンプレミス型のデプロイメントで使用できます。詳しくは、[このページ](../../installation/using/capability-matrix.md)を参照してください。

![](assets/snowflake_3.png)

## Linux でのSnowflake {#snowflake-linux}

を設定するには、以下を実行します。 [!DNL Snowflake] Linux の場合は、次の手順に従います。

1. ODBC をインストールする前に、次のパッケージが Linux ディストリビューションにインストールされていることを確認します。

   * Red Hat/CentOS の場合：

     ```
     yum update
     yum upgrade
     yum install -y grep sed tar wget perl curl
     ```

   * Debian の場合：

     ```
     apt-get update
     apt-get upgrade
     apt-get install -y grep sed tar wget perl curl
     ```

1. スクリプトを実行する前に、 `--help` オプション：

   ```
   cd /usr/local/neolane/nl6/bin/fda-setup-scripts/
   ./snowflake_odbc-setup.sh --help
   ```

1. スクリプトが存在するディレクトリにアクセスし、次のスクリプトを root ユーザーとして実行します。

   ```
   cd /usr/local/neolane/nl6/bin/fda-setup-scripts
   ./snowflake_odbc-setup.sh
   ```

1. ODBC ドライバーをインストールした後、Campaign Classicを再起動する必要があります。 これをおこなうには、次のコマンドを実行します。

   ```
   systemctl stop nlserver.service
   systemctl start nlserver.service
   ```

1. Campaign では、 [!DNL Snowflake] 外部アカウント。 外部アカウントの設定方法について詳しくは、 [この節](#snowflake-external).

## Snowflake 外部アカウント {#snowflake-external}

次を作成する必要があります： [!DNL Snowflake] Campaign インスタンスを [!DNL Snowflake] 外部データベース。

1. キャンペーンから **[!UICONTROL エクスプローラ]**&#x200B;をクリックし、 **[!UICONTROL 管理]** &#39;>&#39; **[!UICONTROL Platform]** &#39;>&#39; **[!UICONTROL 外部アカウント]**.

1. 「**[!UICONTROL 新規]**」をクリックします。

1. 外部アカウント&#x200B;**[!UICONTROL タイプ]**&#x200B;として、「**[!UICONTROL 外部データベース]**」を選択します。

1. の下 **[!UICONTROL 設定]**&#x200B;を選択します。 [!DNL Snowflake] から **[!UICONTROL タイプ]** 」ドロップダウンリストから選択できます。

   ![](assets/snowflake_5.png)

1. を追加します。 **[!UICONTROL サーバー]** URL および **[!UICONTROL データベース]**.

1. を設定します。 **[!UICONTROL Snowflake]** 外部アカウント認証：

   * アカウント/パスワード認証の場合は、次を指定する必要があります。

      * **[!UICONTROL アカウント]**：ユーザーの名前

      * **[!UICONTROL パスワード]**：ユーザーアカウントのパスワード。

     ![](assets/snowflake.png)

   * 鍵のペア認証の場合は、 **[!UICONTROL キーペア認証]** タブを使用して、 **[!UICONTROL 秘密鍵]** を認証し、 **[!UICONTROL 秘密鍵]**.

     ![](assets/snowflake_4.png)

1. 「**[!UICONTROL パラメーター]**」タブをクリックし、「**[!UICONTROL 機能をデプロイ]**」ボタンをクリックして機能を作成します。

   >[!NOTE]
   >
   >すべての関数を使用するには、リモートデータベースでAdobe Campaign SQL 関数を作成する必要があります。 詳しくは、[このページ](../../configuration/using/adding-additional-sql-functions.md)を参照してください。

   ![](assets/snowflake_2.png)

1. クリック **[!UICONTROL 保存]** 設定が完了したら、次の手順に従います。

コネクタは、次のオプションをサポートしています。

| オプション | 説明 |
|---|---|
| workschema | ワークテーブルに使用するデータベーススキーマ  |
| warehouse | 使用するデフォルトのウェアハウスの名前。ユーザーのデフォルト値より優先されます。 |
| TimeZoneName | デフォルトでは空で、Campaign Classic アプリケーションサーバーのシステムのタイムゾーンが使用されます。このオプションは、TIMEZONE セッションパラメーターを強制的に指定するために使用できます。<br>詳しくは、[このページ](https://docs.snowflake.net/manuals/sql-reference/parameters.html#timezone)を参照してください。 |
| WeekStart | WEEK_START セッションパラメーター。デフォルトでは 0 に設定されています。<br>詳しくは、[このページ](https://docs.snowflake.com/en/sql-reference/parameters.html#week-start)を参照してください。 |
| UseCachedResult | USE_CACHED_RESULTS セッションパラメーター。デフォルトでは TRUE に設定されています。このオプションは、Snowflake でキャッシュされた結果を無効にするために使用できます。<br>詳しくは、[このページ](https://docs.snowflake.net/manuals/user-guide/querying-persisted-results.html)を参照してください。 |
| bulkThreads | Snowflakeのバルクローダーに使用するスレッドの数が多いと、より大きなバルクロードでより高いパフォーマンスが得られます。 デフォルトでは 1 に設定されています。数は、装置スレッドの数に応じて調整できます。 |
| chunkSize | バルクローダーチャンクのファイルサイズを決定します。 デフォルトでは 128MB に設定されています。 bulkThreads と組み合わせて使用すると、より最適なパフォーマンスを得るために変更できます。 同時にアクティブなスレッドが多いほど、パフォーマンスが向上します。 <br>詳しくは、 [Snowflake文書](https://docs.snowflake.net/manuals/sql-reference/sql/put.html). |
| StageName | 事前にプロビジョニングされた内部ステージの名前。 新しい一時ステージを作成する代わりに、一括読み込みで使用されます。 |
