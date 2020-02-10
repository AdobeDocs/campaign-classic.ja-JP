---
title: SMS チャネル
seo-title: SMS チャネル
description: SMS チャネル
seo-description: null
page-status-flag: never-activated
uuid: be6a2abc-ba5c-4363-bf38-cc309ee3a8d9
contentOwner: sauviat
products: SG_CAMPAIGN/CLASSIC
audience: delivery
content-type: reference
topic-tags: sending-messages-on-mobiles
discoiquuid: 8b101c0b-3611-4f15-813b-7c0bf54fc48a
index: y
internal: n
snippet: y
translation-type: tm+mt
source-git-commit: 6e587747be546860c0a485b44aee79d396f25cec

---


# SMS チャネル{#sms-channel}

Adobe Campaign には、パーソナライズした SMS メッセージを大量配信する機能があります。受信者のプロファイルには、携帯電話番号が少なくとも 1 つ登録されている必要があります。

>[!NOTE]
>
>また、Adobe Campaign では、**Adobe Campaign モバイルアプリチャネル（NMAC）**&#x200B;オプションを使用してモバイル端末に通知を送信することもできます。
> 
>詳しくは、モバイルアプリチャネルにつ [いての節を参照してください](../../delivery/using/about-mobile-app-channel.md) 。

以下のセクションでは、SMSチャネルに固有の情報を提供します。 For global information on how to create a delivery, refer to [this section](../../delivery/using/steps-about-delivery-creation-steps.md).

## SMS チャネルの設定 {#setting-up-sms-channel}

携帯電話に送信するには、次が必要です。

1. コネクタとメッセージのタイプを指定する外部アカウント。

   使用可能なコネクタは次のとおりです。NetSize、汎用SMPP（バイナリ・モードをサポートするSMPPバージョン3.4）、Sybase365(SAP SMS 365)、CLX通信、Tele2、O2、拡張汎用SMPP。

1. 使用する外部アカウントへの参照を含んだ配信テンプレート。

### 外部アカウントの有効化 {#activating-an-external-account}

The list of external accounts can be found in the **[!UICONTROL Platform]** > **[!UICONTROL External accounts]** node of the Adobe Campaign explorer tree.

* 例えば、というデフォルトのアカウントに移動しま **[!UICONTROL NetSize mobile delivery]**&#x200B;す。
* タブで、ボッ **[!UICONTROL General]** クスをオンにし **[!UICONTROL Enabled]** ます。

   ![](assets/s_user_external_account_01.png)

