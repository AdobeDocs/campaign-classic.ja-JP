---
solution: Campaign Classic
product: campaign
title: E メールの配信品質
description: E メールの配信品質
audience: installation
content-type: reference
topic-tags: additional-configurations
translation-type: tm+mt
source-git-commit: fd6195ca447fa0345189f3153f44ad2f9a067210
workflow-type: tm+mt
source-wordcount: '3040'
ht-degree: 19%

---


# 技術的な E メール設定{#email-deliverability}

## 概要 {#overview}

次の節では、電子メール配信時にAdobe Campaignインスタンスの出力を制御するために必要な設定の概要を説明します。

>[!NOTE]
>
>設定によっては、Adobeがサーバとインスタンスの設定ファイルにアクセスする場合など、Adobeがホストする配置に対してのみ実行できる場合があります。 各デプロイメントの詳細については、[「モデルのホスト](../../installation/using/hosting-models.md)」セクションまたは[このページ](../../installation/using/capability-matrix.md)を参照してください。

配信品質に関する概念とベストプラクティスについて詳しくは、[](../../delivery/using/about-deliverability.md)を参照してください。

Adobe Campaignプラットフォームによる電子メールの効率的な送受信に関する技術的な推奨事項は、この[セクション](../../delivery/using/technical-recommendations.md)に記載されています。

## 動作の仕組み {#operating-principle}

1つ以上のAdobe Campaignインスタンスの出力を制御して、ドメインに応じて送信される電子メールの数を制限できます。 例えば、**yahoo.com**&#x200B;のアドレスに対して1時間あたり20,000件に制限し、その他すべてのドメインに対して1時間あたり100,000件のメッセージを設定できます。

配信サーバーが使用する各IPアドレス(**mta**)に対してメッセージ出力を制御する必要があります。 複数のマシン上で分類され、様々なAdobe Campaignインスタンスに属する複数の&#x200B;**mta**&#x200B;は、電子メール配信用に同じIPアドレスを共有できます。プロセスは、これらのIPアドレスの使用を調整するために設定する必要があります。

**stat**&#x200B;モジュールは次のように動作します。一連のIPアドレスに関してメールサーバに送信されるすべての接続要求とメッセージを転送します。 統計サーバは配信を追跡し、設定された割り当てに基づいて送信を有効または無効にできます。

![](assets/s_ncs_install_mta.png)

* 統計サーバ(**stat**)は、Adobe Campaignベースにリンクされ、構成を読み込みます。
* 配信サーバ(**mta**)は、必ずしも自分のインスタンスに属しているとは限らない統計情報サーバにUDPを使用します。

### 配信サーバ{#delivery-servers}

**mta**&#x200B;モジュールは、**mtachild**&#x200B;子モジュールにメッセージを配布します。 各&#x200B;**mtachild**&#x200B;は、統計サーバーから認証を要求し、送信する前に、メッセージを準備します。

手順は、以下のとおりです。

1. **mta**&#x200B;は、有効なメッセージを選択し、使用可能な&#x200B;**mtachild**&#x200B;を割り当てます。
1. **mtachild**&#x200B;は、メッセージの作成に必要なすべての情報（コンテンツ、パーソナライゼーション要素、添付ファイル、画像など）を読み込みます。 メッセージを&#x200B;**電子メールトラフィックシェイパ**&#x200B;に転送します。
1. 電子メールトラフィックシェーパーが統計サーバーの認証(**smtp stat**)を受け取るとすぐに、受信者にメッセージが送信されます。

![](assets/s_ncs_install_email_traffic_shaper.png)

### 電子メールサーバの統計と制限{#email-server-statistics-and-limitations}

統計サーバーは、メッセージを受信する各電子メールサーバーに対して次の統計情報を維持します。

* 開いているポイントインタイム接続の数、
* 過去1時間に送信されたメッセージの数、
* 成功/拒否された接続の割合、
* 未到達サーバーへの接続率。

