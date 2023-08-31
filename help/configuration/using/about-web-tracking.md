---
product: campaign
title: Web トラッキングについて
feature: Configuration, Instance Settings
description: Web トラッキングについて
role: User, Data Engineer, Developer
badge-v7-only: label="v7" type="Informative" tooltip="Campaign Classic v7 にのみ適用されます"
exl-id: 91c31703-75e6-47a4-a877-35682dd687a9
source-git-commit: 28638e76bf286f253bc7efd02db848b571ad88c4
workflow-type: tm+mt
source-wordcount: '199'
ht-degree: 8%

---

# Web トラッキングについて{#about-web-tracking}

Adobe Campaignプラットフォームでは、インターネットユーザーが E メールメッセージのリンクをクリックしたときの動作を示す標準的なトラッキングに加えて、インターネットユーザーが Web サイトを閲覧した際の方法に関する情報を収集できます。 このデータ収集は、Web トラッキングモジュールによって実行されます。

インターネットユーザーが特定の配信から E メール内の追跡対象リンクをクリックすると、ブロードログ識別子 (broadlogId) と配信識別子 (deliveryId) を含むセッション cookie がリダイレクトサーバーによって送信されます。

次に、Web クライアントは、Web トラッキングタグを含むページにユーザーが訪問するたびに、この Cookie をサーバーに送信します。 これは、Web クライアントが閉じられるまで、セッション中（つまり、）続きます。

この方法で、リダイレクションサーバーは次のデータを収集します。

* パラメーターとして送信された識別子を介して表示されたページの URL
* web ページの訪問元の配信（セッション cookie を使用）
* セッション cookie を使用してクリックしたインターネットユーザーの識別子。
* 生成されたビジネス量などの追加情報。

次の図は、クライアントと様々なサーバー間のダイアログのステージを示しています。

![](assets/d_ncs_integration_webtracking_structure1.png)
