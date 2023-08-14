---
product: campaign
title: オファーカテゴリの作成
description: オファーカテゴリの作成
feature: Interaction, Offers
badge-v7-only: label="v7" type="Informative" tooltip="Campaign Classic v7 にのみ適用されます"
audience: interaction
content-type: reference
topic-tags: managing-an-offer-catalog
exl-id: ed97a1b5-c870-4b67-98b6-16adc316fd46
source-git-commit: 3a9b21d626b60754789c3f594ba798309f62a553
workflow-type: ht
source-wordcount: '296'
ht-degree: 100%

---

# オファーカテゴリの作成{#creating-offer-categories}



オファーカテゴリの作成は、**[!UICONTROL デザイン]**&#x200B;環境でのみ実行できます。オファーカテゴリで作成／修正されたオファーが承認されると、オファーカテゴリは、自動的に&#x200B;**[!UICONTROL ライブ]**&#x200B;環境にデプロイされます（つまり、利用できるようになります）。デフォルトでは、**[!UICONTROL デザイン]**&#x200B;環境には、すべてのオファーを受け取るカテゴリが含まれています。サブカテゴリを作成すると、カタログオファーに階層を追加できます。

各カテゴリには実施日を定義できます（この日付を過ぎると、カテゴリに含まれるオファーはターゲットに提示されなくなります）。特定のカテゴリのオファーがオファーエンジンによって優先的に選択されるようにする（例えば、商品の露出度を高める）には、一定期間、カテゴリに乗数の重み付けを追加して重み付けを増加できます。

追加のカテゴリを作成するには、次の手順に従います。

1. **[!UICONTROL オファーカタログ]**&#x200B;フォルダーに移動します。

   ![](assets/offer_cat_create_001.png)

1. 右クリックし、ドロップダウンリストから「**[!UICONTROL 新しい「オファーカテゴリ」フォルダーを作成]**」を選択します。

   ![](assets/offer_cat_create_002.png)

1. カテゴリの名前を変更します。「**[!UICONTROL 一般]**」タブを使用して、後でラベルを編集することもできます。

   ![](assets/offer_cat_create_003.png)

   >[!NOTE]
   >
   >これらの手順を、作成するカテゴリの数だけ繰り返します。

   その後、必要に応じて次の操作を実行します。

   * 「**[!UICONTROL 実施要件]**」タブで、実施日を割り当てます。

     ![](assets/offer_cat_create_004.png)

   * 「**[!UICONTROL テーマ]**」フィールドで、このカテゴリからオファーを選択するのに使用できるキーワードを入力します。

     ![](assets/offer_cat_create_005.png)

     >[!NOTE]
     >
     >オファーエンジンの呼び出し時には、テーマやカテゴリがパラメーターに合致した部分のみがカタログから選択されます。

   * 「**[!UICONTROL 乗数の重み付け]**」フィールドを使用して、一定期間、カテゴリのオファーの重み付けを一時的に「増加」させます。

     ![](assets/offer_cat_create_006.png)

カテゴリに含まれるオファーのダッシュボードでは、実施要件ルールの概要を確認できます。表示するには、オファーの「**[!UICONTROL スケジュールおよび実施要件ルール]**」リンクをクリックします。

![](assets/offer_create_006.png)
