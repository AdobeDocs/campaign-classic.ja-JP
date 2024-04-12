---
product: campaign
title: キャンペーン配信設定の構成
description: Campaign 配信設定の設定方法を学ぶ
feature: Installation, Channel Configuration
badge-v7-prem: label="オンプレミス/ハイブリッドのみ" type="Caution" url="https://experienceleague.adobe.com/docs/campaign-classic/using/installing-campaign-classic/architecture-and-hosting-models/hosting-models-lp/hosting-models.html?lang=ja" tooltip="オンプレミスデプロイメントとハイブリッドデプロイメントにのみ適用されます"
audience: installation
content-type: reference
topic-tags: initial-configuration
exl-id: 2968d8db-2b4b-48e6-a22e-daba5ffe0576
source-git-commit: 14ba450ebff9bba6a36c0df07d715b7279604222
workflow-type: tm+mt
source-wordcount: '476'
ht-degree: 6%

---

# 配信設定の指定 {#delivery-settings}



配信パラメーターは、 **serverConf.xml** フォルダー。

* **DNS 設定**：から MTA モジュールによって行われる MX タイプの DNS クエリへの応答に使用される配信ドメインと DNS サーバーの IP アドレス（またはホスト）を指定します **`<dnsconfig>`** 以降。

  >[!NOTE]
  >
  >この **nameServer** パラメーターは、Windows のインストールに不可欠です。 Linux のインストールの場合、空のままにする必要があります。

  ```
  <dnsConfig localDomain="domain.com" nameServers="192.0.0.1,192.0.0.2"/>
  ```

ニーズや設定に応じて、次の設定も実行できます。 [SMTP リレー](#smtp-relay)、の数を調整 [MTA 子プロセス](#mta-child-processes), [送信 SMTP トラフィックの管理](#managing-outbound-smtp-traffic-with-affinities).

## SMTP リレー {#smtp-relay}

MTA モジュールは、SMTP ブロードキャスト（ポート 25）のネイティブ メール転送エージェントとして機能します。

ただし、セキュリティポリシーで必要な場合は、リレーサーバーに置き換えることもできます。 その場合、グローバルスループットはリレーサーバーになります（リレーサーバーのスループットがAdobe Campaignサーバーのスループットよりも劣っている場合）。

この場合、これらのパラメーターは **`<relay>`** セクション。 メールの転送に使用する SMTP サーバーの IP アドレス（またはホスト）と、関連するポート（デフォルトでは 25）を指定する必要があります。

```
<relay address="192.0.0.3" port="25"/>
```

>[!IMPORTANT]
>
>この動作モードは、リレーサーバー固有のパフォーマンス（待ち時間、帯域幅など）によってスループットが大幅に低下する可能性があるので、配信に関する重大な制限を意味します。 さらに、（SMTP トラフィックの分析によって検出された）同期配信エラーを検証する機能は制限され、リレーサーバーが使用できない場合は送信できません。

## MTA 子プロセス {#mta-child-processes}

サーバの CPU パワーと利用可能なネットワークリソースに応じて、ブロードキャストのパフォーマンスを最適化するために、子プロセスの数（デフォルトでは maxSpareServers 2）を制御することができます。 この設定は、 **`<master>`** 個々のコンピューターの MTA 設定のセクション。

```
<master dataBasePoolPeriodSec="30" dataBaseRetryDelaySec="60" maxSpareServers="2" minSpareServers="0" startSpareServers="0">
```

も参照してください。 [メール送信の最適化](../../installation/using/email-deliverability.md#email-sending-optimization).

## アフィニティ付き送信 SMTP トラフィックの管理 {#managing-outbound-smtp-traffic-with-affinities}

>[!IMPORTANT]
>
>アフィニティ設定は、あるサーバーから別のサーバーへと一貫している必要があります。 設定の変更は MTA を実行するすべてのアプリケーションサーバーでレプリケートする必要があるので、アフィニティ設定については、Adobeにお問い合わせいただくことをお勧めします。

IP アドレスとのアフィニティを介した送信 SMTP トラフィックを改善できます。

それには、次の手順に従います。

1. にアフィニティを入力 **`<ipaffinity>`** の節 **serverConf.xml** ファイル。

   1 つのアフィニティに、複数の異なる名前を付けることができます。名前を区切るには、 **;** 文字。

   例：

   ```
    IPAffinity name="mid.Server;WWserver;local.Server">
             <IP address="XX.XXX.XX.XX" heloHost="myserver.us.campaign.net" publicId="123" excludeDomains="neo.*" weight="5"/
   ```

   関連するパラメーターを表示するには、を参照してください。 **serverConf.xml** ファイル。

1. ドロップダウンリストでのアフィニティ選択を有効にするには、 **IPAffinity** 列挙。

   ![](assets/ipaffinity_enum.png)

   >[!NOTE]
   >
   >列挙の詳細 [このドキュメント](../../platform/using/managing-enumerations.md).

   次に、タイポロジで以下に示すように、使用するアフィニティを選択できます。

   ![](assets/ipaffinity_typology.png)

   >[!NOTE]
   >
   >以下も参照してください。 [配信サーバーの設定](../../installation/using/email-deliverability.md#delivery-server-configuration).

**関連トピック**
* [技術的なメール設定](email-deliverability.md)
* [Campaign での MX サーバーの使用](using-mx-servers.md)
* [メール BCC の設定](email-archiving.md)
