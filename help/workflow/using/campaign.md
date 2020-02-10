---
title: キャンペーン
seo-title: キャンペーン
description: キャンペーン
seo-description: null
page-status-flag: never-activated
uuid: 9e5cf203-e5e9-4383-b628-aa6f131491e0
contentOwner: sauviat
products: SG_CAMPAIGN/CLASSIC
audience: workflow
content-type: reference
topic-tags: technical-workflows
discoiquuid: de892ec4-c378-4b22-875e-aa9345f82552
index: y
internal: n
snippet: y
translation-type: tm+mt
source-git-commit: 0d687b57f75b432547baef57021b716a8ce37ad4

---


# キャンペーン{#campaign}

以下に説明するワークフローは、デフォルトで **Campaign** モジュールと共にインストールされます。このモジュールについて詳しくは、この[節](../../campaign/using/designing-marketing-campaigns.md)を参照してください。

>[!CAUTION]
>
>キャンペーンプロセスをキャンペーンレベルで実行するには、これらのワークフローを開始する必要があります。

<table> 
 <tbody> 
  <tr> 
   <td> <strong>ラベル</strong><br /> </td> 
   <td> <strong>内部名</strong><br /> </td> 
   <td> <strong>説明</strong><br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">コスト計算</span> <br /> </td> 
   <td> <span class="uicontrol">budgetMgt</span><br /> </td> 
   <td> 予算、プラン、プログラム、キャンペーン、配信およびタスクに関する費用行とコスト行の計算を開始します。<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">在庫 : オーダーおよびアラート</span> <br /> </td> 
   <td> <span class="uicontrol">stockMgt</span><br /> </td> 
   <td> このワークフローは、受注明細に対する在庫計算を開始し、警告アラートのしきい値を管理します。<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">キャンペーンの配信ジョブ</span> <br /> </td> 
   <td> <span class="uicontrol">deliveryMgt</span><br /> </td> 
   <td> 承認された配信をトリガーし、外部配信のサービスプロバイダーの後処理を開始します。また、承認通知とリマインダーも送信します。<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">キャンペーンジョブ</span> <br /> </td> 
   <td> <span class="uicontrol">operationMgt</span><br /> </td> 
   <td> マーケティングキャンペーンに関するジョブ（ターゲティングの開始、ファイル抽出など）を管理します。また、繰り返しキャンペーンと定期的キャンペーンに関連するワークフローも作成します。<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">サービスプロバイダーのジョブ</span> <br /> </td> 
   <td> <span class="uicontrol">supplierMgt</span><br /> </td> 
   <td> This workflow starts processing the provider (email to the router and post-processing) once deliveries have been approved. <br /> </td> 
  </tr> 
 </tbody> 
</table>

