---
product: campaign
title: 重要な概念
description: Campaign Classic に関する FAQ
badge-v7-only: label="v7" type="Informative" tooltip="Applies to Campaign Classic v7 only"
audience: platform
content-type: reference
topic-tags: starting-with-adobe-campaign
exl-id: f0d884ae-0789-4ad9-a8fa-adeffbb560ea
source-git-commit: 8debcd3d8fb883b3316cf75187a86bebf15a1d31
workflow-type: tm+mt
source-wordcount: '866'
ht-degree: 100%

---

# 主要概念 {#key-concepts}



Adobe Campaign の利用を開始するための主要な手順を説明します。

## Adobe ID を使用して Campaign Classic に接続できますか？ {#can-i-connect-to-campaign-classic-with-an-adobe-id-}

IMS（Adobe Identity Management System）との統合により、ユーザーは Adobe ID を使用して Adobe Campaign コンソールに接続できます。統合には次のメリットがあります。

* Experience Cloud のすべてのソリューションに同じ ID を使用できます。
* Adobe Campaign で異なる統合を使用する場合にも、接続が記憶されます。
* パスワード管理ポリシーをよりセキュアにできます。
* Federated ID アカウント（外部の ID プロバイダー）を使用します。

Adobe ID を使用した Campaign Classic へのアクセスについて[詳しくは、ここをクリック](../../integrations/using/about-adobe-id.md)してください。

## 使用している Campaign のバージョンを確認する方法はありますか？  {#what-is-my-version-of-campaign-}

Campaign クライアントコンソールの&#x200B;**ヘルプ／バージョン情報**&#x200B;メニューで、お使いの[バージョンおよびビルド番号](../../platform/using/launching-adobe-campaign.md#getting-your-campaign-version)を確認できます。

## オンプレミス環境とホスト環境では作業する際にどのような違いがありますか？ {#what-are-the-differences-when-working-on-premise-vs--in-a-hosted-environment-}

Adobe Campaign Classic には一連のモジュールとオプションが付属しています。これらのモジュールと設定の使用可否は、インストールの[デプロイメントタイプ](../../installation/using/hosting-models.md)がホスト（マネージドサービス）、ハイブリッド、オンプレミスのどれであるかによって異なります。

詳しくは、[ここをクリック](../../installation/using/capability-matrix.md)してください。

## ユーザー権限を設定するにはどうすればよいですか？ {#how-can-i-set-up-user-permissions-}

Campaign 管理者は、組織のユーザーに対して権限を設定できます。

以下は、各種の権限や制限によって承認または拒否できる操作です。

* 特定の機能へのアクセス
* 特定のデータへのアクセス
* データの作成、変更、削除

ユーザー権限について[詳しくは、ここをクリック](../../platform/using/access-management.md)してください。

## Campaign でプライバシーコンプライアンスを確保するにはどうすればよいですか？ {#how-to-be-gdpr-compliant-with-campaign-}

Adobe Campaign には、GDPR および CCPA に則ってプライバシーを遵守するのに役立つ一連のツールが用意されています。

