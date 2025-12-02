---
product: campaign
title: すべての訪問の収集
description: すべての訪問の収集
feature: Configuration, Instance Settings
role: Developer
exl-id: cc554d0d-bbab-4f72-b870-5fef5a2fda9d
source-git-commit: 9f5205ced6b8d81639d4d0cb6a76905a753cddac
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

サーバーは、**serverConf.xml** ファイルの特定の要素をオーバーロードすることで設定されます。 これらのファイルは、Adobe Campaign インストールディレクトリのサブディレクトリ **conf** に保存されます。

### リダイレクトサーバー {#redirection-server}

リダイレクトサーバーの場合、**redirection** 要素の **trackWebVisitors** 属性を **true** に設定します。

```
<redirection P3PCompactPolicy="CAO DSP COR CURa DEVa TAIa OUR BUS IND UNI COM NAV"
databaseId="" defLogCount="30" expirationURL="" maxJobsInCache="100"
startRedirection="true" startRedirectionInModule="true" trackWebVisitors="true"
trackingPassword=""
```

## デフォルトの一致するキャンペーンの設定 {#configuring-a-default-matching-campaign}

クライアントコンソールを使用してトラッキング情報を表示するには、次の手順に従います。

* **ダミー配信** を作成します（配信マッピングは、ターゲットスキーマのマッピングと同じである必要があります）。
* **NmsTracking_WebTrackingDelivery** オプションに、この配信の **内部名** を入力します。

メール内をクリックした直後ではない、すべてのサイトトラッキング情報は、作成したダミーの配信で表示できます。
