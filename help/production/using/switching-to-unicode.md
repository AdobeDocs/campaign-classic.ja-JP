---
title: Unicodeへの切り替え
seo-title: Unicodeへの切り替え
description: Unicodeへの切り替え
seo-description: null
page-status-flag: never-activated
uuid: 5f15b285-7377-453a-aa98-ca4cf14a4c80
contentOwner: sauviat
products: SG_CAMPAIGN/CLASSIC
audience: production
content-type: reference
topic-tags: updating-adobe-campaign
discoiquuid: 0f5399a8-860d-4a1b-86a9-9011b973346b
index: y
internal: n
snippet: y
translation-type: tm+mt
source-git-commit: 579329d9194115065dff2c192deb0376c75e67bd

---


# Unicodeへの切り替え{#switching-to-unicode}

Linux/PostgreSQLの既存 **のprod** Instanceの場合、Unicodeに切り替える手順は次のとおりです。

1. データベースへの書き込みプロセスを停止します。

   ```
   su - neolane
   nlserver shutdown
   ```

1. データベースのダンプ：

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

1. トラッキングサーバー上：

   ```
   su - neolane
   cd nl6/conf
   vi config-prod.xml
   ```

   データベ **ース識別子** (databaseId ****)に関連する値の前にu文字を追加します。

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

   * データが正しく表示され、特に強調文字が正しく表示されていることを確認します。
   * 配信を開始し、トラッキングの取得が機能することを確認します。

