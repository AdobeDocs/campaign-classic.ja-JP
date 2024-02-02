---
product: campaign
title: ミッドソーシングインフラストラクチャでの Campaign SMS チャネルの設定
description: ミッドソーシングインフラストラクチャで Campaign で SMS チャネルを設定する方法を説明します
badge-v7: label="v7" type="Informative" tooltip="Campaign Classic v7 に適用されます"
badge-v8: label="v8" type="Positive" tooltip="Campaign v8 にも適用されます"
feature: SMS
role: User, Developer, Admin
source-git-commit: 4165f5988dfeee2f3b4d872c445ace11c9aa4fe1
workflow-type: tm+mt
source-wordcount: '1089'
ht-degree: 47%

---

# ミッドソーシングインフラストラクチャでの SMS チャネルの設定 {#setting-up-sms-channel}

ミッドサーバーを持つ携帯電話に送信するには、次が必要です。

1. マーケティングサーバーで作成された SMS 外部アカウントに使用するミッドサーバーで作成された SMS オペレーター。

1. チャネルと配信モードを指定する、マーケティングサーバー上の外部アカウント。

1. コネクタとメッセージタイプの詳細を示す、ミッドサーバー上の外部アカウント。

1. 送信プロセスを合理化するために、外部アカウントを参照する配信テンプレート。

>[!NOTE]
>
> SMS 配信の場合、タイポロジでは、**1 つ**&#x200B;の専用アプリケーションサーバーコンテナで作成された特定の SMS アフィニティを使用する必要があります。[詳細情報](../../installation/using/configure-delivery-settings.md#managing-outbound-smtp-traffic-with-affinities)

## ミッドサーバーでの SMS オペレーターの作成 {#create-sms-operator}

設定プロセスを開始するには、特に外部アカウント用の SMS オペレーターをミッドサーバー上に作成する必要があります。

>[!IMPORTANT]
>
>各 SMS コネクタには、一意の SMS 演算子が必要です。

1. Adobe Analytics の **[!UICONTROL 管理]** > **[!UICONTROL アクセス管理]** > **[!UICONTROL オペレーターノード]** ツリーのノードで、 **[!UICONTROL 新規]** アイコン。

   ![](assets/sms_operator_mid_3.png)

1. ユーザーの **[!UICONTROL 識別パラメーター]**（ログイン、パスワード、名前など）。 オペレーターがAdobe Campaignに安全にログインするには、ログインとパスワードが必要です。

   なお、 **[!UICONTROL 名前（ログイン）]** は、後でミッドサーバーで SMPP 外部アカウントに名前を付けるために使用します。

   ![](assets/sms_operator_mid_1.png)

1. オペレーターに付与する権限を、「オペレーターアクセス権」セクションで選択します。

   オペレーターに権限を割り当てるには、 **[!UICONTROL 追加]** ボタンをクリックします。 次に、 **[!UICONTROL オペレーターグループ]** または **[!UICONTROL ネームド権限]** を「使用可能なグループ」リストから選択します。

   ![](assets/sms_operator_mid_2.png)

1. クリック **[!UICONTROL 保存]** をクリックして、オペレーターの作成を完了します。 これで、プロファイルが既存のオペレーターのリストに含まれます。

## マーケティングサーバーでの SMS 外部アカウントの作成 {#create-accound-mkt}

ミッドサーバー対応の携帯電話に SMS を送信するには、まずマーケティングサーバーで SMS 外部アカウントを作成する必要があります。

1. ツリーの&#x200B;**[!UICONTROL プラットフォーム]**／**[!UICONTROL 外部アカウント]**&#x200B;ノードで、**[!UICONTROL 新規]**&#x200B;アイコンをクリックします。

   ![](assets/mid_external_account_2.png)

1. 次を入力： **[!UICONTROL ラベル]** および **[!UICONTROL 内部名]**. 内部名は、後でミッドサーバーで SMPP 外部アカウントに名前を付けるために使用されます。

1. アカウントタイプを次のように定義します。 **[!UICONTROL Routing]**、チャネルを **[!UICONTROL モバイル (SMS)]**、配信モードは **[!UICONTROL ミッドソーシング]**.

   ![](assets/mid_external_account_1.png)

