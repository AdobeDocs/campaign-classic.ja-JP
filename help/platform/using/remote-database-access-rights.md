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
source-git-commit: d2758b5e81d1720a4f01a610e51c4a33995d88d1

---


# リモートデータベースのアクセス権 {#remote-database-access-rights}

まず、ユーザーが FDA で外部データベースの操作を実行できるように、Adobe Campaign で特定のネームド権限を設定する必要があります。

1. Adobe Campaignエクスプ **[!UICONTROL Administration > Access Management > Named Rights]** ローラーでノードを選択します。
1. 任意のラベルを指定して新しい権限を作成します。
1. The **[!UICONTROL Name]** field must take the following format **user:base@server**, where :

   * **user** は、外部データベースのユーザーの名前に対応します。
   * **base** は、外部データベースの名前に対応します。
   * **server** は、外部データベースサーバーの名前に対応します。

      >[!NOTE]
      >
      >**:base** の部分は、Oracle では省略可能です。

1. Save the named right then link it to your chosen user from the **[!UICONTROL Administration > Access Management > Operators]** node of the Adobe Campaign explorer.

次に、外部データベースに格納されているデータを処理できるように、Adobe Campaign ユーザーに少なくともデータベースに対する「書き込み」権限を付与して、作業用テーブルの作成を許可する必要があります。作業用テーブルは Adobe Campaign で自動的に削除されます。

一般に必要となる権限には次のものがあります。

* **CONNECT**：リモートデータベースへの接続
* **READ Data**：顧客データが格納されたテーブルへの読み取り専用アクセス
* **READ &#39;MetaData&#39;**：テーブル構造を取得するためのサーバーデータカタログへのアクセス
* **LOAD**：作業用テーブルへの一括読み込み（収集や結合の作業で必要）
* **TABLE/INDEX/PROCEDURE/FUNCTION** の&#x200B;**CREATE/DROP**
* **EXPLAIN**（推奨）：問題が発生した場合にパフォーマンスの監視に使用
* **WRITE Data**（統合シナリオに応じて）

>[!NOTE]
>
>データベース管理者は、これらの権限を各データベースエンジン特有の権限に対応付ける必要があります。詳しくは、[RDBMS 特有の権限](https://docs.campaign.adobe.com/doc/AC6.1/en/technicalResources/technicalResources.html)を参照してください。