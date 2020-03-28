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
translation-type: ht
source-git-commit: c10a0a11c6e9952aa47da1f7a15188c79c62508d

---


# データの読み込み（RDBMS）{#data-loading-rdbms}

「**[!UICONTROL データの読み込み（RDBMS）]**」アクティビティでは、外部データベースに直接アクセスし、ターゲティングに必要なデータを収集できます。

パフォーマンスを向上させるには、外部データベースのデータを使用できるクエリアクティビティの使用をお勧めします。詳しくは、[外部データベースへのアクセス（FDA）](../../workflow/using/accessing-an-external-database--fda-.md)を参照してください。

手順は以下のようになります。

1. リストからデータソースを選択し、抽出するデータが含まれるテーブル名を入力します。

   ![](assets/s_advuser_wf_sgbd_sample_1.png)

   対応するフィールドに入力したテーブル名は、外部テンプレート内のデータを収集するテンプレートとして使用されます。ワークフローによって処理されるテーブル名は、データの読み取りアクティビティのインバウンドトランジションによって自動生成または伝達されます。使用するテーブルを選択するには、「**[!UICONTROL 詳細..]**.」リンクをクリックし、「**[!UICONTROL トランジションで指定]**」または「**[!UICONTROL 手動で指定]**」オプションを選択します。

   ![](assets/s_advuser_wf_sgbd_sample_5.png)

1. 「**[!UICONTROL 抽出する列を選択...]**」リンクをクリックして、収集するデータをデータベース内で選択します。

   ![](assets/s_advuser_wf_sgbd_sample_2.png)

1. このデータに対してフィルターを定義できます。それには、「**[!UICONTROL クエリを編集...]**」リンクをクリックします。

   このように収集されたデータは、ワークフローのライフサイクルを通じて使用できます。

