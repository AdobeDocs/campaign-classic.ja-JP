---
product: campaign
title: ネットワーク設定
description: システム通信のガイドラインを学ぶ
feature: Installation, Instance Settings
badge-v7-prem: label="オンプレミス/ハイブリッドのみ" type="Caution" url="https://experienceleague.adobe.com/docs/campaign-classic/using/installing-campaign-classic/architecture-and-hosting-models/hosting-models-lp/hosting-models.html?lang=ja" tooltip="オンプレミスデプロイメントとハイブリッドデプロイメントにのみ適用されます"
audience: installation
content-type: reference
topic-tags: prerequisites-and-recommendations-
exl-id: b86236ae-95e9-4406-b60f-6d90ad0d4a01
source-git-commit: 14ba450ebff9bba6a36c0df07d715b7279604222
workflow-type: tm+mt
source-wordcount: '707'
ht-degree: 2%

---

# ネットワーク設定{#network-configuration}



## プロセス間の通信 {#communication-between-processes}

アプリケーションの特定のプロセスは、他の人と通信するか、LAN とインターネットにアクセスする必要があります。 つまり、これらのプロセスでは、一部の TCP ポートを開く必要があります。

Adobe Campaign プラットフォームの様々なアプリケーションサーバー間での内部通信には、埋め込み Apache Tomcat ポートを優先度（デフォルトは 8080）として使用します。

### 配信サーバー {#delivery-server}

配信サーバー（**nlserver mta**）、次のポートが開いている必要があります。

<table> 
 <tbody> 
  <tr> 
   <td> ポート<br /> </td> 
   <td> 宛先<br /> </td> 
   <td> コメント<br /> </td> 
  </tr> 
  <tr> 
   <td> 25/tcp （smtp）<br /> </td> 
   <td> どこでも<br /> </td> 
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
   <td> NetSize SMS ルータに SMS トラフィックを送信するために使用されます [ オプション ]。<br /> </td> 
  </tr> 
  <tr> 
   <td> 7777/udp<br /> </td> 
   <td> 統計サーバー<br /> </td> 
   <td> 統計サーバーにアクセスしています。<br /> </td> 
  </tr> 
 </tbody> 
</table>

### 受信メール {#inbound-mail}

受信メール回復プロセス（**nlserver inMail**）、次のポートが開いている必要があります。

<table> 
 <tbody> 
  <tr> 
   <td> ポート<br /> </td> 
   <td> 宛先<br /> </td> 
   <td> コメント<br /> </td> 
  </tr> 
  <tr> 
   <td> 110/tcp （pop3）<br /> </td> 
   <td> 内部メールサーバー<br /> </td> 
   <td> バウンスメッセージを取得するための POP3 トラフィック。<br /> </td> 
  </tr> 
  <tr> 
   <td> 25/tcp （smtp）<br /> </td> 
   <td> 内部メールサーバー<br /> </td> 
   <td> 事前定義済みのルールによって自動的に処理されない残りのバウンスメッセージを送信するための SMTP トラフィック。<br /> </td> 
  </tr> 
 </tbody> 
</table>

### アプリケーションサーバー {#application-server}

アプリケーションサーバー（**nlserver web**）、次のポートが開いている必要があります。

<table> 
 <tbody> 
  <tr> 
   <td> ポート<br /> </td> 
   <td> 宛先<br /> </td> 
   <td> コメント<br /> </td> 
  </tr> 
  <tr> 
   <td> 80/tcp （http）<br /> 443/tcp （https）<br /> </td> 
   <td> どこでも<br /> </td> 
   <td> HTTP または HTTPS トラフィック（配信品質オファーを含む）。<br /> </td> 
  </tr> 
 </tbody> 
</table>

Adobe Campaign プラットフォームの複数のアプリケーションサーバーが相互に通信する必要がある場合、リダイレクトモジュール統合が実行された web サーバーの HTTP ポートではなく、Apache Tomcat サーバーのポート（デフォルトは 8080）を使用することをお勧めします。 つまり、これらのサーバー間でポートを開く必要があります。

### SMS 配信ステータス {#sms-delivery-status}

