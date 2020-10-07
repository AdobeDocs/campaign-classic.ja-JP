---
title: Unicode への切り替え
seo-title: Unicode への切り替え
description: Unicode への切り替え
seo-description: null
page-status-flag: never-activated
uuid: 5f15b285-7377-453a-aa98-ca4cf14a4c80
contentOwner: sauviat
products: SG_CAMPAIGN/CLASSIC
audience: production
content-type: reference
topic-tags: updating-adobe-campaign
discoiquuid: 0f5399a8-860d-4a1b-86a9-9011b973346b
translation-type: tm+mt
source-git-commit: 70b143445b2e77128b9404e35d96b39694d55335
workflow-type: tm+mt
source-wordcount: '122'
ht-degree: 9%

---


# Unicode への切り替え{#switching-to-unicode}

Linux/PostgreSQLの既存の **prod** Instanceの場合、unicodeに切り替える手順は次のとおりです。

1. データベースへの書き込みプロセスを停止します。

   ```
   su - neolane
   nlserver shutdown
   ```

1. データベースをダンプします。

   ```
   su - postgres
   pg_dump mydatabase > mydatabase.sql
   ```

1. Unicodeデータベースの作成：

   ```
   createdb -E UNICODE mydatabase_unicode
   ```

1. データベースの復元：

   ```
   psql mydatabase_unicode < mydatabase.sql
   ```

1. データベースがUnicodeであることを示すオプションを更新します。

   ```
   psql mydatabase_unicode
   update XtkOption set sStringValue = 'u'||sStringValue where sName='XtkDatabaseId' and sStringValue not like 'u%';
   ```

1. トラッキングサーバーでは、次の操作を行います。

   ```
   su - neolane
   cd nl6/conf
   vi config-prod.xml
   ```

   デ追加ータベース識別子( **databaseId******)に関連する値の前にあるu文字：

   ```
   <web>
    <redirection databaseId="u7F0000010554364C" trackingPassword="myPassword="/>
   </web>
   ```

1. データベースを呼び出すサーバーの場合：

   ```
   su - neolane
   cd nl6/conf
   vi config-prod.xml
   ```

   データベース参照の変更：

   ```
   <dataSource name="default">
    <dbcnx encrypted="1" 
    login="<dbuser>:<base_unicode>" password="xxxx="
    provider="postgresql" server="yyyy"/>
   </dataSource>
   ```

1. すべてのマシンを再起動します。

   ```
   /etc/init.d/apache stop
   /etc/init.d/nlserver6 stop
   /etc/init.d/nlserver6 start
   /etc/init.d/apache start
   ```

1. スイッチを確認します。 これを行うには、Adobe Campaignコンソールから接続し、次の操作を行います。

   * データが正しく表示され、特にアクセント付きの文字が正しく表示されていることを確認します。
   * 配信を起動し、トラッキングの取得が機能するかどうかを確認します。

