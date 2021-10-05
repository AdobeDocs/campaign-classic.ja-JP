---
product: campaign
title: セキュリティとプライバシーのチェックリスト
description: セキュリティとプライバシーに関して確認すべき重要な要素について詳しく説明します。
audience: installation
content-type: reference
topic-tags: prerequisites-and-recommendations-
exl-id: ec40498e-e673-4792-8dcf-8bb7e852b532
source-git-commit: 0c97efef21bfd3b8671847c3e1c27bb76cf167e4
workflow-type: tm+mt
source-wordcount: '486'
ht-degree: 54%

---

# セキュリティとプライバシーのチェックリスト{#get-started-security-privacy}

![](../../assets/v7-only.svg)

この節では、セキュリティとプライバシーに関して確認すべき重要な要素について説明します。 一部の設定はオンプレミスのお客様のみ実行できます。

## プライバシー

<img src="assets/do-not-localize/icon_privacy.svg" width="60px">

プライバシー設定と強化は、セキュリティを最適化するうえで重要な要素です。 プライバシーに関するベストプラクティスをいくつか示します。

* HTTP ではなく HTTPS を使用して、お客様の PII を保護します
* PII 閲覧の制限を使用してプライバシーを保護し、データの乱用を防止します。
* 暗号化されたパスワードが制限されていることを確認する.
* ミラーページや Web アプリケーションなどのように、個人情報を含む可能性があるページを保護します。

[詳細情報](../../installation/using/privacy.md)

## アクセス管理

<img src="assets/do-not-localize/icon_access.svg" width="60px">

アクセス管理は、セキュリティ強化の重要な部分です。 ここでは、主なベストプラクティスを紹介します。

* 十分なセキュリティグループを作成する
* 各オペレーターのアクセス権が適切であることを確認する
* 管理オペレーターの使用を避け、管理グループのオペレーターが多くなりすぎないようにする

[詳細情報](../../installation/using/access-management.md)

## スクリプトとコーディングのガイドライン

<img src="assets/do-not-localize/icon_scripting.svg" width="60px">

Adobe Campaign（ワークフロー、JavaScript、JSSP など）で開発する場合、常に次のガイドラインに従います。

* **スクリプティング**:SQL 文を避けるには、文字列連結の代わりにパラメータ化関数を使用し、使用する SQL 関数をパラメータに追加して SQL インジェクションを避け許可リストます。

* **データモデルの保護**：ネームド権限を使用してオペレーターのアクションを制限し、システムフィルター（sysFilter）を追加します

* **Web アプリケーションに Captcha を追加**:パブリックのランディングページとサブスクリプションページに captcha を追加する方法を説明します。

[詳細情報](../../installation/using/scripting-coding-guidelines.md)

## ネットワーク、データベース、SSL/TLS

<img src="assets/do-not-localize/icon_network.svg" width="60px">

オンプレミス型のアーキテクチャをデプロイする際にチェックすべき最も重要な要素は、ネットワーク設定です。

また、データベースエンジンのセキュリティに従うことも必須です。

[詳細情報](../../installation/using/network-database.md)

>[!CAUTION]
>
>2021 年 7 月 14 日以降、TLS 1.2 プロトコルをサポートしないクライアントシステムは、すべてのAdobe製品およびサービスへのアクセスを失います。 この日より前に、すべてのユーザーおよびクライアントシステムが TLS 1.2 に準拠していることを確認してください。 [詳細情報](https://helpx.adobe.com/x-productkb/multi/eol-tls-support.html)

## サーバー設定

<img src="assets/do-not-localize/icon_server.svg" width="60px">

設定は、すべてのサーバーでおこなう必要があります。設定ファイルのタイプは **serverConf.xml** と **`config-<instance>.xml`** です。 次に、確認する必要がある重要な要素を示します。

* **セキュリティゾーン**:プロキシのクライアントの IP アドレスを直接考慮するように、セキュリティゾーンを設定します。

* **ファイルのアップロード保護**:新しい uploadAllowList 属性を使用して、Adobe Campaignサーバーにアップロードできるファイルのタイプを制限します。これは、サーバー設定ファイルで使用できます。

* **リレー**：使用していないモジュール／アプリケーションのリレールールを無効にして、リレー設定を微調整します。

* **送信接続の保護**&#x200B;と&#x200B;**コマンドの制限**（サーバー側）

* また、HTTP ヘッダーを追加したり、checkIPConsistent、enableTLS、sessionTimeOutSec などを有効にしたりすることもできます。詳しくは、[Campaign サーバーの設定に関するドキュメント ](../../installation/using/configuring-campaign-server.md) および [ サーバーの設定ファイルに関する説明 ](../../installation/using/the-server-configuration-file.md) を参照してください。

[詳細情報](../../installation/using/server-configuration.md)

## Web サーバー設定

<img src="assets/do-not-localize/icon_web.svg" width="60px">

Web サーバー (Apache/IIS) を設定する際は、次のベストプラクティスに従う必要があります。

* 古い SSL のバージョンと暗号を無効にする
* メソッドのTRACE
* バナーを削除します。
* クエリのサイズを制限して、重要なファイルがアップロードされないようにする

[詳細情報](../../installation/using/web-server-configuration.md)
