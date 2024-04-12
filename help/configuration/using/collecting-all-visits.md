---
product: campaign
title: すべての訪問の収集
description: すべての訪問の収集
feature: Configuration, Instance Settings
role: Data Engineer, Developer
exl-id: cc554d0d-bbab-4f72-b870-5fef5a2fda9d
source-git-commit: b666535f7f82d1b8c2da4fbce1bc25cf8d39d187
workflow-type: tm+mt
source-wordcount: '296'
ht-degree: 3%

---

# すべての訪問の収集{#collecting-all-visits}

Adobe Campaignが提供する web トラッキングモジュールを使用すると、メッセージがクリックされた後に、サイトトラッキングのコンテキストで受信者が実行したサイトの特定のページへの訪問を収集できます。

ただし、プラットフォームを設定して、そのプラットフォームに既知のユーザーによる web トラッキングタグを持つページへのすべての訪問を収集することができます。

プラットフォームで認識されるユーザーとは、既に配信のターゲットとなっており、受信メッセージを少なくとも 1 回クリックした受信者です。 この受信者の識別には、永続的な Cookie が使用されます。

>[!IMPORTANT]
>
>Adobe Campaign プラットフォームは、メッセージをクリックしてサイトにアクセスするコンテキスト以外で web サイトトラッキングツールとして使用するためのものではありません。 このオプションを有効にすると、サーバー（リダイレクト、アプリケーションおよびデータベース）をホストするマシン上でリソースの使用率が非常に高くなる可能性があります。 ハードウェアアーキテクチャがこの読み込みをサポートできることを確認し、ホームページなど、最も頻繁にアクセスするページに web トラッキングタグを配置しないようにすることをお勧めします。

## サーバー設定 {#server-configuration}

サーバーは、の特定の要素をオーバーロードすることで設定されます。 **serverConf.xml** ファイル。 これらのファイルは、 **conf** Adobe Campaign インストールディレクトリのサブディレクトリ。

### リダイレクトサーバー {#redirection-server}

リダイレクトサーバーには、 **trackWebVisitors** 属性 **リダイレクト** 要素の移動先 **true**.

```
<redirection P3PCompactPolicy="CAO DSP COR CURa DEVa TAIa OUR BUS IND UNI COM NAV"
databaseId="" defLogCount="30" expirationURL="" maxJobsInCache="100"
startRedirection="true" startRedirectionInModule="true" trackWebVisitors="true"
trackingPassword=""
```

## デフォルトの一致するキャンペーンの設定 {#configuring-a-default-matching-campaign}

クライアントコンソールを使用してトラッキング情報を表示するには、次の手順に従います。

* を作成 **ダミー配信** 配信マッピングは、ターゲットスキーマのマッピングと同一である必要があります。
* を入力 **内部名** この配信の **NmsTracking_WebTrackingDelivery** オプション。

メール内をクリックした直後ではない、すべてのサイトトラッキング情報は、作成したダミーの配信で表示できます。
