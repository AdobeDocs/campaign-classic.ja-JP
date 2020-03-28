---
title: オファーの作成
seo-title: オファーの作成
description: オファーの作成
seo-description: null
page-status-flag: never-activated
uuid: 9e8b0351-e2a5-4043-be86-e275d2f849ea
contentOwner: sauviat
products: SG_CAMPAIGN/CLASSIC
audience: interaction
content-type: reference
topic-tags: managing-an-offer-catalog
discoiquuid: 010c88f4-9444-448f-bb7b-7191517d2e23
index: y
internal: n
snippet: y
translation-type: ht
source-git-commit: 215e4d1ca78938b38b53cae0357612deebf7727b

---


# オファーの作成{#creating-an-offer}

## オファーの作成 {#creating-the-offer}

オファーを作成するには、次の手順に従います。

1. **[!UICONTROL キャンペーン]**&#x200B;ウィンドウに移動し、「**[!UICONTROL オファー]**」リンクをクリックします。

   ![](assets/offer_create_001.png)

1. 「**[!UICONTROL 作成]**」ボタンをクリックします。

   ![](assets/offer_create_005.png)

1. ラベルを変更し、オファーが属するカテゴリを選択します。

   ![](assets/offer_create_002.png)

1. 「**[!UICONTROL 保存]**」をクリックして、オファーを作成します。

   ![](assets/offer_create_003.png)

   オファーが、プラットフォームで利用できるようになり、コンテンツを設定できるようになります。

   ![](assets/offer_create_004.png)

## オファーの実施要件の設定 {#configuring-offer-eligibility}

「**[!UICONTROL 実施要件]**」タブで、そのオファーが有効で提示可能である期間、ターゲットに適用するフィルター、オファーの重み付けを定義します。

### 実施期間の定義 {#defining-the-eligibility-period-of-an-offer}

オファーの実施期間を定義するには、ドロップダウンリストを使用して、開始日と終了日をカレンダーから選択します。

![](assets/offer_eligibility_create_002.png)

オファーがインタラクションエンジンによって選択される期間は、この範囲に含まれる日のみです。また、オファーカテゴリの実施日も設定されている場合は、最も厳しい制限期間が適用されます。

### ターゲットに対するフィルター {#filters-on-the-target}

オファーターゲットにはフィルターを適用できます。

