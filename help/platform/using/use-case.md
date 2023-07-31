---
product: campaign
title: 使用例
description: 使用例
feature: Subscriptions, Email, Data Management
badge-v7: label="v7" type="Informative" tooltip="Campaign Classicv7 に適用"
badge-v8: label="v8" type="Positive" tooltip="Campaign v8 にも適用されます"
audience: platform
content-type: reference
topic-tags: filtering-data
exl-id: 85ded096-7d27-41b3-8ef2-93f5ca8def82
source-git-commit: 3a9b21d626b60754789c3f594ba798309f62a553
workflow-type: tm+mt
source-wordcount: '288'
ht-degree: 96%

---

# ユースケース{#use-case}



## 購読者のメールフォーマットに対するフィルターの作成 {#creating-a-filter-on-the-email-format-of-subscribers}

この使用例では、受信者の E メールフォーマットに基づいてニュースレターの購読を並べ替えるフィルターの作成方法を示します。

そのためには、定義済みフィルターを使用する必要があります。これらのフィルターは、ドキュメントタイプにリンクされており、**[!UICONTROL 管理／設定／定義済みフィルター]**&#x200B;ノードを使用してアクセスされます。これらのデータフィルターは、アプリケーションでエディター（またはドキュメント）の各タイプに対して使用できます。

データフィルターは定義済みフィルターと同じ方法で作成されますが、フィルターが適用されるドキュメントタイプを選択するための追加のフィールドがあります。

次の手順に従います。

1. **[!UICONTROL 管理／設定／定義済みフィルター]**&#x200B;ノードを使用して新しいフィルターを作成します。
1. **[!UICONTROL リンクを選択]**&#x200B;アイコンをクリックして、対象のドキュメントを選択します。

   ![](assets/s_ncs_user_filter_choose_schema.png)

1. 購読スキーマ（nms:subscription）を選択して、「**[!UICONTROL OK]**」をクリックします。

   ![](assets/s_ncs_user_filter_select_schema.png)

1. **[!UICONTROL リンクを編集]**&#x200B;をクリックして、選択したドキュメントのフィールドを表示します。

   ![](assets/s_ncs_user_filter_edit_schema.png)

   選択したドキュメントのコンテンツを確認できます。

   ![](assets/s_ncs_user_filter_view_schema.png)

   これらのフィールドにアクセスして、フィルターエディターの本文でフィルター条件を定義できます。アプリケーションフィルターは、詳細フィルターと同じ方法で定義されます。[詳細フィルターの作成](../../platform/using/creating-filters.md#creating-an-advanced-filter)を参照してください。

1. E メールフォーマットが定義されていない購読のみを表示する、購読の新しいフィルターを作成します。

   ![](assets/s_ncs_user_filter_parameters.png)

1. 「**[!UICONTROL 保存]**」をクリックして、このタイプのリストの定義済みフィルターにフィルターを追加します。
1. これで、受信者プロファイルの「**[!UICONTROL 購読]**」タブでこのフィルターを使用できます。「**[!UICONTROL フィルター]**」ボタンをクリックすると、「不明なメール形式」フィルターにアクセスできます。

   ![](assets/s_ncs_user_filter_on_events.png)

   現在のフィルターの名前は、リストの上に表示されます。フィルターをキャンセルするには、**[!UICONTROL このフィルターを削除]**&#x200B;アイコンをクリックします。

   ![](assets/s_ncs_user_filter_on_subscriptions.png)
