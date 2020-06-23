---
title: Adobe Target との統合
seo-title: Adobe Target との統合
description: Adobe Target との統合
seo-description: null
page-status-flag: never-activated
uuid: de482b31-0b7b-4669-8a00-28da48c6c5a9
contentOwner: sauviat
products: SG_CAMPAIGN/CLASSIC
audience: integrations
content-type: reference
topic-tags: adobe-target
discoiquuid: 44c7acdd-6b7a-4e88-b2a7-3e9bf8a6eab5
index: y
internal: n
snippet: y
translation-type: tm+mt
source-git-commit: 0c3737b22c7bf4e614c5a2fbe8e8fd954d3ece8a
workflow-type: tm+mt
source-wordcount: '209'
ht-degree: 95%

---


# Adobe Target との統合{#integrating-with-adobe-target}

Adobe Experience Cloud 内での Adobe Campaign と Adobe Target（Classic および Standard）間の統合により、Adobe Campaign の E メール配信に Adobe Target からのオファーを含めることができます。

これは、Adobe Campaign を使用して送信された E メールを受信者が開封すると、Adobe Target が呼び出され、コンテンツの動的バージョンが表示されるという仕組みになっています。この動的バージョンは、E メールを作成したときに事前に指定したルールに応じて自動生成されます。

Adobe Campaign と Adobe Target の統合について詳しくは、[4 つのヒントとテクニック](https://www.adobe.com/content/dam/www/us/en/marketing/campaign/pdfs/Adobe_Campaign_for_Target_Tips_and_Tricks.pdf)を参照してください。
>[!NOTE]
>
>この統合が対応するのは、静的画像だけです。残りのコンテンツをパーソナライズすることはできません。

Adobe Target は複数のタイプのデータを使用できます。

* Adobe Campaign データマートからのデータ
* Adobe Target で訪問者 ID にリンクされたセグメント。ただし、使用されるデータに法的制限がない場合に限ります。
* Adobe Target データ：ユーザーエージェント、IP アドレス、位置情報データ

>[!NOTE]
>
>Adobe Campaign と Adobe Target 間の統合に関する情報は、[Adobe Target ヘルプページ](https://docs.adobe.com/content/help/en/target/using/integrate/campaign-and-target.html)を参照してください。
