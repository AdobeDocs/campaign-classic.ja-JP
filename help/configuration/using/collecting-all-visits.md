---
product: campaign
title: すべての訪問の収集
description: すべての訪問の収集
feature: Configuration, Instance Settings
role: Data Engineer, Developer
badge-v7-only: label="v7" type="Informative" tooltip="Campaign Classic v7 にのみ適用されます"
exl-id: cc554d0d-bbab-4f72-b870-5fef5a2fda9d
source-git-commit: 28638e76bf286f253bc7efd02db848b571ad88c4
workflow-type: tm+mt
source-wordcount: '304'
ht-degree: 5%

---

# すべての訪問の収集{#collecting-all-visits}

Adobe Campaignが提供する Web トラッキングモジュールを使用すると、メッセージをクリックした後のサイトトラッキングのコンテキストで、受信者が実行したサイトの特定のページへの訪問回数を収集できます。

ただし、プラットフォームを設定して、プラットフォームに知られているユーザーによる Web トラッキングタグを使用して、ページに対するすべての訪問を収集することはできます。

プラットフォームに知られるユーザーとは、配信のターゲットに既になっていて、少なくとも 1 回受信メッセージをクリックした受信者を指します。 この受信者の識別には、永続的な Cookie が使用されます。

>[!IMPORTANT]
>
>Adobe Campaignプラットフォームは、メッセージをクリックした後にサイトに訪問するコンテキスト以外の、Web サイトトラッキングツールとしての使用を目的としていません。 このオプションを有効にすると、サーバーをホストするマシン（リダイレクト、アプリケーション、データベース）上のリソースの使用量が非常に多くなる場合があります。 この読み込みをハードウェアアーキテクチャで確実にサポートできるようにし、また、ホームページなど、最も頻繁にアクセスするページに Web トラッキングタグを配置しないようにすることをお勧めします。

## サーバー設定 {#server-configuration}

サーバーは、 **serverConf.xml** ファイル。 これらのファイルは、 **conf** Adobe Campaignインストールディレクトリのサブディレクトリ。

### リダイレクトサーバー {#redirection-server}

リダイレクションサーバーの場合、 **trackWebVisitors** の属性 **リダイレクト** 要素から **true**.

```
<redirection P3PCompactPolicy="CAO DSP COR CURa DEVa TAIa OUR BUS IND UNI COM NAV"
databaseId="" defLogCount="30" expirationURL="" maxJobsInCache="100"
startRedirection="true" startRedirectionInModule="true" trackWebVisitors="true"
trackingPassword=""
```

## デフォルトの一致キャンペーンの設定 {#configuring-a-default-matching-campaign}

クライアントコンソールからトラッキング情報を表示するには、次の操作を行う必要があります。

* の作成 **ダミー配信** （配信マッピングは、ターゲットスキーマのマッピングと同一である必要があります）。
* 次を入力します。 **内部名** 配信の **NmsTracking_WebTrackingDelivery** オプション。

E メールのクリックの直後にないすべてのサイトトラッキング情報は、作成したダミー配信で表示できます。
