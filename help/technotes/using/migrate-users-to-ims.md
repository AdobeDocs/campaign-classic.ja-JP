---
title: Campaign オペレーターの Adobe Identity Management System（IMS）への移行
description: Campaign オペレーターの Adobe Identity Management System（IMS）への移行方法を説明します
exl-id: f01948c7-b523-492d-a4e8-67f4adde5fc5
source-git-commit: bc9367d598474b7971f25c27980ff25dd93bf87a
workflow-type: ht
source-wordcount: '0'
ht-degree: 100%

---

# Campaign オペレーターの Adobe Identity Management System（IMS）への移行 {#migrate-users-to-ims}

セキュリティと認証プロセスを強化する取り組みの一環として、Adobe Campaign では、エンドユーザー認証モードをログイン/パスワードネイティブ認証から Adobe Identity Management System（IMS）に移行することを強くお勧めしています。 すべてのオペレーターは、[Adobe Identity Management System（IMS）](https://helpx.adobe.com/jp/enterprise/using/identity.html){target="_blank"}を使用して Campaign に接続する必要があります。

Campaign v8 ユーザー名やパスワードを使用した接続（別名ネイティブ認証）は許可されなくなります。**アドビでは、Campaign v8 にスムーズに移行できるように、Campaign v7.3.5 でこの移行を実行することをお勧めします。**

この記事では、Adobe Developer Console でテクニカルオペレーターをテクニカルアカウントに移行するために必要な手順について詳しく説明します。

## 変更点{#move-to-ims-changes}

Campaign Classic では、すべての標準ユーザーは、Adobe Identity Management System（IMS）により、Adobe ID を使用して Adobe Campaign クライアントコンソールに既に接続しています。ただし、ユーザー名とパスワードでの接続は引き続き可能です。これは、Campaign v8 以降では使用できなくなります。

さらに、セキュリティと認証プロセスを強化する取り組みの一環として、Adobe Campaign クライアントアプリケーションは、IMS テクニカルアカウントトークンを使用して Campaign API を直接呼び出すようになりました。テクニカルオペレーターの移行について詳しくは、[このページ](ims-migration.md)にある専用の記事を参照してください。

この変更は Campaign Classic v7 で既に適用されており、Campaign v8 に移行するためには&#x200B;**必須**&#x200B;となります。

## 影響の有無{#migrate-ims-impacts}

この手順は、まだ Adobe ID を使用して Campaign に接続していないすべての Campaign ユーザーに適用されます。

組織内のオペレーターが Campaign クライアントコンソールにログイン／パスワード（別名ネイティブ認証）影響を受けるので、以下で説明するようにこれらのオペレーターを Adobe IMS に移行する必要があります。

[Adobe Identity Management System（IMS）](https://helpx.adobe.com/jp/enterprise/using/identity.html){target="_blank"}への移行は、他の Adobe Experience Cloud ソリューションやアプリのほとんどは既に IMS 上にあるので、環境を安全かつ標準化するためにセキュリティ上不可欠です。

## ホスト環境と Managed Services 環境を移行する方法 {#ims-migration-procedure}

### 前提条件 {#ims-migration-prerequisites}

移行プロセスを開始する前に、アドビのテクニカルチームが既存のオペレーターグループとネームド権限を Adobe Identity Management System（IMS）に移行できるように、アドビトランジションマネージャー（Managed Services をご利用の場合）またはアドビカスタマーケア（その他のホスト環境をご利用の場合）にお問い合わせいただく必要があります。

### 主な手順 {#ims-migration-steps}

この移行の主な手順を以下に示します。

1. アドビでは、環境を Campaign v7.3.5 にアップグレードします。
1. アップグレード後も、ネイティブユーザーまたは IMS の両方の方法で新しいユーザーを引き続き作成できます。
1. 内部の Campaign 管理者は、Campaign クライアントコンソール上のすべてのネイティブユーザーに一意のメールアドレスを追加し、これが完了したらアドビ担当者またはアドビカスタマーケアにご確認いただく必要があります。この手順について詳しくは、[この節](#ims-migration-id)を参照してください。
1. アドビ担当者またはアドビカスタマーケアと連携して、技術に詳しくないユーザー（オペレーター）と製品プロファイルの自動移行をアドビが実行する日付を確保します。この手順には、サービスのダウンタイムが発生しない 1 時間の時間枠が必要です。
1. 内部の Campaign 管理者がこれらの変更を検証し、サインオフします。この移行後は、ログイン名とパスワードで認証するオペレーターをさらに作成する必要はありません。

テクニカルオペレーターを Adobe Developer Console に移行することもできます。詳しくは、この[テクニカルノート](ims-migration.md)を参照してください。

この移行が完了したら、アドビトランジションマネージャー（Managed Services をご利用の場合）またはアドビカスタマーケア（ホスト型のお客様の場合）に確認します。 その後、アドビは、移行が完了した旨を表示します。これにより、環境が保護され、標準化されます。


## ハイブリッド環境とオンプレミス環境の移行 {#ims-migration-procedure-on-prem}

この移行の主な手順を以下に示します。

1. 環境を Campaign v7.3.5 にアップグレードします。
1. アップグレード後も、ネイティブユーザーまたは IMS の両方の方法で新しいユーザーを引き続き作成できます。
1. 社内 Campaign 管理者の方は、[このセクション](../../integrations/using/configuring-ims.md)の説明に従い、Adobe IMS を構成する必要があります。
1. 次に、Campaign クライアントコンソールで、すべてのネイティブユーザーに一意の E メールを追加します。 この手順について詳しくは、[この節](#ims-migration-id)を参照してください。
1. Adobe Admin Console でのユーザーおよび製品プロファイルの作成について詳しくは、[Campaign v8 ドキュメント](https://experienceleague.adobe.com/docs/campaign/campaign-v8/admin/permissions/manage-permissions.html?lang=ja){target="_blank"}を参照してください。
1. すべてのオペレーターに対して「**Adobe ID を使用して接続**」オプションを有効にします。
1. 接続に対して Adobe IMS を実装するには、[このページ](../../integrations/using/implementing-ims.md)を参照してください。

また、テクニカルオペレーターを Adobe Developer Console に移行することもできます。詳しくは、[このテクニカルノート](ims-migration.md)を参照してください。


## よくある質問 {#ims-migration-faq}

### 移行を開始できるのはいつですか？ {#ims-migration-start}

[Adobe Identity Management System（IMS）](https://helpx.adobe.com/jp/enterprise/using/identity.html){target="_blank"}への移行の推奨事項は、環境を Campaign Classic v7.3.5 にアップグレードすることです。

Campaign Classic v7.3.5 にアップグレードしたら、ステージング環境で IMS への移行を開始し、それに応じて実稼動環境を計画できます。

### Campaign Classic v7.3.5 にビルドをアップグレードすると、どうなりますか？ {#ims-migration-after-upgrade}

環境を Campaign Classic v7.3.5 にアップグレードしたら、[Adobe Identity Management System（IMS）](https://helpx.adobe.com/jp/enterprise/using/identity.html){target="_blank"}への移行を開始できます。

### 移行が完了するのはいつですか？ {#ims-migration-end}

エンドユーザーと技術ユーザーを Adobe Identity Management System（IMS）に移行する処理が完了したら、アドビ担当者／カスタマーサポートに連絡し、アドビが移行を完了としてマークできるようにする必要があります。

### 移行後にユーザーを作成するにはどうすればよいですか？ {#ims-migration-native}

アドビでは、Campaign Classic v7.3.5 にアップグレードした後は、IMS ユーザーのみを作成することをお勧めします。

Campaign 管理者は、Adobe Admin Console と Campaign クライアントコンソールを通じて組織のユーザーに権限を付与できます。ユーザーは、Adobe ID を使用して Adobe Campaign にログオンします。IMS を使用して権限を設定する方法については、[Campaign v8 ドキュメント](https://experienceleague.adobe.com/docs/campaign/campaign-v8/admin/permissions/gs-permissions.html?lang=ja){target="_blank"}を参照してください。

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

ホスト環境および Managed Services 環境のお客様の場合、移行（ユーザーと製品プロファイルの移行）を完了するには、アドビでは、どのインスタンス（ワークフローなど）もダウンタイムなしで 1 時間の時間枠を必要とします。

この期間中、すべての Campaign ユーザーはログオフし、IMS への移行が完了したら Adobe ID を使用して再度ログインする必要があります。

アドビでは、移行期間中はすべてのユーザーをログオフすることを強くお勧めします。

### 組織内のユーザーは既に IMS を使用していますが、引き続き IMS への移行を実行する必要がありますか？{#ims-migration-needed}

この移行には、エンドユーザーの移行（および製品プロファイル）と技術ユーザーの移行（カスタムコードの API で使用）という 2 つの側面があります。

すべてのユーザー（Campaign オペレーター）が IMS を使用している場合でも、製品プロファイルの移行を計画するには、アドビ担当者／カスタマーサポートに問い合わせる必要があります。また、カスタムコードで使用した可能性のある技術ユーザーも移行する必要があります。詳しくは、[このページ](ims-migration.md)を参照してください。

## 便利なリンク {#ims-useful-links}

* [Adobe Developer Console へのテクニカルユーザーの移行](ims-migration.md)
* [Adobe Campaign v8 リリースノート](../../rn/using/latest-release.md)
* [Adobe Identity Management System（IMS）とは](https://helpx.adobe.com/jp/enterprise/using/identity.html){target="_blank"}
