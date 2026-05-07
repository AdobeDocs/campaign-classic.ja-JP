---
product: campaign
title: モジュールおよびよくある問題
description: モジュールおよびよくある問題
feature: Monitoring, Troubleshooting
badge-v7-prem: label="オンプレミス／ハイブリッドのみ" type="Caution" url="https://experienceleague.adobe.com/docs/campaign-classic/using/installing-campaign-classic/architecture-and-hosting-models/hosting-models-lp/hosting-models.html?lang=ja" tooltip="オンプレミスデプロイメントとハイブリッドデプロイメントにのみ適用されます"
audience: production
content-type: reference
topic-tags: troubleshooting
exl-id: dbd50178-0a16-46ed-bfad-47beb3c2a420
source-git-commit: 14ba450ebff9bba6a36c0df07d715b7279604222
workflow-type: tm+mt
source-wordcount: '288'
ht-degree: 17%

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
   <td> 書き出しプロセス <br />の実行 </td> 
   <td> この書き出しをスケジュールしたオペレーターは、書き出しを再開する必要があります。 差分または完全に再起動します。<br /> </td> 
  </tr> 
  <tr> 
   <td> 読み込み </td> 
   <td> インポートプロセスの実行<br /> </td> 
   <td> この書き出しをスケジュールしたオペレーターは、書き出しを再開する必要があります。 データベースに重複がないか確認してください。<br /> </td> 
  </tr> 
  <tr> 
   <td> inMail </td> 
   <td> バウンスメールボックスの読み取り<br /> </td> 
   <td> バウンスメールが転送されなくなった場合は、このモジュールを確認してください。<br /> </td> 
  </tr> 
  <tr> 
   <td> MTA </td> 
   <td> メールの配信<br /> </td> 
   <td> メールが送信されなくなった場合は、このモジュールを確認してください。<br /> </td> 
  </tr> 
  <tr> 
   <td> 統計 </td> 
   <td> MTA接続統計を維持<br /> </td> 
   <td> メールが送信されなくなった場合は、このモジュールを確認してください。<br /> </td> 
  </tr> 
  <tr> 
   <td> syslogd </td> 
   <td> ログの書き込み<br /> </td> 
   <td> ログファイルに一部のログが見つからない場合は、モジュールがポート 6666を使用していることを確認します。 開いているポートの<a href="../../production/using/general-architecture.md#list-of-open-ports" target="_blank"> リスト </a>を参照してください。<br /> </td> 
  </tr> 
  <tr> 
   <td> tracking </td> 
   <td> トラッキングログの統合と取得<br /> </td> 
   <td> トラッキングログが転送されなくなった場合は、このモジュールを確認してください。<br /> </td> 
  </tr> 
  <tr> 
   <td> trackinglogd </td> 
   <td> ログの書き込みとパージ サーバー<br />のトラッキング </td> 
   <td> トラッキングログが転送されなくなり、サーバー上のファイルにログのトレースがない場合は、このモジュールを確認してください。 <a href="../../production/using/tracking-logs-issues.md" target="_blank"> トラッキングログの問題</a>.<br />を参照してください </td> 
  </tr> 
  <tr> 
   <td> ウォッチドッグ </td> 
   <td> 起動と監視のインスタンス <br /> </td> 
   <td> プロセスが開始されない場合は、このモジュールを確認してください。<br /> </td> 
  </tr> 
  <tr> 
   <td> Web </td> 
   <td> アプリケーションサーバー（HTTPおよびSOAP） <br /> </td> 
   <td> コンソールとweb接続が機能しない場合は、このモジュールを確認し、<strong>xtk:session</strong> type error<br />をトリガーします </td> 
  </tr> 
  <tr> 
   <td> wfserver </td> 
   <td> ワークフローインスタンスの実行を制御します。<br /> </td> 
   <td> 問題が発生した場合は、このモジュールを再起動してください。 必要に応じて、<a href="../../production/using/log-precision.md" target="_blank"> ログ精度</a> セクションで詳細に説明されているログの精度を向上させる手順を適用します。<br /> </td> 
  </tr> 
 </tbody> 
</table>
