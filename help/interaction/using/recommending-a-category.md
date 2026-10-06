---
product: campaign
title: カテゴリのレコメンデーション
description: カテゴリのレコメンデーション
feature: Interaction, Offers
audience: interaction
content-type: reference
topic-tags: managing-an-offer-catalog
exl-id: cb062cb2-dfea-46aa-8d9e-580e4dc7bb25
TQID: 'https://experienceleague.adobe.com/YArBURjF1snwwyf6ZoO5goOPNMSiBTux5Ch53Zgzpfk'
product_v2:
  - id: dfc56824-e8b9-499e-85d4-21aedb507314
    internal-label: Campaign
  - id: fd6e6e36-54e4-4f1a-96fc-1a750e400d50
    internal-label: Campaign Classic v7
feature_v2:
  - id: b6fcaf36-3bc4-4604-94f3-81b5d3f41ecf
    internal-label: Offer Management
  - id: 65702805-0026-5ca1-843a-144fa79f0883
    internal-label: Interaction
  - id: ea08db70-4682-59a2-9408-9aedd9548e07
    internal-label: Offers
source-git-commit: a43e591a565a18d79f583d975e3e812c5435b0c0
workflow-type: tm+mt
source-wordcount: '170'
ht-degree: 100%
---
# カテゴリのレコメンデーション{#recommending-a-category}



場合によっては、受信者は、すべてのオファーを受ける資格があるわけではないと見なされることがあります。 すべての受信者がオファーの提案を受け取れるように、システムで 1 つまたは様々なオファーカテゴリをレコメンデーションに追加できます。 メインオファーとは異なり、それらの「バックアップ」オファーには、資格のある重み付けの大きいオファーがない場合にのみ提示されるように、小さい（ただし 0 ではない）重み付けを設定する必要があります。 また、レコメンデーションに必ず含められるよう、バックアップオファーにはプレゼンテーションルールが何も適用されていない状態にしておく必要があります。 これにより、提案中に重みの大きいオファーがない場合でも、受信者は、このカテゴリのオファーを少なくとも 1 つ受け取ります。

カテゴリが常にレコメンデーションに含められるようにするには、次の手順に従います。

1. エクスプローラーを開き、ツリー構造のオファーカタログをクリックします。
1. 「**[!UICONTROL 実施要件]**」タブをクリックし、「**[!UICONTROL レコメンデーションにこのカテゴリを常に含める]**」チェックボックスをオンにします。
1. 「**[!UICONTROL 保存]**」をクリックして確定し、操作を完了します。

   ![](assets/offer_cat_default_001.png)
