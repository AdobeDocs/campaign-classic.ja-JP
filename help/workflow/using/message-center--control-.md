---
title: Message Center（コントロール）
seo-title: Message Center（コントロール）
description: Message Center（コントロール）
seo-description: null
page-status-flag: never-activated
uuid: bdb3610b-a893-4e60-a9f7-f21d90b66919
contentOwner: sauviat
products: SG_CAMPAIGN/CLASSIC
audience: workflow
content-type: reference
topic-tags: technical-workflows
discoiquuid: 69e3e99f-d392-4316-926c-3c3c675415ad
index: y
internal: n
snippet: y
translation-type: ht
source-git-commit: c10a0a11c6e9952aa47da1f7a15188c79c62508d

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

