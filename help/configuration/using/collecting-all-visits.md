---
product: campaign
title: すべての訪問の収集
description: すべての訪問の収集
audience: configuration
content-type: reference
topic-tags: setting-up-web-tracking
exl-id: cc554d0d-bbab-4f72-b870-5fef5a2fda9d
source-git-commit: 98d646919fedc66ee9145522ad0c5f15b25dbf2e
workflow-type: tm+mt
source-wordcount: '297'
ht-degree: 3%

---

# すべての訪問の収集{#collecting-all-visits}

Adobe Campaignが提供するWebトラッキングモジュールを使用すると、メッセージをクリックした後のサイトトラッキングのコンテキストで、受信者が実行したサイトの特定のページへの訪問を収集できます。

ただし、プラットフォームで既知のユーザーによるWebトラッキングタグを使用してページへのすべての訪問を収集するように、プラットフォームを設定することはできます。

プラットフォームに認知されるユーザーとは、配信のターゲットとなっていて、少なくとも1回受信メッセージをクリックした受信者です。 永続的なCookieを使用してこの受信者を識別します。

>[!IMPORTANT]
>
>Adobe Campaignプラットフォームは、メッセージのクリック後にサイトを訪問するコンテキスト以外の、Webサイトトラッキングツールとして使用することを意図していません。 このオプションを有効にすると、サーバーをホストするマシン（リダイレクト、アプリケーション、データベース）上のリソースの使用量が非常に多くなる場合があります。 この読み込みをハードウェアアーキテクチャでサポートできるようにし、ホームページなど、最も頻繁に訪問されるページにWebトラッキングタグを配置しないようにすることをお勧めします。

## サーバー設定 {#server-configuration}

サーバーは、**serverConf.xml**&#x200B;ファイルの特定の要素をオーバーロードすることで設定されます。 これらのファイルは、Adobe Campaignインストールディレクトリの&#x200B;**conf**&#x200B;サブディレクトリに保存されます。

### リダイレクションサーバー{#redirection-server}

リダイレクションサーバーの場合、**redirection**&#x200B;要素の&#x200B;**trackWebVisitors**&#x200B;属性を&#x200B;**true**&#x200B;に設定します。

```
<redirection P3PCompactPolicy="CAO DSP COR CURa DEVa TAIa OUR BUS IND UNI COM NAV"
databaseId="" defLogCount="30" expirationURL="" maxJobsInCache="100"
startRedirection="true" startRedirectionInModule="true" trackWebVisitors="true"
trackingPassword=""
```

## デフォルトの一致キャンペーン{#configuring-a-default-matching-campaign}の設定

クライアントコンソールからトラッキング情報を表示するには、次の操作が必要です。

* **ダミーの配信**&#x200B;を作成します（配信マッピングはターゲットスキーマのマッピングと同じである必要があります）。
* **NmsTracking_WebTrackingDelivery**&#x200B;オプションに、この配信の&#x200B;**内部名**&#x200B;を入力します。

Eメールのクリックの直後に発生しないすべてのサイトトラッキング情報は、作成したダミー配信で表示できます。
