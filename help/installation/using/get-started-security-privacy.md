---
product: campaign
title: セキュリティとプライバシーのチェックリスト
description: セキュリティとプライバシーに関する重要な要素について詳しく見る
feature: Installation, Privacy, Access Management, Privacy Tools
audience: installation
content-type: reference
topic-tags: prerequisites-and-recommendations-
exl-id: ec40498e-e673-4792-8dcf-8bb7e852b532
TQID: https://experienceleague.adobe.com/UvWC8wEoOcNmpLClAoF-pK8WaPNZTzoLbGaF6nwUKDw
product_v2: id: dfc56824-e8b9-499e-85d4-21aedb507314
feature_v2: id: a7760dfc-5c44-4d77-bb68-c50b1e265c93
subfeature_v2: id: ac72e249-ebbf-4bb6-96c9-596af925419aid: ac9c0a9c-8a76-4419-bd64-9c34c5782666id: fb2a841f-c522-491f-9901-a1b939d252df
topic_v2: id: cdd65e7e-8839-44a2-bc21-0e03623b5dd1id: d095671a-1355-40aa-8b5f-06c33c68080bid: e0eb8757-182f-49f3-94a4-1587d16f5094id: f4e6943a-c91a-4134-a2c7-f4f20cfff2f0
source-git-commit: 4c295c0dabae8aba298390a3da2422a3fa1219f9
workflow-type: tm+mt
source-wordcount: 450
ht-degree: 52%

---

# セキュリティとプライバシーのチェックリスト{#get-started-security-privacy}



このセクションでは、セキュリティとプライバシーに関して確認すべき重要な要素について紹介します。 一部の設定は、オンプレミスのお客様のみが実行できます。

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

* **スクリプト**: SQL ステートメントを避け、文字列の連結の代わりにパラメーター化された関数を使用し、SQL関数を追加してSQL 許可リストに使用することでSQL インジェクションを避けます。

* **データモデルの保護**：ネームド権限を使用してオペレーターのアクションを制限し、システムフィルター（sysFilter）を追加します

* **Web アプリケーションでキャプチャを追加**：公開ランディングページとサブスクリプションページでキャプチャを追加する方法について説明します。

[詳細情報](../../installation/using/scripting-coding-guidelines.md)

## ネットワーク、データベース、SSL/TLS

<img src="assets/do-not-localize/icon_network.svg" width="60px">

オンプレミス型のアーキテクチャをデプロイする際にチェックすべき最も重要な要素は、ネットワーク設定です。

また、データベースエンジンのセキュリティを遵守することも不可欠です。

[詳細情報](../../installation/using/network-database.md)


## サーバー設定

<img src="assets/do-not-localize/icon_server.svg" width="60px">

すべてのサーバーで設定を実行する必要があります。 設定ファイルのタイプは&#x200B;**serverConf.xml**&#x200B;および&#x200B;**`config-<instance>.xml`**&#x200B;です。 次に、確認する必要がある重要な要素を示します。

* **セキュリティゾーン**: プロキシのクライアントのIP アドレスを直接考慮するようにセキュリティゾーンを設定します。

* **ファイルアップロード保護**：新しいuploadAllowList属性を使用して、Adobe Campaign サーバーにアップロードできるファイルの種類を制限します。 これは、サーバー設定ファイルで使用できます。

* **リレー**：使用していないモジュール／アプリケーションのリレールールを無効にして、リレー設定を微調整します。

* **送信接続保護**&#x200B;および&#x200B;**コマンド制限** （サーバーサイド）

* 追加のHTTP ヘッダーを追加したり、checkIPConsistentをアクティブ化したり、enableTLS、sessionTimeOutSecなどを実行することもできます。詳しくは、[Campaign サーバー設定ドキュメント ](../../installation/using/configuring-campaign-server.md)および[ サーバー設定ファイルの説明](../../installation/using/the-server-configuration-file.md)を参照してください。

[詳細情報](../../installation/using/server-configuration.md)

## Web サーバーの設定

<img src="assets/do-not-localize/icon_web.svg" width="60px">

Web サーバー（Apache/IIS）を設定する際には、いくつかのベストプラクティスに従う必要があります。

* 古い SSL のバージョンと暗号を無効にする
* TRACE メソッドの削除
* バナーを削除します。
* 重要なファイルがアップロードされないように、クエリサイズを制限する

[詳細情報](../../installation/using/web-server-configuration.md)
