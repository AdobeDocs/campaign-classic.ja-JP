---
product: campaign
title: インスタンスのデプロイ
description: Campaign デプロイウィザードの詳細を説明します
badge-v7-only: label="v7" type="Informative" tooltip="Applies to Campaign Classic v7 only"
badge-v7-prem: label="on-premise & hybrid" type="Caution" url="https://experienceleague.adobe.com/docs/campaign-classic/using/installing-campaign-classic/architecture-and-hosting-models/hosting-models-lp/hosting-models.html" tooltip="Applies to on-premise and hybrid deployments only"
audience: installation
content-type: reference
topic-tags: initial-configuration
exl-id: 8b07447c-9a86-4b56-8d29-e0b01357a6ec
source-git-commit: 84dc10d9f1979b7b9277fbc6837bc5ee9ab0e9dd
workflow-type: tm+mt
source-wordcount: '3491'
ht-degree: 6%

---

# インスタンスのデプロイ{#deploying-an-instance}

>[!NOTE]
>
>サーバー側の設定は、Adobeがホストするデプロイメントの場合、Adobeが実行する必要があります。 様々なデプロイメントについて詳しくは、 [ホスティングのモデル](../../installation/using/hosting-models.md) セクションまたは [このページ](../../installation/using/capability-matrix.md).

## デプロイメントウィザード {#deployment-wizard}

Adobe Campaignには、Adobe Campaignクライアントコンソールで、接続先のインスタンスのパラメーターを定義するためのグラフィカルアシスタントが用意されています。

デプロイウィザードを起動するには、「 」を選択します。 **ツール/詳細設定/デプロイウィザード**.

![](assets/s_ncs_install_deployment_wiz_01.png)

設定手順は、以下のとおりです。

