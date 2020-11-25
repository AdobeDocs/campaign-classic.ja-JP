---
solution: Campaign Classic
product: campaign
title: 接続の失敗
description: 接続の失敗
audience: production
content-type: reference
topic-tags: troubleshooting
translation-type: tm+mt
source-git-commit: eb7e1c98f69ba20ef4222bfefea74fdaf6072397
workflow-type: tm+mt
source-wordcount: '349'
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
   <td>次の場所にログオンします。 <b>http(s)://&lt;urlserver&gt;/r/test</b> URL。 サーバーは、次の種類のメッセージを返す必要があります。

    &lt;pre>
    &lt;redir status=&#39;OK&#39; date=&#39;YYYY/MM/DD HH:MM:SS&#39; build=&#39;XXXX&#39; host=&#39;&lt;hostname>&#39; localHost=&#39;&lt;server>&#39;/>
    &lt;/pre>
    
    この結果を取得しない場合は、統合を考慮するWebサーバー設定を確認してください。&lt;/td>
</tr>
  <tr> 
   <td>Adobe CampaignWebモジュールが起動しているか。</td> 
   <td>
   次のURLに接続します。 <b>http(s)://&gt;URLSERVER&lt;/nl/jsp/logon.jsp</b>* Tomcat Javaエラーが発生した場合：

    JAVA統合は正しく実行されているか。 Adobe CampaignにはSUN JDKが必要です。
    
    It is integrated in the file [path of application]/nl6/customer.sh
    
    * If you oven a blank page:
    
    Has theAdobe CampaignWeb module starped up? DD/MM/YYYY
    
    [...]web@default (27515) - 55.2 Mb
    [...]
    のAdobe Campaign Classic(7.X YY.R build XXX@SHA1)の場合は、&lt;pre>
    
    
    
    
    
    
    
    
    
    
    nlserver pdumpHH:MM:SS > Application serverを入手する必要があります。/pre>開始*を使用しない場合は、次のコマンドを使用して再起動します。&lt;pre>pre> webのコマンドです。
</tr>
  <tr>
  	<td>セキュリティゾーンの一般的な構成を確認します。</td>
  	<td>セキュリティゾーンの構成について詳しくは、[this section](../../installation/using/configuring-campaign-server.md#defining-security-zones)を参照してください。</td>
  </tr>
 </tbody> 
</table>
