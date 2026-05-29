---
product: campaign
title: ディメンションを変更
description: ディメンションを変更
feature: Workflows, Targeting Activity
hide: true
exl-id: c3de99f8-089f-4c7c-be11-f375a9463eaa
TQID: https://experienceleague.adobe.com/b9Vd8VOP-JcDHPeEInwq3UaFYrjLv2rWkcgyYOMAsiE
product_v2:
  - id: dfc56824-e8b9-499e-85d4-21aedb507314
feature_v2: []
subfeature_v2:
  - id: ee25c34b-ea50-427b-9369-ba0a160f7d70
  - id: b5f0aaf4-1e48-400d-95ac-6eb3078cf22f
  - id: d1110311-2ca4-442b-be37-088a6db845ee
source-git-commit: 38eab6b8da73163e4476e91c0ef73f25c3f57546
workflow-type: tm+mt
source-wordcount: 398
ht-degree: 96%

---

# ディメンションを変更{#change-dimension}



「ディメンションを変更」アクティビティを使用して、ターゲットの構築サイクル中にターゲティングディメンションを変更できます。 軸の移動は、データテンプレートと入力ディメンションに依存します。 これにより、「契約」ディメンションから「クライアント」ディメンションに切り替えることができます。

さらに、このアクティビティを使用して、新規ターゲットの追加列を定義できます。

データの重複排除条件を定義することもできます。

## 設定モード {#configuration-mode}

「ディメンションの変更」アクティビティを設定するには、次の手順に従います。

1. 新しいターゲティングディメンションを「**[!UICONTROL ディメンションを変更]**」フィールド経由で選択します。

   ![](assets/s_user_change_dimension_param1.png)

1. ディメンションの変更時に、すべての要素を保持することも、出力に含める要素を選択することもできます。 次の例では、maxです。 重複の数は2に設定されます。

   ![](assets/s_user_change_dimension_limit.png)

   レコードを 1 つだけ保持する場合は、1 つのコレクションが作業スキーマに表示されます。このコレクションは、最終結果でターゲットにならないすべてのレコードを表します（1 つのレコードのみが保持されるため）。 ほかのすべてのコレクションと同様に、このコレクションを使用して、集計を自動生成したり、列内の情報を取得したりできます。

   例えば、「**[!UICONTROL 顧客]**」ディメンションを「**[!UICONTROL 受信者]**」ディメンションに変更すると、購入数を追加するだけでなく、特定の店舗の顧客のターゲティングが可能になります。

1. この情報の一部のみを保持するように選択する場合、重複管理モードで設定できます。

   ![](assets/s_user_change_dimension_param2.png)

   青い矢印を使用して、重複処理の優先度を定義できます。

   上の例では、受信者はまずメールアドレスに基づいて重複排除され、次に必要に応じてアカウント番号に基づいて重複排除されます。

1. 「**[!UICONTROL 結果]**」タブで、追加情報を追加できます。

   例えば、**Substring**&#x200B;タイプ関数を使用して、郵便番号に基づいて国を収集できます。 手順は次のとおりです。

   * 「**[!UICONTROL データを追加...]**」リンクをクリックし、「**[!UICONTROL フィルタリングディメンションにリンクされたデータ]**」を選択します。

     ![](assets/wf_change-dimension_sample_01.png)

     >[!NOTE]
     >
     >追加列の作成と管理について詳しくは、[データの追加](query.md#adding-data)を参照してください。

   * 以前のターゲティングディメンション（軸変更の前）を選択し、受信者の「**[!UICONTROL 場所]**」サブツリーで「**[!UICONTROL 郵便番号]**」を選択して「**[!UICONTROL 式を編集]**」をクリックします。

     ![](assets/wf_change-dimension_sample_02.png)

   * 「**[!UICONTROL 詳細選択]**」をクリックし、「**[!UICONTROL 式を使用して数式を編集]**」を選択します。

     ![](assets/wf_change-dimension_sample_03.png)

   * リストで提供される関数を使用して、実行される計算を指定します。

     ![](assets/wf_change-dimension_sample_04.png)

   * 最後に、作成した列のラベルを入力します。

     ![](assets/wf_change-dimension_sample_05.png)

1. ワークフローを実行して、この設定の結果を確認します。 次の図に示すように、ディメンションアクティビティの変更前と変更後のテーブル内のデータを比較し、さらにワークフローテーブルの構造も比較します。

   ![](assets/wf_change-dimension_sample_06.png)

   ![](assets/wf_change-dimension_sample_07.png)
