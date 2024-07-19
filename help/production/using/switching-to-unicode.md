---
product: campaign
title: Unicode への切り替え
description: Unicode への切り替え
feature: Monitoring
badge-v7-prem: label="オンプレミス／ハイブリッドのみ" type="Caution" url="https://experienceleague.adobe.com/docs/campaign-classic/using/installing-campaign-classic/architecture-and-hosting-models/hosting-models-lp/hosting-models.html?lang=ja" tooltip="オンプレミスデプロイメントとハイブリッドデプロイメントにのみ適用されます"
audience: production
content-type: reference
topic-tags: updating-adobe-campaign
exl-id: 4cfecf2f-cf98-42c1-b979-cdd26d5de48b
source-git-commit: 14ba450ebff9bba6a36c0df07d715b7279604222
workflow-type: tm+mt
source-wordcount: '130'
ht-degree: 8%

---

# Unicode への切り替え{#switching-to-unicode}



Linux/PostgreSQL の既存の **prod** インスタンスの場合、Unicode に切り替える手順は次のとおりです。

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

1. Unicode データベースを作成します。

   ```
   createdb -E UNICODE mydatabase_unicode
   ```

1. データベースを復元します。

   ```
   psql mydatabase_unicode < mydatabase.sql
   ```

1. データベースが Unicode であることを示すオプションを更新します。

   ```
   psql mydatabase_unicode
   update XtkOption set sStringValue = 'u'||sStringValue where sName='XtkDatabaseId' and sStringValue not like 'u%';
   ```

1. トラッキングサーバーで：

   ```
   su - neolane
   cd nl6/conf
   vi config-prod.xml
   ```

   データベース識別子（**databaseId**）に関連する値の前に **u** 文字を追加します。

   ```
   <web>
    <redirection databaseId="u7F0000010554364C" trackingPassword="myPassword="/>
   </web>
   ```

1. データベースを呼び出すサーバー上：

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

1. 切り替えを確認します。 これを行うには、Adobe Campaign コンソールを使用して接続し、次の手順を実行します。

   * データ、特にアクセント記号が正しく表示されていることを確認します。
   * 配信を開始し、トラッキング取得が機能することを確認します。
