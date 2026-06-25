---
title: Adobe Identity Management System（IMS）への移行
description: 認証プロセスを Adobe Identity Management System（IMS）へ移行する方法を学ぶ
exl-id: 84853dbe-8b6f-4875-b29a-c1b755423a3c
TQID: https://experienceleague.adobe.com/DKwv-rLrgm0ce9cycT1QMtBgQP-2pnMNhqHlH1xJWvo
product_v2:
  - id: dfc56824-e8b9-499e-85d4-21aedb507314
feature_v2:
  - id: b12f6872-9271-4369-85e5-86969a0b99a2
topic_v2:
  - id: d095671a-1355-40aa-8b5f-06c33c68080b
subfeature_v2:
  - id: cbcf4d90-26be-46e2-b16a-aebc529dc41e
source-git-commit: 38eab6b8da73163e4476e91c0ef73f25c3f57546
workflow-type: ht
source-wordcount: 479
ht-degree: 100%

---

# Adobe Identity Management System（IMS）への移行 {#migrate-to-ims}

セキュリティと認証プロセスを強化する取り組みの一環として、Adobe Campaign では、エンドユーザー認証モードをログイン/パスワードネイティブ認証から [Adobe Identity Management System（IMS）](https://helpx.adobe.com/jp/enterprise/using/identity.html){target="_blank"}に移行することを強くお勧めしています。

さらに、Adobe Campaign クライアントアプリケーションは、IMS テクニカルアカウントトークンを使用して Campaign API を直接呼び出すようになりました。 テクニカルオペレーターを Adobe Developer Console に移行してください。

>[!CAUTION]
>
>この変更は Campaign Classic v7 で既に適用されており、Campaign v8 に移行するためには&#x200B;**必須**&#x200B;となります。 Campaign v8 では、ネイティブのユーザー／パスワード認証は許可されていません。 **アドビでは、Campaign v8 にスムーズに移行できるように、Campaign v7.3.5 でこの移行を実行することをお勧めします。**
>

## 移行手順 {#ims-steps}

[Adobe Identity Management System（IMS）](https://helpx.adobe.com/jp/enterprise/using/identity.html){target="_blank"}への移行は環境のセキュリティを確保し、標準化するために不可欠なセキュリティです。他の Adobe Experience Cloud ソリューションおよびアプリのほとんどは既に IMS に準拠しています。

アドビでは、この移行作業をサポートしています。 詳細なコンテキストと段階的なガイドラインについては、以下の記事を参照してください。

* エンドユーザー認証の移行について詳しくは、[このページ](migrate-users-to-ims.md)を参照してください。
* テクニカルオペレーター認証の移行について詳しくは、[このページ](ims-migration.md)を参照してください。
* Campaign v7.4.1 以降では、[このページ](impact-ims-migration.md)で説明されているように、ユーザーインターフェイスと API 制限を有効にして、ネイティブ認証に固有のオプションと機能を削除します。


## IMS 移行互換バージョン {#ims-versions}

この移行の前提条件は、環境を次のいずれかの製品バージョンにアップグレードすることです。

* Campaign v7.4.1（推奨）
* Campaign v7.3.5
* Campaign v7.3.3.IMS
* Campaign v7.3.2.IMS

これらの Campaign のバージョンについて詳しくは、[リリースノート](../../rn/using/latest-release.md)を参照してください。

## よくある質問 {#ims-migration-faq}

### 移行を開始できるのはいつですか？ {#ims-migration-start}

[Adobe Identity Management System（IMS）](https://helpx.adobe.com/jp/enterprise/using/identity.html){target="_blank"}への移行の推奨事項は、環境を Campaign Classic v7.4.1（または [IMS 移行互換バージョン](#ims-versions)）にアップグレードすることです。

最新バージョンにアップグレードしたら、ステージング環境で IMS への移行を開始し、それに応じて本番環境を計画できます。

### Campaign Classic v7.4.1 にビルドをアップグレードすると、どうなりますか？ {#ims-migration-after-upgrade}

環境を Campaign Classic v7.4.1（または [IMS 移行互換バージョン](#ims-versions)）にアップグレードしたら、[Adobe Identity Management System（IMS）](https://helpx.adobe.com/jp/enterprise/using/identity.html){target="_blank"}への移行を開始できます。

### 移行が完了するのはいつですか？ {#ims-migration-end}

エンドユーザーの移行とテクニカルオペレーターを Adobe Identity Management System（IMS）に移行する処理が完了したら、環境を更新して、ネイティブ認証に固有で IMS 認証では適用されないオプションを削除する必要があります。 この更新は、Campaign v7.4.1 以降でのみ使用できます。[詳細情報](impact-ims-migration.md)



## 便利なリンク {#ims-useful-links}

* [エンドユーザーの IMS への移行](migrate-users-to-ims.md)
* [Adobe Developer Console へのテクニカルオペレーターの移行](ims-migration.md)
* [Adobe Campaign Classic v7 最新リリースノート](../../rn/using/latest-release.md)
* [Adobe Identity Management System（IMS）とは](https://helpx.adobe.com/jp/enterprise/using/identity.html){target="_blank"}
