---
title: メッセージングサーバ
seo-title: メッセージングサーバ
description: メッセージングサーバ
seo-description: null
page-status-flag: never-activated
uuid: d7de0405-23eb-4a0d-80a5-c75d661771bb
contentOwner: sauviat
products: SG_CAMPAIGN/CLASSIC
audience: installation
content-type: reference
topic-tags: prerequisites-and-recommendations-
discoiquuid: 1556e87f-9d92-4548-a75a-4f44030ab8d5
index: y
internal: n
snippet: y
translation-type: tm+mt
source-git-commit: 46f5bfb41bfe9c938ac0ffa767ead3e47a32047d

---


# メッセージングサーバ{#messaging-server}

Adobe Campaignは送信電子メールをネイティブに処理しますが、返された電子メールにリンクされた受信メッセージを（メーラーデーモンから）受信するには、従来の電子メールサーバーが必要です。 このサーバーで構成されたメールボックスは、アプリケーションによって自動的に処理されます。

POP3アクセス用に設定されたすべてのサーバは、メールの取得時にSMTP &quot;Message-ID&quot;ヘッダを保持している場合、返信メールの受信に使用できます。 例えば、Qmail、SendMail、およびMicrosoft Exchangeを使用した実装は現在実稼働中です。 ただし、Lotus Notes/Dominoの一部のインストールでは、「Message-Id」ヘッダーの管理に関する問題が明らかになりました。

>[!CAUTION]
>
>このメールサーバは、負荷の大きい次の処理を行う必要がある場合があります。最初の段階では、通常のリストは最大10%の直帰率を生み出します（100,000件のメッセージを送信する場合、10,000回のバウンスを受け取ることを期待します）。
>
>そのため、このタスクには大きな影響を与える可能性があるので、会社のメッセージングサーバーを使用しないことをお勧めします。
>
>DNSの特定のサブドメインと、バウンスメール用の専用サーバを設定することをお勧めします。
