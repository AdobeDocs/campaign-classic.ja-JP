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

Adobe Campaign Platform を使用すると、インターネットユーザーがメールメッセージ内のリンクをクリックする際の動作を示す標準のトラッキングに加えて、インターネットユーザーが web サイトを閲覧する方法に関する情報を収集できます。 このデータ収集は、Web トラッキングモジュールによって実行されます。

インターネットユーザーが、特定の配信からのメール内のトラッキング対象リンクをクリックすると、リダイレクトサーバーは、broadlog 識別子（broadlogId）と配信識別子（deliveryId）を含むセッション cookie をデポジットします。

次に、web クライアントは、ユーザーが web トラッキングタグを含むページにアクセスするたびに、この cookie をサーバーに送信します。 これは、Web クライアントが閉じられるまで、セッション全体で継続されます。

リダイレクトサーバーは、次の方法でデータを収集します。

* パラメーターとして送信された識別子を使用して表示されたページの URL。
* セッション cookie を介して web ページが訪問された配信。
* セッション cookie を使用してクリックしたインターネットユーザーの識別子
* 追加情報（生成された事業量など）。

次の図は、クライアントと様々なサーバー間のダイアログの段階を示しています。

![](assets/d_ncs_integration_webtracking_structure1.png)
