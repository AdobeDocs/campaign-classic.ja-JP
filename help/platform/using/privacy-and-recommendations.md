---
title: プライバシーと推奨事項
seo-title: プライバシーと推奨事項
description: プライバシーと推奨事項
seo-description: null
page-status-flag: never-activated
uuid: a044bbea-521d-4c1e-8aab-7d51a87fc94b
contentOwner: sauviat
products: SG_CAMPAIGN/CLASSIC
audience: platform
content-type: reference
topic-tags: starting-with-adobe-campaign
discoiquuid: 14369acf-9149-4649-947a-c16289e35eb6
translation-type: tm+mt
source-git-commit: 247d73933991047603b8d61c7489d976c448dd52
workflow-type: tm+mt
source-wordcount: '1804'
ht-degree: 92%

---


# プライバシーと同意{#privacy-and-recommendations}

## 一般的な推奨事項 {#general-recommendations}

Adobe Campaign は、個人情報や機密データを含む膨大な量のデータを収集および処理するための強力なツールです。そのため、プライバシー管理は慎重におこなう必要があります。

* 常に、個人情報を責任を持って倫理的に使用してください。

* 迷惑メール／プッシュ通知／SMS メッセージ（「スパム」）を送信しないでください。アドビは、顧客の生涯価値およびロイヤリティを促進するうえで許可型マーケティングの原則を重要視しています。したがって、未承諾メッセージの送信に Adobe Campaign を使用することを固く禁止しています。

