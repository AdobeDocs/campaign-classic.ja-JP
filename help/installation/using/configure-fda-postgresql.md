---
product: campaign
title: PostgreSQL へのアクセスの設定
description: PostgreSQL へのアクセスを設定する方法を説明します
feature: Installation, Instance Settings
badge-v7-only: label="v7" type="Informative" tooltip="Campaign Classicv7 にのみ適用"
exl-id: 2c678f45-2555-4647-9885-bd002db7df37
source-git-commit: 3a9b21d626b60754789c3f594ba798309f62a553
workflow-type: tm+mt
source-wordcount: '395'
ht-degree: 14%

---

# PostgreSQL へのアクセスの設定 {#configure-fda-postgresql}



キャンペーンを使用 **Federated Data Access** (FDA) 外部の PostgreSQL データベースに保存された情報を処理するオプション。

## PostgreSQL 設定 {#postgresql-configuration}

最初に Libpq をインストールする必要があります。 Libpq を使用すると、クライアントプログラムは PostgreSQL バックエンドサーバにクエリを送信し、これらのクエリの結果を受け取ることができます。

次の手順に従って、へのアクセスを設定します。 [!DNL PostgreSQL]:

* CentOS の場合は、次のコマンドを実行します。 `sudo apt-get -y install libpq-dev`.

* Linux の場合は、次のコマンドを実行します。 `yum install postgresql-devel`.

* Windows の場合、Libpq は `libpq.dll` Adobe Campaignのインストールに含まれる

Adobe Campaignで、 [!DNL PostgreSQL] 外部アカウント。 外部アカウントの設定方法について詳しくは、 [この節](#postgresql-external).

## PostgreSQL 外部アカウント {#postgresql-external}

>[!NOTE]
>
> PostgreSQL は CentOS 7 および 6 で利用できます。

次を作成する必要があります： [!DNL PostgreSQL] Campaign インスタンスを [!DNL PostgreSQL] 外部データベース。

1. キャンペーンから **[!UICONTROL エクスプローラ]**&#x200B;をクリックし、 **[!UICONTROL 管理]** &#39;>&#39; **[!UICONTROL Platform]** &#39;>&#39; **[!UICONTROL 外部アカウント]**.

1. 「**[!UICONTROL 新規]**」をクリックします。

1. 外部アカウント&#x200B;**[!UICONTROL タイプ]**&#x200B;として、「**[!UICONTROL 外部データベース]**」を選択します。

1. の下 **[!UICONTROL 設定]**&#x200B;を選択します。 [!DNL PostgreSQL, Greenplum] から **[!UICONTROL タイプ]** 」ドロップダウンリストから選択できます。

   ![](assets/postgresql_1.png)

1. を設定します。 **[!UICONTROL PostgreSQL]** 外部アカウント認証：

   * **[!UICONTROL サーバー]**：[!DNL PostgreSQL] サーバーの URL.

   * **[!UICONTROL アカウント]**：ユーザーの名前.

   * **[!UICONTROL パスワード]**：ユーザーアカウントのパスワード.

   * **[!UICONTROL データベース]**：データベースの名前（オプション）。

   * **[!UICONTROL 作業スキーマ]**：作業中のスキーマの名前。 [詳細情報](https://www.postgresql.org/docs/current/ddl-schemas.html)

   * **[!UICONTROL タイムゾーン]**：で設定されたタイムゾーン [!DNL PostgreSQL]. [詳細情報](https://www.postgresql.org/docs/7.2/timezones.html)

1. 「**[!UICONTROL パラメーター]**」タブをクリックし、「**[!UICONTROL 機能をデプロイ]**」ボタンをクリックして機能を作成します。

   >[!NOTE]
   >
   >すべての関数を使用するには、リモートデータベースでAdobe Campaign SQL 関数を作成する必要があります。 詳しくは、[このページ](../../configuration/using/adding-additional-sql-functions.md)を参照してください。

1. クリック **[!UICONTROL 保存]** 設定が完了したら、次の手順に従います。

コネクタは、次のオプションをサポートしています。

| オプション | 説明 |
|:-:|:-:|
| PGSQL_CONNECT_TIMEOUT | 接続の最大待機時間（秒）。 <br>詳しくは、 [PostgreSQL のドキュメント](https://www.postgresql.org/docs/12/libpq-connect.html#LIBPQ-CONNECT-CONNECT-TIMEOUT). |
| PGSQL_KEEPALIVES_IDLE | TCP がキープアライブメッセージをサーバに送信するまでの無操作状態（秒）。 <br>詳しくは、 [PostgreSQL のドキュメント](https://www.postgresql.org/docs/12/libpq-connect.html#LIBPQ-KEEPALIVES-IDLE). |
| PGSQL_KEEPALIVES_INTVL | サーバが確認しなかった TCP キープアライブメッセージを再送信するまでの秒数。  <br>詳しくは、 [PostgreSQL のドキュメント](https://www.postgresql.org/docs/12/libpq-connect.html#LIBPQ-KEEPALIVES-INTERVAL). |
| PGSQL_KEEPALIVES_CNT | クライアントのサーバへの接続が無効と見なされる前に失われる可能性のある TCP キープアライブの数。 <br>詳しくは、 [PostgreSQL のドキュメント](https://www.postgresql.org/docs/12/libpq-connect.html#LIBPQ-KEEPALIVES-COUNT). |
