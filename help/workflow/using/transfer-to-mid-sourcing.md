---
product: campaign
title: ミッドソーシング転送
description: ミッドソーシング転送ワークフローの詳細を説明します
hide: true
hidefromtoc: true
feature: Workflows
source-git-commit: 776c664a99721063dce5fa003cf40c81d94f8c78
workflow-type: ht
source-wordcount: '107'
ht-degree: 100%

---


# ミッドソーシング転送{#transfer-to-mid-sourcing}



以下に説明するワークフローは、デフォルトで&#x200B;**ミッドソーシング転送**&#x200B;モジュールと共にインストールされます。このモジュールについて詳しくは、[Campaign Classic v7 インストールガイド](../../installation/using/mid-sourcing-deployment.md)を参照してください。

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
   <td> <p>ミッドソーシングサーバー上の配信のカウント情報を収集します。カウント情報には、送信された配信の数など、一般的な配信達成度が含まれています。</p> <p>開封数などのトラッキング情報は含まれていません。</p> <p>デフォルトで、10 分おきにトリガーされます。</p> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">ミッドソーシング (配信ログ)</span> <br /> </td> 
   <td> <span class="uicontrol">defaultMidSourcingLog</span> <br /> </td> 
   <td> ミッドソーシングサーバー上の配信ログを収集します。デフォルトで、1 時間おきにトリガーされます。<br /> </td> 
  </tr> 
 </tbody> 
</table>

