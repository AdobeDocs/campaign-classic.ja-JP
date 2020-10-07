---
title: Web トラッキングについて
seo-title: Web トラッキングについて
description: Web トラッキングについて
seo-description: null
page-status-flag: never-activated
uuid: 59d18ffb-c26e-4571-8364-5e85ec587349
contentOwner: sauviat
products: SG_CAMPAIGN/CLASSIC
audience: configuration
content-type: reference
topic-tags: setting-up-web-tracking
discoiquuid: 38ba9be9-dabc-41d4-878c-d772955301fe
translation-type: tm+mt
source-git-commit: 70b143445b2e77128b9404e35d96b39694d55335
workflow-type: tm+mt
source-wordcount: '195'
ht-degree: 6%

---


# Web トラッキングについて{#about-web-tracking}

電子メールメッセージ内のリンクをクリックしたときの行動を示す標準的な追跡に加えて、Adobe Campaignプラットフォームでは、インターネットユーザーがWebサイトを閲覧する方法に関する情報を収集できます。 このデータ収集は、Webトラッキングモジュールによって実行されます。

インターネットユーザが、特定の配信から電子メール内の追跡対象リンクをクリックすると、リダイレクトサーバは、ブロードログ識別子(broadlogId)と配信識別子(deliveryId)を含むセッションcookieを預け入れる。

次に、Webクライアントは、ユーザーがWebトラッキングタグーを含むページを訪問するたびに、このCookieをサーバーに送信します。 この処理は、セッション全体（Webクライアントが閉じられるまで）で続行されます。

リダイレクトサーバーは次のデータをこの方法で収集します。

* パラメーターとして送信された識別子を介して表示されたページのURL
* セッションcookieを介した、Webページの訪問元の配信。
* セッションcookieを使用してクリックしたインターネットユーザーの識別子。
* 生成されたビジネス量などの追加情報。

次の図に、クライアントと様々なサーバー間のダイアログのステージを示します。

![](assets/d_ncs_integration_webtracking_structure1.png)

