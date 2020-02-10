---
title: モジュールと頻繁な問題
seo-title: モジュールと頻繁な問題
description: モジュールと頻繁な問題
seo-description: null
page-status-flag: never-activated
uuid: d53324ce-b6e2-40d7-932d-36ce4a6f5cf8
contentOwner: sauviat
products: SG_CAMPAIGN/CLASSIC
audience: production
content-type: reference
topic-tags: troubleshooting
discoiquuid: a44f5e71-3f9b-4d02-8b7a-a9782bb6bdd8
index: y
internal: n
snippet: y
translation-type: tm+mt
source-git-commit: 20f835c357d016643ea1f3209ee4dfb6d3239f90

---


# モジュールと頻繁な問題{#modules-and-frequent-issues}

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
   <td> このエクスポートをスケジュールしたオペレーターは、再起動する必要があります。 差分またはフル・リリース。<br /> </td> 
  </tr> 
  <tr> 
   <td> インポート </td> 
   <td> インポートプロセスの実行<br /> </td> 
   <td> このエクスポートをスケジュールしたオペレーターは、再起動する必要があります。 データベースで重複を確認します。<br /> </td> 
  </tr> 
  <tr> 
   <td> inMail </td> 
   <td> バウンスメールボックスの読み取り中<br /> </td> 
   <td> バウンスメールが転送されなくなった場合は、このモジュールを選択します。<br /> </td> 
  </tr> 
  <tr> 
   <td> MTA </td> 
   <td> 電子メールの配信<br /> </td> 
   <td> メールの送信が終了した場合は、このモジュールをチェックします。<br /> </td> 
  </tr> 
  <tr> 
   <td> stat </td> 
   <td> MTA 接続統計を維持<br /> </td> 
   <td> メールの送信が終了した場合は、このモジュールをチェックします。<br /> </td> 
  </tr> 
  <tr> 
   <td> syslogd </td> 
   <td> ログの書き込み<br /> </td> 
   <td> ログファイルに一部のログがない場合は、モジュールでポート6666が使用されていることを確認します。 「オープン・ポ <a href="../../production/using/general-architecture.md#list-of-open-ports" target="_blank">ートのリスト」を参照</a>。<br /> </td> 
  </tr> 
  <tr> 
   <td> tracking </td> 
   <td> トラッキングログの統合と取得<br /> </td> 
   <td> トラッキングログが転送されなくなった場合は、このモジュールを確認します。<br /> </td> 
  </tr> 
  <tr> 
   <td> trackinglogd </td> 
   <td> Tracking log writing and purging server<br /> </td> 
   <td> トラッキングログが転送されなくなり、サーバー上のファイルにログの跡がない場合は、このモジュールをチェックします。 トラッキングロ <a href="../../production/using/tracking-logs-issues.md" target="_blank">グに関する問題を参照してくださ</a>い。<br /> </td> 
  </tr> 
  <tr> 
   <td> 番犬 </td> 
   <td> 起動および監視インスタンス<br /> </td> 
   <td> 開始するプロセスがない場合は、このモジュールをチェックします。<br /> </td> 
  </tr> 
  <tr> 
   <td> Web </td> 
   <td> Application server (HTTP and SOAP)<br /> </td> 
   <td> コンソールとWeb接続が動作しない場合はこのモジュールをチェックし、 <strong>xtk:session</strong> typeエラーをトリガします。<br /> </td> 
  </tr> 
  <tr> 
   <td> wfserver </td> 
   <td> ワークフローインスタンスの実行を制御します。<br /> </td> 
   <td> 問題が発生した場合は、このモジュールを再起動します。 必要に応じて、「ログの精度」セクションで詳細に説明したログの精度を上げる <a href="../../production/using/log-precision.md" target="_blank">手順を適用し</a> ます。<br /> </td> 
  </tr> 
 </tbody> 
</table>

