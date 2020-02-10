---
title: ネットワーク構成
seo-title: ネットワーク構成
description: ネットワーク構成
seo-description: null
page-status-flag: never-activated
uuid: 17357170-7440-4603-bea6-2e4b9086ae72
contentOwner: sauviat
products: SG_CAMPAIGN/CLASSIC
audience: installation
content-type: reference
topic-tags: prerequisites-and-recommendations-
discoiquuid: 639d2f42-e397-4694-942c-b2b8ad94ce9c
index: y
internal: n
snippet: y
translation-type: tm+mt
source-git-commit: 46f5bfb41bfe9c938ac0ffa767ead3e47a32047d

---


# ネットワーク構成{#network-configuration}

## プロセス間の通信 {#communication-between-processes}

アプリケーションの特定のプロセスは、他のユーザーと通信したり、LANやインターネットにアクセスしたりする必要があります。 つまり、一部のTCPポートは、これらのプロセスで開く必要があります。

Adobe Campaignプラットフォームの様々なアプリケーションサーバー間での内部通信には、埋め込みApache tomcatポートを優先順位（デフォルトで8080）として使用します。

### 配信サーバー {#delivery-server}

配信サーバー(**nlserver mta**)の場合、次のポートを開く必要があります。

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
   <td> 電子メールブロードキャスト用のSMTPトラフィック。<br /> </td> 
  </tr> 
  <tr> 
   <td> 53/udp（ドメイン）<br /> </td> 
   <td> DNSサーバー<br /> </td> 
   <td> DNSクエリ。<br /> </td> 
  </tr> 
  <tr> 
   <td> 38000/tcp（デフォルトポート）<br /> </td> 
   <td> SMSゲートウェイ<br /> </td> 
   <td> SMSトラフィックをNetSize SMSルータに送信するために使用します。[option]<br /> </td> 
  </tr> 
  <tr> 
   <td> 7777/udp<br /> </td> 
   <td> 統計サーバ<br /> </td> 
   <td> 統計サーバーへのアクセス。<br /> </td> 
  </tr> 
 </tbody> 
</table>

### 受信メール {#inbound-mail}

受信メールリカバリプロセス(**nlserver inMail**)では、次のポートを開く必要があります。

<table> 
 <tbody> 
  <tr> 
   <td> ポート<br /> </td> 
   <td> 宛先<br /> </td> 
   <td> コメント<br /> </td> 
  </tr> 
  <tr> 
   <td> 110/tcp (pop3)<br /> </td> 
   <td> 内部メールサーバ<br /> </td> 
   <td> POP3トラフィックを使用してバウンスメッセージを取得します。<br /> </td> 
  </tr> 
  <tr> 
   <td> 25/tcp (smtp)<br /> </td> 
   <td> 内部メールサーバ<br /> </td> 
   <td> 事前定義されたルールで自動的に処理されない残りのバウンスメッセージを送信するSMTPトラフィック。<br /> </td> 
  </tr> 
 </tbody> 
</table>

### Application server {#application-server}

アプリケーションサーバー(**nlserver web**)の場合は、次のポートを開く必要があります。

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
   <td> HTTPまたはHTTPSトラフィック（配信品質オファーを含む）。<br /> </td> 
  </tr> 
 </tbody> 
</table>

Adobe Campaignプラットフォームの複数のアプリケーションサーバーが相互に通信する必要がある場合は、Apache tomcatサーバーのポートを使用することをお勧めします(デフォルトでは、8080)を、リダイレクトモジュール統合が実行されたWebサーバーのHTTPポートの代わりに使用します。 つまり、これらのサーバ間でポートを開く必要があります。

### SMS配信状態 {#sms-delivery-status}

SMS配信(nlserver sms ****)を追跡するには、次のポートが開いている必要があります。

<table> 
 <tbody> 
  <tr> 
   <td> ポート<br /> </td> 
   <td> 宛先<br /> </td> 
   <td> コメント<br /> </td> 
  </tr> 
  <tr> 
   <td> 38000/tcp（デフォルトポート）<br /> </td> 
   <td> SMSゲートウェイ<br /> </td> 
   <td> NetSize SMSゲートウェイ[option]で管理される配信キューの状態をクエリします。<br /> </td> 
  </tr> 
 </tbody> 
</table>

### リッチクライアント {#rich-client}

