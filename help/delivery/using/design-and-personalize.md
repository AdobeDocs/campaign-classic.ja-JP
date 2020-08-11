---
title: パーソナライズされたコンテンツの作成
seo-title: パーソナライズされたコンテンツの作成
page-status-flag: never-activated
uuid: a540efc7-105d-4c7f-a2ee-ade4d22b3445
contentOwner: sauviat
products: SG_CAMPAIGN/CLASSIC
audience: delivery
content-type: reference
topic-tags: deliveries-best-practices
discoiquuid: 0cbc4e92-482f-4dac-a1fb-b738e7127938
index: y
internal: n
snippet: y
translation-type: tm+mt
source-git-commit: c804745ae58a9bded885ac5aef32f019f43e82be
workflow-type: tm+mt
source-wordcount: '1280'
ht-degree: 55%

---


# パーソナライズされたコンテンツの作成 {#build-personalized-content}

メッセージコンテンツを設計するときは、配信の実行を妨げる可能性がある一般的な問題が発生しないようにします。Most of the time, possible errors are related to [personalization](../../delivery/using/about-personalization.md), [formatting](../../delivery/using/defining-the-email-content.md#message-content) and [images](../../delivery/using/defining-the-email-content.md#adding-images).

## パーソナライゼーションの最適化 {#optimize-personalization}

配信の実行を妨げる可能性がある一般的な問題を回避し、受信者のエクスペリエンスを向上させるために、Adobe Campaign でメッセージをパーソナライズできます。

Adobe Campaignデータベースに格納された受信者のデータを使用したり、トラッキング、ランディングページ、購読などを通じて収集されたデータを使用したりできます。
パーソナライゼーションの基本につ [いては、この節に説明します](../../delivery/using/personalization-fields.md)。

エラーを避けるために、メッセージコンテンツが適切に設計されていることを確認します。多くのエラーはパーソナライゼーションに関係しています。

**ヒント**:サードパーティベンダーが提供する外部ファイルからのパーソナライゼーションフィールドで、外部HTMLコンテンツが誤っている場合があります。 この問題を避けるには、構文、タグの使い方、使用されている文字などを確認します。例えば、Adobe Campaign のパーソナライゼーションタグは必ず &lt;%=table.field%> という形式で使用します。詳しくは、[この節](../../delivery/using/about-personalization.md)を参照してください。

パーソナライゼーションブロック内でのパラメーターの使い方が間違っていると、問題になる場合があります。例えば、JavaScript の変数は次のように使用する必要があります。

    &lt;%
    
    var brand = &quot;xxx&quot;
    
    %>

For more on personalization blocks, refer to the [this section](../../delivery/using/personalization-blocks.md).

配信の準備分析を向上させるために、ワークフローでパーソナライゼーションデータを準備できます。 これは、パーソナライゼーションデータが外部テーブルからFederated Data Access(FDA)を介して送られる場合に特に使用します。 このオプションについては、この節で説明 [します](../../delivery/using/personalization-fields.md#optimizing-personalization)

## 最適化されたコンテンツの作成 {#optimize-content}

E メールを作成する際は、以下の一般的なベストプラクティスを考慮してください。

* デザインをシンプルにする

* モバイルユーザーに注意

* 完全な画像ベースの電子メールを避ける

* 電子メールセーフフォントの使用

* 特殊文字のエンコード

### 件名

Work on the [subject line](../../delivery/using/defining-the-email-content.md#message-content) to improve open rates:

* 長すぎる件名は避けます。最大50文字を使用

* 「free」や「オファー」など、スパムと見なされる可能性のある繰り返しの単語を使用しないでください。

* 大文字や、「!」、「£」、「€」、「$」などの特殊文字は使用しないでください。

### ミラーページ

常にミラーページリンクを含めます。 電子メールの先頭に優先順位を付けます。 [詳細情報](../../delivery/using/sending-messages.md#generating-the-mirror-page)

### Unsubscription link

購読解除リンクは不可欠です。購読解除リンクが表示され、有効である必要があり、フォームが機能する必要があります。By default, when the message is analyzed, a [typology rule](../../delivery/using/steps-validating-the-delivery.md#validation-process-with-typologies) checks whether an opt-out link has been included and generates a warning if it is missing.

**ヒント**:人為的エラーは常に可能なので、送信のたびにオプトアウトリンクが正しく機能することを確認してください。 例えば、配達確認を送信するときは、リンクが有効であること、フォームがオンラインであること、「今後のこの受信者への連絡は不要」フィールドが「はい」に変更されていることを確認します。

この節では、オプトアウトリンクを挿入する方法 [について説明します](../../delivery/using/personalization-blocks.md#personalization-blocks-example)。

### E メールのサイズ

パフォーマンスや配信品質の問題を回避するため、電子メールの最大サイズは約35 KB **です**。 To check the message size, go the **[!UICONTROL Preview]** tab and choose a test profile. メッセージが生成されると、サイズが右上隅に表示されます。

E メールの制限を守るには、以下を考慮してください。

* 重複したスタイルまたは未使用のスタイルを削除する

* 一部の電子メールコンテンツをランディングページに移動

* コードの縮小

最後の送信の前に、変更をテストしてください

### SMS の長さ

デフォルトでは、SMS の文字数は GSM（Global System for Mobile Communications）標準に準じています。GSM エンコードを使用する SMS メッセージは 160 文字以内に制限されています。複数の部分に分けて送信されるメッセージの場合は、SMS 1 件につき 153 文字以内です。

表記変換では、SMS の特定の文字が GSM 標準に準じていない場合に、別の文字に置き換えられます。パーソナライゼーションフィールドを SMS メッセージのコンテンツに入れると、GSM エンコードに対応していない文字が含まれる場合があります。文字の表記変換を許可するには、対応する&#x200B;**[!UICONTROL 外部アカウント]**&#x200B;の「SMPP チャネル設定」タブにあるチェックボックスをオンにします。Learn more [in this section](../../delivery/using/sms-channel.md#creating-an-smpp-external-account).

**ヒント**:

* SMS メッセージのすべての文字をそのまま維持するには（例えば、固有名詞が改変されないようにするには）、表記変換を有効にしないでください。

* ただし、SMS メッセージに GSM 標準に準じていない文字が多数含まれる場合は、表記変換を有効にしてメッセージ送信のコストを抑えることができます。

Learn more [in this section](../../delivery/using/sms-channel.md#about-character-transliteration).

## フォーマット {#formatting}

フォーマットに関する一般的なエラーを回避するには、次の点を確認します。

* Correct **date formatting**: Adobe Campaign provides date formatting functions for the JavaScript templates and XSL stylesheets. [詳細情報](../../delivery/using/formatting.md#date-display)

* 電子メールでの **認証文字の使用** :電子メールアドレスに有効な文字のリストは、&quot;XtkEmail_Characters&quot;オプションで定義されます。 この節では、キャンペーンオプションにアクセス [する方法を説明します](../../installation/using/configuring-campaign-options.md)。 特殊文字を適切に処理するには、Adobe Campaign を Unicode でインストールする必要があります。

* Configuration of **Email Authentication**:電子メールヘッダーにDKIM署名が含まれていることを確認します。 DKIM（Domain Keys Identified Mail）認証を使用すると、受信 E メールサーバーは、送信したと主張する個人または法人によってメッセージが実際に送信されたかと、メッセージコンテンツが最初に送信された（および DKIM が「署名された」）ときと受信時で変更されているかどうかを検証できます。この標準は、通常、「From」または「Sender」ヘッダーのドメインを使用します。詳しくは、[この節](../../delivery/using/technical-recommendations.md#dkim)を参照してください。

### レスポンシブ電子メールデザイン

レスポンシブデザインでは、電子メールが開かれたデバイスに合わせて最適にレンダリングされます。

* Web HTMLではなくレスポンシブ電子メールHTMLを使用する

* プレビューモードを使用して配達確認を送信し、可能な限り多くのデバイスでレンダリングをテストします

* The Adobe Campaign Classic Digital Content Editor (DCE) module includes some responsive design formatted templates for mobile available via **[!UICONTROL Resources]** > **[!UICONTROL Templates]** > **[!UICONTROL Content templates]**. この記事 [の詳細情報](https://theblog.adobe.com/responsive-email-design-101/)

## 画像の管理 {#manage-images}

画像を使用する場合は、次のガイドラインに従ってください。

### 画像のブロックを禁止

一部の E メールクライアントはデフォルトで画像をブロックし、一部のユーザーはデータ使用時に保存する画像をブロックするように設定を変更します。したがって、画像をダウンロードしないと、メッセージ全体が失われる可能性があります。 これを回避するには：

* コンテンツと画像とテキストのバランスを取ります。画像のみの E メールは避けます。

* 画像にテキストを含める必要がある場合は、代替テキストやタイトルテキストを使用して、必ずメッセージが伝わるようにします。代替テキストやタイトルテキストのスタイルを設定して、外観を改善します。

* 背景画像は一部の E メールクライアントでサポートされていないので、使用しないようにします。

### 画像をレスポンシブにする

画像をレスポンシブでサイズ変更可能にします。これは作成に時間がかかるので、コストに影響する可能性があります。

### 絶対画像参照の使用

外部からアクセスできるようにするには、キャンペーンにリンクされた電子メールやパブリックリソースで使用される画像が、外部からアクセス可能なサーバー上に存在している必要があります。

* インスタンスの設定でパブリックリソースの管理が有効になっているかどうかを確認できます。[詳細情報](../../installation/using/deploying-an-instance.md#managing-public-resources)

* 配信ウィザードで、画像を含んだ HTML ページをインポートするか、HTML エディターの&#x200B;**[!UICONTROL 画像]**&#x200B;アイコンを使用して直接画像を挿入します。[詳細情報](../../delivery/using/defining-the-email-content.md#adding-images)

* 画像が表示されない場合は、その画像がサーバー上で使用できることを確認してください。そのためには、配信から「ソース」タブをクリックします。使用する画像を探し、各画像の URL をコピーして Web ブラウザーに貼り付けます。画像が表示されない場合は、IT 管理者か、配信コンテンツを提供しているサードパーティベンダーに問い合わせてください。

## メッセージのプレビュー {#preview-msg}

Adobeでは、メッセージをプレビューして、個人設定と受信者に対する配信の表示方法を確認することをお勧めします。

* In the delivery wozard, the **[!UICONTROL Preview]** sub-tab lets you view the rendering of each content for a recipient. コンテンツのパーソナライゼーションフィールドや条件付き要素は、選択したプロファイル内の対応する情報で置き換えられます。[詳細情報](../../delivery/using/defining-the-email-content.md#message-content)

* 各プレビュー中に自動的にアンチスパムチェックを行う。 「 **[!UICONTROL プレビュー]** 」サブタブで、「 [SpamAssicin](../../delivery/using/spamassassin.md) spam scoring」をチェックします。  「 **[!UICONTROL 詳細…]** 」をクリックして、警告の詳細を確認します。  これを行う前に、SpamAssinが正しくインストールされ、Adobe Campaignアプリケーションサーバーに設定されていることを確認してください。 [詳細情報](../../installation/using/configuring-spamassassin.md)
