---
title: AdobeのIdentity Management System （IMS）への移行
description: AdobeIdentity Management System （IMS）に認証プロセスを移行する方法について説明します
source-git-commit: 106f0409f452595209f0e2aa2fa187a2e04338a9
workflow-type: tm+mt
source-wordcount: '454'
ht-degree: 27%

---

# AdobeのIdentity Management System （IMS）への移行 {#migrate-to-ims}

セキュリティと認証プロセスを強化する取り組みの一環として、Adobe Campaignではエンドユーザー認証モードをログイン/パスワードネイティブ認証からに移行することを強くお勧めします [AdobeIdentity Managementシステム（IMS）](https://helpx.adobe.com/jp/enterprise/using/identity.html){target="_blank"}.

さらに、Adobe Campaign クライアントアプリケーションは、IMS テクニカルアカウントトークンを使用して Campaign API を直接呼び出すようになりました。 テクニカルオペレーターをAdobe Developer コンソールに移行する必要があります。

>[!CAUTION]
>
>この変更は、Campaign Classic v7 に既に適用されており、次のようになります **mandatory** を Campaign v8 に移行します。 Campaign v8 では、ネイティブのユーザー/パスワード認証は許可されていません。 **Adobeは、Campaign v8 にスムーズに移行できるように、Campaign v7.3.5 以降で、この移行を実行することをお勧めします。**
>

## 移行手順 {#ims-steps}

[Adobe Identity Management System（IMS）](https://helpx.adobe.com/jp/enterprise/using/identity.html){target="_blank"}への移行は、他の Adobe Experience Cloud ソリューションやアプリのほとんどは既に IMS 上にあるので、環境を安全かつ標準化するためにセキュリティ上不可欠です。

アドビでは、この移行作業をサポートしています。以下の記事に、詳細なコンテキストと手順に関するガイドラインが記載されています。

* エンドユーザー認証の移行について詳しくは、こちらを参照してください [このページ](migrate-users-to-ims.md).
* テクニカルオペレーター認証の移行について詳しくは、こちらを参照してください [このページ](ims-migration.md).
* Campaign v7.4.1 以降では、以下に説明するように、ユーザーインターフェイスと API 制限を有効にして、ネイティブ認証に固有のオプションと機能を削除します。 [このページ](impact-ims-migration.md).


## IMS 移行互換バージョン {#ims-versions}

この移行の前提条件は、環境を次のいずれかの製品バージョンにアップグレードすることです。

* Campaign v7.4.1 （推奨）
* Campaign v7.3.5
* Campaign v7.3.3.IMS
* Campaign v7.3.2.IMS

これらの Campaign のバージョンについて詳しくは、[リリースノート](../../rn/using/latest-release.md)を参照してください。

## よくある質問 {#ims-migration-faq}

### 移行を開始できるのはいつですか？ {#ims-migration-start}

への移行に関する推奨事項 [AdobeIdentity Managementシステム（IMS）](https://helpx.adobe.com/jp/enterprise/using/identity.html){target="_blank"} お使いの環境をCampaign Classic v7.4.1 （または [IMS 移行互換バージョン](#ims-versions)）に設定します。

最新バージョンにアップグレードしたら、ステージング環境で IMS への移行を開始し、それに応じて実稼動環境を計画できます。

### Campaign Classic v7.4.1 へのビルドアップグレード後、どうなりますか？ {#ims-migration-after-upgrade}

Campaign Classicが環境 v7.4.1 （または [IMS 移行互換バージョン](#ims-versions)）、への移行を開始できます。 [AdobeIdentity Managementシステム（IMS）](https://helpx.adobe.com/jp/enterprise/using/identity.html){target="_blank"}.

### 移行が完了するのはいつですか？ {#ims-migration-end}

エンドユーザーの移行とテクニカルオペレーターのAdobeIdentity Management System （IMS）への移行が完了したら、環境を更新して、ネイティブ認証に固有で IMS 認証では適用されないオプションを削除する必要があります。 この更新は、Campaign v7.4.1 以降でのみ使用できます。 [詳細情報](impact-ims-migration.md)



## 便利なリンク {#ims-useful-links}

* [エンドユーザーの IMS への移行](migrate-users-to-ims.md)
* [Adobe Developer コンソールへのテクニカルオペレーターの移行](ims-migration.md)
* [Adobe Campaign Classic v7 の最新のリリースノート](../../rn/using/latest-release.md)
* [Adobe Identity Management System（IMS）とは](https://helpx.adobe.com/jp/enterprise/using/identity.html){target="_blank"}
