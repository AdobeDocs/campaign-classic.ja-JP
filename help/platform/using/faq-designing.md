---
product: campaign
title: メッセージデザインに関する FAQ
description: Campaign Classic に関する FAQ
feature: Audiences, Troubleshooting
badge-v7-only: label="v7" type="Informative" tooltip="Campaign Classic v7 にのみ適用されます"
audience: platform
content-type: reference
topic-tags: starting-with-adobe-campaign
exl-id: 48926e87-03d9-4aa0-89cb-e3fb4f99c1f5
source-git-commit: 3a9b21d626b60754789c3f594ba798309f62a553
workflow-type: tm+mt
source-wordcount: '348'
ht-degree: 100%

---

# メッセージデザインに関する FAQ {#design-messages-faq}



Adobe Campaign でオムニチャネルメッセージをデザインするための主な手順について説明します。

## Campaign でメールをデザインする際の具体的なガイドラインはありますか？ {#are-there-specific-guidelines-when-designing-emails-with-campaign-}

E メールのデザインを始める前に、配信のデザインと Adobe Campaign での送信に関する概念とベストプラクティスを理解しておくことをお勧めします。

[詳しくはここをクリック](../../delivery/using/delivery-best-practices.md)してください。

## 配信テンプレートとは何ですか？ {#what-is-a-delivery-template-}

配信の設定とパラメーターは、再利用できるように配信テンプレートに保存できます。

[詳しくはここをクリック](../../delivery/using/about-templates.md)してください。

## Campaign で既存の HTML をインポートしてメールを簡単に作成できますか？ {#can-i-easily-import-an-existing-html-to-create-an-email-in-campaign-}

Adobe Campaign で電子メールを作成して送信するために、既存の HTML をワンクリックでインポートする方法があります。

[詳しくはここをクリック](../../delivery/using/defining-the-email-content.md#message-content)してください。

## Campaign DCE を使用してメールのコンテンツを作成する方法は？ {#how-to-use-campaign-dce-to-create-an-email-content-}

[Campaign デジタルコンテンツエディターでのメールのデザイン](../../web/using/use-case--creating-an-email-delivery.md)では、Campaign DCE を使用してメールをデザインする方法を、例を通して説明しています。

## 購読ベースのニュースレターを Campaign で作成するにはどうすればよいですか？ {#how-can-i-create-a-subscription-based-newsletter-in-campaign-}

[ニュースレターサービスの作成](../../delivery/using/managing-subscriptions.md)では、ニュースレターを作成し購読を管理するための主な手順を説明しています。

## メッセージをパーソナライズするにはどうすればよいですか？ {#how-can-i-personalize-messages-}

Adobe Campaign で配信されるメッセージは、コンテンツや外観をいくつかの方法でパーソナライズできます。さらに、受信者のプロファイルから取得した条件に基づいて、それらの方法を組み合わせることもできます。Adobe Campaign には、全体として次のようなパーソナライゼーション機能が備わっています。

* メッセージ形式のパーソナライズ：[詳しくはここをクリック](../../delivery/using/defining-the-email-content.md#message-content)してください。
* パーソナライゼーションフィールドの動的な挿入：[詳しくはここをクリック](../../delivery/using/personalization-fields.md)してください。
* 定義済みパーソナライゼーションブロックを挿入するか、独自のブロックを作成します。[詳しくはここをクリック](../../delivery/using/personalization-blocks.md)してください。
* 条件付きコンテンツの作成：[詳しくはここをクリック](../../delivery/using/conditional-content.md)してください。また、[この節](../../delivery/using/conditional-content.md)も参照してください。

## 多言語メッセージを送信できますか？ {#can-i-send-multilingual-messages-}

受信者の環境設定や国などに応じて、多言語のメッセージを受信者に送信することができます。

これには、[条件](../../delivery/using/conditional-content.md)を使用して、受信者のプロファイルに応じて、メッセージの内容をローカライズし、パーソナライズする方法があります。[ワークフロー](../../workflow/using/split.md)を使用して、優先言語のテストに応じて、送信するメッセージのバージョンを選択することもできます。

## Web フォームをローカライズするにはどうすればよいですか？ {#how-can-i-localize-a-webform-}

Web アプリケーションは多言語にローカライズすることができます。翻訳のメカニズムについては、[この節](../../web/using/translating-a-web-form.md)を参照してください。
