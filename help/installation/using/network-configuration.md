---
product: campaign
title: ネットワーク設定
description: システム通信のガイドラインを学ぶ
feature: Installation, Instance Settings
badge-v7-only: label="v7" type="Informative" tooltip="Campaign Classic v7 にのみ適用されます"
badge-v7-prem: label="オンプレミスおよびハイブリッド" type="Caution" url="https://experienceleague.adobe.com/docs/campaign-classic/using/installing-campaign-classic/architecture-and-hosting-models/hosting-models-lp/hosting-models.html?lang=ja" tooltip="オンプレミスデプロイメントとハイブリッドデプロイメントにのみ適用されます"
audience: installation
content-type: reference
topic-tags: prerequisites-and-recommendations-
exl-id: b86236ae-95e9-4406-b60f-6d90ad0d4a01
source-git-commit: 3a9b21d626b60754789c3f594ba798309f62a553
workflow-type: tm+mt
source-wordcount: '691'
ht-degree: 8%

---

# ネットワーク設定{#network-configuration}



## プロセス間の通信 {#communication-between-processes}

アプリケーションの特定のプロセスは、他のユーザーと通信したり、LAN やインターネットにアクセスしたりする必要があります。 つまり、これらのプロセスでは、一部の TCP ポートを開く必要があります。

Adobe Campaignプラットフォームの様々なアプリケーションサーバー間の内部通信には、埋め込みの Apache Tomcat ポートを優先（デフォルトでは 8080）として使用します。

### 配信サーバー {#delivery-server}

配信サーバー (**nlserver mta**) の場合は、次のポートを開く必要があります。

<table> 
 <tbody> 
  <tr> 
   <td> ポート<br /> </td> 
   <td> 宛先<br /> </td> 
   <td> コメント<br /> </td> 
  </tr> 
  <tr> 
   <td> 25/tcp (smtp)<br /> </td> 
   <td> 任意の場所<br /> </td> 
   <td> E メールブロードキャスト用の SMTP トラフィック。<br /> </td> 
  </tr> 
  <tr> 
   <td> 53/udp （ドメイン）<br /> </td> 
   <td> DNS サーバー<br /> </td> 
   <td> DNS クエリ。<br /> </td> 
  </tr> 
  <tr> 
   <td> 38000/tcp （デフォルトポート）<br /> </td> 
   <td> SMS ゲートウェイ<br /> </td> 
   <td> SMS トラフィックを NetSize SMS ルーターに送信するために使用します [option]。<br /> </td> 
  </tr> 
  <tr> 
   <td> 7777/udp<br /> </td> 
   <td> 統計サーバー<br /> </td> 
   <td> 統計サーバーにアクセスします。<br /> </td> 
  </tr> 
 </tbody> 
</table>

### インバウンドメール {#inbound-mail}

インバウンドメールの回復プロセス (**nlserver inMail**) の場合は、次のポートを開く必要があります。

<table> 
 <tbody> 
  <tr> 
   <td> ポート<br /> </td> 
   <td> 宛先<br /> </td> 
   <td> コメント<br /> </td> 
  </tr> 
  <tr> 
   <td> 110/tcp (pop3)<br /> </td> 
   <td> 内部メールサーバー<br /> </td> 
   <td> バウンスメッセージを取得する POP3 トラフィック。<br /> </td> 
  </tr> 
  <tr> 
   <td> 25/tcp (smtp)<br /> </td> 
   <td> 内部メールサーバー<br /> </td> 
   <td> 事前定義されたルールで自動的に処理されない残りのバウンスメッセージを送信する SMTP トラフィック。<br /> </td> 
  </tr> 
 </tbody> 
</table>

### アプリケーションサーバー {#application-server}

アプリケーションサーバーの場合 (**nlserver web**) の場合は、次のポートを開く必要があります。

<table> 
 <tbody> 
  <tr> 
   <td> ポート<br /> </td> 
   <td> 宛先<br /> </td> 
   <td> コメント<br /> </td> 
  </tr> 
  <tr> 
   <td> 80/tcp (http)<br /> 443/tcp (https)<br /> </td> 
   <td> 任意の場所<br /> </td> 
   <td> HTTP または HTTPS トラフィック（配信品質オファーを含む）。<br /> </td> 
  </tr> 
 </tbody> 
</table>

Adobe Campaignプラットフォームの複数のアプリケーションサーバーが相互に通信する必要がある場合は、リダイレクトモジュール統合が実行された Web サーバーの HTTP ポートではなく、Apache Tomcat サーバーのポート（デフォルトでは 8080）を使用することをお勧めします。 これは、これらのサーバー間でポートを開く必要があることを意味します。

### SMS 配信ステータス {#sms-delivery-status}

SMS 配信を追跡するには、以下を実行します (**nlserver sms**) の場合は、次のポートを開く必要があります。

<table> 
 <tbody> 
  <tr> 
   <td> ポート<br /> </td> 
   <td> 宛先<br /> </td> 
   <td> コメント<br /> </td> 
  </tr> 
  <tr> 
   <td> 38000/tcp （デフォルトポート）<br /> </td> 
   <td> SMS ゲートウェイ<br /> </td> 
   <td> NetSize SMS ゲートウェイ [option] で管理される配信キューのステータスを問い合わせます。<br /> </td> 
  </tr> 
 </tbody> 
</table>

### リッチクライアント {#rich-client}

