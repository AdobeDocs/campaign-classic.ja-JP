---
product: campaign
title: すべての訪問の収集
description: すべての訪問の収集
audience: configuration
content-type: reference
topic-tags: setting-up-web-tracking
exl-id: cc554d0d-bbab-4f72-b870-5fef5a2fda9d
source-git-commit: 20509f44c5b8e0827a09f44dffdf2ec9d11652a1
workflow-type: tm+mt
source-wordcount: '297'
ht-degree: 3%

---

# すべての訪問の収集{#collecting-all-visits}

![](../../assets/v7-only.svg)

Adobe Campaignが提供する Web トラッキングモジュールを使用すると、メッセージをクリックした後のサイトトラッキングのコンテキストで、受信者が実行した、サイトの特定のページへの訪問回数を収集できます。

ただし、プラットフォームで既知のユーザーが Web トラッキングタグを使用してページへのすべての訪問を収集するようにプラットフォームを設定することはできます。

プラットフォームで認識されるユーザーとは、配信のターゲットとなっていて、少なくとも 1 回受信したメッセージをクリックした受信者を指します。 永続的な Cookie は、この受信者を識別するために使用されます。

>[!IMPORTANT]
>
>Adobe Campaignプラットフォームは、メッセージをクリックした後にサイトを訪問するコンテキスト以外の、Web サイトトラッキングツールとして使用することを意図していません。 このオプションを有効にすると、サーバーをホストするマシン（リダイレクト、アプリケーション、データベース）上のリソースの使用量が非常に多くなる場合があります。 この読み込みをハードウェアアーキテクチャでサポートできること、およびホームページなど、最も頻繁に訪問されるページに Web トラッキングタグを配置しないようにすることをお勧めします。

## サーバー設定 {#server-configuration}

サーバーは、**serverConf.xml** ファイルの特定の要素をオーバーロードすることで設定されます。 これらのファイルは、Adobe Campaignインストールディレクトリの **conf** サブディレクトリに保存されます。

### リダイレクトサーバー {#redirection-server}

リダイレクションサーバーの場合、**redirection** 要素の **trackWebVisitors** 属性を **true** に設定します。

```
<redirection P3PCompactPolicy="CAO DSP COR CURa DEVa TAIa OUR BUS IND UNI COM NAV"
databaseId="" defLogCount="30" expirationURL="" maxJobsInCache="100"
startRedirection="true" startRedirectionInModule="true" trackWebVisitors="true"
trackingPassword=""
```

## デフォルトの一致キャンペーンの設定 {#configuring-a-default-matching-campaign}

クライアントコンソールからトラッキング情報を表示するには、次の操作が必要です。

* **ダミー配信** を作成します（配信マッピングはターゲットスキーマのマッピングと同じである必要があります）。
* **NmsTracking_WebTrackingDelivery** オプションに、この配信の **内部名** を入力します。

E メール内でのクリックの直後にないすべてのサイトトラッキング情報は、作成したダミー配信で表示できます。
