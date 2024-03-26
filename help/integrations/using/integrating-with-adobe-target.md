---
product: campaign
title: Adobe Campaign と Adobe Target の連携
description: Adobe Campaign と Adobe Target の統合方法を説明します
feature: Target Integration
badge-v7: label="v7" type="Informative" tooltip="Campaign Classic v7 に適用されます"
badge-v8: label="v8" type="Positive" tooltip="Campaign v8 にも適用されます"
audience: integrations
content-type: reference
topic-tags: adobe-target
exl-id: 2e29d090-b87b-4cff-a703-58e1da082f04
source-git-commit: 3a9b21d626b60754789c3f594ba798309f62a553
workflow-type: tm+mt
source-wordcount: '204'
ht-degree: 100%

---

# Campaign と Target の連携{#integrating-with-adobe-target}



Adobe Campaign を Adobe Target と連携して使用すると、メールコンテンツを最適化できます。

メールコンテンツを最適化するには、Adobe Target でリダイレクトオファーを作成した後、Adobe Campaign を使用してメールオファーを管理します。例えば、男性の受信者と女性の受信者に異なるオファーを表示できます。

統合は、メールが開かれたときに行われます。顧客がメールを開くと、Target に対する呼び出しが行われて、コンテンツの動的バージョンが表示されます。コンテンツは、すべてのブラウザーでサポートされている静的画像で構成されています。 Target は、オファーに対する反応をオーディエンスレベルまたはセッションレベルで追跡し、そのデータは Target レポートで使用できます。 詳しくは、[Adobe Target のドキュメント](https://experienceleague.adobe.com/docs/target/using/integrate/campaign-and-target.html?lang=ja)を参照してください。


>[!NOTE]
>
>この統合が対応するのは、静的画像だけです。残りのコンテンツをパーソナライズすることはできません。

Adobe Target は複数のタイプのデータを使用できます。

* Adobe Campaign データマートからのデータ
* Adobe Target で訪問者 ID にリンクされたセグメント。ただし、使用されるデータに法的制限がない場合に限ります。
* Adobe Target データ：ユーザーエージェント、IP アドレス、位置情報データ
