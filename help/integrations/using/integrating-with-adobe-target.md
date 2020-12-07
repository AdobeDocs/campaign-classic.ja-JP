---
solution: Campaign Classic
product: campaign
title: Adobe Target との統合
description: Adobe Target との統合
audience: integrations
content-type: reference
topic-tags: adobe-target
translation-type: ht
source-git-commit: 972885c3a38bcd3a260574bacbb3f507e11ae05b
workflow-type: ht
source-wordcount: '205'
ht-degree: 100%

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
>Adobe Campaign と Adobe Target 間の統合に関する情報は、[Adobe Target ヘルプページ](https://docs.adobe.com/content/help/ja-JP/target/using/integrate/campaign-and-target.html)を参照してください。
