---
title: ミッドソーシング転送
seo-title: ミッドソーシング転送
description: ミッドソーシング転送
seo-description: null
page-status-flag: never-activated
uuid: 6b5be5a0-d1ea-428b-a755-74dd34b1d53d
contentOwner: sauviat
products: SG_CAMPAIGN/CLASSIC
audience: workflow
content-type: reference
topic-tags: technical-workflows
discoiquuid: 57b873e9-e934-410b-b966-040cebd94e3e
index: y
internal: n
snippet: y
translation-type: ht
source-git-commit: c10a0a11c6e9952aa47da1f7a15188c79c62508d

---


# ミッドソーシング転送{#transfer-to-mid-sourcing}

以下に説明するワークフローは、デフォルトで&#x200B;**ミッドソーシング転送**&#x200B;モジュールと共にインストールされます。このモジュールについて詳しくは、この[節](../../installation/using/mid-sourcing-deployment.md)を参照してください。

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
   <td> <p>ミッドソーシングサーバー上の配信のカウント情報を収集します。カウント情報には、送信された配信の数など、一般的な配信指標が含まれています。</p> <p>開封数などのトラッキング情報は含まれていません。</p> <p>デフォルトで、10 分おきにトリガーされます。</p> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">ミッドソーシング (配信ログ)</span> <br /> </td> 
   <td> <span class="uicontrol">defaultMidSourcingLog</span> <br /> </td> 
   <td> ミッドソーシングサーバー上の配信ログを収集します。デフォルトで、1 時間おきにトリガーされます。<br /> </td> 
  </tr> 
 </tbody> 
</table>