同時に、モジュールは、特定の電子メールサーバーに関する制限のリストを読み込みます。

* 同時接続の最大数、
* 1時間あたりの最大メッセージ数、
* 1回の接続で最大メッセージ数。

### IPアドレスの管理{#managing-ip-addresses}

統計サーバは、複数のインスタンスまたは複数のマシンを同じパブリックIPアドレスと組み合わせることができます。 したがって、特定のインスタンスにリンクされるわけではありませんが、ドメインごとの制限を回復するには、インスタンスに問い合わせる必要があります。

配信統計は、各ターゲットMXと各ソースIPに対して保持されます。 例えば、対象のドメインのMXが5で、プラットフォームが3つの異なるIPアドレスを使用できる場合、サーバーはこのドメインに対して最大15個の一連のインジケーターを管理できます。

ソースIPアドレスはパブリックIPアドレス（リモート電子メールサーバーで表示されるアドレス）と一致します。 このIPアドレスは、NATルータが指定されている場合、**mta**&#x200B;をホストするマシンのアドレスと異なる場合があります。 このため、統計サーバはパブリックIP(**publicId**)と一致する識別子を使用します。 ローカルアドレスとこの識別子との関連付けは、**serverConf.xml**&#x200B;設定ファイルで宣言されます。 **serverConf.xml**&#x200B;で使用できるすべてのパラメーターは、この[セクション](../../installation/using/the-server-configuration-file.md)に一覧表示されます。

## {#delivery-output-controlling}を制御する配信出力

電子メールサーバーにメッセージを配信するために、**Email Traffic Shaper**&#x200B;コンポーネントは、統計サーバーからの接続を要求します。 要求が受け入れられると、接続が開きます。

メッセージを送信する前に、モジュールはサーバーから「トークン」を要求します。 一般に、これらは少なくとも10個のトークンのセットであり、サーバーへのクエリ数が減少します。

接続と配信に関連するすべての統計情報が保存されます。 再起動時に、情報は一時的に失われます。各クライアントは、送信統計のローカルコピーを保持し、定期的に（2分ごとに）サーバに返します。 その後、サーバーはデータの集計を再度行うことができます。

以下の節では、**電子メールトラフィックシェーパー**&#x200B;コンポーネントによるメッセージの処理について説明します。

### メッセージ配信{#message-delivery}

メッセージが送信されると、次の3つの結果が生じる可能性があります。