[このドキュメント](privacy-and-recommendations.md)を参照して、Adobe Campaign のツールと機能、ベストプラクティスについて把握し、GDPR を遵守しながらアドビのサービスを利用する方法を学んでください。Adobe Campaign Classic の実装手順については、[この記事](https://helpx.adobe.com/jp/campaign/kb/acc-privacy.html)を参照してください。

## Campaign ユーザーインターフェイスについて知っておくべき概念は何ですか？ {#what-are-campaign-user-interface-concepts-i-should-know-}

Adobe Campaign ワークスペースの基本事項について詳しくは、[この節](../../platform/using/adobe-campaign-workspace.md)を参照してください。

![](assets/do-not-localize/how-to-video.png) [ビデオで Campaign ワークスペースを確認する](https://experienceleague.adobe.com/docs/campaign-classic-learn/tutorials/getting-started/exploring-the-adobe-campaign-classic-user-interface.html?lang=ja)

## メッセージのオーディエンスを選択するにはどうすればよいですか？ {#how-can-i-select-the-target-population-of-my-messages-}

Adobe Campaign では、各種の戦略を使用してオーディエンスの作成とターゲット受信者の選択をおこなうことができます。

[詳しくはここをクリック](../../delivery/using/steps-defining-the-target-population.md)してください。

## ワークフローとは何ですか？ {#what-is-a-workflow-}

Adobe Campaign には、アプリケーションサーバーの様々なモジュール間でプロセスおよびタスク全体にわたる調整をおこなうワークフローモジュールが含まれています。この包括的なグラフィカル環境を使用すると、セグメント化、キャンペーン実行、ファイル処理、人の参加などを含むプロセスを設計できます。ワークフローエンジンは、これらのプロセスを実行およびトラッキングします。

例えば、ワークフローを使用して、サーバーからファイルをダウンロードしたり、ファイルを解凍したり、ファイルに含まれるレコードを Adobe Campaign データベースにインポートしたりできます。

またワークフローには、1 人または複数のオペレーターを関連付けて、通知の対象とすることや、プロセスの選択や承認に関与させることもできます。この方法により、配信アクションを作成して 1 人または複数のオペレーターにタスクを割り当て、コンテンツに対して作業する、ターゲットを指定する、配信開始前に配達確認を承認する、などが可能になります。

ワークフローについて[詳しくはここをクリック](../../workflow/using/about-workflows.md)してください。「[ワークフローのベストプラクティス](../../workflow/using/building-a-workflow.md)」も参照してください。

## 最初の E メールを作成し送信するにはどうすればよいですか？ {#how-to-create-and-send-a-first-email-}

[詳しくはここをクリック](../../delivery/using/about-email-channel.md)してください。

![](assets/do-not-localize/how-to-video.png) [ビデオでこれを確認する](https://experienceleague.adobe.com/docs/campaign-classic-learn/tutorials/getting-started/creating-a-campaign-and-an-email.html?lang=ja)

## SMS メッセージを送信するにはどうすればよいですか？ {#how-to-send-sms-messages-}

プラットフォームを設定して SMS メッセージを送信する方法については、[この節](../../delivery/using/sms-channel.md)を参照してください。

## プッシュ通知を送信するにはどうすればよいですか？ {#how-to-send-push-notifications-}

Adobe Campaign を使用して、パーソナライズされたプッシュ通知をアプリを介して iOS および Android デバイスに送信する方法については、[こちら](../../delivery/using/create-notifications-ios.md)（iOS デバイスの場合）を参照してください。

## オンライン調査を設計および共有するにはどうすればよいですか？ {#how-to-design-and-share-an-online-survey-}

Campaign Classic を使用して調査を設計および公開するための重要な手順とともに、[オンライン調査を作成](../../surveys/using/getting-started-with-surveys.md)する方法を説明します。

## ランディングページを作成するにはどうすればよいですか？ {#how-to-create-landing-page-}

Adobe Campaign デジタルコンテンツエディターを使用すると、ランディングページを作成してデータベースフィールドとのマッピングを定義することができます。

[詳しくはここをクリック](../../web/using/creating-a-landing-page.md)してください。

## 配信をトラッキングするにはどうすればよいですか？ {#how-can-i-track-deliveries-}

Campaign Classic で送られた配信を専用の[配信レポート](../../reporting/using/delivery-reports.md)によってトラッキングし、さらに配信を監視することができます。

Campaign でのトラッキング管理について詳しくは、[このページ](https://helpx.adobe.com/jp/campaign/kb/acc-tracking.html)を参照してください。

## セキュリティに関するベストプラクティス（オンプレミス）にはどのようなものがありますか？ {#what-are-security-best-practices--on-premise--}

オンプレミスデプロイメントのセキュリティ設定と強化に関して確認すべき重要な要素については、[セキュリティ設定チェックリスト](https://helpx.adobe.com/jp/campaign/kb/acc-security.html)を参照してください。

## エラーメッセージを翻訳するにはどうすればよいですか？ {#how-to-translate-an-error-message-}

エラーメッセージが外国語で表示されましたか？すべてのエラーメッセージとその翻訳のリストは、[このページ](https://experienceleague.adobe.com/developer/campaign-errors/error_codes.html?lang=ja)に掲載されています。

## Campaign で web フォームを作成して回答を収集できますか？ {#can-i-create-a-webform-and-collect-answers-in-campaign-}

[Web フォームの作成](../../web/using/about-web-forms.md)（Web フォームのデザイン、テスト、公開および回答の収集）方法を説明します。

## 非推奨（廃止予定）の機能およびバージョンのリストはありますか？ {#is-there-a-list-of-deprecated-features-and-versions-}

アドビでは、製品の機能を継続的に評価し、各機能をより強力なバージョンに置き換えるために長期的な計画を策定したり、将来的な想定や拡張に備えるために特定のパーツの再実装を決定したりしています。Campaign はサードパーティ製ツールと連携しており、サポート対象バージョンのみに対応するために、定期的に互換性が更新されています。

[詳しくはここをクリック](../../rn/using/deprecated-features.md)してください。

## リリースされた新しいドキュメント更新やヘルプ資料はありますか？ {#are-there-new-documentation-updates-and-help-materials-released-}

最新の Campaign Classic ドキュメント更新のリストは[このページ](https://experienceleague.adobe.com/docs/campaign-classic/using/documentation-updates.html?lang=ja)にあります。

また、最新の技術メモのリストについては、[このページ](https://helpx.adobe.com/jp/campaign/kb/article-list.html)を参照してください。
