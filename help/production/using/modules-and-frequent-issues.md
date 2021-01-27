---
solution: Campaign Classic
product: campaign
title: モジュールおよびよくある問題
description: モジュールおよびよくある問題
audience: production
content-type: reference
topic-tags: troubleshooting
translation-type: tm+mt
source-git-commit: 972885c3a38bcd3a260574bacbb3f507e11ae05b
workflow-type: tm+mt
source-wordcount: '255'
ht-degree: 8%

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
   <td> エクスポート処理<br />の実行 </td> 
   <td> このエクスポートをスケジュールしたオペレーターは、再起動する必要があります。 デルタまたはフルの再起動。<br /> </td> 
  </tr> 
  <tr> 
   <td> インポート </td> 
   <td> インポート処理<br />の実行 </td> 
   <td> このエクスポートをスケジュールしたオペレーターは、再起動する必要があります。 データベースの重複を確認します。<br /> </td> 
  </tr> 
  <tr> 
   <td> inMail </td> 
   <td> 直帰のメールボックス<br />を読んでいます </td> 
   <td> バウンスメールが転送されなくなった場合は、このモジュールをチェックします。<br /> </td> 
  </tr> 
  <tr> 
   <td> MTA </td> 
   <td> 電子メール<br />を配信 </td> 
   <td> メールの送信が終了した場合は、このモジュールをチェックしてください。<br /> </td> 
  </tr> 
  <tr> 
   <td> stat </td> 
   <td> MTA 接続統計を維持<br /> </td> 
   <td> メールの送信が終了した場合は、このモジュールをチェックしてください。<br /> </td> 
  </tr> 
  <tr> 
   <td> syslogd </td> 
   <td> ログ書き込み<br /> </td> 
   <td> ログファイルに一部のログがない場合は、モジュールでポート6666が使用されていることを確認してください。 <a href="../../production/using/general-architecture.md#list-of-open-ports" target="_blank">オープンポートのリスト</a>を参照してください。<br /> </td> 
  </tr> 
  <tr> 
   <td> tracking </td> 
   <td> トラッキングログの統合と取得<br /> </td> 
   <td> トラッキングログが転送されなくなった場合は、このモジュールをチェックしてください。<br /> </td> 
  </tr> 
  <tr> 
   <td> trackinglogd </td> 
   <td> トラッキングログの書き込みとサーバーの削除<br /> </td> 
   <td> トラッキングログが転送されなくなり、サーバー上のファイルにログの痕跡がない場合は、このモジュールをチェックします。 <a href="../../production/using/tracking-logs-issues.md" target="_blank">トラッキングログの問題</a>を参照してください。<br /> </td> 
  </tr> 
  <tr> 
   <td> 番犬 </td> 
   <td> 起動および監視インスタンス<br /> </td> 
   <td> プロセス開始がない場合は、このモジュールをチェックしてください。<br /> </td> 
  </tr> 
  <tr> 
   <td> Web </td> 
   <td> アプリケーションサーバー（HTTPおよびSOAP）<br /> </td> 
   <td> コンソールとWeb接続が動作せず、トリガーが<strong>xtk:session</strong>タイプのエラー<br />でない場合は、このモジュールをチェックしてください。 </td> 
  </tr> 
  <tr> 
   <td> wfserver </td> 
   <td> ワークフローインスタンスの実行を制御します。<br /> </td> 
   <td> 問題が発生した場合は、このモジュールを再起動します。 必要に応じて、<a href="../../production/using/log-precision.md" target="_blank">ログの精度</a>のセクションで詳細に説明されているログの精度を上げる手順を適用します。<br /> </td> 
  </tr> 
 </tbody> 
</table>

