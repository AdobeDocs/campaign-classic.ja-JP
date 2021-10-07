---
product: campaign
title: Unicode への切り替え
description: Unicode への切り替え
audience: production
content-type: reference
topic-tags: updating-adobe-campaign
exl-id: 4cfecf2f-cf98-42c1-b979-cdd26d5de48b
source-git-commit: 20509f44c5b8e0827a09f44dffdf2ec9d11652a1
workflow-type: tm+mt
source-wordcount: '119'
ht-degree: 7%

---

# Unicode への切り替え{#switching-to-unicode}

![](../../assets/v7-only.svg)

Linux/PostgreSQL の既存の **prod** インスタンスの場合、Unicode に切り替える手順は次のとおりです。

1. データベースに書き込むプロセスを停止します。

   ```
   su - neolane
   nlserver shutdown
   ```

1. データベースをダンプします。

   ```
   su - postgres
   pg_dump mydatabase > mydatabase.sql
   ```

1. Unicode データベースの作成：

   ```
   createdb -E UNICODE mydatabase_unicode
   ```

1. データベースの復元：

   ```
   psql mydatabase_unicode < mydatabase.sql
   ```

1. データベースが Unicode であることを示すオプションを更新します。

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

   データベース識別子に関連する値の前に **u** 文字を追加します (**databaseId**)。

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

   データベース参照を変更します。

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

1. スイッチを確認します。 これをおこなうには、Adobe Campaignコンソールから接続し、次の手順に従います。

   * データ（特にアクセント記号付きの文字）が正しく表示されていることを確認します。
   * 配信を開始し、トラッキングの取得が機能することを確認します。
