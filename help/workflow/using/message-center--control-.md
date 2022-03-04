---
product: campaign
title: Message Center（コントロール）
description: Message Center（コントロール）
feature: Workflows
source-git-commit: b94c4bfd478b4a8fbcefe6341608dd6a14bb31d3
workflow-type: tm+mt
source-wordcount: '155'
ht-degree: 100%

---


# Message Center（コントロール）{#message-center-control}

![](../../assets/common.svg)

以下で説明するワークフローは、毎時間実行されるようにスケジュールされています。このワークフローは、デフォルトで **Message Center - コントロール**&#x200B;モジュールと共にインストールされます。


詳しくは、Campaign のバージョンに応じて、次の節を参照してください。

![](assets/do-not-localize/v7.jpeg)[  Campaign v7 ドキュメント](../../message-center/using/about-transactional-messaging.md)

![](assets/do-not-localize/v8.png)[  Campaign v8 ドキュメント](https://experienceleague.adobe.com/docs/campaign/campaign-v8/send/transactional.html?lang=ja)


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
     <li> <p>配信の送信後 3 時間おきに、強制隔離されたすべての E メールアドレスを復元できます。</p> </li> 
    </ul> </td> 
  </tr> 
 </tbody> 
</table>

