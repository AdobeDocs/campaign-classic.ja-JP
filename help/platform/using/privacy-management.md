---
solution: Campaign Classic
product: campaign
title: プライバシー管理
description: プライバシー管理の詳細を説明します
audience: platform
content-type: reference
topic-tags: starting-with-adobe-campaign
translation-type: tm+mt
source-git-commit: c86b2d377c66e79cf4f10053f588796b95e6877e
workflow-type: tm+mt
source-wordcount: '887'
ht-degree: 97%

---


# プライバシー管理 {#privacy-management}

Adobe Campaign には、[プライバシー規制](#privacy-management-regulations)（GDPR、CCPA、PDPA、LGPD など）を遵守するのに役立つ一連のツールが用意されています。

GDPR などのプライバシー規制に対する対応するために Adobe Campaign で提供されている 5 つの主な機能を次に示します。
* **アクセスする権利**
* **削除する権利**
* **同意管理**
* **データリテンション**
* **権限管理**

![](assets/privacy-gdpr-use-cases.png)

詳しくは、[アクセス権と忘れられる権利](#right-access-forgotten)および[同意、保存、役割](#consent-retention-roles)を参照してください。

<!--This section presents general information on what Privacy management is and the features provided by Adobe Campaign to manage the [Right to Access and Right to be Forgotten](#right-access-forgotten).

It also contains information on important features to manage Privacy ([Consent, Retention and Roles](#consent-retention-roles)), as well as best practices to help you with your Privacy compliance when using Adobe Campaign.-->

## プライバシー管理に関する規制 {#privacy-management-regulations}

Adobe Campaign の機能は、次の規則の遵守に役立ちます。

* **GDPR**（[EU 一般データ保護規則](https://ec.europa.eu/info/law/law-topic/data-protection/reform/what-does-general-data-protection-regulation-gdpr-govern_en)）は欧州連合（EU）で施行されるプライバシー保護法律で、EU 諸国のデータ保護要件を現代の状況に合わせて整合化することを目的としています。
* **CCPA**（[カリフォルニア州消費者プライバシー法](https://leginfo.legislature.ca.gov/faces/codes_displayText.xhtml?lawCode=CIV&amp;division=3.&amp;title=1.81.5.&amp;part=4.&amp;chapter=&amp;article=)）は、カリフォルニア州民に個人情報に関する新しい権利を提供し、カリフォルニア州でビジネスをおこなう特定の事業者に対してデータ保護の責任を課します。
* **PDPA**（[個人情報保護法](https://secureprivacy.ai/thailand-pdpa-summary-what-businesses-need-to-know/)）は、新しいプライバシー法で、タイのデータ保護要件を現代の状況に合わせて整合化することを目的としています。
* **LGPD**（[Lei Geral de Proteção de Dados、一般データ保護法](https://iapp.org/media/pdf/resource_center/Brazilian_General_Data_Protection_Law.pdf)）は、2021 年前半から適用され、ブラジルで個人データを収集および処理するすべての会社に対して有効となります。

これらすべての規則は、前述の各地域または国（EU、米国カリフォルニア州、タイ、ブラジル）に居住するデータ主体のデータを保持する Adobe Campaign のお客様に適用されます。

<!--Several Privacy capabilities are available in Adobe Campaign, including consent management, data retention settings, and rights management. See [Consent, Retention and Roles](#consent-retention-roles). In addition to this, Adobe Campaign helps facilitate your readiness as Data Controller for certain Privacy requests. See [Right to Access and Right to be Forgotten](#right-access-forgotten).-->

>[!NOTE]
>
>個人データおよびデータを管理する様々なエンティティ（データ管理者、データ処理者、データ主体）について詳しくは、[個人データとペルソナ](../../platform/using/privacy-and-recommendations.md#personal-data)を参照してください。

## アクセスする権限と忘れられる権利 {#right-access-forgotten}

プライバシーの準備を容易にするために、Adobe Campaign では&#x200B;**アクセス**&#x200B;要求と&#x200B;**削除**&#x200B;要求の処理が可能になりました。

* **アクセスする権利**&#x200B;とは、データ主体がデータ管理者に対し、自分に関する個人データが処理されているかどうか、また処理されている場合はその場所と目的について確認できることを指します。データ管理者は、個人データのコピーを電子形式で無償提供する必要があります。

* **忘れられる権利**（削除要求）とは、データ消去とも呼ばれるもので、データ主体はデータ管理者に対して、自分の個人データの消去、および第三者によるデータ処理を防止するために、データ拡散の停止を指示できることを指します。

**アクセス**&#x200B;リクエストと&#x200B;**削除**&#x200B;リクエストの作成方法、および Adobe Campaign によるリクエストの処理方法については、[実装手順](../../platform/using/privacy-requests.md)を参照してください。

<!--Tutorials on Privacy management in Campaign Standard are also available [here](https://docs.adobe.com/content/help/en/campaign-standard-learn/tutorials/privacy/privacy-overview.html).
https://experienceleague.corp.adobe.com/docs/campaign-standard-learn/tutorials/privacy/privacy-overview.html?lang=en-->

## 同意、リテンション、役割 {#consent-retention-roles}

新しく導入された&#x200B;**アクセスする権利**&#x200B;と&#x200B;**忘れられる権利**&#x200B;の他にも、Adobe Campaign はプライバシーに必要な重要機能を各種用意しています。

* [同意管理](#consent-management)：環境設定管理用の購読機能
* [データリテンション](#data-retention)：すべての標準ログテーブルのデータリテンション期間。リテンション期間の追加はワークフローで設定可能
* [権限管理](#rights-management)：ネームド権限により管理されるデータアクセス

### 同意管理 {#consent-management}

同意とは、データ主体に関する個人データの処理についてデータ主体からの同意を得ることを指します。処理に関して必要な同意を得ることは、データ管理者がおこないます。Adobe Campaign には、サービスに関連する同意を顧客が管理するための機能はありますが、アドビは同意自体についての責任を負いません。顧客は自社内の法務部門と連携して、同意のプロセスと手続きを自ら判断する必要があります。

同意に関する側面を管理する機能は、発売当初から Adobe Campaign の中核機能でした。購読管理プロセスにより、顧客はどの受信者がどの種類の購読を登録しているかをトラッキングできます。購読の種類には、ニュースレター、毎日または毎週のプロモーションなどのマーケティングプログラムがあります。

![](assets/privacy-consent-management.png)

同意の管理について詳しくは、[詳細なドキュメント](../../delivery/using/managing-subscriptions.md)を参照してください。

Adobe Campaign が提供する同意管理ツールに加えて、消費者が個人情報の販売をオプトアウトしたかどうかをトラッキングすることもできます。[こちらの節](../../platform/using/privacy-requests.md#sale-of-personal-information-ccpa)を参照してください。

### データリテンション {#data-retention}

Campaign の組み込みログテーブルには保持期間がプリセットされており、通常はデータ保存期間が 6 か月以内に制限されています。

組み込みテーブルのデフォルトの保持期間は以下のとおりです。リテンションは実装時にアドビの技術管理者が設定します。値は顧客の要件に基づくため、実装ごとに異なる場合があります。

* **統合されたトラッキング**：1 年
* **配信ログ**：6 ヶ月
* **トラッキングログ**：1 年
* **削除された配信**：1 週間
* **却下をインポート**：6 か月
* **訪問者プロファイル**：1 か月
* **オファーの提案**：1 年
* **イベント**：1 ヶ月
* **イベント処理の統計**：1 か月
* **アーカイブしたイベント**：1 年
* **無視されたパイプラインイベント**：1 か月

削除の場合と同様、標準ワークフロー機能を使用して、任意のカスタムテーブルのリテンション期間を設定することができます。

リテンションの詳細について知りたい場合、またはカスタムテーブルの設定が必要な場合は、アドビのコンサルタントまたは技術管理者にお問い合わせください。

### 権限管理 {#rights-management}

Adobe Campaign では、事前作成された役割またはカスタムの役割を使用して、様々な Campaign オペレーターに割り当てられている権限を管理できます。

その利点の 1 つとして、各種類のデータについて社内のどのユーザーがアクセスできるかを管理できることが挙げられます。例えば、様々な地域を複数のマーケターで担当している場合に、各マーケターが自分の担当地域からのみデータにアクセスできるようにすることが可能です。

同様に、ユーザーごとに各種の機能を設定することができます。例えば、配信の送信者を限定することができます。また、プライバシーの管理に関して言えば、データの変更やエクスポートをできるユーザーを限定することもできます。

![](assets/privacy-user-management.png)

アクセス管理について詳しくは、[詳細なドキュメント](../../platform/using/access-management.md)を参照してください。