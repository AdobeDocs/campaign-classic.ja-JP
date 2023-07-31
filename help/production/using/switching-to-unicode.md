---
product: campaign
title: Unicode への切り替え
description: Unicode への切り替え
feature: Monitoring
badge-v7-only: label="v7" type="Informative" tooltip="Campaign Classicv7 にのみ適用"
badge-v7-prem: label="オンプレミスおよびハイブリッド" type="Caution" url="https://experienceleague.adobe.com/docs/campaign-classic/using/installing-campaign-classic/architecture-and-hosting-models/hosting-models-lp/hosting-models.html?lang=ja" tooltip="オンプレミスデプロイメントとハイブリッドデプロイメントにのみ適用されます"
audience: production
content-type: reference
topic-tags: updating-adobe-campaign
exl-id: 4cfecf2f-cf98-42c1-b979-cdd26d5de48b
source-git-commit: 3a9b21d626b60754789c3f594ba798309f62a553
workflow-type: tm+mt
source-wordcount: '144'
ht-degree: 18%

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

1. データベースを復元します。

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

   次を追加： **u** データベース識別子に関連する値の前の文字 (**databaseId**):

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
