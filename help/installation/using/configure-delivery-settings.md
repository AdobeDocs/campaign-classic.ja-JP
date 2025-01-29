---
product: campaign
title: キャンペーン配信設定の構成
description: Campaign 配信設定の設定方法を学ぶ
feature: Installation, Channel Configuration
badge-v7-prem: label="オンプレミス／ハイブリッドのみ" type="Caution" url="https://experienceleague.adobe.com/docs/campaign-classic/using/installing-campaign-classic/architecture-and-hosting-models/hosting-models-lp/hosting-models.html?lang=ja" tooltip="オンプレミスデプロイメントとハイブリッドデプロイメントにのみ適用されます"
audience: installation
content-type: reference
topic-tags: initial-configuration
exl-id: 2968d8db-2b4b-48e6-a22e-daba5ffe0576
source-git-commit: 14ba450ebff9bba6a36c0df07d715b7279604222
workflow-type: tm+mt
source-wordcount: '476'
ht-degree: 7%

---

# 配信設定の指定 {#delivery-settings}



配信パラメーターは、**serverConf.xml** フォルダーで設定する必要があります。

* **DNS 設定**:MTA モジュールによって **`<dnsconfig>`** 以降に実行される MX 型 DNS クエリへの応答に使用される配信ドメインと DNS サーバーの IP アドレス（またはホスト）を指定します。

  >[!NOTE]
  >
  >**nameServers** パラメーターは、Windows のインストールに不可欠です。 Linux のインストールの場合、空のままにする必要があります。

  ```
  <dnsConfig localDomain="domain.com" nameServers="192.0.0.1,192.0.0.2"/>
  ```

また、ニーズと設定に応じて、[SMTP リレー ](#smtp-relay) の設定、[MTA 子プロセス ](#mta-child-processes) 数の適応、[ 送信 SMTP トラフィックの管理 ](#managing-outbound-smtp-traffic-with-affinities) の設定を実行することもできます。

## SMTP リレー {#smtp-relay}

MTA モジュールは、SMTP ブロードキャスト（ポート 25）のネイティブ メール転送エージェントとして機能します。

ただし、セキュリティポリシーで必要な場合は、リレーサーバーに置き換えることもできます。 その場合、グローバルスループットはリレーサーバーになります（リレーサーバーのスループットがAdobe Campaignサーバーのスループットよりも劣っている場合）。

この場合、これらのパラメーターは「**`<relay>`**」セクションで SMTP サーバーを設定することで設定されます。 メールの転送に使用する SMTP サーバーの IP アドレス（またはホスト）と、関連するポート（デフォルトでは 25）を指定する必要があります。

```
<relay address="192.0.0.3" port="25"/>
```

>[!IMPORTANT]
>
>この動作モードは、リレーサーバー固有のパフォーマンス（待ち時間、帯域幅など）によってスループットが大幅に低下する可能性があるので、配信に関する重大な制限を意味します。 さらに、（SMTP トラフィックの分析によって検出された）同期配信エラーを検証する機能は制限され、リレーサーバーが使用できない場合は送信できません。

## MTA 子プロセス {#mta-child-processes}

子プロセス（デフォルトでは maxSpareServers）の数を制御することで、サーバのCPUパワーと利用可能なネットワークリソースに応じてブロードキャストのパフォーマンスを最適化することができます。 この設定は、個々のコンピューターの MTA 設定の **`<master>`** セクションで行われます。

```
<master dataBasePoolPeriodSec="30" dataBaseRetryDelaySec="60" maxSpareServers="2" minSpareServers="0" startSpareServers="0">
```

[ メール送信の最適化 ](../../installation/using/email-deliverability.md#email-sending-optimization) も参照してください。

## アフィニティ付き送信 SMTP トラフィックの管理 {#managing-outbound-smtp-traffic-with-affinities}

>[!IMPORTANT]
>
>アフィニティ設定は、あるサーバーから別のサーバーへと一貫している必要があります。 設定の変更は MTA を実行するすべてのアプリケーションサーバーでレプリケートする必要があるので、アフィニティ設定については、Adobeにお問い合わせいただくことをお勧めします。

IP アドレスとのアフィニティを介した送信 SMTP トラフィックを改善できます。

それには、次の手順に従います。

1. **serverConf.xml** ファイルの **`<ipaffinity>`** セクションにアフィニティを入力します。

   1 つのアフィニティに、複数の異なる名前を付けることができます。名前を区切るには、**;** 文字を使用します。

   例：

   ```
    IPAffinity name="mid.Server;WWserver;local.Server">
             <IP address="XX.XXX.XX.XX" heloHost="myserver.us.campaign.net" publicId="123" excludeDomains="neo.*" weight="5"/
   ```

   関連するパラメーターを表示するには、**serverConf.xml** ファイルを参照してください。

1. ドロップダウンリストでのアフィニティ選択を有効にするには、**IPAffinity** 列挙にアフィニティ名を追加する必要があります。

   ![](assets/ipaffinity_enum.png)

   >[!NOTE]
   >
   >列挙について詳しくは、[ このドキュメント ](../../platform/using/managing-enumerations.md) を参照してください。

   次に、タイポロジで以下に示すように、使用するアフィニティを選択できます。

   ![](assets/ipaffinity_typology.png)

   >[!NOTE]
   >
   >[ 配信サーバーの設定 ](../../installation/using/email-deliverability.md#delivery-server-configuration) も参照してください。

**関連トピック**
* [技術的なメール設定](email-deliverability.md)
* [Campaign での MX サーバーの使用](using-mx-servers.md)
* [メール BCC の設定](email-archiving.md)