ここで、[セキュリティとプライバシーチェックリスト](https://helpx.adobe.com/jp/campaign/kb/acc-security.html)を参照して、セキュリティとプライバシーに関してチェックすべき重要な要素を確認します。

### プライバシー規制 {#privacy-regulations}

プライバシーを正しく処理し、個人データを管理するには、事業をおこなう地域に適用される法律の範囲内で作業してください。次の規則が含まれます。
* [GDPR](https://ec.europa.eu/info/law/law-topic/data-protection/reform/what-does-general-data-protection-regulation-gdpr-govern_en)（ヨーロッパの一般データ保護規則）
* [DPA](https://www.gov.uk/data-protection)（英国実施の GDPR）
* [プライバシーと電子通信に関する欧州指令](https://eur-lex.europa.eu/legal-content/EN/TXT/?uri=CELEX:02002L0058-20091219)
* [CAN-SPAM 法](https://www.ftc.gov/tips-advice/business-center/guidance/can-spam-act-compliance-guide-business)（商用 E メールのルールと要件を設定する米国の法律）
* [CCPA](https://leginfo.legislature.ca.gov/faces/codes_displayText.xhtml?lawCode=CIV&amp;division=3.&amp;title=1.81.5.&amp;part=4.&amp;chapter=&amp;article=)（カリフォルニア州消費者プライバシー法）
* [PDPA](https://secureprivacy.ai/thailand-pdpa-summary-what-businesses-need-to-know/)（タイ個人データ保護法）
* [LGPD](https://iapp.org/media/pdf/resource_center/Brazilian_General_Data_Protection_Law.pdf)（ブラジルの一般データ保護法 - 2020 年 8 月 16 日施行）

>[!NOTE]
>
>GDPR、CCPA、PDPA、LGPD が Adobe Campaign にどのように適用されるかについては、[このページ](https://helpx.adobe.com/jp/campaign/kb/campaign-privacy-overview.html#whatisgdpr)を参照してください。

### Adobe Experience Cloud プライバシー {#experience-cloud-privacy}

Adobe Campaign は、Adobe Experience Cloud ソリューションの一部です。Campaign でのプライバシーの扱い方は、次のような Experience Cloud の一般原則に従います。

* **Adobe Experience Cloud を使用する際に収集される情報**

   Adobe Experience Cloud ソリューションを使用する会社は、収集して Adobe Experience Cloud アカウントに送信する情報を選択します。収集される情報のタイプの例としては、Web 閲覧アクティビティ、IP アドレス、モバイルデバイスからの位置情報、キャンペーン成功率、購入品目、買い物かごに入れた品目などがあります。

   >[!NOTE]
   >
   >すべてのアドビ製品について、Campaign はアプリと Web サイトのユーザーに関する情報を収集します。詳しくは、[アドビのプライバシーポリシー](https://www.adobe.com/jp/privacy/policy.html)を参照してください。

* **Adobe Experience Cloud を使用した情報収集の仕組み**

   * Adobe Experience Cloud ソリューションでは、情報を収集できるように、Web ビーコン（タグやピクセルとも呼ばれます）などの Cookie および同様のテクノロジーを使用します。Cookie および Adobe Campaign を使用した追跡機能について詳しくは、[この節](#tracking-capabilities)を参照してください。
   * モバイルアプリで Adobe Experience Cloud テクノロジーを使用することもできます。Campaign を使用してモバイル配信を送信する方法について詳しくは、[SMS チャネル](../../delivery/using/sms-channel.md)と[モバイルアプリのチャネル](../../delivery/using/about-mobile-app-channel.md)を参照してください。

* **Adobe Experience Cloud の使用に関するユーザーのプライバシー選択**

   アドビから、次の内容を説明するプライバシーポリシーをお客様に提供するように求められます。

   * Adobe Experience Cloud に関するプライバシープラクティス
   * Adobe Experience Cloud に関連して、ユーザーが情報の収集や使用に関する環境設定をおこなう方法

   >[!NOTE]
   >
   >すべてのアドビ製品と同様に、Campaign のユーザーは、アプリや Web サイトを通じて収集した共有情報をオプトアウトできます。詳しくは、[Adobe Experience Cloud の使用に関する FAQ](https://www.adobe.com/jp/privacy/experience-cloud-usage-info-faq.html) を参照してください。

Adobe Experience Cloud のプライバシーについて詳しくは、[このページ](https://www.adobe.com/jp/privacy/marketing-cloud.html)を参照してください。

## 個人データと個人 {#personal-data}

プライバシーを管理する場合、どのデータを誰がどのように扱うかを定義することが重要です。
* **個人データ**&#x200B;は、生きている個人を直接または間接的に識別できる情報です。
* **個人の機密データ**&#x200B;は、個人の人種、政治観、宗教的信念、犯罪歴、遺伝情報、健康データ、性的嗜好、生体認証情報、および労働組合の組合員に関する情報です。

[主な法律](#privacy-regulations)は、データを管理する様々なエンティティを次のように参照しています。
* **データ管理者**&#x200B;は、個人データの収集、使用、共有の方法と目的を決定する権限です。
* **データ処理者**&#x200B;は、データ管理者の指示に従って個人データを収集、使用、または共有する個人または関係者です。
* **データ主体**&#x200B;は、個人データが収集、使用、共有され、その個人データを参照して直接または間接的に識別できる、生きている個人のことです。

したがって、個人データを収集し共有する会社はデータ管理者で、そのクライアントはデータ主体です。Adobe Campaign は、お客様の指示に従って個人データを処理する際に、データ処理者として機能します。[プライバシーリクエスト](#privacy-requests)を管理する場合など、データ主体との関係を処理するのはデータ管理者としての責任であることに注意してください。

Campaign を、[Adobe Analytics](../../platform/using/adobe-analytics-data-connector.md)、[Audience Manager または People コアサービス](../../integrations/using/sharing-audiences-with-adobe-experience-cloud.md)、[Campaign Standard](../../integrations/using/synchronizing-audiences.md) などのシステム間でオーディエンスを転送できる他の Experience Cloud ソリューションと統合する場合、または[ CRM コネクタ](../../platform/using/crm-connectors.md)を介して他のソリューションと統合する場合は、個人データの保護に特別な注意を払う必要があります。

## データの取得 {#data-acquisition}

Adobe Campaign を使用すると、個人情報や機密情報などのデータを収集できます。したがって、受信者の同意を受け取り、監視する必要があります。

* 受信者は常に通信の受信に同意するようにします。これをおこなうには、できるだけ早くオプトアウトリクエストを守り、二重のオプトインプロセスを通じて同意を確認します。詳しくは、[二重のオプトインを備えた購読フォームの作成](../../web/using/use-cases--web-forms.md#create-a-subscription--form-with-double-opt-in)を参照してください。
* 不正なリストを読み込まず、シードアドレスを使用して、クライアントファイルが不正に使用されていないことを確認してください。詳しくは、[シードアドレスについて](../../delivery/using/about-seed-addresses.md)を参照してください。
* 同意と権限の管理を通じて、受信者の好みを追跡し、組織内の誰がどのデータにアクセスできるかを管理できます。詳しくは、[この節](#consent)を参照してください。
* 受信者からのプライバシーリクエストを促進および管理します。詳しくは、[この節](#privacy-requests)を参照してください。

## プライバシーの管理 {#privacy-management}

プライバシー管理とは、プライバシー規制（GDPR、CCPA など）の遵守に役立つすべてのプロセスとツールを指します。プライバシー管理の概要を[このページ](https://helpx.adobe.com/jp/campaign/kb/campaign-privacy-overview.html)で確認します。

Adobe Campaign では、プライバシー管理に関する様々な機能を提供しています。
* 同意の管理、データ保持、ユーザーの役割：[この節](#consent)を参照してください。
* プライバシーリクエスト（アクセスする権利と忘れられる権利）：[この節](#privacy-requests)を参照してください。
* 個人情報の販売のオプトアウト（CCPA 固有）：[この節](https://helpx.adobe.com/jp/campaign/kb/acc-privacy.html#ccpa)を参照してください。

Campaign の主なプライバシー機能と関与する個人の例を[この節](https://helpx.adobe.com/jp/campaign/kb/campaign-privacy-more.html#gdprpersonasandflow)に示します。


### 同意、リテンション、役割 {#consent}

元々、Adobe Campaign はプライバシーに不可欠な重要な機能を提供しています。

* **同意の管理**：購読管理プロセスを通じて、受信者の環境設定を管理し、どの受信者がどの購読タイプにオプトインしたかを追跡できます。詳しくは、[購読について](../../delivery/using/about-services-and-subscriptions.md)を参照してください。
* **データ保持**：すべての組み込みの標準ログテーブルには事前に設定された保存期間があり、通常、データのストレージは 6 か月以下に制限されます。その他の保存期間は、ワークフローで設定できます。詳しくは、アドビのコンサルタントまたは技術管理者にお問い合わせください。
* **権限管理**：Adobe Campaign では、事前作成された役割またはカスタムの役割を使用して、様々な Campaign オペレーターに割り当てられている権限を管理できます。これにより、会社内で様々なタイプのデータにアクセス、変更、書き出しできるユーザーを管理できます。詳しくは、[アクセス管理について](../../platform/using/access-management.md)を参照してください。

これらの機能および Adobe Campaign での管理方法について詳しくは、[このページ](https://helpx.adobe.com/jp/campaign/kb/campaign-privacy-overview.html#consent)を参照してください。

### プライバシーリクエスト {#privacy-requests}

Adobe Campaign は、特定のプライバシーリクエストに対するデータコントローラーとしての準備を容易にするための追加機能を提供します。

* **アクセスする権利**&#x200B;とは、データ主体がデータ管理者に対し、自分に関する個人データが処理されているかどうか、また処理されている場合はその場所と目的について確認できることを指します。

* 「**忘れられる権利**（削除リクエスト）」は、データ主体に対して、データ管理者が個人データを消去する権限を与えます。

>[!NOTE]
>
>GDPR、CCPA、PDPA、LGPD のプライバシーコンプライアンスに役立つツール群を紹介します。これらの様々な規則について詳しくは、[このページ](https://helpx.adobe.com/jp/campaign/kb/campaign-privacy-overview.html#whatisgdpr)を参照してください。

<!--* **GDPR** (General Data Protection Regulation) is the European Union’s (EU) privacy law that harmonizes and modernizes data protection requirements. GDPR applies to Adobe Campaign customers who hold data for Data Subjects residing in the EU.

* **CCPA** (California Consumer Privacy Act) provides California residents new rights in regards to their personal information and imposes data protection responsibilities on certain entities whom conduct business in California.

* **Thailand's PDPA** (Personal Data Protection Act) is the new privacy law that harmonizes and modernizes data protection requirements for Thailand. This regulation applies to Adobe Campaign customers who hold data for Data Subjects residing in this country.

Brazil's Lei Geral de Proteção de Dados (LGPD) will be effective starting Aug, 16 for all companies collecting or processing personal data in Brazil. This regulation also applies to Adobe Campaign customers who hold data for Data Subjects residing in this country.-->

**アクセス**&#x200B;リクエストと&#x200B;**削除**&#x200B;リクエストは、[このページ](https://helpx.adobe.com/jp/campaign/kb/acc-privacy.html#righttoaccess)に表示されます。これらのリクエストを作成するための実装手順については、[この節](https://helpx.adobe.com/jp/campaign/kb/acc-privacy.html#ManagingPrivacyRequests)で詳しく説明します。 <!--Tutorials are also available [here](https://docs.adobe.com/content/help/en/campaign-standard-learn/tutorials/privacy/privacy-overview.html).-->

## トラッキング機能 {#tracking-capabilities}

### Cookie {#cookies}

Adobe Campaignでは、その追跡機能のおかげで、次の3種類のcookieを使用して配信受信者の閲覧を追跡できます。セッションcookieと2つの永続的なcookie。

* A **session cookie**: the **nlid** cookie contains the identifier of the email sent to the contact (**broadlogId**) and the identifier of the message template (**deliveryId**). Adobe Campaign が送信した E メールに含まれている URL を連絡先のユーザーがクリックすると追加され、この連絡先での Web 上の行動をトラッキングできるようになります。このセッション Cookie は、ブラウザーが閉じられると自動的に消去されます。連絡先のユーザーは、Cookie を拒否するようにブラウザーを設定できます。

* 永続的な **cookie**:UUID **** (Universal Unique IDentifier)cookieは、Adobe Experience Cloudのソリューション間で共有されます。 新しい値が生成されるとクライアントブラウザーから表示されなくなるまで、1回設定されます。 このcookieを使用すると、Webサイトの訪問時にExperience Cloudソリューションを操作するユーザーを識別できます。 このレポートは、ランディングページ(不明な顧客アクティビティを受信者に関連付けるため)または配信によって預け入れることができます。 この Cookie の説明については、[こちら](https://docs.adobe.com/content/help/ja-JP/core-services/interface/ec-cookies/cookies-mc.html)を参照してください。

<!--The **nllastdelid** cookie (introduced in Campaign Classic 20.3) is a permanent cookie which contains the **deliveryId** of the last delivery that user clicked the link from. This cookie is used - when the session cookie is missing - to identify the tracking table that will be used.-->

GDPR（一般データ保護規則）などの規制では、企業は Cookie をインストールする前に Web サイトのユーザーの同意をリクエストすることが規定されています。

* Cookie の使用を許可するためのチェックボックスを伴う認証リクエスト（例えばページ上に表示される）を使用して、サイトに Web トラッキングツールがあることをユーザーに通知したり、ランディングページの上部にバナーを追加したりする必要があります。
* ポップアップウィンドウはブラウザーでブロックされていることが多いので、避ける必要があります。

### メッセージトラッキング {#message-tracking}

Adobe Campaign では、送信された E メールと配信受信者の動作（開く、リンクのクリック、購読解除など）を追跡できます。詳しくは、[メッセージトラッキングについて](../../delivery/using/about-message-tracking.md)を参照してください。

これをおこなうには、[トラッキングされたリンク](../../delivery/using/how-to-configure-tracked-links.md)をメッセージに追加して、配信ダッシュボードの「[トラッキング](../../delivery/using/monitoring-a-delivery.md#tracking-logs)」タブで配信と受信者の動作の影響を測定します。トラッキングデータは、[トラッキングインジケーター](../../reporting/using/delivery-reports.md#tracking-indicators)レポートで解釈されます。

### Web トラッキング {#web-tracking}

また、Adobe Campaign では、受信者が Web サイトをどのように参照するかを監視できます。トラッキングタグを挿入して、情報を収集し、Web アプリケーションページ上の訪問回数を測定します。詳しくは、[Web アプリケーションのトラッキング](../../web/using/tracking-a-web-application.md)を参照してください。

Web トラッキングの設定については、[この節](../../configuration/using/about-web-tracking.md)で説明しています。

Adobe Campaign では、トラッキングをさらに管理するために、オプトアウトバナーを表示して、行動追跡をオプトアウトしたエンドユーザーの Web 行動の追跡を停止できます。詳しくは、[Web アプリケーショントラッキングのオプトアウト](../../web/using/web-application-tracking-opt-out.md)を参照してください。
