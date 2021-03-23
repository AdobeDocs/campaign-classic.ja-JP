---
solution: Campaign Classic
product: campaign
title: Adobe Campaign Classic の配信品質について
description: Adobe Campaign Classic の配信品質管理について説明します。
audience: delivery
content-type: reference
topic-tags: deliverability-management
translation-type: tm+mt
source-git-commit: d6a581ae86e50c17ac20fe54baf305b864e11790
workflow-type: tm+mt
source-wordcount: '774'
ht-degree: 63%

---


# メッセージコンテンツの制御 {#control-message-content}

電子メールがお客様の受信者に届き、電子メールの配信速度を向上させるためには、Eメールが様々なルールを尊重する必要があります。 そうしないと、特定のメッセージの内容がスパムとして検出される場合があります。 Adobe Campaignには、コンテンツをこれらのルールに準拠させるためのツールがいくつか用意されています。

メッセージの内容を設計する際は、次の原則に従います。

* [送信者のアドレス](#sender-address):このアドレスは、送信者を明示的に識別する必要があります。ドメインは、送信者によって所有され、登録されている必要があります。ドメイン登録は、プライベートにしません。
* [個人設定](#personalization):コンテンツをパーソナライズし、受信者ごとの送信時間を定義すると、メッセージが開かれる可能性が高くなります。
* 画像とテキスト：適切なテキスト/画像の比率を考慮します（例えば、60%テキストと40%画像）。
* [購読解除](#opt-out) リンクとランディングページ:購読解除リンクは必須です。購読解除リンクが表示され、有効である必要があり、フォームが機能する必要があります。
* プレビュー:Adobe Campaignが提供するツールを使用して、電子メールの内容を確認し、最適化します（[受信トレイレンダリング](#message-responsiveness)、[SpamAssin](#spamassassin)）。

コンテンツのデザイン時に配信品質を最適化するためのその他のヒントについては、『Adobe配信品質のベストプラクティスガイド』を参照してください。[](https://experienceleague.adobe.com/docs/deliverability-learn/deliverability-best-practice-guide/content-best-practices-for-optimal-delivery.html)

>[!NOTE]
>
>電子メールコンテンツの編集について詳しくは、[電子メールコンテンツ](../../delivery/using/defining-the-email-content.md)の定義および[パーソナライズされたコンテンツ](../../delivery/using/design-and-personalize.md)の作成を参照してください。

## 送信者のアドレス {#sender-address}

特定のISPは、メッセージを受け付ける前に、送信者のアドレス(**[!UICONTROL From]**)の有効性をチェックします。 正しくない形式のアドレスは、受信サーバーによって拒否される可能性があります。

インスタンスレベル（**[!UICONTROL ツール／詳細設定／デプロイウィザード...]**...）または最も頻繁に使用されるシナリオで、正しいアドレスが指定されていることを確認する必要があります。

詳しくは、[送信者の定義](../../delivery/using/defining-the-email-content.md)を参照してください。

## パーソナライゼーション {#personalization}

受信者の体験を向上させ、電子メールを開くように、Adobe Campaignを使用してメッセージをパーソナライズできます。

Adobe Campaignでのパーソナライゼーションフィールドの使用に関する詳細は、[このセクション](../../delivery/using/personalization-fields.md)を参照してください。

コンテンツを作成する際のパーソナライゼーションを最適化するためのヒントについては、[このセクション](../../delivery/using/design-and-personalize.md#optimize-personalization)を参照してください。

## オプトアウトリンクとフォーム {#opt-out}

デフォルトでは、メッセージが分析される場合、[タイポロジルール](../../delivery/using/steps-validating-the-delivery.md#validation-process-with-typologies)でオプトアウトリンクが含まれているかどうかがチェックされ、見つからない場合は警告が表示されます。このルールを変更して、単純な警告ではなくエラーを表示し、このリンクなしに配信がおこなわれないようにすることができます。

毎回、送信前に、オプトアウトリンクが適切に機能することを確認する必要があります。例えば、配達確認を送信する際に、リンクが有効であること、フォームがオンラインであること、「**[!UICONTROL 今後のこの受信者への連絡は不要]**」フィールドが「**[!UICONTROL はい]**」に変更されることを確認します。リンクの入力時やフォームの変更時にヒューマンエラーが発生する可能性は常にあるので、このチェックは体系的におこなう必要があります。

オプトアウトリンクを挿入する方法については、[この節](../../delivery/using/personalization-blocks.md#personalization-blocks-example)を参照してください。

オプトアウトリンクをクリックした受信者が選択を確認できないとしても、配信開始後に購読解除に関する問題が検出された場合は購読解除を手動で実行できます（一括更新機能を使用するなど）。

原則として、例えば E メールアドレスや名前などのフィールドを入力するよう求めることで、オプトアウトしたい受信者を邪魔しないでください。フォームには 1 つの検証ボタンのみを表示し、紐付けは暗号化された識別子にのみ実行します。

追加の確認のリクエストは信頼できません。ユーザーが 2 つの E メールアドレスを同じボックスにリダイレクトさせている可能性があります（firstname.lastname@club.com と firstname.lastname@internet-club.com など）。受信者が最初のアドレスのみを覚えていて、もう 1 つのアドレスに送信されたメッセージを使用して購読解除する場合、暗号化された識別子と入力された E メールアドレスが一致しないので、フォームはこれを拒否します。

## 受信ボックスレンダリング {#message-responsiveness}

メッセージを送信する前に、異なるデバイスでメッセージがどのように表示されるかを確認して、メッセージの応答性をテストできます。 これは、様々なWebクライアント、Webメール、デバイスに最適な方法で表示されるようにするためです。

この確認のために、Adobe Campaign ではレンダリングをキャプチャして専用のレポートで利用できるようにしています。これにより、異なるコンテキストで受信される可能性のある送信済みのメッセージをプレビューできます。

詳しくは、[受信ボックスレンダリング](../../delivery/using/inbox-rendering.md)を参照してください。

## SpamAssassin {#spamassassin}

SpamAssassin と連携するように Adobe Campaign を設定できます。連携することで、E メールを評価し、受信時に使用されるスパム対策ツールによってメッセージがスパムと見なされるリスクがあるかどうかを判断できます。

配信を開始する前に、「**[!UICONTROL プレビュー]**」タブでリスクを評価できます。テストの結果が警告メッセージとして表示されます。

詳しくは、[この節](../../delivery/using/spamassassin.md)を参照してください。