---
product: campaign
title: Web トラッキングについて
description: Web トラッキングについて
audience: configuration
content-type: reference
topic-tags: setting-up-web-tracking
exl-id: 91c31703-75e6-47a4-a877-35682dd687a9
source-git-commit: 98d646919fedc66ee9145522ad0c5f15b25dbf2e
workflow-type: tm+mt
source-wordcount: '192'
ht-degree: 4%

---

# Web トラッキングについて{#about-web-tracking}

Adobe Campaignプラットフォームでは、インターネットユーザーが電子メールメッセージのリンクをクリックしたときの行動を示す標準的なトラッキングに加えて、インターネットユーザーがWebサイトを閲覧した際の情報を収集できます。 このデータ収集は、Webトラッキングモジュールによって実行されます。

インターネットユーザが、特定の配信から電子メール内の追跡対象リンクをクリックすると、リダイレクトサーバは、broadlog識別子(broadlogId)と配信識別子(deliveryId)とを含むセッションcookieを預ける。

次に、Webクライアントは、Webトラッキングタグを含むページにユーザーが訪問するたびに、このCookieをサーバーに送信します。 これは、Webクライアントが閉じられるまで、セッション中続きます。

この方法で、リダイレクションサーバーは次のデータを収集します。

* パラメーターとして送信される識別子を介して表示されたページのURL
* webページの訪問元の配信（セッションcookieを使用）
* セッションcookieを使用してクリックしたインターネットユーザーの識別子。
* 生成されたビジネス量などの追加情報。

次の図は、クライアントと様々なサーバー間のダイアログのステージを示しています。

![](assets/d_ncs_integration_webtracking_structure1.png)
