---
solution: Campaign Classic
product: campaign
title: Adobe Campaign Classic ドキュメントのアップデート
description: このページでは、Adobe Campaign Classicのドキュメントのすべての新機能と更新をリストします
feature: 概要
role: ビジネス従事者
level: 初心者
translation-type: tm+mt
source-git-commit: d41119e61ee2088e1b8cab65354547420f8e7737
workflow-type: tm+mt
source-wordcount: '4270'
ht-degree: 97%

---


# ドキュメントのアップデート{#documentation-updates}

このページには、毎月および Campaign の各リリースに関するすべての新機能とドキュメントのアップデートが記載されています。

リリース関連の更新については、[Adobe Campaign Classic リリースノート](../../rn/using/latest-release.md)を参照してください。

## 2021 年 3 月 {#march-2021}

Campaign Classicに関するサポートを受けるためのガイドラインとリファレンスが新しいページに追加されました。 [詳細情報](https://helpx.adobe.com/jp/campaign/kb/ac-support.html)

セキュリティとプライバシーに関するベストプラクティスと実行するチェックについて説明する新しいセクションが追加されました。 [詳細情報](../../installation/using/get-started-security-privacy.md)

[権限管理の章](../../platform/using/access-management.md)が改訂され、[オペレーター](../../platform/using/access-management-operators.md)、[オペレーターのグループ](../../platform/using/access-management-groups.md)、[ネームド権限](../../platform/using/access-management-named-rights.md)、[フォルダー管理](../../platform/using/access-management-folders.md)の詳細などを説明する節に分割されました。

以下の新しいページでは、キャンペーンの作成と管理の方法について説明します。
* [キャンペーンテンプレートの作成と設定](../../campaign/using/marketing-campaign-templates.md)
* [マーケティングキャンペーンの配信](../../campaign/using/marketing-campaign-deliveries.md)
* [キャンペーンのオーディエンスの選択](../../campaign/using/marketing-campaign-target.md)
* [関連ドキュメントの管理](../../campaign/using/marketing-campaign-assets.md)
* [承認プロセスの設定と管理](../../campaign/using/marketing-campaign-approval.md)

task.setCompleted() メソッドを使用してタスクを終了し将来のリコールを防ぐ方法に関する情報が、「**[!UICONTROL 高度な JavaScript]**」アクティビティの節に追加されました。[詳細情報](../../workflow/using/sql-code-and-javascript-code.md#adv-js-code-desc)

「[配信品質](../../delivery/using/about-deliverability.md)」セクションが更新され、新しい「[Adobe配信品質のベストプラクティスガイド](https://experienceleague.corp.adobe.com/docs/deliverability-learn/deliverability-best-practice-guide/introduction.html)」へのリンクが追加されました。 様々なAdobeソリューションに適用できる配信品質に関する一般的な情報はすべて、[ベストプラクティスガイド付録](https://experienceleague.corp.adobe.com/docs/deliverability-learn/deliverability-best-practice-guide/additional-resources/general-resources.html#additional-resources)に移動されました。

## 2021 年 2 月 {#release-21.1}

**21.1 リリースに伴うドキュメントのアップデート**

新しい **E メールフィードバックサービス**&#x200B;機能（プライベートベータ版）は、[ここ](../../delivery/using/sending-with-enhanced-mta.md#email-feedback-service)に記載されています。

**サーバー設定ファイル**&#x200B;の節が更新され、キャンペーンが IMS を使用して別のサービスに接続するために必要な設定パラメーターが追加されました。[詳細を表示](../../installation/using/the-server-configuration-file.md#ims)

配信ステータスのリストで、**サービスプロバイダーで受信済み**&#x200B;の説明が更新されました。このステータスは、[E メールフィードバックサービス](../../delivery/using/sending-with-enhanced-mta.md#email-feedback-service)を使用して送信される E メール配信にも使用されるようになりました。[詳細を表示](../../delivery/using/delivery-statuses.md#list-delivery-statuses)

新しいログイン画面で Adobe Campaign に接続するために使用できるキーボードショートカットがドキュメントに記載されるようになりました。[詳細を表示](../../platform/using/launching-adobe-campaign.md#connecting-to-adobe-campaign)

**その他のアップデート**

ワークフローを使用して A/B テストを実行する方法に関する詳細情報が記載された新しい節が追加されました。[詳細を表示](../../delivery/using/get-started-a-b-testing.md)

Adobe Campaign Enhanced MTA の節は[ここ](../../delivery/using/sending-with-enhanced-mta.md)に移動しました。

[!DNL Campaign Classic] のトラッキング機能の概要を説明した新しいページが追加されました。[詳細を表示](../../delivery/using/about-message-tracking.md)

トラッキングに関連する一般的な問題の解決に役立つトラブルシューティングの節が追加されました。[詳細を表示](../../delivery/using/tracking-troubleshooting.md)

**E メールの送信**&#x200B;の節が再編成され、新しいサブセクションで明確化されました。[詳細を表示](../../delivery/using/sending-messages.md)

トラッキングをサポートするパーソナライズ可能な E メールにリンクを追加する方法に関する情報を追加しました。[詳細を表示](../../delivery/using/tracking-personalized-links.md)。

## 2021 年 1 月 {#jan-2021}

**[!UICONTROL 分岐]**&#x200B;アクティビティの節にベストプラクティスの記述が補われました。[詳細を表示](../../workflow/using/fork.md)

**CRM コネクタ**&#x200B;の節の更新、改善、再構成がおこなわれました。[詳細を表示](../../platform/using/crm-connectors.md)。

**Adobe Campaign と Microsoft Dynamics** を接続する手順が専用のページで詳しく説明されています。[詳細を表示](../../platform/using/crm-ms-dynamics.md)。

Oracle オンデマンド API は、Campaign に接続された CRM として非推奨となりました。[詳細を表示](../../rn/using/deprecated-features.md)。

Adobe Campaign のインスタンスで使用されている埋め込み Tomcat web サーブレットの現在のバージョンを調べる方法については、[こちら](../../production/using/locate-tomcat-version.md)を参照してください。

テクニカルワークフローと関連するパッケージのリストが増補され、1 つのページにまとめられました。[詳細を表示](../../workflow/using/about-technical-workflows.md)

**監視**&#x200B;ガイドのトラブルシューティングの節が再構成され、ランディングページが追加されました。[詳細を表示](../../production/using/troubleshooting.md)。

新しい&#x200B;**データのインポートとエクスポート**&#x200B;の節が、ワークフロー、データ圧縮、暗号化、インポートのベストプラクティスに関する新しいページで利用できます。[詳細を表示](../../platform/using/get-started-data-import-export.md)

## 2020 年 12 月 {#dec-2020}

**配信の監視**&#x200B;の節が、主題に沿ったトピックに再編成されました。[詳細を表示](../../delivery/using/about-delivery-monitoring.md)

送信者の IP アドレスを配信ログに追加する方法について、使用例が追加されました。[詳細を表示](../../delivery/using/delivery-dashboard.md#use-case)

プライバシー FAQ は[この節](../../platform/using/privacy-faq.md)に移動しました。

**[!UICONTROL 重複の除外]**&#x200B;アクティビティの結合機能の使用方法に関するユースケースが追加されました。[詳細を表示](../../workflow/using/deduplication-merge.md)

SMS コネクタのプロトコルと設定に関するページの完全な説明が、[こちら](../../delivery/using/sms-protocol.md)で参照できるようになりました。

アクセス権の問題を回避するために、イベントフォルダーを実行インスタンス上の表示として設定しないように警告する注を、**トランザクションメッセージ**&#x200B;の節に追加しました。[詳細を表示](../../message-center/using/event-collection.md)

## 2020 年 11 月 {#nov-2020}

Campaign データモデルの概要が改善され、再構成されました。[詳細を表示](../../configuration/using/about-data-model.md)。

外部アカウント設定は[この節](../../installation/using/external-accounts.md)に移動されました。

Campaign Federated Data Access（FDA）のドキュメントが改善され、各外部データベース設定の詳細が追加され、[この節](../../installation/using/about-fda.md)に移りました。

[Campaign 20.2.3 リリース](../../rn/using/release--20-2.md#release-20-2-3-build-9182)は一般提供（GA）に移行しました。

プライバシー節は移動し、[プライバシー管理](../../platform/using/privacy-management.md)および[プライバシーリクエストの管理](../../platform/using/privacy-requests.md)の 2 つの新しいページが追加されました。

ミッドソーシングサーバーの設定ページに、外部アカウントの内部名を設定した後に更新しないように明記する注記が追加されました。[詳細を表示](../../installation/using/mid-sourcing-server.md)

外部 SFTP サーバーへのパスを指定する際に使用する構文に関する情報が追加されました。[詳細を表示](../../platform/using/sftp-server-usage.md#external-SFTP-server)

個人データとペルソナ節には、プライバシーに関して様々な個人がどのように関わっているかを示す、使用例のシナリオが追加更新されています。[詳細を表示](../../platform/using/privacy-and-recommendations.md#use-case-scenario)

プライバシーに関してよくある質問の一覧を記載した新しい節を追加しました。[詳細を表示](../../platform/using/privacy-faq.md)

## 2020 年 10 月 {#oct-2020}

**20.3 リリースに含まれる新機能**

iOS のプッシュ通知の改善点 - [詳細を表示](../../delivery/using/configuring-the-mobile-application.md)

Android のプッシュ通知の改善点 - [詳細を表示](../../delivery/using/configuring-the-mobile-application-android.md)

**リリースに伴うその他のドキュメントのアップデート**

互換性マトリックスが更新されました。[詳細を表示](../../rn/using/compatibility-matrix.md)

非推奨（廃止予定）および削除された機能ページが更新されました。[詳細を表示](../../rn/using/deprecated-features.md)

リリースノートと[!DNL Gold Standard]リリースの互換表が、専用のセクションで提供されるようになりました。
[詳細を表示](../../rn/using/gold-standard.md#gs-11)。

パイプラインにアクセスするために当初は oAUTH 認証設定に基づいていた Triggers 統合が変更され、Adobe I/O に移動しました。[詳細情報](../../integrations/using/configuring-adobe-io.md)

**その他のアップデート**

Tomcat 8 のアップデートを反映するように、ドキュメントのページが更新されました。

詳細は、「Adobe Campaign バージョンの取得」の節の「バージョン情報」の説明に追加されました。[詳細を表示](../../platform/using/launching-adobe-campaign.md#getting-your-campaign-version)

ビルドの更新を実行する際のガイドラインは、「Adobe Campaign Classic の更新」の節に追加されました。[詳細を表示](../../production/using/build-upgrade.md)

Campaign ビルドのアップグレードに関する FAQ は、Campaign に関するよくある質問に追加されました。[詳細を表示](../../platform/using/faq-build-upgrade.md)

Campaign オンプレミスモデル、ホストモデル、およびハイブリッドホスティングモデルが、専用の節で説明されるようになりました。[詳細を表示](../../installation/using/hosting-models.md)

ホスティングモデルごとの Campaign 機能マトリックスが更新され、インストールガイドに移動しました。[詳細を表示](../../installation/using/capability-matrix.md)

「キャンペーンレポートの高度な機能」の節が強化され、カスタムレポートで URL パラメーターと変数を使用する方法の詳細が示されました。[詳細を表示](../../reporting/using/advanced-functionalities.md)

レポートのプロパティページは、設定を容易にするために再編成され、強化されました。[詳細を表示](../../reporting/using/properties-of-the-report.md)

レガシーバイナリプロトコルから HTTP/2 ベースの APN プロバイダー API に移行する方法の詳細に関する新しいテクニカルノートが作成されました。[詳細を表示](https://helpx.adobe.com/jp/campaign/kb/migrate-to-apns-http2.html)

## 2020 年 9 月 {#september-2020}

アクティブなプロファイルの数がマーケティングインスタンスでのみ使用できることを示す注記が追加されました。[詳細を表示](../../platform/using/about-profiles.md#active-profiles)

フィールドを既存の参照テーブルにリンクするための、スキーマエディションに関する新しいサンプルが追加されました。[詳細を表示](../../configuration/using/examples-of-schemas-edition.md#uc-link)

配信内のシードアドレスでの追加データの使用に関する注記が追加されました。[詳細を表示](../../delivery/using/creating-seed-addresses.md#defining-addresses)

## 2020 年 8 月 {#aug-2020}

配信のデザインと Campaign を使用した送信に関するベストプラクティスについては、該当する節を参照してください。[詳細を表示](../../delivery/using/delivery-best-practices.md)

配信品質ベストプラクティスのランディングページが改善され、サブセクションへのアクセスが容易になりました。[詳細を表示](../../delivery/using/about-deliverability.md)

次のトピックのハウツービデオを視聴できるようになりました。

* [タイポロジルールと定義済みフィルターを使用した疲労管理の設定方法](../../campaign/using/about-campaign-typologies.md)

* [キャンペーンでの E メールの作成方法](../../campaign/using/marketing-campaign-deliveries.md)

* [条件付きコンテンツを含む多言語ニュースレターの作成方法](../../delivery/using/conditional-content.md)

* [配信テンプレートの設定およびデプロイ方法](../../delivery/using/creating-a-delivery-template.md)

* [E メールに対して AMP を有効化して使用する方法](../../delivery/using/defining-interactive-content.md)

* [動的コンテンツブロックを使用して E メールをパーソナライズする方法](../../delivery/using/personalization-blocks.md)

* [パーソナライゼーションフィールドを使用して E メールをパーソナライズする方法](../../delivery/using/personalization-fields.md)

* [E メールのシードと配達確認の管理方法](../../delivery/using/steps-defining-the-target-population.md)

* [繰り返し配信の設定方法](../../workflow/using/recurring-delivery.md)

* [連続配信の設定方法](../../workflow/using/continuous-delivery.md)

FTP サーバーに接続した後に「ホスト名を解決できませんでした」というエラーが発生した場合に実行するチェックと操作に関する情報が追加されました。[詳細を表示](../../platform/using/sftp-server-usage.md)

新しい使用例は、[ワークフローの使用例](../../workflow/using/about-workflow-use-cases.md)のリストで参照されています。

* コンテンツの作成、編集、公開の自動化
* 配信送信前の受信者承認プロセスの設定
* クエリでのインスタンス変数の呼び出し
* 母集団に対する分割率の適用

**[!UICONTROL AND 結合]**&#x200B;アクティビティの節に、変数の使用に関する情報と注意事項が追加されました。[詳細を表示](../../workflow/using/and-join.md)

## 2020 年 7 月 {#july-2020}

増分クエリを使用してリストを自動的に更新する方法に関する使用例が、ワークフローの使用例に追加されました。[詳細を表示](../../workflow/using/about-workflow-use-cases.md)

[リリースノート](../../rn/using/latest-release.md)の編成が変更され、ビルドのステータス、アップグレードプロセス、レコメンデーション、重要なリンクに関する情報が[概要ページ](../../rn/using/latest-release.md)に追加されました。また、[[!DNL Gold Standard]  リリース専用のページが追加され](../../rn/using/gold-standard.md)、[互換表](../../rn/using/compatibility-matrix.md)が統合されました。

Campaign Classic の監視に関するガイドラインを含む新しい節を追加しました。[詳細を表示](../../production/using/monitoring-guidelines.md)

プライバシーと同意の節が強化され、より詳細な情報と役に立つリンクが追加されました。[詳細を表示](../../platform/using/privacy-and-recommendations.md)

Campaign Classic のプライバシー管理ページが更新され、「規則」フィールドに関する情報が追加されました。このフィールドは、自動プライバシーリクエストプロセスを設定する API を使用する場合に利用できます。[詳細を表示](https://helpx.adobe.com/jp/campaign/kb/acc-privacy.html#ManagingPrivacyRequests)

「プライバシー管理の概要」ページが更新され、タイの個人データ保護法（PDPA）とブラジルの Lei Geral de Proteção de Dados（LGPD）に関する情報が含まれるようになりました。[詳細を表示](https://helpx.adobe.com/jp/campaign/kb/campaign-privacy-overview.html#whatisgdpr)

サブワークフローのログおよびエラー発生時の動作に関する情報が追加されました。[詳細を表示](../../workflow/using/sub-workflow.md)

**[!UICONTROL スケジューラー]**&#x200B;アクティビティの節に、ベストプラクティスが追加されました。[詳細を表示](../../workflow/using/scheduler.md)

## 2020 年 6 月{#june-2020}

強制隔離されたアドレスの削除の節が更新されました。これには、アドレスが強制隔離リストから自動的に削除される場合の明確な説明も含まれます。[詳細を表示](../../delivery/using/understanding-quarantine-management.md#removing-a-quarantined-address)

コントロールパネルと Campaign ワークフローを使用したデータの[暗号化](../../platform/using/zip-encrypt.md)および[](../../platform/using/unzip-decrypt.md)復号化の方法に関する使用例が追加されました。

Experience Cloud Triggers と Adobe Campaign Classic の統合ページは、[こちら](../../integrations/using/about-triggers.md)に移動されました。

## 2020 年 7 月 {#release-20-2}

**20.2 リリースに含まれる新機能**

顔文字のサポート - [詳細を表示](../../delivery/using/customizing-emoticon-list.md)

Azure Synapse FDA コネクタ - [詳細を表示](../../installation/using/configure-fda-synapse.md)

タイとブラジルのプライバシーに関する法律 - [詳細を表示](https://helpx.adobe.com/jp/campaign/kb/acc-privacy.html#ManagingPrivacyRequests)

**リリースに伴うその他のドキュメントのアップデート**

トランザクションメッセージテンプレートを非公開にする新しいオプションについては、[この節](../../message-center/using/template-unpublication.md)に記載されています。

パーソナライズされた URL からダウンロードした画像と添付ファイルを含む E メールを送信するときに制限を設定できる新しいオプションが、Campaign Classic オプションのリストに追加されました。[詳細を表示](../../installation/using/configuring-campaign-options.md#delivery)

新しい「**データベースで配信パートを準備**」オプションについては、[こちら](../../delivery/using/steps-validating-the-delivery.md#improving-delivery-analysis)を参照してください。

配信の検証の節が明確になり、更新されました。[詳細を表示](../../delivery/using/steps-validating-the-delivery.md)

新しいトラッキングリンクの署名メカニズムに関連するパラメーターが、[サーバー設定ファイル](../../installation/using/the-server-configuration-file.md)の節に追加されました。

互換性マトリックスが更新されました。[詳細を表示](https://helpx.adobe.com/jp/campaign/kb/compatibility-matrix.html)

クリーンアップワークフローの節が更新されました。[詳細情報](../../production/using/database-cleanup-workflow.md)

Campaign ネットワークエンドポイントは、この[節](../../installation/using/campaign-network-endpoints.md)に移動されました。

Spam Assassin のインストールの節が、新しいインストールファイル名で更新されました。[詳細情報](../../installation/using/configuring-spamassassin.md#installing-spamassassin)

環境の複製に関する節が更新されました。[詳細情報](../../production/using/duplicating-environments.md#step-2---export-the-target-environment-configuration--dev-)

## 2020 年 5 月 {#may-2020}

配信品質の監視の節が移動され、改善されました。[詳細を表示](../../delivery/using/monitoring-deliverability.md)

配信品質のトラブルシューティングの節が移動され、改善されました。[詳細を表示](../../delivery/using/deliverability-faq.md)

新しいプラットフォームの起動時の配信品質のガイドラインが強化されました。 [詳細を表示](https://experienceleague.adobe.com/docs/deliverability-learn/deliverability-best-practice-guide/introduction.html#transition-process)

添付ファイル付きトランザクション E メールの送信の節が移動され、更新されました。[詳細を表示](../../message-center/using/transactional-email-with-attachments.md)

データパッケージのベストプラクティスに関する節が移動および更新されました。[詳細を表示](../../platform/using/working-with-data-packages.md#data-package-best-practices)

## 2020 年 4 月 {#april-2020}

FDA 権限テーブルは、「外部データベースへのアクセス（FDA）」ドキュメントに移動されました。[詳細を表示](../../installation/using/remote-database-access-rights.md)

FAQ を更新し、ソフトキャッシュとハードキャッシュを消去する方法に関するヒントを追加しました。[詳細を表示](../../platform/using/faq-campaign-config.md#perform-soft-cache-clear)

データモデルのベストプラクティスの節を改善し、インデックスに関する追加情報を追加しました。[詳細を表示](../../configuration/using/data-model-best-practices.md#indexes)

Adobe Campaign の組み込みデータモデルに関する節の各テーブルに詳細を追加して更新しました。[詳細を表示](../../configuration/using/data-model-description.md)

ワークフローの使用例が更新され、主題の節に再構成されました。[詳細を表示](../../workflow/using/about-workflow-use-cases.md)

[バウンスメール強制隔離](../../delivery/using/understanding-delivery-failures.md#bounce-mail-qualification)と [E メール管理ルール](../../delivery/using/understanding-delivery-failures.md#email-management-rules)の節の情報を更新して強化しました。

Adobe Campaign Enhanced MTA の記事が更新されました。現在は Campaign Classic にのみ適用されます。[詳細を表示](https://helpx.adobe.com/jp/campaign/kb/acc-campaign-enhanced-mta.html)

## 2020 年 3 月 {#march-2020}

データモデルのベストプラクティスを更新し、[シーケンス](../../configuration/using/data-model-best-practices.md#sequences)、[パフォーマンス](../../configuration/using/data-model-best-practices.md#performance)、[大きなテーブル](../../configuration/using/data-model-best-practices.md#large-tables)などの新しい節を追加しました。[詳細を表示](../../configuration/using/data-model-best-practices.md)

Adobe Campaign の組み込みデータモデルとテーブル間の相互作用を説明する新しい節が利用可能になりました。[詳細を表示](../../configuration/using/data-model-description.md)

追加のキーリンクがドキュメントホームページに追加されました。[詳細を表示](../../campaign-classic-home.md)

Adobe Target のダイナミックオファーを Adobe Campaign の E メールに統合する方法に関する使用例を追加しました。[詳細を表示](../../integrations/using/inserting-a-dynamic-image.md)

Adobe Campaign で使用できる様々な言語の詳細を説明する新しい節を追加しました。[詳細を表示](../../platform/using/adobe-campaign-workspace.md#languages)

アクセス管理ガイドラインを更新し、ネームド権限に関する詳細な情報が追加されました。[詳細を表示](../../platform/using/access-management-named-rights.md)

## 2020 年 2 月 {#february-2020}

Adobe Campaign データモデルの設計時のベストプラクティスと主要な推奨事項の概要を説明する新しい節を追加しました。[詳細を表示](../../configuration/using/data-model-best-practices.md)

技術的な E メール設定に関する新しい節が追加されました。[詳細を表示](../../installation/using/email-deliverability.md)

「配信品質 FAQ」が更新され、「割り当てに達しました」というエラーメッセージの詳細が追加されました。[詳細を表示](https://helpx.adobe.com/jp/campaign/kb/acc-deliverability-faq.html#FAQ)

E メール用の AMP が、新しい E メールプロバイダーでサポートされるようになりました。関連ドキュメントが更新されました。[詳細を表示](../../delivery/using/defining-interactive-content.md)

E メールのアーカイブの節が改善されました。[詳細を表示](../../installation/using/email-archiving.md#recommendations-and-limitations)

## 2020 年 1 月{#release-20-1}

**20.1 リリースに含まれる新機能**

Snowflake FDA コネクタ - [詳細を表示](../../installation/using/configure-fda-snowflake.md)

Hadoop FDA コネクタの機能強化 - [詳細を表示](../../installation/using/configure-fda-hadoop.md)

**リリースに伴うその他のドキュメントのアップデート**

[インストール](../../installation/using/general-architecture.md)、[実稼動](../../production/using/foreword.md)、および[設定](../../configuration/using/additional-parameters.md)ガイドが、nlserver サービスの起動に使用する新しい systemd ユニットについて更新されました。引き続き /etc/init.d/nlserver6 を使用できますが、nlserver サービスとのインタラクションには systemctl コマンドを使用することをお勧めします。

インストールガイドを更新し、互換性マトリックスの最新バージョンと同期しました。新しいサポート対象システムが追加されました。非推奨（廃止予定）およびサポート対象外のシステムに関する記載は削除されました。[詳細を表示](../../installation/using/general-architecture.md)

互換性マトリックスを更新し、Hadoop 3.0 および Snowflake の FDA コネクタを追加しました。[詳細を表示](https://helpx.adobe.com/campaign/kb/compatibility-matrix.html)

IP アフィニティのベストプラクティスがインストールガイドに追加されました。[詳細を表示](../../installation/using/email-deliverability.md#list-of-ip-addresses-to-use)

データベースのクリーンアップワークフローの節が更新されました。指定されたバッチの数値が、コードの実装内容を反映するようになりました。[詳細を表示](../../production/using/database-cleanup-workflow.md)

FDA over HTTP に関する制限が、トランザクションメッセージガイドに追加されました。[詳細を表示](../../production/using/database-cleanup-workflow.md)

**[!UICONTROL JavaScript コード]**&#x200B;と&#x200B;**[!UICONTROL 高度な JavaScript コード]**&#x200B;ワークフローアクティビティのタイムアウト期間を定義できる新しいオプションに関する情報が追加されました。[詳細を表示](../../workflow/using/sql-code-and-javascript-code.md)

**[!UICONTROL 管理]**／**[!UICONTROL 監査]**／**[!UICONTROL ワークフローステータス]**&#x200B;ノードで利用可能な新しい&#x200B;**[!UICONTROL 開始保留中]**&#x200B;ビューに関する情報が追加されました。[詳細を表示](../../workflow/using/monitoring-workflow-execution.md#filtering-workflows-status)

[プッシュ通知の送信](../../delivery/using/about-mobile-app-channel.md)ガイドを移動および再編成し、情報を明確にして改善しました。

URL レポート設定の新しいパラメーターは、[こちら](../../reporting/using/properties-of-the-report.md#defining-additional-settings)で説明されています。

「**Campaign Classic オンプレミスとホスト機能マトリックス**」ページが更新され、新しい FDA コネクタが追加されました。[詳細を表示](../../installation/using/capability-matrix.md)。

**Campaign Classic 機能マトリックス**&#x200B;ページを更新しました。[詳細を表示](https://helpx.adobe.com/campaign/kb/compatibility-matrix.html)

新しい **[!UICONTROL Nmsaddress のクリーンアップ]**&#x200B;ワークフローの情報は、[ここ](../../production/using/database-cleanup-workflow.md#cleanup-of-nmsaddress)に記載されています。

ワークフローでクエリアクティビティを使用する際の制限が追加されました。[詳細を表示](../../workflow/using/query.md)。

ソフトエラーが発生した際にアドレスを強制隔離へと送信する、拡張された E メールアドレス検証ルールの詳細について説明する新しい節が追加されました。[詳細を表示](../../delivery/using/understanding-quarantine-management.md#soft-error-management)

インスタンスが Enhanced MTA を使用しているかどうかを示す設定ファイルのパラメーターがドキュメントに追加されました。[詳細を表示](../../installation/using/the-server-configuration-file.md#mta)

配信品質の節が移動および再編成され、新しい内容で改善されました。[詳細を表示](../../delivery/using/about-deliverability.md)

Adobe Campaign Classic のデータモデルの基本と各テーブルの説明にアクセスする方法について説明する新しい節が追加されました。[詳細を表示](../../configuration/using/about-data-model.md)

Adobe Campaign Enhanced MTA の記述を更新し、Enhanced MTA ヘッダーをすべてのメッセージに追加しないインスタンスに、特定のタイポロジパッケージをインストールする方法について詳細が追加されました。[詳細を表示](https://helpx.adobe.com/jp/campaign/kb/acc-campaign-enhanced-mta.html#impacts)

クエリの設計に関する使用事例が別個の節に再編成されました。[詳細を表示](../../workflow/using/querying-recipient-table.md)

Adobe Campaign Classic のオファー管理およびインタラクションモジュールの使用に関するヒントとテクニックについて、新しい節が追加されました。[詳細を表示](../../interaction/using/interaction-best-practices.md#tips-managing-offers)

オファーの管理方法の理解を深めるのに役立つ、複数のビデオへのリンクがインタラクションドキュメントに追加されました。[詳細を表示](../../interaction/using/interaction-and-offer-management.md)

インスタンスで実行されるクエリを最適化する方法に関するベストプラクティスの記述がドキュメントに統合されました。[詳細を表示](../../workflow/using/query.md#optimizing-queries)

レポートガイドが更新、再編成されました。[詳細を表示](../../reporting/using/about-adobe-campaign-reporting-tools.md)

ワークフローでインスタンス変数を使用する方法の例が追加されました。[詳細を表示](../../workflow/using/javascript-scripts-and-templates.md)

## 2019 年 12 月 {#december-2019}

「WdbcOptions_TempDbName」オプションがキャンペーンオプションのリストに追加されました。[詳細を表示](../../installation/using/configuring-campaign-options.md)

FDA のマトリックスページは、[ここ](../../installation/using/remote-database-access-rights.md)に移動されました。

アクセス権のマトリックスページは、[ここ](https://experienceleague.adobe.com/docs/campaign-classic/assets/access-rights-matrix.pdf?lang=en)に移動されました。

AMP でインタラクティブコンテンツを定義する方法について説明する節が移動されました。[詳細を表示](../../delivery/using/defining-interactive-content.md)

**19.2 リリースに含まれる新機能**

カリフォルニア州消費者プライバシー法（CCPA） - [詳細を表示](https://helpx.adobe.com/jp/campaign/kb/acc-privacy.html)

AMP を使用したインタラクティブコンテンツ - [詳細を表示](../../delivery/using/defining-interactive-content.md)

ワークフローのライブ監視 - [詳細を表示](../../workflow/using/monitoring-workflow-execution.md#filtering-workflows-status)

セキュア SMS メッセージ（TLS） - [詳細を表示](https://helpx.adobe.com/jp/campaign/kb/sms-connector-protocol-and-settings.html)

**リリースに伴うその他のドキュメントのアップデート**

Adobe Campaign Enhanced MTA のドキュメントが入手できるようになりました。[詳細を表示](https://helpx.adobe.com/campaign/kb/acc-campaign-enhanced-mta.html)

キャンペーン内で「開始準備中」の状態に留まるワークフローをトラブルシュートする方法について、新しい節が追加されました。[詳細を表示](../../production/using/workflow-execution.md#start-as-soon-as-possible-in-campaigns)

新しい「NmsOperation_DeliveryPreparationWindow」および「WdbcKillSessionPolicy」オプションがキャンペーンオプションのリストに追加されました。[詳細を表示](../../installation/using/configuring-campaign-options.md)

Adobe Campaign Classic データモデルの基本を説明する新しいドキュメントが追加されました。[詳細を表示](https://helpx.adobe.com/jp/campaign/kb/acc-datamodel.html)

配信プロパティの新しいオプション「**最長パーソナライゼーション実行時間**」については、この[節](../../delivery/using/personalization-fields.md#timing-out-personalization)で説明されています。

logon() および query() で **HttpServletRequest** を使用する API 呼び出しの例が更新されました。[詳細を表示](../../configuration/using/web-service-calls.md)。

スキーマ定義の **sqlDefault** 属性に関する推奨事項が追加されました。[詳細を表示](../../configuration/using/schema/attribute.md)。

Adobe Campaign とアドビのリアルタイムカスタマーデータプラットフォーム（CDP）の統合については、**Adobe Experience Cloud との統合**&#x200B;ガイドで参照されるようになりました。[詳細を表示](../../integrations/using/about-campaign-integrations.md)。

## 2019 年 11 月 {#november-2019}

[ミッドソーシングサーバーの多重化](../../installation/using/mid-sourcing-server.md#multiplexing-the-mid-sourcing-server)および[複数のコントロールインスタンスのサポート](../../message-center/using/transactional-messaging-architecture.md#supporting-several-control-instances)の節に、完全にホストされたクライアントおよびハイブリッドクライアントにおいては、これらのデプロイメントがサポートされていないことに言及する警告が追加されました。

E メールの送信時に使用する文字エンコーディングの強制適用方法を説明する新しい節が追加されました。[詳細を表示](../../delivery/using/sending-messages.md#character-encoding)

アクセス管理に関する節が更新され、「**プライバシーデータ権限**」が追加されました。[詳細を表示](../../platform/using/access-management-named-rights.md)

パーソナライゼーションフィールドの内容は 1024 文字を超過できないことを明確にする情報が追加されました。[詳細を表示](../../delivery/using/personalization-fields.md)

コントロールパネルのドキュメントは、新しいコラボレーションドキュメントセットに統合されました。[詳細を表示](https://docs.adobe.com/content/help/ja-JP/control-panel/using/control-panel-home.html)

配信のベストプラクティス入門ガイドが更新されました。[詳細を表示](../../delivery/using/delivery-best-practices.md)

## 2019 年 10 月 {#october-2019}

Campaign Standard および Campaign Classic のエラーメッセージのリストが更新されました。[詳細を表示](https://docs.adobe.com/content/help/en/campaign-classic/technicalresources/error_messages/error_codes.html)

GDPR の入門ガイドが改善され、強化されました。GDPR や CCPA を含む、プライバシー管理に関するドキュメントになりました。[詳細を表示](https://helpx.adobe.com/content/help/jp/campaign/kb/campaign-privacy.html)

Campaign Classic でのトラッキングについて、新しいトラブルシューティングページが追加されました。[詳細を表示](https://helpx.adobe.com/jp/campaign/kb/classic-tracking-troubleshooting.html)。

Adobe Analytics Data Connector の新しいベストプラクティスのページが追加されました。[Adobe Analytics Data Connector の詳細を表示](../../platform/using/adobe-analytics-data-connector.md)

配信のベストプラクティス入門ガイドが移動され、更新されました。[詳細を表示](../../delivery/using/delivery-best-practices.md)

複数の外部アカウントが拡張された汎用 SMPP コネクタを同じプロバイダーアカウントで使用する際の問題を回避するための推奨事項が、SMS チャネルのドキュメントに追加されました。[詳細を表示](../../delivery/using/sms-channel.md#automatic-reply)

ワークフローの同時実行を防ぐ方法に関する情報がスケジューラーアクティビティのドキュメントに追加されました。[詳細を表示](../../workflow/using/scheduler.md)

オンプレミスインストールの受信ボックスレンダリングを設定する手順がドキュメントに追加されました。[詳細を表示](../../delivery/using/inbox-rendering.md#activating-inbox-rendering)

## 2019 年 9 月 {#september-2019}

Campaign Classic の管理に関する一般的なガイドラインを提供する新しいページが追加されました。[詳細を表示](../../production/using/monitoring-guidelines.md)

ワークフロー監視に関する情報は、新しい専用の節に集約されました。[詳細を表示](../../workflow/using/monitoring-workflow-execution.md)。

Adobe Campaign Classic のトラッキングに関する一般的なガイドラインを提供する新しいページが追加されました。[詳細を表示](https://helpx.adobe.com/jp/campaign/kb/acc-tracking.html)。

ワークフローと配信のパフォーマンス改善のためのベストプラクティスが更新されました。[ワークフローの詳細](../../workflow/using/workflow-best-practices.md)および[配信の詳細](../../delivery/using/delivery-performances.md#best-practices-performance)を参照してください。

## 2019 年 5 月 {#release-19-1}

**19.1 リリースに含まれる新機能**

コントロールパネル - [詳細を表示](https://docs.adobe.com/content/help/en/control-panel/using/control-panel-home.html)

監査記録 - [詳細を表示](../../production/using/audit-trail.md)

**リリースに伴うその他のドキュメントのアップデート**

ビルドアップグレードに関する新しい FAQ が作成されました。[詳細を表示](https://helpx.adobe.com/jp/campaign/kb/build-upgrade-faq.html)

[互換性マトリックス](https://helpx.adobe.com/campaign/kb/compatibility-matrix.html)が更新されました。サポートされるデータベースシステム、Android/iOS のバージョン、および関連する SDK のリストが更新されました。[19.0 互換性マトリックス](https://helpx.adobe.com/jp/campaign/kb/compatibility-matrix-19-0.html)がアーカイブされました。

「Campaign Classic の非推奨（廃止予定）および削除された機能」ページが更新されました。[詳細を表示](https://helpx.adobe.com/jp/campaign/kb/deprecated-and-removed-features.html)

インストールガイドにサーバー設定ファイルの説明が追加されました。[詳細を表示](../../installation/using/the-server-configuration-file.md)

ホストモデルおよびハイブリッドモデルのインストールおよび設定手順を説明する節が追加されました。[詳細を表示](../../installation/using/hosting-models.md)

Campaign サーバーのアンインストール手順を説明する節が追加されました。[詳細を表示](../../installation/using/uninstalling-campaign.md)

[セキュリティ](https://helpx.adobe.com/jp/campaign/kb/acc-security.html)、[配信品質](../../delivery/using/about-deliverability.md)および[プライバシー](../../platform/using/privacy-management.md)の入門ガイドが更新されました。

前処理ワークフローオプションの説明が更新され、製品の変更が反映されました。[詳細を表示](../../workflow/using/data-loading--file-.md)

Experience Cloud Triggers のテクニカルノートが更新されました。[詳細を表示](../../integrations/using/about-triggers.md)

エラーメッセージのリストが更新されました。[詳細を表示](https://docs.adobe.com/content/help/en/campaign-classic/technicalresources/error_messages/error_codes.html)

トランザクションメッセージングの SOAP 認証方法に関する詳細が追加されました。[詳細を表示](../../message-center/using/event-description.md)

Apache の設定手順が更新されました。[詳細を表示](../../installation/using/integration-into-a-web-server-for-linux.md)

Campaign Standard および Classic のエンドポイントのリストを含む新しいページが追加されました。[詳細を表示](../../installation/using/campaign-network-endpoints.md)

データパッケージのベストプラクティス記事が更新されました。[詳細を表示](../../configuration/using/data-model-best-practices.md)

オファーの管理に関するドキュメントが更新され、ベストプラクティスを説明する新しい節が追加されました。[詳細を表示](../../interaction/using/interaction-best-practices.md)

Adobe Campaign Classic のオファーカタログの使用に関する新しいナレッジベース記事が作成されました。[詳細を表示](https://helpx.adobe.com/jp/campaign/kb/offer-best-practices.html)

サブワークフローアクティビティの節に、使用例が追加されました。[詳細を表示](../../workflow/using/sub-workflow.md)

[Campaign Classic オンプレミスとホスト機能マトリックス](../../installation/using/capability-matrix.md)のページが更新され、「BCC で E メールを送信」に関する情報が追加されました。

トランザクションメッセージングのドキュメントが更新され、テンプレートのパブリッシュに関する注意事項が追加されました。[詳細を表示](../../message-center/using/template-publication.md)

未処理のバウンスメールの節が更新され、「転送先アドレス」フィールドおよび「エラーのアドレス」フィールドに関する詳細が追加されました。[詳細を表示](../../installation/using/deploying-an-instance.md)

ワークフロー計画のベストプラクティスに関する新しい節が追加されました。[詳細を表示](../../workflow/using/workflow-best-practices.md)

キャンペーンオプションのリストに、XtkSecurity_Restrict_EditXML および NmsOperation_OperationMgtDebug の 2 つの新しいオプションが追加されました。
[詳細を表示](../../installation/using/configuring-campaign-options.md)

Campaign Classic で使用できる様々な外部アカウントと、その設定方法に関する情報が追加されました。
[詳細を表示](../../installation/using/external-accounts.md)

Analytics Data Connector の節が更新され、インターフェイスの変更が反映されるようになりました。
[詳細を表示](../../platform/using/adobe-analytics-data-connector.md)

請求レポートに関する情報が追加されました。
[詳細を表示](../../production/using/monitoring-processes.md)

共有オーディエンスの統合に関するドキュメントが更新されました。
[詳細を表示](../../integrations/using/configuring-shared-audiences-integration-in-adobe-campaign.md)

[SMS コネクタのプロトコルと設定](https://helpx.adobe.com/campaign/kb/sms-connector-protocol-and-settings.html)および[シーケンスの自動生成](https://helpx.adobe.com/jp/campaign/kb/sequence_auto_generation.html#Switchtoadedicatedsequence)のテクニカルノートが更新されました。

テクニカルワークフローの節が更新されました。[詳細を表示](../../workflow/using/about-technical-workflows.md)

Campaign ドメイン名の設定手順が改善および更新されました。[詳細を表示](https://helpx.adobe.com/jp/campaign/kb/domain-name-delegation.html)

Google Cloud Messaging（GCM）から Firebase Cloud Messaging（FCM）への Android アプリの移行手順が更新されました。[詳細を表示](https://helpx.adobe.com/jp/campaign/kb/migrate-to-fcm.html)

Campaign ハードウェアのサイズ設定ガイドが更新されました。[詳細を表示](https://helpx.adobe.com/jp/campaign/kb/hardware-sizing-guide.html)

Teradata 外部アカウントの Query Banding に関する情報が追加されました。[詳細を表示](../../installation/using/external-accounts.md)

## 2019 年 1 月{#release-doc-16-01-2019}

Experience Cloud Triggers のテクニカルノートが更新されました。[詳細を表示](../../integrations/using/about-triggers.md)

オファーの承認の節に注意事項を追加し、「承認コンテンツ」の表示は、すべてのオファーが有効化または承認されているかどうかに関わらず、コンテンツ承認プロセスが達成されたことを示すことを明確にしました。[詳細を表示](../../interaction/using/offer-catalog-overview.md)

新しい節がインストールガイドに追加され、管理／プラットフォーム／オプションノードのオプションが一覧で示されました。[詳細を表示](../../installation/using/configuring-campaign-options.md)

メーリングリストを保護するためのシードアドレスの使用に関する情報が追加されました。[詳細を表示](../../delivery/using/creating-seed-addresses.md)

配信を作成して送信する際の重要な手順が新しい節に再編成されました。必要に応じて様々なチャネルの参照も追加されました。[詳細を表示](../../delivery/using/steps-about-delivery-creation-steps.md)

[E メールのアーカイブ](../../installation/using/email-archiving.md)の節が移動および再編成され、明確になった情報で改善されました。

* 接続あたりの E メールおよび BCC 送信 IP パラメーターに関するベストプラクティスが追加されました。

* 以前のビルド（Adobe Campaign 17.2 ビルド 8795 以前）で E メールアーカイブを既に使用している場合に、新しい E メールアーカイブシステム（BCC）へアップグレードする手順を更新しました。

ワークフローによる自動化ガイドに、使用例、「パーソナライズされたアラートのオペレーターへの送信」が追加されました。[詳細を表示](../../workflow/using/sending-personalized-alerts-to-operators.md)

新しいバージョンへの移行の節が更新されました。Adobe Campaign v6.11 への移行ができなくなったので、このドキュメントでは、Adobe Campaign Classic v7 への移行手順のみの詳細を説明しています。[詳細を表示](../../migration/using/about-migration.md)

一時的な配信エラーの後の再試行の節が明確化されました。[詳細を表示](../../delivery/using/understanding-delivery-failures.md)

E メールコンテンツの定義の節に、デジタルコンテンツエディターの節へのリンクが追加されました。[詳細を表示](../../delivery/using/defining-the-email-content.md)

トランザクションメッセージングのアーキテクチャの節が更新され、コントロールインスタンスと実行インスタンスは同じマシンにインストールできないことを説明する警告が追加されました。[詳細を表示](../../message-center/using/transactional-messaging-architecture.md)

ワークフローの監視の節が更新され、ビルド 8700 ～ 8977（18.10）に関する注意事項が追加されました。これらのビルド用のワークフローヒートマップパッケージのインストール方法に関するテクニカルノートへのリンクも含まれます。[詳細を表示](../../workflow/using/heatmap.md)

ワークフローのエンリッチメントアクティビティを使用してカスタムデータフィールドを含む E メールを送信する方法に関する使用例が追加されました。[詳細を表示](../../workflow/using/email-enrichment-with-custom-date-fields.md)

機能に関するビデオが[ここ](https://docs.adobe.com/content/help/ja-JP/campaign-classic-learn/tutorials/overview.html)に移動されました。
