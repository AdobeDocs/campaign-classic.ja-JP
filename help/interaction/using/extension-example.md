---
product: campaign
title: 拡張の例
description: 拡張の例
audience: interaction
content-type: reference
topic-tags: advanced-parameters
exl-id: d4acf99b-cef4-48f7-b4cd-c032ec12592f
source-git-commit: 07a5742c6f142c786ad8ba2f8774e7e90e8cd191
workflow-type: tm+mt
source-wordcount: '153'
ht-degree: 100%

---

# 拡張の例{#extension-example}

![](../../assets/common.svg)

インバウンドコンタクト先（コールセンターや Web サイト）の場合、一連の実施要件ルールを使用して、コンタクト先に対して最も関連度の高いオファーが提案されます。オファーの実施要件の基準をエンリッチメントさせるには、**nms:interaction** スキーマを拡張します。

* 新しいインタラクションコンテキストを追加するには、**nms:interaction** スキーマを拡張し、必要な数の **attribute** 要素をスキーマに作成します。

   次の例では、国コードと直近に閲覧したページの基準を追加しています。

   ![](assets/s_ncs_configuration_offer_schemas.png)

* これで、実施要件の基準を定義する際に、以前作成した属性を利用できます。

   次の例では、ユーザーの居住国や最後に閲覧した Web ページに基づいてオファーを表示するための実施要件基準を作成しています。

   ![](assets/s_ncs_configuration_offer_context.png)

* SOAP 呼び出しを設定する際に、**context** XML 要素を挿入し、インタラクションスキーマに追加されたコンテキスト情報を参照します。詳しくは、[SOAP による統合（サーバーサイド）](../../interaction/using/integration-via-soap--server-side-.md)を参照してください。