1. **成功**:メッセージが正常に送信されました。メッセージが更新されます。
1. **Message Failed**:接続されたサーバーは、選択された受信者のメッセージを拒否しました。この結果は、リターンコード550 ～ 599に一致しますが、例外を定義できます。
1. **セッション失敗** （上向き5.11）:このメッセージに対する **** 回答を [受け取ると、メッセージは破棄されます(](#message-abandonment)メッセージの中断を参照)。別のパスにメッセージが送信されるか、他のパスが使用できない場合はpendingに設定されます（[Message pending](#message-pending)を参照）。

   >[!NOTE]
   >
   >**パス**&#x200B;は、Adobe Campaign **mta**&#x200B;とターゲット&#x200B;**mta**&#x200B;との間の接続です。 Adobe Campaign **mta**&#x200B;は、複数の開始IPおよび複数のターゲットドメインIPから選択できます。

### メッセージの中断{#message-abandonment}

破棄されたメッセージは&#x200B;**mta**&#x200B;に返され、**mtachild**&#x200B;で管理されなくなります。

**mta**&#x200B;は、このメッセージの手順(回復、中断、強制隔離など)を決定します。 」をクリックします。

### 保留中のメッセージ{#message-pending}

メッセージは、アクティブなキューに到着し、使用可能なパスがない場合に追加されます。

通常、接続エラーが発生した後、パスは一定の時間使用不可とマークされます。 使用できない期間は、エラーの頻度と発生時間によって異なります。

## 統計サーバの構成{#statistics-server-configuration}

統計サーバは、複数のインスタンスで使用できます。これを使用するインスタンスとは独立して設定する必要があります。

開始を行います。

### 開始構成{#start-configuration}

デフォルトでは、**stat**&#x200B;モジュールは各インスタンスに対して起動します。 インスタンスが同じマシン上で相互化されている場合、またはインスタンスが同じIPアドレスを共有している場合は、単一の統計サーバーが使用されます。他の人は障害を持つ必要があります。

### サーバーポートの定義{#definition-of-the-server-port}

デフォルトでは、統計サーバーはポート7777をリッスンします。 このポートは、**serverConf.xml**&#x200B;ファイルで変更できます。 **serverConf.xml**&#x200B;で使用できるすべてのパラメーターは、この[セクション](../../installation/using/the-server-configuration-file.md)に一覧表示されます。

```
<stat port="1234"/>
```

## MX構成{#mx-configuration}

>[!IMPORTANT]
>
>ホスト型またはハイブリッド型のインストールの場合、[拡張MTA](../../delivery/using/sending-with-enhanced-mta.md)にアップグレードした場合、**[!UICONTROL MX management]**&#x200B;配信のスループットルールは使用されなくなります。 Enhanced MTA は独自の MX ルールを使用します。これにより、独自の E メールレピュテーション履歴および E メールを送信しているドメインから送信されるリアルタイムのフィードバックに基づいて、スループットをドメインごとにカスタマイズすることができます。

以下の節は、レガシーキャンペーンMTAを使用したオンプレミスインストールおよびホスト/ハイブリッドインストールにのみ適用されます。

### MX ルールについて {#about-mx-rules}

MX（Mail eXchanger）ルールは、送信サーバーと受信サーバーの間の通信を管理するルールです。

これらのルールは、定期的にクライアントインスタンスを供給するために、毎朝6AM（サーバー時間）に自動的にリロードされます。

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

このレコードの場合、ユーザーは 8 個のピア IP アドレスに接続できます。ユーザーには 2 つのパブリック IP アドレスがあるので、yahoo.com のメールサーバーに到達するのに、8 * 2 = 16 個の組み合わせが存在することになります。これらの組み合わせをそれぞれパスと呼びます。

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

以下に、MXルールの使用例を示します。

![](assets/s_ncs_examples_mx_rules.png)

以下の例では、特定のドメインに対して 1 時間あたりのメッセージ数の上限が 10,000 件になっていますが、MTA のスループット能力はこの上限を上回っています。

この場合、トラフィックは 1 時間ごとに 5 分間の 12 周期に分割され、メッセージ数の実際の上限は 1 周期につき 833 件になります。

これらのメッセージはできるだけ速く配信されます。

![](assets/s_ncs_traffic_shaping.png)

### MX 管理の設定 {#configuring-mx-management}

MXに準拠するルールは、ツリーの&#x200B;**[!UICONTROL [管理] > [キャンペーン管理] > [配信不能な管理] > [メールルールセット]]**&#x200B;ドキュメントの&#x200B;**[!UICONTROL MX management]**&#x200B;ノードで定義されます。

**[!UICONTROL MX management]**&#x200B;ドキュメントがノードに存在しない場合は、手動で作成できます。 手順は次のとおりです。

1. 新しいメールルールのセットを作成します。
1. **[!UICONTROL MX management]**&#x200B;モードを選択します。

   ![](assets/s_ncs_install_mx_mgt_rule.png)

1. **[!UICONTROL Internal name]**&#x200B;フィールドに&#x200B;**defaultMXRules**&#x200B;と入力します。

変更を考慮するには、統計サーバを再起動する必要があります。

統計サーバーを再起動せずに設定を再読み込みするには、サーバーをホストするマシンで次のコマンドを使用します。`nlserver stat -reload`

>[!NOTE]
>
>このコマンドラインは、**nlserver restart** よりも推奨されます。再起動するまでに収集された統計データが失われることもなく、また、使用時のピークが MX ルールで定義された割り当てに違反するおそれもなくなります。

### MXルールの設定{#configuring-mx-rules}

**[!UICONTROL MX management]**&#x200B;ドキュメントリストは、MXルールにリンクされているすべてのドメインを識別します。

次のルールが順に適用されます。MXマスクがターゲットのMXと互換性がある最初のルールが適用されます。

各ルールで使用できるパラメーターは次のとおりです。

* **[!UICONTROL MXマスク]**:ルールを適用するドメイン。各規則はMXのアドレスマスクを定義します。 したがって、このマスクと名前が一致するMXはすべて有効です。 マスクには、「*」と「?」を含めることができます。 汎用文字。

   例えば、次のアドレスがあります。

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

   この場合、MXルール`*.google.com`が使用されます。 見てのとおり、MX ルールマスクは、メール内のドメインと必ずしも一致しません。gmail.comの電子メールアドレスに適用されるMXルールは、`*.google.com`マスクを持つものです。

* **[!UICONTROL 識別子の範囲]**:このオプションを使用すると、ルールを適用する識別子(publicID)の範囲を指定できます。次を指定できます。

   * 数値：このルールは、このpublicIdにのみ適用されます。
   * 数値の範囲（**数値1 — 数値2**）:この2つの数字の間のすべてのpublicIdにルールが適用されます。

   >[!NOTE]
   >
   >フィールドが空の場合、ルールはすべての識別子に適用されます。

   パブリック ID は、1 つまたは複数の MTA で使用されるパブリック IP アドレスの内部識別子です。これらの ID は MTA サーバーの **config-instance.xml** ファイルに定義されます。

   ![](assets/s_ncs_install_mta_ips.png)

* **[!UICONTROL 共有]**:このMX規則のプロパティのスコープを定義します。これをオンにすると、インスタンスで使用可能なすべての IP アドレスですべてのパラメーターが共有されます。オフにすると、MX ルールは IP アドレスごとに定義されます。メッセージの最大数は、使用可能な IP アドレスの数を乗算したものになります。
* **[!UICONTROL 最大接続数]**:送信者のドメインへの同時接続の最大数。
* **[!UICONTROL 最大メッセージ数]**:接続で送信できるメッセージの最大数。メッセージがこの数を超えると、接続は閉じられ、新しい接続が開きます。
* **[!UICONTROL 1時間あたりのメッセージ]**:送信者のドメインに1時間で送信できるメッセージの最大数です。
* **[!UICONTROL 接続タイムアウト]**:ドメインに接続するための時間のしきい値。

   >[!NOTE]
   >
   >このしきい値の前に&#x200B;**timeout**&#x200B;を発行できます。これは、お使いのWindowsのバージョンによって異なります。

* **[!UICONTROL タイムアウトデータ]**:メッセージの内容を送信した後の最大待機時間（SMTPプロトコルのDATAセクション）。
* **[!UICONTROL タイムアウト]**:SMTPサーバーとの他の交換の最大待機時間です。
* **[!UICONTROL TLS]**:電子メール配信の暗号化を可能にするTLSプロトコルを選択して有効にすることができます。MXマスクごとに、次のオプションを使用できます。

   * **[!UICONTROL デフォルト設定]**:これは、適用されるserverConf.xml設定ファイルで指定されている一般的な設定です。

      >[!IMPORTANT]
      >
      >デフォルトの設定は変更しないことをお勧めします。

   * **[!UICONTROL 無効]** :メッセージは、暗号化せずに系統的に送信されます。
   * **[!UICONTROL ご都合主義]** :受信サーバー(SMTP)がTLSプロトコルを生成できる場合、メッセージ配信は暗号化されます。

設定の例：

![](assets/s_ncs_install_mx_mgt_rule_details.png)

### E メールフォーマットの管理{#managing-email-formats}

送信メッセージの形式を定義して、表示されるコンテンツが各受信者のアドレスのドメインに合わせて自動的に調整されるようにします。

これを行うには、**[!UICONTROL 管理]** > **[!UICONTROL キャンペーン管理]****[!UICONTROL 配信不能管理]** > **[!UICONTROL メールルールセット]**&#x200B;にある&#x200B;**[!UICONTROL E メールフォーマットの管理]**&#x200B;ドキュメントに移動します。

このドキュメントには、Adobe Campaignが管理する日本語形式に対応する定義済みのすべてのドメインのリストが含まれています。 詳しくは、[このドキュメント](../../delivery/using/defining-the-email-content.md#sending-emails-on-japanese-mobiles)を参照してください。

![](assets/mail_rule_sets.png)

**MIME構造** (Multipurpose Internet Mail Extensions)パラメータを使うと、異なるメールクライアントに送信するメッセージ構造を定義できます。 次の 3 つのオプションを使用できます。

* **Multipart**:メッセージは、テキストまたはHTML形式で送信されます。HTML形式を受け入れない場合、メッセージはテキスト形式で表示できます。

   デフォルトでは、マルチパート構造は&#x200B;**multipart/alternative**&#x200B;ですが、メッセージに画像が追加されると自動的に&#x200B;**multipart/related**&#x200B;になります。 特定のプロバイダーは、デフォルトで&#x200B;**マルチパート/関連**&#x200B;の形式を想定していますが、**[!UICONTROL マルチパート/関連]**&#x200B;を強制オプションを使用すると、イメージが添付されていない場合でも、この形式が適用されます。

* **HTML**:HTMLのみのメッセージが送信されます。HTML形式を受け入れない場合、メッセージは表示されません。
* **テキスト**:テキストのみの形式のメッセージが送信されます。テキスト形式のメッセージの利点は、非常に小さいサイズです。

「**[!UICONTROL 画像を含める]**」オプションが有効になっている場合は、電子メールの本文に直接表示されます。 画像がアップロードされ、URLリンクがそのコンテンツに置き換えられます。

このオプションは、特に日本の市場では、デコメール&#x200B;**、**&#x200B;デコメール&#x200B;**、**&#x200B;デコメメメール&#x200B;**に使われています。**&#x200B;詳しくは、[このドキュメント](../../delivery/using/defining-the-email-content.md#sending-emails-on-japanese-mobiles)を参照してください。

>[!IMPORTANT]
>
>電子メールに画像を挿入すると、サイズが大幅に増えます。

## 配信サーバーの構成{#delivery-server-configuration}

### クロック同期{#clock-synchronization}

Adobe Campaignプラットフォーム（データベースを含む）を構成するすべてのサーバーのクロックを同期し、同じタイムゾーンに設定する必要があります。

### 統計サーバ{#coordinates-of-the-statistics-server}の座標

統計サーバーのアドレスは、**mta**&#x200B;に入力する必要があります。

構成の&#x200B;**mta**&#x200B;要素の&#x200B;**statServerAddress**&#x200B;プロパティを使用して、使用するポートのアドレスと番号を指定できます。

```
<mta statServerAddress="emailStatServer:7777">
   [...]
 </mta>
```

同じマシン上で統計サーバーを使用するには、少なくとも&#x200B;**localhost**&#x200B;値を持つマシンの名前を入力する必要があります。

```
 <mta statServerAddress="localhost">
```

>[!IMPORTANT]
>
>このフィールドに値が入力されていない場合、**mta**&#x200B;は開始されません。

### {#list-of-ip-addresses-to-use}を使用するIPアドレスのリスト

トラフィック管理に関する設定は、設定ファイルの&#x200B;**mta/child/smtp**&#x200B;要素にあります。

**IPAffinity**&#x200B;要素ごとに、マシンに使用できるIPアドレスを宣言する必要があります。

例：

```
<IPAffinity localDomain="<domain>" name="default">
  <IP address="192.168.0.11" publicId="1" weight="5"/>
  <IP address="192.168.0.12" heloHost="revdns1.campaign.com" publicId="2" weight="5"/>
  <IP address="192.168.0.13" publicId="3" weight="1"/>
</IPAffinity>
```

パラメーターは次のとおりです。

* **アドレス**:これは、使用するMTAホストマシンのIPアドレスです。
* **heloHost**:この識別子は、SMTPサーバーに表示されるIPアドレスを表します。

* **publicId**:この情報は、NATルータの背後にある複数のAdobe Campaign **** mtasharedがIPアドレスを共有する場合に役立ちます。統計サーバは、この識別子を用いて、この起点とターゲットサーバとの間の接続と送信の統計を記憶する。
* **重み付け**:アドレスの相対的な使用頻度を定義できます。デフォルトでは、すべてのアドレスの重み付けは1に等しくなります。

>[!NOTE]
>
>serverConf.xmlファイルでは、1つのIPが一意の識別子(public_id)を持つ単一のhelohostに対応していることを確認する必要があります。 複数のhelohostsにマッピングできないので、配信のスロットリングの問題が発生する可能性があります。

前の例では、通常の条件を満たす場合、アドレスは次のように配布されます。

    * &quot;1&quot;:5 / (5+5+1) = 45%
    * &quot;2&quot;:5 / (5+5+1) = 45%
    * &quot;3&quot;:1 / (5+5+1) = 10%

例えば、最初のアドレスを特定のMXに対して使用できない場合、次のようにメッセージが送信されます。

    * &quot;2&quot;:5 / (5+1) = 83%
    * &quot;3&quot;:1 / (5+1) = 17%

* **includeDomains**:このIPアドレスは、特定のドメインに属する電子メールに対して予約できます。これは、1つ以上のワイルドカード(&#39;*&#39;)を含むことができるマスクのリストです。 属性を指定しない場合、すべてのドメインでこのIPアドレスを使用できます。

   例：**includeDomains=&quot;wanadoo.com,orange.com,yahoo.*&quot;**

* **excludeDomains**:このIPアドレスのドメインのリストを除外します。このフィルターは、**includeDomains**&#x200B;フィルターの後に適用されます。

   ![](assets/s_ncs_install_mta_ips.png)

## 電子メール送信の最適化{#email-sending-optimization}

Adobe Campaign **mta**&#x200B;の内部アーキテクチャは、電子メール配信を最適化するための設定に影響を与えます。 配信の改善に関するヒントをいくつか示します。

### maxWaitingMessagesパラメーター{#adjust-the-maxwaitingmessages-parameter}を調整

**maxWaitingMessages**&#x200B;パラメーターは、**mtachild**&#x200B;によって事前に準備されたメッセージの最大数を示します。 メッセージは、送信または破棄された後にのみ、このリストから削除されます。

このパラメーターは非常に重要で、メッセージがドメインで並べ替えられていない場合は特に重要です。

**maxWorkingSetMb** (256)のしきい値に達すると、配信サーバはメッセージの送信を停止します。 **mtachild**&#x200B;開始が再び上がるまで、パフォーマンスは大幅に低下します。 この問題を回避するには、**maxWorkingSetMb**&#x200B;パラメーターのしきい値を増やすか、**maxWaitingMessages**&#x200B;パラメーターのしきい値を減らします。

**maxWorkingSetMb**&#x200B;パラメーターは、メッセージの最大数に平均メッセージサイズを乗じて2.5を乗じて経験的に計算されます。例えば、メッセージの平均サイズが50 kBで、**maxWaitingMessages**&#x200B;パラメーターが1,000の場合、使用メモリが使用されます平均125 MB。

### mtachildの数を調整{#adjust-the-number-of-mtachild}

子の数が、マシンのプロセッサ数を超えてはなりません(約 1,000個のセッション)。 8 **mtachild**&#x200B;を超えないことをお勧めします。 その後、十分な寿命を確保するために、**子**(**maxMsgPerChild**)あたりのメッセージ数を増やすことができます。
