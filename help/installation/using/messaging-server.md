---
product: campaign
title: メッセージサーバー
description: メッセージサーバー
badge-v7-only: label="v7" type="Informative" tooltip="Applies to Campaign Classic v7 only"
badge-v7-prem: label="on-premise & hybrid" type="Caution" url="https://experienceleague.adobe.com/docs/campaign-classic/using/installing-campaign-classic/architecture-and-hosting-models/hosting-models-lp/hosting-models.html?lang=en" tooltip="Applies to on-premise and hybrid deployments only"
audience: installation
content-type: reference
topic-tags: prerequisites-and-recommendations-
exl-id: d9ffa58d-81e3-4291-8502-3cb7c326b666
source-git-commit: a5762cd21a1a6d5a5f3a10f53a5d1f43542d99d4
workflow-type: tm+mt
source-wordcount: '162'
ht-degree: 3%

---

# メッセージサーバー{#messaging-server}



Adobe Campaignは送信電子メールをネイティブに処理しますが、返された電子メールにリンクされた受信メッセージを（メーラーデーモンから）受信するには、従来の電子メールサーバーが必要です。 このサーバーで構成されたメールボックスは、アプリケーションによって自動的に処理されます。

POP3 アクセス用に設定されたすべてのサーバーは、メールの取得時に SMTP の「Message-ID」ヘッダーを保持している場合、返信メールの受信に使用できます。 例えば、Qmail、SendMail、Microsoft Exchange を使用した実装は、現在実稼動中です。 しかし、Lotus Notes/domino の一部のインストールでは、「Message-Id」ヘッダーの管理に問題が発生していました。

>[!CAUTION]
>
>このメールサーバーは、負荷の大きいサーバーを処理する必要がある場合があります：最初のフェーズでは、一般的なリストは、最大 10%のバウンス率を生み出す可能性があります（100,000 件のメッセージを送信する場合は、10,000 件のバウンスを受け取ることを期待します）。
>
>このタスクに会社のメッセージングサーバーを使用することは、大きな影響を受ける可能性があるので、お勧めしません。
>
>DNS の特定のサブドメインとバウンスメール用の専用サーバーを設定することをお勧めします。
