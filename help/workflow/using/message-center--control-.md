---
solution: Campaign Classic
product: campaign
title: Message Center（コントロール）
description: Message Center（コントロール）
audience: workflow
content-type: reference
topic-tags: technical-workflows
translation-type: tm+mt
source-git-commit: 972885c3a38bcd3a260574bacbb3f507e11ae05b
workflow-type: tm+mt
source-wordcount: '157'
ht-degree: 100%

---


# Message Center（コントロール）{#message-center-control}

以下で説明するワークフローは、毎時間実行されるようにスケジュールされています。このワークフローは、デフォルトで **Message Center（コントロール）**&#x200B;モジュールと共にインストールされます。このモジュールについて詳しくは、この[節](../../message-center/using/about-transactional-messaging.md)を参照してください。

Message Center モジュールに関連するテクニカルワークフローの設定方法について詳しくは、[このページ](../../message-center/using/technical-workflows.md)を参照してください。

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

