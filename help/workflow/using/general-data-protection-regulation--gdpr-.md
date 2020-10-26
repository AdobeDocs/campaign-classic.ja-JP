---
title: 一般データ保護規則（GDPR）
seo-title: 一般データ保護規則（GDPR）
description: 一般データ保護規則（GDPR）
seo-description: null
page-status-flag: never-activated
uuid: cb5f5d79-52ac-4ce4-abc7-a3a1f0a001cf
contentOwner: sauviat
products: SG_CAMPAIGN/CLASSIC
audience: workflow
content-type: reference
topic-tags: technical-workflows
discoiquuid: 050c804e-87b7-4d68-b787-c396fec329d2
translation-type: ht
source-git-commit: 70b143445b2e77128b9404e35d96b39694d55335
workflow-type: ht
source-wordcount: '108'
ht-degree: 100%

---


# プライバシーデータ保護規則{#general-data-protection-regulation-gdpr}

以下に説明するワークフローは、デフォルトで&#x200B;**プライバシーデータ保護規則**&#x200B;モジュールと共にインストールされます。このモジュールについて詳しくは、この[記事](https://helpx.adobe.com/jp/campaign/kb/acc-privacy.html)を参照してください。

<table> 
 <tbody> 
  <tr> 
   <td> <strong>ラベル</strong><br /> </td> 
   <td> <strong>内部名</strong><br /> </td> 
   <td> <strong>説明</strong><br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">プライバシーリクエストを収集</span> <br /> </td> 
   <td> <span class="uicontrol">collectPrivacyRequests</span> <br /> </td> 
   <td> このワークフローでは、Adobe Campaign に保存されている受信者のデータを生成し、プライバシーリクエストの画面でダウンロードできるようにします。<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">プライバシーリクエストデータを削除</span> <br /> </td> 
   <td> <span class="uicontrol">deletePrivacyRequestsData</span> <br /> </td> 
   <td> このワークフローでは、Adobe Campaign に保存されている受信者のデータを削除します。<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">プライバシーリクエストのクリーンアップ</span> <br /> </td> 
   <td> <span class="uicontrol">cleanupPrivacyRequests</span> <br /> </td> 
   <td> このワークフローでは、90 日より古いアクセス要求ファイルが消去されます。<br /> </td> 
  </tr> 
 </tbody> 
</table>

