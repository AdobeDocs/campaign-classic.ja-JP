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
index: y
internal: n
snippet: y
translation-type: tm+mt
source-git-commit: 579329d9194115065dff2c192deb0376c75e67bd

---


# すべての訪問の収集{#collecting-all-visits}

Adobe Campaignに用意されているWebトラッキングモジュールを使用すると、メッセージ内でのクリックに続くサイトトラッキングのコンテキストで、受信者が実行したサイトの特定のページへの訪問を収集できます。

ただし、プラットフォームに対して既知のユーザーによるWebトラッキングタグを使用してページへのすべての訪問を収集するように、プラットフォームを設定できます。

プラットフォームに知られるユーザーは、配信によって既にターゲット設定され、少なくとも1回受信メッセージをクリックした受信者です。 永続的なcookieは、この受信者を識別するために使用されます。

>[!CAUTION]
>
>Adobe Campaignプラットフォームは、メッセージをクリックした後のサイト訪問のコンテキストを超えて、Webサイトトラッキングツールとしての使用を想定していません。 このオプションを有効にすると、サーバー（リダイレクト、アプリケーション、およびデータベース）をホストするマシン上のリソースの使用量が非常に多くなる可能性があります。 ハードウェアアーキテクチャがこの読み込みをサポートできること、およびホームページなど最も頻繁に訪問されるページにWebトラッキングタグを配置しないようにすることをお勧めします。

## サーバー設定 {#server-configuration}

サーバーは、 **serverConf.xmlファイルの特定の要素をオーバーロードして設定します** 。 これらのファイルは、Adobe Campaignインスト **ールディレクトリの** confサブディレクトリに保存されます。

### リダイレクトサーバー {#redirection-server}

リダイレクトサーバーの場合、リダイレ **クト要素のtrackWebVisitors** 属性を **** trueに設定します ****。

```
<redirection P3PCompactPolicy="CAO DSP COR CURa DEVa TAIa OUR BUS IND UNI COM NAV"
databaseId="" defLogCount="30" expirationURL="" maxJobsInCache="100"
startRedirection="true" startRedirectionInModule="true" trackWebVisitors="true"
trackingPassword=""
```

## デフォルトの一致キャンペーンの設定 {#configuring-a-default-matching-campaign}

クライアントコンソールからトラッキング情報を表示するには、次の操作を行う必要があります。

* ダミー配 **信を作成** （配信マッピングはターゲットスキーマのマッピングと同じにする必要があります）、
* NmsTracking_WebTrackingDelivery **オプションに** 、この配信の内部名 **を入力します** 。

電子メール内でのクリックの直後以外のサイトトラッキング情報は、作成したダミー配信で表示できます。
