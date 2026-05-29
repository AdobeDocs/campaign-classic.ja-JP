---
product: campaign
title: ネットワーク設定
description: システムのコミュニケーションガイドラインを学ぶ
feature: Installation, Instance Settings
badge-v7-prem: label="オンプレミス／ハイブリッドのみ" type="Caution" url="https://experienceleague.adobe.com/docs/campaign-classic/using/installing-campaign-classic/architecture-and-hosting-models/hosting-models-lp/hosting-models.html?lang=ja" tooltip="オンプレミスデプロイメントとハイブリッドデプロイメントにのみ適用されます"
audience: installation
content-type: reference
topic-tags: prerequisites-and-recommendations-
exl-id: b86236ae-95e9-4406-b60f-6d90ad0d4a01
TQID: https://experienceleague.adobe.com/jynrfZrBNI6ergWQ2ONvI97Or1coFkVD-cLeaK14K70
product_v2:
  - id: dfc56824-e8b9-499e-85d4-21aedb507314
feature_v2: []
subfeature_v2: []
source-git-commit: bb41e9407ab5853b0194bb325bbf3f17bc3ea232
workflow-type: tm+mt
source-wordcount: 725
ht-degree: 5%

---

# ネットワーク設定{#network-configuration}



## プロセス間のコミュニケーション {#communication-between-processes}

アプリケーションの特定のプロセスは、他の人と通信したり、LANとインターネットにアクセスしたりする必要があります。 つまり、一部のTCP ポートは、これらのプロセスに対してオープンにする必要があります。

組み込みのApache Tomcat ポートを、Adobe Campaign プラットフォームの様々なアプリケーションサーバー間の内部通信の優先度（デフォルトでは8080）として使用します。

### 配信サーバー {#delivery-server}

配信サーバー（**nlserver mta**）の場合、次のポートを開く必要があります。

<table> 
 <tbody> 
  <tr> 
   <td> ポート <br /> </td> 
   <td> 宛先<br /> </td> 
   <td> コメント <br /> </td> 
  </tr> 
  <tr> 
   <td> 25/tcp （smtp） <br /> </td> 
   <td> どこでも<br /> </td> 
   <td> メール放送用SMTP トラフィック。<br /> </td> 
  </tr> 
  <tr> 
   <td> 53/udp （ドメイン） <br /> </td> 
   <td> DNS サーバー<br /> </td> 
   <td> DNS クエリ。<br /> </td> 
  </tr> 
  <tr> 
   <td> 38000/tcp （既定のポート） <br /> </td> 
   <td> SMS ゲートウェイ <br /> </td> 
   <td> NetSize SMS ルーターにSMS トラフィックを送信するために使用されます[ オプション ]。<br /> </td> 
  </tr> 
  <tr> 
   <td> 7777/udp<br /> </td> 
   <td> 統計サーバー<br /> </td> 
   <td> 統計サーバーにアクセスしています。<br /> </td> 
  </tr> 
 </tbody> 
</table>

### インバウンドメール {#inbound-mail}

受信メールの回復プロセス （**nlserver inMail**）の場合、次のポートを開く必要があります。

<table> 
 <tbody> 
  <tr> 
   <td> ポート <br /> </td> 
   <td> 宛先<br /> </td> 
   <td> コメント <br /> </td> 
  </tr> 
  <tr> 
   <td> 110/tcp （pop3） <br /> </td> 
   <td> 内部メール サーバー<br /> </td> 
   <td> バウンス メッセージをピックアップするPOP3 トラフィック。<br /> </td> 
  </tr> 
  <tr> 
   <td> 25/tcp （smtp） <br /> </td> 
   <td> 内部メール サーバー<br /> </td> 
   <td> 定義済みのルールによって自動的に処理されない残りのバウンス メッセージを送信するためのSMTP トラフィック。<br /> </td> 
  </tr> 
 </tbody> 
</table>

### アプリケーションサーバー {#application-server}

アプリケーションサーバー（**nlserver web**）の場合、次のポートを開く必要があります。

<table> 
 <tbody> 
  <tr> 
   <td> ポート <br /> </td> 
   <td> 宛先<br /> </td> 
   <td> コメント <br /> </td> 
  </tr> 
  <tr> 
   <td> 80/tcp （http） <br /> 443/tcp （https） <br /> </td> 
   <td> どこでも<br /> </td> 
   <td> HTTPまたはHTTPS トラフィック （配信品質オファーを含む）。<br /> </td> 
  </tr> 
 </tbody> 
</table>

Adobe Campaign プラットフォームの複数のアプリケーションサーバーが相互に通信する必要がある場合は、リダイレクトモジュールの統合が実行されたWeb サーバーのHTTP ポートではなく、Apache Tomcat サーバーのポート（デフォルトでは8080）を使用することをお勧めします。 つまり、これらのサーバー間でポートを開く必要があります。

### SMS配信ステータス {#sms-delivery-status}

SMS配信（**nlserver sms**）を追跡するには、次のポートを開く必要があります。

<table> 
 <tbody> 
  <tr> 
   <td> ポート <br /> </td> 
   <td> 宛先<br /> </td> 
   <td> コメント <br /> </td> 
  </tr> 
  <tr> 
   <td> 38000/tcp （既定のポート） <br /> </td> 
   <td> SMS ゲートウェイ <br /> </td> 
   <td> NetSize SMS ゲートウェイによって管理されている配信キューの状態をクエリします[ オプション ]。<br /> </td> 
  </tr> 
 </tbody> 