Adobe Campaignリッチクライアント(**nlclient**)の場合は、次のポートを開く必要があります。

<table> 
 <tbody> 
  <tr> 
   <td> ポート<br /> </td> 
   <td> 宛先<br /> </td> 
   <td> コメント<br /> </td> 
  </tr> 
  <tr> 
   <td><p> 80/tcp (http)</p><p>443/tcp(https)</p><br /> </td> 
   <td> Application server<br /> </td> 
   <td> SOAPトラフィック(HTTP)。<br /> </td> 
  </tr> 
 </tbody> 
</table>

## データベースアクセス {#database-access}

データベースを使用するすべてのコンポーネントがデータベースに接続できる必要があります。 これは、単独で動作するリダイレクションサーバーと、アプリケーションサーバーとの通信にHTTP（またはHTTPS）のみを使用するシンWin32クライアントを除く、ほとんどのコンポーネントの場合です。

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

また、Adobe Campaignから直接実行される電子メールキャンペーンを表示できるように、一部のコンポーネントはパブリックインターネットからアクセスできる必要があります。 つまり、一部のポートをコンポーネント用に開く必要があります。

### リダイレクトサーバー {#redirection-server}

<table> 
 <tbody> 
  <tr> 
   <td> リスニングポート<br /> </td> 
   <td> 場所<br /> </td> 
  </tr> 
  <tr> 
   <td><p> 80/tcp (http)</p><p> 443/tcp(https)</p><br /> </td> 
   <td> どこでも。 トラッキング対象リンクをクリックするたびに、サーバー上でHTTPリクエストが生成されます。<br /> </td> 
  </tr> 
 </tbody> 
</table>

### 外部Webサーバー {#external-web-server}

このサーバーは、Webフォーム、ミラーページなどをホストします。 次のポートを開く必要があります。

<table> 
 <tbody> 
  <tr> 
   <td> リスニングポート<br /> </td> 
   <td> 場所<br /> </td> 
  </tr> 
  <tr> 
   <td><p> 80/tcp (http)</p><p> 443/tcp(https)</p><br /> </td> 
   <td> どこでも。 WebフォームがAdobe Campaignプラットフォームから直接管理される場合や、ミラーページが使用される場合に必要です。<br /> </td> 
  </tr> 
 </tbody> 
</table>

### 内部アプリケーションサーバー(Web) {#internal-application-server--web-}

<table> 
 <tbody> 
  <tr> 
   <td> リスニングポート<br /> </td> 
   <td> 場所<br /> </td> 
  </tr> 
  <tr> 
   <td><p> 80/tcp (http)</p><p> 443/tcp(https)</p><br /> </td> 
   <td> シンクライアントまたはリッチクライアントを実行するすべてのコンピュータ。<br /> </td> 
  </tr> 
 </tbody> 
</table>

## Adobe Experience Managerとの統合 {#integration-with-adobe-experience-manager}

Adobe CampaignとAdobe Experience Managerの統合では、インストールが「オンプレミス」の場合、複数のポートを開く必要があります。 この統合の設定について詳しくは、詳細なドキュメントを参照 [してください](../../integrations/using/about-adobe-experience-manager.md)。

<table> 
 <tbody> 
  <tr> 
   <td> リスニングポート<br /> </td> 
   <td> 説明<br /> </td> 
  </tr> 
  <tr> 
   <td> 80<br /> </td> 
   <td> Adobe CampaignへのAEM接続<br /> </td> 
  </tr> 
  <tr> 
   <td><p> 4502</p><p> 4503</p><br /> </td> 
   <td> AEMの「オーサリング」インスタンスと「発行」インスタンスへのAdobe Campaignの接続。 開くポートは、AEMの設定に応じて、デフォルトのポートと異なる場合があります。<br /> </td> 
  </tr> 
 </tbody> 
</table>

## 帯域幅 {#bandwidth}

考慮するネットワーク構成の別のキーパラメーター。 ほとんどの場合、送信され、電子メールのブロードキャスト中は需要が多くなります。 以下に、当社の経験に基づく設定の例を示します。

* 1時間あたり10,000件のメールに対して1 Mb/秒（平均サイズ30 Kb）
* 1時間あたり100,000通のメールに対して8～10 Mb/秒（平均サイズ30 Kb）

帯域幅に制約がある場合は、需要が低い夜にキャンペーンを実行するようにスケジュールできます。
