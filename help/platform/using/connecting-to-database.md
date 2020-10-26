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
translation-type: ht
source-git-commit: 70b143445b2e77128b9404e35d96b39694d55335
workflow-type: ht
source-wordcount: '686'
ht-degree: 100%

---


# データベースへの接続 {#connecting-to-the-database}

外部データベースへの接続を有効にするには、対象のデータソースおよびデータの読み込みが必要なテーブルの名前を接続パラメーターで指定する必要があります。

>[!CAUTION]
>
>Adobe Campaign ユーザーが外部データベースのデータを処理するには、外部データベースおよび Adobe Campaign アプリケーションサーバーに対する特定の権限が必要です。詳しくは、[リモートデータベースのアクセス権](../../platform/using/remote-database-access-rights.md)の節を参照してください。
>
>誤作動を回避するために、リモートの共有データにアクセスするオペレーターは分離された環境で作業をおこなう必要があります。

## 共有接続の作成 {#creating-a-shared-connection}

共有外部データベースへの接続を有効にすると、この接続がアクティブである限り、データベースは Adobe Campaign 経由でアクセスできます。

1. この設定は、あらかじめ&#x200B;**[!UICONTROL 管理／プラットフォーム／外部アカウント]**&#x200B;ノードで定義する必要があります。
1. 「**[!UICONTROL 新規]**」ボタンをクリックして、「**[!UICONTROL 外部データベース]**」タイプを選択します。
1. 外部データベースの&#x200B;**[!UICONTROL 接続]**&#x200B;パラメーターを定義します。

   **ODBC** タイプのデータベースに接続する場合は、「**[!UICONTROL サーバー]**」フィールドに、サーバー名ではなく ODBC データソースの名前を入力する必要があります。また、使用するデータベースによっては、追加の設定が必要になることがあります。[データベースタイプ別の特定の設定](../../platform/using/specific-configuration-database.md)の節を参照してください。

1. パラメーターを入力したら、「**[!UICONTROL 接続をテスト]**」ボタンをクリックして承認します。

   ![](assets/wf-external-account-create.png)

1. 必要に応じて、「**[!UICONTROL 有効]**」オプションのチェックを解除して、設定は削除せずに、このデータベースへのアクセスを無効にします。
1. このデータベースに Adobe Campaign からアクセスするには、SQL 関数をデプロイする必要があります。「**[!UICONTROL パラメーター]**」タブをクリックし、「**[!UICONTROL 機能をデプロイ]**」ボタンをクリックします。

   ![](assets/wf-external-account-functions.png)

「**[!UICONTROL パラメーター]**」タブでは、テーブル用およびインデックス用の固有の作業用テーブル領域をそれぞれ定義できます。

## 一時的な接続の作成 {#creating-a-temporary-connection}

ワークフローアクティビティから外部データベースへの接続を直接定義できます。この場合、接続はローカルの外部データベース上に置かれ、現在のワークフロー内で使用するために予約されます。外部アカウントには保存されません。このタイプの定時接続はワークフローの様々なアクティビティ、特に「**[!UICONTROL クエリ]**」、「**[!UICONTROL データ読み込み (RDBMS)]**」、「**[!UICONTROL エンリッチメント]**」または「**[!UICONTROL 分割]**」アクティビティで作成できます。

>[!CAUTION]
>
>このタイプの設定は推奨されませんが、データを収集するために定期的に使用される場合があります。ただし、[共有接続の作成](#creating-a-shared-connection)の節で説明しているように、外部アカウントを作成する必要があります。

例えば、「クエリ」アクティビティで、外部データベースへの定期的な接続を作成する手順は次のようになります。

1. 「**[!UICONTROL データを追加]**」をクリックし、「**[!UICONTROL 外部データ]**」オプションを選択します。
1. 「**[!UICONTROL データソースをローカルで定義]**」オプションを選択します。

   ![](assets/wf_add_data_local_external_data.png)

1. ドロップダウンリストからターゲットのデータベースエンジンを選択します。サーバーの名前を入力し、認証パラメーターを指定します。

   外部データベースの名前も指定します。

   ![](assets/wf_add_data_local_external_data_param.png)

   「**[!UICONTROL 次へ]**」ボタンをクリックします。

1. データが格納されているテーブルを選択します。

   該当するフィールドにテーブルの名前を直接入力するか、編集アイコンをクリックしてデータベーステーブルのリストにアクセスできます。

   ![](assets/wf_add_data_local_external_data_select_table.png)

1. 「**[!UICONTROL 追加]**」ボタンをクリックして、外部データベースのデータと Adobe Campaign データベースのデータとの間の 1 つまたは複数の紐付けを定義します。「**[!UICONTROL リモートフィールド]**」と「**[!UICONTROL ローカルフィールド]**」の「**[!UICONTROL 式を編集]**」アイコンを使用して、各テーブルのフィールドのリストにアクセスできます。

   ![](assets/wf_add_data_local_external_data_join.png)

1. 必要に応じて、フィルタリング条件とデータ並べ替えモードを指定します。
1. 外部データベースで収集する追加のデータを選択します。追加データを選択するには、追加するフィールドをダブルクリックして「**[!UICONTROL 出力列]**」に表示します。

   ![](assets/wf_add_data_local_external_data_select.png)

   「**[!UICONTROL 完了]**」をクリックして、この設定を確認します。

## 接続の保護 {#secure-connection}

>[!NOTE]
>
>接続の保護は PostgreSQL でのみ利用可能です。

外部の FDA アカウントを設定するときに外部データベースへのアクセスを保護できます。

そのためには、サーバーアドレスと使用するポートのアドレスの後に &quot;**:ssl**&quot; を追加します。例：**192.168.0.52:4501:ssl**。

これで、データはセキュアな SSL プロトコル経由で送信されます。

## 任意の追加設定 {#additional-configurations}

必要に応じて、外部データベースのデータを処理するためのスキーマを作成できます。同様に、Adobe Campaign では外部テーブルのデータでマッピングを定義できます。これらは一般的な設定で、ワークフローだけに適用されるわけではありません。

>[!NOTE]
>
>Adobe Campaign でのスキーマの作成および新しいデータマッピングの定義について詳しくは、[このページ](../../configuration/using/about-schema-edition.md)を参照してください。