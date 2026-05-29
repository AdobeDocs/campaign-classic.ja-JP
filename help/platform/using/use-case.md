---
product: campaign
title: ユースケース
description: ユースケース
feature: Subscriptions, Email, Data Management
audience: platform
content-type: reference
topic-tags: filtering-data
exl-id: 85ded096-7d27-41b3-8ef2-93f5ca8def82
hide: true
TQID: https://experienceleague.adobe.com/WuZ0tN8noOI48gW8vl4-923lo2aC8-Jcaz6Ph76nlmE
product_v2:
  - id: dfc56824-e8b9-499e-85d4-21aedb507314
feature_v2:
  - id: c5474392-5419-4296-9e41-f6f4ce4f6e9b
  - id: afa4204e-6d08-4e29-bc35-26aafb656d48
topic_v2:
  - id: ebde5b41-29c9-4f5e-9ef6-1197e85409e3
  - id: eddd9b14-83bd-4ff4-9072-54a4a484abb7
subfeature_v2:
  - id: f529d0bd-1401-4c88-9833-43228cc1d40f
  - id: e739ee2b-6228-412e-878f-45de0791417d
source-git-commit: 38eab6b8da73163e4476e91c0ef73f25c3f57546
workflow-type: tm+mt
source-wordcount: 293
ht-degree: 100%

---

# 使用例{#use-case}



## 登録者のメールフォーマットに対するフィルターの作成 {#creating-a-filter-on-the-email-format-of-subscribers}

この使用例では、受信者のメールフォーマットに基づいてニュースレターの購読を並べ替えるフィルターの作成方法を示します。

そのためには、定義済みフィルターを使用する必要があります。これらのフィルターは、ドキュメントタイプにリンクされており、**[!UICONTROL 管理／設定／定義済みフィルター]**&#x200B;ノードを使用してアクセスされます。 これらのデータフィルターは、アプリケーションでエディター（またはドキュメント）の各タイプに対して使用できます。

データフィルターは定義済みフィルターと同じ方法で作成されますが、フィルターが適用されるドキュメントタイプを選択するための追加のフィールドがあります。

次の手順に従います。

1. **[!UICONTROL 管理／設定／定義済みフィルター]**&#x200B;ノードを使用して新しいフィルターを作成します。
1. **[!UICONTROL リンクを選択]**&#x200B;アイコンをクリックして、対象のドキュメントを選択します。

   ![](assets/s_ncs_user_filter_choose_schema.png)

1. 購読スキーマ (nms:subscription) を選択して、「**[!UICONTROL OK]**」をクリックしｍさう。

   ![](assets/s_ncs_user_filter_select_schema.png)

1. **[!UICONTROL リンクを編集]**&#x200B;をクリックして、選択したドキュメントのフィールドを表示します。

   ![](assets/s_ncs_user_filter_edit_schema.png)

   選択したドキュメントのコンテンツを確認できます。

   ![](assets/s_ncs_user_filter_view_schema.png)

   これらのフィールドにアクセスして、フィルターエディターの本文でフィルター条件を定義できます。 アプリケーションフィルターは、詳細フィルターと同じ方法で定義されます。 フィルターについて詳しくは、[Campaign v8（コンソール）ドキュメント](https://experienceleague.adobe.com/ja/docs/campaign/campaign-v8/audience/create-filters){target=_blank}を参照してください。


1. メールフォーマットが定義されていない購読のみを表示する、購読の新しいフィルターを作成します。

   ![](assets/s_ncs_user_filter_parameters.png)

1. 「**[!UICONTROL 保存]**」をクリックして、このタイプのリストの定義済みフィルターにフィルターを追加します。
1. これで、受信者プロファイルの「**[!UICONTROL 購読]**」タブでこのフィルターを使用できます。「**[!UICONTROL フィルター]**」ボタンをクリックすると、「不明なメールフォーマット」フィルターにアクセスできます。

   ![](assets/s_ncs_user_filter_on_events.png)

   現在のフィルターの名前は、リストの上に表示されます。 フィルターをキャンセルするには、**[!UICONTROL このフィルターを削除]**&#x200B;アイコンをクリックします。

   ![](assets/s_ncs_user_filter_on_subscriptions.png)
