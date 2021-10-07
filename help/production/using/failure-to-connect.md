---
product: campaign
title: 接続の失敗
description: 接続の失敗
audience: production
content-type: reference
topic-tags: troubleshooting
exl-id: 3c793dc1-9654-4289-a3d2-30c3078fd848
source-git-commit: 20509f44c5b8e0827a09f44dffdf2ec9d11652a1
workflow-type: tm+mt
source-wordcount: '376'
ht-degree: 4%

---

# 接続の失敗{#failure-to-connect}

![](../../assets/v7-only.svg)

接続の問題の原因は複数で、様々なコンテキストに依存する場合があります。

次のテストを試してみてください。接続の失敗が解決しない場合は、[Adobeカスタマーケア ](https://helpx.adobe.com/jp/enterprise/admin-guide.html/enterprise/using/support-for-experience-cloud.ug.html) にお問い合わせください。



<table> 
<thead> 
<tr> 
<th>チェック <br /> </th> 
<th>解決策<br /> </th> 
</tr> 
</thead> 
<tbody> 
<tr> 
<td>コンピュータからインターネットにアクセスできますか？</td> 
<td>インターネット上の Web サイトに接続できることを確認します（例： ）。 接続できない場合は、お使いのコンピューターに問題があります。 システム管理者に問い合わせてください。</td>
</tr>
<tr> 
<td>別のサービスを介してAdobe Campaignをホストするサーバーに接続できますか。</td> 
<td>SSH またはその他の手段を使用してサーバーに接続します。 これができない場合は、ホスト会社に問題があります。 システム管理者に問い合わせてください。</td>
</tr>
<tr> 
<td>Web サーバーは応答しますか。</td> 
<td>Web ブラウザーを使用してAdobe Campaignサーバーにアクセスする URL に接続します。<b>http(s:// &lt;urlserver&gt;</b>) 応答しない場合、Web サーバーはマシン上で停止します。 サービスを再起動するには、ホスト会社のシステム管理者に問い合わせてください。</td>
</tr>
<tr> 
<td>Adobe Campaignは正しく統合されていますか。</td> 
<td>次の場所にログオンします。<b>http(s://&lt;urlserver&gt;/r/test</b> URL。 サーバーは、次のタイプのメッセージを返す必要があります。&lt;redir status='OK' date='YYYY/MM/DD HH:MM:SS' build='XXXX' host='&lt;hostname&gt;' localHost='&lt;server&gt;'/&gt;
この結果が得られない場合は、統合が考慮された Web サーバーの設定を確認します。</td>
</tr>
<tr> 
<td>次の URL に接続します。<b>http(s)://&lt;URLSERVER&gt;/nl/jsp/logon.jsp</b></td>
<td>Tomcat Java エラーが発生した場合は、JAVA 統合が正しく実行されているかどうかを確認します。 ファイル [application のパス ]/nl6/customer.shに統合されています。</td>
</tr>
<tr> 
<td>次の URL に接続します。<b>http(s)://&lt;URLSERVER&gt;/nl/jsp/logon.jsp</b></td>
<td>空白のページが取得された場合は、Adobe Campaign Web モジュールが起動しているかどうかを確認します。 コマンド nlserver pdump は、DD/MM/YYYY のAdobe Campaign Classic(7.X YY.R build XXX@SHA1) のアプリケーションサーバーを返す必要があります。 そうでない場合は、nlserver start web コマンドを使用してモジュールを再起動します</td>
</tr>
<tr>
<td>セキュリティゾーンの一般的な設定を確認します。</td>
<td>セキュリティゾーンの設定について詳しくは、<a href="https://experienceleague.adobe.com/docs/campaign-classic/using/installing-campaign-classic/additional-configurations/configuring-campaign-server.html?lang=en#configuring-campaign-server"/> この節を参照してください。</a></td>
</tr>
<tr>
<td>コマンド nlserver pdump が <b>No tasks</b> を返す</td>
<td>Adobe Campaignアプリケーション全体を再起動する必要があります。 これをおこなうには、次のコマンドを使用します。<b>nlserver watchdog -svc -noconsole</b></td>
</tr>
</tbody> 
</table>
