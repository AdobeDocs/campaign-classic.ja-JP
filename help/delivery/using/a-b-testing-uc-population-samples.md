---
product: campaign
title: 母集団サンプルの設定
description: 専用のユースケースを通じて A/B テストを実行する方法を学ぶ
badge-v8: label="v8 にも適用されます" type="Positive" tooltip="Campaign v8 にも適用されます"
feature: A/B Testing
role: User
exl-id: 1ca01cab-734a-4299-b112-04eec51222fb
TQID: https://experienceleague.adobe.com/HWbHtS5F-je1GiNdr25dD17W-MpJ-K3xp-T8kKC-c10
product_v2: id: dfc56824-e8b9-499e-85d4-21aedb507314
role_v2: id: b69b2659-1057-424e-8fc5-ed9e016dc554
feature_v2: id: b631758a-142d-425f-b9aa-f756d85cb979id: c858a28b-ea19-49b0-8d48-828717fad89c
subfeature_v2: id: d5bbe3da-ba85-4242-817e-54f7c4b943e0id: e739ee2b-6228-412e-878f-45de0791417d
source-git-commit: 38eab6b8da73163e4476e91c0ef73f25c3f57546
workflow-type: ht
source-wordcount: 206
ht-degree: 100%

---

# AA/B テスト：母集団サンプルを設定 {#step-2--configuring-population-samples}

## クエリアクティビティの設定 {#configuring-the-query-activity}

* 「**[!UICONTROL クエリ]**」アクティビティをダブルクリックします。

  ![](assets/use_case_abtesting_createrecipients_001.png)

* 「**[!UICONTROL クエリを編集]**」リンクをクリックし、ターゲティング対象の受信者を選択します。

  ![](assets/use_case_abtesting_createrecipients_002.png)

* 「**[!UICONTROL クエリ]**」アクティビティを「**[!UICONTROL 分割]**」アクティビティとリンクします。

  ![](assets/use_case_abtesting_createrecipients_003.png)

## 分割アクティビティの設定 {#configuring-the-split-activity}

このアクティビティでは、配信 A を受信する母集団、配信 B を受信する母集団、その他の母集団といったように複数の母集団を作成することができます。 ランダムな抽出を行うことで、各配信の母集団の部分のみをターゲットにすることが可能です。

1. 母集団 A の作成

   * 「**[!UICONTROL 分割]**」アクティビティをダブルクリックします。

     ![](assets/use_case_abtesting_createrecipients_004.png)

   * 既存のタブで、ラベルを母集団 A に変更します。

     ![](assets/use_case_abtesting_createrecipients_005.png)

   * 「**[!UICONTROL 選択レコード数の制限]**」オプションを選択します。

     ![](assets/use_case_abtesting_createrecipients_006.png)

   * 「**[!UICONTROL 編集]**」リンクをクリックし、「**[!UICONTROL ランダムサンプリングを有効化]**」を選択して、「**[!UICONTROL 次へ]**」をクリックします。

     ![](assets/use_case_abtesting_createrecipients_007.png)

   * しきい値を 10% に設定して、「**[!UICONTROL 完了]**」をクリックします。

     ![](assets/use_case_abtesting_createrecipients_008.png)

1. 母集団 B の作成

   * 「**[!UICONTROL 追加]**」をクリックして、母集団 B に使用する新しいタブを作成します。

     ![](assets/use_case_abtesting_createrecipients_009.png)

   * A と同じように、母集団を 10% に制限します。

     ![](assets/use_case_abtesting_createrecipients_010.png)

1. その他の母集団の作成

   * 「**[!UICONTROL 一般]**」タブに移動します。

     ![](assets/use_case_abtesting_createrecipients_011.png)

   * 「**[!UICONTROL 補集合を生成]**」を選択します。

     ![](assets/use_case_abtesting_createrecipients_012.png)

   * ラベルを変更して、この母集団には A も B も含まれないように指定し、「**[!UICONTROL OK]**」をクリックしてアクティビティを閉じます。

     ![](assets/use_case_abtesting_createrecipients_013.png)

これで、2 つの配信テンプレートを作成できるようになりました。 [詳細情報](a-b-testing-uc-delivery-templates.md)）。
