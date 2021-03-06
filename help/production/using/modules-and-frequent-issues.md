---
product: campaign
title: モジュールおよびよくある問題
description: モジュールおよびよくある問題
audience: production
content-type: reference
topic-tags: troubleshooting
exl-id: dbd50178-0a16-46ed-bfad-47beb3c2a420
source-git-commit: 20509f44c5b8e0827a09f44dffdf2ec9d11652a1
workflow-type: tm+mt
source-wordcount: '255'
ht-degree: 8%

---

# モジュールおよびよくある問題{#modules-and-frequent-issues}

![](../../assets/v7-only.svg)

次に、頻繁な問題の影響を受けるモジュールのリストを示します。

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
   <td> この書き出しをスケジュールしたオペレーターは、再度開始する必要があります。 デルタまたはフル再起動。<br /> </td> 
  </tr> 
  <tr> 
   <td> インポート </td> 
   <td> インポートプロセスの実行<br /> </td> 
   <td> この書き出しをスケジュールしたオペレーターは、再度開始する必要があります。 データベースで重複を確認します。<br /> </td> 
  </tr> 
  <tr> 
   <td> inMail </td> 
   <td> バウンスメールボックスの読み取り<br /> </td> 
   <td> バウンスメールが転送されなくなった場合は、このモジュールをチェックします。<br /> </td> 
  </tr> 
  <tr> 
   <td> MTA </td> 
   <td> E メールを配信<br /> </td> 
   <td> メールが送信されなくなった場合は、このモジュールを確認します。<br /> </td> 
  </tr> 
  <tr> 
   <td> stat </td> 
   <td> MTA 接続統計を維持<br /> </td> 
   <td> メールが送信されなくなった場合は、このモジュールを確認します。<br /> </td> 
  </tr> 
  <tr> 
   <td> syslogd </td> 
   <td> ログの書き込み<br /> </td> 
   <td> ログファイルに一部のログがない場合は、モジュールがポート 6666 を使用していることを確認します。 参照： <a href="../../production/using/general-architecture.md#list-of-open-ports" target="_blank">オープンポートのリスト</a>.<br /> </td> 
  </tr> 
  <tr> 
   <td> tracking </td> 
   <td> トラッキングログの統合と取得<br /> </td> 
   <td> トラッキングログが転送されなくなった場合は、このモジュールをチェックします。<br /> </td> 
  </tr> 
  <tr> 
   <td> trackinglogd </td> 
   <td> トラッキングログの書き込みとサーバーのパージ<br /> </td> 
   <td> トラッキングログが転送されなくなり、サーバー上のファイルにログのトレースがない場合は、このモジュールをチェックします。 参照： <a href="../../production/using/tracking-logs-issues.md" target="_blank">トラッキングログの問題</a>.<br /> </td> 
  </tr> 
  <tr> 
   <td> 監視 </td> 
   <td> 起動および監視インスタンス<br /> </td> 
   <td> プロセスが開始しない場合は、このモジュールをチェックします。<br /> </td> 
  </tr> 
  <tr> 
   <td> Web </td> 
   <td> アプリケーションサーバー（HTTP および SOAP）<br /> </td> 
   <td> コンソールと Web 接続が機能せず、トリガーが機能しない場合は、このモジュールをチェックし、 <strong>xtk:session</strong> 型エラー<br /> </td> 
  </tr> 
  <tr> 
   <td> wfserver </td> 
   <td> ワークフローインスタンスの実行を制御します。<br /> </td> 
   <td> 問題が発生した場合は、このモジュールを再起動します。 必要に応じて、 <a href="../../production/using/log-precision.md" target="_blank">ログの精度</a> 」セクションに入力します。<br /> </td> 
  </tr> 
 </tbody> 
</table>
