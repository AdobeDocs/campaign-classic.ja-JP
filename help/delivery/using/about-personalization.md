---
product: campaign
title: パーソナライゼーションの基本を学ぶ
description: Campaign でメッセージをパーソナライズし条件付きコンテンツを使用する方法を説明します。
badge-v8: label="v8 にも適用されます" type="Positive" tooltip="Campaign v8 にも適用されます"
feature: Personalization
role: User
exl-id: 555082a2-1b62-4aa4-b80c-77b1a1ef9491
source-git-commit: e34718caefdf5db4ddd61db601420274be77054e
workflow-type: tm+mt
source-wordcount: '148'
ht-degree: 100%

---

# パーソナライゼーションの基本を学ぶ{#about-personalization}

Adobe Campaign で配信されるメッセージは、コンテンツや外観をいくつかの方法でパーソナライズできます。さらに、受信者のプロファイルから取得した条件に基づいて、それらの方法を組み合わせることもできます。メール配信の場合は、配信の要素やパーソナライゼーション条件を、メッセージの「**[!UICONTROL ソース]**」タブに JavaScript を記述して直接定義できます。Adobe Campaign には、全体として次のようなパーソナライゼーション機能が備わっています。

* メッセージ形式のパーソナライズ：[メッセージコンテンツ](defining-the-email-content.md#message-content)を参照してください。
* パーソナライゼーションフィールドの動的な挿入：[パーソナライゼーションフィールド](personalization-fields.md)を参照してください。
* 定義済みパーソナライゼーションブロックの挿入：[パーソナライゼーションブロック](personalization-blocks.md)を参照してください。
* 条件付きコンテンツの作成：[条件付きコンテンツ](conditional-content.md)の節を参照してください。

>[!CAUTION]
>
>次に示す変数は内部変数です。これらをパーソナライゼーションに使用できますが、値の変更は絶対にしないでください。**delivery**、**message**、**dataSource**、**targetData**、**provider**、**coupon**、**couponValue**、**proposition**。
