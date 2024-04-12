---
product: campaign
title: PostgreSQL へのアクセスの設定
description: PostgreSQL へのアクセスを設定する方法を説明します
feature: Installation, Instance Settings
exl-id: 2c678f45-2555-4647-9885-bd002db7df37
source-git-commit: b666535f7f82d1b8c2da4fbce1bc25cf8d39d187
workflow-type: tm+mt
source-wordcount: '359'
ht-degree: 11%

---

# PostgreSQL へのアクセスの設定 {#configure-fda-postgresql}



Campaign の使用 **連合データアクセス** （FDA）外部 PostgreSQL データベースに保存された情報を処理するオプション。

## PostgreSQL 設定 {#postgresql-configuration}

最初に Libpq をインストールする必要があります。 Libpq を使用すると、クライアントプログラムは PostgreSQL バックエンドサーバに問い合わせを送信し、その問い合わせの結果を受け取ることができます。

へのアクセスを設定するには、次の手順に従います [!DNL PostgreSQL]:

* CentOS の場合、次のコマンドを実行します `sudo apt-get -y install libpq-dev`.

* Linux の場合、次のコマンドを実行します `yum install postgresql-devel`.

* Windows の場合、Libpq はによって実装されます。 `libpq.dll` （Adobe Campaignのインストールに含まれる）。

Adobe Campaignで、以下を設定できます [!DNL PostgreSQL] 外部アカウント。 外部アカウントの設定方法について詳しくは、次を参照してください。 [この節](#postgresql-external).

## PostgreSQL 外部アカウント {#postgresql-external}

>[!NOTE]
>
> PostgreSQL は CentOS 7 および 6 で使用できます。

を作成する必要があります [!DNL PostgreSQL] campaign インスタンスをユーザーに接続するための外部アカウント [!DNL PostgreSQL] 外部データベース。

1. Campaign から **[!UICONTROL エクスプローラー]**&#x200B;を選択し、 **[!UICONTROL 管理]** &#39;>&#39; **[!UICONTROL Platform]** &#39;>&#39; **[!UICONTROL 外部アカウント]**.

1. 「**[!UICONTROL 新規]**」をクリックします。

1. 外部アカウント&#x200B;**[!UICONTROL タイプ]**&#x200B;として、「**[!UICONTROL 外部データベース]**」を選択します。

1. 次の下 **[!UICONTROL 設定]**&#x200B;を選択 [!DNL PostgreSQL, Greenplum] から **[!UICONTROL タイプ]** ドロップダウン。

   ![](assets/postgresql_1.png)

1. の設定 **[!UICONTROL PostgreSQL]** 外部アカウント認証：

   * **[!UICONTROL サーバー]**：の URL [!DNL PostgreSQL] サーバー。

   * **[!UICONTROL アカウント]**：ユーザーの名前。

   * **[!UICONTROL パスワード]**：ユーザーアカウントのパスワード。

   * **[!UICONTROL データベース]**：データベースの名前（オプション）。

   * **[!UICONTROL 作業スキーマ]**：作業用スキーマの名前。 [詳細情報](https://www.postgresql.org/docs/current/ddl-schemas.html)

   * **[!UICONTROL Timezone]**：で設定されたタイムゾーン [!DNL PostgreSQL]. [詳細情報](https://www.postgresql.org/docs/7.2/timezones.html)

1. 「**[!UICONTROL パラメーター]**」タブをクリックし、「**[!UICONTROL 機能をデプロイ]**」ボタンをクリックして機能を作成します。

   >[!NOTE]
   >
   >すべての関数を使用するには、リモートデータベースにAdobe Campaign SQL 関数を作成する必要があります。 詳しくは、[このページ](../../configuration/using/adding-additional-sql-functions.md)を参照してください。

1. クリック **[!UICONTROL 保存]** 設定が完了したら、

コネクタは、次のオプションをサポートしています。

| オプション | 説明 |
|:-:|:-:|
| PGSQL_CONNECT_TIMEOUT | 接続の最大待機時間（秒単位）。 <br>詳しくは、次を参照してください [PostgreSQL ドキュメント](https://www.postgresql.org/docs/12/libpq-connect.html#LIBPQ-CONNECT-CONNECT-TIMEOUT). |
| PGSQL_KEEPALIVES_IDLE | TCP がキープアライブ メッセージをサーバーに送信するまでの非アクティブな時間（秒）。 <br>詳しくは、次を参照してください [PostgreSQL ドキュメント](https://www.postgresql.org/docs/12/libpq-connect.html#LIBPQ-KEEPALIVES-IDLE). |
| PGSQL_KEEPALIVES_INTVL | サーバーによって確認されなかった TCP キープアライブ メッセージが再送信されるまでの秒数です。  <br>詳しくは、次を参照してください [PostgreSQL ドキュメント](https://www.postgresql.org/docs/12/libpq-connect.html#LIBPQ-KEEPALIVES-INTERVAL). |
| PGSQL_KEEPALIVES_CNT | クライアントのサーバーへの接続が停止していると見なされるまで失われる可能性がある TCP キープアライブの数。 <br>詳しくは、次を参照してください [PostgreSQL ドキュメント](https://www.postgresql.org/docs/12/libpq-connect.html#LIBPQ-KEEPALIVES-COUNT). |
