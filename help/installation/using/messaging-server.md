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
source-wordcount: '176'
ht-degree: 9%

---

# メッセージサーバー{#messaging-server}



Adobe Campaignは送信メールをネイティブに処理しますが、返されたメールにリンクされた受信メッセージ（メーラーデーモンから）を受信するには、従来のメールサーバーが必要です。 このサーバーで構成されたメールボックスは、アプリケーションによって自動的に処理されます。

POP3 アクセス用に設定されたすべてのサーバーは、メールの取得時に SMTP 「Message-ID」ヘッダーを保持している場合、返信メールの受信に使用できます。 例えば、Qmail、SendMail およびMicrosoft Exchange を使用した実装は、現在実稼動中です。 しかし、Lotus Notes/domino の一部のインストールでは、「Message-Id」ヘッダーの維持に関する問題が明らかになりました。

>[!CAUTION]
>
>このメールサーバーは、高負荷に対応しなければならない場合があります。初期フェーズでは、一般的なリストは、最大 10% のバウンス率を生成できます（10 万件のメッセージを送信した場合、10,000 件のバウンスを受信すると予測されます）。
>
>そのため、このタスクでは会社のメッセージングサーバーを使用しないことをお勧めします。サーバーが強く影響を受ける可能性があるからです。
>
>DNS の特定のサブドメインと、バウンスメール専用のサーバーを設定することをお勧めします。
