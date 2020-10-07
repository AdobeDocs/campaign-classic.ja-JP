---
title: ブロックリストデータベース
seo-title: ブロックリストデータベース
description: ブロックリストデータベース
seo-description: null
page-status-flag: never-activated
uuid: 8a4a69f9-87d5-4044-bc55-76cdcb2e7800
contentOwner: sauviat
products: SG_CAMPAIGN/CLASSIC
audience: delivery
content-type: reference
topic-tags: deliverability-management
discoiquuid: eede254d-2b25-46ed-b10f-fa1d54780a75
translation-type: tm+mt
source-git-commit: 70b143445b2e77128b9404e35d96b39694d55335
workflow-type: tm+mt
source-wordcount: '377'
ht-degree: 97%

---


# ブロックリストデータベース{#blocklisting-databases}

いくつかの組織では、スパム送信者に使用されていると考えられている IP アドレスおよびドメインのデータベースを維持管理しています。これらのサイトを参考にすると、特定のメッセージがスパムとして拒否された理由を理解するのに役立ちます。通常、これらのリストに誤って登録されたアドレスの削除を申請することは可能です。

これらのデータベースは RBL（リアルタイムブラックホールリスト）と呼ばれ、DNS メカニズムを通じて参照されます。次の 3 種類の RBL があります。

* IP アドレス別：スパムを送信しているかスパムを中継している可能性の高い IP アドレスをリストアップします。
* 送信者ドメイン別：スパムを送信しているか誤って設定された送信者ドメイン（バウンスメールアドレスのフルドメイン）をリストアップします。
* Web ドメイン別：スパムコンテンツに含まれているリンクや画像の URL にあるドメイン（登録機関に登録されている高レベルのドメイン）をリストアップします。Adobe Campaign では、通常、考慮に入れるべきドメインは、トラッキングに使用されるアドレスです。

次に、最も広く使用されている RBL のリストを示します。詳細なリストについては、https://www.dnsstuff.com/を参照してくだ [さい](https://tools.dnsstuff.com/)。

* **Spamhaus**

   [https://www.spamhaus.org/](https://www.spamhaus.org/) を参照してください。

   データベースのほうが重要です。このリストで分類されているのは、一般に深刻な状況です。このような状況が発生した場合は、ただちに対応し、商用サービス、配信品質サービスおよび Adobe Campaign サポートに警告を出す必要があります。

* **SpamCop**

   [https://www.spamcop.net/](https://www.spamcop.net/) を参照してください。

   最も有名なデータベースの 1 つです。お使いの IP アドレスのいずれかがこのリストに載っている場合は、一般に、送信したメッセージが SpamCop ユーザーによりスパムであると宣言されたか、SpamCop ハニーポットにメッセージを送信したことがあるという意味です。

* **URIBL**

   [https://www.uribl.com/](https://www.uribl.com/) を参照してください。

   このリストでは、スパムとして宣言されたメッセージで定期的に見られるドメインを特定しています。お使いのドメインがこのリストに載った場合は、配信品質に重大な影響が及ぶおそれがあります。配信品質サービスと Adobe Campaign サポートにただちに知らせる必要があります。

* **SURBL**

   [http://www.surbl.org/](http://www.surbl.org/) を参照してください。

   SURBL では、スパムで定期的に見られる Web サイトを特定しています。お使いのドメインがこのリストに載った場合は、配信品質に重大な影響が及ぶおそれがあります。配信品質サービスと Adobe Campaign サポートにただちに知らせる必要があります。

* **iX Manitu**

   IP アドレスのリストで、ドイツで広く使用されています。[https://www.heise.de/ix/nixspam/](https://www.heise.de/ix/nixspam/) を参照してください。

<!--* SORBS

  [https://www.nl.sorbs.net](https://www.nl.sorbs.net) compiles a list of IP addresses that are reputed to be dynamic IP address (i.e. attributed temporarily to ISP subscribers) or "open relay" addresses. Certain domains check whether the IP address of a sender is not listed on this site before accepting email. Checking the IP addresses on this site can prove useful.-->