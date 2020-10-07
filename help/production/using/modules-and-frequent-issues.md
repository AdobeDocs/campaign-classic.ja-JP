---
title: モジュールおよびよくある問題
seo-title: モジュールおよびよくある問題
description: モジュールおよびよくある問題
seo-description: null
page-status-flag: never-activated
uuid: d53324ce-b6e2-40d7-932d-36ce4a6f5cf8
contentOwner: sauviat
products: SG_CAMPAIGN/CLASSIC
audience: production
content-type: reference
topic-tags: troubleshooting
discoiquuid: a44f5e71-3f9b-4d02-8b7a-a9782bb6bdd8
translation-type: tm+mt
source-git-commit: 70b143445b2e77128b9404e35d96b39694d55335
workflow-type: tm+mt
source-wordcount: '259'
ht-degree: 10%

---


# モジュールおよびよくある問題{#modules-and-frequent-issues}

頻繁に発生する問題の影響を受けるモジュールのリストを次に示します。

<table> 
 <thead> 
  <tr> 
   <th> モジュール </th> 
   <th> 実行範囲 </th> 
   <th> トラブルシューティング </th> 
  </tr> 
 </thead> 
 <tbody> 
  <tr> 
   <td> エクスポート </td> 
   <td> エクスポートプロセスの実行<br /> </td> 
   <td> このエクスポートをスケジュールしたオペレーターは、再起動する必要があります。 差分またはフル再起動。<br /> </td> 
  </tr> 
  <tr> 
   <td> インポート </td> 
   <td> インポート・プロセスの実行<br /> </td> 
   <td> このエクスポートをスケジュールしたオペレーターは、再起動する必要があります。 データベースで重複を確認します。<br /> </td> 
  </tr> 
  <tr> 
   <td> inMail </td> 
   <td> バウンスメールボックスの読み取り<br /> </td> 
   <td> バウンスメールが転送されなくなった場合は、このモジュールをチェックします。<br /> </td> 
  </tr> 
  <tr> 
   <td> MTA </td> 
   <td> 電子メールを配信<br /> </td> 
   <td> メールが送信されなくなった場合は、このモジュールをチェックします。<br /> </td> 
  </tr> 
  <tr> 
   <td> stat </td> 
   <td> MTA 接続統計を維持<br /> </td> 
   <td> メールが送信されなくなった場合は、このモジュールをチェックします。<br /> </td> 
  </tr> 
  <tr> 
   <td> syslogd </td> 
   <td> ログの書き込み<br /> </td> 
   <td> ログファイルに一部のログがない場合は、モジュールでポート6666が使用されていることを確認してください。 オープンポートの <a href="../../production/using/general-architecture.md#list-of-open-ports" target="_blank">リストを参照</a>。<br /> </td> 
  </tr> 
  <tr> 
   <td> tracking </td> 
   <td> トラッキングログの統合と取得<br /> </td> 
   <td> トラッキングログが転送されなくなった場合は、このモジュールを選択します。<br /> </td> 
  </tr> 
  <tr> 
   <td> trackinglogd </td> 
   <td> Tracking log writing and purging server<br /> </td> 
   <td> トラッキングログが転送されなくなり、サーバー上のファイルにログの痕跡がない場合は、このモジュールをチェックします。 「 <a href="../../production/using/tracking-logs-issues.md" target="_blank">トラッキングログに関する問題</a>」を参照してください。<br /> </td> 
  </tr> 
  <tr> 
   <td> 番犬 </td> 
   <td> 起動および監視インスタンス<br /> </td> 
   <td> プロセスの開始がない場合は、このモジュールをチェックします。<br /> </td> 
  </tr> 
  <tr> 
   <td> Web </td> 
   <td> Application server (HTTP and SOAP)<br /> </td> 
   <td> コンソールとWeb接続が動作せず、 <strong>xtk:session</strong> typeエラーが発生する場合は、このモジュールをチェックしてください。<br /> </td> 
  </tr> 
  <tr> 
   <td> wfserver </td> 
   <td> ワークフローインスタンスの実行を制御します。<br /> </td> 
   <td> 問題が発生した場合は、このモジュールを再起動します。 必要に応じて、「 <a href="../../production/using/log-precision.md" target="_blank">ログの精度</a> 」セクションに詳細なログの精度を上げる手順を適用します。<br /> </td> 
  </tr> 
 </tbody> 
</table>

