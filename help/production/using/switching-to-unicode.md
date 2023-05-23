---
product: campaign
title: Unicode への切り替え
description: Unicode への切り替え
badge-v7-only: label="v7" type="Informative" tooltip="Applies to Campaign Classic v7 only"
badge-v7-prem: label="on-premise & hybrid" type="Caution" url="https://experienceleague.adobe.com/docs/campaign-classic/using/installing-campaign-classic/architecture-and-hosting-models/hosting-models-lp/hosting-models.html" tooltip="Applies to on-premise and hybrid deployments only"
audience: production
content-type: reference
topic-tags: updating-adobe-campaign
exl-id: 4cfecf2f-cf98-42c1-b979-cdd26d5de48b
source-git-commit: 4661688a22bd1a82eaf9c72a739b5a5ecee168b1
workflow-type: tm+mt
source-wordcount: '119'
ht-degree: 7%

---

# Unicode への切り替え{#switching-to-unicode}



既存の **prod** Linux/PostgreSQL のインスタンスでは、unicode に切り替える手順は次のとおりです。

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

   を **u** データベース識別子に関連する値の前の文字 (**databaseId**):

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

1. スイッチを確認します。 これをおこなうには、Adobe Campaignコンソールから接続し、以下の手順に従います。

   * データが正しく表示されること、特にアクセント記号付き文字が表示されていることを確認します。
   * 配信を開始し、トラッキングの取得が機能することを確認します。
