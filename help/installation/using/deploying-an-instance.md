---
title: インスタンスのデプロイ
seo-title: インスタンスのデプロイ
description: インスタンスのデプロイ
seo-description: null
page-status-flag: never-activated
uuid: 5694b07a-6c1c-45a3-8a22-fd9da163c28c
contentOwner: sauviat
products: SG_CAMPAIGN/CLASSIC
audience: installation
content-type: reference
topic-tags: initial-configuration
discoiquuid: 71fc8bfc-40e0-4592-a540-bd6807ded3a0
index: y
internal: n
snippet: y
translation-type: tm+mt
source-git-commit: a2cb740fe9b71435f602b738bd270fd3a0954901

---


# インスタンスのデプロイ{#deploying-an-instance}

>[!NOTE]
>
>サーバー側の設定は、アドビがホストするデプロイメントに対してのみ、アドビが実行できます。 各デプロイメントの詳細については、「 [ホスティングモデル](../../installation/using/hosting-models.md) 」の節または [この記事を参照してください](https://helpx.adobe.com/jp/campaign/kb/acc-on-prem-vs-hosted.html)。

## デプロイメントウィザード {#deployment-wizard}

Adobe Campaignクライアントコンソールで使用できるグラフィカルウィザードを使用すると、接続先のインスタンスのパラメータを定義できます。

デプロイメントウィザードを開始するには、 **ツール/詳細/デプロイメントウィザード**&#x200B;を選択します。

![](assets/s_ncs_install_deployment_wiz_01.png)

設定手順は、以下のとおりです。

1. [一般パラメーター](#general-parameters)
1. [電子メールチャネルパラメーター](#email-channel-parameters)
1. [バウンスされた電子メールの管理](#managing-bounced-emails)
1. [トラッキング設定](#tracking-configuration)
1. [モバイルチャネルパラメーター](#mobile-channel-parameters)
1. [地域設定](#regional-settings)
1. [インターネットからのアクセス](#access-from-the-internet)
1. [パブリックリソースの管理](#managing-public-resources)
1. [データの削除](#purging-data)

## 一般パラメーター {#general-parameters}

配置ウィザードの最初の手順では、インスタンスに関する一般情報を入力できます。

![](assets/s_ncs_install_deployment_wiz_02.png)

### 一般情報 {#general-information}

ウィンドウの下部では、アクティブにするオプションを選択できます。

* **[!UICONTROL Customer identifier used in billing]** : これは、インスタンスの名前とバージョン番号です。
* **[!UICONTROL Common name of the customer]** : 会社名を含む文字列を入力します。 この情報は、購読解除リンクで使用できます。
* **[!UICONTROL Namespace]** : 小文字の短い識別子を入力します。 目的は、アップグレードの場合に、特定の設定と工場出荷時の設定を区別することです。 デフォルトの名前空間は **cus** — （お客様向け）です。

### 技術的なオプション {#technical-options}

ウィンドウの下部では、アクティブにするオプションを選択できます。

次のオプションを使用できます。

* **[!UICONTROL Email channel]** : 電子メール配信をアクティブにするには 「 [電子メールチャネルのパラメーター](#email-channel-parameters)」を参照してください。
* **[!UICONTROL Tracking]** : ターゲット母集団（開きとクリック）の追跡を有効にする。 「 [トラッキングの設定](#tracking-configuration)」を参照してください。
* **[!UICONTROL Managing bounced emails]** : 受信メールの受信に使用するPOPアカウントを定義する場合。 「バウンス電子メールの [管理](#managing-bounced-emails)」を参照してください。
* **[!UICONTROL LDAP integration]** : LDAPディレクトリを介したユーザー認証を設定する。 「LDAP [経由の接続」を参照してください](../../installation/using/connecting-through-ldap.md)。

## 電子メールチャネルパラメーター {#email-channel-parameters}

次の手順では、メッセージヘッダーに表示する情報を定義します。

これらのパラメーターは、配信テンプレートーで過負荷になる場合や、各配信ーに対して個別に（必要な権限を持つユーザーの場合）設定できます。

### 配信 E メールのパラメーター {#parameters-for-delivered-emails}

![](assets/s_ncs_install_deployment_wiz_04.png)

次のパラメーターを指定します。

* **[!UICONTROL Sender name]** : 送信者の名前、
* **[!UICONTROL Sender address]** : 送信者のアドレス。
* **[!UICONTROL Reply address text]** : 受信者が電子メールクライアントソフトウェアのボタンをクリックしたときに使用される、カスタマイズ可能な名前。 **[!UICONTROL Reply]**
* **[!UICONTROL Reply address]** : 受信者が電子メールクライアントソフトウェアでボタンをクリックしたときに使用する電子メールアドレス。 **[!UICONTROL Reply]**
* **[!UICONTROL Error address]** : エラーのあるメッセージの電子メールアドレス。 これは、存在しないターゲットアドレスが原因でAdobe Campaignサーバーが受信した電子メールなど、バウンスメールの処理に使用する技術的なアドレスです。

これに加えて、送信者アドレスとエラーアドレスに対して認証された **マスク** を指定できます。 必要に応じて、これらのマスクはコンマで区切ることができます。 この設定はオプションです。 フィールドを入力すると、Adobe Campaignは、配信時(分析中、アドレスに変数が含まれない場合)にそのアドレスが有効であるかどうかを確認します。 このオペレーティングモードでは、配信の問題を引き起こす可能性のあるアドレスが使用されていないことを確認します。 配信アドレスは、配信サーバーで設定する必要があります。

### アドレスに使用できる文字 {#characters-authorized-in-addresses}

<!--This window enables you to define, for all email campaigns, the delivery and address-quality management options.-->

Adobe Campaignデータベースでは、すべての電子メールアドレスを次のように作成する必要があります。 `x@y.z`. **x**、 **y****、** zの各文字は空にできず、許可されていない文字を含めてはいけません。

データベースの電子メールフィールドで、許可された文字（「データポリシー」）をここで定義できます。 リストに含まれない文字は禁止され、インターフェイス、Webフォーム、データの読み込みを介してデータベースに情報を入力する場合に拒否されます。

次の2つのリストを使用できます。 **ヨーロッパのみ** 、または **米国のみ**。 必要に応じて、他の文字を追加できます。

### 配信パラメーター {#delivery-parameters}

「 **Advanced parameters...** 」リンクを使用すると、配信オプション、再試行にリンクされたパラメーター、強制隔離にアクセスできます。

![](assets/s_ncs_install_deployment_wiz_05.png)

このウィンドウでは、すべての電子メールキャンペーンに対して、配信とアドレスの質の管理オプションを定義できます。

次のオプションを使用できます。

* **[!UICONTROL Delivery duration of messages]** : これ以降、配信は停止されます（デフォルトでは5日）。
* **[!UICONTROL Online resources validity duration]** : ミラーページを生成するために受信者プロファイルからの情報が保持される時間、
* **[!UICONTROL Exclude recipients who no longer wish to be contacted]** : このオプションを選択すると、ブラックリスト登録済み受信者に接続されません。
* **[!UICONTROL Automatically ignore doubles]** : このオプションを選択すると、重複アドレスは配信されません。

### Retry parameters {#retry-parameters}

リカバリに関する情報は、「 **リカバリ期間** 」と「リカバリ **数** 」の各フィールドに表示されます。 受信者が未到達の場合（受信トレイがいっぱいの場合など）は、デフォルトで、プログラムが5回連絡を試み、各試行の間隔を1時間とします(最大配信時間)。 これらの値は、必要に応じて変更できます。

### 強制隔離パラメーター {#quarantine-parameters}

強制隔離の設定オプションは次のとおりです。

* **[!UICONTROL Duration between two significant errors]** : 値を入力（既定では&quot;1d&quot;）: 1 day)を指定して、失敗した場合にエラーカウンターを増やすまでのアプリケーションの待機時間を定義します。
* **[!UICONTROL Maximum number of errors before quarantine]** : この値に達すると、電子メールアドレスが隔離されます（デフォルトは「5」です）。 アドレスは6番目のエラー時に隔離されます)。 これは、連絡先が後続の配信から自動的に除外されることを意味します。

## バウンスされた電子メールの管理 {#managing-bounced-emails}

バウンスメールは、配信エラーを認定するために非常に重要です。 これらのエラーは、ルールで原因が特定されたら、NP@Iに分類されます。

この手順は、導入ウィザードの最初の段階で **電子メールチャネル** と **バウンスのメール** 管理オプションが選択されている場合にのみ使用できます。 Refer to [General parameters](#general-parameters).

この段階では、バウンスメールを管理するための設定を定義できます。

![](assets/s_ncs_install_deployment_wiz_06.png)

### 受信メールの取得に使用するPOPアカウント {#pop-account-used-to-retrieve-incoming-mails}

受信電子メールを取得するためにアカウントに接続するパラメーターを指定します。

* **[!UICONTROL Label]** : 以下に示すすべてのパラメーターを含む名前、
* **[!UICONTROL Server]** : バウンスメール（受信メール）の取得に使用するサーバ、
* **[!UICONTROL Security]** : 必要に応じて、ドロップダウンリスト **[!UICONTROL SSL]** から選択します。
* **[!UICONTROL Port]** : サーバポート（通常は110）、
* **[!UICONTROL Account]** : バウンスメールに使用するアカウント名、
* **[!UICONTROL Password]** : アカウントに関連付けられているパスワード。

POP設定を指定したら、「 **Test** 」をクリックして、設定が正しいことを確認します。

### 未処理のバウンスメール {#unprocessed-bounce-mails}

バウンスはAdobe Campaignによって自動的に処理され、[ **管理] > [キャンペーン管理] > [配信不能管理] > [配信ログ資格** ]の順に選択したルールが適用されます。 For more on this, refer to [Bounce mail management](../../delivery/using/understanding-delivery-failures.md#bounce-mail-management).

未処理のバウンスは、Adobe Campaignインターフェイスに表示されません。 これらは、次のフィールドを使用してサードパーティのメールボックスに転送されない限り、自動的に削除されます。

* **[!UICONTROL Forwarding address]** : Adobe Campaignプラットフォームによって収集されたすべてのエラーメッセージ（処理済みまたは未処理のメッセージ）をサードパーティのアドレスに転送するには、このフィールドに入力します。
* **[!UICONTROL Address for errors]** : inMailプロセスで認定できなかったエラーメッセージのみをサードパーティのアドレスに転送するには、このフィールドに入力します。
* **[!UICONTROL SMTP server]** : 未処理のバウンス電子メールの送信に使用するサーバー。

>[!CAUTION]
>
>未処理のバウンス電子メールを転送する場合は、 **[!UICONTROL Address for errors]** フィールドへの入力のみを推奨します。 ただし、使用するアドレスを定期的にチェックしていることを確認してください。これは、メールサーバに大きな負荷がかかる可能性があるためです。 詳しくは、アカウント担当者にお問い合わせください。

## トラッキング設定 {#tracking-configuration}

次の手順では、インスタンスの追跡を設定します。 インスタンスを宣言し、トラッキングサーバーに登録する必要があります。

この手順は、デプロイメントウィザードの最初のページで **電子メールチャネル** と **追跡** オプションが選択されている場合にのみ提供されます。 Refer to [General parameters](#general-parameters).

Webトラッキング（トラッキングモード、タグの作成と挿入など）の詳細については、 [このドキュメントを参照してください](../../configuration/using/about-web-tracking.md)。

### 動作の仕組み {#operating-principle}

インスタンスの追跡をアクティブ化すると、送信中に配信内のURLが変更され、追跡が有効になります。

* デプロイメントウィザードのこのページに入力された外部URL（セキュリティで保護されているかどうかにかかわらず）に関する情報を使用して、新しいURLを作成します。 この情報に加え、変更されたリンクには次の情報が含まれます。 配信、受信者、URLの識別子。

   トラッキング情報は、トラッキングサーバー上のAdobe Campaignによって収集され、受信者プロファイルと配信にリンクされたデータ( **[!UICONTROL Tracking]** タブ)を強化します。

   内部URLに関する情報は、Adobe Campaignアプリケーションサーバーがトラッキングサーバーに接続する場合にのみ使用されます。

   For more on this, refer to [Tracking server](#tracking-server).

* URLを設定したら、追跡を有効にする必要があります。 これを行うには、インスタンスをトラッキングサーバーに登録する必要があります。

   For more on this, refer to [Saving tracking](#saving-tracking).

### トラッキングサーバー {#tracking-server}

![](assets/s_ncs_install_deployment_wiz_08.png)

このインスタンスでの追跡の効率性を保証するには、次の情報を表示する必要があります。
<!--With Mid-sourcing architecture, you can externalize tracking management. To do this:-->

* **[!UICONTROL External URL]** および/または **[!UICONTROL Secure external URL]** : 送信する電子メールに使用するリダイレクトURLを入力します。
* **[!UICONTROL Internal URL(s)]** : ログを収集してURLをアップロードするために、Adobe Campaignサーバーがトラッキングサーバーに接続するためにのみ使用するURL。 インスタンスに関連付ける必要はありません。

   URLを指定しない場合、デフォルトでトラッキングURLが使用されます。

ミッドソーシングアーキテクチャを使用して、トラッキング管理を外部化できます。 手順は次のとおりです。

1. オプションを選択し **[!UICONTROL Externalize tracking management]** ます。 これにより、ミッドソーシングサーバーをトラッキングサーバーとして使用できます。
1. ミッドソーシングサーバーに接続でき **[!UICONTROL External account]****[!UICONTROL Instance name]** るように、フィールドとフィールドに値を入力します。

   詳しくは、「 [ミッドソーシングサーバ](../../installation/using/mid-sourcing-server.md)」を参照してください。

1. サーバーへの接続を承認するには、 **[!UICONTROL Enable the tracking instance]** ボタンをクリックします。

   ![](assets/s_ncs_install_deployment_wiz_18.png)

### トラッキングの保存 {#saving-tracking}

URLを入力したら、トラッキングサーバーを登録する必要があります。

トラッキングサーバーで「 **登録」リンクをクリックし** 、使用可能なオプションの1つを選択します。

![](assets/s_ncs_install_deployment_wiz_09.png)

トラッキングを実装するためのアーキテクチャには、次の3つのタイプが考えられます。

1. **既存のインスタンスのトラッキングのサポートを追加**

   この選択は、インスタンスが他のニーズ（MTAサーバーなど）に対して既に作成されている場合に適用されます。 トラッキングサーバーとして使用されるサーバーに対して設定します。

   ![](assets/s_ncs_install_deployment_wiz_11.png)

   トラッキングインスタンスを構成するには、リダイレクトサーバーの **内部** アカウントのパスワードを入力します。

   >[!NOTE]
   >
   >複数のトラッキングサーバーを使用する場合は、すべて同じ名前とパスワードを使用する必要があります。

   インスタンスの名前とパスワードを指定します。

1. **トラッキング専用の新しいインスタンスを作成**

   このオプションは、追跡インスタンスが追跡用に予約されており、他のアプリケーションモジュールがない場合に役立ちます。

   ![](assets/s_ncs_install_deployment_wiz_10.png)

   トラッキングインスタンスを構成するには、リダイレクトサーバーの **内部** アカウントのパスワードを入力します。

   >[!NOTE]
   >
   >複数のトラッキングサーバーを設定する場合は、すべて同じパスワードを使用する必要があります。

   インスタンスの名前、パスワード、および関連するDNSマスク（など）を指定し **[!UICONTROL Campaign*]**&#x200B;ます。

1. **既に設定済みのトラッキングインスタンスの検証**

   このオプションは、 **内部アカウントのパスワードを持っていない場合に使用されます** 。 この場合、トラッキングアカウントはトラッキングサーバー上に事前に設定されています。 トラッキングインスタンスを検証するリダイレクトサーバーのトラッキングアカウントのパスワードを入力してください。

   ![](assets/s_ncs_install_deployment_wiz_17.png)

   検証するインスタンスの名前を指定します。

「 **承認** 」をクリックして、記録プロセスをトラッキングサーバーと開始します。

前のウィンドウに戻ると、トラッキングサーバーレベルでの登録を確認するメッセージが表示されます。

![](assets/s_ncs_install_deployment_wiz_tracking_ok.png)

URL検索にリンクされたパラメーターは、標準インストールの場合は変更 **できません** 。 その他のパラメーターについては、アドビにお問い合わせください。

## モバイルチャネルパラメーター {#mobile-channel-parameters}

次の手順では、モバイルに対する配信（SMSおよびWAPプッシュ）の既定の設定を定義します。

>[!NOTE]
>
>モバイルチャネルはオプションです。 このステージは、購入済みの場合にのみ表示されます。 使用許諾契約書を確認してください。

![](assets/s_ncs_install_deployment_wiz_12.png)

### SMS 配信用のデフォルトアカウント {#default-account-for-sms-delivery}

次の情報を入力します。

* **[!UICONTROL Label]** : このSMS/Wapプッシュアカウントの名前を入力してください。 例えば、ルータ名を使用したい場合があります。
* **[!UICONTROL Server]**,,,,, **[!UICONTROL Port]**,,,, **[!UICONTROL Account]**, **[!UICONTROL Password]**, **[!UICONTROL Connector]**, **[!UICONTROL Send Endpoint]**, **[!UICONTROL Reception Endpoint]****[!UICONTROL Notification Endpoint]** , fieldsの場合： 必要な設定については、サービスプロバイダーにお問い合わせください。

### 送信された SMS のパラメーター {#parameters-of-sms-sent}

「 **優先度** 」ドロップダウンリストで、次の操作を行います。 「通常」、「高」または「緊急」を選択して、送信するメッセージに適用します。

### 詳細設定パラメーター {#advanced-parameters}

「 **Advanced parameters...** 」リンクを使用すると、「retry」オプションと「強制隔離」オプションにアクセスできます。

![](assets/s_ncs_install_deployment_wiz_13.png)

再試行に関する情報は、「再試行 **期間** 」および「再試行 **数** 」フィールドで確認できます。 モバイルが未到達の場合、デフォルトでは、プログラムは15分以上の間隔(最大配信期間)で5回再試行します。 これらの値は、ニーズに合わせて調整できます。

強制隔離の設定オプションは次のとおりです。

* **[!UICONTROL Time between two significant errors]** : デフォルト値を入力（デフォルトは「1d」）: day)を使用して、エラーが発生した場合にエラーカウンターを増やすまでのアプリケーションの待機時間を定義します。
* **[!UICONTROL Maximum number of errors before quarantine]** : この値に達すると、モバイル番号は隔離されます（デフォルトは「5」です）。 6番目の誤りで番号が隔離されます)。 これは、連絡先が今後の配信から自動的に除外されることを意味します。

## 地域設定 {#regional-settings}

この段階では、データポリシーの環境設定を行うことができます。

![](assets/s_ncs_install_deployment_wiz_14.png)

* **[!UICONTROL Consider all phone numbers as international ones]** : このオプションを選択すると、国際書式が電話番号に適用されます（書式を適用する前に桁数がチェックされないので、国の接頭辞は必須です）。 このオプションを選択しない場合は、国際電話番号の前に自分で「+」または「00」を付ける必要があります。
* **[!UICONTROL Store all phone numbers using the international format]** : このオプションは、 **インポートまたは編集される国内の電話番号に関するものです** 。 国内形式（425 555 0150など）と国際形式(例： +1 425 555 0150)

## インターネットからのアクセス {#access-from-the-internet}

>[!CAUTION]
>
>プライバシー保護のために、すべての外部リソースに対して HTTPS を使用することをお勧めします。

この手順では、インターネットで公開されるAdobe CampaignページのアクセスURLを定義します。

また、Web フォームにリンクする文書のオプションをここに指定する必要があります。

![](assets/s_ncs_install_deployment_wiz_15.png)

### Web上で公開されるサーバ {#servers-exposed-on-the-web}

このページを使用してサーバーURLを入力します。

1. インターネット上に公開されているアプリケーションサーバーにアクセスします。 購読/購読解除フォーム、エクストラネットなど
1. Web上に公開されていないリソースのアプリケーションサーバーへのアクセス： フォーム、イントラネット、確認ページ。
1. 配信のミラーページにアクセスします。

   ミラーページは、電子メールの内容を表示する動的なページです。 メッセージに挿入されたリンクを介してアクセスされ、受信者に送信される、パーソナライズされた要素を含むことができます。 ミラーページは、受信者の形式（テキストまたはHTML）に関係なく、電子メールソフトではなく、配信ブラウザでメッセージを読む可能性をに与える。 ただし、必要なHTMLコンテンツが定義されている場合に限り、特定の配信に対してミラーページが生成されます。

Adobe Campaignを使用すると、これら3つのURLを区別して、複数のプラットフォームに負荷を分散できます。

## パブリックリソースの管理 {#managing-public-resources}

>[!CAUTION]
>
>プライバシー保護のために、すべての外部リソースに対して HTTPS を使用することをお勧めします。

キャンペーンに関連する E メールやパブリックリソースで使用される画像を外部から表示するには、その画像を外部からアクセスできるサーバー上に置く必要があります。その後、外部の受信者や演算子で使用できます。

![](assets/s_ncs_install_deployment_wiz_img_uploading.png)

この手順では、次のように入力する必要があります。

1. 新しいパブリックリソースのURL。 詳しくは、「 [パブリックリソースURL](#public-resources-url) 」の節を参照してください。
1. 配信の画像検出モード。 詳しくは、「 [配信画像検出](#delivery-image-detection) 」の項を参照してください。
1. 公開オプション For more information, refer to the [Publication modes](#publication-modes) section.

Public resources are accessible via the **Administration > Resources > Online > Public resources** node of the Adobe Campaign tree. ライブラリに収集され、電子メールに含めることができますが、キャンペーンやタスク、コンテンツ管理でも使用できます。

![](assets/install_pub_resources_view.png)

### パブリックリソースURL {#public-resources-url}

最初のフィールドでは、リソースのアップロード後に使用するURLの開始を指定できます。 アップロードされると、この新しいURLを介してリソースにアクセスできます。

配信では、パブリックリソースライブラリに保存されている画像や、サーバに保存されている他のローカル画像や画像を使用できます。

* 電子メール画像の場合は、https:// **** server **/res/img** URL。

   この値は、各配信で上書きできます。

* パブリックリソースの場合、URL https:// **** server **/res/** instance(****instance ****はトラッキングインスタンスの名前)。

### 配信画像の検出 {#delivery-image-detection}

配信では、パブリックリソースライブラリに保存されている画像や、サーバに保存されている他のローカル画像や画像を使用できます。

フィールド **URLマスク** ：画像を自動的にアップロードする際にスキップするURLマスクのリストを指定できます。 例えば、外部からアクセスできるサイト、特にインターネットサイト上に保存されている画像を使用する場合、このフィールドにサイトのURLを入力できます。

![](assets/s_ncs_install_deployment_wiz_img_mask.png)

複数のURLマスクを指定する場合は、コンマで各URLマスクを区切ります。

* 電子メールでの画像の使用と管理については、 [この節を参照してください](../../delivery/using/defining-the-email-content.md#adding-images)。
* 配信ウィザードでは、これらのURLから呼び出された画像のステータスは「無視」になります。

### パブリケーションモード {#publication-modes}

ウィザードの下部では、パブリックリソースとイメージのパブリケーションオプションを選択できます。 これらのオプションは、Web フォームと調査でも使用できます。

次のパブリケーションモードを使用できます。

* トラッキングサーバー

   リソースは、別のトラッキングサーバーに自動的にコピーされます。 これらは、手順 [追跡の設定で設定します](#tracking-configuration)。

* その他のAdobe Campaignサーバー

   リソースのコピー先となる、他の1つのAdobe Campaignサーバーを使用することもできます。

   サーバー側で、専用のAdobe Campaignサーバーを使用するには、次のコマンドを使用して新しいインスタンスを作成する必要があります。

   ```
   nlserver config -addtrackinginstance:<trackingA>/<trackingA*>
   ```

   次に、パスワードを入力します。

   専用サーバのパラメータは、 、 **[!UICONTROL Media URL(s)]**、の各フィールドに示され **[!UICONTROL Password]** ま **[!UICONTROL Instance name]** す。

   ![](assets/s_ncs_install_images_upload_b.png)

* 手動のパブリケーションスクリプト(パブリックリソースのみ)

   ![](assets/s_ncs_install_images_upload_c.png)

   スクリプトを使用して画像を公開できます。

   * 次のスクリプトを作成する必要があります。 その内容は、設定に応じて異なります。
   * スクリプトは次のコマンドによって呼び出されます。

      ```
      [INSTALL]/copyToFrontal.vbs "$(XTK_INSTALL_DIR)\var\<instance>\upload\" "img1,img2,img3"
      ```

      ここ `[INSTALL]` で、はAdobe Campaignのインストールフォルダーへのアクセスパスです。

   * Unixでは、スクリプトが実行可能であることを確認します。

イメージの場合は、NmsDelivery_ImageSubDirectory **** オプションを介して指定された「images」フォルダーから、1つ以上のフロントサーバーにイメージをコピーする必要があります。 これらのサーバーには、新しく設定したURLを介して画像にアクセスできるように画像が格納されます。

手動のパブリケーション・スクリプトを使用しないAdobe Campaign・サーバ上でのパブリケーションのイベントでは、デフォルトで、に配信のイメージが保存され `$(XTK_INSTALL_DIR)/var/res/img/ directory`ます。 対応するURLは次のとおりです。 **`https://server/res/img`**.

`XTK_INSTALL_DIR)/var/res/$(INSTANCE_NAME)`.」対応するURLは次のとおりです。 **`https://server/res/instance`** instanceは、トラッキングインスタンスの名前です。

>[!NOTE]
>
>パブリックリソースストレージディレクトリは変更できます。 For more on this, refer to [Managing public resources](#managing-public-resources).

### パブリックリソースの同期 {#synchronizing-public-resources}

この機能により、複数のスペア・サーバ上のパブリックリソース **を** 同期できます。

トラッキングサーバにパブリックリソースが存在しない場合、またはリソースが404エラーを返した場合、トラッキングサーバはスペアサーバの1つでリソースを探します。

スペアサーバの宣言と設定は、マーケティングサーバの **serverConf.xml** ファイルで行う必要があります。 serverConf.xmlで使用可能なすべてのパラメ **ーターをこの** 節に示します [](../../installation/using/the-server-configuration-file.md)。

**申告**

```
<redirection>
<spareServer enabledIf="" id="" url=""/>
</redirection>
```

**設定**

同期する必要がある各パブリックリソースに対して、パーツ内の `<url>` 要素にstatus属性を追加する必要があり `<relay>` ます。

status属性には、次の3つの値のいずれかを指定できます。

* スペア： パブリックリソースが同期される

* normal: 既存の動作（同期なし）

* blacklist: URLは、404エラーを返す場合はブラックリスト登録済みです。 ブラックリスト表示の時間（秒）は、 **timeout** 属性で定義されます。この属性のデフォルト値は60秒です。

既製の同期設定は次のとおりです。

```
(extracted from the serverConf.xml file)

<redirection P3PCompactPolicy="CAO DSP COR CURa DEVa TAIa OUR BUS IND UNI COM NAV"
databaseId="" defLogCount="30" expirationURL="" maxJobsInCache="100"
startRedirection="true" startRedirectionInModule="true" trackWebVisitors="false" trackingPassword="">
<spareServer enabledIf="" id="1" url=""/>
</redirection>

....


<relay debugRelay="false" forbiddenCharsInAuthority="?#.@/:" forbiddenCharsInPath="?#/"
           modDir="index.html" startRelay="false" startRelayInModule="true" timeout="60">
   <url IPMask="" deny="" hostMask="" relayHost="true" relayPath="true" status="normal" targetUrl="https://localhost:8080" timeout="" urlPath="/view/*"/>
      <url IPMask="" deny="" hostMask="" relayHost="true" relayPath="true" status="blacklist" targetUrl="https://localhost:8080" timeout="" urlPath="*.jsp"/>
      <url IPMask="" deny="" hostMask="" relayHost="true" relayPath="true" status="blacklist" targetUrl="https://localhost:8080" timeout="" urlPath="*.jssp"/>
      <url IPMask="" deny="" hostMask="" relayHost="true" relayPath="true" status="blacklist" targetUrl="https://localhost:8080" timeout="" urlPath="/webApp/*"/>
      <url IPMask="" deny="" hostMask="" relayHost="true" relayPath="true" status="blacklist" targetUrl="https://localhost:8080" timeout="" urlPath="/report/*"/>
      <url IPMask="" deny="" hostMask="" relayHost="true" relayPath="true" status="blacklist" targetUrl="https://localhost:8080" timeout="" urlPath="/jssp/*"/>
      <url IPMask="" deny="" hostMask="" relayHost="true" relayPath="true" status="normal" targetUrl="https://localhost:8080" timeout="" urlPath="/strings/*"/>
      <url IPMask="" deny="" hostMask="" relayHost="true" relayPath="true" status="normal" targetUrl="https://localhost:8080" timeout="" urlPath="/interaction/*"/>
      <url IPMask="" deny="" hostMask="" relayHost="true" relayPath="true" status="normal" targetUrl="https://localhost:8080" timeout="" urlPath="/barcode/*"/>

      <url IPMask="" deny="" hostMask="" relayHost="false" relayPath="false" status="spare" targetUrl="" timeout="" urlPath="/favicon.*"/>
      <url IPMask="" deny="" hostMask="" relayHost="false" relayPath="false" status="spare" targetUrl="" timeout="" urlPath="/*.html"/>
      <url IPMask="" deny="" hostMask="" relayHost="false" relayPath="false" status="spare" targetUrl="" timeout="" urlPath="/*.png"/>
      <url IPMask="" deny="" hostMask="" relayHost="false" relayPath="false" status="spare" targetUrl="" timeout="" urlPath="/*.jpg"/>

 </relay>
```

## データの削除 {#purging-data}

デプロイメントウィザードの最後のステージでは、古いデータの自動削除を設定できます。 値は日単位で表されます。

![](assets/s_ncs_install_deployment_wiz_16.png)

データは、データベースクリーンアップワークフローを介して自動的に削除されます。 このワークフローを構成および操作する方法と、削除されたアイテムの詳細については、この [ドキュメントを参照してください](../../production/using/database-cleanup-workflow.md)。
