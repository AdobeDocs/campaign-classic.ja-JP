---
title: 外部データベースへのアクセス
seo-title: 外部データベースへのアクセス
description: 外部データベースへのアクセス
seo-description: null
page-status-flag: never-activated
uuid: b84359b9-c584-431d-80d5-71146d9b6854
contentOwner: sauviat
products: SG_CAMPAIGN/CLASSIC
audience: platform
content-type: reference
topic-tags: connectors
discoiquuid: dd3d14cc-5153-428d-a98a-32b46f0fe811
index: y
internal: n
snippet: y
translation-type: tm+mt
source-git-commit: 4969c5e56f1911b3abfd770ca4f8f5ed25784a52

---


# データベースへの接続 {#connecting-to-the-database}

外部データベースへの接続を有効にするには、対象のデータソースおよびデータの読み込みが必要なテーブルの名前を接続パラメーターで指定する必要があります。

>[!CAUTION]
>
>Adobe Campaign ユーザーが外部データベースのデータを処理するには、外部データベースおよび Adobe Campaign アプリケーションサーバーに対する特定の権限が必要です。詳細については、「リモート・データベース・アク [セス権」の節を参照してくださ](#remote-database-access-rights) い。
>
>誤作動を回避するために、リモートの共有データにアクセスするオペレーターは分離された環境で作業をおこなう必要があります。

## 共有接続の作成 {#creating-a-shared-connection}

共有外部データベースへの接続を有効にすると、この接続がアクティブである限り、データベースは Adobe Campaign 経由でアクセスできます。

1. 設定は、ノードを介して事前に定義する必要があ **[!UICONTROL Administration > Platform > External accounts]** ります。
1. ボタンをクリ **[!UICONTROL New]** ックし、タイプを選択 **[!UICONTROL External database]** します。
1. Define the **[!UICONTROL Connection]** parameters of the external database.

   For connections to an **ODBC** type database the **[!UICONTROL Server]** field must contain the name of the ODBC data source and not the server name. また、使用するデータベースによっては、追加の設定が必要になることがあります。「データベースタ [イプ別の設定」の節を参照](#specific-configurations-by-database-type) 。

1. Once the parameters are entered, click the **[!UICONTROL Test the connection]** button to approve them.

   ![](assets/wf-external-account-create.png)

1. If necessary, uncheck the **[!UICONTROL Enabled]** option to disable access to this database without deleting its configuration.
1. このデータベースに Adobe Campaign からアクセスするには、SQL 関数をデプロイする必要があります。タブをクリックし **[!UICONTROL Parameters]** てから、ボタンをクリッ **[!UICONTROL Deploy functions]** クします。

   ![](assets/wf-external-account-functions.png)

You can define specific work tablespaces for the tables and for the index in the **[!UICONTROL Parameters]** tab.

## 一時的な接続の作成 {#creating-a-temporary-connection}

ワークフローアクティビティから外部データベースへの接続を直接定義できます。この場合、接続はローカルの外部データベース上に置かれ、現在のワークフロー内で使用するために予約されます。外部アカウントには保存されません。This type of punctual connection can be created on different activities of the workflow, particularly the **[!UICONTROL Query]**, the **[!UICONTROL Data loading (RDBMS)]**, the **[!UICONTROL Enrichment]** activity or the **[!UICONTROL Split]** activity.

>[!CAUTION]
>
>このタイプの設定は推奨されませんが、データを収集するために定期的に使用される場合があります。ただし、[共有接続の作成](#creating-a-shared-connection)の節で説明しているように、外部アカウントを作成する必要があります。

例えば、「クエリ」アクティビティで、外部データベースへの定期的な接続を作成する手順は次のようになります。

1. をクリックし、 **[!UICONTROL Add data...]** オプションを選択 **[!UICONTROL External data]** します。
1. オプションを選 **[!UICONTROL Locally defining the data source]** 択します。

   ![](assets/wf_add_data_local_external_data.png)

1. ドロップダウンリストからターゲットのデータベースエンジンを選択します。サーバーの名前を入力し、認証パラメーターを指定します。

   外部データベースの名前も指定します。

   ![](assets/wf_add_data_local_external_data_param.png)

   ボタンをクリッ **[!UICONTROL Next]** クします。

1. データが格納されているテーブルを選択します。

   該当するフィールドにテーブルの名前を直接入力するか、編集アイコンをクリックしてデータベーステーブルのリストにアクセスできます。

   ![](assets/wf_add_data_local_external_data_select_table.png)

1. Click the **[!UICONTROL Add]** button to define one or several reconciliation fields between the external database data and the data in the Adobe Campaign database. とのア **[!UICONTROL Edit expression]** イコンを使 **[!UICONTROL Remote field]** 用して、 **[!UICONTROL Local field]** 各テーブルのフィールドのリストにアクセスできます。

   ![](assets/wf_add_data_local_external_data_join.png)

1. 必要に応じて、フィルタリング条件とデータ並べ替えモードを指定します。
1. 外部データベースで収集する追加のデータを選択します。To do this, double click on the fields(s) that you want to add to display them in the **[!UICONTROL Output columns]**.

   ![](assets/wf_add_data_local_external_data_select.png)

   Click **[!UICONTROL Finish]** to confirm this configuration.

## 接続の保護 {#secure-connection}

>[!NOTE]
>
>安全な接続はPostgreSQLでのみ利用できます。

外部の FDA アカウントを設定するときに外部データベースへのアクセスを保護できます。

そのためには、サーバーアドレスと使用するポートのアドレスの後に &quot;**:ssl**&quot; を追加します。例： **192.168.0.52:4501:ssl**。

これで、データはセキュアな SSL プロトコル経由で送信されます。

## 任意の追加設定 {#additional-configurations}

必要に応じて、外部データベースのデータを処理するためのスキーマを作成できます。同様に、Adobe Campaign では外部テーブルのデータでマッピングを定義できます。これらは一般的な設定で、ワークフローだけに適用されるわけではありません。

>[!NOTE]
>
>Adobe Campaign でのスキーマの作成および新しいデータマッピングの定義について詳しくは、[このページ](../../configuration/using/about-schema-edition.md)を参照してください。