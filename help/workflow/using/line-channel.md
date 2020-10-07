---
title: LINE チャネル
seo-title: LINE チャネル
description: LINE チャネル
seo-description: null
page-status-flag: never-activated
uuid: 0b0e34b2-7ee9-456a-9ed9-7ede889584b6
contentOwner: sauviat
products: SG_CAMPAIGN/CLASSIC
audience: workflow
content-type: reference
topic-tags: technical-workflows
discoiquuid: 367314a2-eb6d-4710-8a47-5a51049ad924
translation-type: tm+mt
source-git-commit: 70b143445b2e77128b9404e35d96b39694d55335
workflow-type: tm+mt
source-wordcount: '97'
ht-degree: 100%

---


# LINE チャネル{#line-channel}

以下に説明するワークフローは、デフォルトで&#x200B;**LINE Channel** モジュールと共にインストールされます。このモジュールについて詳しくは、この[節](../../delivery/using/line-channel.md)を参照してください。

<table> 
 <tbody> 
  <tr> 
   <td> <strong>ラベル</strong><br /> </td> 
   <td> <strong>内部名</strong><br /> </td> 
   <td> <strong>説明</strong><br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">LINE V2 アクセストークンの更新</span> <br /> </td> 
   <td> <span class="uicontrol">updateLineV2AccessToken</span> <br /> </td> 
   <td> このワークフローは、アクセストークンを LINE V2 に更新します。<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">ブロックした LINE ユーザーを削除</span> <br /> </td> 
   <td> <span class="uicontrol">deleteBlockedLineUsersV2</span> <br /> </td> 
   <td> このワークフローは、LINE 公式アカウントにブロックされてから 180 日が経過した後に LINE V2 ユーザーのデータを削除するようにします。<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">MID から LINE ユーザー ID への移行</span> <br /> </td> 
   <td> <span class="uicontrol">MIDToUserIDMigration</span> <br /> </td> 
   <td> このワークフローは、LINE V1 から LINE V2 へ移行用に、LINE V2 ユーザーの ID を生成します。<br /> </td> 
  </tr> 
 </tbody> 
</table>

