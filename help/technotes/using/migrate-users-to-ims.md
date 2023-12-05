---
title: Campaign オペレーターの Adobe Identity Management System（IMS）への移行
description: Campaign オペレーターの Adobe Identity Management System（IMS）への移行方法を説明します
source-git-commit: 18166dd389847d6b844ed478e19c42e457abeb80
workflow-type: tm+mt
source-wordcount: '1153'
ht-degree: 40%

---

# Campaign オペレーターの Adobe Identity Management System（IMS）への移行 {#migrate-users-to-ims}

セキュリティと認証プロセスを強化する取り組みの一環として、Adobe Campaignでは、エンドユーザー認証モードをログイン/パスワードネイティブ認証からAdobeIdentity Management System(IMS) に移行することを強くお勧めします。 すべての演算子は、 [AdobeIdentity Managementシステム (IMS)](https://helpx.adobe.com/jp/enterprise/using/identity.html){target="_blank"} をクリックして、Campaign に接続します。

Campaign v8 では、ユーザー/パスワード（ネイティブ認証）との接続は許可されなくなります。 **Adobeは、Campaign v8 にスムーズに移行できるよう、Campaign v7.3.5 でこの移行を実行することをお勧めします。**

この記事では、Adobe Developer Console でテクニカルオペレーターをテクニカルアカウントに移行するために必要な手順について詳しく説明します。

## 変更点{#move-to-ims-changes}

Campaign Classicを使用すると、すべての通常のユーザーは、既にAdobe IDを使用して、AdobeIdentity Management System(IMS) を通じてAdobe Campaignクライアントコンソールに接続できます。 ただし、ユーザー/パスワードの接続は引き続き利用できます。 Campaign v8 では、この機能は使用できなくなります。

さらに、セキュリティと認証プロセスを強化する取り組みの一環として、Adobe Campaign クライアントアプリケーションは、IMS テクニカルアカウントトークンを使用して Campaign API を直接呼び出すようになりました。テクニカルオペレーターの移行について詳しくは、[このページ](ims-migration.md)にある専用の記事を参照してください。

この変更はCampaign Classicv7 で既に適用され、次の日付になります。 **必須** をクリックして、Campaign v8 に移行します。

## 影響の有無{#migrate-ims-impacts}

この手順は、Adobe IDと Campaign にまだ接続していないすべての Campaign ユーザーに適用されます。

組織内のオペレーターが Campaign クライアントコンソールにログイン／パスワード（別名ネイティブ認証など ) の権限を持つ場合は影響が生じ、以下に説明するように、これらのオペレーターをAdobe IMSに移行する必要があります。

