---
product: campaign
title: Web トラッキングについて
feature: Configuration, Instance Settings
description: Web トラッキングについて
role: User, Developer
exl-id: 91c31703-75e6-47a4-a877-35682dd687a9
source-git-commit: 9f5205ced6b8d81639d4d0cb6a76905a753cddac
workflow-type: tm+mt
source-wordcount: '192'
ht-degree: 4%

---

# Web トラッキングについて{#about-web-tracking}

Adobe Campaignを使用すれば、電子メール内のリンクをクリックしたオーディエンスの行動を追跡できる標準の追跡に加えて、オーディエンスがweb サイトをどのように閲覧しているのかに関するデータを収集できます。 このデータ収集は、web トラッキングモジュールによって実行されます。

インターネットユーザーが特定の配信から電子メール内のトラッキングリンクをクリックすると、連絡されたリダイレクトサーバーは、ブロードログ識別子（broadlogId）および配信識別子（deliveryId）を含むセッションクッキーをデポジットする。

Web クライアントは、ユーザーがWeb トラッキングタグを含むページにアクセスするたびに、このCookieをサーバーに送信します。 これは、セッション全体を通して、つまりweb クライアントが閉じるまで続きます。

リダイレクトサーバーは、次のデータを収集します。

* パラメーターとして送信された識別子を使用して、表示されたページのURL。
* セッション Cookieを介したweb ページの訪問元の配信。
* セッション cookieを介してクリックしたインターネットユーザーの識別子。
* 関連する情報を入力できます。

次の図は、クライアントと様々なサーバー間のダイアログの段階を示しています。

![](assets/d_ncs_integration_webtracking_structure1.png)
