---
product: campaign
title: 接続の失敗
description: 接続の失敗
feature: Monitoring
badge-v7-prem: label="オンプレミスおよびハイブリッド" type="Caution" url="https://experienceleague.adobe.com/docs/campaign-classic/using/installing-campaign-classic/architecture-and-hosting-models/hosting-models-lp/hosting-models.html?lang=ja" tooltip="オンプレミスデプロイメントとハイブリッドデプロイメントにのみ適用されます"
audience: production
content-type: reference
topic-tags: troubleshooting
exl-id: 3c793dc1-9654-4289-a3d2-30c3078fd848
source-git-commit: b666535f7f82d1b8c2da4fbce1bc25cf8d39d187
workflow-type: tm+mt
source-wordcount: '370'
ht-degree: 5%

---

# 接続の失敗{#failure-to-connect}



接続の問題が発生する理由は複数あり、様々なコンテキストに依存します。

次のテストを試すことができます。接続エラーが解決しない場合は、 [Adobeカスタマーケア](https://helpx.adobe.com/jp/enterprise/admin-guide.html/enterprise/using/support-for-experience-cloud.ug.html).



<table> 
<thead> 
<tr> 
<th>チェック<br /> </th> 
<th>解決策<br /> </th> 
</tr> 
</thead> 
<tbody> 
<tr> 
<td>お使いのコンピューターからインターネットにアクセスできますか？</td> 
<td>インターネット上の Web サイト（例：）に接続できることを確認します。 接続できない場合は、問題はお使いのコンピューターにあります。 システム管理者にお問い合わせください。</td>
</tr>
<tr> 
<td>別のサービスを使用してAdobe Campaignをホストするサーバーに接続できますか？</td> 
<td>SSH またはその他の方法でサーバーに接続します。 これが不可能な場合は、ホスト会社に問題があります。 システム管理者にお問い合わせください。</td>
</tr>
<tr> 
<td>Web サーバーは応答しますか？</td> 
<td>Web ブラウザーを使用してAdobe Campaign サーバーのアクセス URL に接続します。 <b>http （s）:// &lt;urlserver&gt;</b>. 応答しない場合、web サーバーはマシン上で停止します。 サービスを再起動するには、ホスト会社のシステム管理者に問い合わせてください。</td>
</tr>
<tr> 
<td>Adobe Campaignは正しく統合されていますか？</td> 
<td>にログオンします。 <b>http （s）://&lt;urlserver&gt;/r/test</b> URL。 サーバーは次のタイプのメッセージを返します。 &lt;redir status="OK" date="YYYY/MM/DD HH&lt;span id="0" translate="no"/&gt;SS" build="XXXX" host="&lt;hostname&gt;" localhost="&lt;server&gt;" /&gt;
この結果が得られない場合は、統合が考慮されていることを web サーバー設定で確認します。:MM:</td>
</tr>
<tr> 
<td>次の URL に接続します。 <b>http （s）://&lt;urlserver&gt;/nl/jsp/logon.jsp</b></td>
<td>Tomcat Java エラーを取得した場合は、JAVA 統合が正しく実行されているかどうかを確認します。 ファイル [ アプリケーションのパス ]/nl6/customer.shに統合されています</td>
</tr>
<tr> 
<td>次の URL に接続します。 <b>http （s）://&lt;urlserver&gt;/nl/jsp/logon.jsp</b></td>
<td>空白のページが取得された場合は、Adobe Campaign web モジュールが起動しているかどうかを確認します。 コマンド nlserver pdump は、Adobe Campaign Classic（7.X YY.R ビルド XXX@SHA1）の DD/MM/YYYY のアプリケーションサーバーを返します。 そうでない場合は、nlserver start web コマンドでモジュールを再起動します。</td>
</tr>
<tr>
<td>セキュリティゾーンの一般的な設定を確認します。</td>
<td>セキュリティゾーンの設定について詳しくは、次を参照してください。 <a href="https://experienceleague.adobe.com/docs/campaign-classic/using/installing-campaign-classic/additional-configurations/configuring-campaign-server.html#configuring-campaign-server"/>この節。</a></td>
</tr>
<tr>
<td>nlserver pdump コマンドの戻り値 <b>タスクなし</b></td>
<td>Adobe Campaign アプリケーション全体を再起動する必要があります。 これを行うには、次のコマンドを使用します。 <b>nlserver watchdog -svc -noconsole</b></td>
</tr>
</tbody> 
</table>
