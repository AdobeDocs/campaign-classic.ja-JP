---
product: campaign
title: 接続の失敗
description: 接続の失敗
feature: Monitoring
badge-v7-prem: label="オンプレミス／ハイブリッドのみ" type="Caution" url="https://experienceleague.adobe.com/docs/campaign-classic/using/installing-campaign-classic/architecture-and-hosting-models/hosting-models-lp/hosting-models.html?lang=ja" tooltip="オンプレミスデプロイメントとハイブリッドデプロイメントにのみ適用されます"
audience: production
content-type: reference
topic-tags: troubleshooting
exl-id: 3c793dc1-9654-4289-a3d2-30c3078fd848
TQID: https://experienceleague.adobe.com/zQXUUtLQveDPTu8blS48gCzTl8lv09vlJXAtjAjgtW4
product_v2:
  - id: dfc56824-e8b9-499e-85d4-21aedb507314
topic_v2:
  - id: c1579802-ddd4-4214-8a91-97b2066abe11
  - id: d095671a-1355-40aa-8b5f-06c33c68080b
source-git-commit: 4c295c0dabae8aba298390a3da2422a3fa1219f9
workflow-type: tm+mt
source-wordcount: 417
ht-degree: 11%

---

# 接続の失敗{#failure-to-connect}



接続の問題の理由は複数あり、さまざまなコンテキストに依存します。

次のテストを試すことができます。接続エラーが解決しない場合は、[Adobe カスタマーケア &#x200B;](https://helpx.adobe.com/jp/enterprise/admin-guide.html/enterprise/using/support-for-experience-cloud.ug.html)にお問い合わせください。



<table> 
<thead> 
<tr> 
<th>チェック <br /> </th> 
<th>解決策<br /> </th> 
</tr> 
</thead> 
<tbody> 
<tr> 
<td>パソコンからインターネットにアクセスできますか？</td> 
<td>インターネット上のWeb サイトに接続できることを確認してください（例）。 接続できない場合は、問題はお使いのコンピューターにあります。 システム管理者にお問い合わせください。</td>
</tr>
<tr> 
<td>別のサービスを介してAdobe Campaignをホストしているサーバーに接続できますか？</td> 
<td>SSHまたはその他の方法でサーバーに接続します。 これが不可能な場合は、ホスト会社に問題があります。 システム管理者に問い合わせます。</td>
</tr>
<tr> 
<td>Web サーバーは応答しますか？</td> 
<td>Web ブラウザーを使用してAdobe Campaign サーバーアクセス URLに接続します：<b>http （s）:// &lt;urlserver&gt;</b>。 応答しない場合、Web サーバーはコンピューター上で停止します。 サービスを再起動するには、ホスト会社のシステム管理者に問い合わせてください。</td>
</tr>
<tr> 
<td>Adobe Campaignは正しく統合されていますか？</td> 
<td><b>http （s）://&lt;urlserver&gt;/r/test</b> URLにログオンします。 サーバーは次のタイプのメッセージを返す必要があります。&lt;redir status='OK' date='YYYY/MM/DD HH:MM:SS' build='XXXX' host='&lt;hostname&gt;' localHost='&lt;server&gt;'/&gt;
この結果が得られない場合は、Web サーバー設定で統合が考慮されていることを確認してください。</td>
</tr>
<tr> 
<td>次のURLに接続します：<b>http （s）://&lt;URLSERVER&gt;/nl/jsp/logon.jsp</b></td>
<td>Tomcat Java エラーが発生した場合は、JAVA統合が正しく実行されているかどうかを確認します。 ファイル [ アプリケーションのパス ]/nl6/customer.shに統合されます。</td>
</tr>
<tr> 
<td>次のURLに接続します：<b>http （s）://&lt;URLSERVER&gt;/nl/jsp/logon.jsp</b></td>
<td>空白のページが表示された場合は、Adobe Campaign Web モジュールが起動しているかどうかを確認します。 コマンド nlserver pdumpは、DD/MM/YYYYのAdobe Campaign Classic （7.X YY.R build XXX@SHA1）のApplication serverを返す必要があります。 そうでない場合は、nlserver start web コマンドでモジュールを再起動します</td>
</tr>
<tr>
<td>セキュリティゾーンの一般的な構成を確認します。</td>
<td>セキュリティゾーンの設定について詳しくは、この節の<a href="https://experienceleague.adobe.com/docs/campaign-classic/using/installing-campaign-classic/additional-configurations/configuring-campaign-server.html?lang=ja#configuring-campaign-server"/>を参照してください。</a></td>
</tr>
<tr>
<td>コマンド nlserver pdumpは<b> タスクを返しません</b></td>
<td>Adobe Campaign アプリケーション全体を再起動する必要があります。 これを行うには、次のコマンドを使用します。<b>nlserver watchdog -svc -noconsole</b></td>
</tr>
</tbody> 
</table>
