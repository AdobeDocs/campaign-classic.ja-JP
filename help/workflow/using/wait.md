---
title: 待機
seo-title: 待機
description: 待機
seo-description: null
page-status-flag: never-activated
uuid: 55e4f15d-8d69-45b1-b842-5ccdfdedf550
contentOwner: sauviat
products: SG_CAMPAIGN/CLASSIC
audience: workflow
content-type: reference
topic-tags: flow-control-activities
discoiquuid: 41bcfe67-b5d6-4ee6-9f8a-6a7a208e2036
index: y
internal: n
snippet: y
translation-type: tm+mt
source-git-commit: 579329d9194115065dff2c192deb0376c75e67bd

---


# 待機{#wait}

「**待機**」アクティビティは、数秒から数ヶ月間の任意の遅延時間が経過した後で、トランジションを有効化します。待機は、ほかのタスクの実行をブロックしません。ワークフローは、このタスクが保留になっている間に並行してタスクを実行できます。

下例の図に示すように、エディターを使用してラベルと待機時間を入力できます。

![](assets/edit_wait.png)

このフィ **[!UICONTROL Duration]** ールドでは、選択した単位で値を表すことができます。（事業者の地域設定による）

* 地域の設定を指定しない場合： **秒** 、分、 **m** 、 **h** 、時 **、d、****** 年。 承認時に、値は最も読みやすい単位に自動的に変換されます。

   デフォルトの単位は日付（**d**）です。

* 一方、例えば、地域設定が「フランス語」に設定されている場合は、次のようになります。秒数分時 **** 間h **時** 間 **j** 時間分mn時 ************ 間 承認時に、値は最も読みやすい単位に自動的に変換されます。上の例では、「**90s**」は「**1mn 30s**」のように変換されます。

   デフォルトの単位は日付（**d**）です。

