---
product: campaign
title: インスタンスのデプロイ
description: Campaign デプロイウィザードの詳細を説明します
audience: installation
content-type: reference
topic-tags: initial-configuration
exl-id: 8b07447c-9a86-4b56-8d29-e0b01357a6ec
source-git-commit: 20509f44c5b8e0827a09f44dffdf2ec9d11652a1
workflow-type: tm+mt
source-wordcount: '3193'
ht-degree: 5%

---

# インスタンスのデプロイ{#deploying-an-instance}

![](../../assets/v7-only.svg)

>[!NOTE]
>
>サーバー側の設定は、AdobeがホストするデプロイメントのAdobeでのみ実行できます。 様々なデプロイメントの詳細については、[ モデルのホスティング ](../../installation/using/hosting-models.md) の節または [ このページ ](../../installation/using/capability-matrix.md) を参照してください。

## デプロイメントウィザード {#deployment-wizard}

Adobe Campaignのクライアントコンソールで使用できるグラフィカルウィザードを使用して、接続先のインスタンスのパラメーターを定義できます。

デプロイウィザードを起動するには、**ツール/詳細設定/デプロイウィザード** を選択します。

![](assets/s_ncs_install_deployment_wiz_01.png)

設定手順は、以下のとおりです。

1. [一般パラメーター](#general-parameters)
1. [E メールチャネルパラメーター](#email-channel-parameters)
1. [バウンス電子メールの管理](#managing-bounced-emails)
1. [トラッキング設定](#tracking-configuration)
1. [モバイルチャネルパラメーター](#mobile-channel-parameters)
1. [地域設定](#regional-settings)
1. [インターネットからのアクセス](#access-from-the-internet)
1. [パブリックリソースの管理](#managing-public-resources)
1. [データのパージ](#purging-data)

## 一般パラメーター {#general-parameters}

デプロイウィザードの最初の手順では、インスタンスに関する一般情報を入力できます。

![](assets/s_ncs_install_deployment_wiz_02.png)

### 一般情報 {#general-information}

ウィンドウの下部のセクションで、アクティブにするオプションを選択できます。

* **[!UICONTROL 請求で使用される顧客 ID]** :インスタンスの名前とバージョン番号を指定できます。
* **[!UICONTROL 顧客の共通名]** :会社名を含む文字列を入力します。この情報は、購読解除リンクで使用できます。
* **[!UICONTROL 名前空間]** :短い識別子を小文字で入力します。目的は、アップグレードの際に、特定の設定と出荷時の設定を区別することです。 デフォルトの名前空間は、お客様向けの **cus** です。

### 技術的なオプション {#technical-options}

ウィンドウの下部のセクションで、アクティブにするオプションを選択できます。

次のオプションを使用できます。

* **[!UICONTROL E メールチャネル]** :：電子メール配信を有効にします。[E メールチャネルパラメーター ](#email-channel-parameters) を参照してください。
* **[!UICONTROL トラッキング]** :ターゲット母集団（開封数およびクリック数）の追跡を有効にする場合。[ トラッキング設定 ](#tracking-configuration) を参照してください。
* **[!UICONTROL バウンス電子メールの管理]** :受信メールの受信に使用する POP アカウントを定義する。[ バウンスメールの管理 ](#managing-bounced-emails) を参照してください。
* **[!UICONTROL LDAP の統合]** :LDAP ディレクトリを介してユーザー認証を設定する。[LDAP を介した接続 ](../../installation/using/connecting-through-ldap.md) を参照してください。

## E メールチャネルパラメーター {#email-channel-parameters}

次の手順では、メッセージヘッダーに表示する情報を定義できます。

これらのパラメーターは、配信テンプレートで重複して設定される場合や、（ユーザーが必要な権限を持っている場合）配信ごとに個別に定義する場合に重複して設定できます。

### 配信 E メールのパラメーター {#parameters-for-delivered-emails}

![](assets/s_ncs_install_deployment_wiz_04.png)

次のパラメータを指定します。

* **[!UICONTROL 送信者名]** :送信者の名前
* **[!UICONTROL 送信者のアドレス]** :送信者のアドレス
* **[!UICONTROL 返信アドレスのテキスト]** :受信者が電子メールクライアントソフトウェアの「返信」ボタンをクリッ **** クしたときに使用される名前（カスタマイズ可能）。
* **[!UICONTROL 返信アドレス]** :受信者が電子メールクライアントソフトウェアの「返信」ボ **** タンをクリックしたときに使用する電子メールアドレス。
* **[!UICONTROL エラーアドレス]** :エラーが発生したメッセージの E メールアドレス。これは、ターゲットアドレスが存在しないことが原因でAdobe Campaignサーバーが受信した E メールを含む、バウンスメールの処理に使用される技術的なアドレスです。

これに加えて、送信者のアドレスとエラーアドレスに対して許可する **masks** を指定できます。 必要に応じて、コンマで区切ることができます。 この設定はオプションです。 フィールドに入力すると、Adobe Campaignは配信時（分析中に、アドレスに変数が含まれていない場合）にそのアドレスが有効であるかどうかを確認します。 この動作モードでは、配信の問題を引き起こす可能性のあるアドレスをトリガーしないようにします。 配信アドレスは、配信サーバーで設定する必要があります。

### アドレスに使用できる文字 {#characters-authorized-in-addresses}

<!--This window enables you to define, for all email campaigns, the delivery and address-quality management options.-->

Adobe Campaignデータベースでは、すべての E メールアドレスが次のように作成される必要があります。`x@y.z`. **x**、**y** および **z** 文字は空にできません。また、許可されていない文字を含めることはできません。

ここで、許可する文字（「データポリシー」）をデータベースの email フィールドに定義できます。 リストに含まれていない文字は禁止されるので、インターフェイス、Web フォーム、データのインポートを使用してデータベースに情報を入力する際に拒否されます。

次の 2 つのリストを使用できます。**ヨーロッパのみ** または **米国のみ**。 必要に応じて、その他の文字を追加できます。

### 配信パラメーター {#delivery-parameters}

**詳細設定パラメーター…** リンクを使用して、配信オプション、再試行および強制隔離にリンクされたパラメーターにアクセスできます。

![](assets/s_ncs_install_deployment_wiz_05.png)

このウィンドウでは、すべての E メールキャンペーンに対して、配信およびアドレスの質の管理オプションを定義できます。

次のオプションを使用できます。

* **[!UICONTROL メッセージの配信期間]** :この時間を過ぎると、配信は停止されます（デフォルトでは 5 日間）。
* **[!UICONTROL オンラインリソースの有効期間]** :ミラーページを生成するために受信者プロファイルからの情報を保持する時間
* **[!UICONTROL 今後連絡を希望しない受信者を除外]** :このオプションを選択した場合、「受信者にブロックリスト連絡を送信しない」で、
* **[!UICONTROL コピーを自動的に無視]** :このオプションを選択した場合、重複アドレスは配信されません。

### 再試行パラメーター {#retry-parameters}

リカバリに関する情報は、「**リカバリ期間**」および「**リカバリ回数**」フィールドに記載されています。受信者に到達できない場合、例えば受信ボックスがいっぱいの場合、デフォルトでは、各試行の間隔（最大配信時間）が 1 時間で 5 回連絡が試行されます。 これらの値は、ニーズに合わせて変更できます。

### 強制隔離パラメーター {#quarantine-parameters}

強制隔離の設定オプションを次に示します。

* **[!UICONTROL 2 つの重大なエラーの間の期間]** :値（デフォルトでは「1d」）を入力します。1 日 ) を指定して、エラーが発生した場合にエラーカウンターを増やすまでのアプリケーションの待機時間を定義します。
* **[!UICONTROL 強制隔離前の最大エラー数]** :この値に達すると、E メールアドレスが強制隔離されます（デフォルトは「5」）。6 回目のエラー発生時にアドレスが強制隔離されます )。これは、連絡先が後続の配信から自動的に除外されることを意味します。

## バウンス電子メールの管理 {#managing-bounced-emails}

配信エラーを検証するには、バウンスメールが非常に重要です。 これらのエラーは、ルールが原因を特定した後、 NP@Iに分類されます。

この手順は、デプロイウィザードの最初の段階で **E メールチャネル** と **バウンスメール** の管理オプションが選択されている場合にのみ使用できます。 [ 一般的なパラメータ ](#general-parameters) を参照してください。

この段階では、バウンスメールを管理するための設定を定義できます。

![](assets/s_ncs_install_deployment_wiz_06.png)

### 受信メールの取得に使用する POP アカウント {#pop-account-used-to-retrieve-incoming-mails}

受信電子メールを取得するためのアカウントに接続するパラメーターを指定します。

* **[!UICONTROL ラベル]** :以下に示すすべてのパラメーターを含む名前
* **[!UICONTROL サーバー]** :バウンスメール（受信メール）の取得に使用するサーバー
* **[!UICONTROL セキュリティ]** :必要に応じて、ドロッ **** プダウンリストから SSL を選択します。
* **[!UICONTROL ポート]** :サーバポート（通常は 110）
* **[!UICONTROL アカウント]** :バウンスメールに使用するアカウントの名前
* **[!UICONTROL パスワード]** :アカウントに関連付けられたパスワード。

POP 設定を指定したら、「**テスト**」をクリックして、設定が正しいことを確認します。

### 未処理のバウンスメール {#unprocessed-bounce-mails}

バウンスはAdobe Campaignによって自動的に処理され、**管理/キャンペーン管理/配信不能件数の管理/配信ログの検証** ノードにリストされているルールを適用します。 詳しくは、[ バウンスメール管理 ](../../delivery/using/understanding-delivery-failures.md#bounce-mail-management) を参照してください。

未処理のバウンスは、Adobe Campaignインターフェイスに表示されません。 次のフィールドを使用してサードパーティのメールボックスに転送されない限り、自動的に削除されます。

* **[!UICONTROL 転送アドレス]** :Adobe Campaignプラットフォームで収集されたすべてのエラーメッセージ（処理済みまたは未処理）をサードパーティのアドレスに転送するには、このフィールドに入力します。
* **[!UICONTROL エラーのアドレス]** :inMail プロセスで認定できなかったエラーメッセージのみをサードパーティのアドレスに転送するには、このフィールドに入力します。
* **[!UICONTROL SMTP サーバー]** :未処理のバウンス E メールの送信に使用するサーバー。

>[!IMPORTANT]
>
>未処理のバウンス E メールを転送する場合は、Adobeは「**[!UICONTROL エラーのアドレス]**」フィールドにのみ入力することをお勧めします。 ただし、メールサーバーに大きな負荷がかかる可能性があるので、使用するアドレスが定期的にチェックされていることを確認してください。 詳しくは、アカウント担当者にお問い合わせください。

## トラッキング設定 {#tracking-configuration}

次の手順では、インスタンスの追跡を設定できます。 インスタンスが宣言され、トラッキングサーバーに登録されている必要があります。

この手順は、デプロイウィザードの最初のページで **E メールチャネル** と **トラッキング** のオプションが選択されている場合にのみ表示されます。 [ 一般的なパラメータ ](#general-parameters) を参照してください。

Web トラッキング（トラッキングモード、タグの作成と挿入など）について詳しくは、[ このドキュメント ](../../configuration/using/about-web-tracking.md) を参照してください。

### 動作原理 {#operating-principle}

インスタンスのトラッキングを有効にすると、送信中に配信の URL が変更され、トラッキングが有効になります。

* デプロイウィザードのこのページで入力した外部 URL（セキュリティで保護されているかどうかに関わらず）に関する情報を使用して、新しい URL を作成します。 この情報に加えて、変更されたリンクには次の情報が含まれます。配信の識別子、受信者および URL。

   トラッキング情報は、トラッキングサーバー上のAdobe Campaignによって収集され、受信者のプロファイルと配信にリンクされたデータをエンリッチメントします（**[!UICONTROL 「トラッキング]**」タブ）。

   内部 URL に関する情報は、Adobe Campaignアプリケーションサーバーがトラッキングサーバーに接続する場合にのみ使用されます。

   詳しくは、[ トラッキングサーバー ](#tracking-server) を参照してください。

* URL を設定したら、トラッキングを有効にする必要があります。 これをおこなうには、インスタンスをトラッキングサーバーに登録する必要があります。

   詳しくは、[ トラッキングの保存 ](#saving-tracking) を参照してください。

### トラッキングサーバー {#tracking-server}

![](assets/s_ncs_install_deployment_wiz_08.png)

このインスタンスでのトラッキングの効率を保証するには、次の情報を表示する必要があります。
<!--With Mid-sourcing architecture, you can externalize tracking management. To do this:-->

* **[!UICONTROL 外部]** URL またはセキュ **[!UICONTROL ア外部 URL]** :送信する E メールで使用するリダイレクト URL を入力します。
* **[!UICONTROL 内部 URL]** :ログの収集と URL のアップロードのためにAdobe Campaignサーバーがトラッキングサーバーに接続する際にのみ使用される URL。インスタンスに関連付ける必要はありません。

   URL を指定しない場合、デフォルトでトラッキング URL が使用されます。

ミッドソーシングアーキテクチャを使用して、トラッキング管理を外部化できます。 手順は次のとおりです。

1. 「**[!UICONTROL Externalize tracking management]**」オプションを選択します。これにより、ミッドソーシングサーバーをトラッキングサーバーとして使用できます。
1. ミッドソーシングサーバーに接続できるように、「**[!UICONTROL 外部アカウント]**」および「**[!UICONTROL インスタンス名]**」フィールドを設定します。

   詳しくは、[ ミッドソーシングサーバー ](../../installation/using/mid-sourcing-server.md) を参照してください。

1. 「**[!UICONTROL トラッキングインスタンスを有効にする]**」ボタンをクリックして、サーバーへの接続を承認します。

   ![](assets/s_ncs_install_deployment_wiz_18.png)

### トラッキングの保存 {#saving-tracking}

URL に値が入力されたら、トラッキングサーバーを登録する必要があります。

「トラッキングサーバーへの登録 **** 」リンクをクリックし、使用可能なオプションの 1 つを選択します。

![](assets/s_ncs_install_deployment_wiz_09.png)

トラッキングを実装する場合、次の 3 つのタイプのアーキテクチャが考えられます。

1. **既存のインスタンスのトラッキングのサポートを追加**

   この選択は、他のニーズ（MTA サーバーなど）に合わせてインスタンスが既に作成されている場合に適用されます。 トラッキングサーバーとして使用されるサーバー上で使用する。

   ![](assets/s_ncs_install_deployment_wiz_11.png)

   トラッキングインスタンスを設定するには、リダイレクトサーバーの **内部** アカウントのパスワードを入力します。

   >[!NOTE]
   >
   >複数のトラッキングサーバーを使用する場合は、すべて同じ名前とパスワードを使用する必要があります。

   インスタンスの名前とパスワードを指定します。

1. **トラッキング専用の新しいインスタンスを作成**

   このオプションは、トラッキングインスタンスがトラッキング用に予約され、他のアプリケーションモジュールがない場合に役立ちます。

   ![](assets/s_ncs_install_deployment_wiz_10.png)

   トラッキングインスタンスを設定するには、リダイレクトサーバーの **内部** アカウントのパスワードを入力します。

   >[!NOTE]
   >
   >複数のトラッキングサーバーを設定する場合は、すべて同じパスワードを使用する必要があります。

   インスタンスの名前、パスワード、および **[!UICONTROL Campaign*]** など、関連する DNS マスクを指定します。

1. **事前設定済みのトラッキングインスタンスの検証**

   このオプションは、**内部** アカウントのパスワードがない場合に使用します。この場合、トラッキングアカウントはトラッキングサーバーに事前に設定されています。 トラッキングインスタンスを検証するリダイレクトサーバーのトラッキングアカウントのパスワードを入力します。

   ![](assets/s_ncs_install_deployment_wiz_17.png)

   検証するインスタンスの名前を指定します。

「**承認**」をクリックして、トラッキングサーバーでの記録プロセスを開始します。

前のウィンドウに戻ると、トラッキングサーバーレベルでの登録を確認するメッセージが表示されます。

![](assets/s_ncs_install_deployment_wiz_tracking_ok.png)

URL 検索 **に関連するパラメータは、標準インストールの場合は変更** しないでください。 その他のパラメーターについては、Adobeにお問い合わせください。

## モバイルチャネルパラメーター {#mobile-channel-parameters}

次の手順では、モバイルへの配信（SMS および WAP プッシュ）のデフォルト設定を定義できます。

>[!NOTE]
>
>モバイルチャネルはオプションです。このステージは、購入済みの場合にのみ表示されます。 ライセンス契約をご確認ください。

![](assets/s_ncs_install_deployment_wiz_12.png)

### SMS 配信用のデフォルトアカウント {#default-account-for-sms-delivery}

次の情報を入力します。

* **[!UICONTROL ラベル]** :この SMS/WAP プッシュアカウントの名前を入力します。例えば、ルータの名前を使用できます。
* **[!UICONTROL サーバー]**、**[!UICONTROL ポート]**、**[!UICONTROL アカウント]**、**[!UICONTROL パスワード]**、**[!UICONTROL コネクタ]**、**[!UICONTROL 送信エンドポイント]**、**[!UICONTROL 受信 endpoint]**、**[!UICONTROL Notification Endpoint]** フィールド：必要な設定については、サービスプロバイダーにお問い合わせください。

### 送信された SMS のパラメーター {#parameters-of-sms-sent}

「**優先度**」ドロップダウンリストで、次の手順に従います。「通常」、「高」または「緊急」を選択して、送信するメッセージに適用します。

### 詳細設定パラメーター {#advanced-parameters}

**詳細設定パラメーター…** リンクを使用して、再試行および強制隔離のオプションにアクセスできます。

![](assets/s_ncs_install_deployment_wiz_13.png)

再試行に関する情報は、「**再試行の期間**」および「**再試行の回数**」フィールドに記載されています。モバイルに到達できない場合、デフォルトでは、15 分以上の間隔（最大配信期間）で 5 回再試行されます。 これらの値は、ニーズに合わせて調整できます。

強制隔離の設定オプションを次に示します。

* **[!UICONTROL 2 つの重大なエラーの間隔]** :デフォルト値を入力します（デフォルトは「1d」）。日 ) を使用して、エラーカウンターを増分して失敗を待機する時間を定義します。
* **[!UICONTROL 強制隔離前の最大エラー数]** :この値に達すると、モバイル番号が強制隔離されます（デフォルトは「5」）。6 回目のエラー発生時に、この数が強制隔離されます )。つまり、連絡先は今後の配信から自動的に除外されます。

## 地域設定 {#regional-settings}

この段階では、データポリシーの設定を含めることができます。

![](assets/s_ncs_install_deployment_wiz_14.png)

* **[!UICONTROL すべての電話番号を国際電話番号と見なします]** 。このオプションを選択すると、国際書式が電話番号に適用されます（書式を適用する前に桁数がチェックされないので、国のプレフィックスは必須です）。このオプションを選択しない場合は、自分で「+」または「00」というプレフィックスを国際電話番号に付ける必要があります。
* **[!UICONTROL すべての電話番号を国際形式で保存]** :このオプションは、読み込ま **** れたり編集された国内電話番号にのみ適用されます。国内形式（425 555 0150 など）と国際形式 ( 例：+1 425 555 0150)

## インターネットからのアクセス {#access-from-the-internet}

>[!IMPORTANT]
>
>プライバシー保護のために、すべての外部リソースに対して HTTPS を使用することをお勧めします。

この手順では、インターネットで公開されるAdobe Campaignページのアクセス URL を定義できます。

また、Web フォームにリンクするパブリッシュオプションをここに指定する必要があります。

![](assets/s_ncs_install_deployment_wiz_15.png)

### Web で公開されるサーバー {#servers-exposed-on-the-web}

このページを使用して、サーバー URL を以下のように設定します。

1. インターネットで公開されたアプリケーションサーバーにアクセスする：購読/購読解除フォーム、エクストラネットなど
1. Web で公開されていないリソースのアプリケーションサーバーにアクセスします。フォーム、イントラネット、確認ページ
1. 配信のミラーページにアクセスします。

   ミラーページは、E メールのコンテンツを表示する動的なページです。 受信者に送信されるメッセージに挿入されたリンクを介してアクセスされ、パーソナライズされた要素を含めることができます。 ミラーページを使用すると、受信者は、配信形式 ( テキストまたはHTML) に関係なく、電子メールソフトウェアではなく、インターネットブラウザーでメッセージを読むことができます。 ただし、ミラーページは、必要な配信コンテンツが定義されている場合にのみ、特定のHTMLに対して生成されます。

Adobe Campaignでは、これらの 3 つの URL を区別して、複数のプラットフォームにわたって負荷を分散できます。

## パブリックリソースの管理 {#managing-public-resources}

>[!IMPORTANT]
>
>プライバシー保護のために、すべての外部リソースに対して HTTPS を使用することをお勧めします。

キャンペーンに関連する E メールやパブリックリソースで使用される画像を外部から表示するには、その画像を外部からアクセスできるサーバー上に置く必要があります。その後、外部の受信者やオペレーターが使用できるようになります。

![](assets/s_ncs_install_deployment_wiz_img_uploading.png)

この手順では、次を入力する必要があります。

1. 新しいパブリックリソース URL。 詳しくは、[ パブリックリソース URL](#public-resources-url) の節を参照してください。
1. 配信の画像検出モード。 詳しくは、[ 配信画像の検出 ](#delivery-image-detection) の節を参照してください。
1. 公開オプション。 詳しくは、[ パブリッシュモード ](#publication-modes) の節を参照してください。

パブリックリソースには、Adobe Campaignツリーの **管理/リソース/オンライン/パブリックリソース** ノードからアクセスできます。 これらはライブラリに収集され、E メールに含めることができますが、キャンペーンやタスク、コンテンツ管理にも使用できます。

![](assets/install_pub_resources_view.png)

### パブリックリソース URL {#public-resources-url}

最初のフィールドでは、アップロード後のリソースに使用する URL の開始を指定できます。 アップロードすると、この新しい URL を使用してリソースにアクセスできます。

配信では、パブリックリソースライブラリに保存された画像や、サーバーに保存されたその他のローカル画像や画像を使用できます。

* 電子メール画像の場合、**https://** server **/res/img** の URL。

   この値は、配信ごとに上書きできます。

* パブリックリソースの場合、URL **https://** server **/res/** instance ****（**instance**はトラッキングインスタンスの名前）。

### 配信画像の検出 {#delivery-image-detection}

配信では、パブリックリソースライブラリに保存された画像や、サーバーに保存されたその他のローカル画像や画像を使用できます。

「**URL マスク**」フィールドで、画像を自動的にアップロードする際にスキップする URL マスクのリストを指定できます。 例えば、外部からアクセス可能なサイト（特にインターネットサイト）に保存されている画像を使用する場合、このフィールドにサイトの URL を入力できます。

![](assets/s_ncs_install_deployment_wiz_img_mask.png)

複数の URL マスクを指定する場合は、コンマで区切ります。

* E メールでの画像の使用と管理については、[ この節 ](../../delivery/using/defining-the-email-content.md#adding-images) を参照してください。
* 配信ウィザードで、これらの URL から呼び出された画像のステータスが「無視」になります。

### 公開モード {#publication-modes}

ウィザードの下部のセクションで、パブリックリソースとパブリック画像の公開オプションを選択できます。

次のパブリッシュモードを使用できます。

* トラッキングサーバー

   リソースは、別のトラッキングサーバーに自動的にコピーされます。 手順 [ トラッキング設定 ](#tracking-configuration) で設定します。

* その他のAdobe Campaignサーバー

   リソースのコピー先として、他の 1 台のAdobe Campaignサーバーを使用できます。

   サーバー側で、専用のAdobe Campaignサーバーを使用するには、次のコマンドを使用して新しいインスタンスを作成する必要があります。

   ```
   nlserver config -addtrackinginstance:<trackingA>/<trackingA*>
   ```

   次に、パスワードを入力します。

   専用サーバーのパラメーターは、**[!UICONTROL メディア URL]**、**[!UICONTROL パスワード]**、**[!UICONTROL インスタンス名]** の各フィールドに指定します。

   ![](assets/s_ncs_install_images_upload_b.png)

* 手動パブリッシュスクリプト（パブリックリソースのみ）

   ![](assets/s_ncs_install_images_upload_c.png)

   スクリプトを使用して画像を公開できます。

   * 次のスクリプトを作成する必要があります。その内容は、設定によって異なります。
   * スクリプトは、次のコマンドによって呼び出されます。

      ```
      [INSTALL]/copyToFrontal.vbs "$(XTK_INSTALL_DIR)\var\<instance>\upload\" "img1,img2,img3"
      ```

      `[INSTALL]` は、Adobe Campaignのインストールフォルダーへのアクセスパスです。

   * Unix では、スクリプトが実行可能であることを確認します。

画像の場合、**NmsDelivery_ImageSubDirectory** オプションで指定した「画像」フォルダーから、1 つ以上のフロントサーバーに画像をコピーする必要があります。 これらのサーバーには画像が保存され、新しく設定された URL を介して画像にアクセスできるようになります。

手動での公開スクリプトを使用せずにAdobe Campaignサーバーで公開した場合、デフォルトでは、配信の画像は `$(XTK_INSTALL_DIR)/var/res/img/ directory` に保存されます。 対応する URL は次のとおりです。**`https://server/res/img`**.

`XTK_INSTALL_DIR)/var/res/$(INSTANCE_NAME)`.対応する URL は次のとおりです。**`https://server/res/instance`** ここで、instance はトラッキングインスタンスの名前です。

>[!NOTE]
>
>パブリックリソースストレージディレクトリを変更できます。 詳しくは、[ パブリックリソースの管理 ](#managing-public-resources) を参照してください。

### パブリックリソースの同期 {#synchronizing-public-resources}

この機能を使用すると、複数のスペア・サーバ上のパブリック・リソース **を** 同期できます。

パブリックリソースがトラッキングサーバーに存在しない場合、またはリソースが 404 エラーを返した場合、トラッキングサーバーは、いずれかのスペアサーバーでリソースを探します。

スペアサーバーの宣言と設定は、マーケティングサーバーの **serverConf.xml** ファイルでおこなう必要があります。 **serverConf.xml** で使用できるすべてのパラメーターは、この [ セクション ](../../installation/using/the-server-configuration-file.md) に記載されています。

**宣言**

```
<redirection>
<spareServer enabledIf="" id="" url=""/>
</redirection>
```

**設定**

同期する必要があるパブリックリソースごとに、`<relay>` パートの `<url>` 要素に status 属性を追加する必要があります。

status 属性には、次の 3 つの値のいずれかを指定できます。

* スペア：パブリックリソースが同期されている

* 標準：既存の動作（同期なし）

* ブラックリスト：404 エラーが返された場合ブロックリスト、URL はに追加されます。 内の URL の時間（秒）ブロックリストは、**timeout** 属性で定義されます。デフォルト値は 60 秒です。

同期の標準設定は次のとおりです。

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

## データのパージ {#purging-data}

デプロイウィザードの最後の段階で、古いデータの自動パージを設定できます。 値は日数で表します。

![](assets/s_ncs_install_deployment_wiz_16.png)

データは、データベースクリーンアップワークフローで自動的に削除されます。 このワークフローの設定と操作の方法、および削除した項目の詳細については、この [ ドキュメント ](../../production/using/database-cleanup-workflow.md) を参照してください。
