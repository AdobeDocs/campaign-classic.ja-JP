---
product: campaign
title: Adobe Target との統合
description: Adobe Target との統合
audience: integrations
content-type: reference
topic-tags: adobe-target
exl-id: 2e29d090-b87b-4cff-a703-58e1da082f04
source-git-commit: 0996cc313be93300bce2f094c97e45a794cd459e
workflow-type: ht
source-wordcount: '171'
ht-degree: 100%

---

# Adobe Target との統合{#integrating-with-adobe-target}

![](../../assets/v7-only.svg)

Adobe Experience Cloud 内での Adobe Campaign と Adobe Target（Classic および Standard）間の統合により、Adobe Campaign の E メール配信に Adobe Target からのオファーを含めることができます。

これは、Adobe Campaign を使用して送信された E メールを受信者が開封すると、Adobe Target が呼び出され、コンテンツの動的バージョンが表示されるという仕組みになっています。この動的バージョンは、E メールの作成時に事前に指定したルールに応じて自動生成されます。

>[!NOTE]
>
>この統合では、静的画像のみをサポートします。残りのコンテンツをパーソナライズすることはできません。

Adobe Target は複数のタイプのデータを使用できます。

* Adobe Campaign データマートからのデータ
* Adobe Target で訪問者 ID にリンクされたセグメント。ただし、使用されるデータに法的制限がない場合に限ります。
* Adobe Target データ：ユーザーエージェント、IP アドレス、位置情報データ

>[!NOTE]
>
>Adobe Campaign と Adobe Target の統合については、[Adobe Target ヘルプページ](https://experienceleague.adobe.com/docs/target/using/integrate/campaign-and-target.html?lang=ja)も参照してください。
