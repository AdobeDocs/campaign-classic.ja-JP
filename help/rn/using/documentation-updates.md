---
title: Adobe Campaign Classic ドキュメントのアップデート
description: このページには、Adobe Campaign Classic の各リリースに関するすべての新機能とドキュメントのアップデートが記載されています。
page-status-flag: never-activated
uuid: 269d590c-5a6d-40b9-a879-02f5033863fc
contentOwner: sauviat
products: SG_CAMPAIGN/CLASSIC
audience: rns
content-type: reference
topic-tags: latest-release-notes
discoiquuid: 5df34f55-135a-4ea8-afc2-f9427ce5ae7b
index: y
internal: n
snippet: y
translation-type: tm+mt
source-git-commit: 11aab98507be594bde79e21c9a5e8ae0b2e8fe36

---


# ドキュメントのアップデート{#documentation-updates}

Adobe Campaign Classic ドキュメントのすべての最新アップデートについて説明します。

このページには、Adobe Campaign Classic の各リリースに関するすべての新機能とドキュメントのアップデートが記載されています。

[Adobe Campaign Classic リリースノート](../../rn/using/latest-release.md)もご覧ください。

## April 2020 {#april-2020}

FDA権限テーブルは、「外部データベースへのアクセス」(FDA)ドキュメントに移動されました。 [詳細を表示](../../platform/using/remote-database-access-rights.md)

