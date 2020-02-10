---
title: 配信テンプレートの作成
seo-title: 配信テンプレートの作成
description: 配信テンプレートの作成
seo-description: null
page-status-flag: never-activated
uuid: 8ceae1ec-9e02-4809-aa8b-1e6bd7790950
contentOwner: sauviat
products: SG_CAMPAIGN/CLASSIC
audience: delivery
content-type: reference
topic-tags: using-delivery-templates
discoiquuid: 0e67d9dd-3ee8-4c06-98a4-3a2c644b6c0a
index: y
internal: n
snippet: y
translation-type: tm+mt
source-git-commit: 7dbc876fae0bde78e3088ee1ab986cd09e9bcc38

---


# 配信テンプレートの作成{#creating-a-delivery-template}

## テンプレートへの既存の配信の変換 {#converting-an-existing-delivery-to-a-template}

配信をテンプレートに変換すると、新しい繰り返し配信アクションの作成に使用できます。To convert a delivery to a template, select it from the delivery list, accessible via the **[!UICONTROL Campaign management]** node of the tree.

Right-click and select **[!UICONTROL Actions > Save as template...]**.

![](assets/s_ncs_user_campaign_save_as_scenario.png)

これにより、選択した配信から配信テンプレートが作成されます。You must enter the folder where it is saved (in the **[!UICONTROL Folder]** field) as well as the folder where the deliveries created based on this template are created (in the **[!UICONTROL Execution folder]** field).

![](assets/s_ncs_user_campaign_save_as_scenario_a.png)

設定モードについて詳しくは、「テンプレートの配信へ [のリンク」を参照してください](../../delivery/using/creating-a-delivery-from-a-template.md#linking-the-template-to-a-delivery)。

## 新しいテンプレートの作成 {#creating-a-new-template}

配信テンプレートを設定するには、次の手順に従います。

1. Campaign エクスプローラーを開きます。
1. **リソース**&#x200B;フォルダーで、「**テンプレート**」、「**配信テンプレート**」の順に選択します。

   ![](assets/delivery_template_1.png)

1. ツールバーで「**新規**」をクリックして、新しい配信テンプレートを作成します。

   ![](assets/delivery_template_2.png)

1. フォルダーの&#x200B;**ラベル**&#x200B;と&#x200B;**内部名**&#x200B;を修正します。
1. テンプレートを保存してから再度開きます。
1. 「**プロパティ**」ボタンをクリックしてから、必要に応じて値を修正します。

   ![](assets/delivery_template_3.png)

1. 「**一般**」タブで、**実行フォルダー**、**フォルダー**、**ルーティング**&#x200B;の各ドロップダウンメニューで選択された場所を確定または変更します。

   ![](assets/delivery_template_4.png)

1. 「**E メールパラメーター**」カテゴリに E メールの件名とターゲット母集団を入力します。
1. **HTML コンテンツ**&#x200B;を追加してテンプレートをパーソナライズします。ミラーページのリンクと購読解除リンクを追加することもできます。
1. 「**プレビュー**」タブを選択します。**パーソナライゼーションをテスト**&#x200B;ドロップダウンメニューで&#x200B;**受信者**&#x200B;を選択し、選択したプロファイルとしてテンプレートをプレビューします。

   ![](assets/delivery_template_5.png)

1. 「**保存**」をクリックします。これで、テンプレートを配信で使用できるようになります。

>[!NOTE]
>
>設定エラーを防ぐために、新しいテンプレートを作成するのではなく、ネイティブテンプレートをコピーしてプロパティを変更することをお勧めします。
