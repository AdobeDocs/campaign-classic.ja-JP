---
title: すべての訪問の収集
seo-title: すべての訪問の収集
description: すべての訪問の収集
seo-description: null
page-status-flag: never-activated
uuid: c2869b3d-33bb-4a22-a8e6-ac037f0665d9
contentOwner: sauviat
products: SG_CAMPAIGN/CLASSIC
audience: configuration
content-type: reference
topic-tags: setting-up-web-tracking
discoiquuid: 7f841368-3867-4d6e-9720-c038d9bea0ce
translation-type: tm+mt
source-git-commit: 70b143445b2e77128b9404e35d96b39694d55335
workflow-type: tm+mt
source-wordcount: '300'
ht-degree: 4%

---


# すべての訪問の収集{#collecting-all-visits}

Adobe Campaignが提供するWebトラッキングモジュールを使用すると、受信者がメッセージ内でクリックした後のサイトトラッキングのコンテキストで、メッセージによって実行されたサイトの特定のページへの訪問回数を収集できます。

ただし、プラットフォームで既知のユーザーがWebトラッキングタグーを使用してページへのすべての訪問を収集するように、プラットフォームを設定できます。

プラットフォームに知られる受信者は、配信が既にターゲットを定め、少なくとも1回は受信メッセージをクリックしたユーザである。 この受信者を識別するには、永続的なcookieが使用されます。

>[!IMPORTANT]
>
>Adobe Campaignプラットフォームは、メッセージをクリックした後のサイト訪問のコンテキストを超えて、Webサイトトラッキングツールとして使用することを意図していません。 このオプションを有効にすると、サーバーをホストするコンピューター（リダイレクト、アプリケーション、およびデータベース）のリソースの使用量が非常に多くなる可能性があります。 この読み込みは、ハードウェアアーキテクチャが確実にサポートし、ホームページなど、最も頻繁にアクセスされるページにWebトラッキングタグを配置しないようにすることをお勧めします。

## サーバー設定 {#server-configuration}

サーバーは、serverConf.xml **ファイルの特定の要素をオーバーロードして設定します** 。 これらのファイルは、Adobe Campaignのインストールディレクトリの **conf** サブディレクトリに保存されます。

### リダイレクトサーバー {#redirection-server}

リダイレクトサーバーの場合、リダイレクト **要素のtrackWebVisitors** 属性を **trueに設定し** ます ****。

```
<redirection P3PCompactPolicy="CAO DSP COR CURa DEVa TAIa OUR BUS IND UNI COM NAV"
databaseId="" defLogCount="30" expirationURL="" maxJobsInCache="100"
startRedirection="true" startRedirectionInModule="true" trackWebVisitors="true"
trackingPassword=""
```

## デフォルトの一致キャンペーンの設定 {#configuring-a-default-matching-campaign}

クライアントコンソールを使用して表示追跡情報を取得するには、次の操作を行う必要があります。

* ダミー **配信を作成します** (配信マッピングはターゲットスキーマのマッピングと同じでなければなりません)。
* NmsTracking_WebTrackingDelivery **配信にこのオプションの****** 内部名を入力します。

電子メール内でのクリックの直後に発生しないサイトトラッキング配信は、作成したダミー情報ですべて表示できます。
