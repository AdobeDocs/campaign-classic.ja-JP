---
product: campaign
title: メッセージサーバー
description: メッセージサーバー
audience: installation
content-type: reference
topic-tags: prerequisites-and-recommendations-
exl-id: d9ffa58d-81e3-4291-8502-3cb7c326b666
source-git-commit: 98d646919fedc66ee9145522ad0c5f15b25dbf2e
workflow-type: tm+mt
source-wordcount: '162'
ht-degree: 3%

---

# メッセージサーバー{#messaging-server}

Adobe Campaignは送信電子メールをネイティブに処理しますが、返された電子メールにリンクされた受信メッセージを（メーラーデーモンから）受信するには、従来の電子メールサーバーが必要です。 このサーバーで構成されたメールボックスは、アプリケーションによって自動的に処理されます。

POP3アクセス用に設定されたすべてのサーバーは、メールを取得する際にSMTPの「Message-ID」ヘッダーを保持している場合、返信メールの受信に使用できます。 例えば、Qmail、SendMail、Microsoft Exchangeを使用した実装は、現在実稼動中です。 しかし、Lotus Notes/Dominoの一部のインストールでは、「Message-Id」ヘッダーの保守に問題があったことが明らかになりました。

>[!CAUTION]
>
>このメールサーバーは、負荷が大きい場合に処理する必要がある可能性があります。最初のフェーズでは、一般的なリストは最大10%のバウンス率を生み出す可能性があります（10万件のメッセージを送信する場合は、10,000件のバウンスを受け取ることを期待します）。
>
>そのため、このタスクに対して会社のメッセージングサーバーを使用することは、大きな影響を受ける可能性があるのでお勧めしません。
>
>DNSの特定のサブドメインとバウンスメール用の専用サーバーを設定することをお勧めします。
