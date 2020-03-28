---
title: ライブ／デザイン環境
seo-title: ライブ／デザイン環境
description: ライブ／デザイン環境
seo-description: null
page-status-flag: never-activated
uuid: 38ee2f6a-e446-4ac6-b962-40b648eeaf66
contentOwner: sauviat
products: SG_CAMPAIGN/CLASSIC
audience: interaction
content-type: reference
topic-tags: managing-environments
discoiquuid: 3cea2be4-4da4-4ebd-a241-1bbaa5abb16e
index: y
internal: n
snippet: y
translation-type: ht
source-git-commit: 1c86322fa95aee024f6c691b61a10c21a9a22eb7

---


# ライブ／デザイン環境{#live-design-environments}

## 動作の仕組み {#operating-principle}

インタラクションは、次の 2 つのオファー環境を使用して運用されます。

* **[!UICONTROL デザイン環境]**：編集の対象となる、変更可能なオファーを含んだオファー環境。これらのオファーは、承認サイクルを経ておらず、コンタクト先には配信されません。
* **[!UICONTROL ライブ環境]**：コンタクト先に提示される承認済みのオファーを含んだオファー環境。この環境のオファーは、読み取り専用です。

![](assets/offer_environments_overview_001.png)

各&#x200B;**[!UICONTROL デザイン]**&#x200B;環境は、**[!UICONTROL ライブ]**&#x200B;環境にリンクされています。オファーの作成が完了すると、そのコンテンツと実施要件ルールは、承認サイクルに進みます。承認サイクルを完了したオファーは、**[!UICONTROL ライブ]**&#x200B;環境に自動的にデプロイされ、その瞬間から、配信できるようになります。

デフォルトでは、インタラクションには、1 つの&#x200B;**[!UICONTROL デザイン]**&#x200B;環境とそれにリンクされた 1 つの&#x200B;**[!UICONTROL ライブ]**&#x200B;環境が用意されています。これらの環境は、標準の受信者テーブルをターゲットとするように事前に設定されています。

>[!NOTE]
>
>別のテーブル（匿名オファー用の訪問者テーブルや特定の受信者テーブル）をターゲットにするには、ターゲットマッピングウィザードを使用して環境を作成する必要があります。詳しくは、[オファー環境の作成](#creating-an-offer-environment)を参照してください。

![](assets/offer_environments_overview_002.png)

オファーマネージャーと配信責任者では、アクセスできる環境の表示が異なります。配信責任者は、**[!UICONTROL ライブ]**&#x200B;オファー環境のみを表示し、オファーを使用して配信できます。オファーマネージャーは、**[!UICONTROL デザイン]**&#x200B;環境を表示および変更したり、**[!UICONTROL ライブ]**&#x200B;環境を表示したりできます。詳しくは、[オペレーターのプロファイル](../../interaction/using/operator-profiles.md)を参照してください。

## オファー環境の作成 {#creating-an-offer-environment}

デフォルトでは、インタラクションには、受信者テーブルをターゲットとするように事前設定された環境（識別されたオファー）が 1 つ用意されています。別のテーブル（匿名オファー用の訪問者テーブルや特定の受信者テーブル）をターゲットにするには、次の設定を適用する必要があります。

1. **[!UICONTROL 管理]**／**[!UICONTROL キャンペーン管理]**／**[!UICONTROL 配信マッピング]**&#x200B;ノードにカーソルを置きます。使用する配信マッピング（匿名オファーを使用する場合は「**[!UICONTROL 訪問者]**」）を右クリックし、**[!UICONTROL アクション]**／**[!UICONTROL ターゲティングディメンションのオプションを変更]**&#x200B;を選択します。

   ![](assets/offer_env_anonymous_001.png)

1. 「**[!UICONTROL 次へ]**」をクリックしてウィザードの次の画面に進み、「**[!UICONTROL 提案のストレージスキーマを生成]**」ボックスをオンにして、「**[!UICONTROL 保存]**」をクリックします。

   ![](assets/offer_env_anonymous_002.png)

   >[!NOTE]
   >
   >このボックスが既にオンになっている場合は、一度オフにしてからもう一度オンにしてください。

1. 先ほど有効にしたターゲットマッピングからターゲティング情報が取得され、2 つの環境（**[!UICONTROL デザイン]**&#x200B;および&#x200B;**[!UICONTROL ライブ]**）が作成されます。この環境には、ターゲティング情報があらかじめ設定されています。

   **[!UICONTROL 訪問者]**&#x200B;マッピングを有効にした場合、環境の「**[!UICONTROL 一般]**」タブにある「**[!UICONTROL 受信する匿名インタラクション専用の環境]**」ボックスが自動的にオンになります。

   このオプションを設定すると、（特に環境のオファースペースを設定する際の）匿名インタラクションに特有の機能を有効にできます。また、「識別された」環境を「匿名」環境に切り替えることができるオプションを設定することもできます。

   例えば、受信者環境のオファースペース（識別されたコンタクト先）と訪問者環境に合ったオファースペース（識別されていないコンタクト先）をリンクすると、受信者が識別されている場合とそうでない場合とで異なるオファーを提供できます。詳しくは、[オファースペースの作成](../../interaction/using/creating-offer-spaces.md)を参照してください。

   ![](assets/offer_env_anonymous_003.png)

>[!NOTE]
>
>インバウンドチャネルでの匿名インタラクションについて詳しくは、[匿名インタラクション](../../interaction/using/anonymous-interactions.md)を参照してください。

