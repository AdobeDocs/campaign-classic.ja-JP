---
product: campaign
title: モジュールおよびよくある問題
description: モジュールおよびよくある問題
feature: Monitoring, Troubleshooting
badge-v7-prem: label="オンプレミスおよびハイブリッド" type="Caution" url="https://experienceleague.adobe.com/docs/campaign-classic/using/installing-campaign-classic/architecture-and-hosting-models/hosting-models-lp/hosting-models.html?lang=ja" tooltip="オンプレミスデプロイメントとハイブリッドデプロイメントにのみ適用されます"
audience: production
content-type: reference
topic-tags: troubleshooting
exl-id: dbd50178-0a16-46ed-bfad-47beb3c2a420
source-git-commit: b666535f7f82d1b8c2da4fbce1bc25cf8d39d187
workflow-type: tm+mt
source-wordcount: '266'
ht-degree: 10%

---

# モジュールおよびよくある問題{#modules-and-frequent-issues}



頻繁に発生する問題の影響を受けるモジュールのリストを以下に示します。

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
   <td> この書き出しをスケジュールしたオペレーターは、再度開始する必要があります。 差分または完全な再起動。<br /> </td> 
  </tr> 
  <tr> 
   <td> 読み込み </td> 
   <td> インポートプロセスの実行<br /> </td> 
   <td> この書き出しをスケジュールしたオペレーターは、再度開始する必要があります。 データベースに重複がないか確認します。<br /> </td> 
  </tr> 
  <tr> 
   <td> inMail </td> 
   <td> バウンスメールボックスの読み取り<br /> </td> 
   <td> バウンスメールが転送されなくなった場合は、このモジュールを選択します。<br /> </td> 
  </tr> 
  <tr> 
   <td> MTA </td> 
   <td> メールを配信<br /> </td> 
   <td> メールが送信されなくなった場合は、このモジュールを選択します。<br /> </td> 
  </tr> 
  <tr> 
   <td> 統計 </td> 
   <td> MTA 接続統計を管理します<br /> </td> 
   <td> メールが送信されなくなった場合は、このモジュールを選択します。<br /> </td> 
  </tr> 
  <tr> 
   <td> syslogd </td> 
   <td> ログ書き込み<br /> </td> 
   <td> ログファイルに一部のログが見つからない場合は、モジュールがポート 6666 を使用していることを確認します。 こちらを参照してください <a href="../../production/using/general-architecture.md#list-of-open-ports" target="_blank">開いているポートのリスト</a>.<br /> </td> 
  </tr> 
  <tr> 
   <td> tracking </td> 
   <td> トラッキングログの統合と取得<br /> </td> 
   <td> トラッキングログが転送されなくなった場合は、このモジュールを確認します。<br /> </td> 
  </tr> 
  <tr> 
   <td> trackinglogd </td> 
   <td> トラッキングログの書き込みおよびパージサーバー<br /> </td> 
   <td> トラッキングログが転送されなくなり、サーバー上のファイルにログの痕跡がない場合は、このモジュールを確認します。 こちらを参照してください <a href="../../production/using/tracking-logs-issues.md" target="_blank">トラッキングログの問題</a>.<br /> </td> 
  </tr> 
  <tr> 
   <td> ウォッチドッグ </td> 
   <td> 起動および監視インスタンス<br /> </td> 
   <td> プロセスが開始しない場合は、このモジュールを確認します。<br /> </td> 
  </tr> 
  <tr> 
   <td> Web </td> 
   <td> アプリケーションサーバー（HTTP および SOAP）<br /> </td> 
   <td> トリガー コンソール接続と web 接続が機能しない場合は、このモジュールを確認して、 <strong>xtk:session</strong> エラーを入力<br /> </td> 
  </tr> 
  <tr> 
   <td> wfserver </td> 
   <td> ワークフローインスタンスの実行を制御します。<br /> </td> 
   <td> 問題が発生した場合は、このモジュールを再起動します。 必要に応じて、で説明されているログの精度を高めるための手順を適用します。 <a href="../../production/using/log-precision.md" target="_blank">ログの精度</a> セクション。<br /> </td> 
  </tr> 
 </tbody> 
</table>
