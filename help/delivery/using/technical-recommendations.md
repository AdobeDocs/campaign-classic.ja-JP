---
title: Adobe Campaign Classic で配信品質を向上させるための技術的な推奨事項
description: Adobe Campaign Classic を使用して配信品質を向上させるために使用できるテクニック、設定およびツールを紹介します。
page-status-flag: never-activated
uuid: 71be1087-e5ff-4a7a-85ca-36803839e72f
contentOwner: sauviat
products: SG_CAMPAIGN/CLASSIC
audience: delivery
content-type: reference
topic-tags: deliverability-management
discoiquuid: fc95538b-b54d-44ec-81aa-f51b62982699
index: y
internal: n
snippet: y
translation-type: ht
source-git-commit: 15581517df8d2f397285bbadebd83b7f4539dfd7
workflow-type: ht
source-wordcount: '2463'
ht-degree: 100%

---


# 技術的な推奨事項{#technical-recommendations}

配信品質を向上させるために使用できるテクニック、設定、ツールのいくつかを以下に示します。

## 設定 {#configuration}

### リバース DNS {#reverse-dns}

Adobe Campaign は、IP アドレスに対してリバース DNS が提供されているかどうか、そのリバース DNS が正しく IP を指しているかどうかを確認します。

ネットワーク設定で重要な点は、送信メッセージの IP アドレスごとに正しいリバース DNS が必ず定義されるようにすることです。つまり、特定の IP アドレスには、最初の IP アドレスにループバックする対応 DNS（A レコード）を記述したリバース DNS レコード（PTR レコード）があるということです。

