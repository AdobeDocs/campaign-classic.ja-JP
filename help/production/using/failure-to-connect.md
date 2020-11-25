---
solution: Campaign Classic
product: campaign
title: 接続の失敗
description: 接続の失敗
audience: production
content-type: reference
topic-tags: troubleshooting
translation-type: tm+mt
source-git-commit: 68fee697b65b2ba69f456803e0a7cebca9be3760
workflow-type: tm+mt
source-wordcount: '337'
ht-degree: 2%

---


# 接続の失敗{#failure-to-connect}

接続の問題の原因は複数の場合があり、様々なコンテキストに応じて異なります。

次のテストを試してみてください。接続の失敗が引き続き発生する場合は、 **Adobe Campaignサポートに問い合わせてください**。



<table> 
 <thead> 
  <tr> 
   <th>チェック<br /> </th> 
   <th>解決策<br /> </th> 
  </tr> 
 </thead> 
 <tbody> 
  <tr> 
   <td>コンピューターからインターネットにアクセスできますか。</td> 
   <td>インターネット上のWebサイトに接続できることを確認します（例）。 接続できない場合は、コンピューターに問題があります。 システム管理者に問い合わせてください。</td>
  </tr>
  <tr> 
   <td>別のサービスを介してサーバーホスティングAdobe Campaignに接続できますか。</td> 
   <td>SSHまたは他の方法でサーバーに接続します。 これが不可能な場合は、ホスト会社に問題があります。 システム管理者に問い合わせてください。</td>
  </tr>
  <tr> 
   <td>Webサーバーは応答しますか。</td> 
   <td>Webブラウザーを使用してAdobe CampaignサーバーのアクセスURLに接続します。 <b>http(s):// &lt;urlserver&gt;</b>. 応答しない場合、Webサーバーはマシン上で停止します。 サービスを再起動するには、ホスト会社のシステム管理者に問い合わせてください。</td>
  </tr>
  <tr> 
   <td>Adobe Campaignは正しく統合されているか。</td> 
   <td>次の場所にログオンします。 <b>http(s)://&lt;urlserver&gt;/r/test</b> URL。 サーバーは、次の種類のメッセージを返す必要があります。&lt;redir status='OK' date='YYYY/MM/DD HH:MM:SS' build='XXXX' host='&lt;hostname&gt;' localHost='&lt;server&gt;'/&gt;この結果を得ない場合は、統合を考慮したWebサーバーの設定を確認してください。</td>
  </tr>
  <tr> 
   <td>次のURLに接続します。 <b>http(s)://&lt;URLSERVER&gt;/nl/jsp/logon.jsp</b></td>
   <td>Tomcat Javaエラーが発生した場合は、JAVA統合が正しく実行されているかどうかを確認します。 It is integrated in the file [path of application]/nl6/customer.sh</td>
  </tr>
  <tr> 
   <td>次のURLに接続します。 <b>http(s)://&lt;URLSERVER&gt;/nl/jsp/logon.jsp</b></td>
   <td>空白のページが取得された場合は、Adobe CampaignWebモジュールが起動しているかどうかを確認します。 nlserver pdumpコマンドは、DD/MM/YYYYのAdobe Campaign Classic(7.X YY.R build XXX@SHA1)のアプリケーションサーバーを返す必要があります。 そうでない場合は、コマンドnlserver開始Webを使用してモジュールを再起動します</td>
  </tr>
   <tr>
  	<td>セキュリティゾーンの一般的な構成を確認します。</td>
  	<td>セキュリティゾーンの構成について詳しくは、[this section](../../installation/using/configuring-campaign-server.md#defining-security-zones)を参照してください。</td>
  </tr>
 </tbody> 
</table>