Adobe Campaignリッチクライアントの場合 (**nlclient**) の場合は、次のポートを開く必要があります。

<table> 
 <tbody> 
  <tr> 
   <td> ポート<br /> </td> 
   <td> 宛先<br /> </td> 
   <td> コメント<br /> </td> 
  </tr> 
  <tr> 
   <td><p> 80/tcp (http)</p><p>443/tcp (https)</p><br /> </td> 
   <td> アプリケーションサーバー<br /> </td> 
   <td> SOAP トラフィック (HTTP)。<br /> </td> 
  </tr> 
 </tbody> 
</table>

## データベースアクセス {#database-access}

データベースを使用するすべてのコンポーネントが、データベースに接続できる必要があります。 これは、ほとんどのコンポーネントに当てはまります。ただし、単独で動作するリダイレクションサーバーと、アプリケーションサーバーとの通信に HTTP（または HTTPS）のみを使用するシン Win32 クライアントを除きます。

デフォルトのポートは次のとおりです。

<table> 
 <tbody> 
  <tr> 
   <td> データベースタイプ<br /> </td> 
   <td> ポート（デフォルト）<br /> </td> 
   <td> 宛先<br /> </td> 
  </tr> 
  <tr> 
   <td> <strong>Oracle</strong><br /> </td> 
   <td> 1521/tcp<br /> </td> 
   <td> データベースサーバー<br /> </td> 
  </tr> 
  <tr> 
   <td> <strong>PostgreSQL</strong><br /> </td> 
   <td> 5432/tcp<br /> </td> 
  </tr> 
  <tr> 
   <td> <strong>Microsoft SQL Server</strong><br /> </td> 
   <td> 1433/tcp<br /> </td> 
  </tr> 
  <tr> 
   <td> <strong>DB2</strong><br /> </td> 
   <td> 50000/tcp<br /> </td> 
  </tr> 
 </tbody> 
</table>

## 外部アクセス {#external-access}

また、Adobe Campaignから直接実行された E メールキャンペーンを表示できるよう、パブリックインターネットから特定のコンポーネントにアクセスできる必要があります。 つまり、コンポーネントの一部のポートを開く必要があります。

### リダイレクトサーバー {#redirection-server}

<table> 
 <tbody> 
  <tr> 
   <td> リスニングポート<br /> </td> 
   <td> 場所<br /> </td> 
  </tr> 
  <tr> 
   <td><p> 80/tcp (http)</p><p> 443/tcp (https)</p><br /> </td> 
   <td> どこでも。 追跡対象のリンクをクリックするたびに、サーバー上で HTTP リクエストが生成されます。<br /> </td> 
  </tr> 
 </tbody> 
</table>

### 外部 Web サーバー {#external-web-server}

このサーバーは、Web フォームやミラーページなどをホストします。 次のポートを開く必要があります。

<table> 
 <tbody> 
  <tr> 
   <td> リスニングポート<br /> </td> 
   <td> 場所<br /> </td> 
  </tr> 
  <tr> 
   <td><p> 80/tcp (http)</p><p> 443/tcp (https)</p><br /> </td> 
   <td> どこでも。 Web フォームをAdobe Campaignプラットフォームから直接管理する場合、またはミラーページを使用する場合に必要です。<br /> </td> 
  </tr> 
 </tbody> 
</table>

### 内部アプリケーションサーバー (Web) {#internal-application-server--web-}

<table> 
 <tbody> 
  <tr> 
   <td> リスニングポート<br /> </td> 
   <td> 場所<br /> </td> 
  </tr> 
  <tr> 
   <td><p> 80/tcp (http)</p><p> 443/tcp (https)</p><br /> </td> 
   <td> シンクライアントまたはリッチクライアントを実行しているすべてのコンピュータ。<br /> </td> 
  </tr> 
 </tbody> 
</table>

## Adobe Experience Managerとの統合 {#integration-with-adobe-experience-manager}

Adobe CampaignとAdobe Experience Managerの統合では、インストールが「オンプレミス」の場合は、複数のポートを開く必要があります。 この統合の設定について詳しくは、 [詳細なドキュメント](../../integrations/using/about-adobe-experience-manager.md).

<table> 
 <tbody> 
  <tr> 
   <td> リスニングポート<br /> </td> 
   <td> 説明<br /> </td> 
  </tr> 
  <tr> 
   <td> 80<br /> </td> 
   <td> Adobe CampaignとのAEM接続<br /> </td> 
  </tr> 
  <tr> 
   <td><p> 4502</p><p> 4503</p><br /> </td> 
   <td> AEMの「オーサリング」および「パブリッシュ」インスタンスへのAdobe Campaign接続 開くポートは、AEMの設定に応じて、デフォルトのポートとは異なる場合があります。<br /> </td> 
  </tr> 
 </tbody> 
</table>

## 帯域幅 {#bandwidth}

考慮するネットワーク設定の別のキーパラメーター。 E メール放送の間、ほとんど常にアウトバウンドで、多くの需要があります。 以下に、アドビの経験に基づく設定の例をいくつか示します。

* 1 時間あたり 10,000 通のメールに対して 1 MB/秒（平均サイズは 30 KB）
* 1 時間あたり 100,000 通のメールの場合は 8～10 Mb/秒（平均サイズは 30 Kb）

帯域幅に関して制約がある場合は、需要が低い夜にキャンペーンを実行するようにスケジュールを設定できます。
