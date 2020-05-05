---
title: Adobe Campaign Classic でのインタラクティブコンテンツの定義
description: Adobe Campaign Classic で AMP を使用してインタラクティブで動的な E メールコンテンツを定義する方法について説明します。
page-status-flag: never-activated
uuid: ddcc2e3b-e251-4a7a-a22a-28701522839f
contentOwner: sauviat
products: SG_CAMPAIGN/CLASSIC
audience: delivery
content-type: reference
topic-tags: sending-emails
discoiquuid: 2ea2747f-957f-41a9-a03f-20c03fa99116
index: y
internal: n
snippet: y
translation-type: ht
source-git-commit: 1815f9fc6063ec86d6c12ef492396e5afb82b3e1

---


# インタラクティブコンテンツの定義{#defining-interactive-content}

Adobe Campaign では、特定の条件下での動的な E メールの送信を可能にする、新しいインタラクティブ [AMP for Email](https://amp.dev/about/email/) フォーマットを試すことができます。

>[!IMPORTANT]
>
>* この機能は、Adobe Campaign のベータ版機能です。
>* AMP for Email は、開発者が動的でインタラクティブな E メールを作成できる新しいオープンソースフォーマットです。現在、Gmail、Outlook、Mail.ru など、いくつかの E メールプロバイダーでサポートされています。


現在実行可能なのは次の操作のみです。
* 適切に設定された特定のアドレスに AMP E メールを配信するテスト。
* 対応するプロバイダーに登録した後、AMP E メールを Gmail、Outlook または Mail.ru アドレスに配信。

AMP E メールのテストと送信について詳しくは、[AMP E メールのターゲティング](#targeting-amp-email)を参照してください。

この機能は、Adobe Campaign の専用パッケージで使用できます。使用するには、このパッケージをインストールする必要があります。インストールしたら、サーバーを再起動してパッケージを有効にします。

ハイブリッドおよびホストアーキテクチャの場合、パッケージは、[ミッドソーシングサーバー](../../installation/using/mid-sourcing-server.md)と[実行インスタンス](../../message-center/using/creating-a-shared-connection.md#execution-instance)を含むすべてのサーバーにインストールする必要があります。アカウント担当者にお問い合わせください。

Adobe Campaign での AMP の有効化方法および使用方法については、この[ビデオ](https://docs.adobe.com/content/help/en/campaign-learn/campaign-classic-tutorials/sending-messages/email-channel/defining-interactive-email-content-with-amp.html)をご覧ください。

## AMP for Email について {#about-amp-for-email}

**AMP for Email** は、新しいフォーマットで、メッセージ内に AMP コンポーネントを含めることで、アクションにつながるリッチなコンテンツにより E メールのエクスペリエンスを強化できます。E メール内で直接利用できる最新のアプリ機能により、受信者はメッセージ自体のコンテンツを動的に操作できます。

次に例を示します。
* AMP を使用して記述された E メールには、画像カルーセルなどのインタラクティブな要素を含めることができます。
* コンテンツはメッセージ内で最新の状態に保たれます。
* 受信者は、受信ボックスを離れることなく、フォームに返信するなどの操作を実行できます。

AMP for Email は、既存の E メールと互換性があります。メッセージの AMP バージョンは、HTML やプレーンテキストに加えて、新しい MIME パートとして E メールに埋め込まれ、すべての E メールクライアント間での互換性を確保します。

AMP for Email のフォーマット、仕様および要件について詳しくは、[AMP 開発者向けドキュメント](https://amp.dev/ja/documentation/guides-and-tutorials/learn/email-spec/amp-email-format/?format=email)を参照してください。

## Adobe Campaign で AMP for Email を使用するための重要な手順 {#key-steps-to-use-amp}

Adobe Campaign で AMP E メールを正常にテストして送信するには、以下の手順に従います。
1. **[!UICONTROL AMP サポート (ベータ)]** パッケージをインストールします。[Campaign 標準パッケージのインストール](../../installation/using/installing-campaign-standard-packages.md)を参照してください。
1. Adobe Campaign 内で E メールを作成し、AMP コンテンツを作成します。[Adobe Campaign での AMP E メールコンテンツの作成](#build-amp-email-content)を参照してください。
1. AMP フォーマットをサポートする E メールプロバイダーからのすべての配信要件に従っていることを確認します。[AMP for Email の配信要件](#amp-for-email-delivery-requirements)を参照してください。

   >[!NOTE]
   >
   >AMP for Email は、ベータ版機能としてテスト用途に使用できます。現在、この形式のテストをサポートしている E メールプロバイダーは少数です。

1. ターゲットを定義する場合、AMP フォーマットを表示できる受信者を選択していることを確認してください。[AMP E メールのターゲティング](#targeting-amp-email)を参照してください。

   >[!NOTE]
   >
   >現在、AMP E メールの配信をテストできるのは、適切に設定された特定の E メールアドレスに対して送信する場合または AMP ベータプログラムに参加する E メールプロバイダーに登録した後に限られています。

1. 通常どおりにメールを送信します。[AMP E メールの送信](#sending-amp-email)を参照してください。

## Adobe Campaign での AMP E メールコンテンツの作成 {#build-amp-email-content}

AMP フォーマットを使用して E メールを作成するには、以下の手順に従います。

>[!IMPORTANT]
>
>[AMP 開発者向けドキュメント](https://amp.dev/ja/documentation/guides-and-tutorials/learn/email_fundamentals/?format=email)に記載されている AMP for Email の要件と仕様に従ってください。また、[AMP for Email のベストプラクティス](https://amp.dev/ja/documentation/guides-and-tutorials/develop/amp_email_best_practices/?format=email)も参照してください。

1. E メール配信を作成する際に、任意のテンプレートを選択します。

   >[!NOTE]
   >
   >特定の AMP テンプレートには、製品リスト、カルーセル、二重のオプトイン、調査、高度なサーバーリクエストなど、使用できる主な機能の例が含まれています。

1. 「**[!UICONTROL AMP コンテンツ]**」タブをクリックします。

   ![](assets/amp_tab.png)

1. 必要に応じて AMP コンテンツを編集します。

   >[!NOTE]
   >
   >最初の AMP E メールの作成について詳しくは、[AMP 開発者向けドキュメント](https://amp.dev/ja/documentation/guides-and-tutorials/start/create_email/?format=email)を参照してください。

   例えば、AMP テンプレートの製品リストコンポーネントを使用して、サードパーティ製システムの製品リストを維持したり、Adobe Campaign 内部で製品リストを維持したりできます。価格やその他の要素を調整すると、受信者がメールボックスから再び E メールを開いたときに、その要素が自動的に反映されます。

1. 必要に応じて AMP コンテンツをパーソナライズします。通常、Adobe Campaign で HTML フォーマットに対しておこなう場合と同様に、パーソナライゼーションフィールドとパーソナライゼーションブロックを使用します。

   ![](assets/amp_tab_perso.png)

1. 編集が完了したら、AMP コンテンツ全体を選択して、[AMP Web ベースのバリデーター](https://validator.ampproject.org)または類似の Web サイトにコピー＆ペーストします。

   >[!NOTE]
   >
   >画面の上部にあるドロップダウンリストから **AMP4 EMAIL** を選択していることを確認します。

   ![](assets/amp_validator.png)

   エラーはインラインでフラグ付けされます。

   >[!NOTE]
   >
   >Adobe Campaign AMP エディターは、コンテンツの検証用には設計されていません。[AMP Web ベースのバリデーター](https://validator.ampproject.org)などの外部 Web サイトを使用して、コンテンツが正しいかどうかを確認します。

1. AMP コンテンツが検証に合格するまで、必要に応じて修正を加えます。

   ![](assets/amp_validator_pass.png)

1. 検証済みのコンテンツを [AMP Playground](https://playground.amp.dev) または類似の Web サイトにコピー＆ペーストして、コンテンツをプレビューします。

   >[!NOTE]
   >
   >画面の上部にあるドロップダウンリストから **AMP for Email** を選択していることを確認します。

   ![](assets/amp_playground.png)

   >[!NOTE]
   >
   >AMP コンテンツを Adobe Campaign で直接プレビューすることはできません。[AMP Playground](https://playground.amp.dev) などの外部 Web サイトを使用します。

1. Adobe Campaign に戻り、検証済みのコンテンツを「**[!UICONTROL AMP コンテンツ]**」タブにコピー＆ペーストします。

1. 「**[!UICONTROL HTML コンテンツ]**」タブまたは「**[!UICONTROL テキストコンテンツ]**」タブに切り替えて、これら 2 つのフォーマットのうち少なくとも 1 つに対してコンテンツを定義します。

   >[!IMPORTANT]
   >
   >AMP コンテンツに加えて HTML またはプレーンテキストバージョンが E メールに含まれていない場合、その E メールは送信できません。

## AMP for Email の配信要件 {#amp-for-email-delivery-requirements}

Adobe Campaign で AMP コンテンツを作成する場合、（受信者の E メールプロバイダー特有の）動的な E メールの配信条件を満たす必要があります。

現在、この形式のテストをサポートしている E メールプロバイダーは Gmail、Outlook、Mail.ru の 3 つです。

Gmail アカウントに対して AMP フォーマットで配信をテストするために必要なすべての手順と仕様については、該当する [Gmail](https://developers.google.com/gmail/ampemail?)、[Outlook ](https://docs.microsoft.com/ja-jp/outlook/amphtml/) および [Mail.ru](https://postmaster.mail.ru/amp) 開発者向けドキュメントを参照してください。

特に、以下の要件を満たす必要があります。
* [Gmail](https://developers.google.com/gmail/ampemail/security-requirements)、[Outlook](https://docs.microsoft.com/ja-jp/outlook/amphtml/security-requirements) および [Mail.ru](https://postmaster.mail.ru/amp/?lang=en#howto) 特有の AMP セキュリティ要件に従います。
* AMP MIME パートには、[有効な AMP ドキュメント](https://amp.dev/ja/documentation/guides-and-tutorials/learn/validation-workflow/validate_emails/?format=email)が含まれている必要があります。
* AMP MIME パートは 100 KB 未満である必要があります。

また、[Gmail のヒントと既知の制限事項](https://developers.google.com/gmail/ampemail/tips)や、[Outlook 向け AMP のベストプラクティス](https://docs.microsoft.com/ja-jp/outlook/amphtml/best-practices)も参照してください。

## AMP E メールのターゲティング {#targeting-amp-email}

AMP for Email は、ベータ版機能として使用できます。現在、AMP E メールの送信は、以下の 2 つの手順でテストできます。

1. Adobe Campaign では、適切に設定された E メールアドレスに対して AMP を利用した動的な E メールを配信し、その内容と動作を検証できます。[選択したアドレスに対する AMP E メール配信のテスト](#testing-amp-delivery-for-selected-addresses)を参照してください。
1. テストが完了すると、該当する E メールプロバイダーに登録して、送信者ドメインをホワイトリストに登録することで、AMP for Email ベータプログラムの一環として配信またはキャンペーンを送信できます。[E メールロバイダーへの登録と AMP E メールの配信](#delivering-amp-emails-by-registering)を参照してください。

### 選択したアドレスに対する AMP E メール配信のテスト {#testing-amp-delivery-for-selected-addresses}

Adobe Campaign から選択した E メールアドレスへの動的なメッセージの送信をテストできます。

>[!NOTE]
>
>現在、AMP フォーマットのテストは、Gmail、Outlook および Mail.ru でのみサポートされています。

Gmail および Outlook の場合、まずはターゲットとする Gmail および Outlook アカウント用に Adobe Campaign からの配信に使用する送信者のアドレスをホワイトリストに登録する必要があります。

手順は次のとおりです。
1. 該当する E メールプロバイダーに対して、動的な E メールを有効にするオプションがオンになっていることを確認します。
1. 配信の「**[!UICONTROL 送信者]**」フィールドに表示された送信者のアドレスをコピーし、E メールプロバイダーのアカウント設定の適切なセクションに貼り付けます。

詳しくは、[Gmail](https://developers.google.com/gmail/ampemail/testing-dynamic-email) 開発者向けドキュメントおよび [Outlook](https://docs.microsoft.com/ja-jp/outlook/amphtml/register-outlook#individual-mailbox-registration) 開発者向けドキュメントを参照してください。

![](assets/amp_from_field.png)

Mail.ru アドレスへの AMP E メールの送信をテストするには、[Mail.ru 開発者向けドキュメント](https://postmaster.mail.ru/amp/?lang=en#howto)（**ユーザーの場合**&#x200B;の節）の手順に従います。

### E メールロバイダーへの登録と AMP E メールの配信 {#delivering-amp-emails-by-registering}

動的な E メールの配信は、送信者ドメインをホワイトリストに登録するために、AMP ベータプログラムに参加する E メールプロバイダーに登録することで、テストできます。

>[!NOTE]
>
>現在、AMP フォーマットは、Gmail、Outlook および Mail.ru でのみサポートされています。

複数のアドレスでテストが完了したら、任意の Gmail または Outlook アドレスにAMP E メールを送信できます。そのためには、Google または Microsoft に適切に登録し、回答を待つ必要があります。[Gmail](https://developers.google.com/gmail/ampemail/register) 開発者向けドキュメントおよび [Outlook](https://docs.microsoft.com/ja-jp/outlook/amphtml/register-outlook#global-registration) 開発者向けドキュメントに記載されている手順に従います。登録が完了すると、許可された送信者になります。

AMP E メールを Mail.ru アドレスに送信するには、[Mail.ru 開発者向けドキュメント](https://postmaster.mail.ru/amp/?lang=en#howto)に記載されている要件と手順に従います（**E メールの送信者の場合**&#x200B;の節を参照）。

## AMP E メールの送信 {#sending-amp-email}

AMP コンテンツとフォールバックの準備が整い、互換性のあるターゲットを定義したら、通常どおりに E メールを送信できます。

現在、AMP フォーマットは、Gmail、Outlook および Mail.ru でのみ、特定の条件下でサポートされています。他の E メールプロバイダーからのアドレスをターゲットにすることはできますが、E メールの HTML またはプレーンテキストバージョンを受信することになります。

>[!IMPORTANT]
>
>AMP コンテンツに加えて HTML またはプレーンテキストバージョンが E メールに含まれていない場合、その E メールは送信できません。

合致する受信者は、メールボックスに E メールの AMP バージョンが表示されます。

例えば、E メールに製品リストを含めた場合、サードパーティ製システムで価格を編集すると、受信者がメールボックスで E メールを再び開くたびに、価格が自動的に調整されます。

>[!NOTE]
>
>特定のドメインが AMP E メールを受信するのを防ぐためのメール処理ルールを作成できます。[E メールフォーマットの管理](../../installation/using/email-deliverability.md#managing-email-formats)を参照してください。
>
>デフォルトでは、「**[!UICONTROL AMP インクルージョン]**」オプションは「**[!UICONTROL いいえ]**」に設定されています。
