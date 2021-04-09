---
solution: Campaign Classic
product: campaign
title: キャンペーン配信の設定
description: キャンペーン配信の設定方法を説明します。
audience: installation
content-type: reference
topic-tags: initial-configuration
exl-id: 2968d8db-2b4b-48e6-a22e-daba5ffe0576
translation-type: tm+mt
source-git-commit: 401e1be234d52f04cbdf8dfa97f51ac227836cd5
workflow-type: tm+mt
source-wordcount: '462'
ht-degree: 3%

---

# 配信設定を構成{#delivery-settings}

配信パラメーターは、**serverConf.xml**&#x200B;フォルダーで設定する必要があります。

* **DNS構成**:以 **`<dnsconfig>`** 降のMTAモジュールが行うMX型DNSクエリに応答するために使用するDNSサーバーの配信ドメインとIPアドレス（またはホスト）を指定します。

   >[!NOTE]
   >
   >**nameServers**&#x200B;パラメーターは、Windowsでのインストールに必須です。 Linuxでのインストールの場合は、空のままにしておく必要があります。

   ```
   <dnsConfig localDomain="domain.com" nameServers="192.0.0.1,192.0.0.2"/>
   ```

また、ニーズや設定に応じて、次の設定を行うこともできます。[SMTPリレー](#smtp-relay)を構成し、[MTA子プロセス](#mta-child-processes)の数を調整します。[送信SMTPトラフィックの管理](#managing-outbound-smtp-traffic-with-affinities)。

## SMTPリレー{#smtp-relay}

MTAモジュールは、SMTPブロードキャスト用のネイティブメール転送エージェント（ポート25）として機能する。

ただし、セキュリティポリシーで必要な場合は、リレーサーバーで置き換えることができます。 その場合、グローバルスループットは、中継サーバのスループットがAdobe Campaignのスループットより低い場合に限り、中継サーバのスループットとなります。

この場合、これらのパラメーターは&#x200B;**`<relay>`**&#x200B;セクションでSMTPサーバーを設定することで設定されます。 メールの転送に使用するSMTPサーバーのIPアドレス（またはホスト）と、それに関連付けられたポート（デフォルトで25）を指定する必要があります。

```
<relay address="192.0.0.3" port="25"/>
```

>[!IMPORTANT]
>
>この動作モードは、中継サーバ固有の性能（待ち時間、帯域など）が原因でスループットが大幅に低下する可能性があるので、配信に対する重大な制限を意味します。 また、（SMTPトラフィックの分析で検出される）同期配信エラーを認定する能力も限られ、中継サーバが使用できない場合は送信はできません。

## MTA子プロセス{#mta-child-processes}

サーバのCPU電力と使用可能なネットワークリソースに応じてブロードキャストパフォーマンスを最適化するために、子プロセスの数（デフォルトではmaxSpareServers）を制御できます。 この設定は、各コンピュータのMTA設定の&#x200B;**`<master>`**&#x200B;セクションで行います。

```
<master dataBasePoolPeriodSec="30" dataBaseRetryDelaySec="60" maxSpareServers="2" minSpareServers="0" startSpareServers="0">
```

[Eメール送信の最適化](../../installation/using/email-deliverability.md#email-sending-optimization)も参照してください。

## アフィニティ{#managing-outbound-smtp-traffic-with-affinities}で送信SMTPトラフィックを管理

>[!IMPORTANT]
>
>アフィニティの設定は、サーバ間で一貫している必要があります。 構成の変更はMTAを実行するすべてのアプリケーションサーバーに複製される必要があるので、アフィニティ設定についてはAdobeにお問い合わせください。

IPアドレスを持つアフィニティを介した送信SMTPトラフィックを改善できます。

それには、次の手順に従います。

1. **serverConf.xml**&#x200B;ファイルの&#x200B;**`<ipaffinity>`**&#x200B;セクションにアフィニティを入力します。

   1つのアフィニティには、複数の異なる名前を付けることができます。区切るには、**;**&#x200B;文字を使用します。

   例：

   ```
    IPAffinity name="mid.Server;WWserver;local.Server">
             <IP address="XX.XXX.XX.XX" heloHost="myserver.us.campaign.net" publicId="123" excludeDomains="neo.*" weight="5"/
   ```

   関連するパラメーターを表示するには、**serverConf.xml**&#x200B;ファイルを参照してください。

1. ドロップダウンリストでアフィニティを選択できるようにするには、**IPAffinity**&#x200B;定義済みリストにアフィニティ名を追加する必要があります。

   ![](assets/ipaffinity_enum.png)

   >[!NOTE]
   >
   >定義済みリストの詳細は[このドキュメント](../../platform/using/managing-enumerations.md)に記載されています。

   次に示すように、タイポロジに使用するアフィニティを選択できます。

   ![](assets/ipaffinity_typology.png)

   >[!NOTE]
   >
   >[配信サーバの設定](../../installation/using/email-deliverability.md#delivery-server-configuration)も参照できます。

**関連トピック**
* [技術的な電子メール設定](email-deliverability.md)
* [MXサーバーとキャンペーンの使用](using-mx-servers.md)
* [電子メール BCC の設定](email-archiving.md)
