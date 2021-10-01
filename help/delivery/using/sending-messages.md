---
product: campaign
title: Adobe Campaign Classic を使用した E メールの送信
description: E メールの配信を確定し、E メールメッセージを配信する際の特異性を発見する方法について説明します。
audience: delivery
content-type: reference
topic-tags: sending-emails
exl-id: c75a5ea2-8d62-4f98-bccd-7116a4d404fd
source-git-commit: 20509f44c5b8e0827a09f44dffdf2ec9d11652a1
workflow-type: ht
source-wordcount: '219'
ht-degree: 100%

---

# E メールを送信する主な手順 {#confirming-email-delivery}

![](../../assets/common.svg)

E メールを作成および設定したら、メインターゲットに送信できます。 この節では、E メールの配信を確認するための主な手順を示します。

1. E メール配信に固有の設定をすべて設定したことを確認します。詳しくは、[E メールパラメーター](email-parameters.md)を参照してください。
1. E メールの準備が整ったら、メインターゲットに送信する前に、配達確認を送信して潜在的なエラーを検出することをお勧めします。詳しくは、[配達確認の送信](steps-validating-the-delivery.md#sending-a-proof)を参照してください。

1. 完了したら、分析を起動して E メールを検証する必要があります。これをおこなうには、「**[!UICONTROL 送信]**」をクリックし、アクションを選択して「**[!UICONTROL 分析]**」をクリックします。詳しくは、[分析の起動](steps-validating-the-delivery.md#analyzing-the-delivery)を参照してください。

1. 分析が完了したら、「**[!UICONTROL 配信を確定]**」をクリックして、ターゲティングされた受信者に対するメッセージの配信を開始します。詳しくは、[配信の確定](steps-sending-the-delivery.md#confirming-delivery)を参照してください。

   <!--Add screenshot with analysis done and Confirm delivery button activated.-->

>[!NOTE]
>
>配信を検証するプロセス全体については、[この節](steps-validating-the-delivery.md)で説明します。配信を設定して送信するための詳細な手順については、[この節](steps-sending-the-delivery.md)を参照してください。

次の節では、E メール配信に固有の設定について詳しく説明します。
<!--* [Generating the mirror page](generating-mirror-page.md)
* [Email BCC](email-bcc.md)-->
* [メールパラメーター](email-parameters.md)
* [MTA 強化機能を使用したメールの送信](sending-with-enhanced-mta.md)
* [日本の携帯電話向けのメールの送信](sending-emails-on-japanese-mobiles.md)
