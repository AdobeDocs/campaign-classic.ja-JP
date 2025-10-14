---
product: campaign
title: 技術的なメール設定
description: メールの配信時にインスタンスの出力を制御するように Campaign を設定する方法を説明します
feature: Installation, Deliverability
badge-v7-prem: label="オンプレミス／ハイブリッドのみ" type="Caution" url="https://experienceleague.adobe.com/docs/campaign-classic/using/installing-campaign-classic/architecture-and-hosting-models/hosting-models-lp/hosting-models.html?lang=ja" tooltip="オンプレミスデプロイメントとハイブリッドデプロイメントにのみ適用されます"
audience: installation
content-type: reference
topic-tags: additional-configurations
exl-id: 515adad2-6129-450a-bb9e-fc80127835af
source-git-commit: ad6f3f2cf242d28de9e6da5cec100e096c5cbec2
workflow-type: tm+mt
source-wordcount: '3163'
ht-degree: 13%

---

# 技術的なメール設定{#email-deliverability}



## 概要 {#overview}

次の節では、メール配信時のAdobe Campaign インスタンスの出力を制御するために必要な設定の概要について説明します。

>[!NOTE]
>
>サーバーやインスタンスの設定ファイルにアクセスする場合など、Adobeがホストするデプロイメントでは、一部の設定はAdobeでのみ実行できます。 様々なデプロイメントの詳細については、[ モデルのホスティング ](../../installation/using/hosting-models.md) の節または [ このページ ](../../installation/using/capability-matrix.md) を参照してください。

Adobe Campaignの配信品質に関する概念とベストプラクティスについて詳しくは、この [ 節 ](../../delivery/using/about-deliverability.md) を参照してください。

