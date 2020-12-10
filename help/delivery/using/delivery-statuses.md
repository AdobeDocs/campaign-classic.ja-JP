---
solution: Campaign Classic
product: campaign
title: 配信ステータス
description: 配信ダッシュボードで使用できるステータスについての詳細。
audience: delivery
content-type: reference
topic-tags: monitoring-deliveries
translation-type: tm+mt
source-git-commit: de0e4555d3e2c5dff8d86a22ff4db85953105db1
workflow-type: tm+mt
source-wordcount: '602'
ht-degree: 79%

---


# 配信ステータス {#delivery-statuses}

<!--ajouter intro 

ajouter screenshot -->

配信の送信が完了すると、配信ダッシュボードにステータスが表示され、送信が成功したかどうかを監視できます。 可能なステータスについては、次の節で詳しく説明します。

![](assets/delivery-status.png)

発生する可能性のある様々な配信障害とその解決方法についての詳細は、[このページ](../../delivery/using/understanding-delivery-failures.md)を参照してください。

**関連トピック：**

* [配信ダッシュボード](../../delivery/using/delivery-dashboard.md)
* [配信のトラブルシューティング](../../delivery/using/delivery-troubleshooting.md)
* [配信品質について](../../delivery/using/about-deliverability.md)

## 配信ステータスのリスト{#list-delivery-statuses}

<table> 
 <thead> 
  <tr> 
   <th> ステータス<br /> </th> 
   <th> 定義と解決策<br /> </th> 
  </tr> 
 </thead> 
 <tbody> 
  <tr> 
   <td> 送信済み<br /> </td> 
   <td> 配信は、メッセージプロバイダーに正しく送信されました（ただし、受信者が受信しているとは限りません）。<br /> </td> 
  </tr> 
  <tr> 
   <td> 無視<br /> </td> 
   <td> 配信は、アドレスにエラーがあるので受信者に送信されませんでした。ブロックリストへの登録、強制隔離、未指定または重複の可能性があります。 <br /> </td> 
  </tr> 
  <tr> 
   <td> 失敗<br /> </td> 
   <td> 無効なアドレスやインボックスが満杯であることが原因で、配信は受信者に到達できませんでした。パーソナライゼーションブロックの問題に関係していることもあり、その場合、スキーマが配信マッピングと一致しないとエラーが生成されます。<a href="../../delivery/using/understanding-delivery-failures.md" target="_blank">配信エラーについて</a><br />を参照 </td> 
  </tr>
  <tr> 
   <td> 保留中<br /> </td> 
   <td> 配信の送信の準備が完了し、配信サーバー（MTA）によって処理されます。<a href="#pending-status" target="_blank">保留中ステータス</a>を参照してください。<br /> </td> 
  </tr> 
  <tr> 
   <td> 該当なし<br /> </td> 
   <td> メッセージはサーバー（MTA）に取り込まれましたが、まだ処理されていません。<br /> </td> 
  </tr>  
  <tr> 
   <td> 配信がキャンセル済み<br /> </td> 
   <td> 操作がオペレーターによってキャンセルされました。<br /> </td> 
  </tr> 
  <tr> 
   <td> サービスプロバイダーによる判断<br /> </td> 
   <td> SMS サービスプロバイダーが配信を受信しました。<br /> </td> 
  </tr> 
  <tr> 
   <td> モバイルで受信済み<br /> </td> 
   <td> 受信者がモバイルデバイスで SMS を受信しました。<br /> </td> 
  </tr>
  <tr> 
   <td> サービスプロバイダーに送信済み<br /> </td> 
   <td> 配信は SMS サービスプロバイダーに送信されましたが、まだ受信されていません。<br />
   </td> 
  </tr> 
  <tr> 
   <td> 準備済み<br /> </td> 
   <td> 外部コネクタ（モバイルチャネルなど）でのみ使用される中間ステータス。「保留中」ステータスの次に遷移するステータスであり、後続のステータスは外部コネクタが決定します。<br /> </td> 
  </tr> 
 </tbody> 
</table>

Adobe Campaign E メールの配信品質の最適化方法について詳しくは、[配信品質のベストプラクティスガイド](../../delivery/using/deliverability-key-points.md)と[このページ](../../delivery/using/about-deliverability.md)を参照してください。

## 保留中ステータス {#pending-status}

配信を確認した後に、配信のステータスが&#x200B;**[!UICONTROL 保留中]**&#x200B;である場合があります。このステータスは、一部のリソースが使用可能になるのを実行プロセスが待機していることを意味します。

**[!UICONTROL 保留中]**&#x200B;ステータスは、配信はスケジュールされたが特定の日付まで保留されることを意味している可能性があります。詳しくは、[配信のスケジュール](../../delivery/using/steps-sending-the-delivery.md#scheduling-the-delivery-sending)の節を参照してください。

配信が送信されず、ステータスが&#x200B;**[!UICONTROL 保留中]**&#x200B;のままである場合は、次のことが原因である可能性があります。

* MTA（Message Transfert Agent）が開始されておらず、再起動する必要がある可能性があります。MTA は配信サーバーでモジュールとプロセスを実行し、配信サーバーは E メールの送信を管理します。

   これを確認してモジュールを開始する（必要な場合）には、次の手順を実行します。

   >[!NOTE]
   >
   >この操作は、キャンペーンサーバーにアクセスして、**オンプレミス**&#x200B;または&#x200B;**ハイブリッド**&#x200B;ホスティングモデルで実行できます（[ホスティングモデル](../../installation/using/hosting-models.md)を参照）。

   1. MTA サーバーで `mta@<instance>` モジュールが起動されていることを確認します。

      ```
      nlserver pdump
      HH:MM:SS > Application server for Adobe Campaign Classic (X.Y.Z YY.R build nnnn@SHA1) of DD/MM/YYYY
      [...]
      mta@<INSTANCENAME> (9268) - 23.0 Mb
      [...]
      ```

   1. MTA がリストされていない場合は、次のコマンドを使用して開始します。

      ```
      nlserver start mta@<INSTANCENAME>
      ```

      >[!NOTE]
      >
      >`<INSTANCENAME>` をインスタンスの名前（production、development など）に置き換えます。インスタンス名は設定ファイルで識別されます。 `[path of application]nl6/conf/config-<INSTANCENAME>.xml`

* 送信サーバーに設定されていないアフィニティを配信で使用している可能性があります。

   この場合は、トラフィック管理（IP アフィニティ）の設定をチェックし、「**[!UICONTROL IP アドレスを使用してアフィニティを管理する]**」フィールドを使用して、アフィニティを管理する MTA に配信をリンクします。アフィニティについて詳しくは、[この節](../../installation/using/configuring-campaign-server.md#personalizing-delivery-parameters)を参照してください。

* 実行中のキャンペーンが多すぎる場合、配信ステータスは「保留」のままです。

   同時キャンペーンの制限は、**[!UICONTROL NmsOperation_LimitConcurrency]**&#x200B;オプションで定義されます。 デフォルト値は 10 です。

   [このページ](../../installation/using/configuring-campaign-options.md)のオプションの詳細。


**関連トピック：**

* [配信ログと履歴](#delivery-logs-and-history)
* [配信エラーの理解](../../delivery/using/understanding-delivery-failures.md)
* [配信エラーのタイプと理由](../../delivery/using/understanding-delivery-failures.md#delivery-failure-types-and-reasons)
