---
title: Campaign オペレーターの Adobe Identity Management System（IMS）への移行
description: Campaign オペレーターの Adobe Identity Management System（IMS）への移行方法を説明します
exl-id: f01948c7-b523-492d-a4e8-67f4adde5fc5
TQID: 'https://experienceleague.adobe.com/drpNkA9cj7Prid--GixHMQ48CO7ZC9qqX4w5fnTiD88'
product_v2:
  - id: dfc56824-e8b9-499e-85d4-21aedb507314
    internal-label: Campaign
  - id: fd6e6e36-54e4-4f1a-96fc-1a750e400d50
    internal-label: Campaign Classic v7
feature_v2:
  - id: b12f6872-9271-4369-85e5-86969a0b99a2
    internal-label: APIs
  - id: c5474392-5419-4296-9e41-f6f4ce4f6e9b
    internal-label: Administration
  - id: d5ef99fa-df0c-4153-bf94-105ad0724167
    internal-label: Integrations
subfeature_v2:
  - id: efa38731-2723-4334-8d8b-a778af834835
    internal-label: Access management
  - id: cbcf4d90-26be-46e2-b16a-aebc529dc41e
    internal-label: Analytics integration
topic_v2:
  - id: d095671a-1355-40aa-8b5f-06c33c68080b
    internal-label: Security
  - id: eddd9b14-83bd-4ff4-9072-54a4a484abb7
    internal-label: Administration
source-git-commit: 4bc1e76d129c6a6aa15b7e3915232043bd6f4286
workflow-type: ht
source-wordcount: '676'
ht-degree: 100%
---
# Campaign オペレーターの Adobe Identity Management System（IMS）への移行 {#migrate-users-to-ims}

セキュリティと認証プロセスを強化する取り組みの一環として、Adobe Campaign では、エンドユーザー認証モードをログイン/パスワードネイティブ認証から Adobe Identity Management System（IMS）に移行することを強くお勧めしています。 すべてのオペレーターは、[Adobe Identity Management System（IMS）](https://helpx.adobe.com/jp/enterprise/using/identity.html){target="_blank"}を実装して Campaign に接続する必要があります。

この移行について詳しくは、[このページ](ac-ims.md)を参照してください。

## 変更点 {#move-to-ims-changes}

Campaign Classic では、すべての標準ユーザーは、Adobe Identity Management System（IMS）により、Adobe ID を使用して Adobe Campaign クライアントコンソールに既に接続しています。 ただし、ユーザー名とパスワードでの接続は引き続き可能です。 これは、Campaign v8 以降では使用できなくなります。

さらに、セキュリティと認証プロセスを強化する取り組みの一環として、Adobe Campaign クライアントアプリケーションは、IMS テクニカルアカウントトークンを使用して Campaign API を直接呼び出すようになりました。 テクニカルオペレーターの移行について詳しくは、[このページ](ims-migration.md)にある専用の記事を参照してください。

この変更は Campaign Classic v7 で既に適用されており、Campaign v8 に移行するためには&#x200B;**必須**&#x200B;となります。

アドビでは、この移行作業をサポートしています。 詳細なコンテキストと段階的なガイドラインについては、以下の記事を参照してください。

## 影響の有無{#migrate-ims-impacts}

この手順は、まだ Adobe ID を使用して Campaign に接続していないすべての Campaign ユーザーに適用されます。

組織内のオペレーターが Campaign クライアントコンソールにログイン／パスワード（別名 ネイティブ認証）影響を受けるので、以下で説明するようにこれらのオペレーターを Adobe IMS に移行する必要があります。

[Adobe Identity Management System（IMS）](https://helpx.adobe.com/jp/enterprise/using/identity.html){target="_blank"}への移行は環境のセキュリティを確保し、標準化するのに不可欠なセキュリティです。他の Adobe Experience Cloud ソリューションおよびアプリのほとんどは既に IMS に準拠しています。

この変更は、Campaign Classic v7.4.1（および最新の [IMS 移行互換バージョン](ac-ims.md#ims-versions)）以降に適用され、Adobe Campaign v8 に移行するには&#x200B;**必須**&#x200B;となります。

>[!IMPORTANT]
>
>**コントロールパネルアクセスの影響**
>
>ユーザーを IMS に移行すると、Adobe Admin Console 内の製品プロファイルの名前（「Administrators」、「admin」、「admins」、「approval admin」など）に「admin」という単語が含まれている場合、 Campaign コントロールパネルへのアクセス権は自動的に付与されることに注意してください。 Campaign コントロールパネルは、Campaign インスタンスに大きな変更を加えることができるセルフサービスツールです。
>
>製品プロファイルの命名規則を慎重に確認し、許可されたユーザーのみが コントロールパネルにアクセスできるようにします。 コントロールパネル権限の管理について詳しくは、[コントロールパネルドキュメント](https://experienceleague.adobe.com/docs/control-panel/using/discover-control-panel/managing-permissions.html?lang=ja){target="_blank"}を参照してください。


## ハイブリッド環境とオンプレミス環境を移行する方法 {#ims-migration-procedure-on-prem}

この移行の主な手順を以下に示します。

1. 環境を Campaign v7.4.1（または [IMS 移行互換バージョン](#ims-versions)）にアップグレードします。
1. アップグレード後も、ネイティブユーザーまたは IMS の両方の方法で新しいユーザーを引き続き作成できます。
1. 社内 Campaign 管理者の方は、[このセクション](../../integrations/using/configuring-ims.md)の説明に従い、Adobe IMS を構成する必要があります。
1. 次に、Campaign クライアントコンソールで、すべてのネイティブユーザーに一意の E メールを追加します。 この手順について詳しくは、[この節](https://experienceleague.adobe.com/ja/docs/campaign/technotes-ac/tn-new/migrate-users-to-ims#ims-migration-id){target="_blank"}（Campaign v8 ドキュメント）を参照してください。
1. [Campaign v8 ドキュメント](https://experienceleague.adobe.com/docs/campaign/campaign-v8/admin/permissions/manage-permissions.html?lang=ja){target="_blank"}を参照して、Adobe Admin Console でユーザーおよび製品プロファイルを作成します。
1. すべてのオペレーターに対して「**Adobe ID を使用して接続**」オプションを有効にします。
1. 接続に対して Adobe IMS を実装するには、[このページ](../../integrations/using/implementing-ims.md)を参照してください。

また、テクニカルオペレーターを Adobe Developer Console に移行することもできます。詳しくは、[このテクニカルノート](ims-migration.md)を参照してください。

## よくある質問 {#ims-migration-faq}

移行に関するよくある質問（移行後のユーザー作成、ネイティブユーザーのメールアドレスの追加、IMS 経由でのログイン、ダウンタイム、IMS を既に使用している組織、オペレーターの認証タイプの表示）への回答については、[Campaign v8 テクニカルノート](https://experienceleague.adobe.com/ja/docs/campaign/technotes-ac/tn-new/migrate-users-to-ims#ims-migration-faq){target=_blank}（Campaign v8 ドキュメント）を参照してください。

>[!MORELIKETHIS]
>
>* [Adobe Developer Console へのテクニカルユーザーの移行](ims-migration.md)
>* [Adobe Campaign Classic v7 リリースノート](../../rn/using/latest-release.md)
>* [Adobe Identity Management System（IMS）とは](https://helpx.adobe.com/jp/enterprise/using/identity.html){target="_blank"}
