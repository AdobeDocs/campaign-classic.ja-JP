---
solution: Campaign Classic
product: campaign
title: Unicode への切り替え
description: Unicode への切り替え
audience: production
content-type: reference
topic-tags: updating-adobe-campaign
translation-type: tm+mt
source-git-commit: 972885c3a38bcd3a260574bacbb3f507e11ae05b
workflow-type: tm+mt
source-wordcount: '119'
ht-degree: 7%

---


# Unicode への切り替え{#switching-to-unicode}

Linux/PostgreSQLの既存の&#x200B;**prod**&#x200B;インスタンスの場合、unicodeに切り替える手順は次のとおりです。

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

   デ追加ータベース識別子(**databaseId**)に関連する値の前にある&#x200B;**u**&#x200B;文字：

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

