---
product: campaign
title: キャンペーン配信設定
description: キャンペーン配信の設定方法を説明します
audience: installation
content-type: reference
topic-tags: initial-configuration
exl-id: 2968d8db-2b4b-48e6-a22e-daba5ffe0576
source-git-commit: bd9f035db1cbad883e1f27fe901e34dfbc9c1229
workflow-type: tm+mt
source-wordcount: '462'
ht-degree: 5%

---

# 配信設定の指定 {#delivery-settings}

![](../../assets/v7-only.svg)

配信パラメーターは、**serverConf.xml** フォルダーで設定する必要があります。

* **DNS 設定**:以降の MTA モジュールがおこなう MX タイプの DNS クエリに応答するために使用する DNS サーバーの配信ドメインと IP アドレス（またはホスト）を指定 **`<dnsconfig>`** します。

   >[!NOTE]
   >
   >**nameServers** パラメーターは、Windows でのインストールに不可欠です。 Linux でのインストールの場合は、空のままにする必要があります。

   ```
   <dnsConfig localDomain="domain.com" nameServers="192.0.0.1,192.0.0.2"/>
   ```

必要に応じて、次の設定を実行することもできます。[SMTP リレー ](#smtp-relay) を設定し、[MTA 子プロセス ](#mta-child-processes)、[ 送信 SMTP トラフィックの管理 ](#managing-outbound-smtp-traffic-with-affinities) の数を調整します。

## SMTP リレー {#smtp-relay}

MTA モジュールは、SMTP ブロードキャスト（ポート 25）のネイティブメール転送エージェントとして機能します。

ただし、セキュリティポリシーで必要な場合は、リレーサーバーで置き換えることができます。 この場合、グローバルスループットは中継スループットになります ( ただし、中継サーバーのスループットがAdobe Campaignのスループットよりも低い場合 )。

この場合、これらのパラメーターは **`<relay>`** セクションで SMTP サーバーを設定することで設定されます。 メールの転送に使用する SMTP サーバーの IP アドレス（またはホスト）と、それに関連するポート（デフォルトでは 25）を指定する必要があります。

```
<relay address="192.0.0.3" port="25"/>
```

>[!IMPORTANT]
>
>この動作モードは配信に重大な制限を含みます。これは、リレーサーバーの固有のパフォーマンス（待ち時間、帯域幅など）が原因で、スループットを大幅に低下させる可能性があるからです。 また、同期配信エラー（SMTP トラフィックの分析で検出）を検証する能力は限られ、リレーサーバーが利用できない場合は送信ができなくなります。

## MTA 子プロセス {#mta-child-processes}

サーバの CPU 電力と使用可能なネットワークリソースに応じてブロードキャストパフォーマンスを最適化するために、子プロセスの数（デフォルトでは maxSpareServers 2）を制御できます。 この設定は、個々のコンピューターの MTA 設定の **`<master>`** セクションで行います。

```
<master dataBasePoolPeriodSec="30" dataBaseRetryDelaySec="60" maxSpareServers="2" minSpareServers="0" startSpareServers="0">
```

[E メール送信の最適化 ](../../installation/using/email-deliverability.md#email-sending-optimization) も参照してください。

## アフィニティを使用したアウトバウンド SMTP トラフィックの管理 {#managing-outbound-smtp-traffic-with-affinities}

>[!IMPORTANT]
>
>アフィニティの設定は、サーバー間で一貫している必要があります。 設定の変更は MTA を実行するすべてのアプリケーションサーバーでレプリケートする必要があるので、アフィニティの設定については、Adobeに問い合わせることをお勧めします。

IP アドレスを使用してアフィニティを通じて送信 SMTP トラフィックを改善できます。

それには、次の手順に従います。

1. **serverConf.xml** ファイルの **`<ipaffinity>`** セクションにアフィニティを入力します。

   1 つのアフィニティには、複数の異なる名前を指定できます。区切るには、**;** 文字を使用します。

   例：

   ```
    IPAffinity name="mid.Server;WWserver;local.Server">
             <IP address="XX.XXX.XX.XX" heloHost="myserver.us.campaign.net" publicId="123" excludeDomains="neo.*" weight="5"/
   ```

   関連するパラメーターを表示するには、**serverConf.xml** ファイルを参照してください。

1. ドロップダウンリストでアフィニティを選択できるようにするには、**IPAffinity** 列挙にアフィニティ名を追加する必要があります。

   ![](assets/ipaffinity_enum.png)

   >[!NOTE]
   >
   >列挙について詳しくは、[ このドキュメント ](../../platform/using/managing-enumerations.md) を参照してください。

   次に示すように、タイポロジに使用するアフィニティを選択できます。

   ![](assets/ipaffinity_typology.png)

   >[!NOTE]
   >
   >[ 配信サーバーの設定 ](../../installation/using/email-deliverability.md#delivery-server-configuration) も参照してください。

**関連トピック**
* [技術的なメール設定](email-deliverability.md)
* [Campaign での MX サーバーの使用](using-mx-servers.md)
* [メール BCC の設定](email-archiving.md)
