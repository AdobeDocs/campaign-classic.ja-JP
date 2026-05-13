---
product: campaign
title: データの読み込み（RDBMS）
description: データ読み込み（RDBMS）ワークフローアクティビティの詳細を説明します
feature: Workflows, Data Management Activity
hide: true
exl-id: 6e24d5fe-4830-49b4-a0fe-624c5644c920
TQID: https://experienceleague.adobe.com/w7MFQZpUw-a0SIp634sptKz2VKm2MTZisjmN3VLDt2g
product_v2:
  - id: dfc56824-e8b9-499e-85d4-21aedb507314
feature_v2:
  - id: a658c786-869b-4194-a780-2594d663adda
topic_v2:
  - id: ebde5b41-29c9-4f5e-9ef6-1197e85409e3
source-git-commit: 4c295c0dabae8aba298390a3da2422a3fa1219f9
workflow-type: tm+mt
source-wordcount: 203
ht-degree: 85%

---

# データの読み込み（RDBMS）{#data-loading-rdbms}



「**[!UICONTROL データの読み込み（RDBMS）]**」アクティビティでは、外部データベースに直接アクセスし、ターゲティングに必要なデータを収集できます。

パフォーマンスを向上させるには、外部データベースのデータを使用できるクエリアクティビティの使用をお勧めします。 詳しくは、[外部データベースへのアクセス（FDA）](accessing-an-external-database-fda.md)を参照してください。

手順は以下のようになります。

1. リストからデータソースを選択し、抽出するデータが含まれるテーブル名を入力します。

   ![](assets/s_advuser_wf_sgbd_sample_1.png)

   対応するフィールドに入力したテーブル名は、外部テンプレート内のデータを収集するテンプレートとして使用されます。 ワークフローによって処理されるテーブル名は、データの読み取りアクティビティのインバウンドトランジションによって自動生成または伝達されます。 使用するテーブルを選択するには、**[!UICONTROL 詳細…]**. リンクをクリックし、**[!UICONTROL 移行]**&#x200B;または&#x200B;**[!UICONTROL 明示的]** オプションで「指定」を選択します。

   ![](assets/s_advuser_wf_sgbd_sample_5.png)

1. 「**[!UICONTROL 抽出する列を選択...]**」リンクをクリックして、収集するデータをデータベース内で選択します。

   ![](assets/s_advuser_wf_sgbd_sample_2.png)

1. このデータに対してフィルターを定義できます。 これを行うには、**[!UICONTROL クエリを編集…]** リンクをクリックします。

   このように収集されたデータは、ワークフローのライフサイクルを通じて使用できます。
