---
product: campaign
title: メッセージデザインに関する FAQ
description: Campaign Classic に関する FAQ
feature: Audiences, Troubleshooting
audience: platform
content-type: reference
topic-tags: starting-with-adobe-campaign
exl-id: 48926e87-03d9-4aa0-89cb-e3fb4f99c1f5
source-git-commit: 435314fa5907c16166cf7ff6741ff7ad0412d04b
workflow-type: tm+mt
source-wordcount: '362'
ht-degree: 78%

---

# メッセージデザインに関する FAQ {#design-messages-faq}



Adobe Campaign でオムニチャネルメッセージをデザインするための主な手順について説明します。

## Campaign でメールをデザインする際の具体的なガイドラインはありますか？ {#are-there-specific-guidelines-when-designing-emails-with-campaign-}

メールのデザインを始める前に、配信のデザインと Adobe Campaign での送信に関する概念とベストプラクティスを理解しておくことをお勧めします。

詳しくは、[Campaign v8 ドキュメント &#x200B;](https://experienceleague.adobe.com/docs/campaign/campaign-v8/send/delivery-best-practices.html?lang=ja){target="_blank"} を参照してください。

## 配信テンプレートとは何ですか？ {#what-is-a-delivery-template-}

配信の設定とパラメーターは、再利用できるように配信テンプレートに保存できます。

詳しくは、[Campaign v8 ドキュメント &#x200B;](https://experienceleague.adobe.com/docs/campaign/campaign-v8/send/create-templates.html?lang=ja){target="_blank"} を参照してください。

## Campaign で既存の HTML をインポートしてメールを簡単に作成できますか？ {#can-i-easily-import-an-existing-html-to-create-an-email-in-campaign-}

Adobe Campaign で電子メールを作成して送信するために、既存の HTML をワンクリックでインポートする方法があります。

詳しくは、[Campaign v8 ドキュメント &#x200B;](https://experienceleague.adobe.com/docs/campaign/campaign-v8/send/emails/defining-the-email-content.html?lang=ja#message-content){target="_blank"} を参照してください。

## Campaign DCE を使用してメールのコンテンツを作成する方法は？ {#how-to-use-campaign-dce-to-create-an-email-content-}

[Campaign デジタルコンテンツエディターでのメールのデザイン](../../web/using/use-case-creating-an-email-delivery.md)では、Campaign DCE を使用してメールをデザインする方法を、例を通して説明しています。

## 購読ベースのニュースレターを Campaign で作成するにはどうすればよいですか？ {#how-can-i-create-a-subscription-based-newsletter-in-campaign-}

[ニュースレターサービスの作成](../../delivery/using/managing-subscriptions.md)では、ニュースレターを作成し購読を管理するための主な手順を説明しています。

## メッセージをパーソナライズするにはどうすればよいですか？ {#how-can-i-personalize-messages-}

Adobe Campaign で配信されるメッセージは、コンテンツや外観をいくつかの方法でパーソナライズできます。さらに、受信者のプロファイルから取得した条件に基づいて、それらの方法を組み合わせることもできます。Adobe Campaign には、全体として次のようなパーソナライゼーション機能が備わっています。

* メッセージ形式のパーソナライズ：詳しくは、[Campaign v8 ドキュメント &#x200B;](https://experienceleague.adobe.com/docs/campaign/campaign-v8/send/emails/defining-the-email-content.html?lang=ja#message-content){target="_blank"} を参照してください。
* 動的パーソナライゼーションフィールドの挿入詳しくは、[Campaign v8 ドキュメント &#x200B;](https://experienceleague.adobe.com/docs/campaign/campaign-v8/send/personalize/personalization-fields.html?lang=ja){target="_blank"} を参照してください。
* 定義済みパーソナライゼーションブロックを挿入するか、独自のブロックを作成します。[Campaign v8 ドキュメント &#x200B;](https://experienceleague.adobe.com/docs/campaign/campaign-v8/send/personalize/personalization-blocks.html?lang=ja){target="_blank"} を参照してください。
* 条件付きコンテンツの作成[Campaign v8 ドキュメント &#x200B;](https://experienceleague.adobe.com/docs/campaign/campaign-v8/send/personalize/conditional-content.html){target="_blank"} を参照してください。

## 多言語メッセージを送信できますか？ {#can-i-send-multilingual-messages-}

受信者の環境設定や国などに応じて、多言語のメッセージを受信者に送信することができます。

これには、[条件](../../delivery/using/conditional-content.md)を使用して、受信者のプロファイルに応じて、メッセージの内容をローカライズし、パーソナライズする方法があります。また、ワークフローを使用して、優先言語のテストに応じて送信するメッセージのバージョンを選択することもできます。 [Campaign v8 ドキュメント &#x200B;](https://experienceleague.adobe.com/docs/campaign/automation/workflows/wf-activities/targeting-activities/split.html?lang=ja){target="_blank"} を参照してください。

## Web フォームをローカライズするにはどうすればよいですか？ {#how-can-i-localize-a-webform-}

Web アプリケーションは多言語にローカライズすることができます。翻訳のメカニズムについては、[この節](../../web/using/translating-a-web-form.md)を参照してください。