Adobe プラットフォームによるメールの効率的な送受信に関するすべての技術的な推奨事項など、配信品質の概要については、[Adobeの配信品質のベストプラクティスガイド ](https://experienceleague.adobe.com/docs/deliverability-learn/deliverability-best-practice-guide/introduction.html?lang=ja) を参照してください。

## 動作の原則 {#operating-principle}

1 つ以上のAdobe Campaign インスタンスの出力を制御して、ドメインに応じて送信されるメールの数を制限できます。 例えば、**yahoo.com** アドレスの場合は 1 時間あたり 20,000 件に出力を制限し、その他のすべてのドメインでは 1 時間あたり 100,000 件のメッセージを設定できます。

メッセージの出力は、配信サーバーで使用される IP アドレスごとに制御する必要があります（**mta**）。 複数のマシンに分類され、様々なAdobe Campaign インスタンスに属する複数の **mta** が、メール配信用に同じ IP アドレスを共有できます。これらの IP アドレスの使用を調整するには、プロセスを設定する必要があります。

**stat** モジュールは、一連の IP アドレスのメールサーバーに送信されるすべての接続要求とメッセージを転送します。 統計サーバーは配信を追跡し、設定されたクォータに基づいて送信を有効または無効にすることができます。

![](assets/s_ncs_install_mta.png)

* 統計サーバー（**stat**）は、設定を読み込むためにAdobe Campaign ベースにリンクされています。
* 配信サーバー（**mta**）は、UDP を使用して、常に独自のインスタンスに属するとは限らない統計サーバーに接続します。

### 配信サーバー {#delivery-servers}

**mta** モジュールは、メッセージを **mtachild** 子モジュールに配布します。 各 **mtachild** は、統計サーバーから認証を要求して送信する前に、メッセージを準備します。

手順は、以下のとおりです。

1. **mta** は適格なメッセージを選択し、使用可能な **mtachild** を割り当てます。
1. **mtachild** は、メッセージの作成に必要なすべての情報（コンテンツ、パーソナライゼーション要素、添付ファイル、画像など）を読み込み、メッセージを **メールトラフィックシェーパー** に転送します。
1. メールトラフィックシェーパーが統計サーバーの認証（**smtp stat**）を受信するとすぐに、メッセージが受信者に送信されます。

![](assets/s_ncs_install_email_traffic_shaper.png)

### メールサーバーの統計と制限 {#email-server-statistics-and-limitations}

統計サーバーは、メッセージを受信するメールサーバーごとに、次の統計を保持します。

* 開いているポイント・イン・タイム接続の数
* 過去 1 時間に送信されたメッセージの数、
* 接続の成功率/拒否率、
* 到達不能なサーバーへの接続率。

同時に、モジュールは特定のメールサーバーの制限事項のリストを読み込みます。

* 同時接続の最大数
* 1 時間あたりの最大メッセージ数、
* 接続ごとの最大メッセージ数。

### IP アドレスの管理 {#managing-ip-addresses}

統計サーバーは、複数のインスタンスまたは同じパブリック IP アドレスを持つ複数のマシンを組み合わせることができます。 したがって、特定のインスタンスにリンクされていませんが、ドメインごとの制限を復元するには、インスタンスに問い合わせる必要があります。

配信統計は、ターゲット MX ごと、およびソース IP ごとに保持されます。 例えば、ターゲットドメインの MX が 5 で、プラットフォームが 3 つの異なる IP アドレスを使用できる場合、サーバーはこのドメインに対して最大 15 系列の指標を管理できます。

送信元の IP アドレスは、パブリック IP アドレス、つまり、リモート E メール サーバーによって認識されるアドレスと一致します。 NAT ルータが提供されている場合、この IP アドレスは **mta** をホストするマシンのアドレスとは異なる場合があります。 そのため、統計サーバーはパブリック IP （**publicId**）に一致する識別子を使用します。 ローカルアドレスとこの識別子の間の関連付けは、**serverConf.xml** 設定ファイルで宣言されます。 **serverConf.xml** で使用可能なすべてのパラメーターは、この [ セクション ](../../installation/using/the-server-configuration-file.md) に一覧表示されます。

## 配信出力制御 {#delivery-output-controlling}

メールサーバーにメッセージを配信するには、**メールトラフィックシェーパー** コンポーネントで、統計サーバーからの接続をリクエストします。 リクエストが承認されると、接続が開きます。

メッセージを送信する前に、モジュールはサーバーから「トークン」をリクエストします。 これらは通常、10 個以上のトークンのセットで、サーバーへのクエリの数を減らします。

サーバーは、接続と配信に関連するすべての統計を保存します。 再起動すると、情報が一時的に失われます。各クライアントは送信統計情報のローカル・コピーを保持し、定期的に（2 分ごとに）サーバに返します。 その後、サーバーはデータを再集計する場合があります。

次の節では、**メールトラフィックシェーパー** コンポーネントによるメッセージの処理について説明します。

### メッセージ配信 {#message-delivery}

メッセージが送信された場合、次の 3 つの結果が考えられます。

1. **成功**：メッセージは正常に送信されました。 メッセージが更新されます。
1. **メッセージ失敗**：接続されたサーバーは、選択された受信者のメッセージを拒否しました。 この結果はリターン コード 550 ～ 599 と一致しますが、例外は定義できます。
1. **セッション失敗** （5.11 以上）:**mta** がこのメッセージに対する回答を受け取った場合、メッセージは破棄されます（[ メッセージの放棄 ](#message-abandonment) を参照）。 メッセージは別のパスに送信されるか、他のパスが使用できない場合は保留に設定されます（[ メッセージ保留 ](#message-pending) を参照）。

   >[!NOTE]
   >
   >**path** は、Adobe Campaign **mta** とターゲット **mta** の間の接続です。 Adobe Campaign **mta** は、複数の開始 IP および複数のターゲットドメイン IP から選択できます。

### メッセージの放棄 {#message-abandonment}

破棄されたメッセージは **mta** に返され、**mtachild** では管理されなくなります。

**mta** は、応答コードとルールに応じて、このメッセージの手順（回復、放棄、強制隔離など）を決定します。

### メッセージを保留中 {#message-pending}

アクティブなキューに届き、使用可能なパスがない場合、メッセージは保留されます。

通常、パスは、接続エラー後に一定の時間、使用できないものとしてマークされます。 使用不能期間は、エラーの頻度と年齢によって異なります。

## 統計サーバーの設定 {#statistics-server-configuration}

統計サーバーは、複数のインスタンスで使用できます。使用するインスタンスとは別に設定する必要があります。

まず、設定をホストするAdobe Campaign データベースを定義します。

### 設定を開始 {#start-configuration}

デフォルトでは、**stat** モジュールは各インスタンスに対して起動されます。 インスタンスが同じマシン上でプールされる場合、またはインスタンスが同じ IP アドレスを共有する場合は、1 つの統計サーバーが使用され、それ以外は無効にする必要があります。

### サーバーポートの定義 {#definition-of-the-server-port}

デフォルトでは、統計サーバーはポート 7777 でリッスンします。 このポートは、**serverConf.xml** ファイルで変更できます。 **serverConf.xml** で使用可能なすべてのパラメーターは、この [ セクション ](../../installation/using/the-server-configuration-file.md) に一覧表示されます。

```
<stat port="1234"/>
```

## MX 設定 {#mx-configuration}

>[!IMPORTANT]
>
>ホストインストールまたはハイブリッドインストールで [Enhanced MTA](../../delivery/using/sending-with-enhanced-mta.md) にアップグレードした場合、**[!UICONTROL MX 管理]**&#x200B;配信スループットは使用されなくなります。Enhanced MTA は独自の MX ルールを使用します。これにより、独自のメールレピュテーション履歴およびメールを送信しているドメインから送信されるリアルタイムのフィードバックに基づいて、スループットをドメインごとにカスタマイズすることができます。

### MX ルールについて {#about-mx-rules}

>[!NOTE]
>
>この節と以下の節は、従来の Campaign MTA を使用したオンプレミスインストールとホスト/ハイブリッドインストールにのみ適用されます。

MX（Mail eXchanger）ルールは、送信サーバーと受信サーバーの間の通信を管理するルールです。

これらのルールは、クライアントインスタンスを定期的に提供するために、毎日午前 6 時（サーバー時間）に自動的に再読み込みされます。

材料容量と内部ポリシーに応じて、ISP は 1 時間あたりの事前定義済みの接続数とメッセージ数を受け入れます。 これらの変数は、IP および送信ドメインの評判に応じて、ISP システムによって自動的に変更される場合があります。 Adobe Campaign では、配信品質プラットフォームを通じて、ISP 別の 150 個以上の専用ルールに加えて、他のドメイン用の 1 つの汎用ルールを管理します。

接続の最大数は、MTA で使用されるパブリック IP アドレスの数だけに依存しているわけではありません。

例えば、MX ルールで 5 つの接続を許可していて、2 つのパブリック IP を設定している場合、このドメインに対して同時に開かれる接続は 10 個を超えることはできません。 しかし、そうではありません。接続の最大数は、実際には、MTA のパブリック IP の 1 つとクライアントの MTA のパブリック IP の組み合わせであるパスを示します。

以下の例では、ユーザーに 2 つのパブリック IP アドレスが設定されており、ドメインは yahoo.com です。

```
user:~ user$ host -t mx yahoo.com
                yahoo.com mail is handled by 1 mta5.am0.yahoodns.net.
                yahoo.com mail is handled by 1 mta6.am0.yahoodns.net.
                yahoo.com mail is handled by 1 mta7.am0.yahoodns.net.
```

yahoo.comの MX レコードは、yahoo.comに 3 つの Mail Exchanger があることを示しています。 ピア Mail Exchanger に接続するには、MTA がその IP アドレスを DNS に要求します。

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

このレコードの場合、ユーザーは 8 つのピア IP アドレスに接続できます。 ユーザは 2 つのパブリック IP アドレスを持っているので、yahoo.com メールサーバに到達するための 8 * 2 = 16 の組み合わせを提供します。 これらの組み合わせはそれぞれパスと呼ばれます。

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

これら 8 つの IP アドレスのうち 4 つは、既に mta5 で使用されています（98.136.216.26、98.138.112.38、63.250.192.46、98.136.217.203）。 このレコードを使用すると、ユーザーは 4 つの新しい IP アドレスを使用できます。 3 つ目の MX レコードも同様です。

合計 16 個のリモート IP アドレスがあります。 2 つのローカルパブリック IP アドレスと組み合わせると、yahoo.com のメールサーバーに到達するのに 32 個のパスがあります。

>[!NOTE]
>
>2 つの MX レコードが同じ IP アドレスを参照している場合は、これらは 2 つのパスではなく 1 つのパスとみなされます。

MX ルールを使用する例を以下にいくつか示します。

![](assets/s_ncs_examples_mx_rules.png)

以下の例では、特定のドメインに対して 1 時間あたりのメッセージ数の上限が 10,000 件になっていますが、MTA のスループット能力はこの上限を上回っています。

この場合、トラフィックは 1 時間ごとに 5 分間の 12 周期に分割され、メッセージ数の実際の上限は 1 周期につき 833 件になります。

これらのメッセージはできるだけ速く配信されます。

![](assets/s_ncs_traffic_shaping.png)

### MX 管理の設定 {#configuring-mx-management}

MX について準拠するルールは、ツリーの **[!UICONTROL 管理/キャンペーン管理/配信不能件数の管理/メール ルールセット]** ノードの **[!UICONTROL MX 管理]** ドキュメントで定義されます。

**[!UICONTROL MX 管理]** ドキュメントがノードに存在しない場合は、手動で作成できます。 手順は次のとおりです。

1. 新しいメール ルールのセットを作成します。
1. **[!UICONTROL MX 管理]** モードを選択します。

   ![](assets/s_ncs_install_mx_mgt_rule.png)

1. **内部名** フィールドに **[!UICONTROL defaultMXRules]** と入力します。

変更を反映するには、統計サーバーを再起動する必要があります。

統計サーバーを再起動せずに設定をリロードするには、サーバーをホストしているマシンで次のコマンドを使用します：`nlserver stat -reload`

>[!NOTE]
>
>このコマンドラインは、**nlserver restart** よりも推奨されます。 再起動するまでに収集された統計データが失われることもなく、また、使用時のピークが MX ルールで定義された割り当てに違反するおそれもなくなります。

### MX ルールの設定 {#configuring-mx-rules}

**[!UICONTROL MX 管理]** ドキュメントには、MX ルールにリンクされているすべてのドメインが一覧表示されます。

これらのルールは順番に適用されます。MX マスクがターゲットの MX と互換性がある最初のルールが適用されます。

各ルールで使用できるパラメーターは次のとおりです。

* **[!UICONTROL MX マスク]**：ルールが適用されるドメイン。 各ルールは、MX のアドレスマスクを定義します。 したがって、このマスクと名前が一致する MX が適格となります。 マスクには、「&#42;」と「?」を含めることができます 汎用文字。

  例えば、次のアドレスです。

   * a.mx.yahoo.com
   * b.mx.yahoo.com
   * c.mx.yahoo.com

  は、次のマスクと互換性があります。

   * &#42;.yahoo.com
   * ?.mx.yahoo.com

  例えば、E メールアドレス foobar@gmail.com の場合、ドメインは gmail.com で、MX レコードは次のようになります。

  ```
  gmail.com mail exchanger = 20 alt2.gmail-smtp-in.l.google.com.
  gmail.com mail exchanger = 10 alt1.gmail-smtp-in.l.google.com.
  gmail.com mail exchanger = 40 alt4.gmail-smtp-in.l.google.com.
  gmail.com mail exchanger = 5  gmail-smtp-in.l.google.com.
  gmail.com mail exchanger = 30 alt3.gmail-smtp-in.l.google.com.
  ```

  この場合、MX ルール `*.google.com` が使用されます。 このように、MX ルールマスクは必ずしもメールのドメインと一致しません。 gmail.com メールアドレスに適用される MX ルールは、マスク `*.google.com` が付いたルールになります。

* **[!UICONTROL 識別子の範囲]**：このオプションを使用すると、ルールが適用される識別子の範囲（publicID）を指定できます。 以下を指定できます。

   * A 数字：ルールはこの publicId にのみ適用されます。
   * 数値の範囲（**number1-number2**）：ルールは、これら 2 つの数値間のすべての publicIds に適用されます。

  >[!NOTE]
  >
  >フィールドが空の場合、ルールはすべての識別子に適用されます。

  パブリック ID は、1 つ以上の MTA で使用されるパブリック IP の内部識別子です。 これらの ID は MTA サーバーの **config-instance.xml** ファイルに定義されます。

  ![](assets/s_ncs_install_mta_ips.png)

* **[!UICONTROL 共有]**：この MX ルールのプロパティの範囲を定義します。 オンにすると、すべてのパラメーターがインスタンスで使用可能なすべての IP で共有されます。 オフにすると、IP ごとに MX ルールが定義されます。 メッセージの最大数は、使用可能な IP アドレスの数を乗算したものになります。
* **[!UICONTROL 最大接続数]**：送信者のドメインへの同時接続の最大数。
* **[!UICONTROL メッセージの最大数]**:1 つの接続で送信できるメッセージの最大数。 メッセージがこの数を超えると、接続が閉じられ、新しい接続が開かれます。
* **[!UICONTROL 1 時間あたりのメッセージ数]**：送信者のドメインに 1 時間で送信できるメッセージの最大数。
* **[!UICONTROL 接続タイムアウト]**：ドメインに接続する時間のしきい値。

  >[!NOTE]
  >
  >Windows は、Windows のバージョンに応じて、このしきい値の前に **タイムアウト** を発行できます。

* **[!UICONTROL タイムアウトデータ]**：メッセージコンテンツを送信してから最大待機時間（SMTP プロトコルの DATA セクション）。
* **[!UICONTROL タイムアウト]**:SMTP サーバーとの他の交換の最大待機時間。
* **[!UICONTROL TLS]**：メール配信を暗号化できる TLS プロトコルを選択的に有効にできます。 各 MX マスクに対して、次のオプションを使用できます。

   * **[!UICONTROL デフォルト設定]**：これは、適用される serverConf.xml 設定ファイルで指定された一般設定です。

     >[!IMPORTANT]
     >
     >デフォルトの設定は変更しないことをお勧めします。

   * **[!UICONTROL 無効]**：メッセージは、暗号化なしでシステム的に送信されます。
   * **[!UICONTROL 便宜的]**：受信サーバー（SMTP）が TLS プロトコルを生成できる場合、メッセージ配信は暗号化されます。

設定例：

![](assets/s_ncs_install_mx_mgt_rule_details.png)

>[!NOTE]
>
>Adobe Campaignでの MX サーバーの使用について詳しくは、[ この節 ](../../installation/using/using-mx-servers.md) を参照してください。

### E メールフォーマットの管理 {#managing-email-formats}

送信するメッセージの形式を定義して、各受信者のアドレスのドメインに合わせて自動的にコンテンツが表示されるように設定できます。

これを行うには、**[!UICONTROL 管理]**/**[!UICONTROL キャンペーン管理]**/**[!UICONTROL 配信不能件数の管理]**/**[!UICONTROL メールルールセット]** にある **[!UICONTROL メール形式の管理]** ドキュメントに移動します。

このドキュメントには、Adobe Campaignが管理する日本語フォーマットに対応する、事前に定義されたドメインのリストが含まれています。 詳しくは、[Campaign v8 ドキュメント](https://experienceleague.adobe.com/docs/campaign/campaign-v8/send/emails/sending-emails-on-japanese-mobiles.html?lang=ja){target="_blank"}を参照してください。

![](assets/mail_rule_sets.png)

**MIME 構造** （Multipurpose Internet Mail Extensions） パラメーターを使用すると、様々なメールクライアントに送信されるメッセージ構造を定義できます。 次の 3 つのオプションを使用できます。

* **マルチパート**：メッセージは、テキストまたはHTML形式で送信されます。 HTMLが許可されていない場合でも、メッセージはテキストフォーマットで表示できます。

  デフォルトでは、マルチパート構造は **multipart/alternative** ですが、画像がメッセージに追加されると、自動的に **multipart/related** になります。 一部のプロバイダーは、デフォルトで **multipart/related** 形式を想定しています。**[!UICONTROL multipart/related を強制]** オプションは、画像が添付されていない場合でもこの形式を強制します。

* **HTML**: HTMLのみのメッセージが送信されます。 HTML形式が許可されない場合、メッセージは表示されません。
* **テキスト**：テキスト形式のメッセージのみが送信されます。 テキストフォーマットのメッセージの利点は、サイズが非常に小さいことです。

「**[!UICONTROL 画像を含める]**」オプションが有効になっている場合は、メールの本文に直接表示されます。 その後、画像がアップロードされ、URL リンクがコンテンツに置き換えられます。

このオプションは、特に日本市場で **デコメール**、**デコレメール** または **デコレーションメール** に使用されます。 詳しくは、[Campaign v8 ドキュメント ](https://experienceleague.adobe.com/docs/campaign/campaign-v8/send/emails/sending-emails-on-japanese-mobiles.html?lang=ja){target="_blank"} を参照してください。

>[!IMPORTANT]
>
>E メールに画像を挿入すると、サイズが大幅に増加します。

## 配信サーバーの設定 {#delivery-server-configuration}

### クロック同期 {#clock-synchronization}

Adobe Campaign プラットフォーム（データベースを含む）を構成するすべてのサーバーのクロックを同期し、それらのシステムを同じタイムゾーンに設定する必要があります。

### 統計サーバーの座標 {#coordinates-of-the-statistics-server}

統計サーバーのアドレスは、**mta** で指定する必要があります。

設定の **mta** 要素の **statServerAddress** プロパティを使用すると、使用するポートのアドレスと番号を指定できます。

```
<mta statServerAddress="emailStatServer:7777">
   [...]
 </mta>
```

統計サーバーを同じマシンで使用するには、少なくともマシンの名前に **localhost** 値を入力する必要があります。

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

* **address**：使用する MTA ホストマシンの IP アドレスです。
* **heloHost**：この識別子は、SMTP サーバーで表示される IP アドレスを表します。

* **publicId**：この情報は、IP アドレスが NAT ルータの背後で複数のAdobe Campaign **mtas** によって共有されている場合に役立ちます。 統計サーバーはこの識別子を使用して、この開始点とターゲットサーバーの間の接続および送信統計を記憶します。
* **重み付け**：アドレスの相対的な使用頻度を定義できます。 デフォルトでは、すべてのアドレスの重み付けは 1 に等しくなります。

>[!NOTE]
>
>serverConf.xml ファイルで、1 つの IP が一意の識別子（public_id）を持つ 1 つの helohost に対応していることを確認する必要があります。 複数の helohost にマッピングすることはできず、結果として配信スロットルの問題が発生する可能性があります。

前の例では、通常の条件では、アドレスは次のように配布されます。

    * &quot;1&quot;: 5 / （5+5+1） = 45%
    * &quot;2&quot;: 5 / （5+5+1） = 45%
    * &quot;3&quot;: 1 / （5+5+1） = 10%

例えば、特定の MX に対して最初のアドレスを使用できない場合、メッセージは次のように送信されます。

    * &quot;2&quot;: 5 / （5+1） = 83%
    * &quot;3&quot;: 1 / （5+1） = 17%

* **includeDomains**：特定のドメインに属するメールのこの IP アドレスを予約できます。 これは、1 つ以上のワイルドカード （&#39;&#42;&#39;）を含むことができるマスクのリストです。 属性が指定されていない場合、すべてのドメインがこの IP アドレスを使用できます。

  例：**includeDomains=&quot;wanadoo.com,orange.com,yahoo.&#42;&quot;**

* **excludeDomains**：この IP アドレスのドメインのリストを除外します。 このフィルターは、**includeDomains** フィルターの後に適用されます。

  ![](assets/s_ncs_install_mta_ips.png)

## メール送信の最適化 {#email-sending-optimization}

Adobe Campaign **mta** の内部アーキテクチャは、メール配信の設定に影響を与えます。 配信を改善するためのヒントを以下に示します。

### maxWaitingMessages パラメーターの調整 {#adjust-the-maxwaitingmessages-parameter}

**maxWaitingMessages** パラメーターは、**mtachild** によって事前に準備されたメッセージの最大数を示します。 メッセージはこのリストから削除されるのは、送信または破棄された後のみです。

このパラメーターは非常に重要で、メッセージがドメインで並べ替えられない場合に特に重要です。

**maxWorkingSetMb** （256）しきい値に達すると、配信サーバーはメッセージの送信を停止します。 **mtachild** が再び起動するまで、パフォーマンスは大幅に低下します。 この問題を回避するには、**maxWorkingSetMb** パラメーターのしきい値を大きくするか、**maxWaitingMessages** パラメーターのしきい値を小さくします。

**maxWorkingSetMb** パラメーターは、メッセージの最大数に平均メッセージサイズを乗算し、その結果に 2.5 を乗算することで、経験的に計算されます。例えば、メッセージの平均サイズが 50 kB で **maxWaitingMessages** パラメーターが 1,000 に等しい場合、使用されるメモリは平均 125 MB になります。

### mtachild の数の調整 {#adjust-the-number-of-mtachild}

子供の数は、マシン内のプロセッサの数を超えてはいけません（約 1,000 セッション）。 8 **mtachild** を超えないようにすることをお勧めします。 その後、**child** （**maxMsgPerChild**）あたりのメッセージ数を増やして、十分な寿命を得ることができます。
