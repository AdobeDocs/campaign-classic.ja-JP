---
product: campaign
title: Snowflakeへのアクセスの設定
description: FDA でSnowflakeへのアクセスを設定する方法を説明します
feature: Installation, Federated Data Access
audience: platform
content-type: reference
topic-tags: connectors
exl-id: bdb5e422-ecfe-42eb-bd15-39fe5ec0ff1d
source-git-commit: b666535f7f82d1b8c2da4fbce1bc25cf8d39d187
workflow-type: tm+mt
source-wordcount: '518'
ht-degree: 32%

---

# Snowflakeへのアクセスの設定 {#configure-access-to-snowflake}

Campaign の使用 **連合データアクセス** （FDA）外部データベースに保存された情報を処理するオプション。 へのアクセスを設定するには、次の手順に従います [!DNL Snowflake].

1. 設定 [!DNL Snowflake] 日付： [Linux](#snowflake-linux).
1. の設定 [!DNL Snowflake] [外部アカウント](#snowflake-external) Campaign 内

>[!NOTE]
>
>[!DNL Snowflake] コネクタは、ホスト型およびオンプレミス型のデプロイメントで使用できます。詳しくは、[このページ](../../installation/using/capability-matrix.md)を参照してください。

![](assets/snowflake_3.png)

## Linux のSnowflake {#snowflake-linux}

を設定 [!DNL Snowflake] linux の場合は、次の手順に従います。

1. ODBC をインストールする前に、Linux ディストリビューションに次のパッケージがインストールされていることを確認します。

   * Red Hat/CentOS:

     ```
     yum update
     yum upgrade
     yum install -y grep sed tar wget perl curl
     ```

   * Debian の場合

     ```
     apt-get update
     apt-get upgrade
     apt-get install -y grep sed tar wget perl curl
     ```

1. スクリプトを実行する前に、を使用して詳細情報にアクセスできます `--help` オプション：

   ```
   cd /usr/local/neolane/nl6/bin/fda-setup-scripts/
   ./snowflake_odbc-setup.sh --help
   ```

1. スクリプトがあるディレクトリにアクセスし、ルートユーザーとして次のスクリプトを実行します。

   ```
   cd /usr/local/neolane/nl6/bin/fda-setup-scripts
   ./snowflake_odbc-setup.sh
   ```

1. ODBC ドライバをインストールしたら、Campaign Classicを再起動する必要があります。 これをおこなうには、次のコマンドを実行します。

   ```
   systemctl stop nlserver.service
   systemctl start nlserver.service
   ```

1. Campaign では、次の項目を設定できます [!DNL Snowflake] 外部アカウント。 外部アカウントの設定方法について詳しくは、次を参照してください。 [この節](#snowflake-external).

## Snowflake外部アカウント {#snowflake-external}

を作成する必要があります [!DNL Snowflake] campaign インスタンスをユーザーに接続するための外部アカウント [!DNL Snowflake] 外部データベース。

1. Campaign から **[!UICONTROL エクスプローラー]**&#x200B;を選択し、 **[!UICONTROL 管理]** &#39;>&#39; **[!UICONTROL Platform]** &#39;>&#39; **[!UICONTROL 外部アカウント]**.

1. 「**[!UICONTROL 新規]**」をクリックします。

1. 外部アカウント&#x200B;**[!UICONTROL タイプ]**&#x200B;として、「**[!UICONTROL 外部データベース]**」を選択します。

1. 次の下 **[!UICONTROL 設定]**&#x200B;を選択 [!DNL Snowflake] から **[!UICONTROL タイプ]** ドロップダウン。

   ![](assets/snowflake_5.png)

1. を追加 **[!UICONTROL サーバー]** URL と **[!UICONTROL データベース]**.

1. の設定 **[!UICONTROL Snowflake]** 外部アカウント認証：

   * アカウント/パスワード認証の場合、次を指定する必要があります。

      * **[!UICONTROL アカウント]**：ユーザーの名前

      * **[!UICONTROL パスワード]**：ユーザーアカウントのパスワード。

     ![](assets/snowflake.png)

   * キーペア認証の場合は、 **[!UICONTROL キーペア認証]** タブを使用 **[!UICONTROL 秘密鍵]** 認証を行ってコピーするには、 **[!UICONTROL 秘密鍵]**.

     ![](assets/snowflake_4.png)

1. 「**[!UICONTROL パラメーター]**」タブをクリックし、「**[!UICONTROL 機能をデプロイ]**」ボタンをクリックして機能を作成します。

   >[!NOTE]
   >
   >すべての関数を使用するには、リモートデータベースにAdobe Campaign SQL 関数を作成する必要があります。 詳しくは、[このページ](../../configuration/using/adding-additional-sql-functions.md)を参照してください。

   ![](assets/snowflake_2.png)

1. クリック **[!UICONTROL 保存]** 設定が完了したら、

コネクタは、次のオプションをサポートしています。

| オプション | 説明 |
|---|---|
| workschema | ワークテーブルに使用するデータベーススキーマ  |
| warehouse | 使用するデフォルトのウェアハウスの名前。ユーザーのデフォルト値より優先されます。 |
| TimeZoneName | デフォルトでは空で、Campaign Classic アプリケーションサーバーのシステムのタイムゾーンが使用されます。このオプションは、TIMEZONE セッションパラメーターを強制的に指定するために使用できます。<br>詳しくは、[このページ](https://docs.snowflake.net/manuals/sql-reference/parameters.html#timezone)を参照してください。 |
| WeekStart | WEEK_START セッションパラメーター。デフォルトでは 0 に設定されています。<br>詳しくは、[このページ](https://docs.snowflake.com/en/sql-reference/parameters.html#week-start)を参照してください。 |
| UseCachedResult | USE_CACHED_RESULTS セッションパラメーター。デフォルトでは TRUE に設定されています。このオプションは、Snowflakeがキャッシュした結果を無効にするために使用できます。 <br>詳しくは、[このページ](https://docs.snowflake.net/manuals/user-guide/querying-persisted-results.html)を参照してください。 |
| bulkThreads | Snowflakeバルクローダーに使用するスレッドの数。スレッドが多いほど、大きなバルク読み込みのパフォーマンスが向上します。 デフォルトでは 1 に設定されています。この数は、マシンスレッド数に応じて調整できます。 |
| chunkSize | バルクローダーチャンクのファイルサイズを決定します。 デフォルトでは 128MB に設定されています。 bulkThreads と共に使用する場合は、より最適なパフォーマンスが得られるように変更できます。 同時にアクティブなスレッドが多いほど、パフォーマンスが向上します。 <br>詳しくは、次を参照してください [Snowflakeドキュメント](https://docs.snowflake.net/manuals/sql-reference/sql/put.html). |
| StageName | 事前プロビジョニングされた内部ステージの名前。 新しい一時ステージを作成する代わりに、一括読み込みで使用されます。 |