</table>

### リッチクライアント {#rich-client}

Adobe Campaign リッチ クライアント （**nlclient**）の場合、次のポートを開く必要があります。

<table> 
 <tbody> 
  <tr> 
   <td> ポート <br /> </td> 
   <td> 宛先<br /> </td> 
   <td> コメント <br /> </td> 
  </tr> 
  <tr> 
   <td><p> 80/tcp （http）</p><p>443/tcp （https）</p><br /> </td> 
   <td> アプリケーションサーバー<br /> </td> 
   <td> SOAP トラフィック （HTTP）。<br /> </td> 
  </tr> 
 </tbody> 
</table>

## データベースアクセス {#database-access}

データベースを使用するすべてのコンポーネントは、データベースに接続できる必要があります。 これは、ほとんどのコンポーネントで発生します。ただし、リダイレクトサーバーは単独で動作し、シン Win32 クライアントはHTTP （またはHTTPS）を使用してアプリケーションサーバーとのみ通信します。

デフォルトのポートは次のとおりです。

<table> 
 <tbody> 
  <tr> 
   <td> データベースの種類<br /> </td> 
   <td> ポート （既定値） <br /> </td> 
   <td> 宛先<br /> </td> 
  </tr> 
  <tr> 
   <td> <strong>Oracle</strong><br /> </td> 
   <td> 1521/tcp<br /> </td> 
   <td> データベース サーバー<br /> </td> 
  </tr> 
  <tr> 
   <td> <strong>PostgreSQL</strong><br /> </td> 
   <td> 5432/tcp<br /> </td> 
  </tr> 
  <tr> 
   <td> <strong>Microsoft SQL Server</strong><br /> </td> 
   <td> 1433/tcp<br /> </td> 
  </tr> 
 </tbody> 
</table>

## 外部アクセス {#external-access}

さらに、Adobe Campaignから直接実行されたメールキャンペーンを表示できるように、特定のコンポーネントにパブリックインターネットからアクセスできる必要があります。 つまり、一部のポートはコンポーネントに対して開く必要があります。

### リダイレクションサーバー {#redirection-server}

<table> 
 <tbody> 
  <tr> 
   <td> リスニング ポート <br /> </td> 
   <td> 場所<br /> </td> 
  </tr> 
  <tr> 
   <td><p> 80/tcp （http）</p><p> 443/tcp （https）</p><br /> </td> 
   <td> どこでも。 トラッキング対象リンクをクリックするたびに、サーバーにHTTP リクエストが生成されます。<br /> </td> 
  </tr> 
 </tbody> 
</table>

### 外部Web サーバー {#external-web-server}

このサーバーは、Web フォーム、ミラーページなどをホストします。次のポートを開く必要があります。

<table> 
 <tbody> 
  <tr> 
   <td> リスニング ポート <br /> </td> 
   <td> 場所<br /> </td> 
  </tr> 
  <tr> 
   <td><p> 80/tcp （http）</p><p> 443/tcp （https）</p><br /> </td> 
   <td> どこでも。 Web フォームをAdobe Campaign プラットフォームから直接管理する場合、またはミラーページを使用する場合に必要です。<br /> </td> 
  </tr> 
 </tbody> 
</table>

### 内部アプリケーションサーバー（Web） {#internal-application-server--web-}

<table> 
 <tbody> 
  <tr> 
   <td> リスニング ポート <br /> </td> 
   <td> 場所<br /> </td> 
  </tr> 
  <tr> 
   <td><p> 80/tcp （http）</p><p> 443/tcp （https）</p><br /> </td> 
   <td> シン クライアントまたはリッチ クライアントを実行しているすべてのコンピューター。<br /> </td> 
  </tr> 
 </tbody> 
</table>

## Adobe Experience Managerとの連携 {#integration-with-adobe-experience-manager}

インストールが「オンプレミス」の場合は、Adobe CampaignとAdobe Experience Manager間の統合で複数のポートを開く必要があります。 この統合の設定について詳しくは、[詳細ドキュメント &#x200B;](../../integrations/using/about-adobe-experience-manager.md)を参照してください。

<table> 
 <tbody> 
  <tr> 
   <td> リスニング ポート <br /> </td> 
   <td> 説明<br /> </td> 
  </tr> 
  <tr> 
   <td> 80<br /> </td> 
   <td> Adobe Campaign<br />へのAEM接続 </td> 
  </tr> 
  <tr> 
   <td><p> 4502</p><p> 4503</p><br /> </td> 
   <td> AEMの「オーサリング」および「パブリッシング」インスタンスへのAdobe Campaign接続。 開くポートは、AEMの構成によって、既定のポートとは異なる場合があります。<br /> </td> 
  </tr> 
 </tbody> 
</table>

## 帯域幅 {#bandwidth}

考慮に入れるべきネットワーク設定の別のキーパラメータ。 ほとんどの場合、アウトバウンドで利用され、メール配信中に需要が急増します。 ここでは、アドビの経験にもとづいた設定の例をいくつか紹介します。

* 1時間あたり10,000通のメールの場合、1Mb/秒（平均サイズは30 Kb）
* 1時間あたり100,000通のメールの場合、8～10 Mb/秒（平均サイズは30 Kb）

帯域幅に制約がある場合は、需要が少ない夜間にキャンペーンを実行するようにスケジュールを設定することができます。
