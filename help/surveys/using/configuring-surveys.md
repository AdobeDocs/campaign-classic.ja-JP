---
product: campaign
title: オンライン調査の設定
description: オンライン調査の設定方法を説明します
badge-v8: label="v8 にも適用されます" type="Positive" tooltip="Campaign v8 にも適用されます"
feature: Surveys
exl-id: 387bc362-4064-4181-9385-8e0c3423ba3e
TQID: https://experienceleague.adobe.com/1BTkZ--FyHkp7u0eya-lmuELDu8AMmeC96eGsonYcVM
product_v2:
  - id: dfc56824-e8b9-499e-85d4-21aedb507314
feature_v2:
  - id: a4671286-a59f-47e3-b97b-90627a1977d5
subfeature_v2:
  - id: ed29abcd-b6a8-4d4b-ab8b-b7e746973281
source-git-commit: 38eab6b8da73163e4476e91c0ef73f25c3f57546
workflow-type: tm+mt
source-wordcount: 131
ht-degree: 100%

---

# オンライン調査の設定{#configuring-surveys}



## 調査のプロパティ {#survey-properties}

オンライン調査では、独自の要件を満たすため、自由に設定やカスタマイズをおこなうことができます。 パラメーターは、プロパティウィンドウで入力する必要があります。

使用可能なパラメーターについて詳しくは、[このドキュメント](../../web/using/defining-web-forms-properties.md)を参照してください。

![](assets/s_ncs_admin_survey_properties_general.png)

## 調査のデータストレージ {#survey-data-storage}

デフォルトでは、Web フォームフィールドは、受信者テーブルに格納されます。 別のテーブルを使用するには、「**[!UICONTROL ドキュメントタイプ]**」フィールドで選択します。 **[!UICONTROL ズーム]**&#x200B;アイコンを使用すると、選択したテーブルの内容を表示できます。

フィールドに格納されていない（ただしローカル変数に格納されている）ユーザーによって提供された調査の回答は、「**調査への回答**」テーブルに格納されます。 「**[!UICONTROL ライブラリ]**」フィールドに基づいて、使用するスキーマを変更できます。 このフィールドは、**調査**&#x200B;でのみ使用できます。
