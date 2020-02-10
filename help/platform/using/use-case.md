---
title: 使用例
seo-title: 使用例
description: 使用例
seo-description: null
page-status-flag: never-activated
uuid: d4c76fdf-d562-4151-93ec-08b4f6563440
contentOwner: sauviat
products: SG_CAMPAIGN/CLASSIC
audience: platform
content-type: reference
topic-tags: filtering-data
discoiquuid: fbc38e33-60a6-4d21-a598-312293d168fb
index: y
internal: n
snippet: y
translation-type: tm+mt
source-git-commit: 51e4d72abf3a1f48700ca38566dbf06dd24594b8

---


# 使用例{#use-case}

## 購読者の E メールフォーマットのフィルターの作成 {#creating-a-filter-on-the-email-format-of-subscribers}

この使用例では、受信者の E メールフォーマットに基づいてニュースレターの購読を並べ替えるフィルターの作成方法を示します。

To do this, we need to use a predefined filer: these filters are linked to a document type and are accessed via the **[!UICONTROL Administration > Configuration > Predefined filters]** node. これらのデータフィルターは、アプリケーションでエディター（またはドキュメント）の各タイプに対して使用できます。

データフィルターは定義済みフィルターと同じ方法で作成されますが、フィルターが適用されるドキュメントタイプを選択するための追加のフィールドがあります。

次の手順に従います。

1. ノードを使用して新しいフィルターを作 **[!UICONTROL Administration > Configuration > Predefined filters]** 成します。
1. Click the **[!UICONTROL Select link]** icon to select the concerned document:

   ![](assets/s_ncs_user_filter_choose_schema.png)

1. 購読スキーマ（nms:subscription）を選択して、「**[!UICONTROL OK]**」をクリックします。

   ![](assets/s_ncs_user_filter_select_schema.png)

1. Click **[!UICONTROL Edit link]** to view the fields of the selected document.

   ![](assets/s_ncs_user_filter_edit_schema.png)

   選択したドキュメントのコンテンツを確認できます。

   ![](assets/s_ncs_user_filter_view_schema.png)

   これらのフィールドにアクセスして、フィルターエディターの本文でフィルター条件を定義できます。アプリケーションフィルターは、詳細フィルターと同じ方法で定義されます。See [Creating an advanced filter](../../platform/using/creating-filters.md#creating-an-advanced-filter).

1. E メールフォーマットが定義されていない購読のみを表示する、購読の新しいフィルターを作成します。

   ![](assets/s_ncs_user_filter_parameters.png)

1. Click **[!UICONTROL Save]** to add a filter to the pre-defined filters for this type of list.
1. You can now use this filter in the **[!UICONTROL Subscriptions]** tab of the recipient profile; you can access the &quot;Unknown e-mail format&quot; filter by clicking the **[!UICONTROL Filters]** button.

   ![](assets/s_ncs_user_filter_on_events.png)

   現在のフィルターの名前は、リストの上に表示されます。フィルターをキャンセルするには、アイコンをクリッ **[!UICONTROL Delete this filter]** クします。

   ![](assets/s_ncs_user_filter_on_subscriptions.png)

