---
solution: Campaign Classic
product: campaign
title: インタラクション
description: インタラクション
audience: workflow
content-type: reference
topic-tags: technical-workflows
translation-type: tm+mt
source-git-commit: affc541c480ad7e618120fe90270841add06b711
workflow-type: tm+mt
source-wordcount: '153'
ht-degree: 76%

---


# インタラクション{#interaction}

以下に説明するワークフローは、デフォルトで&#x200B;**オファーエンジン (インタラクション)** モジュールと共にインストールされます。このモジュールについて詳しくは、この[節](../../interaction/using/interaction-and-offer-management.md)を参照してください。

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
   <td> <strong>オファーの提案</strong>キューブのために<strong>完全</strong>な集計を更新します。デフォルトで、毎日午前 6 時にトリガーされます。この集計が取得するディメンションは、チャネル、配信、マーケティングオファーおよび日付です。<br /><strong>オファーの提案</strong>キューブは、オファーに基づいてレポートを生成するために使用します。キューブについて詳しくは、<a href="../../reporting/using/about-cubes.md">この節</a>を参照してください。<br /> </td> 
  </tr> 
   <tr> 
   <td> <span class="uicontrol">MessageCenter における完全な集計の計算</span> <br /> </td> 
   <td> <span class="uicontrol">agg_messageCenter_full</span> <br /> </td> 
   <td> This workflow updates the <strong>Full</strong> aggregate for the <strong>Message center</strong> cube. デフォルトで、毎日午前 3 時にトリガーされます。この集計は、次のディメンションを取り込みます。チャネル、日付、ステータス、イベントタイプ。<br /> 次に、 <strong>Message Center</strong> キューブを使用して、イベントに基づくレポートを生成します。 キューブについて詳しくは、<a href="../../reporting/using/about-cubes.md">この節</a>を参照してください。<br /> </td> 
   <td> <br /> </td> 
  </tr> 
 </tbody> 
</table>

