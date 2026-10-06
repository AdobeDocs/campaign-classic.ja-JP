---
product: campaign
title: メッセージサーバー
description: メッセージサーバー
feature: Installation, Instance Settings
badge-v7-prem: label="On-premise/hybrid only" type="Caution" url="https://experienceleague.adobe.com/docs/campaign-classic/using/installing-campaign-classic/architecture-and-hosting-models/hosting-models-lp/hosting-models.html?lang=ja" tooltip="Applies to on-premise and hybrid deployments only"
audience: installation
content-type: reference
topic-tags: prerequisites-and-recommendations-
exl-id: d9ffa58d-81e3-4291-8502-3cb7c326b666
product_v2:
  - id: dfc56824-e8b9-499e-85d4-21aedb507314
    internal-label: Campaign
  - id: fd6e6e36-54e4-4f1a-96fc-1a750e400d50
    internal-label: Campaign Classic v7
feature_v2:
  - id: 7f0a1ee5-eeb8-5478-a9cd-b1896f033118
    internal-label: Instance Settings
  - id: c5474392-5419-4296-9e41-f6f4ce4f6e9b
    internal-label: Administration
subfeature_v2:
  - id: e656c701-3899-4db3-989c-de0980ddfffa
    internal-label: Installation
source-git-commit: a43e591a565a18d79f583d975e3e812c5435b0c0
workflow-type: tm+mt
source-wordcount: '186'
ht-degree: 12%
---
# メッセージサーバー{#messaging-server}



Adobe Campaignはアウトバウンドメールをネイティブに処理しますが、返されるメールにリンクされた受信メッセージを（メーラーデーモンから）受信するには、従来のメールサーバーが必要です。 このサーバーで設定されたメールボックスは、アプリケーションによって自動的に処理されます。

POP3 アクセス用に設定されたすべてのサーバーは、メールを受け取る際にSMTP 「Message-ID」ヘッダーを保持する場合に、リターンメールを受信するために使用できます。 例えば、Qmail、SendMail、Microsoft Exchangeを使用した実装は現在本番稼動中です。 しかし、Lotus Notes/dominoの一部のインストールでは、「Message-Id」ヘッダーの維持に関する問題が明らかになりました。

>[!CAUTION]
>
>このメールサーバーは大量の負荷に対応する必要があります。初期段階では、一般的なリストでは最大10%のバウンス率を生成できます（100,000件のメッセージを送信する場合、10,000件のバウンスが発生すると予想されます）。
>
>そのため、このタスクに自社のメッセージングサーバーを使用することは強く影響を受ける可能性があるため、お勧めしません。
>
>DNSの特定のサブドメインと、バウンスメール用の専用サーバーを設定することをお勧めします。
