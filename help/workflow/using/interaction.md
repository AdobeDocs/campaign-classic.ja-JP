---
product: campaign
title: インタラクション
description: インタラクション
hide: true
feature: Workflows, Interaction, Offers
product_v2:
  - id: dfc56824-e8b9-499e-85d4-21aedb507314
    internal-label: Campaign
  - id: fd6e6e36-54e4-4f1a-96fc-1a750e400d50
    internal-label: Campaign Classic v7
feature_v2:
  - id: 65702805-0026-5ca1-843a-144fa79f0883
    internal-label: Interaction
  - id: ea08db70-4682-59a2-9408-9aedd9548e07
    internal-label: Offers
  - id: a658c786-869b-4194-a780-2594d663adda
    internal-label: Data management
subfeature_v2:
  - id: fcb46c0f-76e1-48bc-9dd0-fcf9d97526cf
    internal-label: Workflows
source-git-commit: a43e591a565a18d79f583d975e3e812c5435b0c0
workflow-type: tm+mt
source-wordcount: '169'
ht-degree: 100%
---

# インタラクション{#interaction}



以下に説明するワークフローは、デフォルトで&#x200B;**オファーエンジン (インタラクション)**&#x200B;アドオンと共にインストールされます。

詳しくは、Campaign のバージョンに応じて、次の節を参照してください。

![](assets/do-not-localize/v7.jpeg)[Campaign v7 ドキュメント](../../interaction/using/interaction-and-offer-management.md)

![](assets/do-not-localize/v8.png)[Campaign v8 ドキュメント](https://experienceleague.adobe.com/docs/campaign/campaign-v8/send/interaction/interaction.html?lang=ja)


<table> 
 <tbody> 
  <tr> 
   <td> <strong>ラベル</strong><br /> </td> 
   <td> <strong>内部名</strong><br /> </td> 
   <td> <strong>説明</strong><br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">完全な集計 (propositionrcp キューブ)</span> <br /> </td> 
   <td> <span class="uicontrol">agg_nmspropositionrcp_full</span> <br /> </td> 
   <td> <strong>オファーの提案</strong>キューブのために<strong>完全</strong>な集計を更新します。 デフォルトで、毎日午前 6 時にトリガーされます。 この集計では、チャネル、配信、マーケティングオファーおよび日付の各ディメンションをキャプチャします。<br /> 次に、<strong>オファーの提案</strong>キューブが使用され、オファーに基づいたレポートを生成します。 キューブについて詳しくは、<a href="../../reporting/using/ac-cubes.md">この節</a>を参照してください。<br /> </td> 
  </tr> 
   <tr> 
   <td> <span class="uicontrol">MessageCenter における完全な集計の計算</span> <br /> </td> 
   <td> <span class="uicontrol">agg_messageCenter_full</span> <br /> </td> 
   <td> このワークフローは、<strong>メッセージセンター</strong>キューブのための<strong>完全な</strong>集計を更新します。 デフォルトで、毎日午前 3 時にトリガーされます。 この集計では、チャネル、日付、ステータス、イベントタイプの各ディメンションをキャプチャします。<br /> 次に、<strong>メッセージセンター</strong>キューブが、イベントに基づいてレポートを生成するために使用されます。 キューブについて詳しくは、<a href="../../reporting/using/ac-cubes.md">この節</a>を参照してください。<br /> </td> 
   <td> <br /> </td> 
  </tr> 
 </tbody> 
</table>

