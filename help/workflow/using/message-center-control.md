---
product: campaign
title: Message Center（コントロール）
description: Message Center（コントロール）
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
source-wordcount: '152'
ht-degree: 100%
---

# Message Center（コントロール）{#message-center-control}



以下で説明するワークフローは、毎時間実行されるようにスケジュールされています。 このワークフローは、デフォルトで **Message Center - コントロール**&#x200B;モジュールと共にインストールされます。


詳しくは、Campaign のバージョンに応じて、次の節を参照してください。

![](assets/do-not-localize/v7.jpeg)[Campaign v7 ドキュメント](../../message-center/using/about-transactional-messaging.md)

![](assets/do-not-localize/v8.png)[Campaign v8 ドキュメント](https://experienceleague.adobe.com/docs/campaign/campaign-v8/send/transactional.html?lang=ja)


<table> 
 <tbody> 
  <tr> 
   <td> <strong>ラベル</strong><br /> </td> 
   <td> <strong>内部名</strong><br /> </td> 
   <td> <strong>説明</strong><br /> </td> 
  </tr> 
  <tr> 
   <td> Message Center &lt;外部アカウント名&gt;<br /> </td> 
   <td> mcSynch_&lt;外部アカウント名&gt;<br /> </td> 
   <td> このワークフローの機能は次のとおりです。<br /> 
    <ul> 
     <li> <p>操作によって処理されるイベントリストを復元します。</p> </li> 
     <li> <p>配信メッセージの選定を復元するために NmsBroadLogMsg テーブルと同期します。</p> </li> 
     <li> <p>NmsBroadLogMsg テーブルとの同期が完了するとただちに、イベント配信ログを復元します。</p> </li> 
     <li> <p>配信 URL のトラッキングを復元するために NmsTrackingUrl テーブルと同期します。</p> </li> 
     <li> <p>NmsTrackingUrl テーブルとの同期が完了するとただちに、イベントトラッキング URL を復元します。</p> </li> 
     <li> <p>配信の送信後 3 時間おきに、強制隔離されたすべてのメールアドレスを復元できます。</p> </li> 
    </ul> </td> 
  </tr> 
 </tbody> 
</table>

