---
product: campaign
title: セキュリティとプライバシーのチェックリスト
description: セキュリティとプライバシーに関して確認する必要がある主な要素について詳しく説明します
feature: Installation, Privacy, Access Management, Privacy Tools
audience: installation
content-type: reference
topic-tags: prerequisites-and-recommendations-
exl-id: ec40498e-e673-4792-8dcf-8bb7e852b532
source-git-commit: 19b40f0b827c4b5b7b6484fe4953aebe61d00d1d
workflow-type: tm+mt
source-wordcount: '445'
ht-degree: 52%

---

# セキュリティとプライバシーのチェックリスト{#get-started-security-privacy}



ここでは、セキュリティとプライバシーに関して確認する必要のある主な要素を紹介します。 一部の設定は、オンプレミスのお客様のみが実行できます。

## プライバシー

<img src="assets/do-not-localize/icon_privacy.svg" width="60px">

プライバシー設定と強化は、セキュリティを最適化するうえで重要な要素です。 プライバシーに関するベストプラクティスをいくつか示します。

* HTTP ではなく HTTPS を使用して、お客様の PII を保護します
* PII 閲覧の制限を使用してプライバシーを保護し、データの乱用を防止します。
* 暗号化されたパスワードが制限されていることを確認します。
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

* **スクリプティング**:SQL 文を避け、文字列の連結の代わりに、パラメーター化関数を使用し、使用する SQL 関数を許可リストに追加して SQL 挿入を避けます。

* **データモデルの保護**：ネームド権限を使用してオペレーターのアクションを制限し、システムフィルター（sysFilter）を追加します

* **Web アプリケーションへの captcha の追加**：公開ランディングページと購読ページで captcha を追加する方法を説明します。

[詳細情報](../../installation/using/scripting-coding-guidelines.md)

## ネットワーク、データベース、SSL/TLS

<img src="assets/do-not-localize/icon_network.svg" width="60px">

オンプレミス型のアーキテクチャをデプロイする際にチェックすべき最も重要な要素は、ネットワーク設定です。

また、データベースエンジンのセキュリティに従う必要もあります。

[詳細情報](../../installation/using/network-database.md)


## サーバー設定

<img src="assets/do-not-localize/icon_server.svg" width="60px">

設定はすべてのサーバーで実行する必要があります。 設定ファイルのタイプはです **serverConf.xml** および **`config-<instance>.xml`**. 次に、確認する必要がある重要な要素を示します。

* **セキュリティゾーン**：セキュリティゾーンを設定して、プロキシのクライアントの IP アドレスを直接考慮するようにします。

* **ファイルのアップロード保護**：新しい uploadAllowList 属性を使用して、Adobe Campaign サーバーにアップロードできるファイルのタイプを制限します。 これは、サーバー設定ファイルで使用できます。

* **リレー**：使用していないモジュール／アプリケーションのリレールールを無効にして、リレー設定を微調整します。

* **発信接続の保護** および **コマンドの制限** （サーバーサイド）

* また、追加の HTTP ヘッダーを追加したり、checkIPConsistent、enableTLS、sessionTimeOutSec などを有効化することもできます。 を参照してください。 [Campaign サーバー設定ドキュメント](../../installation/using/configuring-campaign-server.md) および [サーバー設定ファイルの説明](../../installation/using/the-server-configuration-file.md) を参照してください。

[詳細情報](../../installation/using/server-configuration.md)

## Web サーバーの設定

<img src="assets/do-not-localize/icon_web.svg" width="60px">

Web サーバー（Apache/IIS）を設定する際は、次のベストプラクティスに従う必要があります。

* 古い SSL のバージョンと暗号を無効にする
* TRACE方式を削除する
* バナーを削除します。
* 重要なファイルがアップロードされないようにクエリサイズを制限

[詳細情報](../../installation/using/web-server-configuration.md)
