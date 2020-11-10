---
title: プライバシーの管理
seo-title: プライバシーの管理
description: プライバシーの管理
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
source-git-commit: b8548e8d609ed099433b97b4c0704d27234e81c0
workflow-type: tm+mt
source-wordcount: '898'
ht-degree: 63%

---


# プライバシーの管理 {#privacy-management}

Adobe Campaign には、プライバシー規制（GDPR、CCPA、PDPA、LGPD など）を遵守するのに役立つ一連のツールが用意されています。

* This section presents general information on what Privacy management is and the features provided by Adobe Campaign to manage the [Right to Access and Right to be Forgotten](#right-access-forgotten).

* また、プライバシー([同意、データ保持、ユーザーの役割](#consent-retention-roles))を管理するための重要な機能に関する情報や、Adobe Campaignを使用する際のプライバシーコンプライアンスに役立つベストプラクティスも含まれています。

## プライバシー管理に関する規制 {#privacy-management-regulations}

Adobe Campaignの機能は、次の規則の遵守に役立ちます。

* **GDPR**（[EU 一般データ保護規則](https://ec.europa.eu/info/law/law-topic/data-protection/reform/what-does-general-data-protection-regulation-gdpr-govern_en)）は欧州連合（EU）で施行されるプライバシー保護法律で、EU 諸国のデータ保護要件を現代の状況に合わせて整合化することを目的としています。
* **CCPA**（[カリフォルニア州消費者プライバシー法](https://leginfo.legislature.ca.gov/faces/codes_displayText.xhtml?lawCode=CIV&amp;division=3.&amp;title=1.81.5.&amp;part=4.&amp;chapter=&amp;article=)）は、カリフォルニア州民に個人情報に関する新しい権利を提供し、カリフォルニア州でビジネスをおこなう特定の事業者に対してデータ保護の責任を課します。
* **PDPA** ([Personal Data Protection Act](https://secureprivacy.ai/thailand-pdpa-summary-what-businesses-need-to-know/))は、タイのデータ保護要件を調和・近代化する新しいプライバシー法です。
* **LGPD**（[Lei Geral de Proteção de Dados、一般データ保護法](https://iapp.org/media/pdf/resource_center/Brazilian_General_Data_Protection_Law.pdf)）は、2021 年前半から適用され、ブラジルで個人データを収集および処理するすべての会社に対して有効となります。

これらすべての規則は、前述の各地域または国（EU、米国カリフォルニア州、タイ、ブラジル）に居住するデータ主体のデータを保持する Adobe Campaign のお客様に適用されます。

<!--Several Privacy capabilities are available in Adobe Campaign, including consent management, data retention settings, and rights management. See [Consent, Retention and Roles](#consent-retention-roles). In addition to this, Adobe Campaign helps facilitate your readiness as Data Controller for certain Privacy requests. See [Right to Access and Right to be Forgotten](#right-access-forgotten).-->

>[!NOTE]
>
>個人データおよびデータを管理する様々なエンティティ（データ管理者、データ処理者、データ主体）について詳しくは、[個人データとペルソナ](../../platform/using/privacy-and-recommendations.md#personal-data)を参照してください。

## アクセスする権限と消失させる権限 {#right-access-forgotten}

In order to help you facilitate your Privacy readiness, Adobe Campaign allows you to handle **Access** and **Delete** requests.

* **アクセスする権限**&#x200B;とは、データ主体がデータ管理者に対し、自分に関する個人データが処理されているかどうか、また処理されている場合はその場所と目的について確認できることを指します。データ管理者は、個人データのコピーを電子形式で無償提供する必要があります。

* **消失させる権限**（削除要求）とは、データ消去とも呼ばれるもので、データ主体はデータ管理者に対して、自分の個人データの消去、および第三者によるデータ処理を防止するために、データ拡散の停止を指示できることを指します。

**Access** / **Deleteリクエストの作成方法、およびAdobe Campaignによるリクエストの処理方法については、** 導入手順を参照してください [](../../platform/using/privacy-requests.md)。

<!--Tutorials on Privacy management in Campaign Standard are also available [here](https://docs.adobe.com/content/help/en/campaign-standard-learn/tutorials/privacy/privacy-overview.html).
https://experienceleague.corp.adobe.com/docs/campaign-standard-learn/tutorials/privacy/privacy-overview.html?lang=en-->

## 同意、リテンション、役割 {#consent-retention-roles}

In addition to the most recent **Right to Access** and **Right to be Forgotten** capabilities, Adobe Campaign offers other important features that are essential to Privacy:

* [同意管理](#consent-management)：環境設定管理用の購読機能
* [データリテンション](#data-retention)：すべての標準ログテーブルのデータリテンション期間。リテンション期間の追加はワークフローで設定可能
* [権限管理](#rights-management)：ネームド権限により管理されるデータアクセス

### 同意管理 {#consent-management}

同意とは、データ主体に関する個人データの処理についてデータ主体からの同意を得ることを指します。処理に関して必要な同意を得ることは、データ管理者が行います。Adobe Campaign には、サービスに関連する同意を顧客が管理するための機能はありますが、アドビは同意自体についての責任を負いません。顧客は自社内の法務部門と連携して、同意のプロセスと手続きを自ら判断する必要があります。

同意に関する側面を管理する機能は、発売当初から Adobe Campaign の中核機能でした。購読管理プロセスを通じて、顧客はどの受信者がどのタイプの購読にオプトインしたかを、ニュースレター、日別プロモーション、週別プロモーション、その他のタイプのマーケティングプログラムのいずれかで追跡できます。

![](assets/privacy-consent-management.png)

同意の管理について詳しくは、 [詳細なドキュメントを参照してください](../../delivery/using/managing-subscriptions.md)。

Adobe Campaignが提供する同意管理ツールに加えて、個人情報の販売に対して消費者がオプトアウトしたかどうかを追跡できます。 [こちらの節](../../platform/using/privacy-requests.md#sale-of-personal-information)を参照してください。

### データリテンション {#data-retention}

保存に関しては、キャンペーンに組み込まれているログ・テーブルには事前に設定された保存期間があり、通常、データのストレージは6か月以下に制限されます。

組み込みテーブルのデフォルトの保持期間は以下のとおりです。リテンションは実装時にアドビの技術管理者が設定します。値は顧客の要件に基づくため、実装ごとに異なる場合があります。

* **統合トラッキング**:1 year
* **配信ログ**：6 ヶ月
* **トラッキングログ**:1 year
* **削除された配信**:1 week
* **オブジェクトの読み込み**:6 months
* **訪問者プロファイル**:1 month
* **オファーの提案**:1 year
* **イベント**：1 ヶ月
* **イベント処理の統計**:1 year
* **アーカイブされたイベント**:1 year
* **無視されたパイプラインイベント**:1 month

削除の場合と同様、標準ワークフロー機能を使用して、任意のカスタムテーブルのリテンション期間を設定することができます。

リテンションの詳細について知りたい場合、またはカスタムテーブルの設定が必要な場合は、アドビのコンサルタントまたは技術管理者にお問い合わせください。

### 権限管理 {#rights-management}

Adobe Campaign では、事前作成された役割またはカスタムの役割を使用して、様々な Campaign オペレーターに割り当てられている権限を管理できます。

その利点のひとつとして、各種類のデータについて社内のどのユーザーがアクセスできるかを管理できることがあげられます。例えば、さまざまな地域を複数のマーケッターで担当している場合に、各マーケッターが自分の担当地域からのみデータにアクセスできるようにすることが可能です。

同様に、この機能を使用すると、配信を送信できるユーザーを制限するなど、ユーザーごとに異なる機能を設定したり、データを変更または書き出せるプライバシー管理に関連性を持たせたりできます。

![](assets/privacy-user-management.png)

アクセス管理について詳しくは、 [詳細なドキュメントを参照してください](../../platform/using/access-management.md)。