FAQが更新され、ソフトキャッシュとハードキャッシュをクリアする方法に関するヒントが追加されました。 [詳細を表示](../../platform/using/faq-campaign-config.md#perform-soft-cache-clear)

データモデルのベストプラクティスの節が、インデックスに関する追加情報と共に改善されました。 [詳細を表示](../../configuration/using/data-model-best-practices.md#indexes)

Adobe Campaignの事前定義データモデルについて説明する節が更新され、あらかじめ用意されている各表の詳細と、関連するモジュールへのリンクが追加されました。 [詳細を表示](../../configuration/using/data-model-description.md)

## 2020 年 3 月 {#march-2020}

データモデルのベストプラクティスのページが更新され、 [Sequences](../../configuration/using/data-model-best-practices.md#sequences)、 [Performance](../../configuration/using/data-model-best-practices.md#performance) 、 [Largeの各テーブルなどの新しいセクションが追加さ](../../configuration/using/data-model-best-practices.md#large-tables)れました。 [詳細を表示](../../configuration/using/data-model-best-practices.md)

Adobe Campaignの事前定義データモデルとあらかじめ用意されている表のインタラクションについて説明する新しい節が利用できるようになりました。 [詳細を表示](../../configuration/using/data-model-description.md)

その他のリソースがドキュメントホームページに追加されました。 [詳細を表示](../../campaign-classic-home.md)

アドビのターゲットのダイナミックオファーをAdobe Campaignの電子メールに統合する方法に関する使用例が追加されました。 [詳細を表示](../../integrations/using/inserting-a-dynamic-image.md)

Adobe Campaignで使用できる様々な言語の詳細を説明する新しいセクションが提供されました。 [詳細を表示](../../platform/using/adobe-campaign-workspace.md#languages)

アクセス管理ページが更新され、詳細な情報が表示されました。ネームド権限 [詳細を表示](../../platform/using/access-management.md#named-rights)

## February 2020 {#february-2020}

Adobe Campaignデータモデルのデザイン時に、ベストプラクティスと主要な推奨事項の概要を示す新しい節が利用できるようになりました。 [詳細を表示](../../configuration/using/data-model-best-practices.md)

「電子メールの配信品質」セクションの名前が「技術的な電子メール設定」に変更されました。 [詳細を表示](../../installation/using/email-deliverability.md)

「配信品質FAQ」ドキュメントが更新され、「割り当てが満たされました」というエラーメッセージの詳細が表示されました。 [詳細を表示](https://helpx.adobe.com/campaign/kb/acc-deliverability-faq.html#FAQ)

3つの電子メールプロバイダー(Gmail、Outlook、Mail.ru)によってEmail用のAMPがサポートされるようになりました。AMPを使用してインタラクティブコンテンツを定義する方法を説明する節が更新されました。 [詳細を表示](../../delivery/using/defining-interactive-content.md)

「電子メールのアーカイブ」の節が明確になりました。 [詳細を表示](../../installation/using/email-archiving.md#recommendations-and-limitations)

## 20.1 - 17/02/2020{#release-20-1}

**リリースに含まれる新機能**

雪片FDAコネクタ — 詳 [細情報](../../platform/using/specific-configuration-database.md#configure-access-to-snowflake)

HadoopFDAコネクタの改良点 — [詳細](../../platform/using/specific-configuration-database.md#configure-access-to-hadoop-3)

**リリースに伴うその他のドキュメントのアップデート**

インス [トール](../../installation/using/before-reading.md)、 [実稼働](../../production/using/foreword.md) 、設定ガイドは [](../../configuration/using/additional-parameters.md) 、nlserverサービスの起動時に使用する新しいsystemdユニットで更新されました。 引き続き/etc/init.d/nlserver6を使用できますが、nlserverサービスとの対話にはsystemctlコマンドを使用することをお勧めします。

インストールガイドが更新され、互換表の最新バージョンと同期されました。 新しいサポート対象システムが追加されました。 非推奨およびサポートされていないシステムへの出現は削除されました。 [詳細を表示](../../installation/using/before-reading.md)

互換性マトリックスが更新され、Hadoop 3.0およびSnowflakeのFDAコネクタが追加されました。 [詳細を表示](https://helpx.adobe.com/campaign/kb/compatibility-matrix.html)

IPインストールのベストプラクティスアフィニティがインストールガイドに追加されました。 [詳細を表示](../../installation/using/email-deliverability.md#list-of-ip-addresses-to-use)

データベースのクリーンアップワークフローセクションが更新されました。 指定されたバッチ数値は、コードの実装を反映しています。 [詳細を表示](../../production/using/database-cleanup-workflow.md)

HTTPを使用したFDAに関する制限が、トランザクションメッセージングガイドに追加されました。 [詳細を表示](../../production/using/database-cleanup-workflow.md)

新しいオプションに関する情報が追加され、およびワークフローのアクティビティのタイムアウト期間を定義で **[!UICONTROL JavaScript code]** きるように **[!UICONTROL Advanced JavaScript code]** なりました。 [詳細を表示](../../workflow/using/sql-code-and-javascript-code.md)

> > nodeにある新しい **[!UICONTROL Start Pending]** 表示に情報が **[!UICONTROL Administration]** 追加さ **[!UICONTROL Audit]** れまし **[!UICONTROL Workflows Status]** た。 [詳細を表示](../../workflow/using/monitoring-workflow-execution.md#filtering-workflows-status)

プッシュ [通知の送信ガイドは](../../delivery/using/about-mobile-app-channel.md) 、移動され、整理および改善され、情報が明確になりました。

URLレポート設定の新しいパラメーターは、ここで説明されて [います](../../reporting/using/properties-of-the-report.md#defining-additional-settings)。

Campaign Classic On-premise &amp; Hosted機能マト **リックスページが新しいFDA** ・コネクタで更新されました。 [詳細を表示](https://helpx.adobe.com/campaign/kb/acc-on-prem-vs-hosted.html)

Campaign Classic機能マ **トリックスページが** 、更新されました。 [詳細を表示](https://helpx.adobe.com/campaign/kb/compatibility-matrix.html)

新しいワークフ **[!UICONTROL Cleanup of Nmsaddress]** ローはここに記載され [ています](../../production/using/database-cleanup-workflow.md#cleanup-of-nmsaddress)。

ワークフローでワークフローを使用する場合に、クエリアクティビティの制限が追加されました。 [詳細を表示](../../workflow/using/query.md).

ソフトエラーの場合にアドレスを強制隔離に送信するための、拡張された電子メールアドレス検証ルールの詳細を説明する新しい節が追加されました。 [詳細を表示](../../delivery/using/understanding-quarantine-management.md#soft-error-management)

インスタンスが拡張MTAを使用しているかどうかを示す設定ファイルのパラメーターがドキュメントに記載されています。 [詳細を表示](../../installation/using/the-server-configuration-file.md#mta)

## 2020 年 1 月{#january-2020}

配信品質の節が移動および再編成され、新しい内容で改善されました。[詳細を表示](../../delivery/using/about-deliverability.md)

Adobe Campaign Classic のデータモデルの基本と各テーブルの説明にアクセスする方法について説明する新しい節が追加されました。[詳細を表示](../../configuration/using/about-data-model.md)

Adobe Campaign Enhanced MTA の記述を更新し、Enhanced MTA ヘッダーをすべてのメッセージに追加しないインスタンスに、特定のタイポロジパッケージをインストールする方法について詳細が追加されました。[詳細を表示](https://helpx.adobe.com/campaign/kb/campaign-enhanced-mta.html#impacts)

クエリの設計に関する使用事例が別個の節に再編成されました。[詳細を表示](../../workflow/using/querying-recipient-table.md)

Adobe Campaign Classic のオファー管理およびインタラクションモジュールの使用に関するヒントとテクニックについて、新しい節が追加されました。[詳細を表示](../../interaction/using/interaction-best-practices.md#tips-managing-offers)

オファーの管理方法の理解を深めるのに役立つ、複数のビデオへのリンクがインタラクションドキュメントに追加されました。[詳細を表示](../../interaction/using/interaction-and-offer-management.md)

インスタンスで実行されるクエリを最適化する方法に関するベストプラクティスの記述がドキュメントに統合されました。[詳細を表示](../../workflow/using/query.md#optimizing-queries)

レポートガイドが更新、再編成されました。[詳細を表示](../../reporting/using/about-adobe-campaign-reporting-tools.md)

ワークフローでインスタンス変数を使用する方法の例が追加されました。[詳細を表示](../../workflow/using/javascript-scripts-and-templates.md)

## 2019 年 12 月 {#december-2019}

「WdbcOptions_TempDbName」オプションがキャンペーンオプションのリストに追加されました。[詳細を表示](../../installation/using/configuring-campaign-options.md)

FDA のマトリックスページは、[ここ](/help/rn/using/assets/fda_rdbms_rights.pdf)に移動されました。

アクセス権のマトリックスページは、[ここ](https://docs.adobe.com/content/help/en/campaign-classic/using/getting-started/administration-basics/assets/accessrights.pdf)に移動されました。

AMP でインタラクティブコンテンツを定義する方法について説明する節が移動されました。[詳細を表示](../../delivery/using/defining-interactive-content.md)

## 19.2 - 2019 年 12 月 2 日{#release-19-2}

**リリースに含まれる新機能**

カリフォルニア州消費者プライバシー法（CCPA） - [詳細を表示](https://helpx.adobe.com/campaign/kb/acc-privacy.html)

AMP を使用したインタラクティブコンテンツ - [詳細を表示](../../delivery/using/defining-interactive-content.md)

ワークフローのライブ監視 - [詳細を表示](../../workflow/using/monitoring-workflow-execution.md#filtering-workflows-status)

セキュア SMS メッセージ（TLS） - [詳細を表示](https://helpx.adobe.com/campaign/kb/sms-connector-protocol-and-settings.html)

**リリースに伴うその他のドキュメントのアップデート**

Adobe Campaign Enhanced MTA のドキュメントが入手できるようになりました。[詳細を表示](https://helpx.adobe.com/campaign/kb/campaign-enhanced-mta.html)

キャンペーン内で「開始準備中」の状態に留まるワークフローをトラブルシュートする方法について、新しい節が追加されました。 [詳細を表示](../../production/using/workflow-execution.md#start-as-soon-as-possible-in-campaigns)

新しい「NmsOperation_DeliveryPreparationWindow」および「WdbcKillSessionPolicy」オプションがキャンペーンオプションのリストに追加されました。[詳細を表示](../../installation/using/configuring-campaign-options.md)

Adobe Campaign Classic データモデルの基本を説明する新しいドキュメントが追加されました。[詳細を表示](https://helpx.adobe.com/campaign/kb/acc-datamodel.html)

配信プロパティの新しいオプション「**最長パーソナライゼーション実行時間**」については、この[節](../../delivery/using/personalization-fields.md#timing-out-personalization)で説明されています。

logon() および query() で **HttpServletRequest** を使用する API 呼び出しの例が更新されました。[詳細を表示](../../configuration/using/web-service-calls.md)

スキーマ定義の **sqlDefault** 属性に関する推奨事項が追加されました。[詳細を表示](../../configuration/using/elements-and-attributes.md#attribute-description)

Adobe Campaign とアドビのリアルタイムカスタマーデータプラットフォーム（CDP）の統合については、**Adobe Experience Cloudとの統合**&#x200B;ガイドで参照されるようになりました。[詳細を表示](../../integrations/using/about-campaign-integrations.md)

## 2019 年 11 月 {#november-2019}

[ミッドソーシングサーバーの多重化](../../installation/using/mid-sourcing-server.md#multiplexing-the-mid-sourcing-server)および[複数のコントロールインスタンスのサポート](../../message-center/using/transactional-messaging-architecture.md#supporting-several-control-instances)の節に、完全にホストされたクライアントおよびハイブリッドクライアントにおいては、これらのデプロイメントがサポートされていないことに言及する警告が追加されました。

E メールの送信時に使用する文字エンコーディングの強制適用方法を説明する新しい節が追加されました。[詳細を表示](../../delivery/using/sending-messages.md#character-encoding)

アクセス管理に関する節が更新され、「**プライバシーデータ権限**」が追加されました。[詳細を表示](../../platform/using/access-management.md#named-rights)

パーソナライゼーションフィールドの内容は 1024 文字を超過できないことを明確にする情報が追加されました。[詳細を表示](../../delivery/using/personalization-fields.md)

コントロールパネルのドキュメントは、新しいコラボレーションドキュメントセットに統合されました。[詳細を表示](https://docs.adobe.com/content/help/en/control-panel/using/control-panel-home.html)

配信のベストプラクティス入門ガイドが更新されました。[詳細を表示](https://helpx.adobe.com/campaign/kb/delivery-best-practices.html)

## 2019 年 10 月 {#october-2019}

Campaign Standard および Campaign Classic のエラーメッセージのリストが更新されました。[詳細を表示](https://docs.campaign.adobe.com/doc/AC/en/technicalResources/error_messages/error_codes.html)

GDPR の入門ガイドが改善され、強化されました。GDPR や CCPA を含む、プライバシー管理に関するドキュメントになりました。[詳細を表示](https://helpx.adobe.com/content/help/en/campaign/kb/campaign-privacy.html)

Campaign Classic でのトラッキングについて、新しいトラブルシューティングページが追加されました。[詳細を表示](https://helpx.adobe.com/campaign/kb/classic-tracking-troubleshooting.html)

Adobe Analytics Data Connector の新しいベストプラクティスのページが追加されました。[Adobe Analytics Data Connector の詳細を表示](../../platform/using/adobe-analytics-data-connector.md)

配信のベストプラクティス入門ガイドが移動され、更新されました。[詳細を表示](https://helpx.adobe.com/campaign/kb/delivery-best-practices.html)

複数の外部アカウントが拡張された汎用 SMPP コネクタを同じプロバイダーアカウントで使用する際の問題を回避するための推奨事項が、SMS チャネルのドキュメントに追加されました。[詳細を表示](../../delivery/using/sms-channel.md#automatic-reply)

ワークフローの同時実行を防ぐ方法に関する情報がスケジューラーアクティビティのドキュメントに追加されました。[詳細を表示](../../workflow/using/scheduler.md)

オンプレミスインストールの受信ボックスレンダリングを設定する手順がドキュメントに追加されました。[詳細を表示](../../delivery/using/inbox-rendering.md#activating-inbox-rendering)

## 2019 年 9 月 {#september-2019}

Campaign Classic の管理に関する一般的なガイドラインを提供する新しいページが追加されました。[詳細を表示](https://helpx.adobe.com/campaign/kb/acc-maintenance.html)

ワークフロー監視に関する情報は、新しい専用の節に集約されました。[詳細を表示](../../workflow/using/monitoring-workflow-execution.md)

Adobe Campaign Classic のトラッキングに関する一般的なガイドラインを提供する新しいページが追加されました。[詳細を表示](https://helpx.adobe.com/campaign/kb/acc-tracking.html)

ワークフローと配信のパフォーマンス改善のためのベストプラクティスが更新されました。[ワークフローの詳細](../../workflow/using/workflow-best-practices.md)および[配信の詳細](../../delivery/using/monitoring-a-delivery.md#best-practices-performance)を参照してください。

## 19.1 - 2019 年 5 月 30 日{#release-19-1}

**リリースに含まれる新機能**

コントロールパネル - [詳細を表示](https://docs.adobe.com/content/help/en/control-panel/using/control-panel-home.html)

監査記録 - [詳細を表示](https://docs.campaign.adobe.com/doc/AC/en/PRO_Production_procedures_Audit_trail.html)

**リリースに伴うその他のドキュメントのアップデート**

ビルドアップグレードに関する新しい FAQ が作成されました。[詳細を表示](https://helpx.adobe.com/campaign/kb/build-upgrade-faq.html)

[互換性マトリックス](https://helpx.adobe.com/campaign/kb/compatibility-matrix.html)が更新されました。サポートされるデータベースシステム、Android／iOS のバージョン、および関連する SDK のリストが更新されました。[19.0 互換性マトリックス](https://helpx.adobe.com/campaign/kb/compatibility-matrix-19-0.html)がアーカイブされました。

「Campaign Classic の機能の廃止と削除」ページが更新されました。[詳細を表示](https://helpx.adobe.com/campaign/kb/deprecated-and-removed-features.html)

インストールガイドにサーバー設定ファイルの説明が追加されました。[詳細を表示](https://docs.campaign.adobe.com/doc/AC/en/INS_Appendices_The_server_configuration_file.html)

ホストモデルおよびハイブリッドモデルのインストールおよび設定手順を説明する節が追加されました。[詳細を表示](https://docs.campaign.adobe.com/doc/AC/en/INS_Hybrid_and_Hosted_models_Introduction.html)

Campaign サーバーのアンインストール手順を説明する節が追加されました。[詳細を表示](https://docs.campaign.adobe.com/doc/AC/en/INS_Appendices_Uninstalling_Campaign.html)

The [security](https://docs.campaign.adobe.com/doc/AC/getting_started/EN/security.html), [deliverability](https://docs.campaign.adobe.com/doc/AC/getting_started/EN/deliverability.html) and [privacy](https://helpx.adobe.com/campaign/kb/acc-privacy.html) getting started guides have been updated.

前処理ワークフローオプションの説明が更新され、製品の変更が反映されました。[詳細を表示](https://docs.campaign.adobe.com/doc/AC/en/WKF_Repository_of_activities_Action_activities.html#Data_loading__file_)

Experience Cloud Triggersーのテクニカルノートが更新されました。[詳細を表示](https://helpx.adobe.com/campaign/kb/triggers-and-campaign.html)

エラーメッセージのリストが更新されました。[詳細を表示](https://docs.campaign.adobe.com/doc/AC/en/technicalResources/error_messages/error_codes.html)

トランザクションメッセージングの SOAP 認証方法に関する詳細が追加されました。[詳細を表示](https://docs.campaign.adobe.com/doc/AC/en/MCE_Introduction_Event_description.html)

Apache の設定手順が更新されました。[詳細を表示](https://docs.campaign.adobe.com/doc/AC/en/INS_Installing_Campaign_in_Linux__Integration_into_a_Web_server.html#Configuring_Apache_web_server_in_RHEL)

Campaign Standard および Classic のエンドポイントのリストを含む新しいページが追加されました。[詳細を表示](https://helpx.adobe.com/campaign/kb/campaign-endpoints.html)

データパッケージのベストプラクティス記事が更新されました。[詳細を表示](https://helpx.adobe.com/campaign/kb/data-package-best-practices.html)

オファーの管理に関するドキュメントが更新され、ベストプラクティスを説明する新しい節が追加されました。[詳細を表示](https://docs.campaign.adobe.com/doc/AC/en/ITA_Interaction_Overview_Interaction_best_practices.html)

Adobe Campaign Classic のオファーカタログの使用に関する新しいナレッジベース記事が作成されました。[詳細を表示](https://helpx.adobe.com/campaign/kb/offer-best-practices.html)

サブワークフローアクティビティの節に、使用例が追加されました。[詳細を表示](../../workflow/using/sub-workflow.md)

[Campaign Classic オンプレミス／ホスト機能のマトリックス](https://helpx.adobe.com/campaign/kb/acc-on-prem-vs-hosted.html)のナレッジベース記事が更新され、E メールのアーカイブに関する情報が追加されました。

トランザクションメッセージングのドキュメントが更新され、テンプレートのパブリッシュに関する注意事項が追加されました。[詳細を表示](https://docs.campaign.adobe.com/doc/AC/en/MCE_Template_publication.html)

未処理のバウンスメールの節が更新され、「転送先アドレス」フィールドおよび「エラーのアドレス」フィールドに関する詳細が追加されました。[詳細を表示](https://docs.campaign.adobe.com/doc/AC/en/INS_Initial_configuration_Deploying_an_instance.html#Unprocessed_bounce_mails)

ワークフロー計画のベストプラクティスに関する新しい節が追加されました。[詳細を表示](https://docs.campaign.adobe.com/doc/AC/en/WKF__General_operation_Workflow_best_practices.html#Execution_and_performance)

キャンペーンオプションのリストに、XtkSecurity_Restrict_EditXML および NmsOperation_OperationMgtDebug の 2 つの新しいオプションが追加されました。
[詳細を表示](https://docs.campaign.adobe.com/doc/AC/en/INS_Appendices_Configuring_Campaign_options.html)

Campaign Classic で使用できる様々な外部アカウントと、その設定方法に関する情報が追加されました。
[詳細を表示](https://docs.campaign.adobe.com/doc/AC/en/PTF_Administration_basics_External_accounts.html)

Analytics Data Connector の節が更新され、インターフェイスの変更が反映されるようになりました。
[詳細を表示](https://docs.campaign.adobe.com/doc/AC/en/PTF_Connectors_Adobe_Analytics_Data_Connector.html)

請求レポートに関する情報が追加されました。
[詳細を表示](https://docs.campaign.adobe.com/doc/AC/en/PRO_Production_procedures_Monitoring_processes.html#Billing_report)

共有オーディエンスの統合に関するドキュメントが更新されました。
[詳細を表示](https://docs.campaign.adobe.com/doc/AC/en/ITG_Audience_sharing_Configuring_shared_audiences_integration_in_Adobe_Campaign.html)

[SMS コネクタのプロトコルと設定](https://helpx.adobe.com/campaign/kb/sms-connector-protocol-and-settings.html)および[シーケンスの自動生成](https://helpx.adobe.com/campaign/kb/sequence_auto_generation.html#Switchtoadedicatedsequence)のテクニカルノートが更新されました。

テクニカルワークフローの節が更新されました。[詳細を表示](https://docs.campaign.adobe.com/doc/AC/en/WKF_Technical_workflows_About_technical_workflows.html)

Campaign ドメイン名の設定手順が改善および更新されました。[詳細を表示](https://helpx.adobe.com/campaign/kb/domain-name-delegation.html)

Google Cloud Messaging（GCM）から Firebase Cloud Messaging（FCM）への Android アプリの移行手順が更新されました。[詳細を表示](https://helpx.adobe.com/campaign/kb/migrate-to-fcm.html)

Campaign ハードウェアのサイズ設定ガイドが更新されました。[詳細を表示](https://helpx.adobe.com/campaign/kb/hardware-sizing-guide.html)

Teradata 外部アカウントの Query Band に関する情報が追加されました。[詳細を表示](https://docs.campaign.adobe.com/doc/AC/en/PTF_Administration_basics_External_accounts.html#External_database_external_account)

## 2019 年 1 月{#release-doc-16-01-2019}

Experience Cloud Triggersーのテクニカルノートが更新されました。[詳細を表示](https://helpx.adobe.com/campaign/kb/triggers-and-campaign.html)

オファーの承認の節に注意事項を追加し、「承認コンテンツ」の表示は、すべてのオファーが有効化または承認されているかどうかに関わらず、コンテンツ承認プロセスが達成されたことを示すことを明確にしました。[詳細を表示](https://docs.campaign.adobe.com/doc/AC/en/ITA_Managing_an_offer_catalog_Approving_and_activating_an_offer.html#Approving_offer_content)

新しい節がインストールガイドに追加され、管理／プラットフォーム／オプションノードのオプションが一覧で示されました。[詳細を表示](https://docs.campaign.adobe.com/doc/AC/en/INS_Appendices_Configuring_Campaign_options.html)

メーリングリストを保護するためのシードアドレスの使用に関する情報が追加されました。[詳細を表示](https://docs.campaign.adobe.com/doc/AC/en/DLV_Using_seed_addresses_About_seed_addresses.html)

配信を作成して送信する際の重要な手順が新しい節に再編成されました。必要に応じて様々なチャネルの参照も追加されました。[詳細を表示](../../delivery/using/steps-about-delivery-creation-steps.md)

[E メールのアーカイブ](https://docs.campaign.adobe.com/doc/AC/en/INS_Additional_configurations_Email_archiving.html)の節が移動および再編成され、明確になった情報で改善されました。

* 接続あたりの E メールおよび BCC 送信 IP パラメーターに関するベストプラクティスが追加されました。[詳細を表示](https://docs.campaign.adobe.com/doc/AC/en/INS_Additional_configurations_Email_archiving.html#Best_practices)

* 以前のビルド（Adobe Campaign 17.2 ビルド 8795 以前）で E メールアーカイブを既に使用している場合に、新しい E メールアーカイブシステム（BCC）へアップグレードする手順を更新しました。[詳細を表示](https://docs.campaign.adobe.com/doc/AC/en/INS_Additional_configurations_Email_archiving.html#Updated_email_archiving_system__BCC_)

ワークフローによる自動化ガイドに、使用例、「パーソナライズされたアラートのオペレーターへの送信」が追加されました。[詳細を表示](https://docs.campaign.adobe.com/doc/AC/en/WKF_Use_cases_Sending_personalized_alerts_to_operators.html)

新しいバージョンへの移行の節が更新されました。Adobe Campaign v6.11 への移行ができなくなったので、このドキュメントでは、Adobe Campaign Classic v7 への移行手順のみの詳細を説明しています。[詳細を表示](https://docs.campaign.adobe.com/doc/AC/en/MIG_Migration_overview_About_migration.html)

一時的な配信エラーの後の再試行の節が明確化されました。[詳細を表示](https://docs.campaign.adobe.com/doc/AC/en/DLV_Monitoring_deliveries_Understanding_delivery_failures.html#Retries_after_a_delivery_temporary_failure)

E メールコンテンツの定義の節に、デジタルコンテンツエディターの節へのリンクが追加されました。[詳細を表示](https://docs.campaign.adobe.com/doc/AC/en/DLV_Sending_emails_Defining_the_email_content.html#Message_content)

トランザクションメッセージングのアーキテクチャの節が更新され、コントロールインスタンスと実行インスタンスは同じマシンにインストールできないことを説明する警告が追加されました。[詳細を表示](https://docs.campaign.adobe.com/doc/AC/en/MCE_Introduction_Transactional_messaging_architecture.html)

ワークフローの監視の節が更新され、ビルド 8700 ～ 8977（18.10）に関する注意事項が追加されました。これらのビルド用のワークフローヒートマップパッケージのインストール方法に関するテクニカルノートへのリンクも含まれます。[詳細を表示](https://docs.campaign.adobe.com/doc/AC/en/PRO_Production_procedures_Monitoring_processes.html#About_the_Workflow_HeatMap)

ワークフローのエンリッチメントアクティビティを使用してカスタムデータフィールドを含む E メールを送信する方法に関する使用例が追加されました。[詳細を表示](https://docs.campaign.adobe.com/doc/AC/en/WKF_Use_cases_Email_enrichment_with_custom_date_fields.html)

機能に関するビデオが[ここ](https://docs.adobe.com/content/help/en/campaign-learn/campaign-classic-tutorials/overview.html)に移動されました。

[Teradata](https://helpx.adobe.com/campaign/kb/campaign_fda_teradata.html) と [MySQL 5.7](https://helpx.adobe.com/campaign/kb/campaign_fda_mysql.html) に関する 2 つのテクニカルノートが追加されました。

## 18.10 - 2018 年 11 月 5 日{#release-18-10}

**リリースに含まれる新機能**

プッシュ通知の強化 - [詳細を表示](https://docs.campaign.adobe.com/doc/AC/en/DLV_Sending_push_notifications_Setting_up_mobile_app_channel.html#Integrating_the_SDK_into_the_mobile_application)

SQL データ管理アクティビティ - [詳細を表示](https://docs.campaign.adobe.com/doc/AC/en/WKF_Repository_of_activities_Action_activities.html#SQL_Data_Management)

ワークフローの監視 - [詳細を表示](https://docs.campaign.adobe.com/doc/AC/en/PRO_Production_procedures_Monitoring_processes.html#Workflow_monitoring)

**リリースに伴うその他のドキュメントのアップデート**

Campaign Classic API を[専用ページ](https://docs.campaign.adobe.com/doc/AC/en/jsapi/index.html)から入手できるようになりました。jsapi.chm ファイルを使用していた場合は、新しいオンラインバージョンを参照する必要があります。

互換性マトリックスが更新されました。[詳細を表示](https://helpx.adobe.com/campaign/kb/compatibility-matrix.html)

「Campaign Classic の機能の廃止と削除」ページが更新されました。[詳細を表示](https://helpx.adobe.com/campaign/kb/deprecated-and-removed-features.html)

[リリースノート](https://docs.campaign.adobe.com/doc/AC/en/RN.html)および[従来のリリースノート](https://docs.campaign.adobe.com/doc/AC/en/RN_legacy.html)では、取り消されたビルドに対する警告が追加されました。17.9、18.4 および 18.6 の累積ビルドも追加されました。

[セキュリティ](https://docs.campaign.adobe.com/doc/AC/getting_started/EN/security.html)、[配信品質](https://docs.campaign.adobe.com/doc/AC/getting_started/EN/deliverability.html)および[ビルドアップグレード](https://docs.campaign.adobe.com/doc/AC/getting_started/EN/buildUpgrade.html)の入門ガイドが更新されました。

The [Privacy](https://helpx.adobe.com/campaign/kb/acc-privacy.html) getting started guide has been updated with information on how to invoke the API externally and how to use queryDef to query for the status and download the GDPR file.

アウトバウンド送信時に E メールの添付ファイルをその場で追加する、トランザクションメッセージングの使用例が追加されました。[詳細を表示](https://docs.campaign.adobe.com/doc/AC/en/MCE_Use_case_Purpose.html)

接続しきい値のトラブルシューティングの節が更新されました。[詳細を表示](https://docs.campaign.adobe.com/doc/AC/en/PRO_Troubleshooting_Connection_thresholds.html)

プロキシ接続の設定方法に関する節が追加されました。[詳細を表示](https://docs.campaign.adobe.com/doc/AC/en/INS_Additional_configurations_Configuring_Campaign_server.html#Proxy_connection_configuration)

認証済み外部コマンドの制限に関する節が更新されました。[詳細を表示](https://docs.campaign.adobe.com/doc/AC/en/INS_Additional_configurations_Configuring_Campaign_server.html#Restricting_authorized_external_commands)

SFTP の使用に関するトラブルシューティングの節が追加されました。[詳細を表示](https://docs.campaign.adobe.com/doc/AC/en/PTF_Importing_and_exporting_data_SFTP_server_usage.html)

メッセージの送信ガイドの概要セクションが再編成されました。配信作成のグローバルプロセスおよび様々な配信タイプに関する情報が追加されました。[詳細を表示](https://docs.campaign.adobe.com/doc/AC/en/DLV_About_deliveries_and_channels_Communication_channels.html)

エラーメッセージのリストが更新されました。[詳細を表示](https://docs.campaign.adobe.com/doc/AC/en/technicalResources/error_messages/error_codes.html)

シードアドレスの使用方法に関する節が、メッセージの送信ガイドの概要セクションに移動されました。[詳細を表示](https://docs.campaign.adobe.com/doc/AC/en/DLV_Using_seed_addresses_About_seed_addresses.html)

新規ワークフローの使用例、「同時実行されるワークフローからのアップデートの管理」が追加されました。[詳細を表示](https://docs.campaign.adobe.com/doc/AC/en/WKF_Use_cases_Coordinating_data_updates.html)

受信ボックスレンダリングの節が更新され、Litmus に関する詳細情報およびより詳細な手順が追加されました。[詳細を表示](https://docs.campaign.adobe.com/doc/AC/en/DLV_Deliverability_management_Inbox_rendering.html#Multiplexing_the_mid-sourcing_server)

SpamAssassin の節が改善されました。[詳細を表示](https://docs.campaign.adobe.com/doc/AC/en/DLV_Deliverability_management_SpamAssassin.html)

頻度ルールによるマーケティング疲労の管理の節に使用例が追加されました。[詳細を表示](https://docs.campaign.adobe.com/doc/AC/en/CMP_Campaign_Optimization_Pressure_rules.html#Sending_only_the_highest-weighted_messages)

クロスチャネル配信ワークフローの作成方法を説明する新しい使用例が追加されました。[詳細を表示](https://docs.campaign.adobe.com/doc/AC/en/WKF_Use_cases_Cross-channel_delivery_workflow.html)

E メールのアーカイブの節に推奨事項が追加されました。[詳細を表示](https://docs.campaign.adobe.com/doc/AC/en/INS_Additional_configurations_Email_deliverability.html#Activating_emails_BCC_archiving)

Adobe Campaign の最適な使用のための最低画面解像度に関する新しい推奨事項が追加されました。[詳細を表示](https://docs.campaign.adobe.com/doc/AC/en/PTF_Starting_with_Adobe_Campaign_Adobe_Campaign_workspace.html#Screen_resolution)

Experience Manager 統合ガイドが更新され、この統合の設定が明確化されました。[詳細を表示](https://docs.campaign.adobe.com/doc/AC/en/ITG_Adobe_Experience_Manager_About_Adobe_Experience_Manager.html)

グループタイプリストとリストタイプリストの違いに関する情報が追加されました。[詳細を表示](https://docs.campaign.adobe.com/doc/AC/en/PTF_Profile_management_Creating_and_managing_lists.html#About_lists_in_Adobe_Campaign)

レポートエクストラクトを添付ファイルとして E メールで送信するためのコードが更新されました。[詳細を表示](https://docs.campaign.adobe.com/doc/AC/en/WKF_Use_cases_Sending_a_report_to_a_list.html#Step_3-_Creating_the_workflow)

過去 7 日間、E メールを開封していない受信者をフィルターするクエリの作成方法の例が追加されました。[詳細を表示](https://docs.campaign.adobe.com/doc/AC/en/WKF_Use_cases_Designing_queries.html#Recipients_who_did_not_open_any_delivery)

Adobe Experience Cloud 統合ガイドで、オーディエンスの共有が更新されました。[詳細を表示](https://docs.campaign.adobe.com/doc/AC/en/ITG_Audience_sharing_Sharing_audiences_with_Adobe_Experience_Cloud.html)

よくある質問のヘルプページに、Campaign で利用可能な言語、Web フォームの翻訳および多言語 E メールに関する情報が追加されました。[詳細を表示](../../platform/using/common-questions.md)

英語（米国）と英語（英国）のインスタンスの違いが、専用の節で説明されるようになりました。[詳細を表示](https://docs.campaign.adobe.com/doc/AC/en/PTF_Starting_with_Adobe_Campaign_Adobe_Campaign_workspace.html#Formats_and_units)

[よくある質問](../../platform/using/common-questions.md)のヘルプページに、エラーメッセージのページへのリンクが追加されました。

「オープン」トラッキングモードに関する情報が追加されました。[詳細を表示](https://docs.campaign.adobe.com/doc/AC/en/DLV_Tracking_messages_Personalizing_URL_tracking.html)

Web アプリケーションおよび Web フォームの最低解像度に関する情報が追加されました。[詳細を表示](https://docs.campaign.adobe.com/doc/AC/en/WEB_Web_forms_About_web_forms.html)

Campaign および Adobe Experience Cloud ソリューション統合ガイドが更新され、再編成されました。[詳細を表示](../../integrations/using/about-campaign-integrations.md)

Web フォームにおけるテキスト変数の使用に関する節が追加されました。[詳細を表示](https://docs.campaign.adobe.com/doc/AC/en/WEB_Web_forms_Static_elements_in_a_web_form.html#Using_text_variables)

メッセージの URL トラッキングモードの説明が詳細になりました。[詳細を表示](https://docs.campaign.adobe.com/doc/AC/en/DLV_Tracking_messages_How_to_configure_tracked_links.html)

インスタンス作成の節が再編成されました。[詳細を表示](https://docs.campaign.adobe.com/doc/AC/en/INS_Initial_configuration_Creating_an_instance_and_logging_on.html)

日本の携帯電話での E メール送信に関して説明する新しい節が追加されました。[詳細を表示](https://docs.campaign.adobe.com/doc/AC/en/DLV_Sending_emails_Defining_the_email_content.html#Sending_emails_on_Japanese_mobiles)

パーソナライゼーションの最適化の節が更新され、詳細情報が追加されました。[詳細を表示](https://docs.campaign.adobe.com/doc/AC/en/DLV_Personalizing_deliveries_Personalization_fields.html#Optimizing_personalization)

## 18.6 - 2018 年 7 月 9 日{#release-18-6}

**リリースに含まれる新機能**

互換性マトリックスが更新されました。[詳細を表示](https://helpx.adobe.com/campaign/kb/compatibility-matrix.html)

JSAPI のドキュメントが更新されました。[詳細を表示](https://support.neolane.net/webApp/extranetLogin)

廃止および削除された機能ページが更新されました。[詳細を表示](https://helpx.adobe.com/campaign/kb/deprecated-and-removed-features.html)

**リリースに伴うその他のドキュメントのアップデート**

Campaign Classic ユーザーガイドは、名前が変更され、ナビゲーションの簡素化、ユーザーエクスペリエンス、情報へのアクセスおよびセルフヘルプの改善がおこなわれました。[詳細を表示](https://docs.campaign.adobe.com/doc/AC/en/browseAC.html)

式エディターで使用できる関数のリストが更新されました。[詳細を表示](https://docs.campaign.adobe.com/doc/AC/en/PTF_Creating_queries_Defining_filter_conditions.html#List_of_functions)

セキュリティ入門ガイドが更新され、PI を含むページを保護する方法に関する情報が追加されました。[詳細を表示](https://docs.campaign.adobe.com/doc/AC/getting_started/EN/security.html)

エラーメッセージのリストが更新されました。[詳細を表示](https://docs.campaign.adobe.com/doc/AC/en/technicalResources/error_messages/error_codes.html)

IMS 統合ドキュメントにトラブルシューティングの節が追加されました。[詳細を表示](https://docs.campaign.adobe.com/doc/AC/en/ITG_Connecting_via_an_Adobe_ID_IMS_troubleshooting.html)

ビルドアップグレード入門ガイドが更新されました。[詳細を表示](https://docs.campaign.adobe.com/doc/AC/getting_started/EN/buildUpgrade.html)

IP アフィニティの設定の節が更新されました。[詳細を表示](https://docs.campaign.adobe.com/doc/AC/en/INS_Additional_configurations_Mid-sourcing_server.html#Multiplexing_the_mid-sourcing_server)

パフォーマンスとスループットのトラブルシューティングの節が追加されました。[詳細を表示](https://docs.campaign.adobe.com/doc/AC/en/PRO_Troubleshooting_Performance_and_throughput_issues.html)

組み込みパーソナライゼーションブロックのリストが更新され、例が追加されました。[詳細を表示](https://docs.campaign.adobe.com/doc/AC/en/DLV_Personalizing_deliveries_Personalization_blocks.html#Out-of-the-box_personalization_blocks)

配信エラーの理由のリストが更新されました。[詳細を表示](https://docs.campaign.adobe.com/doc/AC/en/DLV_Monitoring_deliveries_Understanding_delivery_failures.html#Delivery_failure_types_and_reasons)

パッケージ定義の管理に関する新しい節が追加されました。[詳細を表示](https://docs.campaign.adobe.com/doc/AC/en/PTF_Administration_basics_Working_with_data_packages.html#Managing_package_definitions)

Campaign の Adobe Analytics Data Connector との統合の節が改善され、再編成されました。[詳細を表示](https://docs.campaign.adobe.com/doc/AC/en/PTF_Connectors_Adobe_Analytics_Data_Connector.html)

ステップバイステップガイドとハウツービデオへのリンクがある、新しいチュートリアルの節が追加されました。[詳細を表示](https://docs.campaign.adobe.com/doc/AC/en/PTF_Starting_with_Adobe_Campaign_Tutorials.html)

SMS コネクタのプロトコルと設定に関する新しいテクニカルノートが作成されました。[詳細を表示](https://helpx.adobe.com/campaign/kb/sms-connector-protocol-and-settings.html)

配信のベストプラクティス入門ガイドが更新されました。[詳細を表示](https://docs.campaign.adobe.com/doc/AC/getting_started/EN/deliveryBestPractices.html)

Web API デプロイメントを使用した Microsoft Dynamics 365 アカウントの設定が更新されました。[詳細を表示](https://docs.campaign.adobe.com/doc/AC/en/PTF_Connectors_CRM_Connectors.html#Example_for_Microsoft_Dynamics)

Adobe Campaign Classic を Windows プラットフォームにインストールする手順が更新されました。[詳細を表示](https://docs.campaign.adobe.com/doc/AC/en/INS_Installing_Campaign_in_Windows__Installing_the_server.html)

Adobe Experience Cloud と Campaign Classic 間のオーディエンス共有期間について詳述されました。[詳細を表示](https://docs.campaign.adobe.com/doc/AC/en/ITG_Audience_sharing_Importing_and_exporting_audiences.html)

Campaign Classic のナレッジベース記事のリストが更新されました。[詳細を表示](https://helpx.adobe.com/campaign/kb/article-list.html)

パフォーマンスの向上とベストプラクティスに関する新しいテクニカルノートが公開されました。[詳細を表示](https://helpx.adobe.com/campaign/kb/best-practices-for-performance-improvement.html)

A/B テストのサンプルが更新されました。[詳細を表示](https://docs.campaign.adobe.com/doc/AC/en/WKF_Use_cases_A-B_testing.html)

Campaign Classic のよくある質問／FAQ ページが更新されました。[詳細を表示](../../platform/using/common-questions.md)

## 18.4 - 2018 年 4 月 24 日{#release-18-4}

**リリースに含まれる新機能**

EU 一般データ保護規則（GDPR） - [詳細を表示](https://helpx.adobe.com/campaign/kb/acc-privacy.html)

アクティブなプロファイル - [詳細を表示](https://docs.campaign.adobe.com/doc/AC/en/PTF_Profile_management_About_profiles.html#Active_profiles)

Android プッシュコネクタの機能強化 - [詳細を表示](https://docs.campaign.adobe.com/doc/AC/en/DLV_Sending_push_notifications_Setting_up_mobile_app_channel.html#Android_connectors)

**リリースに伴うその他のドキュメントのアップデート**

リリースノートが改善されてユーザーエクスペリエンスが向上し、お客様のご要望に関連するすべてのパッチが含まれるようになりました。[詳細を表示](https://docs.campaign.adobe.com/doc/AC/en/RN.html)

Campaign Classic に関する最もよくある質問を含む新しいページが追加されました。[詳細を表示](../../platform/using/common-questions.md)

エラーメッセージのリストが更新されました。[詳細を表示](https://docs.campaign.adobe.com/doc/AC/en/technicalResources/error_messages/error_codes.html)

Experience Cloud Triggersーのテクニカルノートが更新されました。[詳細を表示](https://helpx.adobe.com/campaign/kb/triggers-and-campaign.html)

旧バージョンの Campaign Classic にプライバシー（GDPR）パッケージをインストールしてデプロイする方法についてのテクニカルノートが追加されました。[詳細を表示](https://helpx.adobe.com/campaign/kb/how-to-install-gdpr-package-on-legacy-versions.html)

新しいシーケンス自動生成メカニズムに関するテクニカルノートが追加されました。[詳細を表示](https://helpx.adobe.com/campaign/kb/sequence_auto_generation.html)

JSAPI のドキュメントが更新されました。[詳細を表示](https://support.neolane.net/webApp/extranetLogin)

互換性マトリックスが更新されました。[詳細を表示](https://helpx.adobe.com/campaign/kb/compatibility-matrix.html)

廃止された機能とバージョンの一覧を示す新しいページが公開されました。[詳細を表示](https://helpx.adobe.com/campaign/kb/deprecated-and-removed-features.html)

RDBMS に関する既知の制限事項とベストプラクティスが追加されました。[詳細を表示](https://docs.campaign.adobe.com/doc/AC/en/INS_Prerequisites_and_recommendations__Database.html)

SFTP の使用に関するベストプラクティスが説明されています。[詳細を表示](https://docs.campaign.adobe.com/doc/AC/en/PTF_Importing_and_exporting_data_SFTP_server_usage.html)

テクニカルワークフローのリストが更新されました。[詳細を表示](https://docs.campaign.adobe.com/doc/AC/en/WKF_Technical_workflows_About_technical_workflows.html)

ナレッジベース記事（旧称「テクニカルノート」）のリストが、こちらから入手できるようになりました。[詳細を表示](https://helpx.adobe.com/campaign/kb/article-list.html)

[ハウツービデオ](https://docs.campaign.adobe.com/doc/AC/en/Videos/Videos.html)が更新されました。

LINE パッケージの廃止後、LINE ドキュメントが更新されました。[詳細を表示](https://docs.campaign.adobe.com/doc/AC/en/DLV_Sending_messages_on_mobiles_LINE_channel.html)

レポート指標の計算に関するドキュメントが更新されました。[詳細を表示](../../reporting/using/indicator-calculation.md)

Oracle とのタイムゾーンファイルの整合に関する情報が追加されました。[詳細を表示](https://docs.campaign.adobe.com/doc/AC/en/MIG_Configuration_General_configurations.html#Oracle)

配信の監視の節が新たに追加され、配信のエラーと強制隔離の管理に関する情報が更新されました。[詳細を表示](https://docs.campaign.adobe.com/doc/AC/en/DLV_Monitoring_deliveries_Monitoring_a_delivery.html)

パーソナライゼーションブロックの節が再編成され、そのまますぐに使用できるパーソナライゼーションブロックに関する新しい情報が追加されました。
[詳細を表示](https://docs.campaign.adobe.com/doc/AC/en/DLV_Personalizing_deliveries_Personalization_blocks.html)

E メールのアーカイブの節が再編成され、```config-<instance name>.xml``` ファイルの設定に関する新しい情報が追加されました。[詳細を表示](https://docs.campaign.adobe.com/doc/AC/en/INS_Additional_configurations_Email_archiving.html#Activating_email_archiving__on_premise_)

Message Center（コントロール）のテクニカルワークフローに関する情報が更新されました。[詳細を表示](https://docs.campaign.adobe.com/doc/AC/en/WKF_Technical_workflows_Message_Center__Control_.html)

SMTP リレーを設定する際のスループット制限に関する情報が追加されました。[詳細を表示](https://docs.campaign.adobe.com/doc/AC/en/INS_Additional_configurations_Configuring_Campaign_server.html#Personalizing_delivery_parameters)

## 17.12 - 2017 年 12 月 14 日{#release-doc-14-12-2017}

[Adobe Campaign Classic ドキュメントセット](https://helpx.adobe.com/support/campaign/classic.html)は、より使いやすくするために再編成されました。

Campaign の主要機能のヘルプ、操作方法、サンプルおよびビデオにアクセスしやすいよう、新しいチュートリアルの節が追加されました。[詳細を表示](https://docs.campaign.adobe.com/doc/AC/en/PTF_Starting_with_Adobe_Campaign_Tutorials.html)

配信ステータスだけでなくエラーを監視するのに役立ち、エラーを解決する方法を説明する新しい節が追加されました。[詳細を表示](https://docs.campaign.adobe.com/doc/AC/en/DLV_Monitoring_deliveries_Monitoring_a_delivery.html)

エラーメッセージのリストが更新されました。[詳細を表示](https://docs.campaign.adobe.com/doc/AC/en/technicalResources/error_messages/error_codes.html)

Experience Cloud Triggersーのテクニカルノートが更新されました。[詳細を表示](https://helpx.adobe.com/campaign/kb/triggers-and-campaign.html)

Campaign Classic 移行ガイドがコレクションに追加されました。[詳細を表示](https://docs.campaign.adobe.com/doc/AC/en/MIG_Migration_overview_About_migration.html)

Campaign の互換性マトリックスが更新されました。[詳細を表示](https://helpx.adobe.com/campaign/kb/compatibility-matrix.html)

該当する場合、設定手順およびインストール手順で、適用されるホスティングモデルが示されるようになりました。[詳細を表示](https://docs.campaign.adobe.com/doc/AC/en/INS_Additional_configurations_Configuring_Campaign_server.html)

オンプレミス、ハイブリッド、および Managed Services のデプロイメントの設定と機能の違いを説明する新しいナレッジベース記事が追加されました。[詳細を表示](https://helpx.adobe.com/campaign/kb/acc-on-prem-vs-hosted.html)

標準パッケージのインストール方法が追加されました。[詳細を表示](https://docs.campaign.adobe.com/doc/AC/en/INS_Initial_configuration_Installing_packages.html)

Audience Manager または People コアサービスとの統合を設定する方法について詳細が追加されました。[詳細を表示](https://docs.campaign.adobe.com/doc/AC/en/ITG_Audience_sharing_Configuring_shared_audiences_integration_in_Adobe_Campaign.html)

PostreSQL を使用する場合、Campaign のインストールに pgcrypto が必要になったことについての記載が、インストールドキュメントに追加されました。[詳細を表示](https://docs.campaign.adobe.com/doc/AC/en/INS_Installing_Campaign_in_Linux__Prerequisites.html#Database_access_layers)

## 17.9 - 2017 年 9 月 25 日{#release-17-9}

**リリースに含まれる新機能**

ACS コネクタの機能強化

SAP HANA コネクタ - [詳細を表示](https://docs.campaign.adobe.com/doc/AC/en/PTF_Connectors_Accessing_an_external_database.html#SAP_HANA)

HiveSQL による Hadoop コネクタ - [詳細を表示](https://docs.campaign.adobe.com/doc/AC/en/PTF_Connectors_Accessing_an_external_database.html#Hadoop)

LINE チャネル：メッセージングの機能強化 - [詳細を表示](https://docs.campaign.adobe.com/doc/AC/en/DLV_Sending_messages_on_mobiles_LINE_channel.html)

**リリースに伴うその他のドキュメントのアップデート**

新しいクエリサンプルが追加されました。[詳細を表示](https://docs.campaign.adobe.com/doc/AC/en/WKF_Use_cases_Designing_queries.html#Filtering_duplicated_recipients)

配信のベストプラクティスガイドが更新されました。[詳細を表示](https://docs.campaign.adobe.com/doc/AC/getting_started/EN/deliveryBestPractices.html)

A/B テストのサンプルが更新され、不足していた手順が追加されました。[詳細を表示](https://docs.campaign.adobe.com/doc/AC/en/WKF_Use_cases_A-B_testing.html)

ハウツービデオが更新されました。[詳細を表示](https://docs.campaign.adobe.com/doc/AC/en/Videos/Videos.html)

E メールのアーカイブの節が更新されました。[詳細を表示](https://docs.campaign.adobe.com/doc/AC/en/INS_Additional_configurations_Email_archiving.html)

ワークフローのスケジューラーの使用方法が明確になりました。[詳細を表示](../../workflow/using/scheduler.md)

一時停止されたワークフローのベストプラクティスが追加されました。[詳細を表示](https://docs.campaign.adobe.com/doc/AC/en/WKF__General_operation_Executing_a_workflow.html)

ワークフローでデータをインポートする際のファイルの前処理およびワークフローでデータをエクスポートする際のファイルの後処理に関する手順が新しくなりました。[こちら](https://docs.campaign.adobe.com/doc/AC/en/WKF__General_operation_Importing_data.html)を参照してください。

SMS メッセージドキュメントの強制隔離メカニズムが更新され、拡張された汎用 SMPP コネクタにおけるエラー管理の特性が反映されました。[詳細を表示](https://docs.campaign.adobe.com/doc/AC/en/DLV_Monitoring_deliveries_Understanding_quarantine_management.html#SMS_quarantines)

モバイルアプリチャネルのドキュメントが強化され、Android でリッチ通知を送信する詳細な手順が追加されました。[詳細を表示](https://docs.campaign.adobe.com/doc/AC/en/DLV_Sending_push_notifications_Setting_up_mobile_app_channel.html#Rich_notifications)

受信ボックスレンダリングのドキュメントが更新されました。[詳細を表示](https://docs.campaign.adobe.com/doc/AC/en/DLV_Deliverability_management_Inbox_rendering.html)

Web トラッキングの設定に関するドキュメントが強化され、例および注意事項が更新されました。[詳細を表示](https://docs.campaign.adobe.com/doc/AC/en/CFG_Setting_up_web_tracking_Additional_parameters.html#Redirection_server_configuration)

SMS チャネルのドキュメントが更新され、拡張された汎用 SMPP コネクタに適用される自動返信の節の情報が明確化されました。[詳細を表示](https://docs.campaign.adobe.com/doc/AC/en/DLV_Sending_messages_on_mobiles_SMS_channel.html#Creating_an_SMPP_external_account)

ソーシャルマーケティングのドキュメントが更新されました。[詳細を表示](../../social/using/about-social-marketing.md)

IP ウォーミングに関する新しいテクニカルノートが追加されました。[詳細を表示](https://docs.campaign.adobe.com/doc/AC/en/technicalResources/Technotes/AdobeCampaign_Deliverability_IP_Warming_overview.pdf)

ビルドアップグレードに関する新しい入門ガイドが追加されました。[詳細を表示](https://docs.campaign.adobe.com/doc/AC/getting_started/EN/buildUpgrade.html)

## 2017 年 5 月{#release-doc-30-05-2017}

はじめにガイドが新しく公開されました。配信の作成とターゲティングから送信や監視に至るまで、Adobe Campaign での配信に関するベストプラクティスを説明します。[詳細を表示](https://docs.campaign.adobe.com/doc/AC/getting_started/EN/deliveryBestPractices.html)

セキュリティに関するはじめにガイドが更新されました。[詳細を表示](https://docs.campaign.adobe.com/doc/AC/getting_started/EN/security.html)

[「E メールのアーカイブ」ドキュメント](https://docs.campaign.adobe.com/doc/AC/en/INS_Additional_configurations_Email_archiving.html)が更新され、[BCC による E メール](https://docs.campaign.adobe.com/doc/AC/en/INS_Additional_configurations_Email_archiving.html#Configuring_the_BCC_email_address__on_premise_)の節と[この機能を有効化する詳細な手順](https://docs.campaign.adobe.com/doc/AC/en/DLV_Sending_emails_Sending_messages.html#Archiving_emails)が追加されました。

いくつかのビデオが追加、更新されました。[詳細を表示](https://docs.campaign.adobe.com/doc/AC/en/Videos/Videos.html)

データベースを更新せずに、外部ファイルから読み込まれた受信者に配信を送信する方法について説明します。[詳細を表示](../../delivery/using/steps-defining-the-target-population.md#selecting-external-recipients)

二重のオプトインの例が更新されました。[詳細を表示](../../web/using/use-cases--web-forms.md)

## 2017 年 3 月{#release-doc-31-03-2017}

配信品質：[はじめにガイド](https://docs.campaign.adobe.com/doc/AC/getting_started/EN/deliverability.html)が更新されました。配信品質ドキュメントに、より詳細な[概要](https://docs.campaign.adobe.com/doc/AC/en/DLV_Deliverability_management_About_deliverability.html)と[実装プロセスおよび主な手順](../../delivery/using/deliverability-key-points.md)の説明が含まれるようになりました。

「ウェーブを使用した送信」の節が移動され、詳細な例、推奨および使用例が追加されてより充実した内容となりました。[詳細を表示](https://docs.campaign.adobe.com/doc/AC/en/DLV_Sending_emails_Sending_messages.html#Sending_using_multiple_waves)

「強制隔離の管理」の節に SMS メッセージに特有のエラーを説明する表が追加されました。[詳細を表示](https://docs.campaign.adobe.com/doc/AC/en/DLV_Monitoring_deliveries_Understanding_quarantine_management.html#SMS_quarantines)

ワークフロー：新しいマルチチャネルワークフローの例が追加されました。[詳細を表示](https://docs.campaign.adobe.com/doc/AC/en/WKF_Repository_of_activities_Action_activities.html#Cross-channel_deliveries)

Experience Cloud Triggersー：Adobe Campaign を使用した設定方法および使用方法に関するテクニカルノートが追加されました。[詳細を表示](https://helpx.adobe.com/campaign/kb/triggers-and-campaign.html)

ワークフローガイドが再構成され、拡張されました。ワークフローの[作成](https://docs.campaign.adobe.com/doc/AC/en/WKF__General_operation_Building_a_workflow.html)および[実行](https://docs.campaign.adobe.com/doc/AC/en/WKF__General_operation_Executing_a_workflow.html)方法、データの[ターゲティング](https://docs.campaign.adobe.com/doc/AC/en/WKF__General_operation_Targeting_data.html)および[管理](https://docs.campaign.adobe.com/doc/AC/en/WKF__General_operation_Targeting_data.html#Data_Management)方法、データの[インポート](https://docs.campaign.adobe.com/doc/AC/en/WKF__General_operation_Importing_data.html)方法、および[データベースを更新](https://docs.campaign.adobe.com/doc/AC/en/WKF__General_operation_How_to_use_workflow_data.html#Updating_the_database)または[配信を送信](https://docs.campaign.adobe.com/doc/AC/en/WKF__General_operation_How_to_use_workflow_data.html#Delivering_via_a_workflow)するためのワークフローデータの使用方法が簡単に見つかります。

[インポートのベストプラクティス](https://docs.campaign.adobe.com/doc/AC/en/WKF__General_operation_Importing_data.html#Import_best_practices)に続いて[インポートワークフロー](https://docs.campaign.adobe.com/doc/AC/en/WKF__General_operation_How_to_use_workflow_data.html#Delivering_via_a_workflow)の例が提供されました。この新しいバージョン向けにインストールガイドが更新されました。[詳細を表示](https://docs.campaign.adobe.com/doc/AC/en/INS_Architecture_and_hosting_models_General_architecture.html)

互換性マトリックスが更新されました。[詳細を表示](https://helpx.adobe.com/campaign/kb/compatibility-matrix.html)

E メール配信にクーポンを含めると、受信者にとって付加価値となります。[詳細を表示](https://docs.campaign.adobe.com/doc/AC/en/DLV_Personalizing_deliveries_Personalized_coupons.html)

## Adobe Campaign v7 - 2017 年 3 月 16 日{#release-17-2}

**リリースに含まれる新機能**

ACS コネクタ

Microsoft Dynamics 用 Web API - [詳細を表示](https://docs.campaign.adobe.com/doc/AC/en/PTF_Connectors_CRM_Connectors.html#Example_for_Microsoft_Dynamics)

BCC メソッドによる E メールのアーカイブ - [詳細を表示](https://docs.campaign.adobe.com/doc/AC/en/INS_Additional_configurations_Email_archiving.html#Updated_email_archiving_system__BCC_)

Amazon Simple Storage Service（S3）コネクタ - [詳細を表示](https://docs.campaign.adobe.com/doc/AC/en/WKF_Repository_of_activities_Event_activities.html#File_transfer)

