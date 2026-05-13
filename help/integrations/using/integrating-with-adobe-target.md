---
product: campaign
title: Adobe Campaign と Adobe Target の連携
description: Adobe Campaign と Adobe Target の統合方法を説明します
feature: Target Integration
badge-v8: label="v8 にも適用されます" type="Positive" tooltip="Campaign v8 にも適用されます"
audience: integrations
content-type: reference
topic-tags: adobe-target
exl-id: 2e29d090-b87b-4cff-a703-58e1da082f04
TQID: https://experienceleague.adobe.com/f58vs0ePAH-7bcfJ8u1GKLzcz0-fHnrwFyOVUWOFW-o
product_v2:
  - id: dfc56824-e8b9-499e-85d4-21aedb507314
feature_v2:
  - id: d5ef99fa-df0c-4153-bf94-105ad0724167
subfeature_v2:
  - id: b1fd1501-3105-4d6b-b4d4-9af53126df75
source-git-commit: 4c295c0dabae8aba298390a3da2422a3fa1219f9
workflow-type: tm+mt
source-wordcount: 209
ht-degree: 100%

---

# Campaign と Target の連携{#integrating-with-adobe-target}



Adobe Campaign を Adobe Target と連携して使用すると、メールコンテンツを最適化できます。

メールコンテンツを最適化するには、Adobe Target でリダイレクトオファーを作成した後、Adobe Campaign を使用してメールオファーを管理します。 例えば、男性の受信者と女性の受信者に異なるオファーを表示できます。

統合は、メールが開かれたときに行われます。 顧客がメールを開くと、Target に対する呼び出しが行われて、コンテンツの動的バージョンが表示されます。 コンテンツは、すべてのブラウザーでサポートされている静的画像で構成されています。 Target は、オファーに対する反応をオーディエンスレベルまたはセッションレベルで追跡し、そのデータは Target レポートで使用できます。 詳しくは、[Adobe Target のドキュメント](https://experienceleague.adobe.com/docs/target/using/integrate/campaign-and-target.html?lang=ja)を参照してください。


>[!NOTE]
>
>この統合では、静的画像のみをサポートします。 残りのコンテンツをパーソナライズすることはできません。

Adobe Target は複数のタイプのデータを使用できます。

* Adobe Campaign データマートからのデータ
* Adobe Target で訪問者 ID にリンクされたセグメント。ただし、使用されるデータに法的制限がない場合に限ります。
* Adobe Target データ：ユーザーエージェント、IP アドレス、位置情報データ
