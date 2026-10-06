---
product: campaign
title: 配信の概要
description: 配信の概要ワークフローアクティビティの詳細を説明します
feature: Workflows, Targeting Activity
hide: true
exl-id: b4dee085-ccc4-43fd-850d-1501a99272aa
TQID: 'https://experienceleague.adobe.com/-KNip5bdMEMgGw7dz6Y4SQ4ueu-iPvYDF0D01hvGn94'
product_v2:
  - id: dfc56824-e8b9-499e-85d4-21aedb507314
    internal-label: Campaign
  - id: fd6e6e36-54e4-4f1a-96fc-1a750e400d50
    internal-label: Campaign Classic v7
feature_v2:
  - id: a658c786-869b-4194-a780-2594d663adda
    internal-label: Data management
subfeature_v2:
  - id: ee25c34b-ea50-427b-9369-ba0a160f7d70
    internal-label: HeatMap
  - id: b5f0aaf4-1e48-400d-95ac-6eb3078cf22f
    internal-label: Execution activities
  - id: d1110311-2ca4-442b-be37-088a6db845ee
    internal-label: Data Management activities
  - id: fcb46c0f-76e1-48bc-9dd0-fcf9d97526cf
    internal-label: Workflows
  - id: ff84ab2f-a7c2-4ced-a3c8-5113f4348d99
    internal-label: Targeting Activity
source-git-commit: a43e591a565a18d79f583d975e3e812c5435b0c0
workflow-type: tm+mt
source-wordcount: '273'
ht-degree: 100%
---
# 配信の概要{#delivery-outline}



**配信の概要**&#x200B;では、キャンペーンワークフローに概要を使用できます。 概要は、あらかじめキャンペーン内に作成しておく必要があります。

Adobe Campaign の配信の概要について詳しくは、この[節](../../campaign/using/marketing-campaign-deliveries.md#associating-and-structuring-resources-linked-via-a-delivery-outline)を参照してください。

アクティビティを設定するには、概要と計画された連絡日を任意に選択するだけです。 フィルタリングルールを追加するには、タイポロジまたはタイポロジルールを追加します。

## 例：配信の概要を使用したオファーの挿入 {#example--inserting-an-offer-via-a-delivery-outline}

キャンペーンワークフローで使用可能な&#x200B;**配信の概要**&#x200B;アクティビティでは、現在進行中のキャンペーンの配信の概要で参照されているオファーを提示できます。

>[!NOTE]
>
>**インタラクション**&#x200B;パッケージをインストールする必要があります。

1. ワークフローで、配信アクティビティを追加する前に、配信の概要アクティビティを追加します。
1. 配信の概要アクティビティで、使用する概要を指定します。

   配信の概要の指定について詳しくは、この[節](../../campaign/using/marketing-campaign-deliveries.md#associating-and-structuring-resources-linked-via-a-delivery-outline)を参照してください。

1. 配信に従って、使用可能なフィールドに入力します。
1. 次の 2 つの場合が考えられます。

   * オファーエンジンを呼び出す場合は、「**[!UICONTROL 選択する提案数を制限]**」ボックスをオンにします。 オファースペースを指定し、配信で提示される提案の数を設定します。

     オファーエンジンによって、オファーの重み付けと実施要件ルールが考慮されます。

   * このボックスをオフにすると、オファーエンジンを呼び出すことなく、配信の概要のすべてのオファーが提示されます。

   プレビューでは、配信で指定されたオファーの数が考慮されます。 ワークフローを実行する際に考慮されるのは、配信の概要で指定されたオファーの数です。

   ![](assets/int_compo_offre_wf1.png)
