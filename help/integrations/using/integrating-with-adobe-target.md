---
product: campaign
title: Adobe Target との統合
description: Adobe Target との統合
audience: integrations
content-type: reference
topic-tags: adobe-target
exl-id: 2e29d090-b87b-4cff-a703-58e1da082f04
source-git-commit: b6e24c63ece12f25b7dafe3fede9e38b3aab2427
workflow-type: tm+mt
source-wordcount: '189'
ht-degree: 40%

---

# Adobe Target との統合{#integrating-with-adobe-target}

![](../../assets/common.svg)

Adobe CampaignをAdobe Targetと共に使用して、E メールのコンテンツを最適化します。

E メールのコンテンツを最適化するには、Adobe Targetでリダイレクトオファーを作成した後、Adobe Campaignを使用して E メールオファーを管理します。 例えば、男性の受信者と女性の受信者に異なるオファーを表示できます。

統合は、電子メールが開かれたときにおこなわれます。 顧客が E メールを開くと、Target に対する呼び出しがおこなわれ、コンテンツの動的バージョンが表示されます。 コンテンツは、すべてのブラウザーでサポートされる静的画像で構成されます。 Target は、オーディエンスまたはセッションレベルでオファーに対する反応を追跡し、そのデータは Target レポートで使用できます。 [詳しくは、 Adobe Targetのドキュメントを参照してください。](https://experienceleague.adobe.com/docs/target/using/integrate/campaign-and-target.html?lang=ja).


>[!NOTE]
>
>この統合が対応するのは、静的画像だけです。残りのコンテンツをパーソナライズすることはできません。

Adobe Target は複数のタイプのデータを使用できます。

* Adobe Campaign データマートからのデータ
* Adobe Target で訪問者 ID にリンクされたセグメント。ただし、使用されるデータに法的制限がない場合に限ります。
* Adobe Target データ：ユーザーエージェント、IP アドレス、位置情報データ
