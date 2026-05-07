---
product: campaign
title: メッセージサーバー
description: メッセージサーバー
feature: Installation, Instance Settings
badge-v7-prem: label="オンプレミス／ハイブリッドのみ" type="Caution" url="https://experienceleague.adobe.com/docs/campaign-classic/using/installing-campaign-classic/architecture-and-hosting-models/hosting-models-lp/hosting-models.html?lang=ja" tooltip="オンプレミスデプロイメントとハイブリッドデプロイメントにのみ適用されます"
audience: installation
content-type: reference
topic-tags: prerequisites-and-recommendations-
exl-id: d9ffa58d-81e3-4291-8502-3cb7c326b666
source-git-commit: 14ba450ebff9bba6a36c0df07d715b7279604222
workflow-type: tm+mt
source-wordcount: '198'
ht-degree: 18%

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
