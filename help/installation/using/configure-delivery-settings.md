---
product: campaign
title: キャンペーン配信設定
description: キャンペーン配信の設定方法を説明します
audience: installation
content-type: reference
topic-tags: initial-configuration
exl-id: 2968d8db-2b4b-48e6-a22e-daba5ffe0576
source-git-commit: 98d646919fedc66ee9145522ad0c5f15b25dbf2e
workflow-type: tm+mt
source-wordcount: '462'
ht-degree: 5%

---

# 配信設定の指定 {#delivery-settings}

配信パラメーターは、**serverConf.xml**&#x200B;フォルダーで設定する必要があります。

* **DNS設定**:以降のMTAモジュールでおこなわれるMXタイプのDNSクエリに応答するために使用するDNSサーバーの配信ドメインとIPアドレス（またはホスト）を指定 **`<dnsconfig>`** します。

   >[!NOTE]
   >
   >**nameServers**&#x200B;パラメーターは、Windowsでのインストールに不可欠です。 Linuxでのインストールの場合は、空のままにする必要があります。

   ```
   <dnsConfig localDomain="domain.com" nameServers="192.0.0.1,192.0.0.2"/>
   ```

必要に応じて、次の設定を実行することもできます。[SMTPリレー](#smtp-relay)を設定し、[MTA子プロセス](#mta-child-processes)、[送信SMTPトラフィックの管理](#managing-outbound-smtp-traffic-with-affinities)の数を調整します。

## SMTPリレー{#smtp-relay}

MTAモジュールは、SMTPブロードキャスト（ポート25）用のネイティブメール転送エージェントとして機能します。

ただし、セキュリティポリシーで必要な場合は、リレーサーバーで置き換えることができます。 その場合、グローバルスループットはリレースループットになります(リレーサーバーのスループットがAdobe Campaignのスループットよりも低い場合)。

この場合、これらのパラメーターは、**`<relay>`**&#x200B;セクションでSMTPサーバーを設定することで設定されます。 メールの転送に使用するSMTPサーバーのIPアドレス（またはホスト）と、それに関連するポート（デフォルトでは25）を指定する必要があります。

```
<relay address="192.0.0.3" port="25"/>
```

>[!IMPORTANT]
>
>この動作モードは、中継サーバーの固有のパフォーマンス（待ち時間、帯域幅など）が原因で、スループットを大幅に低下させる可能性があるので、配信に重大な制限があることを意味します。 また、（SMTPトラフィックの分析で検出される）同期配信エラーを検証する能力は制限され、リレーサーバーが利用できない場合は送信ができなくなります。

## MTA子プロセス{#mta-child-processes}

サーバのCPU電力と使用可能なネットワークリソースに応じてブロードキャストパフォーマンスを最適化するために、子プロセスの数（デフォルトではmaxSpareServers）を制御できます。 この設定は、個々のコンピューターのMTA設定の&#x200B;**`<master>`**&#x200B;セクションで行う必要があります。

```
<master dataBasePoolPeriodSec="30" dataBaseRetryDelaySec="60" maxSpareServers="2" minSpareServers="0" startSpareServers="0">
```

[Eメール送信の最適化](../../installation/using/email-deliverability.md#email-sending-optimization)も参照してください。

## アフィニティ{#managing-outbound-smtp-traffic-with-affinities}を使用して送信SMTPトラフィックを管理します

>[!IMPORTANT]
>
>アフィニティの設定は、サーバー間で一貫性が必要です。 設定の変更はMTAを実行するすべてのアプリケーションサーバーでレプリケートする必要があるので、アフィニティの設定については、Adobeに問い合わせることをお勧めします。

IPアドレスを使用してアフィニティを通じて送信SMTPトラフィックを改善できます。

それには、次の手順に従います。

1. **serverConf.xml**&#x200B;ファイルの&#x200B;**`<ipaffinity>`**&#x200B;セクションにアフィニティを入力します。

   1つのアフィニティには、複数の異なる名前を指定できます。区切るには、**;**&#x200B;文字を使用します。

   例：

   ```
    IPAffinity name="mid.Server;WWserver;local.Server">
             <IP address="XX.XXX.XX.XX" heloHost="myserver.us.campaign.net" publicId="123" excludeDomains="neo.*" weight="5"/
   ```

   関連するパラメーターを表示するには、**serverConf.xml**&#x200B;ファイルを参照してください。

1. ドロップダウンリストでアフィニティを選択できるようにするには、**IPAffinity**&#x200B;列挙にアフィニティ名を追加する必要があります。

   ![](assets/ipaffinity_enum.png)

   >[!NOTE]
   >
   >列挙について詳しくは、[このドキュメント](../../platform/using/managing-enumerations.md)を参照してください。

   次に示すように、タイポロジ用に使用されるアフィニティを選択できます。

   ![](assets/ipaffinity_typology.png)

   >[!NOTE]
   >
   >[配信サーバーの設定](../../installation/using/email-deliverability.md#delivery-server-configuration)も参照してください。

**関連トピック**
* [技術的なメール設定](email-deliverability.md)
* [Campaign での MX サーバーの使用](using-mx-servers.md)
* [メール BCC の設定](email-archiving.md)
