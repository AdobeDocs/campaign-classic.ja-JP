---
product: campaign
title: キャンペーン配信設定
description: キャンペーン配信の設定方法を説明します
badge-v7-only: label="v7" type="Informative" tooltip="Applies to Campaign Classic v7 only"
badge-v7-prem: label="on-premise & hybrid" type="Caution" url="https://experienceleague.adobe.com/docs/campaign-classic/using/installing-campaign-classic/architecture-and-hosting-models/hosting-models-lp/hosting-models.html" tooltip="Applies to on-premise and hybrid deployments only"
audience: installation
content-type: reference
topic-tags: initial-configuration
exl-id: 2968d8db-2b4b-48e6-a22e-daba5ffe0576
source-git-commit: 4661688a22bd1a82eaf9c72a739b5a5ecee168b1
workflow-type: tm+mt
source-wordcount: '462'
ht-degree: 5%

---

# 配信設定の指定 {#delivery-settings}



配信パラメーターは、 **serverConf.xml** フォルダー。

* **DNS 設定**:MTA モジュールが **`<dnsconfig>`** 以降

  >[!NOTE]
  >
  >この **nameServers** パラメーターは、Windows でのインストールに必須です。 Linux でのインストールの場合は、空のままにする必要があります。

  ```
  <dnsConfig localDomain="domain.com" nameServers="192.0.0.1,192.0.0.2"/>
  ```

必要に応じて、次の設定を実行することもできます。設定 [SMTP リレー](#smtp-relay)、 [MTA 子プロセス](#mta-child-processes), [送信 SMTP トラフィックを管理](#managing-outbound-smtp-traffic-with-affinities).

## SMTP リレー {#smtp-relay}

MTA モジュールは、SMTP ブロードキャスト用のネイティブメール転送エージェント（ポート 25）として機能します。

ただし、セキュリティポリシーで必要な場合は、リレーサーバーで置き換えることができます。 この場合、グローバルスループットはリレーのスループットになります ( リレーサーバーのスループットがAdobe Campaignのスループットよりも低い場合 )。

この場合、これらのパラメーターは、 **`<relay>`** 」セクションに入力します。 メールの転送に使用する SMTP サーバーの IP アドレス（またはホスト）と、それに関連するポート（デフォルトでは 25）を指定する必要があります。

```
<relay address="192.0.0.3" port="25"/>
```

>[!IMPORTANT]
>
>この動作モードは、配信に対する重大な制限を意味します。リレーサーバーの固有のパフォーマンス（待ち時間、帯域幅など）が原因で、スループットが大幅に低下する可能性があるからです。 また、（SMTP トラフィックの分析で検出される）同期配信エラーを検証する能力は制限され、リレーサーバーが利用できない場合は送信ができなくなります。

## MTA 子プロセス {#mta-child-processes}

サーバの CPU 処理能力と使用可能なネットワークリソースに応じてブロードキャストパフォーマンスを最適化するために、子プロセスの数（デフォルトでは maxSpareServers）を制御できます。 この設定は、 **`<master>`** 個々のコンピューター上の MTA 設定のセクション。

```
<master dataBasePoolPeriodSec="30" dataBaseRetryDelaySec="60" maxSpareServers="2" minSpareServers="0" startSpareServers="0">
```

また、 [E メール送信の最適化](../../installation/using/email-deliverability.md#email-sending-optimization).

## アフィニティを使用したアウトバウンド SMTP トラフィックの管理 {#managing-outbound-smtp-traffic-with-affinities}

>[!IMPORTANT]
>
>アフィニティの設定は、サーバー間で一貫性を保つ必要があります。 設定の変更は MTA を実行するすべてのアプリケーションサーバーでレプリケートされる必要があるので、アフィニティ設定については、Adobeに問い合わせることをお勧めします。

IP アドレスを使用したアフィニティを通じて、アウトバウンド SMTP トラフィックを改善できます。

それには、次の手順に従います。

1. にアフィニティを入力します。 **`<ipaffinity>`** セクション **serverConf.xml** ファイル。

   1 つのアフィニティには、複数の異なる名前を付けることができます。区切るには、 **;** 文字。

   例：

   ```
    IPAffinity name="mid.Server;WWserver;local.Server">
             <IP address="XX.XXX.XX.XX" heloHost="myserver.us.campaign.net" publicId="123" excludeDomains="neo.*" weight="5"/
   ```

   関連するパラメーターを表示するには、 **serverConf.xml** ファイル。

1. ドロップダウンリストでアフィニティの選択を有効にするには、 **IPAffinity** 列挙。

   ![](assets/ipaffinity_enum.png)

   >[!NOTE]
   >
   >列挙について詳しくは、 [このドキュメント](../../platform/using/managing-enumerations.md).

   その後、タイポロジに関して以下に示すように、使用するアフィニティを選択できます。

   ![](assets/ipaffinity_typology.png)

   >[!NOTE]
   >
   >また、 [配信サーバーの設定](../../installation/using/email-deliverability.md#delivery-server-configuration).

**関連トピック**
* [技術的なメール設定](email-deliverability.md)
* [Campaign での MX サーバーの使用](using-mx-servers.md)
* [メール BCC の設定](email-archiving.md)
