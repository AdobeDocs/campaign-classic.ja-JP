---
solution: Campaign Classic
product: campaign
title: Web トラッキングについて
description: Web トラッキングについて
audience: configuration
content-type: reference
topic-tags: setting-up-web-tracking
translation-type: tm+mt
source-git-commit: 972885c3a38bcd3a260574bacbb3f507e11ae05b
workflow-type: tm+mt
source-wordcount: '192'
ht-degree: 4%

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

