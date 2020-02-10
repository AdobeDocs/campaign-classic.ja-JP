---
title: フィルターの作成
description: クエリを実行する際のフィルターの作成方法を説明します。
page-status-flag: never-activated
uuid: 0556d53e-0fdf-47b3-b1e0-b52e85e0c662
contentOwner: sauviat
products: SG_CAMPAIGN/CLASSIC
audience: workflow
content-type: reference
topic-tags: use-cases
discoiquuid: 7e5605c8-78f2-4011-b317-96a59c699848
index: y
internal: n
snippet: y
translation-type: tm+mt
source-git-commit: cf7c90f0ea9fbce3a4fd53f24189617cbd33fc40

---


# フィルターの作成 {#creating-a-filter}

Adobe Campaign で使用可能なフィルターは、クエリと同じ操作モードで作成されるフィルター条件を使用して定義します。

>[!NOTE]
>
>フィルターの作成について詳しくは、[この節](../../platform/using/filtering-options.md)を参照してください。

ノード **[!UICONTROL Administration > Configuration > Predefined filters]** には、リストおよびオーバービューで使用されるすべてのフィルターが含まれます。

For example, the list of operators can be filtered by **[!UICONTROL Active accounts]**:

![](assets/query_editor_filter_sample_1.png)

The matching filter contains the query on the **[!UICONTROL Account disabled]** value of the **[!UICONTROL Operators]** schema:

![](assets/query_editor_filter_sample_2.png)

For the same list, the **[!UICONTROL By login or label]** filter lets you filter the data on the list based on the value entered in the filter field:

![](assets/query_editor_filter_sample_3.png)

このフィルターは次のように設計されています。

![](assets/query_editor_filter_sample_4.png)

フィルター条件に一致するには、オペレーターアカウントは次のいずれかの条件を満たしている必要があります。

* ラベルに、入力フィールドに入力された文字が含まれている
* オペレーター名に、入力フィールドに入力された文字が含まれている
* 説明領域の内容に、入力フィールドに入力された文字が含まれている

>[!NOTE]
>
>**[!UICONTROL Upper]** 関数を使用すると、大文字と小文字を区別する機能を無効にすることができます。

この列 **[!UICONTROL Taken into account if]** では、これらのフィルター条件の適用条件を定義できます。 ここでは、文字 **$(/tmp/@text)** は、フィルターにリンクされた入力フィールドの内容を表します。

![](assets/query_editor_filter_sample_5.png)

ここでは、**$(/tmp/@text)=&#39;代理店&#39;** となっています。

**$(/tmp/@text)!=&#39;&#39;** 式は、入力フィールドが空でない場合に各条件を適用します。
