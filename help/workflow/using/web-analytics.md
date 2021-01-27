---
solution: Campaign Classic
product: campaign
title: Web 分析
description: Web 分析パッケージの詳細を説明します
audience: workflow
content-type: reference
topic-tags: technical-workflows
translation-type: tm+mt
source-git-commit: 972885c3a38bcd3a260574bacbb3f507e11ae05b
workflow-type: tm+mt
source-wordcount: '182'
ht-degree: 100%

---


# Web 分析{#web-analytics}

以下に説明するワークフローは、デフォルトで **Web 分析コネクタ**&#x200B;モジュールと共にインストールされます。このモジュールについて詳しくは、この[節](../../platform/using/adobe-analytics-data-connector.md)を参照してください。

<table> 
 <tbody> 
  <tr> 
   <td> <strong>ラベル</strong><br /> </td> 
   <td> <strong>内部名</strong><br /> </td> 
   <td> <strong>説明</strong><br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">指標とキャンペーン属性の送信</span> <br /> </td> 
   <td> <span class="uicontrol">webAnalyticsSendMetrics</span> <br /> </td> 
   <td> Adobe® Genesis connector 経由で、Adobe Campaign から Adobe Experience Cloud Suite に電子メールキャンペーン指標を送信します。該当する指標は、<strong>送信済み</strong>（iSent）、<strong>オープン数合計</strong>（iTotalRecipientOpen）、<strong>クリックした受信者の合計数</strong>（iTotalRecipientClick）、<strong>エラー</strong>（iError）、<strong>オプトアウト</strong>（opt-out）（iOptOut）です。<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">変換済み連絡先の特定</span> <br /> </td> 
   <td> <span class="uicontrol">webAnalyticsFindConverted</span> <br /> </td> 
   <td> リマーケティングキャンペーンの後で、購入を完了したサイトの訪問者をインデックス化します。このワークフローで収集されたデータは、<span class="uicontrol">リマーケティングの効率レポート</span>でアクセスできます（この<a href="../../platform/using/adobe-analytics-data-connector.md#creating-a-re-marketing-campaign">ページ</a>を参照）。<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">イベントパージ</span> <br /> </td> 
   <td> <span class="uicontrol">webAnalyticsPurgeWebEvents</span> <br /> </td> 
   <td> 「<span class="uicontrol">存続期間</span>」フィールドで設定した期間に基づいてデータベースフィールドからすべてのイベントを削除できます。<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">Web イベントの復元</span> <br /> </td> 
   <td> <span class="uicontrol">webAnalyticsGetWebEvents</span> <br /> </td> 
   <td> 指定したサイトでのインターネットユーザーの行動に関するセグメントを 1 時間に 1 回ダウンロードし、Adobe Campaign データベースに格納してリマーケティングワークフローを開始します。<br /> </td> 
  </tr> 
 </tbody> 
</table>

