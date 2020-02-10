---
title: インタラクション
seo-title: インタラクション
description: インタラクション
seo-description: null
page-status-flag: never-activated
uuid: 5c8e2353-bb76-4e8d-95d7-61b6c111b6b3
contentOwner: sauviat
products: SG_CAMPAIGN/CLASSIC
audience: workflow
content-type: reference
topic-tags: technical-workflows
discoiquuid: 1683477a-9233-4a25-b0d0-0c81051eb440
index: y
internal: n
snippet: y
translation-type: tm+mt
source-git-commit: 28a32c9a5300c28784ae7a2837075b4dc3aad1fa

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
   <td> <strong>オファーの提案</strong>キューブのために<strong>完全</strong>な集計を更新します。デフォルトで、毎日午前 6 時にトリガーされます。この集計は、次の次元を取得します。チャネル、配信、マーケティングオファーおよび日付を参照してください。<br /><strong>オファーの提案</strong>キューブは、オファーに基づいてレポートを生成するために使用します。キューブについて詳しくは、<a href="../../reporting/using/about-cubes.md">この節</a>を参照してください。<br /> </td> 
  </tr> 
   <tr> 
   <td> <span class="uicontrol">MessageCenterの完全集計計算</span><br /> </td> 
   <td> <span class="uicontrol">agg_messageCenter_full</span><br /> </td> 
   <td> <br /> </td> 
  </tr> 
 </tbody> 
</table>

