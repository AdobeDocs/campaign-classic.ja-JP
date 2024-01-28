---
product: campaign
title: Adobe Campaign Classic v7 ドキュメントの更新
description: このページには、Adobe Campaign Classic のドキュメントの新機能と更新がすべてリストアップされています
feature: Release Notes
badge-v7-only: label="v7" type="Informative" tooltip="Campaign Classic v7 にのみ適用されます"
role: User
level: Beginner
exl-id: 07c1f4a3-cf16-4a9b-b402-e13258799f91
source-git-commit: 31705e7dd0ecb4e66fe4a22369995384d3ce39d4
workflow-type: ht
source-wordcount: '3703'
ht-degree: 100%

---

# ドキュメントの更新{#documentation-updates}

このページでは、すべての新機能とドキュメント更新情報の一覧が月ごとおよび Campaign リリースごとに記載されています。

リリース関連の更新については、[Adobe Campaign Classic リリースノート](../../rn/using/latest-release.md)を参照してください。

## 2024

### 2024年1月 {#jan-2024}

ダイレクトメールのデフォルトの postalAddress フィールドの定義方法と、アドレスが完全であることを確認することが重要な理由に関する情報を追加しました。[詳細情報](../../delivery/using/about-direct-mail-channel.md)

## 2023

### 2023年12月 {#dec-2023}

JWT（JSON web トークン）は、現在非推奨（廃止予定）の段階で、OAuth に置き換えられています。トランジションは、Campaign の今後のリリース内で段階的に実行され、ドキュメントはこれらの更新を反映して更新されます。

Amazon Redshift 用の FDA 外部アカウント設定を追加しました。[詳細情報](../../installation/using/configure-fda-redshift.md)

### 2023年8月 {#aug-2023}

4 Gb を超える圧縮されたファイルの解凍に Adobe Campaign を使用できないことを示す制限を追加しました。[詳細情報](../../platform/using/unzip-decrypt.md)

### 2023年4月 {#apr-2023}

オンプレミス／ハイブリッド環境で Microsoft Edge Chromium を有効にする方法に関するテクニカルノートを追加しました。 [詳細情報](../../technotes/using/edge-chromium.md)

### 2023年3月 {#mar-2023}

7.3.3 の改善点とパッチを含むリリースノートの節を更新しました。[詳細情報](latest-release.md)


+++ 2022


## 2022年11月 {#nov-2022}

7.3.2 の改善点とパッチをリリースノートの節に反映させました。[詳細情報](latest-release.md)

Teradata 17 のサポートを互換性マトリクスに反映させました。[詳細情報](compatibility-matrix.md)

「ファイルとリソースの管理」の節が更新されて、**uploadWhiteList** 属性に関する情報が追加されました。[詳細情報](../../installation/using/file-res-management.md)

