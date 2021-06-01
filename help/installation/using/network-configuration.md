---
product: campaign
title: ネットワーク設定
description: システム通信のガイドラインを学ぶ
audience: installation
content-type: reference
topic-tags: prerequisites-and-recommendations-
exl-id: b86236ae-95e9-4406-b60f-6d90ad0d4a01
source-git-commit: 98d646919fedc66ee9145522ad0c5f15b25dbf2e
workflow-type: tm+mt
source-wordcount: '666'
ht-degree: 5%

---

# ネットワーク設定{#network-configuration}

## プロセス間の通信{#communication-between-processes}

アプリケーションの特定のプロセスは、他のユーザーと通信したり、LANやインターネットにアクセスしたりする必要があります。 これは、これらのプロセスに対して一部のTCPポートを開く必要があることを意味します。

Adobe Campaignプラットフォームの様々なアプリケーションサーバー間での内部通信には、埋め込みのApache Tomcatポートを優先（デフォルトでは8080）として使用します。

### 配信サーバー{#delivery-server}

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
   <td> <br /> </td> 
   <td> 電子メールブロードキャスト用のSMTPトラフィック。<br /> </td> 
  </tr> 
  <tr> 
   <td> 53/udp (domain)<br /> </td> 
   <td> DNSサーバ<br /> </td> 
   <td> DNSクエリ<br /> </td> 
  </tr> 
  <tr> 
   <td> 38000/tcp（デフォルトポート）<br /> </td> 
   <td> SMSゲートウェイ<br /> </td> 
   <td> SMSトラフィックをNetSize SMSルーターに送信するために使用します[option].<br /> </td> 
  </tr> 
  <tr> 
   <td> 7777/udp<br /> </td> 
   <td> 統計サーバ<br /> </td> 
   <td> 統計サーバにアクセスします。<br /> </td> 
  </tr> 
 </tbody> 
</table>

### 受信メール{#inbound-mail}

受信メールの回復プロセス(**nlserver inMail**)の場合、次のポートを開く必要があります。

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
   <td> バウンスメッセージを受け取るPOP3トラフィック。<br /> </td> 
  </tr> 
  <tr> 
   <td> 25/tcp (smtp)<br /> </td> 
   <td> 内部メールサーバ<br /> </td> 
   <td> 事前に定義されたルールで自動的に処理されない残りのバウンスメッセージを送信するSMTPトラフィック。<br /> </td> 
  </tr> 
 </tbody> 
</table>

### アプリケーションサーバー {#application-server}

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
   <td> <br /> </td> 
   <td> HTTPまたはHTTPSトラフィック（配信品質オファーを含む）。<br /> </td> 
  </tr> 
 </tbody> 
</table>

Adobe Campaignプラットフォームの複数のアプリケーションサーバーが相互に通信する必要がある場合は、Apache Tomcatサーバーのポートを使用することをお勧めします(デフォルトでは、8080)を返します。 これは、これらのサーバー間でポートを開く必要があることを意味します。

### SMS配信ステータス{#sms-delivery-status}

SMS配信(**nlserver sms**)を追跡するには、次のポートを開く必要があります。

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
   <td> NetSize SMSゲートウェイによって管理される配信キューの状態を問い合わせます[option].<br /> </td> 
  </tr> 
 </tbody> 
</table>

### リッチクライアント{#rich-client}

Adobe Campaignリッチクライアント(**nlclient**)の場合は、次のポートを開く必要があります。

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
   <td> SOAPトラフィック(HTTP).<br /> </td> 
  </tr> 
 </tbody> 
</table>

## データベースアクセス{#database-access}

データベースを使用するすべてのコンポーネントが、データベースに接続できる必要があります。 これは、単独で動作するリダイレクションサーバと、アプリケーションサーバとの通信にHTTP（またはHTTPS）のみを使用するシンWin32クライアントを除く、ほとんどのコンポーネントに当てはまります。

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

## 外部アクセス{#external-access}

また、Adobe Campaignから直接実行される電子メールキャンペーンを表示できるよう、パブリックインターネットから特定のコンポーネントにアクセスできる必要があります。 これは、コンポーネントに対して一部のポートを開く必要があることを意味します。

### リダイレクションサーバー{#redirection-server}

<table> 
 <tbody> 
  <tr> 
   <td> リスニングポート<br /> </td> 
   <td> 場所<br /> </td> 
  </tr> 
  <tr> 
   <td><p> 80/tcp (http)</p><p> 443/tcp (https)</p><br /> </td> 
   <td> どこでも。 追跡されたリンクをクリックするたびに、サーバー上でHTTPリクエストが生成されます。<br /> </td> 
  </tr> 
 </tbody> 
</table>

### 外部Webサーバー{#external-web-server}

このサーバーは、Webフォームやミラーページなどをホストします。 次のポートを開く必要があります。

<table> 
 <tbody> 
  <tr> 
   <td> リスニングポート<br /> </td> 
   <td> 場所<br /> </td> 
  </tr> 
  <tr> 
   <td><p> 80/tcp (http)</p><p> 443/tcp (https)</p><br /> </td> 
   <td> どこでも。 WebフォームをAdobe Campaignプラットフォームから直接管理する場合、またはミラーページを使用する場合に必要です。<br /> </td> 
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
   <td><p> 80/tcp (http)</p><p> 443/tcp (https)</p><br /> </td> 
   <td> シンクライアントまたはリッチクライアントを実行しているすべてのコンピュータ。<br /> </td> 
  </tr> 
 </tbody> 
</table>

## Adobe Experience Managerとの統合{#integration-with-adobe-experience-manager}

Adobe CampaignとAdobe Experience Managerの統合では、インストールが「オンプレミス」の場合は、複数のポートを開く必要があります。 この統合の設定について詳しくは、[詳細ドキュメント](../../integrations/using/about-adobe-experience-manager.md)を参照してください。

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
   <td> AEMの「オーサリング」および「パブリッシュ」インスタンスへのAdobe Campaign接続 開くポートは、AEMの設定によっては、デフォルトのポートと異なる場合があります。<br /> </td> 
  </tr> 
 </tbody> 
</table>

## 帯域幅 {#bandwidth}

考慮するネットワーク設定の別のキーパラメーター。 メール放送の間、ほとんど常にアウトバウンドで、多くの需要があります。 以下に、アドビの経験に基づく設定の例をいくつか示します。

* 1 MB/秒：1時間あたり10,000通のEメール（平均サイズは30 KB）
* 1時間あたり100,000通の電子メールに対して8～10 Mb/秒（平均サイズは30 Kb）

帯域幅に制約がある場合は、需要が低い夜の間にキャンペーンを実行するようにスケジュールできます。
