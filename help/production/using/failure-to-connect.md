---
product: campaign
title: 接続の失敗
description: 接続の失敗
badge-v7-only: label="v7" type="Informative" tooltip="Applies to Campaign Classic v7 only"
badge-v7-prem: label="on-premise & hybrid" type="Caution" url="https://experienceleague.adobe.com/docs/campaign-classic/using/installing-campaign-classic/architecture-and-hosting-models/hosting-models-lp/hosting-models.html" tooltip="Applies to on-premise and hybrid deployments only"
audience: production
content-type: reference
topic-tags: troubleshooting
exl-id: 3c793dc1-9654-4289-a3d2-30c3078fd848
source-git-commit: 4661688a22bd1a82eaf9c72a739b5a5ecee168b1
workflow-type: tm+mt
source-wordcount: '374'
ht-degree: 4%

---

# 接続の失敗{#failure-to-connect}



接続の問題の原因は複数の場合があり、様々なコンテキストによって異なります。

次のテストを試すことができます。接続の失敗が解決しない場合は、 [Adobeカスタマーケア](https://helpx.adobe.com/jp/enterprise/admin-guide.html/enterprise/using/support-for-experience-cloud.ug.html).



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
<td>インターネット上の Web サイトに接続できることを確認します（例： ）。 接続できない場合は、問題がコンピューター上に存在します。 システム管理者に問い合わせてください。</td>
</tr>
<tr> 
<td>別のサービスを介してAdobe Campaignをホストするサーバーに接続できますか？</td> 
<td>SSH などの方法でサーバーに接続します。 これが不可能な場合は、ホスト会社に問題があります。 システム管理者に問い合わせてください。</td>
</tr>
<tr> 
<td>Web サーバーは応答しますか？</td> 
<td>Web ブラウザーを使用してAdobe Campaignサーバーにアクセスする URL に接続します。 <b>http(s):// &lt;urlserver&gt;</b>. 応答しない場合、Web サーバーはマシン上で停止します。 サービスを再起動するには、ホスト会社のシステム管理者に問い合わせてください。</td>
</tr>
<tr> 
<td>Adobe Campaignは正しく統合されていますか？</td> 
<td>次の場所にログオンします。 <b>http(s)://&lt;urlserver&gt;/r/test</b> URL。 サーバーは、次のタイプのメッセージを返す必要があります。 &lt;redir status="OK" date="YYYY/MM/DD HH&lt;span id="0" translate="no"/&gt;SS" build="XXXX" host="&lt;hostname&gt;" localhost="&lt;server&gt;" /&gt;
この結果が得られない場合は、統合が考慮される Web サーバーの設定を確認します。:MM:</td>
</tr>
<tr> 
<td>次の URL に接続します。 <b>http(s)://&lt;urlserver&gt;/nl/jsp/logon.jsp</b></td>
<td>Tomcat Java エラーが発生した場合は、JAVA 統合が正しく実行されているかどうかを確認します。 ファイル [application のパス ]/nl6/customer.shに統合されています。</td>
</tr>
<tr> 
<td>次の URL に接続します。 <b>http(s)://&lt;urlserver&gt;/nl/jsp/logon.jsp</b></td>
<td>空白のページが取得された場合は、Adobe Campaign Web モジュールが起動しているかどうかを確認します。 コマンド nlserver pdump は、DD/MM/YYYY のAdobe Campaign Classic(7.X YY.R build XXX@SHA1) のアプリケーションサーバーを返す必要があります。 そうでない場合は、nlserver start web コマンドを使用してモジュールを再起動します</td>
</tr>
<tr>
<td>セキュリティゾーンの一般的な設定を確認します。</td>
<td>セキュリティゾーンの設定について詳しくは、 <a href="https://experienceleague.adobe.com/docs/campaign-classic/using/installing-campaign-classic/additional-configurations/configuring-campaign-server.html#configuring-campaign-server"/>この節を参照してください。</a></td>
</tr>
<tr>
<td>コマンド nlserver pdump が返す <b>タスクなし</b></td>
<td>Adobe Campaignアプリケーション全体を再起動する必要があります。 これをおこなうには、次のコマンドを使用します。 <b>nlserver watchdog -svc -noconsole</b></td>
</tr>
</tbody> 
</table>
