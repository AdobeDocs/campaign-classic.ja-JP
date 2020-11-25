---
solution: Campaign Classic
product: campaign
title: 接続の失敗
description: 接続の失敗
audience: production
content-type: reference
topic-tags: troubleshooting
translation-type: tm+mt
source-git-commit: cb6a2247e3b7617511aecf3d2d19985af0216494
workflow-type: tm+mt
source-wordcount: '340'
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
   <td>Webブラウザーを使用してAdobe CampaignサーバーのアクセスURLに接続します。**`http(s):// <urlserver>`**. 応答しない場合、Webサーバーはマシン上で停止します。 サービスを再起動するには、ホスト会社のシステム管理者に問い合わせてください。</td>
  </tr>
  <tr> 
   <td>Adobe Campaignは正しく統合されているか。</td> 
   <td>次の場所にログオンします。**`http(s)://<urlserver>/r/test`* URL サーバーは、次の種類のメッセージを返す必要があります

    &quot;
    &lt;redir status=&#39;OK&#39; date=&#39;YYYY/MM/DD HH:MM:SS&#39; build=&#39;XXXX&#39; host=&#39;&lt;hostname>&#39; localHost=&#39;&lt;server>&#39;/>
    &quot;
    
    この結果が得られない場合は、統合が考慮されるWebサーバーの設定を確認してください。&lt;/td>
</tr>
  <tr> 
   <td>Adobe CampaignWebモジュールが起動しているか。</td> 
   <td>
   次のURLに接続します。**`http(s)://<URLSERVER>/nl/jsp/logon.jsp`** * Tomcat Javaエラーが発生した場合：

    JAVA統合は正しく実行されているか。 Adobe CampaignにはSUN JDKが必要です。
    
    このIDは、**`[アプリケーションのパス]`/nl6/customer.sh**
    
    *空白のページを取得した場合：Adobe CampaignWebモジュール
    
    を起動しましたか？ DD/MM/YYYY
    
    [...]web@default (27515) - 55.2 Mb
    [...]
    &#39;&#39;のAdobe Campaign Classic(7.X YY.R build XXX@SHA1)の場合は、「nlserver
    
    
    
    
    
    
    
    
    
    pdumpHH:MM:SS > Application server for Application server (7. Y.X..........)」を取得する必要があります。そうでない場合は、次のコマンドを使用して再起動します。
</tr>
  <tr>
  	<td>セキュリティゾーンの一般的な構成を確認します。</td>
  	<td>セキュリティゾーンの構成について詳しくは、[this section](../../installation/using/configuring-campaign-server.md#defining-security-zones)を参照してください。</td>
  </tr>
 </tbody> 
</table>
