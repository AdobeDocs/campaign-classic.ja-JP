---
title: キャンペーン設定FAQ
seo-title: Campaign の設定方法
description: Campaign Classic FAQ
page-status-flag: never-activated
uuid: 3f719ac2-cc26-4fb0-adda-84666c8c38e1
contentOwner: sauviat
products: SG_CAMPAIGN/CLASSIC
audience: platform
content-type: reference
topic-tags: starting-with-adobe-campaign
discoiquuid: 16dbe423-018f-4666-9901-2120a8dc609a
index: y
internal: n
snippet: y
translation-type: tm+mt
source-git-commit: 7aa381654805798fcdd24f588160bed15e037a2b

---


# キャンペーン設定FAQ {#settings-faq}

ニーズに合わせて Campaign インスタンスを設定するための主な設定内容について学習します。

## Can I change the language of Campaign interface? {#can-i-change-the-language-of-campaign-interface-}

Campaign の言語はインスタンスを作成するときに選択します。後から変更することはできません。詳しくは、[この節](../../installation/using/creating-an-instance-and-logging-on.md)を参照してください。

Adobe Campaignのユーザーインターフェイスは、次の4言語で利用できます。英語、フランス語、ドイツ語、日本語。 クライアントコンソールとサーバーは同一言語で設定する必要があるのでご注意ください。Campaign インスタンスはそれぞれ、1 つの言語でしか実行できません。

英語であれば、Campaign をインストールする際に米国英語か英国英語を選べます（それぞれ日時のフォーマットが異なります）。これらの差異について詳しくは、[この節](../../platform/using/adobe-campaign-workspace.md#date-and-time)を参照してください。

## Can I use Campaign Classic with other Adobe solutions? {#can-i-use-campaign-classic-with-other-adobe-solutions-}

Adobe Campaign の配信機能と高度なキャンペーン管理機能を、一連のソリューションと組み合わせることで、顧客エクスペリエンスをパーソナライズできます。

[他のアドビソリューションとの連携方法](../../integrations/using/about-campaign-integrations.md)と、[Campaign での IMS の設定方法](../../integrations/using/about-adobe-id.md)を参照してください。

## How can I set up tracking capabilities on my Campaign instance? {#how-can-i-set-up-tracking-capabilities-on-my-campaign-instance-}

エキスパートユーザーは、Campaign インスタンス上でトラッキング機能を設定できます。

[詳しくはここをクリック](../../installation/using/deploying-an-instance.md#tracking-configuration)してください。

## How to configure email deliverability? {#how-to-configure-email-deliverability-}

[配信品質に関するはじめにガイド](http://docs.campaign.adobe.com/doc/AC/getting_started/EN/deliverability.html)のほか、E メール配信品質の設定に関する節も参照すると、Campaign の配信機能を最大化するインスタンスの設定方法を理解できます。

[詳しくはここをクリック](../../installation/using/email-deliverability.md)してください。

## How can I implement content approval? {#how-can-i-implement-content-approval-}

Campaign では、マーケティングキャンペーンのメインステップの承認プロセスを協調モードで設定できます。キャンペーンごとに、配信ターゲット、コンテンツ、およびコストを承認できます。承認を担当する Adobe Campaign オペレーターは、E メールで通知を受け、コンソールから、または Web 接続を介して、承認を許可または却下できます。

Campaign で配信コンテンツの承認を実装する手順について[詳しくはここをクリック](../../campaign/using/marketing-campaign-approval.md#checking-and-approving-deliveries)してください。

## How can I access data stored in an external database? {#how-can-i-access-data-stored-in-an-external-database-}

Adobe Campaign では、Federated Data Access（FDA）オプションを利用することができます。このオプションを使用すると、1 つ以上の外部データベースに格納されている情報を処理することが可能です。Adobe Campaign データの構造を変更しなくても、外部データにアクセスできます。

[詳しくはここをクリック](../../platform/using/connecting-to-database.md)してください。

## Which external databases can I connect Campaign to? {#which-external-databases-can-i-connect-campaign-to-}

Federated Data Access（FDA）を使用した Campaign と外部データベースとの互換性のリストについては、[互換性マトリックス](https://helpx.adobe.com/campaign/kb/compatibility-matrix.html)を参照してください。

## Can Adobe Campaign integrate with LDAP? {#can-adobe-campaign-integrate-with-ldap-}

オンプレミス／ハイブリッドの顧客は、Campaign Classic と LDAP ディレクトリを統合できます。

[方法についてはここをクリック](../../installation/using/connecting-through-ldap.md)してください。

## How can I set up CRM connectors in Campaign? {#how-can-i-set-up-crm-connectors-in-campaign-}

Adobe Campaign では、Adobe Campaign プラットフォームをサードパーティのシステムにリンクするための様々な CRM コネクタが提供されています。これらの CRM コネクタにより、連絡先、アカウント、購入などを同期したり、アプリケーションを様々なサードパーティおよびビジネスアプリケーションと簡単に統合したりすることができます。

これらのコネクタを使用すると、データを迅速かつ容易に統合できます。Adobe Campaignには、CRMで使用可能なテーブルを収集して選択するための専用のウィザードが用意されています。 これにより、システム全体でデータを常に最新にするための双方向の同期が保証されます。

CRM ツールを Adobe Campaign と同期させる方法については、[CRM コネクタの設定](../../platform/using/crm-connectors.md)を参照してください。こちらの [Adobe Campaign と Microsoft Dynamics 365 の統合](https://helpx.adobe.com/campaign/kt/acc/using/acc-integrate-dynamics365-with-acc-feature-video-set-up.html)に関する使用例のビデオをご覧ください。
