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
translation-type: ht
source-git-commit: 215e4d1ca78938b38b53cae0357612deebf7727b

---


# アウトバウンドチャネル{#offers-on-an-outbound-channel}

## E メールのオファー配信 {#email-offer-delivery}

データベースにアフリカ旅行のカテゴリがあり、各オファーの実施要件、コンテキスト、表示域は既に設定されているとします。これから、E メール経由でオファーを提示するためのキャンペーンを作成します。

1. マーケティングキャンペーンとターゲティングワークフローを作成します。

   ![](assets/offer_delivery_example_001.png)

1. E メール配信を編集し、**[!UICONTROL オファー]**&#x200B;アイコンをクリックします。

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

1. 配信に含まれるオファーを確認するために、「**[!UICONTROL プレビュー]**」をクリックします。受信者を選択して、そのユーザーが受け取るオファーのプレビューを表示します。

   ![](assets/offer_delivery_example_009.png)

1. 配信を保存し、ターゲティングワークフローを開始します。
1. 配信を開き、配信の「**[!UICONTROL 監査]**」タブをクリックします。カタログに格納されている様々なオファーの中からオファーエンジンによって選択された提案を確認できます。

   ![](assets/offer_delivery_example_010.png)

## オファーシミュレーションの実行 {#perform-an-offer-simulation}

1. **[!UICONTROL プロファイルとターゲット]**&#x200B;ウィンドウで、「**[!UICONTROL シミュレーション]**」リンクをクリックし、「**[!UICONTROL 作成]**」ボタンをクリックします。

   ![](assets/offer_simulation_001.png)

1. ラベルを選択し、必要に応じて実行設定を指定します。

   ![](assets/offer_simulation_example_002.png)

1. シミュレーションを保存します。新しいタブが表示されます。

   ![](assets/offer_simulation_example_003.png)

1. 「**[!UICONTROL 編集]**」タブをクリックし、「**[!UICONTROL スコープ]**」をクリックします。

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

1. 設定を保存し、「**[!UICONTROL ダッシュボード]**」タブの「**[!UICONTROL 開始]**」をクリックしてシミュレーションを実行します。

   ![](assets/offer_simulation_example_010.png)

1. シミュレーションが完了したら、「**[!UICONTROL 結果]**」タブで、提案の詳しい分類をオファーごとに確認します。

   この例では、オファーエンジンによって 3 件の提案を基にした分類が表示されています。

   ![](assets/offer_simulation_example_011.png)

1. 「**[!UICONTROL オファーの分類（ランク別）]**」を表示し、オファーエンジンによって選択されたオファーのリストを確認します。

   ![](assets/offer_simulation_example_012.png)

1. 必要な場合は、スコープ設定を変更し、「**[!UICONTROL シミュレーションを開始]**」をクリックしてシミュレーションを再実行できます。

   ![](assets/offer_simulation_example_010.png)

1. シミュレーションデータの保存が必要な場合は、レポートの履歴機能または書き出し機能を使用して保存できます。

   ![](assets/offer_simulation_example_013.png)