[Adobe Identity Management System（IMS）](https://helpx.adobe.com/jp/enterprise/using/identity.html){target="_blank"}への移行は、他の Adobe Experience Cloud ソリューションやアプリのほとんどは既に IMS 上にあるので、環境を安全かつ標準化するためにセキュリティ上不可欠です。

## ホスト環境とManaged Services環境を移行する方法は？ {#ims-migration-procedure}

### 前提条件 {#ims-migration-prerequisites}

Adobeの技術チームが既存のオペレーターグループとネームド権限をAdobeIdentity Management System(IMS) に移行できるように、移行プロセスを開始する前に、Adobe移行マネージャー (Managed Servicesのお客様向け ) またはAdobeカスタマーケアに問い合わせる必要があります。

### 主な手順 {#ims-migration-steps}

この移行の主な手順を以下に示します。

1. Adobeは、環境を Campaign v7.3.5 にアップグレードします。
1. アップグレード後も、ネイティブユーザーまたは IMS の両方の方法で新しいユーザーを引き続き作成できます。
1. Campaign の内部キャンペーン管理者は、Campaign クライアントコンソールですべてのネイティブユーザーに一意の E メールを追加し、追加が完了したらAdobe担当者またはカスタマーケアに確認する必要があります。  この手順について詳しくは、[この節](#ims-migration-id)を参照してください。
1. Adobe担当者またはカスタマーケアと協力して、技術以外のユーザー（オペレーター）および製品プロファイルに対してAdobeが自動移行を実行する日付を保護します。 この手順には、1 時間の時間枠が必要です。どのサービスに対してもダウンタイムは発生しません。
1. 内部の Campaign 管理者がこれらの変更を検証し、サインオフします。この移行後は、ログイン名とパスワードで認証するオペレーターをさらに作成する必要はありません。

また、技術オペレーターをAdobe Developer Console に移行することもできます。詳しくは、 [このテクニカルノート](ims-migration.md).

この移行が完了したら、Adobe移行マネージャー (Managed Servicesユーザーの場合 ) またはAdobeカスタマーケア（ホスト型のお客様の場合）に確認します。 Adobeは、移行が完了したことを示します。 これにより、環境が保護され、標準化されます。


## ハイブリッド環境とオンプレミス環境の移行方法は？ {#ims-migration-procedure-on-prem}

この移行の主な手順を以下に示します。

1. 環境を Campaign v7.3.5 にアップグレードします。
1. アップグレード後も、ネイティブユーザーまたは IMS の両方の方法で新しいユーザーを引き続き作成できます。
1. 内部 Campaign 管理者は、 [この節](../../integrations/using/configuring-ims.md).
1. 次に、Campaign クライアントコンソールで、すべてのネイティブユーザーに一意の E メールを追加します。 この手順について詳しくは、[この節](#ims-migration-id)を参照してください。
1. Adobe Admin Consoleでのユーザーおよび製品プロファイルの作成 ( [Campaign v8 ドキュメント](https://experienceleague.adobe.com/docs/campaign/campaign-v8/admin/permissions/manage-permissions.html){target="_blank"}.
1. を有効にします。 **Adobe IDとの接続** オプションを選択できます。
1. 接続のAdobe IMSを実装します。詳しくは、 [このページ](../../integrations/using/implementing-ims.md).

また、技術オペレーターをAdobe Developer Console に移行することもできます。詳しくは、 [このテクニカルノート](ims-migration.md).


## よくある質問 {#ims-migration-faq}

### 移行を開始できるのはいつですか？ {#ims-migration-start}

への移行に関する推奨事項 [AdobeIdentity Managementシステム (IMS)](https://helpx.adobe.com/jp/enterprise/using/identity.html){target="_blank"} は、環境をCampaign Classicv7.3.5 にアップグレードするためのものです。

Campaign Classicv7.3.5 にアップグレードした後は、ステージ環境で IMS の移行を開始し、実稼動環境に合わせて計画できます。

### ビルドをCampaign Classicv7.3.5 にアップグレードした後、どうなりますか？ {#ims-migration-after-upgrade}

環境をCampaign Classicv7.3.5 にアップグレードした後、 [AdobeIdentity Managementシステム (IMS)](https://helpx.adobe.com/jp/enterprise/using/identity.html){target="_blank"}.

### 移行が完了するのはいつですか？ {#ims-migration-end}

AdobeIdentity Management System(IMS) へのエンドユーザーの移行および技術的なユーザーの移行が完了したら、Adobeが移行完了とマークできるよう、Adobe担当者またはカスタマーサポートに連絡する必要があります。

### 移行後にユーザーを作成するにはどうすればよいですか？ {#ims-migration-native}

Adobeは、Campaign Classicv7.3.5 にアップグレードした後、IMS ユーザーのみを作成することをお勧めします。

Campaign 管理者は、Adobe Admin Console と Campaign クライアントコンソールを通じて組織のユーザーに権限を付与できます。ユーザーは、Adobe ID を使用して Adobe Campaign にログオンします。で IMS を使用した権限を設定する方法を説明します。 [Campaign v8 ドキュメント](https://experienceleague.adobe.com/docs/campaign/campaign-v8/admin/permissions/gs-permissions.html?lang=ja){target="_blank"}.

### 現在のネイティブユーザー用のメールアドレスを追加するにはどうすればよいですか？ {#ims-migration-id}

Campaign 管理者は、クライアントコンソールからすべてのネイティブユーザーにメール ID を追加する必要があります。手順は次のとおりです。

1. クライアントコンソールに接続し、**管理／アクセス管理／オペレーター**&#x200B;を参照します。
1. オペレーターリストで更新するオペレーターを選択します。
1. オペレーターフォームの「**連絡窓口**」セクションにオペレーターのメールアドレスを入力します。
1. 変更内容を保存します。

<!--You can also import a CSV file to update all your operator profiles with their email.-->


### IMS 経由で Campaign にログインするにはどうすればよいですか？ {#ims-migration-log}

Campaign と Adobe ID の接続方法については、[この節](../../integrations/using/implementing-ims.md)を参照してください。

### この移行中にダウンタイムは発生しますか？ {#ims-migration-downtime}

ホスト型およびManaged Services型のお客様は、Adobeを完了する（ユーザーと製品プロファイルを移行する）には、移行に 1 時間の時間が必要です。お客様のインスタンス（ワークフローなど）にはダウンタイムは発生しません。

この期間中、すべての Campaign ユーザーはログオフし、IMS への移行が完了したら Adobe ID を使用して再度ログインする必要があります。

アドビでは、移行期間中はすべてのユーザーをログオフすることを強くお勧めします。

### 組織内のユーザーは既に IMS を使用していますが、IMS の移行を実行する必要がありますか？{#ims-migration-needed}

この移行には、エンドユーザーの移行（製品プロファイルを含む）と、技術ユーザーの移行（カスタムコードの API で使用）の 2 つの側面があります。

すべてのAdobe（Campaign オペレーター）が IMS を使用している場合でも、製品プロファイルの移行を計画するには、担当のユーザー担当者またはカスタマーサポートに連絡する必要があります。 また、カスタムコードで使用した技術ユーザーを移行する必要があります。 詳しくは、[このページ](ims-migration.md)を参照してください。

## 便利なリンク {#ims-useful-links}

* [Adobe Developer Console へのテクニカルユーザーの移行](ims-migration.md)
* [Adobe Campaign v8 リリースノート](../../rn/using/latest-release.md)
* [Adobe Identity Management System（IMS）とは](https://helpx.adobe.com/jp/enterprise/using/identity.html){target="_blank"}
