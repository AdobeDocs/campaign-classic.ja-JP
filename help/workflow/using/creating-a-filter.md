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
translation-type: ht
source-git-commit: 70b143445b2e77128b9404e35d96b39694d55335
workflow-type: ht
source-wordcount: '228'
ht-degree: 100%

---


# フィルターの作成 {#creating-a-filter}

Adobe Campaign で使用可能なフィルターは、クエリと同じ操作モードで作成されるフィルター条件を使用して定義します。

>[!NOTE]
>
>フィルターの作成について詳しくは、[この節](../../platform/using/filtering-options.md)を参照してください。

**[!UICONTROL 管理／設定／定義済みフィルター]**&#x200B;ノードには、リストおよび概要で使用するすべてのフィルターが含まれています。

例えば、オペレーターのリストを「**[!UICONTROL アクティブなアカウント]**」でフィルターできます。

![](assets/query_editor_filter_sample_1.png)

対応するフィルターには、「**[!UICONTROL オペレーター]**」スキーマの「**[!UICONTROL 無効なアカウント]**」の値に対するクエリが含まれています。

![](assets/query_editor_filter_sample_2.png)

同じリストで、「**[!UICONTROL ログインまたはラベル別]**」フィルターを使用して、フィルターフィールドに入力した値に基づいてリストのデータをフィルターできます。

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

「**[!UICONTROL 次の場合に考慮]**」列では、これらのフィルター条件の適用基準を定義できます。ここでは、文字 **$(/tmp/@text)** は、フィルターにリンクされた入力フィールドの内容を表します。

![](assets/query_editor_filter_sample_5.png)

ここでは、**$(/tmp/@text)=&#39;代理店&#39;** となっています。

**$(/tmp/@text)!=&#39;&#39;** 式は、入力フィールドが空でない場合に各条件を適用します。
