---
product: campaign
title: 拡張の例
description: 拡張の例
feature: Interaction, Offers
badge-v8: label="v8 にも適用されます" type="Positive" tooltip="Campaign v8 にも適用されます"
audience: interaction
content-type: reference
topic-tags: advanced-parameters
exl-id: d4acf99b-cef4-48f7-b4cd-c032ec12592f
TQID: https://experienceleague.adobe.com/TQZaYrJop03HAw47XPFqgmoxb073iC-xztTp-f-5dEk
product_v2: id: dfc56824-e8b9-499e-85d4-21aedb507314
source-git-commit: 4c295c0dabae8aba298390a3da2422a3fa1219f9
workflow-type: tm+mt
source-wordcount: 160
ht-degree: 79%

---

# 拡張の例{#extension-example}



インバウンドコンタクト先（コールセンターや Web サイト）の場合、一連の実施要件ルールを使用して、コンタクト先に対して最も関連度の高いオファーが提案されます。 オファーの適格性基準を強化するには、**nms:interaction** スキーマを拡張します。

* 新しいインタラクションコンテキストを追加するには、**nms:interaction** スキーマを拡張し、スキーマに必要な数の&#x200B;**属性**&#x200B;要素を作成します。

  次の例では、国コードと直近に閲覧したページの基準を追加しています。

  ![](assets/s_ncs_configuration_offer_schemas.png)

* これで、実施要件の基準を定義する際に、以前作成した属性を利用できます。

  次の例では、ユーザーの居住国や最後に閲覧した Web ページに基づいてオファーを表示するための実施要件基準を作成しています。

  ![](assets/s_ncs_configuration_offer_context.png)

* SOAP 呼び出しを設定する際に、**context** XML 要素を挿入し、インタラクションスキーマに追加されたコンテキスト情報を参照します。 詳しくは、[SOAP による統合（サーバーサイド）](../../interaction/using/integration-via-soap-server-side.md)を参照してください。
