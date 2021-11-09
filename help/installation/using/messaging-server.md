---
product: campaign
title: メッセージサーバー
description: メッセージサーバー
audience: installation
content-type: reference
topic-tags: prerequisites-and-recommendations-
exl-id: d9ffa58d-81e3-4291-8502-3cb7c326b666
source-git-commit: 20509f44c5b8e0827a09f44dffdf2ec9d11652a1
workflow-type: tm+mt
source-wordcount: '162'
ht-degree: 3%

---

# メッセージサーバー{#messaging-server}

![](../../assets/v7-only.svg)

Adobe Campaignは送信電子メールをネイティブに処理しますが、返された電子メールにリンクされた受信メッセージを（メーラーデーモンから）受信するには、従来の電子メールサーバーが必要です。 このサーバーで構成されたメールボックスは、アプリケーションによって自動的に処理されます。

POP3 アクセス用に設定されたすべてのサーバーは、メールの取得時に SMTP の「Message-ID」ヘッダーを保持している場合、返信メールの受信に使用できます。 例えば、Qmail、SendMail、Microsoft Exchange を使用した実装は、現在実稼動中です。 しかし、Lotus Notes/domino の一部のインストールでは、「Message-Id」ヘッダーの管理に問題が発生していました。

>[!CAUTION]
>
>このメールサーバーは、負荷の大きいサーバーを処理する必要がある場合があります：最初のフェーズでは、一般的なリストは、最大 10%のバウンス率を生み出す可能性があります（100,000 件のメッセージを送信する場合は、10,000 件のバウンスを受け取ることを期待します）。
>
>このタスクに会社のメッセージングサーバーを使用することは、大きな影響を受ける可能性があるので、お勧めしません。
>
>DNS の特定のサブドメインとバウンスメール用の専用サーバーを設定することをお勧めします。