* Check that the **[!UICONTROL Mobile]** option is selected for the **[!UICONTROL Channel]** field.
* タブで、ド **[!UICONTROL Mobile]** ロップダウンリストからコネクタを選択します。NetSize、汎用SMPP、Sybase365(SAP SMS 365)、CLX通信、Tele2、O2、または拡張汎用SMPP。 拡張された汎用 SMPP コネクタについて詳しくは、[SMPP 外部アカウントの作成](#creating-an-smpp-external-account)の節を参照してください。

   ![](assets/s_user_external_account_connect_01.png)

* コネクタを、サプライヤーから入手した情報に従って設定します。下の例では、通信事業者は NetSize です。

   ![](assets/s_user_external_account_param.png)

* タブで、デフ **[!UICONTROL Connector]** ォルトで選択されてい **[!UICONTROL Call Web Service]** るアクティブ化モードのままにします。

   ![](assets/s_user_external_account_param_02.png)

* If the **[!UICONTROL Connector]** tab is displayed, specify the access URL for the connector. プロバイダーが NetSize の場合、アドレスの末尾は **netsize.jsp** になります。それ以外のコネクタの場合、URL アドレスの末尾は **smpp34.jsp** です。

### SMPP 外部アカウントの作成 {#creating-an-smpp-external-account}

SMPP プロトコルを使用する場合、新しい外部アカウントを作成することもできます。

SMS のプロトコルと設定について詳しくは、この[技術メモ](https://helpx.adobe.com/campaign/kb/sms-connector-protocol-and-settings.html)を参照してください。

これをおこなうには、以下の手順に従います。

1. ツリーの> **[!UICONTROL Platform]** ノー **[!UICONTROL External accounts]** ドで、アイコンをクリックし **[!UICONTROL New]** ます。
1. アカウントタイプを「**ルーティング**」、チャネルを「**モバイル (SMS)**」、配信モードを「**一括配信**」にそれぞれ設定します。

   ![](assets/extended_smpp_create_account.png)

1. チェックボックスをオ **[!UICONTROL Enabled]** ンにします。
1. タブで、 **[!UICONTROL Mobile]** ドロップダ **[!UICONTROL Extended generic SMPP]** ウンリ **[!UICONTROL Connector]** ストから選択します。

   ![](assets/extended_smpp_connector.png)

   このオプ **[!UICONTROL Enable verbose SMPP traces in the log file]** ションを使用すると、すべてのSMPPトラフィックをログファイルにダンプできます。 コネクタのトラブルシューティングやプロバイダー側が確認できるトラフィックとの比較をおこなうには、このオプションを有効にする必要があります。

1. Contact your SMS service provider who will explain to you how to complete the different external account fields from the **[!UICONTROL Connection settings]** tab.

   Then, contact your provider, depending on the one chosen, who will give you the value to enter into the **[!UICONTROL SMSC implementation name]** field.

   MTA の子ごとのプロバイダーへの接続数を指定できます。デフォルトでは 1 に設定されています。

1. デフォルトでは、SMS の文字数は GSM 標準に準じています。

   GSM エンコードを使用する SMS メッセージは 160 文字以内に制限されています。複数の部分に分けて送信されるメッセージの場合は、SMS 1 件につき 153 文字以内です。

   >[!NOTE]
   >
   >2 文字としてカウントされる文字もあります（中括弧、角括弧、ユーロ記号など）。
   >
   >使用可能な GSM 文字の一覧については、下記を参照してください。

   必要に応じて、文字の表記変換をチェックボックスで指定できます。

   ![](assets/extended_smpp_transliteration.png)

   詳しくは、[この節](#about-character-transliteration)を参照してください。

1. In the **[!UICONTROL Throughput and delays]** tab, you can specify the maximum throughput of outbound messages (&quot;MT&quot;, Mobile Terminated) in MT per second. 該当するフィールドに「0」と入力した場合、スループットは無制限となります。

   期間を示すどのフィールドでも、値は秒単位で入力する必要があります。

1. タブで、エ **[!UICONTROL Mapping of encodings]** ンコーディングを定義できます。

   詳しくは、[この節](#about-text-encodings)を参照してください。

1. このタブで **[!UICONTROL SMSC specificities]** は、このオプシ **[!UICONTROL Send full phone number]** ョンはデフォルトで無効になっています。 SMPP プロトコルに準拠し、数字のみを SMS プロバイダー（SMSC）のサーバーに送信する場合は、このオプションを有効にしないでください。

   ただし、特定のプロバイダーで「+」がプレフィックスとして必要な場合は、プロバイダーにお問い合わせください。必要に応じて、このオプションを有効にするようプロバイダーから指示があります。

   このチェ **[!UICONTROL Enable TLS over SMPP]** ックボックスを使用して、SMPPトラフィックを暗号化できます。 詳しくは、この[技術メモ](https://helpx.adobe.com/campaign/kb/sms-connector-protocol-and-settings.html)を参照してください。

1. If you are configuring an **[!UICONTROL Extended generic SMPP]** connector, you can set up automatic replies.

   詳しくは、[この節](#automatic-reply)を参照してください。

### 文字の表記変換について {#about-character-transliteration}

Character transliteration can be set up in a SMPP mobile delivery external account, under the **[!UICONTROL Mobile]** tab.

表記変換では、SMS の特定の文字が GSM 標準に準じていない場合に、別の文字に置き換えられます。

* If transliteration is **[!UICONTROL authorized]**, each character that is not taken into account is replaced by a GSM character when the message is sent. 例えば、「ë」は「e」に置き換えられます。そのため、メッセージは若干改変されますが、文字制限は同じです。
* When transliteration is **[!UICONTROL not authorized]**, each message that contains characters that are not taken into account is sent in binary format (Unicode): all of the characters are therefore sent as they are. ただし、Unicode を使用する SMS メッセージは 70 文字以内に制限されています。複数の部分に分けて送信されるメッセージの場合は、SMS 1 件につき 67 文字以内です。文字数が上限を超えると、メッセージは複数に分かれて送信されますが、追加料金が発生する場合があります。

>[!CAUTION]
>
>パーソナライゼーションフィールドを SMS メッセージのコンテンツに入れると、GSM エンコードに対応していない文字が含まれる場合があります。

デフォルトでは、文字の表記変換は無効です。SMS メッセージのすべての文字をそのまま送信する場合（例えば、固有名詞が改変されないようにする場合）、このオプションは無効にしておくことをお勧めします。

ただし、SMS メッセージに Unicode メッセージ用の文字が多数含まれる場合、このオプションを有効にしてメッセージ送信のコストを抑えることもできます。

下記の表では、GSM 標準に準じた文字を紹介します。メッセージ本文に、ここで紹介されていない文字が含まれている場合、メッセージ全体がバイナリフォーマット（Unicode）に変換され、文字数が 70 文字以内に制限されます。

**基本的な文字**

<table> 
 <tbody> 
  <tr> 
   <td> @ </td> 
   <td> <img height="21px" src="assets/delta.png" /> </td> 
   <td> SP </td> 
   <td> 0 </td> 
   <td> ¡ </td> 
   <td> P </td> 
   <td> ¿ </td> 
   <td> p </td> 
  </tr> 
  <tr> 
   <td> £ </td> 
   <td> _ </td> 
   <td> ! </td> 
   <td> 1 </td> 
   <td> A </td> 
   <td> Q </td> 
   <td> a </td> 
   <td> q </td> 
  </tr> 
  <tr> 
   <td> $ </td> 
   <td> <img height="21px" src="assets/phi.png" /> </td> 
   <td> " </td> 
   <td> 2 </td> 
   <td> B </td> 
   <td> R </td> 
   <td> b </td> 
   <td> r </td> 
  </tr> 
  <tr> 
   <td> ¥ </td> 
   <td> <img height="21px" src="assets/gamma.png" /> </td> 
   <td> # </td> 
   <td> 3 </td> 
   <td> C </td> 
   <td> S </td> 
   <td> c </td> 
   <td> s </td> 
  </tr> 
  <tr> 
   <td> è </td> 
   <td> <img height="21px" src="assets/delta.png" /> </td> 
   <td> ¤ </td> 
   <td> 4 </td> 
   <td> D </td> 
   <td> T </td> 
   <td> d </td> 
   <td> t </td> 
  </tr> 
  <tr> 
   <td> é </td> 
   <td> <img height="21px" src="assets/omega.png" /> </td> 
   <td> % </td> 
   <td> 2018 年 </td> 
   <td> E </td> 
   <td> U </td> 
   <td> e </td> 
   <td> u </td> 
  </tr> 
  <tr> 
   <td> ù </td> 
   <td> <img height="21px" src="assets/pi.png" /> </td> 
   <td> &amp; </td> 
   <td> 2018 年 </td> 
   <td> F </td> 
   <td> V </td> 
   <td> f </td> 
   <td> v </td> 
  </tr> 
  <tr> 
   <td> ì </td> 
   <td> <img height="21px" src="assets/psi.png" /> </td> 
   <td> ' </td> 
   <td> 7 </td> 
   <td> G </td> 
   <td> W </td> 
   <td> g </td> 
   <td> w </td> 
  </tr> 
  <tr> 
   <td> ò </td> 
   <td> <img height="21px" src="assets/sigma.png" /> </td> 
   <td> ( </td> 
   <td> 8 </td> 
   <td> H </td> 
   <td> X </td> 
   <td> h </td> 
   <td> x </td> 
  </tr> 
  <tr> 
   <td> Ç </td> 
   <td> <img height="21px" src="assets/theta.png" /> </td> 
   <td> ) </td> 
   <td> 9 </td> 
   <td> I </td> 
   <td> Y </td> 
   <td> i </td> 
   <td> y </td> 
  </tr> 
  <tr> 
   <td> LF </td> 
   <td> <img height="21px" src="assets/xi.png" /> </td> 
   <td> * </td> 
   <td> : </td> 
   <td> J </td> 
   <td> Z </td> 
   <td> j </td> 
   <td> z </td> 
  </tr> 
  <tr> 
   <td> Ø </td> 
   <td> ESC </td> 
   <td> + </td> 
   <td> ; </td> 
   <td> K </td> 
   <td> Ä </td> 
   <td> k </td> 
   <td> ä </td> 
  </tr> 
  <tr> 
   <td> ø </td> 
   <td> Æ </td> 
   <td> , </td> 
   <td> &lt; </td> 
   <td> L </td> 
   <td> Ö </td> 
   <td> l </td> 
   <td> ö </td> 
  </tr> 
  <tr> 
   <td> CR </td> 
   <td> æ </td> 
   <td> - </td> 
   <td> = </td> 
   <td> M </td> 
   <td> Ñ </td> 
   <td> m </td> 
   <td> ñ </td> 
  </tr> 
  <tr> 
   <td> Å </td> 
   <td> ß </td> 
   <td> . </td> 
   <td> &gt; </td> 
   <td> N </td> 
   <td> Ü </td> 
   <td> n </td> 
   <td> ü </td> 
  </tr> 
  <tr> 
   <td> å </td> 
   <td> É </td> 
   <td> / </td> 
   <td> ? </td> 
   <td> O </td> 
   <td> § </td> 
   <td> o </td> 
   <td> à </td> 
  </tr> 
 </tbody> 
</table>

SP:スペース

ESC:Escape

LF:ラインフィード

CR:キャリッジリターン

**高度な文字（2 回カウント）**

^ { } `[ ~ ]` | €

### テキストのエンコードについて {#about-text-encodings}

Adobe Campaign では、SMS メッセージの送信時に 1 つまたは複数のテキストエンコードを使用できます。エンコードごとに独自の文字セットがあり、SMS メッセージに入力できる文字数もそれぞれ異なります。

When configuring a new SMPP mobile delivery external account, you can define the **[!UICONTROL Mapping of encodings]** in the **[!UICONTROL Mobile]** tab: the **[!UICONTROL data_coding]** field allows Adobe Campaign to communicate which encoding is used to the SMSC.

>[!NOTE]
>
>**data_coding** の値と実際に使用されているエンコードの間のマッピングは標準化されています。しかし、一部の SMSC には独自のマッピングがあり、その場合、**Adobe Campaign** 管理者がこのマッピングを宣言する必要があります。詳しくは、プロバイダーにお問い合わせください。

必要に応じて、**data_codings** を宣言してエンコードを強制適用できます。この場合、表のエンコードの 1 つを指定します。

* エンコードのマッピングが定義されていない場合、コネクタは一般的な動作をおこないます。

   * **data_coding = 0** を設定して、GSM エンコードの使用を試行します。
   * GSM エンコードが失敗した場合は、**data_coding = 8** を設定して、**UCS2** エンコードの使用を試行します。

* 使用するエンコードと、リンクされた **[!UICONTROL data_coding]** フィールド値を指定した場合、Adobe Campaign はリストの最初のエンコードを使用します。最初のエンコードが使用できない場合、その次のエンコードを使用します。

>[!CAUTION]
>
>宣言の順序は重要です。**コスト**&#x200B;が少ない順にリストを設定し、SMS メッセージになるべく多くの文字を使用できるようにすることをお勧めします。
>
>使用するエンコードのみを宣言してください。SMSC から提供されているエンコードの中に、使用目的に該当しないものがあれば、それはリストで宣言しないでください。

### 自動返信 {#automatic-reply}

拡張された汎用 SMPP コネクタを設定している場合は、自動返信を設定できます。

When a subscriber replies to an SMS message which was sent to them via Adobe Campaign and their message contains a keyword such as &quot;STOP&quot;, you can configure messages which are automatically sent back to them in the **[!UICONTROL Automatic reply sent to the MO]** section.

>[!NOTE]
>
>キーワードは大文字と小文字が区別されません。

キーワードごとにショートコードを指定します。これは、通常は配信の送信に使用する数字で、送信者名を表します。その後、購読者に送信するメッセージを入力します。

You can also link an action to your automatic response: **[!UICONTROL Send to quarantine]** or **[!UICONTROL Remove from quarantine]**. 例えば、受信者が「STOP」というキーワードを送信した場合、その受信者には自動的に購読解除の確認が送信され、さらにその受信者が強制隔離に送信されます。

![](assets/extended_smpp_reply.png)

If you link the **[!UICONTROL Remove from quarantine]** action to an automatic response, the recipients sending the corresponding keyword are automatically removed from quarantine.

受信者は、//メニュー **[!UICONTROL Non deliverables and addresses]** で表に表示され **[!UICONTROL Administration]** る受信者 **[!UICONTROL Campaign Management]** で **[!UICONTROL Non deliverables Management]** す。

* To send the same reply no matter what the short code, leave the **[!UICONTROL Short code]** column empty.
* To send the same reply no matter what the keyword, leave the **[!UICONTROL Keyword]** column empty.
* To carry out an action without sending a response, leave the **[!UICONTROL Response]** column empty. これにより、例えば、「STOP」以外のメッセージを送信したユーザーを強制隔離から削除できます。

同じプロバイダーアカウントで拡張汎用SMPPコネクタを使用して複数の外部アカウントがある場合は、次の問題が発生する可能性があります。短いコードへの応答を送信する場合、外部アカウント接続で受け取る可能性があります。 その結果、送信される自動応答が期待されるメッセージになりませんでした。
これを回避するには、使用しているプロバイダーに応じて、次のいずれかのソリューションを適用します。
* 各外部アカウントに対して1つのプロバイダーアカウントを作成します。
* 「>」タブの **[!UICONTROL System type]** フィールドを使用 **[!UICONTROL Mobile]** して、各 **[!UICONTROL Connection settings]** 短いコードを区別します。 プロバイダーにアカウントごとに異なる値を尋ねます。

   ![](assets/extended_smpp_system-type.png)

拡張汎用SMPPコネクタを使用して外部アカウントを設定する手順については、「SMPP外部アカウ [ントの作成」の節を参照してくださ](../../delivery/using/sms-channel.md#creating-an-smpp-external-account) い。

### 配信テンプレートの変更 {#changing-the-delivery-template}

Adobe Campaign には、モバイルへの配信用テンプレートが用意されています。このテンプレートはノードで使用で **[!UICONTROL Resources > Templates > Delivery templates]** きます。 For more on this, refer to the [About templates](../../delivery/using/about-templates.md) section.

SMS チャネルでの配信の場合は、使用するチャネルコネクタへの参照を含んだテンプレートを作成する必要があります。

ネイティブ配信テンプレートを保持しておくために、テンプレートのコピーを作成してから設定することをお勧めします。

次の例では、既に有効化した NetSize アカウントを使用してメッセージを配信するテンプレートを作成します。手順は次のとおりです。

1. ノードに移動し **[!UICONTROL Delivery templates]** ます。
1. テンプレートを右クリ **[!UICONTROL Send to mobiles]** ックし、を選択しま **[!UICONTROL Duplicate]**&#x200B;す。

   ![](assets/s_user_mobile_template_change_01.png)

1. テンプレートのラベルを変更します。

   ![](assets/s_user_mobile_template_change_02.png)

1. クリック **[!UICONTROL Properties]**.
1. In the **[!UICONTROL General]** tab, select a routing mode that corresponds to an external account that you configured, for example **[!UICONTROL NetSize mobile delivery]**.

   ![](assets/s_user_mobile_template_change_03.png)

1. Click **[!UICONTROL Save]** to create the template.

   ![](assets/s_user_mobile_template_list.png)

これで、SMS 経由で配信できる外部アカウントと配信テンプレートを用意できました。

## SMS 配信の作成 {#creating-a-sms-delivery}

### 配信チャネルの選択 {#selecting-the-delivery-channel}

新しい SMS 配信を作成するには、次の手順に従います。

>[!NOTE]
>
>配信の作成に関するグローバルな概念については、[この節](../../delivery/using/steps-about-delivery-creation-steps.md)で説明しています。

1. 新しい配信を作成します（例えば、配信ダッシュボードから）。
1. 以前に作成した配信テン **[!UICONTROL Send to mobiles (NetSize)]** プレートを選択します。 For more on this, refer to the [Changing the delivery template](#changing-the-delivery-template) section.

   ![](assets/s_user_mobile_wizard.png)

1. ラベル、コードおよび説明を設定して配信を識別します。詳しくは、[この節](../../delivery/using/steps-create-and-identify-the-delivery.md#identifying-the-delivery)を参照してください。
1. Click **[!UICONTROL Continue]** to confirm this information and display the message configuration window.

## SMS コンテンツの定義 {#defining-the-sms-content}

SMS のコンテンツを作成するには、次の手順に従います。

1. Enter the content of the message in the **[!UICONTROL Text content]** section of the wizard. ツールバーのボタンで、コンテンツのインポート、保存、検索ができます。最後のボタンは、パーソナライゼーションフィールドを挿入するために使用します。

   ![](assets/s_ncs_user_wizard_sms01_138.png)

   The use of personalization fields is presented in the [About personalization](../../delivery/using/about-personalization.md) section.

1. Click **[!UICONTROL Preview]** at the bottom of the page to view the rendering of the message with its personalization. To launch the preview, select a recipient using the **[!UICONTROL Test personalization]** button in the toolbar. 定義済みターゲットの中から受信者を選択することも、別の受信者を指定することもできます。

   ![](assets/s_ncs_user_wizard_sms01_139.png)

   SMS メッセージを承認したり、コンテンツエディターの右側に表示される携帯電話画面で SMS のコンテンツを表示したりできます。画面のクリックや、マウスによるコンテンツのスクロールが可能です。

   ![](assets/s_ncs_user_wizard_sms01_140.png)

1. Click the **[!UICONTROL Data loaded]** link to view the information concerning the recipient.

   ![](assets/s_user_mobile_wizard_sms_02.png)

   >[!NOTE]
   >
   >SMS メッセージの文字数には制限があり、Latin-1（ISO-8859-1）コードページを使用する場合は 160 字以内です。メッセージが Unicode で作成されている場合、上限は 70 文字です。また、使用する文字によってメッセージの長さ制限が変化することがあります。For more information on message length, refer to the [About character transliteration](#about-character-transliteration) section.
   >
   >パーソナライゼーションフィールドまたは条件付きコンテンツが含まれる場合、メッセージのサイズは受信者によって異なります。メッセージの長さはパーソナライゼーションを適用した後の状態で評価する必要があります。
   >
   >分析を開始すると、メッセージの長さがチェックされ、制限を超える場合は警告が表示されます。

1. NetSize コネクタ、またはいずれかの SMPP コネクタを使用する場合は、配信の送信者名をパーソナライズできます。For more on this, refer to the [Advanced parameters](#advanced-parameters) section.

## ターゲット母集団の選択 {#selecting-the-target-population}

配信のターゲット母集団を選択する際の詳細なプロセスについては、[この節](../../delivery/using/steps-defining-the-target-population.md)を参照してください。

For more on the use of personalization fields, refer to [About personalization](../../delivery/using/about-personalization.md).

For more on the inclusion of a seed list, refer to [About seed addresses](../../delivery/using/about-seed-addresses.md).

## SMS メッセージの送信 {#sending-sms-messages}

To approve your message and send it to the recipients of the delivery being created, click **[!UICONTROL Send]**.

配信を検証および送信する際の詳細なプロセスについては、以下の節を参照してください。

* [配信の検証](../../delivery/using/steps-validating-the-delivery.md)
* [配信の送信](../../delivery/using/steps-sending-the-delivery.md)

### 詳細設定パラメーター {#advanced-parameters}

The **[!UICONTROL Properties]** button gives access to the advanced delivery parameter. The parameters specific to SMS deliveries are in the **[!UICONTROL SMS parameters]** section of the **[!UICONTROL Delivery]** tab.

次のオプションを使用できます。

* **送信者のアドレス**（NetSize コネクタ、SMPP コネクタのみ）：配信の送信者名をパーソナライズできます。使用できる文字は半角英数字のみ、長さは 11 字以内です。また、数字のみで構成される文字列は指定できません。条件を指定することにより、例えば、受信者の市外局番に基づいて名前を変更できます。

   ```
   <% if( String(recipient.mobilePhone).indexOf("+1") == 0){ %>NeoShopUS<%} else {%>NeoShopWorld<%}%>
   ```

   >[!CAUTION]
   >
   >送信者名の変更については規制が適用される場合があります。お住まいの国の法律を確認してください。また、通信事業者が送信者名の変更機能を提供しているかどうかについても確認する必要があります。

* **送信モード**：SMS によるメッセージ送信です。
* **優先順位**：メッセージに付与する重要度レベルです。**[!UICONTROL Normal]** デフォルトでは、優先度が選択されています。 Ask your service provider about the cost of SMS sent with **[!UICONTROL High]** priority.
* **通信のタイプ**：SMS 配信に割り当てるアプリケーションを選択します。The **[!UICONTROL Direct Marketing]** option is selected by default and is the most common one used.

**NetSize コネクタに特有のパラメーター**

![](assets/s_user_mobile_sms_adv_netsize.png)

* **単一のメッセージに複数の SMS を使用**：メッセージの長さが 160 字を超える場合に複数の SMS メッセージを使用して送信することを許可します。

**SMPP コネクタに特有のパラメーター**

![](assets/s_user_mobile_sms_adv_smpp.png)

* **メッセージごとの SMS の最大数**：1 件のメッセージ送信に使用できる SMS の数を指定します。値が 0 の場合、メッセージの配信に使用する SMS の数に制限はありません。また、例えば 1 や 2 の場合、この数の SMS に収まらない長さのメッセージは送信されません。

## SMS 配信の監視とトラッキング {#monitoring-and-tracking-sms-deliveries}

メッセージを送信した後は、配信を監視およびトラッキングできます。詳しくは、以下の節を参照してください。

* [配信の監視](../../delivery/using/monitoring-a-delivery.md)
* [配信エラーの理解](../../delivery/using/understanding-delivery-failures.md)
* [メッセージトラッキングについて](../../delivery/using/about-message-tracking.md)

## インバウンドメッセージの処理 {#processing-inbound-messages}

**nlserver sms** モジュールは、一定の時間間隔で SMS ルーターにクエリを発行します。これにより、Adobe Campaign で配信の進行状況をトラッキングし、ステータスレポートや受信者の購読解除リクエストに対処できます。

* **ステータスレポート**：配信ログを参照してメッセージのステータスをチェックできます。

   >[!NOTE]
   >
   >送信されるそれぞれの SMS のプライマリキーは、外部アカウントにリンクされます。これは次のことを意味します。
   >
   > * 削除された SMS アカウントのステータスレポートは、正常に処理されません。
   > * SMSアカウントを単一の外部アカウントにリンクすることで、ステータスレポートが正しいアカウントに関連付けられていることを確認できます


* **購読解除**：SMS 配信の停止を希望する受信者は、STOP という単語を含んだメッセージを返信することで受信を停止できます。プロバイダーとの契約上認められている場合は、**インバウンド SMS** ワークフローアクティビティを使用してメッセージを取得し、クエリを作成して、関係する複数の受信者のために「**今後のこの受信者への連絡は不要**」オプションを有効化できます。

   [ワークフロー](../../workflow/using/executing-a-workflow.md#architecture)ガイドを参照してください。

## InSMS スキーマ {#insms-schema}

InSMS スキーマには、受信 SMS に関する情報が含まれます。それらの情報に関するフィールドの説明は、desc 属性を使用して取得できます。

* **message**：受信した SMS の内容
* **origin**：メッセージ送信元の携帯電話番号
* **providerId**：SMSC（メッセージセンター）から返されたメッセージの識別子
* **created**：受信メッセージが Adobe Campaign に挿入された日付
* **extAccount**:Adobe Campaign外部アカウント。

   >[!CAUTION]
   >
   >次のフィールドは NetSize に特有のものです。
   >
   >使用する通信事業者が NetSize ではない場合、これらのフィールドの値は空とみなされます。

* **alias**：受信メッセージのエイリアス
* **separator**：エイリアスとメッセージ本文との区切り記号
* **messageDate**：通信事業者がメッセージに付けた日付
* **receivalDate**：メッセージが通信事業者から SMSC（メッセージセンター）に届いた日付
* **deliveryDate**：メッセージが SMSC（メッセージセンター）から送信された日付
* **largeAccount**：受信 SMS にリンクされた顧客アカウントコード
* **countryCode**：通信事業者の国コード
* **operatorCode**：通信事業者のネットワークコード
* **linkedSmsId**:送信SMSにリンクされているAdobe Campaign識別子(broadlogId)。このSMSは応答です。

## Managing automatic replies (American regulation) {#managing-automatic-replies--american-regulation-}

Adobe Campaign 経由で送信した SMS メッセージに対し、購読者から STOP、HELP、YES のようなキーワードを含む応答が返ってきた場合、米国市場では、自動応答メッセージを返すように設定しておく必要があります。

例えば、STOP というキーワードを含むメッセージが受信者から届いた場合は、その受信者に対して、購読解除を受け付けたことを示す確認メッセージを送信します。

このタイプのメッセージで使用する送信者名は、配信の送信時に通常使用される短いコードです。

>[!CAUTION]
>
>次の詳細手順は、SMPP コネクタ（拡張された SMPP コネクタは除く）の場合のみ有効です。詳しくは、「SMPP外部アカウントの作 [成」の節を参照してください](#creating-an-smpp-external-account) 。
>
>これは、米国の通信事業者が国内のマーケティングキャンペーンで実行する認証プロセスの一環です。このようなキーワードを含む購読者の SMS メッセージを受信した場合は、ただちに購読者に返信する必要があります。

1. 次のような XML ファイルを作成します。

   ```
   <autoreply>
     <shortcode name="12345">
       <reply keyword="STOP" text="You will not receive SMS anymore" />
       <reply keyword="HELP" text="Powered by Adobe Campaign" />
     </shortcode>
     <shortcode name="43115">
       <reply keyword="STOP" text="Vous ne recevrez plus de SMS" />
       <reply keyword="HELP" text="Service rendu par Adobe Campaign" />
     </shortcode>
     <shortcode name="*">
       <reply keyword="ADOBE" text="This text is replied when you send ADOBE to any short code" />
     </shortcode>
   </autoreply>
   ```

1. For the **name** attribute of the **`<shortcode>`** tag, specify the short code that will be displayed in the place of the message sender name.

   In each **`<reply>`** tag, enter the **keyword** attribute with a keyword and the **text** attribute with the message that you would like to send for this keyword.

   >[!NOTE]
   >
   >各キーワードは、大文字の英字で記述する必要があります。

   複数のキーワードに対して同じメッセージを送信する場合は、該当する行をコピーします。

   次に例を示します。

   ```
   <reply keyword="STOP" text="You will not receive SMS anymore" />
   <reply keyword="QUIT" text="You will not receive SMS anymore" />
   ```

1. 完成したら、ファイルを **smsAutoReply.xml** という名前で保存します。

   Linux ではファイル名の大文字と小文字が区別される点に注意してください。

1. このファイルを、Adobe Campaign の **conf** ディレクトリ内の、Web サーバーと同じ場所にコピーします。

>[!CAUTION]
>
>こうした自動メッセージは、履歴には記録されず、[配信ダッシュボード](../../delivery/using/monitoring-a-delivery.md#delivery-dashboard)にも表示されません。
>
>これらのメッセージは、[商業的な頻度ルール](../../campaign/using/pressure-rules.md)の対象とはみなされません。
