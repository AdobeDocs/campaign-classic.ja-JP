---
product: campaign
title: 接続の失敗
description: 接続の失敗
audience: production
content-type: reference
topic-tags: troubleshooting
exl-id: 3c793dc1-9654-4289-a3d2-30c3078fd848
source-git-commit: 98d646919fedc66ee9145522ad0c5f15b25dbf2e
workflow-type: tm+mt
source-wordcount: '377'
ht-degree: 4%

---

# 接続の失敗{#failure-to-connect}

接続の問題の原因は複数で、様々なコンテキストによって異なります。

次のテストを試してみてください。接続エラーが解決しない場合は、[Adobeカスタマーケア](https://helpx.adobe.com/jp/enterprise/admin-guide.html/enterprise/using/support-for-experience-cloud.ug.html)にお問い合わせください。



<table> 
<thead> 
<tr> 
<th>チェック<br /> </th> 
<th>解決策<br /> </th> 
</tr> 
</thead> 
<tbody> 
<tr> 
<td>コンピューターからインターネットにアクセスできますか？</td> 
<td>インターネット上のWebサイトに接続できることを確認します（例： ）。 接続できない場合は、問題がコンピューター上に存在します。 システム管理者に問い合わせてください。</td>
</tr>
<tr> 
<td>別のサービスを介してAdobe Campaignをホストするサーバーに接続できますか。</td> 
<td>SSHなどの方法でサーバーに接続します。 これが不可能な場合は、ホスト会社に問題があります。 システム管理者に問い合わせてください。</td>
</tr>
<tr> 
<td>Webサーバーは応答しますか。</td> 
<td>Webブラウザーを使用してAdobe CampaignサーバーにアクセスするURLに接続します。<b>http(s):// &lt;urlserver&gt;</b>. 応答しない場合、Webサーバーはマシン上で停止します。 サービスを再起動するには、ホスト会社のシステム管理者に問い合わせてください。</td>
</tr>
<tr> 
<td>Adobe Campaignは正しく統合されていますか。</td> 
<td>次の場所にログオンします。<b>http(s)://&lt;urlserver&gt;/r/test</b> URL。 サーバーは、次のタイプのメッセージを返す必要があります。&lt;redir status='OK' date='YYYY/MM/DD HH:MM:SS' build='XXXX' host='&lt;hostname&gt;' localHost='&lt;server&gt;'/&gt;
この結果が得られない場合は、統合が考慮されるWebサーバーの設定を確認します。</td>
</tr>
<tr> 
<td>次のURLに接続します。<b>http(s)://&lt;URLSERVER&gt;/nl/jsp/logon.jsp</b></td>
<td>Tomcat Javaエラーが発生した場合は、JAVA統合が正しく実行されているかどうかを確認します。 これは、ファイル[applicationのパス]/nl6/customer.shに統合されています。</td>
</tr>
<tr> 
<td>次のURLに接続します。<b>http(s)://&lt;URLSERVER&gt;/nl/jsp/logon.jsp</b></td>
<td>空白のページが取得された場合は、Adobe Campaign Webモジュールが起動しているかどうかを確認します。 コマンドnlserver pdumpは、DD/MM/YYYYのAdobe Campaign Classic(7.X YY.R build XXX@SHA1)のアプリケーションサーバーを返す必要があります。 そうでない場合は、nlserver start webコマンドを使用してモジュールを再起動します。</td>
</tr>
<tr>
<td>セキュリティゾーンの一般的な設定を確認します。</td>
<td>セキュリティゾーンの設定について詳しくは、<a href="https://experienceleague.adobe.com/docs/campaign-classic/using/installing-campaign-classic/additional-configurations/configuring-campaign-server.html?lang=en#configuring-campaign-server"/>この節を参照してください。</a></td>
</tr>
<tr>
<td>コマンドnlserver pdumpは、<b>タスク</b>を返しません</td>
<td>Adobe Campaignアプリケーション全体を再起動する必要があります。 これを行うには、次のコマンドを使用します。<b>nlserver watchdog -svc -noconsole</b></td>
</tr>
</tbody> 
</table>
