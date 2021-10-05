---
product: campaign
title: 技術的な E メール設定
description: E メールの配信時にインスタンスの出力を制御する Campaign の設定方法を説明します。
audience: installation
content-type: reference
topic-tags: additional-configurations
exl-id: 515adad2-6129-450a-bb9e-fc80127835af
source-git-commit: 4661a65c83f3b9b7da9ea902f387155c5933e59f
workflow-type: tm+mt
source-wordcount: '3090'
ht-degree: 19%

---

# 技術的なメール設定{#email-deliverability}

![](../../assets/v7-only.svg)

## 概要 {#overview}

次の節では、E メールの配信時にAdobe Campaignインスタンスの出力を制御するために必要な設定の概要を説明します。

>[!NOTE]
>
>一部の設定は、Adobeが実行できるのは、Adobeがホストするデプロイメントの場合のみです。例えば、サーバーとインスタンスの設定ファイルにアクセスする場合などです。 様々なデプロイメントの詳細については、[ モデルのホスティング ](../../installation/using/hosting-models.md) の節または [ このページ ](../../installation/using/capability-matrix.md) を参照してください。

Adobe Campaignでの配信品質に関する概念とベストプラクティスについて詳しくは、この [ 節 ](../../delivery/using/about-deliverability.md) を参照してください。

