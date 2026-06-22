---
product: campaign
title: 待機
description: 待機ワークフローアクティビティの詳細を説明します
feature: Workflows
hide: true
exl-id: 4872f756-14d7-4e37-a9cf-b929c77e34ca
TQID: https://experienceleague.adobe.com/sQ3GwMFQnhy6eOmFSfMUwT8Z3UE0p4cHLAjr8CjS2FM
product_v2:
  - id: dfc56824-e8b9-499e-85d4-21aedb507314
feature_v2: []
subfeature_v2:
  - id: ee25c34b-ea50-427b-9369-ba0a160f7d70
  - id: b5f0aaf4-1e48-400d-95ac-6eb3078cf22f
  - id: d1110311-2ca4-442b-be37-088a6db845ee
source-git-commit: c35995a47788db080636c66827a4bd6dc98806cf
workflow-type: tm+mt
source-wordcount: 193
ht-degree: 100%

---

# 待機{#wait}



「**待機**」アクティビティは、数秒から数ヶ月間の任意の遅延時間が経過した後で、トランジションを有効化します。 待機は、ほかのタスクの実行をブロックしません。ワークフローは、このタスクが保留になっている間に並行してタスクを実行できます。

下例の図に示すように、エディターを使用してラベルと待機時間を入力できます。

![](assets/edit_wait.png)

「**[!UICONTROL 期間]**」フィールドの値は、選択した単位（オペレーターの地域設定）で表すことができます。

* 地域設定が指定されていない場合は、**s**（秒）、**m**（分）、**h**（時間）、**d**（日）、**y**（年）になります。 承認時に、値は最も読みやすい単位に自動的に変換されます。

  デフォルトの単位は日（**d**）です。

* 一方、例えば、地域設定が「Français」に設定されている場合は、**s**（秒）、**mn**（分）、**h**（時間）、**j**（日）、**m**（月）、**a**（年）のようになります。 承認時に、値は最も読みやすい単位に自動的に変換されます。上の例では、「**90s**」は「**1mn 30s**」のように変換されます。

  デフォルトの単位は日（**d**）です。

