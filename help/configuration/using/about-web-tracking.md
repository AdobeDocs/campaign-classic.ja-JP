---
product: campaign
title: Web トラッキングについて
feature: Configuration, Instance Settings
description: Web トラッキングについて
role: User, Developer
exl-id: 91c31703-75e6-47a4-a877-35682dd687a9
TQID: https://experienceleague.adobe.com/FfA6FEH5WP2JJGVR4BhpjO19Yj4mt8irvyJLwuzCThs
product_v2: id: dfc56824-e8b9-499e-85d4-21aedb507314
role_v2: id: b69b2659-1057-424e-8fc5-ed9e016dc554id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2: id: d3cdead0-685a-4489-9250-4bb709942f66
feature_v2: []
subfeature_v2: []
source-git-commit: bb41e9407ab5853b0194bb325bbf3f17bc3ea232
workflow-type: tm+mt
source-wordcount: 192
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