1. Adobe Analytics の **[!UICONTROL ミッドソーシング]** 「 」タブで、ミッドソーシングサーバー接続のパラメーターを指定します。

   次の詳細を入力： [以前に作成した SMS コネクタ](#create-sms-operator) （内） **[!UICONTROL アカウント]** および **[!UICONTROL パスワード]** フィールド。

   ![](assets/mid_external_account_7.png)

1. 「 」をクリックして設定を確定します **[!UICONTROL 接続をテストする]**.

1. 「**[!UICONTROL 保存]**」をクリックします。

## ミッドサーバーでの SMPP 外部アカウントの作成 {#creating-smpp-mid}

>[!IMPORTANT]
>
>複数の外部 SMS アカウントに同じアカウントとパスワードを使用すると、アカウント間で競合や重複が生じる可能性があります。 [SMS のトラブルシューティングページ](troubleshooting-sms.md#external-account-conflict)を参照してください。

マーケティングサーバーで SMS 外部アカウントを正常に設定したら、次の手順は、ミッドサーバーに SMPP 外部アカウントを確立することです。

SMS プロトコルと設定の詳細については、こちらの [ページ](sms-protocol.md)を参照してください。

これをおこなうには、以下の手順に従います。

1. ツリーの&#x200B;**[!UICONTROL プラットフォーム]**／**[!UICONTROL 外部アカウント]**&#x200B;ノードで、**[!UICONTROL 新規]**&#x200B;アイコンをクリックします。

1. 次を入力： **[!UICONTROL ラベル]** および **[!UICONTROL 内部名]**.

   >[!WARNING]
   >
   >割り当て時 **[!UICONTROL 内部名]**で、必ず指定した命名規則に従ってください。
   > </br>`SMS Operator Name_Internal Name of the Marketing SMS external account`

   ![](assets/mid_external_account_6.png)

1. アカウントタイプを「**ルーティング**」、チャネルを「**モバイル (SMS)**」、配信モードを「**一括配信**」にそれぞれ設定します。

   ![](assets/mid_external_account_3.png)

1. 「**[!UICONTROL 有効]**」ボックスをオンにします。

1. 「**[!UICONTROL モバイル]**」タブで、**[!UICONTROL コネクタ]**&#x200B;ドロップダウンリストから「**[!UICONTROL 拡張された汎用 SMPP]**」を選択します。

   ![](assets/mid_external_account_4.png)

1. 「**[!UICONTROL ログファイルの詳細 SMPP トレースを有効にする]**」オプションを使用すると、ログファイル内のすべての SMPP トラフィックをダンプできます。このオプションは、コネクタのトラブルシューティングや、プロバイダーが確認できるトラフィックとの比較をおこなう場合にのみ有効にする必要があります。

1. 「**[!UICONTROL 接続設定]**」タブで各種の外部アカウントフィールドを入力する方法については、SMS サービスプロバイダーにお問い合わせください。

   また、「**[!UICONTROL SMSC 実装名]**」フィールドに入力する値については、選択したプロバイダーにお問い合わせください。

   MTA の子ごとのプロバイダーへの接続数を指定できます。デフォルトでは 1 に設定されています。

1. デフォルトでは、SMS の文字数は GSM 標準に準じています。

   GSM エンコードを使用する SMS メッセージは 160 文字以内に制限されています。複数の部分に分けて送信されるメッセージの場合は、SMS 1 件につき 153 文字以内です。

   >[!NOTE]
   >
   >2 文字としてカウントされる文字もあります（中括弧、角括弧、ユーロ記号など）。
   >
   >使用可能な GSM 文字のリストについては、 [この節](sms-set-up.md#about-character-transliteration).

   文字の表記変換を許可するには、対応するボックスをオンにします。

   ![](assets/mid_external_account_5.png)

1. 「**[!UICONTROL スループットと遅延]**」タブでは、送信メッセージの最大スループット（「MT」：モバイル終了）を 1 秒あたりの MT として指定できます。該当するフィールドに「0」と入力した場合、スループットは無制限となります。

   期間を示すどのフィールドでも、値は秒単位で入力する必要があります。

1. 「**[!UICONTROL エンコードのマッピング]**」タブでは、エンコードを定義できます。

   詳しくは、[この節](sms-set-up.md#about-text-encodings)を参照してください。

1. デフォルトでは、「**[!UICONTROL SMSC 特異性]**」タブの「**[!UICONTROL 完全な電話番号を送信]**」オプションは無効になっています。SMPP プロトコルに準拠し、数字のみを SMS プロバイダー（SMSC）のサーバーに送信する場合は、このオプションを有効にしないでください。

   ただし、特定のプロバイダーで「+」がプレフィックスとして必要な場合は、プロバイダーにお問い合わせください。必要に応じて、このオプションを有効にするようプロバイダーから指示があります。

   「**[!UICONTROL SMPP 経由での TLS を有効化]**」チェックボックスを使用すると、SMPP トラフィックを暗号化することができます。詳しくは、この [ページ](sms-protocol.md)を参照してください。

1. **[!UICONTROL 拡張された汎用 SMPP]** コネクタを設定している場合は、自動応答を設定できます。

   詳しくは、[この節](sms-set-up.md#automatic-reply)を参照してください。

## 配信テンプレートの変更 {#changing-the-delivery-template}

Adobe Campaignは、 **[!UICONTROL リソース/テンプレート/配信テンプレート]** ノード。 詳しくは、[テンプレートについて](about-templates.md)の節を参照してください。

SMS チャネルを通じてメッセージを送信するには、チャネルコネクタへの参照を含むテンプレートを作成する必要があります。

ネイティブ配信テンプレートを保持するには、テンプレートを複製してから設定することをお勧めします。

次の例では、前に作成した SMPP アカウントを使用してメッセージを配信しやすくするテンプレートを生成します。 手順は次のとおりです。

1. Adobe Analytics の **[!UICONTROL リソース]** > **[!UICONTROL テンプレート]** > **[!UICONTROL 配信テンプレート]** ツリーのノードで、 **[!UICONTROL モバイルに送信]** テンプレートを選択します。 **[!UICONTROL 複製]**.

   ![](assets/delivery_template_mid_1.png)

1. テンプレートのラベルを変更します（例：**モバイルに送信済み（SMPP）**）。

   ![](assets/delivery_template_mid_2.png)

1. 「**[!UICONTROL プロパティ]**」をクリックします。

1. Adobe Analytics の **[!UICONTROL 一般]** 」タブで、セクションで作成した外部アカウントに対応するルーティングモードを選択します。 [マーケティングサーバーでの SMS 外部アカウントの作成](#create-accound-mkt).

   ![](assets/delivery_template_mid_3.png)

1. 「**[!UICONTROL 保存]**」をクリックし、テンプレートを作成します。

   ![](assets/delivery_template_mid_4.png)

これで、SMS 経由で配信できる外部アカウントと配信テンプレートを用意できました。

## 関連トピック {#related-topics}

* [SMS 文字の表記変換](sms-set-up.md#about-character-transliteration)
* [テキストエンコーディング](sms-set-up.md#about-text-encodings)
* [自動返信](sms-set-up.md#automatic-reply)