セキュリティゾーンに関するドキュメントが更新されて、**allowDebug** 属性に関する情報が追加されました。 [詳細情報](../../installation/using/security-zones.md#recommendations)

移行ガイドが更新されました。 サポートされていない Adobe Campaign バージョンへの参照が削除されました。[詳細情報](../../migration/using/about-migration.md)


## 2022年7月 {#july-2022}

新しい配信サーバーへの移行について詳しくは、新しいテクニカルノートを参照してください。 [詳細情報](../../technotes/using/deliverability-server.md)

**7.3.1 リリースに伴うドキュメントの更新**

互換性マトリックスを更新しました。 [詳細情報](compatibility-matrix.md)

リリースノートの節を更新しました。 [詳細情報](rn-overview.md)

iOS 15 での時間依存の通知。 [詳細情報](../../delivery/using/create-notifications-ios.md)


## 2022年3月 {#mar-2022}

「**[!UICONTROL SMTP 配信をテスト]**」オプションの詳細な説明を追加しました。[詳細情報](../../delivery/using/steps-sending-the-delivery.md#delivery-additiona-parameters)

「アップグレードの基本を学ぶ」ページが更新され、Campaign コンソールのアップグレードガイドラインが明確になりました。[詳細情報](../../rn/using/rn-overview.md)

新しい Campaign v7.2.2 ビルドが利用できるようになりました。 [詳細情報](../../rn/using/latest-release.md)

<!--Added troubleshooting information related to the ACS connector. [Read more](../../integrations/using/troubleshooting-the-acs-connector.md)-->

提供が終了した従来の PostgreSQL バージョンが、[廃止される機能および削除された機能](../../rn/using/deprecated-features.md#dbe-eol)ページに追加されました。

## 2022年2月 {#february-2022}

 「**ファイル転送**&#x200B;アクティビティ」の節を更新し、「**転送後にソースファイルを削除**」オプションが選択されていない場合に SFTP ディレクトリにあるアーカイブ済みコンテンツのサイズを手動で監視するように追記しました。[詳細情報](../../workflow/using/file-transfer.md#properties)

「強制隔離とブロックリストの比較」の節の内容が明快になりました。[詳細情報](../../delivery/using/understanding-quarantine-management.md#quarantine-vs-denylist)

アドレスを強制隔離に送信する方法と強制隔離リストからアドレスを削除する方法に関する節が更新されました。[詳細情報](../../delivery/using/understanding-quarantine-management.md#removing-a-quarantined-address)

同じワークフローで複数の停止リクエストを実行しないことをお勧めするワークフローのベストプラクティスが追加されました。[詳細情報](../../workflow/using/workflow-best-practices.md)

キャンペーン内での繰り返し配信の実行を停止する方法に関する情報を追加しました。[詳細情報](../../workflow/using/recurring-delivery.md)

## 2022年1月 {#january-2022}

**7.2.1 リリースに伴うドキュメントのアップデート**

互換性マトリックスを更新しました。 [詳細情報](compatibility-matrix.md)

リリースノートの節を更新しました。 [詳細情報](rn-overview.md)

FDA 外部アカウント設定を Snowflake 用に更新しました。 [詳細情報](../../installation/using/configure-fda-snowflake.md)

FDA 外部アカウント設定を Azure Synapse Analytics 用に更新しました。 [詳細情報](../../installation/using/configure-fda-synapse.md#azure-external)

Google BigQuery FDA コネクタを更新しました。 [詳細情報](../../installation/using/configure-fda-google-big-query.md)

廃止に伴い、Microsoft CRM、Salesforce、Oracle CRM On Demand アクションアクティビティがドキュメントから削除されました。

新しいオプション「**エラー時に中止**」をワークフローの「エラー管理」の節に追加しました。 [詳細情報](../../workflow/using/advanced-parameters.md#in-case-of-errors)

CRM コネクタアクティビティに「バッチ更新」オプションを追加しました。 [詳細情報](../../workflow/using/crm-connector.md)

+++

+++ 2021

## 2021年12月{#dec-2021}

Campaign Classic v7 リリースノートが再編成され、ナビゲーションを簡素化されました。[詳細情報](rn-overview.md)

Campaign のフォーム編集に関するドキュメントが更新および改善されました。[詳細情報](../../configuration/using/editing-forms.md)

CentOs 8 が EOL（提供終了）に達し、Adobe Campaign Classic で非推奨になりました。[詳細情報](deprecated-features.md)

## 2021年11月{#nov-2021}

受信 SMS（MO）に関する制限事項を追加しました。[詳細情報](../../delivery/using/sms-protocol.md#multipart)

CRM コネクタデプロイメントの移行プロセスログの詳細を更新しました。[詳細情報](../../migration/using/testing-the-migration.md#verification-process)

Adobe Campaign と Adobe Analytics の統合を実装するための IMS 権限に関する要件を追加しました。[詳細情報](../../platform/using/adobe-analytics-provisioning.md)

Adobe Analytics Data Connector の提供終了日を 2022年3月1日（PT）から 2022年8月17日（PT）に更新しました。[詳細情報](deprecated-features.md)

Adobe Launch で Campaign 拡張機能を設定する方法に関する Adobe Experience Platform モバイル SDK ドキュメントへのリンクを追加しました。[詳細情報](../../delivery/using/integrating-campaign-sdk-into-the-mobile-application.md)

JavaScript を使用して値の計算やデータの交換を行う方法と、SOAP 呼び出しを使用して特定の操作を実行する方法に関する節を追加しました。[詳細情報](../../workflow/using/javascript-scripts-and-templates.md)

ワークフローでの JavaScript コードの実装例を追加しました。 [詳細情報](../../workflow/using/javascript-in-workflows.md)


## 2021年10月{#oct-2021}

既存のテクニカルノートは、新しい&#x200B;**テクニカルノート**&#x200B;の節にグループ化されました。

**ハードウェアサイズについてのレコメンデーション**&#x200B;ページが更新され、**テクニカルノート**&#x200B;の節に追加されました。[詳細情報](../../technotes/using/hardware-sizing.md)

## 2021年9月{#sept-2021}

**21.1.4 リリースに伴うドキュメントのアップデート**

**ゲージ**&#x200B;グラフタイプが削除されました。

Adobe Flash の提供終了に伴い、レポートと web アプリケーションのスクリーンショットおよびパラメーターが更新されました。

[請求テクニカルワークフロー](../../production/using/monitoring-processes.md#billing-report)の説明が更新され、新しいガードレールが追加されました。

## 2021 年 8 月{#aug-2021}

「データソースを変更」という新しいワークフローアクティビティが追加されました - [詳細情報](../../workflow/using/change-data-source.md)

適用の可否を示すバッジがドキュメントページに追加されました。**v7 に適用**&#x200B;の場合は Campaign Classic v7 機能にのみ適用され、**v7 と v8 に適用**&#x200B;の場合は両方のバージョンに共通する機能に適用されます。

Adobe Experience Manager 6.4 以降は Campaign と AEM Assets の統合が廃止されていることを示す注記が追加されました。[詳細情報](../../integrations/using/configuring-access-to-assets.md)


## 2021 年 7 月 {#july-2021}

[Campaign 21.1.3 リリース](../../rn/using/latest-release.md#release-21-1-3-build-9330)が一般提供（GA）に移行しました。


## 2021年6月 {#june-2021}

**トランザクションメッセージ**&#x200B;の節を編成し直して、新しく「はじめに」の節を明確にしました。この節では、プロセスをより深く理解できるよう、[拡張スキーマ](../../message-center/using/about-transactional-messaging.md#transactional-messaging-operating-principle)についても説明しています。[詳細を読む](../../message-center/using/about-transactional-messaging.md)

**21.1.3 リリースに伴うドキュメントのアップデート**

Adobe Journey Orchestration との統合 — [詳細情報](https://experienceleague.adobe.com/docs/journeys/using/action-journeys/acc-action.html?lang=ja)。ステップバイステップの使用例については、[このページ](https://experienceleague.adobe.com/docs/journeys/using/use-cases-journeys/campaign-classic-use-case.html?lang=ja)を参照してください

LINE チャネルの強化 — [詳細情報](../../delivery/using/line-channel.md)

新しい Vertica Analytics FDA コネクタ - [詳細情報](../../installation/using/configure-fda-vertica.md)

新しい Google BigQuery FDA コネクタ - [詳細情報](../../installation/using/configure-fda-google-big-query.md)

「請求」テクニカルワークフローの説明に、「アクティブな請求プロファイルの数（billingActiveContactCount）」で初めに実行したタスクを含みました。[詳細情報](../../workflow/using/about-technical-workflows.md)

## 2021 年 5 月 {#may-2021}

ワークフローヒートマップレポートのドキュメントが更新され、改善されました。 [詳細情報](../../workflow/using/heatmap.md)

Campaign クライアントコンソールの要件が互換性マトリックスで更新されました。 [詳細情報](../../rn/using/compatibility-matrix.md#ClientConsoleoperatingsystems)

Campaign クライアントコンソールのインストール手順を改善し、明確にしました。[詳細情報](../../installation/using/installing-the-client-console.md)

トラッキングする URL の署名の問題に関する新しいテクニカルノートが作成されました。 [詳細情報](../../technotes/using/tracked-urls.md)

## 2021 年 4 月 {#april-2021}

Adobe Experience Platform のソースと宛先を使って Campaign Classic と Adobe Real-time Customer Data Platform（RTCDP）間でデータを共有する方法について、新しい節で説明しています。[詳細情報](../../integrations/using/get-started-sources-destinations.md)

ISP の停止後にバウンスの選定を更新する方法を学ぶための新しいテクニカルノートが作成されました。[詳細情報](../../delivery/using/update-bounce-qualification.md)

## 2021 年 3 月 {#march-2021}

[「SMS の基本を学ぶ」の節](../../delivery/using/sms-channel.md)を再編成し、改善しました。[SMS チャネルの設定方法](../../delivery/using/sms-set-up.md)、[SMS の作成方法](../../delivery/using/sms-create.md)、[SMS の送信方法および追跡方法](../../delivery/using/sms-send.md)を、専用の節で学習できます。

Campaign Classic 用の「ヘルプとサポートのオプション」ページが、コアドキュメントに統合されました。 [詳細情報](../../support.md)

セキュリティとプライバシーに関するベストプラクティスと実行するチェックについて説明する新しいセクションが追加されました。 [詳細情報](../../installation/using/get-started-security-privacy.md)

[権限管理の章](../../platform/using/access-management.md)が改訂され、[オペレーター](../../platform/using/access-management-operators.md)、[オペレーターのグループ](../../platform/using/access-management-groups.md)、[ネームド権限](../../platform/using/access-management-named-rights.md)、[フォルダー管理](../../platform/using/access-management-folders.md)の詳細などを説明する節に分割されました。

以下の新しいページでは、キャンペーンの作成と管理の方法について説明します。
* [キャンペーンテンプレートの作成と設定](../../campaign/using/marketing-campaign-templates.md)
* [マーケティングキャンペーン配信](../../campaign/using/marketing-campaign-deliveries.md)
* [キャンペーンのオーディエンスの選択](../../campaign/using/marketing-campaign-target.md)
* [関連ドキュメントの管理](../../campaign/using/marketing-campaign-assets.md)
* [承認プロセスの設定と管理](../../campaign/using/marketing-campaign-approval.md)

task.setCompleted() メソッドを使用してタスクを終了し将来のリコールを防ぐ方法に関する情報が、「**[!UICONTROL 高度な JavaScript]**」アクティビティの節に追加されました。[詳細情報](../../workflow/using/sql-code-and-javascript-code.md#adv-js-code-desc)

[配信品質](../../delivery/using/about-deliverability.md)の節が更新され、新しい[アドビ配信品質のベストプラクティスガイド](https://experienceleague.adobe.com/docs/deliverability-learn/deliverability-best-practice-guide/introduction.html?lang=ja)へのリンクが追加されました。 様々なアドビソリューションに適用できる配信品質に関する一般的な情報はすべて、[ベストプラクティスガイド付録](https://experienceleague.adobe.com/docs/deliverability-learn/deliverability-best-practice-guide/additional-resources/general-resources.html?lang=ja#additional-resources)に移動しました。

## 2021 年 2 月 {#release-21.1}

**21.1 リリースに伴うドキュメントのアップデート**

**新しいメールフィードバックサービス**&#x200B;機能（プライベートベータ版）は、[、ここに記載されています。](../../delivery/using/sending-with-enhanced-mta.md#email-feedback-service)

**サーバー設定ファイル**&#x200B;の節が更新され、キャンペーンが IMS を使用して別のサービスに接続するために必要な設定パラメーターが追加されました。[詳細を表示](../../installation/using/the-server-configuration-file.md#ims)

配信ステータスのリストで、**サービスプロバイダーで受信済み**&#x200B;の説明が更新されました。このステータスは、[メールフィードバックサービス](../../delivery/using/sending-with-enhanced-mta.md#email-feedback-service)を使用して送信されるメール配信にも使用されるようになりました。[詳細を表示](../../delivery/using/delivery-statuses.md#list-delivery-statuses)

新しいログイン画面で Adobe Campaign に接続するために使用できるキーボードショートカットがドキュメントに記載されるようになりました。[詳細を表示](../../platform/using/launching-adobe-campaign.md#connecting-to-adobe-campaign)

**その他のアップデート**

ワークフローを使用して A/B テストを実行する方法に関する詳細情報が記載された新しい節が追加されました。[詳細を表示](../../delivery/using/get-started-a-b-testing.md)

Adobe Campaign Enhanced MTA の節は[ここ](../../delivery/using/sending-with-enhanced-mta.md)に移動しました。

[!DNL Campaign Classic] のトラッキング機能の概要を説明した新しいページが追加されました。[詳細を表示](../../delivery/using/about-message-tracking.md)

トラッキングに関連する一般的な問題の解決に役立つトラブルシューティングの節が追加されました。[詳細を表示](../../delivery/using/tracking-troubleshooting.md)

**メールの送信**&#x200B;の節が再編成され、新しいサブセクションで明確化されました。[詳細を表示](../../delivery/using/sending-messages.md)

トラッキングをサポートするパーソナライズ可能なメールにリンクを追加する方法に関する情報を追加しました。[詳細を表示](../../delivery/using/tracking-personalized-links.md)。

## 2021 年 1 月 {#jan-2021}

**[!UICONTROL 分岐]**&#x200B;アクティビティの節にベストプラクティスの記述が補われました。[詳細を表示](../../workflow/using/fork.md)

**CRM コネクタ**&#x200B;の節の更新、改善、再構成がおこなわれました。[詳細を表示](../../platform/using/crm-connectors.md)。

**Adobe Campaign と Microsoft Dynamics** を接続する手順が専用のページで詳しく説明されています。[詳細を表示](../../platform/using/crm-ms-dynamics.md)。

Oracle オンデマンド API は、Campaign に接続された CRM として非推奨となりました。[詳細を表示](../../rn/using/deprecated-features.md)。

Adobe Campaign のインスタンスで使用されている埋め込み Tomcat web サーブレットの現在のバージョンを調べる方法については、[こちら](../../production/using/locate-tomcat-version.md)を参照してください。

テクニカルワークフローと関連するパッケージのリストが増補され、1 つのページにまとめられました。[詳細を表示](../../workflow/using/about-technical-workflows.md)

**監視**&#x200B;ガイドのトラブルシューティングの節が再構成され、ランディングページが追加されました。[詳細を表示](../../production/using/troubleshooting.md)。

新しい&#x200B;**データのインポートとエクスポート**&#x200B;の節が、ワークフロー、データ圧縮、暗号化、インポートのベストプラクティスに関する新しいページで利用できます。[詳細を表示](../../platform/using/get-started-data-import-export.md)

+++


+++ 2020


## 2020 年 12 月 {#dec-2020}

**配信の監視**&#x200B;の節が、主題に沿ったトピックに再編成されました。[詳細を表示](../../delivery/using/about-delivery-monitoring.md)

送信者の IP アドレスを配信ログに追加する方法について、使用例が追加されました。[詳細を表示](../../delivery/using/delivery-dashboard.md#use-case)

プライバシー FAQ は[この節](../../platform/using/privacy-faq.md)に移動しました。

**[!UICONTROL 重複の除外]**&#x200B;アクティビティの結合機能の使用方法に関するユースケースが追加されました。[詳細を表示](../../workflow/using/deduplication-merge.md)

SMS コネクタのプロトコルと設定に関するページの完全な説明が、[こちら](../../delivery/using/sms-protocol.md)で参照できるようになりました。

アクセス権の問題を回避するために、イベントフォルダーを実行インスタンス上の表示として設定しないように警告する注を、**トランザクションメッセージ**&#x200B;の節に追加しました。[詳細情報](../../message-center/using/about-event-processing.md#event-collection)

## 2020 年 11 月 {#nov-2020}

Campaign データモデルの概要が改善され、再構成されました。[詳細を表示](../../configuration/using/about-data-model.md)。

外部アカウント設定は[この節](../../installation/using/external-accounts.md)に移動されました。

Campaign Federated Data Access（FDA）のドキュメントが改善され、各外部データベース設定の詳細が追加され、[この節](../../installation/using/about-fda.md)に移りました。

Campaign 20.2.3 リリースが一般提供（GA）に移行しました。

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

[!DNL Gold Standard] リリースのリリースノートと互換性マトリックスが、専用のページで提供されるようになりました。
[詳細を表示](../../rn/using/gold-standard.md)。

パイプラインにアクセスするために当初は oAUTH 認証設定に基づいていた Triggers 統合が変更され、Adobe I/O に移動しました。[詳細情報](../../integrations/using/configuring-adobe-io.md)

**その他のアップデート**

Tomcat 8 のアップデートを反映するように、ドキュメントのページが更新されました。

詳細は、「Adobe Campaign バージョンの取得」の節の「バージョン情報」の説明に追加されました。[詳細を表示](../../platform/using/launching-adobe-campaign.md#getting-your-campaign-version)

ビルドの更新を実行する際のガイドラインは、「Adobe Campaign Classic の更新」の節に追加されました。[詳細情報](../../production/using/build-upgrade.md)

Campaign ビルドのアップグレードに関する FAQ は、Campaign に関するよくある質問に追加されました。[詳細を表示](../../platform/using/faq-build-upgrade.md)

Campaign オンプレミスモデル、ホストモデル、およびハイブリッドホスティングモデルが、専用の節で説明されるようになりました。[詳細を表示](../../installation/using/hosting-models.md)

ホスティングモデルごとの Campaign 機能マトリックスが更新され、インストールガイドに移動しました。[詳細を表示](../../installation/using/capability-matrix.md)

「キャンペーンレポートの高度な機能」の節が強化され、カスタムレポートで URL パラメーターと変数を使用する方法の詳細が示されました。[詳細を表示](../../reporting/using/advanced-functionalities.md)

レポートのプロパティページは、設定を容易にするために再編成され、強化されました。[詳細情報](../../reporting/using/properties-of-the-report.md)

## 2020 年 9 月 {#september-2020}

アクティブなプロファイルの数がマーケティングインスタンスでのみ使用できることを示す注記が追加されました。[詳細を表示](../../platform/using/about-profiles.md#active-profiles)

フィールドを既存の参照テーブルにリンクするための、スキーマエディションに関する新しいサンプルが追加されました。[詳細を表示](../../configuration/using/examples-of-schemas-edition.md#uc-link)

配信内のシードアドレスでの追加データの使用に関する注記が追加されました。[詳細を表示](../../delivery/using/creating-seed-addresses.md#defining-addresses)

## 2020 年 8 月 {#aug-2020}

配信のデザインと Campaign を使用した送信に関するベストプラクティスについては、該当する節を参照してください。[詳細を表示](../../delivery/using/delivery-best-practices.md)

配信品質ベストプラクティスのランディングページが改善され、サブセクションへのアクセスが容易になりました。[詳細を表示](../../delivery/using/about-deliverability.md)

次のトピックのハウツービデオを視聴できるようになりました。

* [タイポロジルールと定義済みフィルターを使用した疲労管理の設定方法](../../campaign-opt/using/about-campaign-typologies.md)

* [キャンペーンへのメールの作成方法](../../campaign/using/marketing-campaign-deliveries.md)

* [条件付きコンテンツを含んだ多言語ニュースレターの作成方法](../../delivery/using/conditional-content.md)

* [配信テンプレートの設定およびデプロイ方法](../../delivery/using/creating-a-delivery-template.md)

* [メールに対して AMP を有効化して使用する方法](../../delivery/using/defining-interactive-content.md)

* [動的コンテンツブロックを使用してメールをパーソナライズする方法](../../delivery/using/personalization-blocks.md)

* [パーソナライゼーションフィールドを使用してメールをパーソナライズする方法](../../delivery/using/personalization-fields.md)

* [メールでのシードと配達確認の管理方法](../../delivery/using/steps-defining-the-target-population.md)

* [繰り返し配信の設定方法](../../workflow/using/recurring-delivery.md)

* [連続配信の設定方法](../../workflow/using/continuous-delivery.md)

FTP サーバーに接続した後に「ホスト名を解決できませんでした」というエラーが発生した場合に実行するチェックとアクションに関する情報が追加されました。[詳細を表示](../../platform/using/sftp-server-usage.md)

新しい使用例は、[ワークフローの使用例](../../workflow/using/about-workflow-use-cases.md)のリストで参照されています。

* コンテンツの作成、編集、公開の自動化
* 配信送信前の受信者承認プロセスの設定
* クエリでのインスタンス変数の呼び出し
* 母集団に対する分割率の適用

**[!UICONTROL AND 結合]**&#x200B;アクティビティの節に、変数の使用に関する情報と注意事項が追加されました。[詳細情報](../../workflow/using/and-join.md)

## 2020 年 7 月 {#july-2020}

増分クエリを使用してリストを自動的に更新する方法に関する使用例が、ワークフローの使用例に追加されました。[詳細を表示](../../workflow/using/about-workflow-use-cases.md)

[リリースノート](../../rn/using/latest-release.md)の編成が変更され、ビルドのステータス、アップグレードプロセス、レコメンデーション、重要なリンクに関する情報が[概要ページ](../../rn/using/latest-release.md)に追加されました。また、[[!DNL Gold Standard] リリース](../../rn/using/gold-standard.md)専用のページが追加され、[互換性マトリックス](../../rn/using/compatibility-matrix.md)が統合されました。

Campaign Classic の監視に関するガイドラインを含む新しい節を追加しました。[詳細を表示](../../production/using/monitoring-guidelines.md)

プライバシーと同意の節が強化され、より詳細な情報と役に立つリンクが追加されました。[詳細を表示](../../platform/using/privacy-and-recommendations.md)

Campaign Classic のプライバシー管理ページが更新され、「規則」フィールドに関する情報が追加されました。このフィールドは、自動プライバシーリクエストプロセスを設定する API を使用する場合に利用できます。[詳細情報](https://helpx.adobe.com/jp/campaign/kb/acc-privacy.html#ManagingPrivacyRequests)

「プライバシー管理の概要」ページが更新され、タイの個人データ保護法（PDPA）とブラジル個人情報保護法（LGPD）に関する情報が含まれるようになりました。[詳細情報](../../platform/using/privacy-and-recommendations.md)

サブワークフローのログおよびエラー発生時の動作に関する情報が追加されました。[詳細を表示](../../workflow/using/sub-workflow.md)

**[!UICONTROL スケジューラー]**&#x200B;アクティビティの節に、ベストプラクティスが追加されました。[詳細情報](../../workflow/using/scheduler.md)

## 2020 年 6 月 {#june-2020}

強制隔離されたアドレスの削除の節が更新されました。これには、アドレスが強制隔離リストから自動的に削除される場合の明確な説明も含まれます。[詳細を表示](../../delivery/using/understanding-quarantine-management.md#removing-a-quarantined-address)

コントロールパネルと Campaign ワークフローを使用したデータの[暗号化](../../platform/using/zip-encrypt.md)および[](../../platform/using/unzip-decrypt.md)復号化の方法に関する使用例が追加されました。

Experience Cloud Triggers と Adobe Campaign Classic の統合ページは、[こちら](../../integrations/using/about-triggers.md)に移動されました。

## 2020 年 7 月 {#release-20-2}

**20.2 リリースに含まれる新機能**

顔文字のサポート - [詳細を表示](../../delivery/using/customizing-emoticon-list.md)

Azure Synapse FDA コネクタ - [詳細を表示](../../installation/using/configure-fda-synapse.md)

タイとブラジルのプライバシーに関する法律 - [詳細を表示](https://helpx.adobe.com/jp/campaign/kb/acc-privacy.html#ManagingPrivacyRequests)

**リリースに伴うその他のドキュメントのアップデート**

トランザクションメッセージテンプレートを非公開にする新しいオプションについては、[この節](../../message-center/using/publishing-message-templates.md#template-unpublication)に記載されています。

パーソナライズされた URL からダウンロードした画像と添付ファイルを含むメールを送信するときに制限を設定できる新しいオプションが、Campaign Classic オプションのリストに追加されました。[詳細を表示](../../installation/using/configuring-campaign-options.md#delivery)

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

新しいプラットフォームを開始する際の配信品質ガイドラインが強化されました。[詳細を表示](https://experienceleague.adobe.com/docs/deliverability-learn/deliverability-best-practice-guide/introduction.html?lang=ja#transition-process)

添付ファイル付きトランザクションメールの送信の節が移動され、更新されました。[詳細を表示](../../message-center/using/transactional-email-with-attachments.md)

データパッケージのベストプラクティスに関する節が移動および更新されました。[詳細情報](../../platform/using/working-with-data-packages.md#data-package-best-practices)

## 2020 年 4 月 {#april-2020}

FDA 権限テーブルは、「外部データベースへのアクセス（FDA）」ドキュメントに移動されました。[詳細を表示](../../installation/using/remote-database-access-rights.md)

FAQ を更新し、ソフトキャッシュとハードキャッシュを消去する方法に関するヒントを追加しました。[詳細を表示](../../platform/using/faq-campaign-config.md#perform-soft-cache-clear)

データモデルのベストプラクティスの節を改善し、インデックスに関する追加情報を追加しました。[詳細を表示](../../configuration/using/data-model-best-practices.md#indexes)

Adobe Campaign のビルトインデータモデルを説明している節で、各テーブルの詳細が更新されました。[詳細を表示](../../configuration/using/data-model-description.md)

ワークフローの使用例が更新され、主題の節に再構成されました。[詳細を表示](../../workflow/using/about-workflow-use-cases.md)

[バウンスメール強制隔離](../../delivery/using/understanding-delivery-failures.md#bounce-mail-qualification)と[メール管理ルール](../../delivery/using/understanding-delivery-failures.md#email-management-rules)の節の情報を更新して強化しました。

Adobe Campaign Enhanced MTA の記事が更新されました。現在は Campaign Classic にのみ適用されます。[詳細情報](https://helpx.adobe.com/jp/campaign/kb/acc-campaign-enhanced-mta.html)

## 2020 年 3 月 {#march-2020}

データモデルのベストプラクティスを更新し、[シーケンス](../../configuration/using/data-model-best-practices.md#sequences)、[パフォーマンス](../../configuration/using/data-model-best-practices.md#performance)、[大きなテーブル](../../configuration/using/data-model-best-practices.md#large-tables)などの新しい節を追加しました。[詳細を表示](../../configuration/using/data-model-best-practices.md)

Adobe Campaign のビルトインデータモデルとテーブル間の相互作用を説明する新しい節が利用可能になりました。[詳細を表示](../../configuration/using/data-model-description.md)

追加のキーリンクがドキュメントホームページに追加されました。[詳細を表示](../../campaign-classic-home.md)

Adobe Target のダイナミックオファーを Adobe Campaign のメールに統合する方法に関する使用例を追加しました。[詳細を表示](../../integrations/using/inserting-a-dynamic-image.md)

Adobe Campaign で使用できる様々な言語の詳細を説明する新しい節を追加しました。[詳細を表示](../../platform/using/adobe-campaign-workspace.md#languages)

アクセス管理ガイドラインを更新し、ネームド権限に関する詳細な情報が追加されました。[詳細情報](../../platform/using/access-management-named-rights.md)

## 2020 年 2 月 {#february-2020}

Adobe Campaign データモデルの設計時のベストプラクティスと主要なレコメンデーションの概要を説明する新しい節を追加しました。[詳細を表示](../../configuration/using/data-model-best-practices.md)

技術的なメール設定に関する新しい節が追加されました。[詳細を表示](../../installation/using/email-deliverability.md)

「配信品質 FAQ」が更新され、「割り当てに達しました」というエラーメッセージの詳細が追加されました。[詳細を表示](https://helpx.adobe.com/jp/campaign/kb/acc-deliverability-faq.html#FAQ)

メール用の AMP が、新しいメールプロバイダーでサポートされるようになりました。関連ドキュメントが更新されました。[詳細を表示](../../delivery/using/defining-interactive-content.md)

メールのアーカイブの節が改善されました。[詳細情報](../../installation/using/email-archiving.md#recommendations-and-limitations)

## 2020 年 1 月 {#release-20-1}

**20.1 リリースに含まれる新機能**

Snowflake FDA コネクタ - [詳細を表示](../../installation/using/configure-fda-snowflake.md)

Hadoop FDA コネクタの機能強化 - [詳細を表示](../../installation/using/configure-fda-hadoop.md)

**リリースに伴うその他のドキュメントのアップデート**

[インストール](../../installation/using/general-architecture.md)、[実稼動](../../production/using/foreword.md)、および[設定](../../configuration/using/additional-parameters.md)ガイドが、nlserver サービスの起動に使用する新しい systemd ユニットについて更新されました。引き続き /etc/init.d/nlserver6 を使用できますが、nlserver サービスとのインタラクションには systemctl コマンドを使用することをお勧めします。

インストールガイドを更新し、互換性マトリックスの最新バージョンと同期しました。新しいサポート対象システムが追加されました。非推奨（廃止予定）およびサポート対象外のシステムに関する記載が削除されました。[詳細を表示](../../installation/using/general-architecture.md)

互換性マトリックスを更新し、Hadoop 3.0 および Snowflake の FDA コネクタを追加しました。[詳細を表示](https://helpx.adobe.com/jp/campaign/kb/compatibility-matrix.html)

IP アフィニティのベストプラクティスがインストールガイドに追加されました。[詳細を表示](../../installation/using/email-deliverability.md#list-of-ip-addresses-to-use)

データベースのクリーンアップワークフローの節が更新されました。指定されたバッチの数値が、コードの実装内容を反映するようになりました。[詳細を表示](../../production/using/database-cleanup-workflow.md)

FDA over HTTP に関する制限が、トランザクションメッセージガイドに追加されました。[詳細を表示](../../production/using/database-cleanup-workflow.md)

**[!UICONTROL JavaScript コード]**&#x200B;と&#x200B;**[!UICONTROL 高度な JavaScript コード]**&#x200B;ワークフローアクティビティのタイムアウト期間を定義できる新しいオプションに関する情報が追加されました。[詳細を表示](../../workflow/using/sql-code-and-javascript-code.md)

**[!UICONTROL 管理]**／**[!UICONTROL 監査]**／**[!UICONTROL ワークフローステータス]**&#x200B;ノードで利用可能な新しい&#x200B;**[!UICONTROL 開始保留中]**&#x200B;ビューに関する情報が追加されました。[詳細を表示](../../workflow/using/monitoring-workflow-execution.md#filtering-workflows-status)

[プッシュ通知の送信](../../delivery/using/about-mobile-app-channel.md)ガイドを移動および再編成し、情報を明確にして改善しました。

URL レポート設定の新しいパラメーターは、[こちら](../../reporting/using/properties-of-the-report.md#defining-additional-settings)で説明されています。

「**Campaign Classic オンプレミスとホスト機能マトリックス**」ページが更新され、新しい FDA コネクタが追加されました。[詳細情報](../../installation/using/capability-matrix.md)。

**Campaign Classic 機能マトリックス**&#x200B;ページを更新しました。[詳細を表示](https://helpx.adobe.com/jp/campaign/kb/compatibility-matrix.html)

新しい **[!UICONTROL Nmsaddress のクリーンアップ]**&#x200B;ワークフローの情報は、[ここ](../../production/using/database-cleanup-workflow.md#cleanup-of-nmsaddress)に記載されています。

ワークフローでクエリアクティビティを使用する際の制限が追加されました。[詳細を表示](../../workflow/using/query.md)。

ソフトエラーが発生した際にアドレスを強制隔離へと送信する、拡張されたメールアドレス検証ルールの詳細について説明する新しい節が追加されました。[詳細を表示](../../delivery/using/understanding-quarantine-management.md#soft-error-management)

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

+++

<!--

### December 2019 {#december-2019}

The "WdbcOptions_TempDbName" option has been added to the list of Campaign options. [Read more](../../installation/using/configuring-campaign-options.md)

The FDA matrix page has been moved [here](../../installation/using/remote-database-access-rights.md).

The Access Rights Matrix page has been moved [here](https://experienceleague.adobe.com/docs/campaign-classic/assets/access-rights-matrix.pdf).

The section describing how to define interactive content with AMP has been moved. [Read more](../../delivery/using/defining-interactive-content.md)

**New capabilities included in 19.2 release**

California Consumer Privacy Act (CCPA) - [Read more](https://helpx.adobe.com/campaign/kb/acc-privacy.html)

Interactive content with AMP - [Read more](../../delivery/using/defining-interactive-content.md)

Workflow live monitoring - [Read more](../../workflow/using/monitoring-workflow-execution.md#filtering-workflows-status)

Secure SMS Messaging (TLS) - [Read more](https://helpx.adobe.com/campaign/kb/sms-connector-protocol-and-settings.html)

**Other documentation updates coming with the release**

The Adobe Campaign Enhanced MTA documentation is now available. [Read more](https://helpx.adobe.com/campaign/kb/acc-campaign-enhanced-mta.html)

A new section has been added on how to troubleshoot a workflow staying in the "Start as soon as possible" state within a campaign. [Read more](../../production/using/workflow-execution.md#start-as-soon-as-possible-in-campaigns)

The new "NmsOperation_DeliveryPreparationWindow" and "WdbcKillSessionPolicy" options have been added to the list of Campaign options. [Read more](../../installation/using/configuring-campaign-options.md)

A new document describing the Adobe Campaign Classic data model basics is now available. [Read more](https://helpx.adobe.com/campaign/kb/acc-datamodel.html)

The new **Maximum personalization run time** option in the delivery properties is documented in this [section](../../delivery/using/personalization-fields.md#timing-out-personalization).

The examples for API calls using an **HttpServletRequest** with logon() and query() have been updated. [Read more](../../configuration/using/web-service-calls.md).

A recommendation for **sqlDefault** attribute in schema definition has been added. [Read more](../../configuration/using/schema/attribute.md)).

The integration between Adobe Campaign and Adobe Real-time Customer Data Platform is now referenced in the **Integrating with Adobe Experience Cloud** guide. [Read more](../../integrations/using/about-campaign-integrations.md).

### November 2019 {#november-2019}

A warning has been added to the [Multiplexing the mid-sourcing server](../../installation/using/mid-sourcing-server.md#multiplexing-the-mid-sourcing-server) and [Supporting several control instances](../../message-center/using/transactional-messaging-architecture.md#supporting-several-control-instances) sections mentioning that these deployments are not supported for fully hosted and hybrid clients.

A new section has been added to describe how to force the character encoding used when sending an email. [Read more](../../delivery/using/sending-messages.md#character-encoding)

The Access management section has been updated with the **Privacy Data right**. [Read more](../../platform/using/access-management-named-rights.md)

Information was added to specify that personalization fields content cannot exceed 1024 characters. [Read more](../../delivery/using/personalization-fields.md)

The Control Panel documentation has been integrated into the new collaborative documentation set. [Read more](https://experienceleague.adobe.com/docs/control-panel/using/control-panel-home.html)

The Delivery Best Practices getting started guide has been updated. [Read more](../../delivery/using/delivery-best-practices.md)

### October 2019 {#october-2019}

The list of error messages for Campaign has been updated. [Read more](https://experienceleague.adobe.com/developer/campaign-errors/error_codes.html)

The GDPR getting started guide has been improved and enriched. It is now a privacy management documentation including GDPR and CCPA. [Read more](https://helpx.adobe.com/content/help/en/campaign/kb/campaign-privacy.html)

A new troubleshooting page has been added for tracking in Campaign Classic. [Read more](https://helpx.adobe.com/campaign/kb/classic-tracking-troubleshooting.html).

A new page of best practices for Adobe Analytics Connector has been added. [Read more on Adobe Analytics Connector](../../platform/using/adobe-analytics-connector.md)

The Delivery Best Practices getting started guide has been moved and updated. [Read more](../../delivery/using/delivery-best-practices.md)

A recommendation has been added to the SMS channel documentation to avoid issues when using multiple external accounts leveraging the Extended generic SMPP connector with the same provider account. [Read more](../../delivery/using/sms-set-up.md#automatic-reply)

Information was added in the Scheduler activity documentation on how to prevent simultaneous executions of a workflow. [Read more](../../workflow/using/scheduler.md)

The steps to configure Inbox rendering for on-premise installations have been added to documentation. [Read more](../../delivery/using/inbox-rendering.md#activating-inbox-rendering)

### September 2019 {#september-2019}

A new page has been added to provide general guidelines for maintaining Campaign Classic. [Read more](../../production/using/monitoring-guidelines.md)

Information related to workflows monitoring has been centralized into a new dedicated section. [Read more](../../workflow/using/monitoring-workflow-execution.md).

A new page about general guidelines for tracking in Adobe Campaign Classic has been added. [Read more](https://helpx.adobe.com/campaign/kb/acc-tracking.html).

The best practices for performance improvements of workflows and deliveries have been updated. [Read more on workflows](../../workflow/using/workflow-best-practices.md) and [more on deliveries](../../delivery/using/delivery-performances.md#best-practices-performance).

### May 2019 {#release-19-1}

**New capabilities included in 19.1 release**

Control Panel - [Read more](https://experienceleague.adobe.com/docs/control-panel/using/control-panel-home.html)

Audit trail - [Read more](../../production/using/audit-trail.md)

**Other documentation updates coming with the release**

A new Build upgrade FAQ has been created. [Read more](https://helpx.adobe.com/campaign/kb/build-upgrade-faq.html)

The [Compatibility matrix](compatibility-matrix.md) has been updated. The list of supported database systems has been updated, Android/iOS versions and related SDKs. The 19.0 Compatibility matrix has been archived.

The 'Deprecated and Removed Features in Campaign Classic' page has been updated. [Read more](deprecated-features.md)

The description of the server configuration file has been added to the Installation guide. [Read more](../../installation/using/the-server-configuration-file.md)

A section has been added describing the installation and configuration steps for hosted and hybrid models. [Read more](../../installation/using/hosting-models.md)

A section has been added describing the Campaign server uninstallation steps. [Read more](../../installation/using/uninstalling-campaign.md)

The [security](https://helpx.adobe.com/campaign/kb/acc-security.html), [deliverability](../../delivery/using/about-deliverability.md) and [privacy](../../platform/using/privacy-management.md) getting started guides have been updated.

The description of the pre-process workflow option has been updated to reflect product changes. [Read more](../../workflow/using/data-loading--file-.md)

The Experience Cloud Triggers technote has been updated. [Read more](../../integrations/using/about-triggers.md)

The list of error messages has been updated. [Read more](https://experienceleague.adobe.com/developer/campaign-errors/error_codes.html)

Added more information on SOAP authentication methods for transactional messaging. [Read more](../../message-center/using/event-description.md)

The Apache configuration steps have been updated. [Read more](../../installation/using/integration-into-a-web-server-for-linux.md)

A new page has been added including the list of endpoints for Classic. [Read more](../../installation/using/campaign-network-endpoints.md)

The Data package best practices article has been updated. [Read more](../../configuration/using/data-model-best-practices.md)

The Managing Offers documentation has been updated with a new section listing best practices. [Read more](../../interaction/using/interaction-best-practices.md)

A new Knowledge base article on using the offer catalog in Adobe Campaign Classic has been created. [Read more](https://helpx.adobe.com/campaign/kb/offer-best-practices.html)

The Sub-workflow activity section has been enhanced with an example of usage. [Read more](../../workflow/using/sub-workflow.md)

The [Campaign Classic On-premise & Hosted capability matrix](../../installation/using/capability-matrix.md) page has been updated with information relating to Email BCC.

The Transactional Messaging documentation has been updated with a note regarding template publication. [Read more](../../message-center/using/publishing-message-templates.md#template-publication)

The Unprocessed bounce mails section has been updated with more details on the Forwarding address and Address for errors fields. [Read more](../../installation/using/deploying-an-instance.md)

A new section on workflow planning best practices has been added. [Read more](../../workflow/using/workflow-best-practices.md)

Added two new options to the list of Campaign options: XtkSecurity_Restrict_EditXML and NmsOperation_OperationMgtDebug.
 [Read more](../../installation/using/configuring-campaign-options.md)

Added information on the different external accounts available in Campaign Classic and how to configure them.
 [Read more](../../installation/using/external-accounts.md)

Updated Analytics Connector section to reflect interface changes.
 [Read more](../../platform/using/adobe-analytics-connector.md)

Added information on the Billing report.
 [Read more](../../production/using/monitoring-processes.md)

Updated documentation on the Shared audiences integration.
 [Read more](../../integrations/using/configuring-shared-audiences-integration-in-adobe-campaign.md)

The following technote has been updated: [SMS connector protocol and settings](https://helpx.adobe.com/campaign/kb/sms-connector-protocol-and-settings.html).

The Technical workflows section has been updated. [Read more](../../workflow/using/about-technical-workflows.md)

The Campaign Domain Name Setup procedure has been improved and updated.

The Campaign Hardware Sizing Guide has been updated. [Read more](https://helpx.adobe.com/campaign/kb/hardware-sizing-guide.html)

Information was added on Query Banding for the Teradata external account. [Read more](../../installation/using/external-accounts.md)

### January 2019{#release-doc-16-01-2019}

The Experience Cloud Triggers technote has been updated. [Read more](../../integrations/using/about-triggers.md)

A note was added in the offer approval section to specify  that the "Content approved" mention indicates that the content approval process has been achieved, whether all offers have been enabled/approved or not. [Read more](../../interaction/using/offer-catalog-overview.md)

A new section was added in the Installation guide, listing options from the Administration / Platform / Options node. [Read more](../../installation/using/configuring-campaign-options.md)

Information was added about the use of seed addresses to protect your mailing list. [Read more](../../delivery/using/creating-seed-addresses.md)

Key steps when creating and sending a delivery have been regrouped into a new section, with references to the various channels when needed. [Read more](../../delivery/using/steps-about-delivery-creation-steps.md)

The [Email archiving](../../installation/using/email-archiving.md) section has been moved, reorganized and improved with clarified information:

* Best practices have been added regarding emails per connection and BCC sending IPs parameters.

* We've updated the steps to upgrade to the new email archiving system (BCC) if you were already using email archiving with an older build (prior to Adobe Campaign 17.2 – build 8795).

A use case has been added to the Automating with Workflows guide: Sending personalized alerts to operators. [Read more](../../workflow/using/sending-personalized-alerts-to-operators.md)

The "Migrating to a new version" section has been updated. The documentation now only details the steps for a migration to Adobe Campaign Classic v7 from any older version, as it is no longer possible to migrate to Adobe Campaign v6.11. [Read more](../../migration/using/about-migration.md)

The "Retries after a delivery temporary failure" section has been clarified. [Read more](../../delivery/using/understanding-delivery-failures.md)

Links to the "Digital Content Editor" section have been added to the "Defining the email content" section. [Read more](../../delivery/using/defining-the-email-content.md)

The "Transactional messaging architecture" section has been updated with a warning specifying that the control and the execution instances cannot be installed on the same machine. [Read more](../../message-center/using/transactional-messaging-architecture.md)

The "Workflow monitoring" section has been updated with a note for builds between 8700 and 8977 (18.10), including a link to the technote on how to install the Workflow HeatMap package for these builds. [Read more](../../workflow/using/heatmap.md)

Added a use case on how to send an email with custom data fields using the Enrichment activity in a workflow. [Read more](../../workflow/using/email-enrichment-with-custom-date-fields.md)

Feature videos have been moved [here](https://experienceleague.adobe.com/docs/campaign-classic-learn/tutorials/overview.html).
-->