1. [一般パラメーター](#general-parameters)
1. [E メールチャネルパラメーター](#email-channel-parameters)
1. [バウンスメールの管理](#managing-bounced-emails)
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

ウィンドウの下部のセクションでは、アクティブにするオプションを選択できます。

* **[!UICONTROL 請求で使用される顧客識別子]** :インスタンスの名前とバージョン番号を指定できます。
* **[!UICONTROL 顧客の共通名]** :会社名を含む文字列を入力します。 この情報は、購読解除リンクで使用できます。
* **[!UICONTROL 名前空間]** :短い識別子を小文字で入力します。 その目的は、アップグレードの場合に、特定の設定と工場出荷時の設定を区別することです。 デフォルトの名前空間はです。 **カス**  — お客様向け

### 技術的なオプション {#technical-options}

ウィンドウの下部のセクションでは、アクティブにするオプションを選択できます。

次のオプションを使用できます。

* **[!UICONTROL E メールチャネル]** ::e メール配信を有効にします。 参照： [E メールチャネルパラメーター](#email-channel-parameters).
* **[!UICONTROL トラッキング]** :ターゲット母集団（開封数およびクリック数）の追跡を有効にする場合。 参照： [トラッキング設定](#tracking-configuration).
* **[!UICONTROL バウンスメールの管理]** :受信メールの受信に使用する POP アカウントを定義する場合。 参照： [バウンスメールの管理](#managing-bounced-emails).
* **[!UICONTROL LDAP 統合]** :LDAP ディレクトリを介してユーザー認証を設定する場合。 参照： [LDAP を介した接続](../../installation/using/connecting-through-ldap.md).

## E メールチャネルパラメーター {#email-channel-parameters}

次の手順では、メッセージヘッダーに表示する情報を定義できます。

これらのパラメーターは、配信テンプレートで個別に、または（ユーザーが必要な権限を持っている場合）各配信に個別にオーバーロードできます。

### 配信 E メールのパラメーター {#parameters-for-delivered-emails}

![](assets/s_ncs_install_deployment_wiz_04.png)

次のパラメーターを指定します。

* **[!UICONTROL 送信者名]** :送信者の名前を入力します。
* **[!UICONTROL 送信者のアドレス]** :送信者の E メールアドレスを入力します。 Adobe Campaignから E メールを送信する際に、 **送信者のアドレス** メールボックスは監視されておらず、マーケティングユーザーはこのメールボックスにアクセスできません。 Adobe Campaignでは、このメールボックスで受信したメールの自動返信や自動転送もできません。 配信品質のベストプラクティスの詳細を説明します [このドキュメント](https://experienceleague.adobe.com/docs/deliverability-learn/deliverability-best-practice-guide/additional-resources/campaign/ac-starting-new-platform.html){_blank}.

* **[!UICONTROL 返信アドレスのテキスト]** :受信者が **[!UICONTROL 返信]** 」ボタンをクリックします。
* **[!UICONTROL 返信アドレス]** :受信者が **[!UICONTROL 返信]** 」ボタンをクリックします。 の目的 **返信アドレス** フィールドは、受信者が **送信者のアドレス**.  このアドレスは、有効な電子メールアドレスで、監視対象のメールボックスにリンクされ、顧客がホストする必要があります。  例えば、サポート用メールボックスの場合があります。 `customer-care@customer.com`:e メールが読み取られ、応答される場所。

* **[!UICONTROL エラーアドレス]** :エラーが発生したメッセージの E メールアドレスを入力します。 ターゲットアドレスが存在しないことが原因でAdobe Campaignサーバーが受信した E メールを含む、バウンスメールの処理に使用される技術的なアドレスです。 このアドレスは、有効な電子メールアドレスで、監視対象のメールボックスにリンクされ、顧客がホストする必要があります。 例えば、バウンスメールボックスの場合があります。 `errors@customer.com`.


これに加えて、 **マスク** 送信者のアドレスとエラーアドレスに対して認証済み。 必要に応じて、これらのマスクをコンマで区切ります。 この設定はオプションです。 フィールドに入力すると、Adobe Campaignは配信時（分析中に、アドレスに変数が含まれていない場合は分析中）にアドレスが有効であることを確認します。 この動作モードでは、配信の問題を引き起こす可能性のあるアドレスを一切使用しないトリガーにします。 配信アドレスは、配信サーバー上で設定する必要があります。

>[!NOTE]
>
>* これらの設定は、Campaign プラットフォームオプションに保存されます。 [詳細情報](../../installation/using/configuring-campaign-options.md)
> 
>* マルチブランディング設定の場合、エラーアドレスを適応させ、E メールルーティング外部アカウントからこの設定を上書きすることができます。 [詳細情報](../../installation/using/external-accounts.md#email-routing-external-account)
>


### アドレスに使用できる文字 {#characters-authorized-in-addresses}

<!--This window enables you to define, for all email campaigns, the delivery and address-quality management options.-->

Adobe Campaignデータベースで、すべての電子メールアドレスを次のように作成する必要があります。 `x@y.z`. この **x**, **y** および **z** 文字は空にできず、許可されていない文字を含めることはできません。

ここで、データベースの email フィールドに、許可する文字（「データポリシー」）を定義できます。 リストに含まれていない文字は禁止されるので、インターフェイス、Web フォーム、データのインポートを使用してデータベースに情報を入力する際に拒否されます。

次の 2 つのリストを使用できます。 **ヨーロッパのみ** または **米国のみ**. 必要に応じて、その他の文字を追加できます。

### 配信パラメーター {#delivery-parameters}

この **詳細設定パラメーター…** リンクを使用すると、配信オプション、再試行と強制隔離にリンクされたパラメーターにアクセスできます。

![](assets/s_ncs_install_deployment_wiz_05.png)

このウィンドウでは、すべての E メールキャンペーンに対して、配信および住所の質の管理オプションを定義できます。

次のオプションを使用できます。

* **[!UICONTROL メッセージの配信期間]** :この時間を過ぎると、配信は停止されます（デフォルトでは 5 日間）。
* **[!UICONTROL オンラインリソースの有効期間]** :ミラーページを生成するために受信者プロファイルからの情報を保持する時間。
* **[!UICONTROL 今後連絡を希望しない受信者を除外]** :このオプションを選択した場合、「受信者ブロックリストを」では連絡されません。
* **[!UICONTROL 重複を自動的に無視]** :このオプションを選択した場合、重複するアドレスは配信されません。

>[!NOTE]
>
>ホストインストールまたはハイブリッドインストールで、 [拡張 MTA](../../delivery/using/sending-with-enhanced-mta.md)、 **[!UICONTROL メッセージの配信期間]** は、 **三五日以下**. 3.5 日を超える値を定義した場合、その値は考慮されません。

### 再試行パラメーター {#retry-parameters}

リカバリに関する情報は、 **回復期間** および **リカバリ数** フィールド：受信者に到達できない場合 ( 例えば、受信ボックスがいっぱいの場合、デフォルトでは、各試行の間隔（最大配信時間）が 1 時間で、5 回連絡が試行されます。 これらの値は、必要に応じて変更できます。

>[!NOTE]
>
>ホストインストールまたはハイブリッドインストールで、 [拡張 MTA](../../delivery/using/sending-with-enhanced-mta.md)に値を指定しない場合、Campaign 再試行パラメーターは使用されなくなりました。 ソフトバウンスの再試行とその間隔は、メッセージの電子メールドメインから返されるバウンス応答のタイプと重大度に基づいて、Enhanced MTA が決定します。

### 強制隔離パラメーター {#quarantine-parameters}

強制隔離の設定オプションを次に示します。

* **[!UICONTROL 2 つの重要なエラーの間の期間]** :値（デフォルトでは「1d」）を入力します。1 日 ) を指定して、エラーが発生した場合にエラーカウンターを増やすまでのアプリケーションの待機時間を定義します。
* **[!UICONTROL 強制隔離前のエラーの最大数]** :この値に達すると、e メールアドレスが強制隔離されます（デフォルトは「5」）。6 回目のエラー発生時にアドレスが強制隔離されます )。 これは、連絡先が後続の配信から自動的に除外されることを意味します。

## バウンスメールの管理 {#managing-bounced-emails}

バウンスメールは、配信エラーの検証に非常に重要です。 ルールが原因を特定したら、これらのエラーはNP@Iに分類されます。

この手順は、 **E メールチャネル** および **バウンスメール** 管理オプションは、デプロイウィザードの最初の段階で選択します。 参照： [一般パラメーター](#general-parameters).

この段階では、バウンスメール管理の設定を定義できます。

![](assets/s_ncs_install_deployment_wiz_06.png)

### 受信メールの取得に使用する POP アカウント {#pop-account-used-to-retrieve-incoming-mails}

受信メールを取得するためのアカウントに接続するパラメーターを指定します。

* **[!UICONTROL ラベル]** :以下に示すすべてのパラメーターを含む名前
* **[!UICONTROL サーバー]** :バウンスメール（受信メール）の取得に使用するサーバー
* **[!UICONTROL セキュリティ]** :必要に応じて、「 」を選択します。 **[!UICONTROL SSL]** をドロップダウンリストから選択します。
* **[!UICONTROL ポート]** :サーバポート（通常は 110）
* **[!UICONTROL アカウント]** :バウンスメールに使用するアカウントの名前
* **[!UICONTROL パスワード]** :アカウントに関連付けられたパスワード。

POP 設定を指定したら、 **テスト** 正しいことを確認するために。

### 未処理のバウンスメール {#unprocessed-bounce-mails}

バウンスはAdobe Campaignで自動的に処理され、 **管理/Campaign Management/配信不能件数の管理/配信ログの検証** ノード。 詳しくは、 [バウンスメール管理](../../delivery/using/understanding-delivery-failures.md#bounce-mail-management).

未処理のバウンスは、Adobe Campaignインターフェイスに表示されません。 次のフィールドを使用してサードパーティのメールボックスに転送されない限り、それらは自動的に削除されます。

* **[!UICONTROL 転送先アドレス]** :Adobe Campaignプラットフォームで収集されたすべてのエラーメッセージ（処理済みまたは未処理）をサードパーティのアドレスに転送するには、このフィールドに入力します。
* **[!UICONTROL エラーのアドレス]** :inMail プロセスで選定できなかったエラーメッセージのみをサードパーティのアドレスに転送するには、このフィールドに入力します。
* **[!UICONTROL SMTP サーバー]** :未処理のバウンス E メールを送信するために使用するサーバー。

>[!IMPORTANT]
>
>未処理のバウンス E メールを転送する場合は、Adobeは **[!UICONTROL エラーのアドレス]** フィールドに入力します。 ただし、メールサーバーに大きな負荷がかかる可能性があるので、使用するアドレスが定期的にチェックされていることを確認してください。 詳しくは、アカウント担当者にお問い合わせください。

## トラッキング設定 {#tracking-configuration}

次の手順では、インスタンスのトラッキングを設定できます。 インスタンスを宣言し、トラッキングサーバーに登録する必要があります。

この手順は、 **E メールチャネル** および **トラッキング** オプションがデプロイウィザードの最初のページで選択されます。 参照： [一般パラメーター](#general-parameters).

Web トラッキング（トラッキングモード、タグの作成と挿入など）について詳しくは、 [このドキュメント](../../configuration/using/about-web-tracking.md).

### 動作の原則 {#operating-principle}

インスタンスのトラッキングを有効にすると、送信中に配信の URL が変更され、トラッキングが有効になります。

* デプロイウィザードのこのページで入力した外部 URL（セキュリティで保護されているかどうかに関わらず）に関する情報を使用して、新しい URL を作成します。 この情報に加えて、変更されたリンクには次の情報が含まれます。配信の識別子、受信者および URL。

  トラッキング情報は、トラッキングサーバー上のAdobe Campaignによって収集され、受信者プロファイルと配信にリンクされたデータ ( **[!UICONTROL トラッキング]** 」タブ ) を参照してください。

  内部 URL に関する情報は、Adobe Campaignアプリケーションサーバーがトラッキングサーバーに接続する場合にのみ使用されます。

  詳しくは、 [トラッキングサーバー](#tracking-server).

* URL を設定したら、トラッキングを有効にする必要があります。 これをおこなうには、インスタンスをトラッキングサーバーに登録する必要があります。

  詳しくは、 [トラッキングを保存中](#saving-tracking).

### トラッキングサーバー {#tracking-server}

![](assets/s_ncs_install_deployment_wiz_08.png)

このインスタンスでのトラッキングの効率を保証するには、次の情報を表示する必要があります。
<!--With Mid-sourcing architecture, you can externalize tracking management. To do this:-->

* **[!UICONTROL 外部 URL]** および/または **[!UICONTROL 外部 URL を保護]** :送信する E メールに使用するリダイレクト URL を入力します。
* **[!UICONTROL 内部 URL]** :ログの収集と URL のアップロードのために、Adobe Campaignサーバーがトラッキングサーバーに接続する際にのみ使用される URL。 インスタンスに関連付ける必要はありません。

  URL を指定しない場合、トラッキング URL がデフォルトで使用されます。

ミッドソーシングアーキテクチャを使用して、トラッキング管理を外部化できます。 手順は次のとおりです。

1. オプションを選択します。 **[!UICONTROL トラッキング管理を外部化]** :ミッドソーシングサーバーをトラッキングサーバーとして使用できます。
1. 次の項目に **[!UICONTROL 外部アカウント]** および **[!UICONTROL インスタンス名]** ミッドソーシングサーバーに接続できるフィールド。

   詳しくは、 [ミッドソーシングサーバー](../../installation/using/mid-sourcing-server.md).

1. 次をクリック： **[!UICONTROL トラッキングインスタンスを有効にする]** ボタンをクリックして、サーバーへの接続を承認します。

   ![](assets/s_ncs_install_deployment_wiz_18.png)

### トラッキングの保存 {#saving-tracking}

URL に値が入力されたら、トラッキングサーバーを登録する必要があります。

リンクをクリックします。 **トラッキングサーバーへの登録** 次に、使用可能なオプションの 1 つを選択します。

![](assets/s_ncs_install_deployment_wiz_09.png)

トラッキングを実装するための 3 つのタイプのアーキテクチャが考えられます。

1. **既存のインスタンスのトラッキングのサポートを追加**

   この選択は、他のニーズ（MTA サーバーなど）のためにインスタンスが既に作成されている場合に、 トラッキングサーバーとして使用されるサーバー上に存在することを確認します。

   ![](assets/s_ncs_install_deployment_wiz_11.png)

   のパスワードを入力 **内部** トラッキングインスタンスを設定するために、リダイレクトサーバー上のアカウントを使用します。

   >[!NOTE]
   >
   >複数のトラッキングサーバーを使用する場合は、すべて同じ名前とパスワードを使用する必要があります。

   インスタンスの名前とパスワードを指定します。

1. **トラッキング専用の新しいインスタンスを作成**

   このオプションは、トラッキングインスタンスがトラッキング用に予約されていて、他のアプリケーションモジュールがない場合に役立ちます。

   ![](assets/s_ncs_install_deployment_wiz_10.png)

   のパスワードを入力 **内部** トラッキングインスタンスを設定するために、リダイレクトサーバー上のアカウントを使用します。

   >[!NOTE]
   >
   >複数のトラッキングサーバーを設定する場合は、すべて同じパスワードを使用する必要があります。

   インスタンスの名前、パスワード、および関連する DNS マスク（例： ）を指定します。 **[!UICONTROL キャンペーン*]**.

1. **既に設定済みのトラッキングインスタンスを検証します**

   このオプションは、 **内部** アカウントこの場合、トラッキングサーバー上に事前に設定されているトラッキングアカウントが表示されます。 トラッキングインスタンスを検証するリダイレクションサーバーのトラッキングアカウントのパスワードを入力します。

   ![](assets/s_ncs_install_deployment_wiz_17.png)

   検証するインスタンスの名前を指定します。

クリック **承認** をクリックして、トラッキングサーバーでの記録プロセスを開始します。

前のウィンドウに戻ると、トラッキングサーバーレベルでの登録を確認するメッセージが表示されます。

![](assets/s_ncs_install_deployment_wiz_tracking_ok.png)

URL 検索にリンクされたパラメーター **は変更できません** 標準インストール用。 その他のパラメーターについては、Adobeにお問い合わせください。

## モバイルチャネルパラメーター {#mobile-channel-parameters}

次の手順では、モバイルへの配信（SMS および WAP プッシュ）のデフォルト設定を定義できます。

>[!NOTE]
>
>モバイルチャネルはオプションです。このステージは、購入済みの場合にのみ表示されます。 使用許諾契約書を確認してください。

![](assets/s_ncs_install_deployment_wiz_12.png)

### SMS 配信用のデフォルトアカウント {#default-account-for-sms-delivery}

次の情報を入力します。

* **[!UICONTROL ラベル]** :この SMS/Wap プッシュアカウントの名前を入力します。 例えば、ルータ名を使用できます。
* の **[!UICONTROL サーバー]**, **[!UICONTROL ポート]**, **[!UICONTROL アカウント]**, **[!UICONTROL パスワード]**, **[!UICONTROL コネクタ]**, **[!UICONTROL エンドポイントを送信]**, **[!UICONTROL 受信エンドポイント]**, **[!UICONTROL 通知エンドポイント]** フィールド：必要な設定については、サービスプロバイダーにお問い合わせください。

### 送信された SMS のパラメーター {#parameters-of-sms-sent}

内 **優先度** ドロップダウンリスト：「標準」、「高」または「至急」を選択して、送信するメッセージに適用します。

### 詳細設定パラメーター {#advanced-parameters}

この **詳細設定パラメーター…** 「 」リンクを使用して、再試行および強制隔離のオプションにアクセスできます。

![](assets/s_ncs_install_deployment_wiz_13.png)

再試行に関する情報は、 **再試行の期間** および **再試行数** フィールド：モバイルに到達できない場合、デフォルトでは、15 分以上の間隔（最大配信期間）で、プログラムは 5 回再試行します。 これらの値は、ニーズに合わせて調整できます。

強制隔離の設定オプションを次に示します。

* **[!UICONTROL 2 つの重大なエラー間の時間]** :デフォルト値を入力します（デフォルトは「1d」）。day) を使用して、エラーカウンターを増分してエラーを待機する時間を定義します。
* **[!UICONTROL 強制隔離前のエラーの最大数]** :この値に達すると、モバイル番号が強制隔離されます（デフォルトでは「5」）。6 回目のエラー発生時に番号が強制隔離されます )。 つまり、連絡先は自動的にそれ以降の配信から除外されます。

## 地域設定 {#regional-settings}

この段階では、データポリシーの環境設定を含めることができます。

![](assets/s_ncs_install_deployment_wiz_14.png)

* **[!UICONTROL すべての電話番号を国際電話番号と見なす]** :このオプションを選択すると、国際形式が電話番号に適用されます（書式を適用する前に桁数がチェックされないので、国のプレフィックスは必須です）。 このオプションを選択しない場合は、自分で国際電話番号に「+」または「00」というプレフィックスを付ける必要があります。
* **[!UICONTROL すべての電話番号を国際形式で保存]** :このオプションは、 **国内** 読み込まれた、または編集された電話番号。 国内形式（425 555 0150 など）を使用するか国際形式 ( 例：+1 425 555 0150)

## インターネットからのアクセス {#access-from-the-internet}

>[!IMPORTANT]
>
>プライバシー保護のために、すべての外部リソースに対して HTTPS を使用することをお勧めします。

この手順では、インターネットに公開されているAdobe Campaignページのアクセス URL を定義できます。

また、Web フォームにリンクするパブリケーションオプションもここに指定する必要があります。

![](assets/s_ncs_install_deployment_wiz_15.png)

### Web 上で公開されるサーバー {#servers-exposed-on-the-web}

このページを使用してサーバー URL を以下のように設定します。

1. インターネットに公開されているアプリケーションサーバーにアクセスする：購読/購読解除用のフォーム、エクストラネットなど
1. Web で公開されていないリソースのアプリケーションサーバーにアクセスする：フォーム、イントラネット、確認ページ。
1. 配信のミラーページにアクセスします。

   ミラーページは、E メールのコンテンツを表示する動的ページです。 受信者に送信されるメッセージに挿入されたリンクを介してアクセスされ、パーソナライズされた要素を含めることができます。 ミラーページを使用すると、受信者は、配信フォーマット ( テキストまたはHTML) に関係なく、E メールソフトウェアではなく、インターネットブラウザーでメッセージを読むことができます。 ただし、特定の配信に対してミラーページが生成されるのは、必要なHTMLコンテンツが定義されている場合のみです。

Adobe Campaignでは、これらの 3 つの URL を区別して、複数のプラットフォームにわたって負荷を分散できます。


>[!NOTE]
>
>* これらの設定は、Campaign プラットフォームオプションに保存されます。 [詳細情報](../../installation/using/configuring-campaign-options.md)
>* マルチブランディング設定の場合、ミラーページの URL を適応させ、E メールルーティング外部アカウントからこの設定を上書きすることができます。 [詳細情報](../../installation/using/configuring-campaign-options.md)


## パブリックリソースの管理 {#managing-public-resources}

>[!IMPORTANT]
>
>プライバシー保護のために、すべての外部リソースに対して HTTPS を使用することをお勧めします。

キャンペーンに関連する E メールやパブリックリソースで使用される画像を外部から表示するには、その画像を外部からアクセスできるサーバー上に置く必要があります。その後、外部の受信者やオペレーターが使用できるようになります。

![](assets/s_ncs_install_deployment_wiz_img_uploading.png)

この手順では、次のように入力する必要があります。

1. 新しいパブリックリソース URL です。 詳しくは、 [パブリックリソース URL](#public-resources-url) 」セクションに入力します。
1. 配信の画像検出モード。 詳しくは、 [配信画像の検出](#delivery-image-detection) 」セクションに入力します。
1. 公開オプション。 詳しくは、 [公開モード](#publication-modes) 」セクションに入力します。

パブリックリソースには、 **管理/リソース/オンライン/パブリックリソース** Adobe Campaignツリーのノード。 ライブラリで収集し、E メールに含めることができますが、キャンペーンやタスク、コンテンツ管理でも使用できます。

![](assets/install_pub_resources_view.png)

### パブリックリソース URL {#public-resources-url}

1 つ目のフィールドでは、アップロード後のリソースに使用する URL の開始を指定できます。 アップロードすると、リソースにはこの新しい URL からアクセスできます。

配信では、パブリックリソースライブラリに保存された画像や、その他のローカル画像やサーバーに保存された画像を使用できます。

* 電子メール画像の場合、 **https://** server **/res/img** URL。

  この値は、配信ごとに上書きできます。

* パブリックリソースの場合は URL **https://** server **/res/**&#x200B;インスタンス&#x200B;****場所&#x200B;**インスタンス**は、トラッキングインスタンスの名前です。

### 配信画像の検出 {#delivery-image-detection}

配信では、パブリックリソースライブラリに保存された画像や、その他のローカル画像やサーバーに保存された画像を使用できます。

フィールド **URL マスク** では、画像を自動的にアップロードする際にスキップする URL マスクのリストを指定できます。 例えば、外部からアクセス可能なサイト（特にインターネットサイト）に格納されている画像を使用する場合、このフィールドにサイトの URL を入力できます。

![](assets/s_ncs_install_deployment_wiz_img_mask.png)

複数の URL マスクを指定する場合は、コンマで区切ります。

* E メールでの画像の使用と管理について詳しくは、 [この節](../../delivery/using/defining-the-email-content.md#adding-images).
* 配信ウィザードでは、これらの URL から呼び出された画像のステータスは「無視」になります。

### 公開モード {#publication-modes}

ウィザードの下部のセクションで、パブリックリソースおよび画像の公開オプションを選択できます。

次のパブリッシュモードを使用できます。

* トラッキングサーバー

  リソースは異なるトラッキングサーバーに自動的にコピーされます。 これらは、ステップで設定されます [トラッキング設定](#tracking-configuration).

* その他のAdobe Campaignサーバー

  リソースをコピーする他のAdobe Campaignサーバーを 1 つ使用することもできます。

  サーバー側で、専用のAdobe Campaignサーバーを使用するには、次のコマンドを使用して新しいインスタンスを作成する必要があります。

  ```
  nlserver config -addtrackinginstance:<trackingA>/<trackingA*>
  ```

  次に、パスワードを入力します。

  専用サーバーのパラメーターは、 **[!UICONTROL メディア URL]**, **[!UICONTROL パスワード]** および **[!UICONTROL インスタンス名]** フィールド。

  ![](assets/s_ncs_install_images_upload_b.png)

* 手動公開スクリプト（パブリックリソースのみ）

  ![](assets/s_ncs_install_images_upload_c.png)

  スクリプトを使用して画像を公開できます。

   * 次のスクリプトを作成する必要があります。その内容は、設定によって異なります。
   * スクリプトは、次のコマンドによって呼び出されます。

     ```
     [INSTALL]/copyToFrontal.vbs "$(XTK_INSTALL_DIR)\var\<instance>\upload\" "img1,img2,img3"
     ```

     場所 `[INSTALL]` は、Adobe Campaignインストールフォルダーへのアクセスパスです。

   * UNIX の場合、スクリプトが実行可能であることを確認します。

画像の場合、 **NmsDelivery_ImageSubDirectory** 1 つ以上のフロントサーバーに対するオプション。 これらのサーバーには画像が保存され、新しく設定された URL 経由で画像にアクセスできるようになります。

手動のパブリッシュスクリプトを使用せずにAdobe Campaignサーバーでパブリッシュした場合、デフォルトでは、配信の画像は `$(XTK_INSTALL_DIR)/var/res/img/ directory`. 対応する URL は次のとおりです。 **`https://server/res/img`**.

`XTK_INSTALL_DIR)/var/res/$(INSTANCE_NAME)`.対応する URL は次のようになります。 **`https://server/res/instance`** instance は、トラッキングインスタンスの名前です。

>[!NOTE]
>
>パブリックリソースストレージディレクトリを変更できます。 詳しくは、 [パブリックリソースの管理](#managing-public-resources).

### パブリックリソースの同期 {#synchronizing-public-resources}

この機能を使用すると、次のことが可能になります。 **パブリックリソースの同期** 複数のスペア・サーバ上

パブリックリソースがトラッキングサーバーに存在しない場合、またはリソースが 404 エラーを返した場合、トラッキングサーバーは、いずれかのスペアサーバーでリソースを探します。

スペアサーバーの宣言と設定は、マーケティングサーバーの **serverConf.xml** ファイル。 次の **serverConf.xml** を [セクション](../../installation/using/the-server-configuration-file.md).

**宣言**

```
<redirection>
<spareServer enabledIf="" id="" url=""/>
</redirection>
```

**設定**

同期が必要なパブリックリソースごとに、status 属性を `<url>` 要素を `<relay>` パーツ：

status 属性には、次の 3 つの値のいずれかを指定できます。

* スペア：パブリックリソースが同期されています

* 標準：既存の動作（同期なし）

* ブラックリスト：404 エラーが返された場合、URL はブロックリストに追加されます。 内の URL の長さ ( 秒ブロックリスト) は、 **timeout** 属性のデフォルト値が 60 秒である。

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

デプロイウィザードの最後の段階では、古いデータの自動パージを設定できます。 値は日数で表します。

![](assets/s_ncs_install_deployment_wiz_16.png)

データは、データベースクリーンアップワークフローで自動的に削除されます。 このワークフローを設定および操作する方法と削除された項目の詳細については、この節を参照してください [文書](../../production/using/database-cleanup-workflow.md).
