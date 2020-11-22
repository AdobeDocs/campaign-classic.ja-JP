---
solution: Campaign Classic
product: campaign
title: メッセージングサーバー
description: メッセージングサーバー
audience: installation
content-type: reference
topic-tags: prerequisites-and-recommendations-
translation-type: tm+mt
source-git-commit: 972885c3a38bcd3a260574bacbb3f507e11ae05b
workflow-type: tm+mt
source-wordcount: '162'
ht-degree: 3%

---


# メッセージングサーバー{#messaging-server}

Adobe Campaignは送信電子メールをネイティブに処理しますが、(メーラーデーモンから)返された電子メールにリンクされた受信メッセージを受信するには、従来の電子メールサーバーが必要です。 このサーバーに構成されたメールボックスは、アプリケーションによって自動的に処理されます。

POP3アクセス用に設定されたすべてのサーバは、メールの取得時にSMTP &quot;Message-ID&quot;ヘッダを保持している場合、返信メールの受信に使用できます。 例えば、Qmail、SendMail、およびMicrosoft Exchangeを使用した実装は、現在実稼動中です。 ただし、Lotus Notes/Dominoの一部のインストールでは、「Message-Id」ヘッダーの管理に関する問題が明らかになりました。

>[!CAUTION]
>
>このメールサーバーは、負荷の大きい次の処理を行う必要がある場合があります。最初の段階では、一般的なリストは最大10%の直帰率を生み出します（100,000件のメッセージを送信する場合、10,000回のバウンスを受け取ることが予測されます）。
>
>そのため、このタスクに対しては会社メッセージングサーバーを使用しないことをお勧めします。これは、大きな影響を受ける可能性があるためです。
>
>DNSの特定のサブドメインと、バウンスメール用の専用サーバを設定することをお勧めします。