SMS 配信をトラッキングするには、次を行います（**nlserver sms**）、次のポートが開いている必要があります。

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
   <td> NetSize SMS ゲートウェイによって管理される配信キューステータスを照会します [ オプション ]。<br /> </td> 
  </tr> 
 </tbody> 
</table>

### リッチクライアント {#rich-client}

Adobe Campaign リッチクライアント （**nlclient**）、次のポートが開いている必要があります。

<table> 
 <tbody> 
  <tr> 
   <td> ポート<br /> </td> 
   <td> 宛先<br /> </td> 
   <td> コメント<br /> </td> 
  </tr> 
  <tr> 
   <td><p> 80/tcp （http）</p><p>443/tcp （https）</p><br /> </td> 
   <td> アプリケーションサーバー<br /> </td> 
   <td> SOAP トラフィック（HTTP）。<br /> </td> 
  </tr> 
 </tbody> 
</table>

## データベースアクセス {#database-access}

データベースを使用するすべてのコンポーネントが、データベースに接続できる必要があります。 これは、単独で動作できるリダイレクトサーバーと、アプリケーションサーバーとの通信にのみ HTTP （または HTTPS）を使用するシン Win32 クライアントを除いて、ほとんどのコンポーネントの場合です。

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

さらに、特定のコンポーネントは、Adobe Campaignから直接実行されたメールキャンペーンを表示できるように、パブリックインターネットからアクセスできる必要があります。 つまり、コンポーネントに対して一部のポートを開く必要があります。

### リダイレクトサーバー {#redirection-server}

<table> 
 <tbody> 
  <tr> 
   <td> リスニングポート<br /> </td> 
   <td> 場所<br /> </td> 
  </tr> 
  <tr> 
   <td><p> 80/tcp （http）</p><p> 443/tcp （https）</p><br /> </td> 
   <td> どこでも。 トラッキングされるリンクをクリックするたびに、サーバー上で HTTP リクエストが生成されます。<br /> </td> 
  </tr> 
 </tbody> 
</table>

### 外部 Web サーバー {#external-web-server}

このサーバーは、Web フォーム、ミラーページなどをホストします。 次のポートを開く必要があります。

<table> 
 <tbody> 
  <tr> 
   <td> リスニングポート<br /> </td> 
   <td> 場所<br /> </td> 
  </tr> 
  <tr> 
   <td><p> 80/tcp （http）</p><p> 443/tcp （https）</p><br /> </td> 
   <td> どこでも。 Web フォームがAdobe Campaign プラットフォームから直接管理される場合、またはミラーページが使用される場合に必要です。<br /> </td> 
  </tr> 
 </tbody> 
</table>

### 内部アプリケーションサーバー（Web） {#internal-application-server--web-}

<table> 
 <tbody> 
  <tr> 
   <td> リスニングポート<br /> </td> 
   <td> 場所<br /> </td> 
  </tr> 
  <tr> 
   <td><p> 80/tcp （http）</p><p> 443/tcp （https）</p><br /> </td> 
   <td> シンクライアントまたはリッチクライアントを実行するすべてのコンピュータ。<br /> </td> 
  </tr> 
 </tbody> 
</table>

## Adobe Experience Managerとの統合 {#integration-with-adobe-experience-manager}

Adobe CampaignとAdobe Experience Managerの統合では、インストールが「オンプレミス」の場合、複数のポートを開く必要があります。 この統合の設定について詳しくは、 [詳細ドキュメント](../../integrations/using/about-adobe-experience-manager.md).

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
   <td> AEMの「オーサリング」インスタンスと「パブリッシング」インスタンスへのAdobe Campaign接続。 開くポートは、AEMの設定に応じて、デフォルトのポートとは異なる場合があります。<br /> </td> 
  </tr> 
 </tbody> 
</table>

## 帯域幅 {#bandwidth}

考慮するネットワーク設定の別のキーパラメーター。 ほとんどの場合、メール配信中のアウトバウンドおよび需要が高まります。 アドビの経験に基づいた設定の例を以下に示します。

* 1 時間あたり 10,000 通のメールで 1 Mb/秒（平均サイズは 30 Kb）
* 1 時間あたり 100,000 通のメールに対して 8 ～ 10 Mb/秒（平均サイズ 30 Kb）

帯域幅の面で制約がある場合は、需要が低い夜にキャンペーンを実行するようにスケジュールできます。
