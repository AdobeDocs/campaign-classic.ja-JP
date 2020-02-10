---
title: アウトバウンドチャネル
seo-title: アウトバウンドチャネル
description: アウトバウンドチャネル
seo-description: null
page-status-flag: never-activated
uuid: a8a7ce5f-0d18-47f2-b258-34b9471de769
contentOwner: sauviat
products: SG_CAMPAIGN/CLASSIC
audience: interaction
content-type: reference
topic-tags: case-study
discoiquuid: 3bd113c3-da67-4f4f-aa40-f4c7860a8569
index: y
internal: n
snippet: y
translation-type: tm+mt
source-git-commit: 215e4d1ca78938b38b53cae0357612deebf7727b

---


# アウトバウンドチャネル{#offers-on-an-outbound-channel}

## E メールのオファー配信 {#email-offer-delivery}

データベースにアフリカ旅行のカテゴリがあり、各オファーの実施要件、コンテキスト、表示域は既に設定されているとします。これから、E メール経由でオファーを提示するためのキャンペーンを作成します。

1. マーケティングキャンペーンとターゲティングワークフローを作成します。

   ![](assets/offer_delivery_example_001.png)

1. Edit the email delivery and click the **[!UICONTROL Offers]** icon.

   ![](assets/offer_delivery_example_002.png)

1. 休暇シーズンに合ったオファー環境用の E メールスペースを選択します。

   ![](assets/offer_delivery_example_003.png)

1. アフリカ旅行のオファーを含んだカテゴリを選択します。

   ![](assets/offer_delivery_example_004.png)

1. 配信するオファーの数を 2 に設定します。

   ![](assets/offer_delivery_example_005.png)

1. オファー管理ウィンドウを閉じ、配信のコンテンツを作成します。

   ![](assets/offer_delivery_example_006.png)

1. メニューを使用して、最初のオファー提案を挿入し、HTML レンダリング関数を選択します。

   ![](assets/offer_delivery_example_007.png)

1. 2 番目のオファー提案を挿入します。

   ![](assets/offer_delivery_example_008.png)

1. Click **[!UICONTROL Preview]** to preview your offers in the delivery then select a recipient to preview the offers as they will receive them.

   ![](assets/offer_delivery_example_009.png)

1. 配信を保存し、ターゲティングワークフローを開始します。
1. Open your delivery and click the **[!UICONTROL Audit]** tab of your delivery: you can see that the offer engine has selected the propositions to be made from the various offers in the catalog.

   ![](assets/offer_delivery_example_010.png)

## オファーシミュレーションの実行 {#perform-an-offer-simulation}

1. 宇宙で、 **[!UICONTROL Profiles and Targets]** リンクをクリック **[!UICONTROL Simulations]** し、ボタンをクリックし **[!UICONTROL Create]** ます。

   ![](assets/offer_simulation_001.png)

1. ラベルを選択し、必要に応じて実行設定を指定します。

   ![](assets/offer_simulation_example_002.png)

1. シミュレーションを保存します。新しいタブが表示されます。

   ![](assets/offer_simulation_example_003.png)

1. タブをクリ **[!UICONTROL Edit]** ックし、次に **[!UICONTROL Scope]**。

   ![](assets/offer_simulation_example_004.png)

1. オファーをシミュレートするカテゴリを選択します。

   ![](assets/offer_simulation_example_005.png)

1. シミュレーションに使用するオファースペースを選択します。

   ![](assets/offer_simulation_example_006.png)

1. 有効制限日を入力します。ここでは、少なくとも開始日を指定する必要があります。この情報は、特定の日において有効なオファーを絞り込むためにオファーエンジンで使用されます。
1. 必要な場合は、1 つまたは複数のテーマを選択し、このキーワードが設定に含まれているオファーのみを提案の対象としてオファー数を限定します。

   この例では、「**Travel**」（旅行）カテゴリの下に、2 つのテーマを持つ 2 つのサブカテゴリがあります。「**Customers>1 year**」（1 年を超える顧客）のテーマに属するオファーに関するシミュレーションを実行することにします。

   ![](assets/offer_simulation_example_007.png)

1. ターゲットにする受信者を選択します。

   ![](assets/offer_simulation_example_008.png)

1. 各受信者に送信されるオファーの数を設定します。

   この例では、オファーエンジンにより、各受信者に対して重み付けが最も大きい 3 つのオファーが選択されます。

   ![](assets/offer_simulation_example_009.png)

1. Save your settings, then click **[!UICONTROL Start]** in the **[!UICONTROL Dashboard]** tab to run the simulation.

   ![](assets/offer_simulation_example_010.png)

1. Once the simulation is finished, consult the **[!UICONTROL Results]** for a detailed breakdown of propositions per offer.

   この例では、オファーエンジンによって 3 件の提案を基にした分類が表示されています。

   ![](assets/offer_simulation_example_011.png)

1. オファーを表 **[!UICONTROL Breakdown of offers by rank]** 示して、オファーエンジンによって選択されたオファーのリストを表示します。

   ![](assets/offer_simulation_example_012.png)

1. If necessary, you can change the scope settings and run the simulation again by clicking **[!UICONTROL Start simulation]**.

   ![](assets/offer_simulation_example_010.png)

1. シミュレーションデータの保存が必要な場合は、レポートの履歴機能または書き出し機能を使用して保存できます。

   ![](assets/offer_simulation_example_013.png)

