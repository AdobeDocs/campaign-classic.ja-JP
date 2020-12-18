---
solution: Campaign Classic
product: campaign
title: すべての訪問の収集
description: すべての訪問の収集
audience: configuration
content-type: reference
topic-tags: setting-up-web-tracking
translation-type: tm+mt
source-git-commit: 972885c3a38bcd3a260574bacbb3f507e11ae05b
workflow-type: tm+mt
source-wordcount: '297'
ht-degree: 3%

---


# すべての訪問の収集{#collecting-all-visits}

Adobe Campaignが提供するWebトラッキングモジュールを使用すると、受信者がメッセージ内でクリックした後のサイトトラッキングのコンテキストで、メッセージによって実行されたサイトの特定のページへの訪問回数を収集できます。

ただし、プラットフォームで既知のユーザーがWebトラッキングタグーを使用してページへのすべての訪問を収集するように、プラットフォームを設定できます。

プラットフォームに知られる受信者は、配信が既にターゲットを定め、少なくとも1回は受信メッセージをクリックしたユーザである。 この受信者を識別するには、永続的なcookieが使用されます。

>[!IMPORTANT]
>
>Adobe Campaignプラットフォームは、メッセージをクリックした後のサイト訪問のコンテキストを超えて、Webサイトトラッキングツールとして使用することを意図していません。 このオプションを有効にすると、サーバーをホストするコンピューター（リダイレクト、アプリケーション、およびデータベース）のリソースの使用量が非常に多くなる可能性があります。 この読み込みは、ハードウェアアーキテクチャが確実にサポートし、ホームページなど、最も頻繁にアクセスされるページにWebトラッキングタグを配置しないようにすることをお勧めします。

## サーバー設定 {#server-configuration}

サーバーは、**serverConf.xml**&#x200B;ファイルの特定の要素をオーバーロードして設定します。 これらのファイルは、Adobe Campaignのインストールディレクトリの&#x200B;**conf**&#x200B;サブディレクトリに保存されます。

### リダイレクトサーバー{#redirection-server}

リダイレクトサーバーの場合、**redirection**&#x200B;要素の&#x200B;**trackWebVisitors**&#x200B;属性を&#x200B;**true**&#x200B;に設定します。

```
<redirection P3PCompactPolicy="CAO DSP COR CURa DEVa TAIa OUR BUS IND UNI COM NAV"
databaseId="" defLogCount="30" expirationURL="" maxJobsInCache="100"
startRedirection="true" startRedirectionInModule="true" trackWebVisitors="true"
trackingPassword=""
```

## デフォルトの一致キャンペーン{#configuring-a-default-matching-campaign}の設定

クライアントコンソールを使用して表示追跡情報を取得するには、次の操作を行う必要があります。

* **ダミー配信**&#x200B;を作成します(配信マッピングはターゲットスキーマのマッピングと同じでなければなりません)。
* **NmsTracking_WebTrackingDelivery**&#x200B;配信に、このオプションの&#x200B;**内部名**&#x200B;を入力します。

電子メール内でのクリックの直後に発生しないサイトトラッキング配信は、作成したダミー情報ですべて表示できます。
