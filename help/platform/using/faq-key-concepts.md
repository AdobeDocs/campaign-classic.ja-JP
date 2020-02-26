---
title: 重要な概念
seo-title: キャンペーンの機能に関するFAQ
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
source-git-commit: 8ef56aa04a3ecc94e9e3dda24562760d6a93739d

---


# 重要な概念 {#key-concepts}

Adobe Campaign を導入するための重要な手順を学習します。

## Can I connect to Campaign Classic with an Adobe ID? {#can-i-connect-to-campaign-classic-with-an-adobe-id-}

IMS（Adobe Identity Management System）との統合により、ユーザーは Adobe ID を使用して Adobe Campaign コンソールに接続できます。統合には次のメリットがあります。

* Experience Cloud のすべてのソリューションに同じ ID を使用できます。
* Adobe Campaign で異なる統合を使用する場合にも、接続が記憶されます。
* パスワード管理ポリシーをよりセキュアにできます。
* フェデレーション ID アカウント（外部の ID プロバイダー）を使用します。

Adobe ID を使用した Campaign Classic へのアクセスについて[詳しくは、ここをクリック](../../integrations/using/about-adobe-id.md)してください。

## What is my version of Campaign? {#what-is-my-version-of-campaign-}

Campaign クライアントコンソールの&#x200B;**ヘルプ／バージョン情報...**&#x200B;メニューで、お使いの[バージョンおよびビルド番号](../../platform/using/launching-adobe-campaign.md#getting-your-campaign-version)を確認できます。

## What are the differences when working on-premise vs. in a hosted environment? {#what-are-the-differences-when-working-on-premise-vs--in-a-hosted-environment-}

Adobe Campaign Classic には一連のモジュールとオプションが付属しています。これらのモジュールの使用可否と設定は、インストール構成の[デプロイメントタイプ](../../installation/using/hosting-models.md)がホスト（マネージドサービス）であるかオンプレミスであるかによって異なります。

