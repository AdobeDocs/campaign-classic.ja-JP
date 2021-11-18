---
product: campaign
title: Web トラッキングについて
description: Web トラッキングについて
audience: configuration
content-type: reference
topic-tags: setting-up-web-tracking
exl-id: 91c31703-75e6-47a4-a877-35682dd687a9
source-git-commit: f000cb8bae164c22d1ede15db4e763cf50530674
workflow-type: tm+mt
source-wordcount: '192'
ht-degree: 4%

---

# Web トラッキングについて{#about-web-tracking}

![](../../assets/v7-only.svg)

Adobe Campaignプラットフォームでは、インターネットユーザーが E メールメッセージのリンクをクリックしたときの動作を示す標準的なトラッキングに加えて、インターネットユーザーが Web サイトを閲覧した際の方法に関する情報を収集できます。 このデータ収集は、Web トラッキングモジュールによって実行されます。

インターネットユーザーが特定の配信から E メール内の追跡対象リンクをクリックすると、ブロードログ識別子 (broadlogId) と配信識別子 (deliveryId) を含むセッション cookie がリダイレクトサーバーによって送信されます。

次に、Web クライアントは、Web トラッキングタグを含むページにユーザーが訪問するたびに、この Cookie をサーバーに送信します。 これは、Web クライアントが閉じられるまで、セッション中（つまり、）続きます。

この方法で、リダイレクションサーバーは次のデータを収集します。

* パラメーターとして送信された識別子を介して表示されたページの URL
* web ページの訪問元の配信（セッション cookie を使用）
* セッション cookie を使用してクリックしたインターネットユーザーの識別子
* 生成されたビジネス量などの追加情報。

次の図は、クライアントと様々なサーバー間のダイアログのステージを示しています。

![](assets/d_ncs_integration_webtracking_structure1.png)
