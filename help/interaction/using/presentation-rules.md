---
title: プレゼンテーションルール
seo-title: プレゼンテーションルール
description: プレゼンテーションルール
seo-description: null
page-status-flag: never-activated
uuid: 460f06f8-cdb9-401d-a45e-e54e56d66781
contentOwner: sauviat
products: SG_CAMPAIGN/CLASSIC
audience: interaction
content-type: reference
topic-tags: case-study
discoiquuid: 8ef303b4-d9ce-40ee-a6c6-ed5012ab8eb8
index: y
internal: n
snippet: y
translation-type: tm+mt
source-git-commit: 28614a6b0c45deef17d9b3275a16e65bdff4538b

---


# プレゼンテーションルール{#presentation-rules}

## プレゼンテーションルールの作成 {#creating-a-presentation-rule}

欧州、アフリカ、米国、カナダ向けの旅行オファーがデータベースに数件格納されている事例があるとします。これからカナダ旅行のオファーを送信しますが、受信者からこの種のオファーが拒否された場合は、以後送信しないようにする必要があります。

そこで、カナダ旅行のオファーを受信者 1 人につき 1 回のみ送信し、拒否された場合は二度と送信しないようにルールを設定します。

1. Adobe Campaignツリーで、///ノードに **[!UICONTROL Administration]** 移動 **[!UICONTROL Campaign management]** し **[!UICONTROL Typology management]** ま **[!UICONTROL Typology rules]** す。
1. 新しいタイプルール **[!UICONTROL Offer presentation]** を作成します。

   ![](assets/offer_typology_example_001.png)

1. 必要に応じて、ラベルと説明を変更します。

   ![](assets/offer_typology_example_002.png)

1. Choose the **[!UICONTROL All channels]** option to extend the rule to all channels.

   ![](assets/offer_typology_example_003.png)

1. Click the **[!UICONTROL Edit expression]** link and choose the **[!UICONTROL Category]** node as an expression.

   ![](assets/offer_typology_example_004.png)

1. カナダ行き旅行のオファーに該当するカテゴリを選択し、「**[!UICONTROL OK]**」をクリックしてクエリウィンドウを閉じます。

   ![](assets/offer_typology_example_005.png)

1. In the **[!UICONTROL Offer presentation]** tab, choose the same dimensions as those configured in the environment.

   ![](assets/offer_typology_example_006.png)

1. ルールを適用する期間を指定します。

   ![](assets/offer_typology_example_007.png)

1. 提案数を 1 つに制限して、既にカナダ旅行のオファーを拒否した受信者に同様のオファーが送られるのを防ぎます。

   ![](assets/offer_typology_example_008.png)

1. フィルターを選 **[!UICONTROL Offers for the same category]** 択して、カナダのカテゴリからすべてのオファーを **除外します** 。

   ![](assets/offer_typology_example_020.png)

1. Select the **[!UICONTROL Rejected propositions]** filter to take into account only propositions rejected by the recipient.

   ![](assets/offer_typology_example_021.png)

1. ルールを適用する受信者を指定します。

   この例では、受信者として「**Frequent travelers**」（よく旅行する人）を選択します。

   ![](assets/offer_typology_example_009.png)

1. オファーのタイポロジ内で、ルールを参照します。

   ![](assets/offer_typology_example_013.png)

1. Go to the offer environment, (**Environment - Recipient** in this case) and reference the new typology just created using the drop-down list in the **[!UICONTROL Eligibility]** tab.

   ![](assets/offer_typology_example_014.png)

## プレゼンテーションルールの適用 {#applying-the-presentation-rule}

ここでは、先ほど作成したタイポロジルールを適用する手順の例を示します。

これから、カナダのカテゴリに属する最初のオファー提案を送信しようとしています。ただし、このオファーを既に拒否したことがある受信者には再送しません。

1. In the **Frequent travelers** recipient folder, choose one of the profiles to check the offers for which they are eligible: click the **[!UICONTROL Propositions]** tab, then the **[!UICONTROL Preview]** tab.

   この例の場合、**Tim Ramsey** というプロファイルは、「**Americas**」（南北アメリカ）カテゴリに属するオファーの実施要件を満たしています。

   ![](assets/offer_typology_example_015.png)

1. 最初に、**よく旅行する人**&#x200B;をターゲットにしたオファーの E メール配信を作成します。
1. オファーエンジン呼び出しパラメーターを選択します。

   この例では、「**Travel in America**」（アメリカ旅行）カテゴリを選択します。このカテゴリには、サブカテゴリの「**Canada**」（カナダ）および「**United States**」（米国）が含まれています。

   ![](assets/offer_typology_example_016.png)

1. メッセージの本文にオファーを挿入し、配信を送信します。For more on this, refer to [About outbound channels](../../interaction/using/about-outbound-channels.md).

   受信者に、実施要件を満たすオファーが届きます。

1. 提案履歴を見ると、この受信者はカナダのオファーを拒否しています。

   ![](assets/offer_typology_example_018.png)

1. この受信者の現在の実施要件に合ったオファーをチェックします。

   カナダ行きのオファーは選択されなくなりました。

   ![](assets/offer_typology_example_019.png)

**関連トピック**

* [オファーを管理し、チャネル間の冗長性を制御](https://helpx.adobe.com/campaign/kb/simplifying-campaign-management-acc.html#Manageoffersandcontrolredundancyacrosschannels)