Adobeプラットフォームによる E メールの効率的な送受信に関するすべての技術的な推奨事項など、配信品質の詳細については、「[Adobe配信品質のベストプラクティスガイド ](https://experienceleague.adobe.com/docs/deliverability-learn/deliverability-best-practice-guide/introduction.html?lang=ja)」を参照してください。

## 動作原理 {#operating-principle}

1 つ以上のAdobe Campaignインスタンスの出力を制御して、ドメインに応じて送信される E メールの数を制限できます。 例えば、**yahoo.com** のアドレスに対して 1 時間あたり 20,000 件の出力を制限し、その他すべてのドメインに対して 1 時間あたり 100,000 件のメッセージを設定できます。

メッセージの出力は、配信サーバーで使用される IP アドレス (**mta**) ごとに制御する必要があります。 複数の **mta** を複数のマシンで分類し、様々なAdobe Campaignインスタンスに属する複数の  は、電子メール配信用に同じ IP アドレスを共有できます。これらの IP アドレスの使用を調整するには、プロセスを設定する必要があります。

**stat** モジュールは次の処理を行います。一連の IP アドレスに対してメールサーバーに送信されるすべての接続要求とメッセージを転送します。 統計サーバーは配信を追跡し、設定されたクォータに基づいて送信を有効または無効にできます。

![](assets/s_ncs_install_mta.png)

* 統計サーバ (**stat**) は、Adobe Campaignベースにリンクされ、設定を読み込みます。
* 配信サーバー (**mta**) は、UDP を使用して、常に自分のインスタンスに属しているとは限らない統計サーバーに接続します。

### 配信サーバー {#delivery-servers}

**mta** モジュールは、メッセージを **mtachild** 子モジュールに配信します。 各 **mtachild** は、統計サーバに認証をリクエストし、メッセージを送信する前に、メッセージを準備します。

手順は、以下のとおりです。

1. **mta** は、適格なメッセージを選択し、使用可能な **mtachild** を割り当てます。
1. **mtachild** は、メッセージの作成に必要なすべての情報（コンテンツ、パーソナライゼーション要素、添付ファイル、画像など）を そして、**E メールトラフィックシェイパー** にメッセージを転送します。
1. E メールトラフィックシェイパーが統計サーバーの承認 (**smtp stat**) を受け取るとすぐに、メッセージが受信者に送信されます。

![](assets/s_ncs_install_email_traffic_shaper.png)

### E メールサーバーの統計と制限事項 {#email-server-statistics-and-limitations}

統計サーバーは、メッセージを受信する各電子メールサーバーに関して、次の統計情報を保持します。

* 開いているポイントインタイム接続の数
* 過去 1 時間に送信されたメッセージの数
* 成功/拒否された接続の割合
* 未到達サーバーへの接続率。

同時に、このモジュールは、特定の電子メールサーバーに関する制限のリストを読み込みます。

* 同時接続の最大数
* 1 時間あたりの最大メッセージ数
* 1 回の接続あたりの最大メッセージ数。

### IP アドレスの管理 {#managing-ip-addresses}

統計サーバは、複数のインスタンスまたは複数のマシンを、同じパブリック IP アドレスで組み合わせることができます。 したがって、特定のインスタンスにリンクされるわけではありませんが、ドメインごとの制限を回復するために、インスタンスに問い合わせる必要があります。

配信統計は、ターゲット MX ごとに、ソース IP ごとに保持されます。 例えば、ターゲットドメインの MX が 5 で、プラットフォームが 3 つの異なる IP アドレスを使用できる場合、サーバーはこのドメインに対して最大 15 個の一連の指標を管理できます。

送信元 IP アドレスは、パブリック IP アドレス（リモート電子メールサーバーで確認されるアドレス）と一致します。 この IP アドレスは、NAT ルータが指定されている場合、**mta** をホストするマシンのアドレスとは異なる場合があります。 このため、統計サーバは、パブリック IP(**publicId**) と一致する識別子を使用します。 ローカルアドレスとこの識別子の関連付けは、**serverConf.xml** 設定ファイルで宣言します。 **serverConf.xml** で使用できるすべてのパラメーターは、この [ セクション ](../../installation/using/the-server-configuration-file.md) に記載されています。

## 配信出力コントロール {#delivery-output-controlling}

電子メールサーバーにメッセージを配信するには、**Email Traffic Shaper** コンポーネントが統計サーバーからの接続を要求します。 要求が受け入れられると、接続が開きます。

メッセージを送信する前に、モジュールはサーバーから「トークン」をリクエストします。 通常、これらは少なくとも 10 個のトークンのセットで、サーバーへのクエリの数が減ります。

サーバーは、接続と配信に関連するすべての統計を保存します。 再起動の場合、情報は一時的に失われます。各クライアントは、送信統計のローカルコピーを保持し、定期的に（2 分ごとに）サーバに返します。 その後、サーバーはデータを再集計できます。

次の節では、**E メールトラフィックシェイパー** コンポーネントによるメッセージの処理について説明します。

### メッセージ配信 {#message-delivery}

メッセージが送信されると、次の 3 つの結果が考えられます。

1. **成功**:メッセージは正常に送信されました。メッセージが更新されます。
1. **メッセージ失敗**:連絡先サーバーが、選択した受信者に対するメッセージを拒否しました。この結果は、リターンコード 550 ～ 599 に一致しますが、例外を定義できます。
1. **セッション失敗** （5.11 上向き）:このメ **** ッセージに対する回答を受け取ると、メッセージは破棄されます ( メッセージの [放棄](#message-abandonment)を参照 )。別のパスにメッセージが送信されるか、他のパスが使用できない場合は「保留」に設定されます（[「メッセージ保留 ](#message-pending)」を参照）。

   >[!NOTE]
   >
   >**パス** は、Adobe Campaign **mta** とターゲット **mta** との間の接続です。 Adobe Campaign **mta** は、複数の開始 IP および複数のターゲットドメイン IP から選択できます。

### メッセージの中断 {#message-abandonment}

破棄されたメッセージは **mta** に返され、**mtachild** では管理されなくなります。

**mta** は、このメッセージの手順（回復、放棄、強制隔離など）を 応答コードとルールに応じて異なります。

### メッセージを保留中 {#message-pending}

アクティブなキューに到達し、使用可能なパスがない場合、メッセージは保留されます。

通常、パスは、接続エラーの発生後、変数の時間は使用不可とマークされます。 使用できない期間は、エラーの頻度と期間によって異なります。

## 統計サーバーの設定 {#statistics-server-configuration}

統計サーバーは、複数のインスタンスで使用できます。これを使用するインスタンスとは独立して設定する必要があります。

まず、設定をホストするAdobe Campaignデータベースを定義します。

### 設定の開始 {#start-configuration}

デフォルトでは、**stat** モジュールは各インスタンスに対して起動されます。 インスタンスが同じマシン上でプールされる場合、またはインスタンスが同じ IP アドレスを共有する場合は、単一の統計サーバーが使用されます。その他の人々は障害を持たなければなりません

### サーバーポートの定義 {#definition-of-the-server-port}

デフォルトでは、統計サーバはポート 7777 をリッスンします。 このポートは、**serverConf.xml** ファイルで変更できます。 **serverConf.xml** で使用できるすべてのパラメーターは、この [ セクション ](../../installation/using/the-server-configuration-file.md) に記載されています。

```
<stat port="1234"/>
```

## MX 設定 {#mx-configuration}

>[!IMPORTANT]
>
>ホストインストールまたはハイブリッドインストールで [Enhanced MTA](../../delivery/using/sending-with-enhanced-mta.md) にアップグレードした場合、**[!UICONTROL MX 管理]**&#x200B;配信スループットは使用されなくなります。Enhanced MTA は独自の MX ルールを使用します。これにより、独自の E メールレピュテーション履歴および E メールを送信しているドメインから送信されるリアルタイムのフィードバックに基づいて、スループットをドメインごとにカスタマイズすることができます。

### MX ルールについて {#about-mx-rules}

>[!NOTE]
>
>この節と以下の節は、オンプレミスインストールと、レガシー Campaign MTA を使用したホスト/ハイブリッドインストールにのみ適用されます。

MX（Mail eXchanger）ルールは、送信サーバーと受信サーバーの間の通信を管理するルールです。

これらのルールは、クライアントインスタンスを定期的に提供するために、毎朝午前 6 時（サーバー時間）に自動的にリロードされます。

ISP では、機器の容量や社内ポリシーに応じて、1 時間につき、あらかじめ定義された数の接続とメッセージを受け付けます。これらの変数は、IP のレピュテーションや送信ドメインに応じて ISP システムによって自動的に変更される可能性があります。Adobe Campaign では、配信品質プラットフォームを通じて、ISP 別の 150 個以上の専用ルールに加えて、他のドメイン用の 1 つの汎用ルールを管理します。

接続の最大数は、MTA で使用されるパブリック IP アドレスの数だけに依存しているわけではありません。

例えば、MX ルールで許可した接続数が 5 で、設定したパブリック IP の数が 2 の場合、このドメインに対して同時に開かれる接続の数は 10 を超えることはできないと思われるでしょう。しかし、そうではありません。接続の最大数は、実際には、MTA のパブリック IP の 1 つとクライアントの MTA のパブリック IP の組み合わせであるパスを示します。

以下の例では、ユーザーに 2 つのパブリック IP アドレスが設定されており、ドメインは yahoo.com です。

```
user:~ user$ host -t mx yahoo.com
                yahoo.com mail is handled by 1 mta5.am0.yahoodns.net.
                yahoo.com mail is handled by 1 mta6.am0.yahoodns.net.
                yahoo.com mail is handled by 1 mta7.am0.yahoodns.net.
```

yahoo.com の MX レコードを見ると、yahoo.com に 3 つの Mail Exchanger があることがわかります。ピア Mail Exchanger に接続するには、MTA がその IP アドレスを DNS に要求します。

```
user:~ user$ host -t a mta5.am0.yahoodns.net
                mta5.am0.yahoodns.net has address 98.136.216.26
                mta5.am0.yahoodns.net has address 98.136.217.202
                mta5.am0.yahoodns.net has address 98.138.112.38
                mta5.am0.yahoodns.net has address 66.196.118.37
                mta5.am0.yahoodns.net has address 63.250.192.46
                mta5.am0.yahoodns.net has address 66.196.118.240
                mta5.am0.yahoodns.net has address 98.136.217.203
                mta5.am0.yahoodns.net has address 98.138.112.35
```

このレコードの場合、ユーザーは 8 個のピア IP アドレスに接続できます。ユーザーが 2 つのパブリック IP アドレスを持っているので、このユーザーは 8 * 2 = 16 の組み合わせで yahoo.com のメールサーバーに到達できます。 これらの組み合わせをそれぞれパスと呼びます。

2 つ目の MX レコードは次のようになります。

```
user:~ user$ host -t a mta6.am0.yahoodns.net
                mta6.am0.yahoodns.net has address 98.138.112.38
                mta6.am0.yahoodns.net has address 98.136.216.26
                mta6.am0.yahoodns.net has address 63.250.192.46
                mta6.am0.yahoodns.net has address 66.196.118.35
                mta6.am0.yahoodns.net has address 98.136.217.203
                mta6.am0.yahoodns.net has address 98.138.112.32
                mta6.am0.yahoodns.net has address 98.138.112.37
                mta6.am0.yahoodns.net has address 66.196.118.33
```

これら 8 個の IP アドレスのうち 4 個は、mta5 で既に使用されています（98.136.216.26、98.138.112.38、63.250.192.46 および 98.136.217.203）。このレコードでは、ユーザーは 4 つの新しい IP アドレスを使用できます。3 つ目の MX レコードも同様です。

全部で、16 個のリモート IP アドレスがあります。2 つのローカルパブリック IP アドレスと組み合わせると、yahoo.com のメールサーバーに到達するのに 32 個のパスがあります。

>[!NOTE]
>
>2 つの MX レコードが同じ IP アドレスを参照している場合は、これらは 2 つのパスではなく 1 つのパスとみなされます。

次に、MX ルールの使用例を示します。

![](assets/s_ncs_examples_mx_rules.png)

以下の例では、特定のドメインに対して 1 時間あたりのメッセージ数の上限が 10,000 件になっていますが、MTA のスループット能力はこの上限を上回っています。

この場合、トラフィックは 1 時間ごとに 5 分間の 12 周期に分割され、メッセージ数の実際の上限は 1 周期につき 833 件になります。

これらのメッセージはできるだけ速く配信されます。

![](assets/s_ncs_traffic_shaping.png)

### MX 管理の設定 {#configuring-mx-management}

MX に準拠するルールは、ツリーの **[!UICONTROL 管理/キャンペーン管理/配信不能件数の管理/メールルールセット]** ノードの **[!UICONTROL MX 管理]** ドキュメントで定義されています。

**[!UICONTROL MX 管理]** ドキュメントがノードに存在しない場合は、手動で作成できます。 手順は次のとおりです。

1. 一連の新しいメールルールを作成します。
1. **[!UICONTROL MX 管理]** モードを選択します。

   ![](assets/s_ncs_install_mx_mgt_rule.png)

1. 「**[!UICONTROL 内部名]**」フィールドに **defaultMXRules** と入力します。

変更を反映するには、統計サーバーを再起動する必要があります。

統計サーバを再起動せずに構成を再読み込みするには、サーバをホストするマシンで次のコマンドを使用します。`nlserver stat -reload`

>[!NOTE]
>
>このコマンドラインは、**nlserver restart** よりも推奨されます。再起動するまでに収集された統計データが失われることもなく、また、使用時のピークが MX ルールで定義された割り当てに違反するおそれもなくなります。

### MX ルールの設定 {#configuring-mx-rules}

**[!UICONTROL MX 管理]** ドキュメントには、MX ルールにリンクされているすべてのドメインが一覧表示されます。

これらのルールは順に適用されます。ターゲット MX と互換性のある MX マスクを持つ最初のルールが適用されます。

各ルールで使用できるパラメーターは次のとおりです。

* **[!UICONTROL MX マスク]**:ルールを適用するドメイン。各ルールは、MX のアドレスマスクを定義します。 したがって、このマスクと名前が一致する MX が有効です。 マスクには、「*」と「?」を含めることができます。 汎用文字。

   例えば、次のアドレスがあるとします。

   * a.mx.yahoo.com
   * b.mx.yahoo.com
   * c.mx.yahoo.com

   は、次のマスクと互換性があります。

   * *.yahoo.com
   * ?.mx.yahoo.com

   例えば、E メールアドレス foobar@gmail.com の場合、ドメインは gmail.com で、MX レコードは次のようになります。

   ```
   gmail.com mail exchanger = 20 alt2.gmail-smtp-in.l.google.com.
   gmail.com mail exchanger = 10 alt1.gmail-smtp-in.l.google.com.
   gmail.com mail exchanger = 40 alt4.gmail-smtp-in.l.google.com.
   gmail.com mail exchanger = 5  gmail-smtp-in.l.google.com.
   gmail.com mail exchanger = 30 alt3.gmail-smtp-in.l.google.com.
   ```

   この場合、MX ルール `*.google.com` が使用されます。 見てのとおり、MX ルールマスクは、メール内のドメインと必ずしも一致しません。gmail.com の電子メールアドレスに適用される MX ルールは、マスク `*.google.com` を持つものです。

* **[!UICONTROL 識別子の範囲]**:このオプションを使用すると、ルールを適用する識別子の範囲 (publicID) を指定できます。以下を指定できます。

   * 数値：このルールは、この publicId にのみ適用されます。
   * 数値の範囲（**数値 1 — 数値 2**）:この 2 つの数値の間のすべての publicId にルールが適用されます。

   >[!NOTE]
   >
   >このフィールドが空の場合、ルールはすべての識別子に適用されます。

   パブリック ID は、1 つまたは複数の MTA で使用されるパブリック IP アドレスの内部識別子です。これらの ID は MTA サーバーの **config-instance.xml** ファイルに定義されます。

   ![](assets/s_ncs_install_mta_ips.png)

* **[!UICONTROL 共有]**:は、この MX ルールのプロパティの範囲を定義します。これをオンにすると、インスタンスで使用可能なすべての IP アドレスですべてのパラメーターが共有されます。オフにすると、MX ルールは IP アドレスごとに定義されます。メッセージの最大数は、使用可能な IP アドレスの数を乗算したものになります。
* **[!UICONTROL 接続の最大数]**:送信者のドメインへの同時接続の最大数。
* **[!UICONTROL メッセージの最大数]**:接続で送信できるメッセージの最大数。メッセージがこの数を超えると、接続が閉じられ、新しい接続が開きます。
* **[!UICONTROL 1 時間あたりのメッセージ数]**:送信者のドメインに 1 時間で送信できるメッセージの最大数。
* **[!UICONTROL 接続タイムアウト]**:ドメインに接続するための時間のしきい値。

   >[!NOTE]
   >
   >このしきい値の前に **タイムアウト** を発行する可能性があります。これは、お使いの Windows のバージョンによって異なります。

* **[!UICONTROL タイムアウトデータ]**:メッセージコンテンツ送信後の最大待機時間（SMTP プロトコルの DATA セクション）。
* **[!UICONTROL タイムアウト]**:SMTP サーバーとの他の交換の最大待機時間です。
* **[!UICONTROL TLS]**:E メール配信を暗号化する TLS プロトコルを選択して有効にすることができます。各 MX マスクに対して、次のオプションを使用できます。

   * **[!UICONTROL デフォルト設定]**:これは、適用される serverConf.xml 設定ファイルで指定された一般的な設定です。

      >[!IMPORTANT]
      >
      >デフォルトの設定は変更しないことをお勧めします。

   * **[!UICONTROL 無効]** :メッセージは、暗号化されずに体系的に送信されます。
   * **[!UICONTROL 日和見主義]** :受信サーバー (SMTP) が TLS プロトコルを生成できる場合、メッセージ配信は暗号化されます。

設定例：

![](assets/s_ncs_install_mx_mgt_rule_details.png)

>[!NOTE]
>
>Adobe Campaignでの MX サーバーの使用について詳しくは、[ この節 ](../../installation/using/using-mx-servers.md) を参照してください。

### E メールフォーマットの管理 {#managing-email-formats}

送信メッセージの形式を定義して、表示されるコンテンツが各受信者のアドレスのドメインに応じて自動的に適応するようにできます。

そのためには、**[!UICONTROL 管理]** / **[!UICONTROL キャンペーン管理]** / **[!UICONTROL 配信不能件数の管理]** / **[!UICONTROL メールルールセット]** にある **[!UICONTROL 電子メールフォーマットの管理]** ドキュメントに移動します。

このドキュメントには、Adobe Campaignが管理する日本語形式に対応する、事前定義済みのすべてのドメインのリストが含まれています。 詳しくは、[ このドキュメント ](../../delivery/using/defining-the-email-content.md#sending-emails-on-japanese-mobiles) を参照してください。

![](assets/mail_rule_sets.png)

**MIME 構造** （多目的インターネットメール拡張）パラメーターを使用すると、様々なメールクライアントに送信されるメッセージ構造を定義できます。 次の 3 つのオプションを使用できます。

* **マルチパート**:メッセージはテキスト形式または HTML 形式で送信されます。HTML 形式が受け入れられない場合でも、メッセージはテキスト形式で表示できます。

   デフォルトでは、マルチパート構造は **マルチパート/オルタナティブ** ですが、画像がメッセージに追加されると、自動的に **マルチパート/関連** になります。 特定のプロバイダーは、デフォルトで **multipart/related** 形式を想定していますが、**[!UICONTROL 「Force multipart/related]**」オプションは、画像が添付されていない場合でも、この形式を適用します。

* **HTML**:HTML のみのメッセージが送信されます。HTML 形式が受け入れられない場合、メッセージは表示されません。
* **テキスト**:テキストのみの形式のメッセージが送信されます。テキスト形式のメッセージの利点は、非常に小さいサイズです。

「**[!UICONTROL 画像を含める]**」オプションが有効になっている場合は、電子メールの本文に直接表示されます。 画像がアップロードされ、URL リンクがコンテンツで置き換えられます。

このオプションは、特に日本の市場で **デコメール**、**デコレメール**、**デコレーションメール** に使用されています。 詳しくは、[ このドキュメント ](../../delivery/using/defining-the-email-content.md#sending-emails-on-japanese-mobiles) を参照してください。

>[!IMPORTANT]
>
>E メールに画像を挿入すると、サイズが大幅に大きくなります。

## 配信サーバーの設定 {#delivery-server-configuration}

### クロック同期 {#clock-synchronization}

Adobe Campaignプラットフォームを構成するすべてのサーバー（データベースを含む）のクロックを同期し、システムを同じタイムゾーンに設定する必要があります。

### 統計サーバの座標 {#coordinates-of-the-statistics-server}

統計サーバのアドレスは、**mta** で指定する必要があります。

設定の **mta** 要素の **statServerAddress** プロパティを使用して、使用するポートのアドレスと番号を指定できます。

```
<mta statServerAddress="emailStatServer:7777">
   [...]
 </mta>
```

同じマシン上で統計サーバーを使用するには、少なくとも **localhost** の値を持つマシン名を入力する必要があります。

```
 <mta statServerAddress="localhost">
```

>[!IMPORTANT]
>
>このフィールドに値が入力されていない場合、**mta** は開始されません。

### 使用する IP アドレスのリスト {#list-of-ip-addresses-to-use}

トラフィック管理に関する設定は、設定ファイルの **mta/child/smtp** 要素にあります。

**IPAffinity** 要素ごとに、マシンで使用できる IP アドレスを宣言する必要があります。

例：

```
<IPAffinity localDomain="<domain>" name="default">
  <IP address="192.168.0.11" publicId="1" weight="5"/>
  <IP address="192.168.0.12" heloHost="revdns1.campaign.com" publicId="2" weight="5"/>
  <IP address="192.168.0.13" publicId="3" weight="1"/>
</IPAffinity>
```

パラメーターは次のとおりです。

* **アドレス**:使用する MTA ホストマシンの IP アドレスです。
* **heloHost**:この識別子は、SMTP サーバーで確認される IP アドレスを表します。

* **publicId**:この情報は、NAT ルータの背後にある複数のAdobe Campaignマタスによって IP アドレスが共有さ **** れる場合に役立ちます。統計サーバは、この識別子を用いて、この開始点とターゲットサーバとの間の接続および送信統計を記憶する。
* **重み付け**:アドレスの相対的な使用頻度を定義できます。デフォルトでは、すべてのアドレスの重み付けは 1 に等しくなります。

>[!NOTE]
>
>serverConf.xml ファイルでは、1 つの IP が一意の識別子 (public_id) を持つ単一の helohost に対応していることを確認する必要があります。 複数のヘロホストにマッピングできないので、配信のスロットリングの問題が発生する可能性があります。

前述の例では、通常の条件の場合、アドレスは次のように配分されます。

    * &quot;1&quot;:5 / (5+5+1) = 45%
     * &quot;2&quot;:5 / (5+5+1) = 45%
     * &quot;3&quot;:1 / (5+5+1) = 10%

例えば、最初のアドレスを特定の MX に対して使用できない場合、メッセージは次のように送信されます。

    * &quot;2&quot;:5 / (5+1) = 83%
     * &quot;3&quot;:1 / (5+1) = 17%

* **includeDomains**:では、この IP アドレスを特定のドメインに属する E メール用に予約できます。これは、1 つ以上のワイルドカード (&#39;*&#39;) を含むことができるマスクのリストです。 属性を指定しない場合、すべてのドメインでこの IP アドレスを使用できます。

   例：**includeDomains=&quot;wanadoo.com,orange.com,yahoo.*&quot;**

* **excludeDomains**:は、この IP アドレスのドメインのリストを除外します。このフィルターは、**includeDomains** フィルターの後に適用されます。

   ![](assets/s_ncs_install_mta_ips.png)

## E メール送信の最適化 {#email-sending-optimization}

Adobe Campaign **mta** の内部アーキテクチャは、E メール配信を最適化するための設定に影響を与えます。 配信の改善に関するヒントをいくつか示します。

### maxWaitingMessages パラメーターの調整 {#adjust-the-maxwaitingmessages-parameter}

**maxWaitingMessages** パラメーターは、事前に **mtachild** によって準備されたメッセージの最大数を示します。 メッセージは、送信または破棄された場合にのみ、このリストから削除されます。

このパラメーターは非常に重要で、メッセージがドメインで並べ替えられない場合は特に重要です。

**maxWorkingSetMb**(256) しきい値に達すると、配信サーバーはメッセージの送信を停止します。 **mtachild** が再び起動するまで、パフォーマンスは大幅に低下します。 この問題を回避するには、**maxWorkingSetMb** パラメーターのしきい値を増やすか、**maxWaitingMessages** パラメーターのしきい値を減らします。

**maxWorkingSetMb** パラメータは、メッセージの最大数に平均メッセージサイズを掛け、その結果に 2.5 を掛けて経験的に計算されます。例えば、メッセージの平均サイズが 50 kB で、**maxWaitingMessages** が 1,000 の場合、使用メモリは平均 125 MB です。

### mtachild の数を調整する {#adjust-the-number-of-mtachild}

子の数は、マシン内のプロセッサ数を超えてはなりません ( 1,000 セッション )。 8 **mtachild** を超えないことをお勧めします。 その後、**子**(**maxMsgPerChild**) あたりのメッセージ数を増やして、十分な寿命を実現できます。