フィルターを適用するには、「**[!UICONTROL クエリを編集]**」リンクをクリックし、適用するフィルターを選択します（[この節](../../platform/using/steps-to-create-a-query.md#step-4---filter-data)を参照）。

![](assets/offer_eligibility_create_003.png)

定義済みフィルターが既にある場合は、ユーザーフィルターのリストから選択できます。詳しくは、[定義済みフィルターの作成](../../interaction/using/creating-predefined-filters.md)を参照してください。

![](assets/offer_eligibility_create_004.png)

### オファーの重み付け {#offer-weight}

ターゲットが複数のオファーの実施要件を満たす場合のために、エンジンにどのオファーを選択させるかの条件を設定するには、オファーに重み付けを 1 つまたは複数割り当てます。また、必要に応じてターゲットにフィルターを適用したり、重み付けを適用するオファースペースを制限したりすることもできます。エンジンは、重み付けの小さいオファーよりも大きいオファーを優先して選択します。

例えば、期間、特定のターゲット、さらにはオファースペースを区別するために、同じオファーに複数の重み付けを設定できます。

例えば、コンタクト先の年齢が 18 歳から 25 歳までの場合は重み付け A を適用し、25 歳を超える場合は重み付け B を適用できます。または、夏の間ずっと有効なオファーについて、7 月には重み付け A を適用し、8 月には重み付け B を適用できます。

>[!NOTE]
>
>オファーに割り当てた重み付けの値を、そのオファーが属するカテゴリのパラメーターに従って一時的に修正させることもできます。詳しくは、[オファーカテゴリの作成](../../interaction/using/creating-offer-categories.md)を参照してください。

オファーの重み付けを作成するには、次の手順に従います。

1. 「**[!UICONTROL 追加]**」をクリックします。

   ![](assets/offer_weight_create_001.png)

1. ラベルを変更し、重み付けを割り当てます。デフォルトの重み付けは 1 です。

   ![](assets/offer_weight_create_006.png)

   >[!CAUTION]
   >
   >値を入力しない場合、重み付けは 0 になり、ターゲットがそのオファーの実施要件を満たすとは判断されなくなります。

1. 特定の期間を対象にして重み付けを適用するには、実施日を定義します。

   ![](assets/offer_weight_create_002.png)

1. 必要に応じて、重み付けを特定のオファースペースに制限します。

   ![](assets/offer_weight_create_003.png)

1. ターゲットにフィルターを適用します。

   ![](assets/offer_weight_create_004.png)

1. 「**[!UICONTROL OK]**」をクリックして重み付けを保存します。

   ![](assets/offer_weight_create_005.png)

   >[!NOTE]
   >
   >選択されたオファーに関して、複数の重み付けの実施要件を満たすターゲットには、それらのうち最大の重み付けが適用されます。オファーエンジンの呼び出し時、1 つのオファーが選択される回数は、1 つのコンタクト先あたり最大 1 回です。

### オファー実施要件ルールの概要 {#a-summary-of-offer-eligibility-rules}

設定が完了すると、実施要件ルールの概要をオファーダッシュボードで利用できるようになります。

概要を表示するには、「**[!UICONTROL スケジュールおよび実施要件ルール]**」リンクをクリックします。

![](assets/offer_eligibility_create_005.png)

## オファーコンテンツの作成 {#creating-the-offer-content}

1. 「**[!UICONTROL 編集]**」タブをクリックし、「**[!UICONTROL コンテンツ]**」タブをクリックします。

   ![](assets/offer_content_create_001.png)

1. オファーコンテンツの各種フィールドに値を入力します。

   * **[!UICONTROL タイトル]**：オファーに表示させるタイトルを指定します。警告：これは、「**[!UICONTROL 一般]**」タブで定義されるオファーのラベルとは異なります。
   * **[!UICONTROL 宛先 URL]**：オファーの URL を指定します。正しく処理されるようにするには、「http://」または「https://」で始める必要があります。
   * **[!UICONTROL 画像 URL]**：オファーの画像を示す URL またはアクセスパスを指定します。
   * **[!UICONTROL HTML コンテンツ]**／**[!UICONTROL テキストコンテンツ]**：オファーの本文を、目的のタブに入力します。トラッキングを生成するには、**[!UICONTROL HTML コンテンツ]**&#x200B;が、`<div>` タイプの要素に含めることができる HTML 要素で構成されている必要があります。例えば、HTML ページ内の `<table>` 要素の結果は次のようになります。

   ```
      <div> 
       <table>
        <tr>
         <th>Month</th>
         <th>Savings</th>   
        </tr>   
        <tr>    
         <td>January</td>
         <td>$100</td>   
        </tr> 
       </table> 
      </div>
   ```

   承認 URL の定義について詳しくは、[提案承認時のステータス設定](../../interaction/using/creating-offer-spaces.md#configuring-the-status-when-the-proposition-is-accepted)の節で説明しています。

   ![](assets/offer_content_create_002.png)

   オファースペースの設定時に定義された必須フィールドを確認するには、「**[!UICONTROL コンテンツ定義]**」リンクをクリックします。詳しくは、[オファースペースの作成](../../interaction/using/creating-offer-spaces.md)を参照してください。

   ![](assets/offer_content_create_003.png)

   この例では、オファーには、タイトル、画像、HTML コンテンツ、宛先 URL を含める必要があります。

## オファーのプレビュー {#previewing-the-offer}

コンテンツの設定が完了すると、そのオファーが受信者にどのように表示されるかをプレビューできるようになります。手順は次のとおりです。

1. 「**[!UICONTROL プレビュー]**」タブをクリックします。

   ![](assets/offer_preview_create_001.png)

1. 表示したいオファーの表示域を選択します。

   ![](assets/offer_preview_create_002.png)

1. オファーコンテンツがパーソナライズされている場合、パーソナライゼーションを表示するオファーターゲットを選択します。

   ![](assets/offer_preview_create_003.png)

## オファーの仮説の作成 {#creating-a-hypothesis-on-an-offer}

オファーの提案に関する仮説を作成すると、該当製品の購入に対するオファーの影響を判別できます。

>[!NOTE]
>
>仮説は Response Manager を使用して実行されます。使用許諾契約書を確認してください。

オファーの提案に対して実行された仮説は、「**[!UICONTROL 測定]**」タブで参照できます。

仮説の作成について詳しくは、[このページ](../../campaign/using/about-response-manager.md)を参照してください。

![](assets/offer_hypothesis_001.png)

