---
product: campaign
title: すべての訪問の収集
description: すべての訪問の収集
feature: Configuration, Instance Settings
role: Developer
exl-id: cc554d0d-bbab-4f72-b870-5fef5a2fda9d
TQID: https://experienceleague.adobe.com/EdEX0IPygnmmYAqewEpX2jRqrCZ723itOEW6DhnMSl8
product_v2:
  - id: dfc56824-e8b9-499e-85d4-21aedb507314
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
source-git-commit: 4c295c0dabae8aba298390a3da2422a3fa1219f9
workflow-type: tm+mt
source-wordcount: 296
ht-degree: 3%

---

# すべての訪問の収集{#collecting-all-visits}

Adobe Campaignが提供するweb トラッキングモジュールを使用すると、受信者がメッセージ内でクリックした後のサイトトラッキングのコンテキストで、受信者が実行したサイトの特定のページへの訪問を収集できます。

ただし、プラットフォームを設定して、プラットフォームで既知のユーザーによるweb トラッキングタグを使用したページへのすべての訪問を収集するように設定できます。

プラットフォームで既知のユーザーとは、配信によって既にターゲティングされており、受信したメッセージを少なくとも1回クリックした受信者です。 永続的なCookieは、この受信者を識別するために使用されます。

>[!IMPORTANT]
>
>Adobe Campaign プラットフォームは、メッセージをクリックした後にサイトにアクセスするコンテキストを超えて、web サイト追跡ツールとして使用することを意図していません。 このオプションを有効にすると、サーバーをホストするマシン（リダイレクト、アプリケーション、データベース）でリソースが非常に多く使用される可能性があります。 ハードウェアアーキテクチャがこの読み込みをサポートできることを確認し、ホームページなど、最も頻繁にアクセスされるページにweb トラッキングタグを配置しないようにすることをお勧めします。

## サーバー設定 {#server-configuration}

サーバーは、**serverConf.xml** ファイルの特定の要素をオーバーロードすることによって設定されます。 これらのファイルは、Adobe Campaign インストールディレクトリの&#x200B;**conf** サブディレクトリに保存されます。

### リダイレクションサーバー {#redirection-server}

リダイレクトサーバーの場合、**redirection**&#x200B;要素の&#x200B;**trackWebVisitors**&#x200B;属性を&#x200B;**true**&#x200B;に設定します。

```
<redirection P3PCompactPolicy="CAO DSP COR CURa DEVa TAIa OUR BUS IND UNI COM NAV"
databaseId="" defLogCount="30" expirationURL="" maxJobsInCache="100"
startRedirection="true" startRedirectionInModule="true" trackWebVisitors="true"
trackingPassword=""
```

## デフォルトのマッチングキャンペーンの設定 {#configuring-a-default-matching-campaign}

クライアントコンソールを使用してトラッキング情報を表示するには、次の操作を行う必要があります。

* **ダミー配信**&#x200B;を作成します（配信マッピングは、ターゲットスキーマのマッピングと同じである必要があります）。
* この配信の&#x200B;**内部名**&#x200B;を&#x200B;**NmsTracking_WebTrackingDelivery** オプションに入力します。

電子メールのクリックの直後ではないサイトのトラッキング情報はすべて、作成されたダミー配信で表示できます。
