---
title: データの読み込み（RDBMS）
seo-title: データの読み込み（RDBMS）
description: データの読み込み（RDBMS）
seo-description: null
page-status-flag: never-activated
uuid: d5ec30f2-398a-4b16-9232-924437da146a
contentOwner: sauviat
products: SG_CAMPAIGN/CLASSIC
audience: workflow
content-type: reference
topic-tags: action-activities
discoiquuid: a128caac-5740-4dac-b14d-1d2fcef3cc69
index: y
internal: n
snippet: y
translation-type: tm+mt
source-git-commit: c10a0a11c6e9952aa47da1f7a15188c79c62508d

---


# データの読み込み（RDBMS）{#data-loading-rdbms}

The **[!UICONTROL Data loading (RDBMS)]** activity lets you access this external database directly and to collect only the data required for targeting.

パフォーマンスを向上させるには、外部データベースのデータを使用できるクエリアクティビティの使用をお勧めします。For more on this, refer to [Accessing an external database (FDA)](../../workflow/using/accessing-an-external-database--fda-.md).

手順は以下のようになります。

1. リストからデータソースを選択し、抽出するデータが含まれるテーブル名を入力します。

   ![](assets/s_advuser_wf_sgbd_sample_1.png)

   対応するフィールドに入力したテーブル名は、外部テンプレート内のデータを収集するテンプレートとして使用されます。ワークフローによって処理されるテーブル名は、データの読み取りアクティビティのインバウンドトランジションによって自動生成または伝達されます。使用するテーブルを選択するには、をクリックしま **[!UICONTROL Advanced..]**&#x200B;す。 」リンクをクリックし、またはオプ **[!UICONTROL Specified in the transition]** ションを選 **[!UICONTROL Explicit]** 択します。

   ![](assets/s_advuser_wf_sgbd_sample_5.png)

1. リンクをク **[!UICONTROL Select the columns to extract...]** リックして、データベースで収集するデータを選択します。

   ![](assets/s_advuser_wf_sgbd_sample_2.png)

1. このデータに対してフィルターを定義できます。これを行うには、リンクをクリック **[!UICONTROL Edit query....]** します。

   このように収集されたデータは、ワークフローのライフサイクルを通じて使用できます。

