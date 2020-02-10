---
title: Webトラッキングについて
seo-title: Webトラッキングについて
description: Webトラッキングについて
seo-description: null
page-status-flag: never-activated
uuid: 59d18ffb-c26e-4571-8364-5e85ec587349
contentOwner: sauviat
products: SG_CAMPAIGN/CLASSIC
audience: configuration
content-type: reference
topic-tags: setting-up-web-tracking
discoiquuid: 38ba9be9-dabc-41d4-878c-d772955301fe
index: y
internal: n
snippet: y
translation-type: tm+mt
source-git-commit: 579329d9194115065dff2c192deb0376c75e67bd

---


# Webトラッキングについて{#about-web-tracking}

電子メールメッセージ内のリンクをクリックしたインターネットユーザーの行動を示す標準的な追跡に加えて、Adobe Campaignプラットフォームでは、インターネットユーザーがWebサイトを閲覧する方法に関する情報を収集できます。 このデータ収集は、Webトラッキングモジュールによって実行されます。

インターネットユーザが、所定の配信から電子メール内の追跡対象リンクをクリックすると、リダイレクトサーバは、ブロードログ識別子(broadlogId)と配信識別子(deliveryId)を含むセッションcookieを預け入れるように通信した。

次に、Webクライアントは、ユーザーがWebトラッキングタグを含むページを訪問するたびに、このCookieをサーバーに送信します。 これは、セッション中（Webクライアントが閉じられるまで）続きます。

リダイレクトサーバーは、この方法で次のデータを収集します。

* パラメーターとして送信された識別子を介して表示されたページのURL
* セッションcookieを使用した、Webページの訪問元の配信。
* セッションcookieを使用してクリックしたインターネットユーザーの識別子。
* 生成されたビジネス量などの追加情報。

次の図に、クライアントと様々なサーバー間のダイアログのステージを示します。

![](assets/d_ncs_integration_webtracking_structure1.png)

