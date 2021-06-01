---
product: campaign
title: モジュールおよびよくある問題
description: モジュールおよびよくある問題
audience: production
content-type: reference
topic-tags: troubleshooting
exl-id: dbd50178-0a16-46ed-bfad-47beb3c2a420
source-git-commit: 98d646919fedc66ee9145522ad0c5f15b25dbf2e
workflow-type: tm+mt
source-wordcount: '255'
ht-degree: 8%

---

# モジュールおよびよくある問題{#modules-and-frequent-issues}

次に、よくある問題の影響を受けるモジュールのリストを示します。

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
   <td> import </td> 
   <td> インポートプロセスの実行<br /> </td> 
   <td> このエクスポートをスケジュールしたオペレーターは、再起動する必要があります。 データベースで重複がないか確認します。<br /> </td> 
  </tr> 
  <tr> 
   <td> inMail </td> 
   <td> バウンスメールボックスの読み取り<br /> </td> 
   <td> バウンスメールが転送されなくなった場合は、このモジュールをチェックします。<br /> </td> 
  </tr> 
  <tr> 
   <td> MTA </td> 
   <td> Eメールを配信<br /> </td> 
   <td> メールの送信が終了した場合は、このモジュールを確認します。<br /> </td> 
  </tr> 
  <tr> 
   <td> stat </td> 
   <td> MTA 接続統計を維持<br /> </td> 
   <td> メールの送信が終了した場合は、このモジュールを確認します。<br /> </td> 
  </tr> 
  <tr> 
   <td> syslogd </td> 
   <td> ログの書き込み<br /> </td> 
   <td> ログファイルに一部のログが見つからない場合は、モジュールがポート6666を使用していることを確認します。 <a href="../../production/using/general-architecture.md#list-of-open-ports" target="_blank">オープンポートのリスト</a>.<br />を参照してください。 </td> 
  </tr> 
  <tr> 
   <td> tracking </td> 
   <td> トラッキングログの統合と取得<br /> </td> 
   <td> トラッキングログが転送されなくなった場合は、このモジュールをチェックします。<br /> </td> 
  </tr> 
  <tr> 
   <td> trackinglogd </td> 
   <td> トラッキングログの書き込みとサーバーのパージ<br /> </td> 
   <td> トラッキングログが転送されなくなり、サーバー上のファイルにログのトレースがない場合は、このモジュールをチェックします。 <a href="../../production/using/tracking-logs-issues.md" target="_blank">トラッキングログの問題</a>を参照してください。<br /> </td> 
  </tr> 
  <tr> 
   <td> ウォッチ </td> 
   <td> 起動および監視インスタンス<br /> </td> 
   <td> 開始するプロセスがない場合は、このモジュールをチェックします。<br /> </td> 
  </tr> 
  <tr> 
   <td> Web </td> 
   <td> アプリケーションサーバー（HTTPおよびSOAP）<br /> </td> 
   <td> コンソールとWeb接続が機能せず、<strong>xtk:session</strong>タイプのエラー<br />がトリガーする場合は、このモジュールをチェックします。 </td> 
  </tr> 
  <tr> 
   <td> wfserver </td> 
   <td> ワークフローインスタンスの実行を制御します。<br /> </td> 
   <td> 問題が発生した場合は、このモジュールを再起動します。 必要に応じて、<a href="../../production/using/log-precision.md" target="_blank">ログの精度</a>の節で説明されているログの精度を高める手順を適用します。<br /> </td> 
  </tr> 
 </tbody> 
</table>
