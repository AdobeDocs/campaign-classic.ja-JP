---
product: campaign
title: Unicodeへの切り替え
description: Unicodeへの切り替え
feature: Monitoring
badge-v7-prem: label="オンプレミス／ハイブリッドのみ" type="Caution" url="https://experienceleague.adobe.com/docs/campaign-classic/using/installing-campaign-classic/architecture-and-hosting-models/hosting-models-lp/hosting-models.html?lang=ja" tooltip="オンプレミスデプロイメントとハイブリッドデプロイメントにのみ適用されます"
audience: production
content-type: reference
topic-tags: updating-adobe-campaign
exl-id: 4cfecf2f-cf98-42c1-b979-cdd26d5de48b
TQID: https://experienceleague.adobe.com/aJOfEU2Pkyc2ekoYnT1duzyjn7XIU--WSHFWrJXwc-0
product_v2: id: dfc56824-e8b9-499e-85d4-21aedb507314
feature_v2: []
subfeature_v2: id: c03a11ff-bdf9-4e5b-b279-f468b4293464id: e519a22f-a06a-42fc-9d09-d78a3ab2c434
source-git-commit: 38eab6b8da73163e4476e91c0ef73f25c3f57546
workflow-type: tm+mt
source-wordcount: 149
ht-degree: 20%

---

# Unicodeへの切り替え{#switching-to-unicode}



Linux/PostgreSQLの既存の&#x200B;**prod** インスタンスの場合、Unicodeに切り替える手順は次のとおりです。

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

1. Unicode データベースを作成します。

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

1. トラッキングサーバーの場合：

   ```
   su - neolane
   cd nl6/conf
   vi config-prod.xml
   ```

   データベース識別子（**databaseId**）に関連する値の前に&#x200B;**u**&#x200B;文字を追加します。

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

1. 切り替えを確認します。 これを行うには、Adobe Campaign コンソールを介して接続し、次の操作を行います。

   * データが正しく表示されているか、特にアクセント文字が正しく表示されているかどうかを確認します。
   * 配信を起動し、トラッキング取得が機能することを確認します。
