---
product: campaign
title: インスタンスのデプロイ
description: Campaign デプロイメントウィザードの詳細情報
feature: Installation, Instance Settings, Deployment
badge-v7-prem: label="オンプレミス／ハイブリッドのみ" type="Caution" url="https://experienceleague.adobe.com/docs/campaign-classic/using/installing-campaign-classic/architecture-and-hosting-models/hosting-models-lp/hosting-models.html?lang=ja" tooltip="オンプレミスデプロイメントとハイブリッドデプロイメントにのみ適用されます"
audience: installation
content-type: reference
topic-tags: initial-configuration
exl-id: 8b07447c-9a86-4b56-8d29-e0b01357a6ec
source-git-commit: 62ab16b206563aa25b8943e606d03a3184eb00db
workflow-type: tm+mt
source-wordcount: '3547'
ht-degree: 5%

---

# インスタンスのデプロイ{#deploying-an-instance}

>[!NOTE]
>
>サーバーサイド設定は、Adobeがホストするデプロイメントに対してのみ、Adobeが実行できます。 様々なデプロイメントの詳細については、[&#x200B; モデルのホスティング &#x200B;](../../installation/using/hosting-models.md) の節または [&#x200B; このページ &#x200B;](../../installation/using/capability-matrix.md) を参照してください。

## 配置ウィザード {#deployment-assistant}

Adobe Campaignには、Adobe Campaign クライアントコンソールで使用できるグラフィカルなアシスタントが用意されており、接続先のインスタンスのパラメーターを定義できます。

デプロイメントウィザードを起動するには、**ツール/詳細/デプロイメントウィザード** を選択します。

![](assets/s_ncs_install_deployment_wiz_01.png)

設定手順は、以下のとおりです。

1. [一般パラメーター](#general-parameters)
1. [メールチャネルのパラメーター](#email-channel-parameters)
1. [バウンスメールの管理](#managing-bounced-emails)
1. [トラッキング設定](#tracking-configuration)
1. [モバイルチャネルのパラメーター](#mobile-channel-parameters)
1. [地域設定](#regional-settings)
1. [インターネットからのアクセス](#access-from-the-internet)
1. [パブリックリソースの管理](#managing-public-resources)
1. [データのパージ](#purging-data)

## 一般パラメーター {#general-parameters}

デプロイメントウィザードの最初の手順では、インスタンスに関する一般情報を入力できます。

![](assets/s_ncs_install_deployment_wiz_02.png)

### 一般情報 {#general-information}

ウィンドウの下部のセクションでは、アクティブにするオプションを選択できます。

* **[!UICONTROL 請求に使用する顧客識別子]**：インスタンス名とバージョン番号を指定できます。
* **[!UICONTROL 顧客の共通名]**：会社名を含む文字列を入力します。 この情報は、購読解除リンクで使用できます。
* **[!UICONTROL 名前空間]**：短い識別子を小文字で入力します。 アップグレードを行う場合、お客様固有の設定と工場出荷時の設定を区別することが目的です。 顧客のデフォルトの名前空間は **cus** です。

### 技術的なオプション {#technical-options}

ウィンドウの下部のセクションでは、アクティブにするオプションを選択できます。

次のオプションを使用できます。

* **[!UICONTROL メールチャネル]**：メール配信を有効化します。 [&#x200B; メールチャネルパラメーター &#x200B;](#email-channel-parameters) を参照してください。
* **[!UICONTROL トラッキング]**：ターゲット母集団（開封数およびクリック数）のトラッキングを有効にします。 [&#x200B; トラッキング設定 &#x200B;](#tracking-configuration) を参照してください。
* **[!UICONTROL バウンスメールの管理]**：受信メールの取得に使用する POP アカウントを定義します。 [&#x200B; バウンスメールの管理 &#x200B;](#managing-bounced-emails) を参照してください。
* **[!UICONTROL LDAP 統合]**:LDAP ディレクトリを使用してユーザー認証を設定します。 [LDAP 経由の接続 &#x200B;](../../installation/using/connecting-through-ldap.md) を参照してください。

## メールチャネルのパラメーター {#email-channel-parameters}

次の手順では、メッセージヘッダーに表示する情報を定義できます。

これらのパラメーターは、配信テンプレートでオーバーロードすることも、配信ごとに個別にオーバーロードすることもできます（ユーザーに必要な権限がある場合）。

### 配信メールのパラメーター {#parameters-for-delivered-emails}

![](assets/s_ncs_install_deployment_wiz_04.png)

次のパラメーターを指定します。

* **[!UICONTROL 送信者名]**：送信者の名前を入力します。
* **[!UICONTROL 送信者のアドレス]**：送信者のメールアドレスを入力します。 Adobe Campaignから電子メールを送信する際、**送信者アドレス** メールボックスは監視されず、マーケティングユーザーはこのメールボックスにアクセスできません。 Adobe Campaignには、このメールボックスで受信した電子メールを自動返信または自動転送する機能もありません。 配信品質のベストプラクティスについて詳しくは [&#x200B; このドキュメント &#x200B;](https://experienceleague.adobe.com/docs/deliverability-learn/deliverability-best-practice-guide/additional-resources/campaign/ac-starting-new-platform.html){_blank} を参照してください。

* **[!UICONTROL 返信アドレステキスト]**：受信者が **[!UICONTROL 返信]** ボタンをクリックしたときに使用される名前を入力します。
* **[!UICONTROL 返信アドレス]**：受信者がメールクライアントソフトウェアの **[!UICONTROL 返信]** ボタンをクリックしたときに使用するメールアドレスを入力します。 「**返信アドレス**」フィールドは、受信者が **送信者アドレス** とは異なるアドレスに返信する場合に使用します。  このアドレスは、有効なメールアドレスで、監視対象のメールボックスにリンクされ、顧客によってホストされている必要があります。  例えば、電子メールが読まれて返信される `customer-care@customer.com` のようなサポート用メールボックスを指定できます。

* **[!UICONTROL エラーアドレス]**：エラーが発生したメッセージのメールアドレスを入力します。 これは、バウンスメールの処理に使用される技術的なアドレスです。これには、存在しないターゲットアドレスが原因でAdobe Campaign サーバーが受信したメールも含まれます。 このアドレスは、有効なメールアドレスで、監視対象のメールボックスにリンクされ、顧客によってホストされている必要があります。 例えば、`errors@customer.com` のようなバウンスメールボックスを指定できます。 このアドレスは、配信または配信テンプレートで、配信/配信テンプレートプロパティの「**SMTP**」タブから変更できます。 詳しくは、[Campaign v8 ドキュメント](https://experienceleague.adobe.com/docs/campaign/campaign-v8/send/emails/email-parameters.html#managing-bounce-emails){target="_blank"}を参照してください。

これに加えて、送信者アドレスとエラーアドレスに対して許可されている **マスク** を指定できます。 必要に応じて、これらのマスクはコンマで区切ることができます。 この設定はオプションです。 フィールドに値を入力すると、Adobe Campaignは配信時に（分析時に、アドレスに変数が含まれていない場合は）、アドレスが有効かどうかを確認します。 このオペレーティングモードでは、配信の問題をトリガーにする可能性のあるアドレスを使用しません。 配信アドレスは、配信サーバーで設定する必要があります。

>[!NOTE]
>
>* これらの設定は、Campaign プラットフォームオプションに保存されます。 [詳細情報](../../installation/using/configuring-campaign-options.md)。
> 
>* マルチブランディング設定の場合は、エラーアドレスを調整し、メールルーティング外部アカウントのこの設定を上書きできます。 [詳細情報](../../installation/using/external-accounts.md#email-routing-external-account)。
>


### アドレスに使用できる文字 {#characters-authorized-in-addresses}

<!--This window enables you to define, for all email campaigns, the delivery and address-quality management options.-->

Adobe Campaign データベースで、すべてのメールアドレスを次のように作成する必要があります。`x@y.z`。 **x**、**y** および **z** 文字は空にすることはできず、許可されていない文字を含めることはできません。

ここで、データベースの「メール」フィールドに許可された文字（「データポリシー」）を定義できます。 リストに含まれない文字は禁止されるため、インターフェイスを使用してデータベースに情報を入力する場合、web フォームを使用する場合、およびデータを読み込む場合に拒否されます。

**ヨーロッパのみ** または **米国のみ** の 2 つのリストを使用できます。 必要に応じて、他の文字を追加できます。

### 配信パラメーター {#delivery-parameters}

「**詳細設定パラメーター…**」リンクを使用すると、配信オプション、再試行および強制隔離にリンクされたパラメーターにアクセスできます。

![](assets/s_ncs_install_deployment_wiz_05.png)

このウィンドウを使用すると、すべてのメールキャンペーンに対して、配信およびアドレス品質管理オプションを定義できます。

次のオプションを使用できます。

* **[!UICONTROL メッセージの配信期間]**：この期間を超えると、配信は停止されます（デフォルトでは 5 日）。
* **[!UICONTROL オンラインリソースの有効期間]**：ミラーページを生成するために受信者プロファイルの情報を保持する時間です。
* **[!UICONTROL 連絡を希望しない受信者を除外]**：このオプションを選択すると、*ブロックリストの受信者には連絡されません。
* **[!UICONTROL 重複を自動的に無視]**：このオプションを選択すると、重複するアドレスには配信されません。

>[!NOTE]
>
>ホストインストールまたはハイブリッドインストールで、[Enhanced MTA](../../delivery/using/sending-with-enhanced-mta.md) にアップグレードした場合、**[!UICONTROL メッセージの配信期間]** は、**3.5 日以内** に設定されている場合にのみ使用されます。 3.5 日を超える値を定義した場合、その値は考慮されません。

### 再試行パラメーター {#retry-parameters}

復元に関する情報は、「**回復期間**」フィールドと「**復元数**」フィールドに表示されます。例えば、受信者の受信ボックスがいっぱいであるなど、受信者に到達できない場合、デフォルトでは、プログラムは受信者と 5 回の通信を試みます。各試行の間隔は 1 時間（最大配信時間）です。 これらの値は、ニーズに合わせて変更できます。

>[!NOTE]
>
>ホストインストールまたはハイブリッドインストールで、[Enhanced MTA](../../delivery/using/sending-with-enhanced-mta.md) にアップグレードした場合、Campaign の再試行パラメーターは使用されなくなります。 ソフトバウンスの再試行とその間隔は、メッセージの電子メールドメインから返されるバウンス応答のタイプと重大度に基づいて、Enhanced MTA が決定します。

### 強制隔離パラメーター {#quarantine-parameters}

強制隔離の設定オプションは次のとおりです。

* **[!UICONTROL 2 つの重要なエラー間の時間]**：値（デフォルトでは「1d」:1 日）を入力して、失敗の場合にエラーカウンターを増分するまでのアプリケーションの待機時間を定義します。
* **[!UICONTROL 強制隔離前のエラーの最大数]**：この値に達すると、メールアドレスが強制隔離されます（デフォルトでは「5」：アドレスは 6 回目のエラーで強制隔離されます）。 これは、連絡先が後続の配信から自動的に除外されることを意味します。

## バウンスメールの管理 {#managing-bounced-emails}

バウンスメールは、配信エラーを検証するために非常に重要です。 これらのエラーは、ルールで原因が特定されると、NP@Iに分類されます。

この手順は、デプロイメントウィザードの最初の段階で **メールチャネル** と **バウンスメール** の管理オプションが選択されている場合にのみ使用できます。 [&#x200B; 一般パラメーター &#x200B;](#general-parameters) を参照してください。

このステージでは、バウンスメールを管理するための設定を定義できます。

![](assets/s_ncs_install_deployment_wiz_06.png)

### 受信メールの取得に使用される POP アカウント {#pop-account-used-to-retrieve-incoming-mails}

受信メールを取得するためにアカウントに接続するパラメーターを指定します。

* **[!UICONTROL Label]**：以下に示すすべてのパラメーターを含む名前。
* **[!UICONTROL サーバー]**：バウンスメール（受信メール）の取得に使用するサーバー
* **[!UICONTROL セキュリティ]**：必要に応じて、ドロップダウンリストから **[!UICONTROL SSL]** を選択します。
* **[!UICONTROL ポート]**：サーバーポート（通常は 110）、
* **[!UICONTROL アカウント]**：バウンスメールに使用するアカウント名
* **[!UICONTROL パスワード]**：アカウントに関連付けられているパスワード。

POP 設定を指定したら、「**テスト**」をクリックして、設定が正しいことを確認します。

### 未処理のバウンスメール {#unprocessed-bounce-mails}

バウンスはAdobe Campaignによって自動的に処理され、**管理/キャンペーン管理/配信不能件数の管理/配信ログの選定** ノードにリストされているルールが適用されます。 詳しくは、[&#x200B; バウンスメールの管理 &#x200B;](../../delivery/using/delivery-failures-quarantine.md#bounce-mail-management) を参照してください。

未処理のバウンスは、Adobe Campaign インターフェイスには表示されません。 次のフィールドを使用してサードパーティのメールボックスに転送されない限り、これらは自動的に削除されます。

* **[!UICONTROL 転送先アドレス]** :Adobe Campaign プラットフォームで収集されたすべてのエラーメッセージ（処理済みまたは未処理）をサードパーティアドレスに転送するには、このフィールドに入力します。
* **[!UICONTROL エラーのアドレス]** :inMail プロセスで選定できなかったエラーメッセージのみをサードパーティアドレスに転送する場合は、このフィールドに入力します。
* **[!UICONTROL SMTP サーバー]**：未処理のバウンスメールの送信に使用されるサーバー。

>[!IMPORTANT]
>
>未処理のバウンスメールを転送するには、Adobeでは **[!UICONTROL エラーのアドレス]** フィールドにのみ入力することをお勧めします。 ただし、メールサーバーに大きな負荷がかかる可能性があるので、使用するアドレスが定期的にチェックされていることを確認してください。 詳しくは、アカウント担当者にお問い合わせください。

## トラッキング設定 {#tracking-configuration}

次の手順では、インスタンスのトラッキングを設定できます。 インスタンスを宣言し、トラッキングサーバーに登録する必要があります。

この手順は、デプロイメントウィザードの最初のページで **メールチャネル** および **トラッキング** オプションが選択されている場合にのみ提供されます。 [&#x200B; 一般パラメーター &#x200B;](#general-parameters) を参照してください。

Web トラッキング（トラッキングモード、タグの作成と挿入など）について詳しくは、[&#x200B; このドキュメント &#x200B;](../../configuration/using/about-web-tracking.md) を参照してください。

### 動作の原則 {#operating-principle}

インスタンスのトラッキングを有効にすると、トラッキングを有効にするように配信内の URL が送信中に変更されます。

* デプロイメントウィザードのこのページに入力された外部 URL に関する情報（セキュアであるかどうかに関わらず）は、新しい URL を作成するために使用されます。 変更されたリンクには、これらの情報と共に、配信の識別子、受信者および URL が含まれます。

  トラッキング情報は、受信者プロファイルと配信にリンクされたデータを強化するために、Adobe Campaignによってトラッキングサーバーで収集されます（「トラッキング **[!UICONTROL タブ]**。

  内部 URL に関する情報は、Adobe Campaign アプリケーションサーバーがトラッキングサーバーに接続する際にのみ使用されます。

  詳しくは、[&#x200B; トラッキングサーバー &#x200B;](#tracking-server) を参照してください。

* URL を設定したら、トラッキングを有効にする必要があります。 それには、トラッキングサーバーにインスタンスを登録する必要があります。

  詳しくは、[&#x200B; トラッキングの保存 &#x200B;](#saving-tracking) を参照してください。

### トラッキングサーバー {#tracking-server}

![](assets/s_ncs_install_deployment_wiz_08.png)

このインスタンスでのトラッキングの効率を保証するには、次の情報を表示する必要があります。
<!--With Mid-sourcing architecture, you can externalize tracking management. To do this:-->

* **[!UICONTROL 外部 URL]** または **[!UICONTROL セキュア外部 URL]**：送信するメールで使用するリダイレクト URL を入力します。
* **[!UICONTROL 内部 URL]** :Adobe Campaign サーバーのみがログを収集して URL をアップロードするためにトラッキングサーバーに接続する際に使用する URL です。 インスタンスに関連付ける必要はありません。

  URL を指定しない場合、トラッキング URL がデフォルトで使用されます。

ミッドソーシングアーキテクチャを使用すると、トラッキング管理を外部化できます。 手順は次のとおりです。

1. **[!UICONTROL トラッキング管理を外部化]** オプションを選択する：これにより、ミッドソーシングサーバーをトラッキングサーバーとして使用できます。
1. **[!UICONTROL 外部アカウント]** および **[!UICONTROL インスタンス名]** フィールドに入力して、ミッドソーシングサーバーに接続できるようにします。

   詳しくは、[&#x200B; ミッドソーシングサーバー &#x200B;](../../installation/using/mid-sourcing-server.md) を参照してください。

1. **[!UICONTROL トラッキングインスタンスを有効にする]** ボタンをクリックして、サーバーへの接続を承認します。

   ![](assets/s_ncs_install_deployment_wiz_18.png)

### トラッキングの保存 {#saving-tracking}

URL を入力したら、トラッキングサーバーを登録する必要があります。

リンク **トラッキングサーバーの登録** をクリックし、使用可能なオプションの 1 つを選択します。

![](assets/s_ncs_install_deployment_wiz_09.png)

トラッキングを実装するためのアーキテクチャには、次の 3 つのタイプがあります。

1. **既存のインスタンスでのトラッキングのサポートの追加**

   この選択は、トラッキングサーバーとして使用されるサーバーで、他のニーズ（MTA サーバーなど）に対応するためにインスタンスが既に作成されている場合に適用されます。

   ![](assets/s_ncs_install_deployment_wiz_11.png)

   トラッキングインスタンスを設定するために、リダイレクションサーバー上の **内部** アカウントのパスワードを入力してください。

   >[!NOTE]
   >
   >複数のトラッキングサーバーを使用する場合、それらはすべて同じ名前とパスワードを使用する必要があります。

   インスタンスの名前とパスワードを指定します。

1. **トラッキング専用の新しいインスタンスを作成**

   このオプションは、トラッキングインスタンスがトラッキング用に予約されていて、他のアプリケーションモジュールを持たない場合に役立ちます。

   ![](assets/s_ncs_install_deployment_wiz_10.png)

   トラッキングインスタンスを設定するために、リダイレクションサーバー上の **内部** アカウントのパスワードを入力してください。

   >[!NOTE]
   >
   >複数のトラッキングサーバーが設定されている場合、それらはすべて同じパスワードを使用する必要があります。

   インスタンスの名前、パスワード、関連付けられている DNS マスク（**[!UICONTROL Campaign*]** など）を指定します。

1. **既に事前設定されているトラッキングインスタンスを検証する**

   このオプションは、**internal** アカウントのパスワードを持っていない場合に使用されます。この場合、トラッキングサーバーにトラッキングアカウントが事前設定されています。 トラッキングインスタンスを検証するための、リダイレクトサーバーのトラッキングアカウントのパスワードを入力します。

   ![](assets/s_ncs_install_deployment_wiz_17.png)

   検証するインスタンス名を指定します。

「**承認**」をクリックして、トラッキングサーバーでの記録プロセスを開始します。

前のウィンドウに戻ると、トラッキングサーバーレベルで登録を確認するメッセージが表示されます。

![](assets/s_ncs_install_deployment_wiz_tracking_ok.png)

標準インストールの場合、URL 検索にリンクされるパラメーター **変更しないでください**。 その他のパラメーターについては、Adobeにお問い合わせください。

## モバイルチャネルのパラメーター {#mobile-channel-parameters}

次の手順では、モバイルに配信する場合のデフォルト設定（SMS および WAP プッシュ）を定義できます。

>[!NOTE]
>
>モバイルチャネルはオプションです。このステージは、購入された場合にのみ表示されます。 使用許諾契約書を確認してください。

![](assets/s_ncs_install_deployment_wiz_12.png)

### SMS 配信用のデフォルトアカウント {#default-account-for-sms-delivery}

次の情報を入力します。

* **[!UICONTROL ラベル]**：この SMS/Wap プッシュアカウントの名前を入力します。 例えば、ルーターの名前を使用したい場合があります。
* **[!UICONTROL サーバー]**、**[!UICONTROL ポート]**、**[!UICONTROL アカウント]**、**[!UICONTROL パスワード]**、**[!UICONTROL コネクタ]**、**[!UICONTROL 送信エンドポイント]**、**[!UICONTROL 受信エンドポイント]**、**[!UICONTROL 通知エンドポイント]** の各フィールドについては、サービスプロバイダーに問い合わせて、必要な設定を入手してください。

### 送信された SMS のパラメーター {#parameters-of-sms-sent}

**優先度** ドロップダウンリストで：送信するメッセージに適用するには、「標準」、「高」、または「緊急」を選択します。

### 詳細設定パラメーター {#advanced-parameters}

「**詳細設定パラメーター…**」リンクを使用すると、再試行および強制隔離オプションにアクセスできます。

![](assets/s_ncs_install_deployment_wiz_13.png)

再試行に関する情報は、「**再試行の期間** および **再試行の数** フィールドで確認できます。モバイルが到達不能な場合、デフォルトでは、プログラムは少なくとも 15 分間隔で 5 回やり直します（最大配信期間）。 これらの値は、ニーズに合わせて調整できます。

強制隔離の設定オプションは次のとおりです。

* **[!UICONTROL 2 つの重要なエラーの間の時間]**：デフォルト値（デフォルトでは「1d」：日）を入力して、エラーのエラーカウンターを増分するまでのアプリケーションの待機時間を定義します。
* **[!UICONTROL 強制隔離前のエラーの最大数]**：この値に達すると、携帯電話番号が強制隔離されます（デフォルトでは「5」：この番号は 6 回目のエラーで強制隔離されます）。 つまり、連絡先は今後の配信から自動的に除外されます。

## 地域設定 {#regional-settings}

この段階では、データポリシー設定を含めることができます。

![](assets/s_ncs_install_deployment_wiz_14.png)

* **[!UICONTROL すべての電話番号を国際電話番号と見なす]**：このオプションを選択すると、アプリケーションは電話番号に国際書式を適用します（書式を適用する前に桁数がチェックされないので、国のプレフィックスは必須です）。 このオプションを選択しない場合、国際電話番号の前に「+」または「00」を付ける必要があります。
* **[!UICONTROL すべての電話番号を国際フォーマットを使用して保存]**：このオプションは、インポートまたは編集された **国内** の電話番号にのみ関係します。 国内書式（425 555 0150 など）と国際書式（+1 425 555 0150 など）のどちらを使用するかを定義します

## インターネットからのアクセス {#access-from-the-internet}

>[!IMPORTANT]
>
>プライバシー保護のために、すべての外部リソースに対して HTTPS を使用することをお勧めします。

この手順では、インターネットに公開されるAdobe Campaign ページのアクセス URL を定義できます。

また、Web フォームにリンクする公開オプションを指定する必要があります。

![](assets/s_ncs_install_deployment_wiz_15.png)

### Web に公開されているサーバー {#servers-exposed-on-the-web}

このページを使用して、次のサーバー URL を入力します。

1. インターネットに公開されているアプリケーションサーバー（購読/購読解除フォーム、エクストラネットなど）にアクセスします。
1. Web に公開されていないリソース（フォーム、イントラネット、確認ページ）のアプリケーションサーバーにアクセスします。
1. 配信のミラーページにアクセスする。

   ミラーページは、メールのコンテンツを表示する動的ページです。 受信者に送信されるメッセージに挿入されたリンクを介してアクセスされ、パーソナライズされた要素を含めることができます。 ミラーページを使用すると、配信フォーマット（テキストまたはHTML）に関係なく、受信者はメールソフトウェアではなくインターネットブラウザーでメッセージを読むことができます。 ただし、ミラーページは、必要なHTML コンテンツが定義されている場合に、特定の配信に対してのみ生成されます。

Adobe Campaignでは、これら 3 つの URL を区別して、複数のプラットフォームに負荷を分散させることができます。


>[!NOTE]
>
>* これらの設定は、Campaign プラットフォームオプションに保存されます。 [詳細情報](../../installation/using/configuring-campaign-options.md)。
>* マルチブランディング設定の場合は、ミラーページの URL を適応させ、メールルーティング外部アカウントのこの設定を上書きできます。 [詳細情報](../../installation/using/configuring-campaign-options.md)。


## パブリックリソースの管理 {#managing-public-resources}

>[!IMPORTANT]
>
>プライバシー保護のために、すべての外部リソースに対して HTTPS を使用することをお勧めします。

キャンペーンにリンクされたメールやパブリックリソースで使用される画像を外部から確認できるようにするには、外部からアクセス可能なサーバーに画像が配置されている必要があります。 その後、外部の受信者やオペレーターがコンテンツフラグメントを使用できるようになります。

![](assets/s_ncs_install_deployment_wiz_img_uploading.png)

この手順では、次を入力する必要があります。

1. 新しいパブリックリソース URL。 詳しくは、[&#x200B; パブリックリソース URL](#public-resources-url) の節を参照してください。
1. 配信の画像検出モード。 詳しくは、「配信画像の検出 [&#x200B; の節を参照し &#x200B;](#delivery-image-detection) ください。
1. 公開オプション。 詳しくは、[&#x200B; 公開モード &#x200B;](#publication-modes) の節を参照してください。

公開リソースには、Adobe Campaign ツリーの **管理/リソース/オンライン/公開リソース** ノードからアクセスできます。 ライブラリに収集され、メールに含めることができますが、キャンペーンやタスク、コンテンツ管理でも使用できます。

![](assets/install_pub_resources_view.png)

### パブリックリソース URL {#public-resources-url}

最初のフィールドでは、アップロード後にリソースに使用される URL の開始を指定できます。 アップロードされたリソースには、この新しい URL からアクセスできます。

配信では、パブリックリソースライブラリに保存されている画像や、サーバーに保存されているその他のローカル画像または画像を使用できます。

* メール画像の場合、**https://** server **/res/img** の URL。

  この値は、配信ごとに上書きできます。

* パブリックリソースの場合、URL **https://** server **/res/** instance **&#x200B;**&#x200B;ここで、**instance**&#x200B;はトラッキングインスタンスの名前です。

### 配信画像の検出 {#delivery-image-detection}

配信では、パブリックリソースライブラリに保存されている画像や、サーバーに保存されているその他のローカル画像または画像を使用できます。

「**URL マスク**」フィールドでは、画像を自動的にアップロードする際にスキップする URL マスクのリストを指定できます。 例えば、外部からアクセス可能なサイト、特にインターネットサイトに保存された画像を使用する場合、このフィールドにサイトの URL を入力できます。

![](assets/s_ncs_install_deployment_wiz_img_mask.png)

複数の URL マスクを指定する場合は、コンマを使用して各 URL マスクを区切ります。

* メールでの画像の使用と管理については、[Campaign v8 ドキュメント &#x200B;](https://experienceleague.adobe.com/docs/campaign/campaign-v8/send/emails/defining-the-email-content.html?lang=ja#adding-images){target="_blank"} を参照してください。
* 配信アシスタントでは、これらの URL から呼び出される画像のステータスは「無視」になります。

### 公開モード {#publication-modes}

アシスタントの下部のセクションでは、公開リソースと画像の公開オプションを選択できます。

次の公開モードを使用できます。

* トラッキングサーバー

  リソースは、別のトラッキングサーバーに自動的にコピーされます。 これらは、手順 [&#x200B; トラッキング設定 &#x200B;](#tracking-configuration) で設定します。

* その他のAdobe Campaign サーバー

  リソースのコピー先となる他のAdobe Campaign サーバーを 1 つ以上使用できます。

  サーバーサイドで専用のAdobe Campaign サーバーを使用するには、次のコマンドで新しいインスタンスを作成する必要があります。

  ```
  nlserver config -addtrackinginstance:<trackingA>/<trackingA*>
  ```

  次に、パスワードを入力します。

  専用サーバーのパラメーターは、「**[!UICONTROL メディア URL]**」、「**[!UICONTROL パスワード]**」および「**[!UICONTROL インスタンス名]**」フィールドに入力します。

  ![](assets/s_ncs_install_images_upload_b.png)

* 手動公開スクリプト（パブリックリソース用のみ）

  ![](assets/s_ncs_install_images_upload_c.png)

  スクリプトを使用して画像を公開できます。

   * このスクリプトを作成する必要があります。スクリプトの内容は、設定によって異なります。
   * スクリプトは次のコマンドで呼び出されます。

     ```
     [INSTALL]/copyToFrontal.vbs "$(XTK_INSTALL_DIR)\var\<instance>\upload\" "img1,img2,img3"
     ```

     ここで、`[INSTALL]` はAdobe Campaign インストールフォルダーへのアクセスパスです。

   * UNIX では、スクリプトが実行可能であることを確認します。

画像の場合、「NmsDelivery_ImageSubDirectory **オプションで指定された「images** フォルダーから 1 つ以上のフロントサーバーに画像をコピーする必要があります。 これらのサーバーは、新しく設定された URL 経由でアクセスできるように画像を保存します。

手動公開スクリプトを使用せずにAdobe Campaign サーバーで公開する場合、デフォルトでは、配信の画像は `$(XTK_INSTALL_DIR)/var/res/img/ directory` に保存されます。 対応する URL は次のとおりです。**`https://server/res/img`**。

`XTK_INSTALL_DIR)/var/res/$(INSTANCE_NAME)`.対応する URL は次のとおりです。**`https://server/res/instance`** ここで、instance はトラッキングインスタンスの名前です。

>[!NOTE]
>
>パブリックリソースストレージディレクトリは変更できます。 詳しくは、[&#x200B; パブリックリソースの管理 &#x200B;](#managing-public-resources) を参照してください。

### パブリックリソースの同期 {#synchronizing-public-resources}

この機能を使用すると、複数のスペアサーバーで **パブリックリソースを同期** できます。

トラッキングサーバーにパブリックリソースがない場合、またはリソースが 404 エラーを返す場合、トラッキングサーバーは予備サーバーの 1 つでリソースを見つけようとします。

予備サーバーの宣言と設定は、Marketing サーバーの **serverConf.xml** ファイルで行う必要があります。 **serverConf.xml** で使用可能なすべてのパラメーターは、この [&#x200B; セクション &#x200B;](../../installation/using/the-server-configuration-file.md) に一覧表示されます。

**申告**

```
<redirection>
<spareServer enabledIf="" id="" url=""/>
</redirection>
```

**設定**

同期する必要がある各パブリックリソースについて、`<url>` の部分の `<relay>` 要素にステータス属性を追加する必要があります。

「ステータス」属性は、次の 3 つの値のいずれかになります。

* スペア：パブリックリソースが同期されています

* 通常：既存の動作（同期なし）

* ブラックリスト：この URL は、404 エラーを返した場合にブロックリストに追加されます。 ブロックリストに含まれる URL のデュレーション（秒単位）は、デフォルト値が 60 秒の **timeout** 属性によって定義されます。

標準で用意されている同期の設定を次に示します。

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

デプロイメントウィザードの最後の段階では、古いデータの自動パージを設定できます。 値は日数で表されます。

![](assets/s_ncs_install_deployment_wiz_16.png)

データベースクリーンアップワークフローを使用すると、データが自動的に削除されます。 このワークフローの設定および操作方法と、削除された項目の詳細については、この [&#x200B; ドキュメント &#x200B;](../../production/using/database-cleanup-workflow.md) を参照してください。
