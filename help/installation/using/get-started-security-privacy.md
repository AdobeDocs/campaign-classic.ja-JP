---
solution: Campaign Classic
product: campaign
title: セキュリティとプライバシーの基本を学ぶ
description: セキュリティとプライバシーに関する主要な要素についての詳細。
audience: installation
content-type: reference
topic-tags: prerequisites-and-recommendations-
translation-type: tm+mt
source-git-commit: 922603492d2c98d751683d3aa481e9ab19bca70c
workflow-type: tm+mt
source-wordcount: '450'
ht-degree: 56%

---


# セキュリティとプライバシーの基本を学ぶ {#get-started-security-privacy}

このセクションでは、セキュリティとプライバシーに関する確認が必要な主要要素について説明します。 一部の設定は、オンプレミスのお客様のみが実行できます。

## プライバシー

<img src="assets/do-not-localize/icon_privacy.svg" width="60px">

プライバシー設定と強化は、セキュリティを最適化するうえで重要な要素です。プライバシーに関するベストプラクティスをいくつか示します。

* HTTP ではなく HTTPS を使用して、お客様の PII を保護します
* PII 閲覧の制限を使用してプライバシーを保護し、データの乱用を防止します。
* 暗号化されたパスワードが制限されていることを確認します。
* ミラーページや Web アプリケーションのように、個人情報を含む可能性があるページを保護します。

[詳細情報](../../installation/using/privacy.md)

## アクセス管理

<img src="assets/do-not-localize/icon_access.svg" width="60px">

アクセス管理は、セキュリティ強化の重要な要素です。ここでは、主なベストプラクティスを紹介します。

* 十分なセキュリティグループを作成する
* 各オペレーターのアクセス権が適切であることをチェックする
* 管理オペレーターを使用しないようにし、さらに管理グループのオペレーターが多くなりすぎないようにする

[詳細情報](../../installation/using/access-management.md)

## スクリプトとコーディングのガイドライン

<img src="assets/do-not-localize/icon_scripting.svg" width="60px">

Adobe Campaign(ワークフロー、JavaScript、JSSPなど)で開発する場合は、次のガイドラインに従ってください。

* **スクリプティング**：SQL 文は使用しないようにします。文字列連結ではなく、パラメーター化関数を使用します。使用する SQL 関数を許可リストに追加して、SQL インジェクションを回避します。

* **データモデルの保護**:ネームド権限を使用して演算子のアクションを制限し、システム・フィルターを追加(sysFilter)

* **Webアプリケーション追加でのcaptchas**:パブリックランディングページと購読ページにcaptchaを追加する方法を説明します。

[詳細情報](../../installation/using/scripting-coding-guidelines.md)

## ネットワーク、データベース、SSL/TLS

<img src="assets/do-not-localize/icon_network.svg" width="60px">

オンプレミス型のアーキテクチャをデプロイする際にチェックすべき最も重要な要素は、ネットワーク設定です。

また、データベースエンジンのセキュリティに従う必要があります。

[詳細情報](../../installation/using/network-database.md)

## サーバー設定

<img src="assets/do-not-localize/icon_server.svg" width="60px">

設定は、すべてのサーバーでおこなう必要があります。設定ファイルの種類は&#x200B;**serverConf.xml**&#x200B;と&#x200B;**`config-<instance>.xml`**&#x200B;です。 次に、確認する必要がある重要な要素を示します。

* **セキュリティゾーン**:プロキシのクライアントのIPアドレスを直接考慮するように、セキュリティゾーンを設定します。

* **ファイルのアップロード保護**:新しいuploadAllowList属性を使用して、Adobe Campaignサーバにアップロードできるファイルの種類を制限します。これは、サーバー設定ファイルで使用できます。

* **リレー**：使用していないモジュール／アプリケーションのリレールールを無効にして、リレー設定を微調整します。

* **送信接続の保護**&#x200B;と&#x200B;**コマンドの制限**（サーバー側）

* また、HTTP ヘッダーを追加したり、checkIPConsistent、enableTLS、sessionTimeOutSec などを有効にしたりすることもできます。詳細については、[キャンペーンサーバー設定ドキュメント](../../installation/using/configuring-campaign-server.md)および[サーバー設定ファイルの説明](../../installation/using/the-server-configuration-file.md)を参照してください。

[詳細情報](../../installation/using/server-configuration.md)

## Web サーバー設定

<img src="assets/do-not-localize/icon_web.svg" width="60px">

Webサーバー(Apache/IIS)を設定する際は、次のいくつかのベストプラクティスに従う必要があります。

* 古い SSL のバージョンと暗号を無効にする
* TRACEメソッドの削除
* バナーを削除します。
* 重要なファイルがアップロードされないようにクエリサイズを制限する

[詳細情報](../../installation/using/web-server-configuration.md)
