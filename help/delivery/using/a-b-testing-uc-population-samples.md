---
solution: Campaign Classic
product: campaign
title: 母集団サンプルの設定
description: 専用の使用例を通してA/Bテストを実行する方法を学びます。
audience: delivery
content-type: reference
topic-tags: a-b-testing
translation-type: ht
source-git-commit: 50a10e16f320a67cb4ad0e31c1cbe8a9365b7887
workflow-type: ht
source-wordcount: '195'
ht-degree: 100%

---


# 母集団サンプルの設定 {#step-2--configuring-population-samples}

## 「クエリ」アクティビティの設定{#configuring-the-query-activity}

* 「**[!UICONTROL クエリ]**」アクティビティをダブルクリックします。

   ![](assets/use_case_abtesting_createrecipients_001.png)

* 「**[!UICONTROL クエリを編集]**」リンクをクリックし、ターゲティング対象の受信者を選択します。

   ![](assets/use_case_abtesting_createrecipients_002.png)

* 「**[!UICONTROL クエリ]**」アクティビティを「**[!UICONTROL 分割]**」アクティビティとリンクします。

   ![](assets/use_case_abtesting_createrecipients_003.png)

## 分割アクティビティの設定 {#configuring-the-split-activity}

このアクティビティでは、配信 A を受信する母集団、配信 B を受信する母集団、その他の母集団といったように複数の母集団を作成することができます。ランダムな抽出をおこなうことで、各配信の母集団の部分のみをターゲティングすることが可能です。

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

これで2つの配信テンプレートを作成できます([手順3:2つの配信テンプレート](../../delivery/using/a-b-testing-uc-delivery-templates.md)を作成します)。