[詳しくはここをクリック](https://helpx.adobe.com/campaign/kb/acc-on-prem-vs-hosted.html)してください。

## How can I set up user permissions? {#how-can-i-set-up-user-permissions-}

Campaign 管理者は、組織のユーザーに対して権限を設定できます。

一連の権限および制限により、承認または拒否される操作を以下に示します。

* 特定の機能へのアクセス
* 特定のデータへのアクセス
* データの作成、変更、削除

ユーザー権限について[詳しくは、ここをクリック](../../platform/using/access-management.md)してください。

## Campaignのプライバシーコンプライアンスを確保する方法 {#how-to-be-gdpr-compliant-with-campaign-}

Adobe Campaignは、GDPRおよびCCPAのプライバシーコンプライアンスを支援するツールのセットを提供しています。

[このドキュメント](https://helpx.adobe.com/campaign/kb/campaign-privacy-overview.html)を参照して、Adobe Campaign のツールと機能、ベストプラクティスについて把握し、GDPR を遵守しながらアドビのサービスを利用する方法を学んでください。Campaign Classicの導入手順についてこの記事で説 [明します](https://helpx.adobe.com/campaign/kb/acc-privacy.html)。

## What are Campaign user interface concepts I should know? {#what-are-campaign-user-interface-concepts-i-should-know-}

Adobe Campaign ワークスペースの基本事項について詳しくは、[この節](../../platform/using/adobe-campaign-workspace.md)を参照してください。[このビデオ](https://docs.adobe.com/content/help/en/campaign-learn/campaign-classic-tutorials/getting-started/interface-overview.html)もご覧ください。

## How can I select the audience of my messages? {#how-can-i-select-the-target-population-of-my-messages-}

Adobe Campaign では、各種の戦略を使用してオーディエンスの作成とターゲット受信者の選択をおこなうことができます。

[詳しくはここをクリック](../../delivery/using/steps-defining-the-target-population.md)してください。

## What is a workflow? {#what-is-a-workflow-}

Adobe Campaign には、アプリケーションサーバーの様々なモジュール間でプロセスおよびタスク全体にわたる調整をおこなうワークフローモジュールが含まれています。この包括的なグラフィカル環境を使用すると、セグメント化、キャンペーン実行、ファイル処理、人の参加などを含むプロセスを設計できます。ワークフローエンジンは、これらのプロセスを実行およびトラッキングします。

例えば、ワークフローを使用して、サーバーからファイルをダウンロードしたり、ファイルを解凍したり、ファイルに含まれるレコードを Adobe Campaign データベースにインポートしたりできます。

また、通知したり、プロセスを選択および承認したりできる 1 人または複数のオペレーターをワークフローに参加させることもできます。この方法では、配信アクションを作成し、1 人または複数のオペレーターにタスクを割り当てて、コンテンツに取り組んだり、ターゲットを指定したり、配信開始前に配達確認を承認したりできます。

ワークフローについて[詳しくはここをクリック](../../workflow/using/about-workflows.md)してください。「[ワークフローのベストプラクティス](../../workflow/using/building-a-workflow.md)」も参照してください。

## How to create and send a first email? {#how-to-create-and-send-a-first-email-}

[詳しくはここをクリック](../../delivery/using/about-email-channel.md)するか、キャンペーンでの E メールの作成方法に関する[このビデオを閲覧](https://docs.adobe.com/content/help/en/campaign-learn/campaign-classic-tutorials/getting-started/creating-a-campaign-and-an-email.html)してください。

## How to send SMS messages? {#how-to-send-sms-messages-}

プラットフォームを設定して SMS メッセージを送信する方法については、[この節](../../delivery/using/sms-channel.md)を参照してください。

## How to send push notifications? {#how-to-send-push-notifications-}

Adobe Campaign を使用すると、アプリを介して iOS および Android 端末に[パーソナライズされたプッシュ通知を送信](../../delivery/using/creating-notifications.md)できます。

## How to design and share an online survey? {#how-to-design-and-share-an-online-survey-}

[オンライン調査を作成](../../web/using/getting-started-with-surveys.md)する方法として、Campaign Classic でオンライン調査を設計してパブリッシュする重要な手順があります。

## How to create landing page? {#how-to-create-landing-page-}

Adobe Campaign デジタルコンテンツエディターを使用すると、ランディングページを作成してデータベースフィールドとのマッピングを定義することができます。

[詳しくはここをクリック](../../web/using/creating-a-landing-page.md)してください。

## How can I track deliveries? {#how-can-i-track-deliveries-}

Campaign Classic で送られた配信を専用の[配信レポート](../../reporting/using/delivery-reports.md)によってトラッキングし、さらに配信を監視することができます。

キャンペーンのトラッキング管理について詳 [しくは](https://helpx.adobe.com/campaign/kb/acc-tracking.html)、

## What are security best practices (on-premise)? {#what-are-security-best-practices--on-premise--}

[セキュリティ設定チェックリスト](https://helpx.adobe.com/campaign/kb/acc-security.html)により、オンプレミスデプロイメントのためのセキュリティ設定と強化に関して確認すべき重要な要素を理解できます。

## How to translate an error message? {#how-to-translate-an-error-message-}

エラーメッセージが外国語で表示されましたか？すべてのエラーメッセージとその翻訳のリストは、[このページ](https://docs.campaign.adobe.com/doc/AC/en/technicalResources/error_messages/error_codes.html)に掲載されています。

## Can I create a webform and collect answers in Campaign? {#can-i-create-a-webform-and-collect-answers-in-campaign-}

Webフォームの作 [成方法を説明します](../../web/using/about-web-forms.md)。Webフォームのデザイン、テスト、発行、回答の収集を行います。

## Is there a list of deprecated features and versions? {#is-there-a-list-of-deprecated-features-and-versions-}

アドビでは、製品の機能を継続的に評価し、各機能をより効果的なバージョンで置き換えるために長期的な計画を策定したり、将来の期待や拡張に備えるために選択したパーツの再実装を決定したりしています。Campaign はサードパーティ製ツールと連携しており、サポート対象バージョンのみに対応するために、定期的に互換性が更新されています。

[詳しくはここをクリック](https://helpx.adobe.com/campaign/kb/deprecated-and-removed-features.html)してください。

## Are there new documentation updates and help materials released? {#are-there-new-documentation-updates-and-help-materials-released-}

最新の Campaign Classic ドキュメント更新のリストは[このページ](https://docs.adobe.com/content/help/en/campaign-classic/using/documentation-updates.html)にあります。

また、最新の技術メモのリストについては、[このページ](https://helpx.adobe.com/campaign/kb/article-list.html)を参照してください。
