---
product: campaign
title: ミッドソーシング転送
description: ミッドソーシング転送ワークフローの詳細を説明します
hide: true
feature: Workflows
product_v2:
  - id: dfc56824-e8b9-499e-85d4-21aedb507314
    internal-label: Campaign
  - id: fd6e6e36-54e4-4f1a-96fc-1a750e400d50
    internal-label: Campaign Classic v7
feature_v2:
  - id: a658c786-869b-4194-a780-2594d663adda
    internal-label: Data management
subfeature_v2:
  - id: fcb46c0f-76e1-48bc-9dd0-fcf9d97526cf
    internal-label: Workflows
source-git-commit: a43e591a565a18d79f583d975e3e812c5435b0c0
workflow-type: tm+mt
source-wordcount: '115'
ht-degree: 100%
---

# ミッドソーシング転送{#transfer-to-mid-sourcing}



以下に説明するワークフローは、デフォルトで&#x200B;**ミッドソーシング転送**&#x200B;モジュールと共にインストールされます。 このモジュールについて詳しくは、[Campaign Classic v7 インストールガイド](../../installation/using/mid-sourcing-deployment.md)を参照してください。

<table> 
 <tbody> 
  <tr> 
   <td> <strong>ラベル</strong><br /> </td> 
   <td> <strong>内部名</strong><br /> </td> 
   <td> <strong>説明</strong><br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">ミッドソーシング (配信カウンター)</span> <br /> </td> 
   <td> <span class="uicontrol">defaultMidSourcingDlv</span> <br /> </td> 
   <td> <p>ミッドソーシングサーバー上の配信のカウント情報を収集します。 カウント情報には、送信された配信の数など、一般的な配信達成度が含まれています。</p> <p>開封数などのトラッキング情報は含まれていません。</p> <p>デフォルトで、10 分おきにトリガーされます。</p> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">ミッドソーシング (配信ログ)</span> <br /> </td> 
   <td> <span class="uicontrol">defaultMidSourcingLog</span> <br /> </td> 
   <td> ミッドソーシングサーバー上の配信ログを収集します。 デフォルトで、1 時間おきにトリガーされます。<br /> </td> 
  </tr> 
 </tbody> 
</table>