特定の ISP を扱う場合には、リバース DNS のドメイン選択が影響を及ぼします。特に、AOL は、リバース DNS と同じドメインに属するアドレスのフィードバックループのみを受け付けます（[フィードバックループ](#feedback-loop)を参照）。

ドメインの設定を検証するツールがあります。[https://mxtoolbox.com/SuperTool.aspx](https://mxtoolbox.com/SuperTool.aspx) を参照してください。

### MX ルール {#mx-rules}

MX（Mail eXchanger）ルールは、送信サーバーと受信サーバーの間の通信を管理するルールです。

より正確に言うと、MX ルールは、Campaign MTA（メール転送エージェント）が E メールを個々の E メールドメインまたは ISP（例：hotmail.com、comcast.net）に送信する速度を制御するために使用されます。これらのルールは、通常、ISP によって公開された制限（例：各 SMTP 接続あたり 20 を超えるメッセージを含めない）に基づいています。

MX 管理について詳しくは、[この節](../../installation/using/email-deliverability.md#mx-configuration)を参照してください。

### TLS {#tls}

TLS（トランスポート層セキュリティ）は、暗号化プロトコルで、2 つの E メールサーバー間の接続を保護したり、E メールのコンテンツを保護して意図された受信者以外によって読まれないようにするために使用できます。

## 認証 {#authentication}

### SPF {#spf}

SPF（Sender Policy Framework）は、E メール認証標準で、ドメインの所有者がドメインの代わりに E メールを送信できる E メールサーバーを指定できます。この標準は、E メールの「Return-Path」ヘッダー（「Envelope From」アドレスとも呼ばれる）のドメインを使用します。

SPF レコードを検証するツールがあります。[https://www.kitterman.com/spf/validate.html](https://www.kitterman.com/spf/validate.html) を参照してください。

SPF は、E メールで使用されているドメイン名が偽装されていないことをある程度確認できる技術です。あるドメインからメッセージが受信されると、そのドメインの DNS サーバーに対して問い合わせが実行されます。その応答は、このドメインから E メールを送信する権限がどのサーバーにあるかを記述した短いレコード（SPF レコード）になります。このレコードを変更する手段がドメインの所有者にしかないと仮定すると、送信者のアドレス（少なくとも「@」の右側の部分）の偽装はこの技術により防止できると考えることができます。

最終版の [RFC 4408 仕様](https://www.rfc-editor.org/info/rfc4408)では、送信者とみなされるドメインを判断するのに、2 つのメッセージ要素、SMTP 「HELO」（または「EHLO」）コマンドで指定されたドメインおよび「Return-Path」（または「MAIL FROM」）ヘッダーのアドレスで指定されたドメインを使用します。後者は、バウンスアドレスでもあります。様々な事項を検討することにより、これらの値の一方のみを考慮に入れることが可能になります。両方のソースで指定されているドメインが必ず同じになるようにすることをお勧めします。

SPF の確認により、送信者ドメインの有効性が次のように評価されます。

* **None**：評価を実行できませんでした。
* **Neutral**：問い合わせられたドメインでは評価が有効になっていません。
* **Pass**：ドメインは真正なものとみなされます。
* **Fail**：ドメインは偽装されており、メッセージを拒否すべきです。
* **SoftFail**：ドメインはおそらく偽装されていますが、この結果だけからメッセージを拒否すべきではありません。
* **TempError**：一時的なエラーで評価が停止しました。メッセージを拒否してもかまいません。
* **PermError**：ドメインの SPF レコードが無効です。

DNS サーバーのレベルで作成されたレコードを考慮するのに最大 48 時間かかる可能性があることに注意する必要があります。この遅延は、受信サーバーの DNS キャッシュの更新頻度によって異なります。

### DKIM {#dkim}

DKIM（DomainKeys Identified Mail）認証は、SPF の後継で、公開鍵暗号化を使用します。受信 E メールサーバーは、送信したと主張する個人または法人によってメッセージが実際に送信されたか、およびメッセージコンテンツが最初に送信された（および DKIM が「署名された」）ときと受信時で変更されているかどうかを検証できます。この標準は、通常、「From」または「Sender」ヘッダーのドメインを使用します。DKIM のセキュリティレベルを確保するのに、ベストプラクティスとして推奨される暗号化サイズは 1024b です。これより小さいサイズの DKIM 鍵は、大多数のアクセスプロバイダーには有効とはみなされません。

DKIM は、Yahoo! の DomainKeys と Cisco の Identified Internet Mail という 2 つの送信ドメイン認証方式を組み合わせて策定されたもので、送信者ドメインの信憑性を確認し、メッセージの整合性を保証するために使用されます。

DKIM が **DomainKeys** 認証方式の後継となりました。

DKIM を使用するには、次のように、いくつかの前提条件を満たす必要があります。

* **セキュリティ**：暗号化が DKIM の重要な要素であり、2013 年春以降の DKIM のセキュリティレベルを保証するには、1024 ビットが、ベストプラクティスで推奨される暗号化サイズです。これより小さいサイズの DKIM 鍵は、大多数のアクセスプロバイダーには有効とはみなされません。
* **レピュテーション**：レピュテーションは IP やドメインに基づいたものですが、より透明性の低い DKIM セレクターも考慮に入れるべき重要な要素です。セレクターの選択は重要です。「default」のままにしないようにします。これは誰にでも使用できるものなので、レピュテーションは非常に弱くなります。**顧客維持／獲得用の通信**&#x200B;と認証には、別のセレクターを実装する必要があります。
* **Adobe Campaign オプションの宣言**：Adobe Campaign では、DKIM 秘密鍵は DKIM セレクターとドメインに基づきます。同じドメイン／サブドメインに対して、セレクターの異なる複数の秘密鍵を作成することは、現時点ではできません。プラットフォームでも E メールでも、どのセレクタードメイン／サブドメインを認証に使用すべきかを定義することはできません。プラットフォームでは、その代わりに、秘密鍵のいずれか 1 つを選択します。つまり、認証は失敗する可能性が高くなります。

>[!NOTE]
>
>* お使いの Adobe Campaign インスタンスに DomainKeys を設定してある場合は、[ドメイン管理ルール](../../delivery/using/understanding-delivery-failures.md#domain-management)で **dkim** を選択するだけです。そうでない場合は、DomainKeys の場合と同じ設定手順（秘密鍵／公開鍵）に従います。
>* DKIM は DomainKeys の改良版なので、同じドメインに DomainKeys と DKIM の両方を有効にする必要はありません。
>* 現在 DKIM が有効になっているドメインは、AOL および Gmail です。


>[!IMPORTANT]
>
>ホストインストールまたはハイブリッドインストールで [Enhanced MTA](https://helpx.adobe.com/jp/campaign/kb/acc-campaign-enhanced-mta.html) にアップグレードした場合、すべてのドメインのすべてのメッセージに対する DKIM の E メール認証署名は、Enhanced MTA がおこないます。

### DMARC {#dmarc}

DMARC（Domain-based Message Authentication, Reporting and Conformance）は、最新の E メール認証です。SPF と DKIM 認証の両方に基づいて E メールの合否を判定します。DMARC は以下の 2 つの点においてユニークで強力な認証方法です。

* 適合性 - 送信者は、認証に失敗したすべてのメッセージをどのように処理するか（「承諾しない」など）について ISP に指示できます。
* レポート - DMARC 認証に失敗したすべてのメッセージを、それぞれに使用された「From」ドメインおよび IP アドレスと共に詳細なレポートを送信者に提供します。これにより、認証に失敗し、ある種の「修正」（IP アドレスの SPF レコードへの追加など）が必要な正当な E メールを、その E メールドメインのフィッシング攻撃のソースおよび横行率と共に識別できます。

DMARC は、[250ok](https://250ok.com/) が生成したレポートを活用できます。

<!--#### Configuring the application {#configuring-the-application}

To define the domain used for the HELO command, edit the instance's configuration file (conf/config-instance.xml) and define a "localDomain" attribute as follows:

```
<serverConf>
  <shared>
    <dnsConfig localDomain="mydomain.net"/>
  </shared>
</serverConf>
```

The MAIL FROM domain is the domain used in technical bounce messages. This address is defined in the deployment wizard or via the NmsEmail_DefaultErrorAddr option.

#### DNS configuration {#dns-configuration}

An SPF record can currently be defined on a DNS server as a TXT type record (code 16) or an SPF type record (code 99). An SPF record takes the form of a character string. For example:

```
v=spf1 ip4:12.34.56.78/32 ip4:12.34.56.79/32 ~all
```

defines the 2 IP addresses 12.34.56.78 and 12.34.56.79 as authorized to send emails for the domain. **~all** means that any other address should be interpreted as a SoftFail.

Recommendations for defining an SPF record:

* Add **~all** (SoftFail) or **-all** (Fail) at the end to reject all servers other than those defined. Without this, servers will be able to forge this domain (with a Neutral evaluation).
* Do not add **ptr** (openspf.org recommends against this as costly and unreliable).-->

## フィードバックループ {#feedback-loop}

メッセージの送信に使用される IP アドレスの範囲に対して、特定の E メールアドレスを ISP レベルで宣言することにより、フィードバックループが機能します。ISP では、受信者からスパムとして報告されたメッセージを、バウンスメッセージの場合と同様の方法で、このメールボックスに送信します。苦情を訴えたユーザーへの今後の配信をブロックするように、プラットフォームを設定する必要があります。これらのユーザーが正しいオプトアウトリンクを使用しなかったとしても、そうしたユーザーにはもう連絡しないことが重要です。ISP では、このような苦情に基づいて、IP アドレスをブラックリストに載せます。ISP によっては、苦情率がおよそ 1％になると、IP アドレスがブラックリストに載ります。

フィードバックループメッセージの形式を定義する標準 [Abuse Feedback Reporting Format（ARF）](https://tools.ietf.org/html/rfc6650)が現在策定中です。

インスタンスのフィードバックループを実装するには、次が必要です。

* 対象インスタンス専用のメールボックス（バウンスメールボックスとなる場合があります）
* 対象インスタンス専用の IP 送信アドレス

Adobe Campaign でシンプルなフィードバックループを実装する場合は、バウンスメッセージ機能が使用されます。フィードバックループメールボックスは、バウンスメールボックスとして使用され、これらのメッセージを検出するためのルールが定義されます。メッセージをスパムとして報告した受信者の E メールアドレスは、強制隔離リストに追加されます。

* **[!UICONTROL 管理／キャンペーン管理／配信不能件数の管理／メールルールセット]**&#x200B;で、理由として「**拒否**」、タイプとして「**ハード**」を指定してバウンスメールルール **Feedback_loop** を作成または変更します。
* メールボックスが特にフィードバックループ用に定義されている場合は、**[!UICONTROL 管理／プラットフォーム／外部アカウント]**&#x200B;で新しい外部バウンスメールアカウントを作成することにより、メールボックスにアクセスするためのパラメーターを定義します。

苦情の通知を処理するメカニズムが直ちに有効になります。このルールが正しく機能していることを確認するには、これらのメッセージが収集されないようにアカウントを一時的に無効にした後、フィードバックループメールボックスの内容を手動で確認します。サーバー上で、次のコマンドを順に実行します。

```
nlserver stop inMail@instance,
nlserver inMail -instance:instance -verbose.
```

複数のインスタンスに単一のフィードバックループアドレスを使用せざるを得ない場合は、次をおこなう必要があります。

* 受信したメッセージをインスタンスと同数のメールボックス上に複製します。
* インスタンスごとに各メールボックスが選択されるようにします。
* 関係するメッセージだけを処理するようにインスタンスを設定します。インスタンス情報は、Adobe Campaign から送信されるメッセージの Message-ID ヘッダーに含まれているので、フィードバックループメッセージにも含まれています。インスタンス設定ファイルの **checkInstanceName** パラメーターを指定するだけです（デフォルトでは、インスタンスは検証されず、その結果、特定のアドレスが誤って強制隔離される可能性があります）。

   ```
   <serverConf>
     <inMail checkInstanceName="true"/>
   </serverConf>
   ```

Adobe Campaign の配信品質サービスは、以下の ISP のフィードバックループサービスへのサブスクリプションを管理します。AOL、BlueTie、Comcast、Cox、EarthLink、FastMail、Gmail、Hotmail、HostedEmail、Libero、Mail.ru、MailTrust、OpenSRS、QQ、RoadRunner、Synacor、Telenor、Terra、UnitedOnline、USA、XS4ALL、Yahoo、Yandex、Zoho。

## List-Unsubscribe {#list-unsubscribe}

### List-Unsubscribe について {#about-list-unsubscribe}

配信品質の最適な管理を実現するには、**List-Unsubscribe** という SMTP ヘッダーを付けることが不可欠です。

このヘッダーは、「スパムとして報告」アイコンの代わりに使用できます。これを付けると、E メールインターフェイスに購読解除リンクが表示されます。

この機能を使用すると、評判を守ることができ、フィードバックは購読解除として実行されます。

>[!NOTE]
>
>この機能はビルド 6831 から使用できます。

List-Unsubscribe を使用するには、次のようなコマンドラインを入力する必要があります。

```
List-Unsubscribe: mailto: client@newsletter.example.com?subject=unsubscribe?body=unsubscribe
```

>[!IMPORTANT]
>
>上記の例は受信者テーブルに基づいています。データベースの実装が別のテーブルに基づいておこなわれている場合は、正しい情報を反映するようにコマンドラインを修正する必要があります。

次のコマンドラインは、動的な **List-Unsubscribe** の作成に使用できます。

```
List-Unsubscribe: mailto: %=errorAddress%?subject=unsubscribe%=message.mimeMessageId%
```

Gmail、Outlook.com および Microsoft Outlook はこの手法をサポートしており、それぞれのインターフェイスで直接、購読解除ボタンを使用できます。この手法を利用すると、苦情率が下がります。

![](assets/s_tn_del_msn_unsubscribe_list.png)

![](assets/s_tn_del_gmail_unsubscribe_list.png)

**List-Unsubscribe** は、次のいずれかの方法で実装できます。

* 配信テンプレートにコマンドラインを直接追加する（[この節](#adding-a-command-line-in-a-delivery-template)を参照）。
* タイポロジルールを作成する（[この節](#creating-a-typology-rule)を参照）。

### 配信テンプレートへのコマンドラインの追加 {#adding-a-command-line-in-a-delivery-template}

コマンドラインは、E メールの SMTP ヘッダーの追加セクションに追加する必要があります。

この追加は E メールごとにおこなうこともできますし、既存の配信テンプレートでおこなうこともできます。また、この機能を組み込んだ配信テンプレートを新しく作成することもできます。

### タイポロジルールの作成 {#creating-a-typology-rule}

ルールには、コマンドラインを生成するスクリプトが含まれている必要があり、このルールを E メールヘッダーに組み込む必要があります。

>[!NOTE]
>
>タイポロジルールを作成することをお勧めします。各 E メールに List-Unsubscribe 機能が自動的に追加されます。

1. List-Unsubscribe: &lt;mailto:unsubscribe@domain.com>

   ユーザーが&#x200B;**購読解除**&#x200B;リンクをクリックすると、デフォルトの E メールクライアントが開きます。このタイポロジルールは、E メールの作成に使用されるタイポロジに追加する必要があります。

1. List-Unsubscribe: `<https://domain.com/unsubscribe.jsp>`

   ユーザーが&#x200B;**購読解除**&#x200B;リンクをクリックすると、購読解除フォームにリダイレクトされます。

   例：

   ![](assets/s_tn_del_unsubscribe_param.png)

## E メールの最適化 {#email-optimization}

### SMTP {#smtp}

SMTP（Simple Mail Transfer Protoco）は、E メール送信のインターネット標準です。

ルールでチェックされない SMTP エラーは、**[!UICONTROL 管理]**／**[!UICONTROL キャンペーン管理]**／**[!UICONTROL 配信不能件数の管理]**／**[!UICONTROL 配信ログの検証]**&#x200B;フォルダーにリスト表示されます。これらのエラーメッセージは、デフォルトでは、到達不能なソフトエラーと解釈されます。SMTP サーバーからのフィードバックを正しく検証する場合は、最もよく起こるエラーを特定し、それに対応するルールを&#x200B;**[!UICONTROL 管理]**／**[!UICONTROL キャンペーン管理]**／**[!UICONTROL 配信不能件数の管理]**／**[!UICONTROL メールルールセット]**&#x200B;に追加する必要があります。これをおこなわないと、プラットフォームは不要な再試行を実行したり（不明ユーザーの場合）、一定回数のテストの後に特定の受信者を誤って強制隔離したりすることになります。

### 専用の IP {#dedicated-ips}

アドビは、高いレピュテーションを得て配信パフォーマンスを最適化するために、ランプアップ IP を持つ各顧客に専用の IP 戦略を提供します。

## IP 証明書 {#ip-certification}

IP 証明書は、スパム対策フィルターや他の E メールブロックシステムによってブロックされることなく、E メールが確実に受信されるようにする、ホワイトリストおよび送信プラクティスのプログラムです。

現在、2 社のプロバイダーが IP 証明書を提供しています。Return Path および Certified Senders Alliance です。

認証された送信者は、世界のメールボックスプロバイダーや E メールセキュリティ会社が使用する E メールホワイトリストに追加されます。こうした商用ホワイトリストは、送信者がスパム対策フィルターを完全にバイパスするシステムや、システムに入ると増加するポイントが割り当てられるシステムに基づいています。

[Return Path Certification](https://www.validity.com/products/returnpath/certification/) プログラムには、次のような多くの利点があります。

* Microsoft、AOL、Yahoo、Gmail、Comcast、Orange、Mail.ru など、大手メールボックスプロバイダーにおける受信ボックスへの配置率が大幅に向上
* Cloudmark、SpamAssassin および Cisco Ironport など、重要なフィルターでの有利な評判と扱い
* 24 時間 365 日の監視をおこなう専門のコンプライアンスチームが、セキュリティアラートを提供し、あらゆるセキュリティ侵害の解決のために協力
* KPI、配置および証明書パフォーマンスに関する詳細情報を提供する、メールボックスプロバイダーのデータ
* 新しい IP アドレスへの移行または取得の際の評判と認知度の強化を含む、シンプルで高速な IP ウォームアップ

[Certified Senders Alliance](https://certified-senders.org/certification-process/) 証明書には、以下のような利点があります。

* 高品質な基準に準拠できる商用 E メール送信者の認証
* 商用 E メールの配信と配信品質を改善し、受信ボックスへの配置率を上げ、スパム対策フィルターにかかる割合を削減
* 法的基準に完全に準拠して、法的リスクや経済的リスクから保護
* CSA Complaints Office からの早期警告および毎日のスパムトラップレポートにより、評判を保護

ISP は、これらのサービスを自由に使用するので、ISP の数はホワイトリストによって異なる可能性があります。

ただし、メッセージコンテンツの分析よりも受信ボックス所有者の行動に基づいてスパム対策フィルターを構築する ISP が増えているため、IP 証明書を使用すれば受信ボックスへ配置や配信が保証されるわけではありません。
