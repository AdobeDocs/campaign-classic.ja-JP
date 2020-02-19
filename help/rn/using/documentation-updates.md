---
title: Adobe Campaign Classicドキュメントの更新
description: このページには、Adobe Campaign Classicの各リリースに関するすべての新機能とドキュメントの更新の一覧が記載されています。
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
source-git-commit: cc6f0f2989977c5a199dbfd413c6a2bac4628545

---


# ドキュメントの更新{#documentation-updates}

Adobe Campaign Classicドキュメントの最新のすべての更新について説明します。

このページには、Adobe Campaign Classicの各リリースに関するすべての新機能とドキュメントの更新の一覧が記載されています。

また、 [Adobe Campaign Classicリリースノート](../../rn/using/latest-release.md)を参照することもできます。

## 20.1 - 17/02/2020{#release-20-1}

**リリースに含まれる新機能**

雪片FDAコネクタ — [詳細情報](../../platform/using/specific-configuration-database.md#configure-access-to-snowflake)

Hadoop FDAコネクタの強化 — [詳細情報](../../platform/using/specific-configuration-database.md#configure-access-to-hadoop-3)

**リリースに伴うその他のドキュメントの更新**

[インストール](../../installation/using/before-reading.md)、 [実稼働](../../production/using/foreword.md) 、[構成](../../configuration/using/additional-parameters.md)ガイドは、 nlserverサービスの起動で使用する新しいsystemdユニットで更新されました。 /etc/init.d/nlserver6は引き続き使用できますが、nlserverサービスとの対話にはsystemctlコマンドを使用することをお勧めします。

インストールガイドが更新され、互換表の最新バージョンと同期されました。 新しいサポート対象システムが追加されました。 非推奨およびサポートされていないシステムへのオカレンスは削除されました。 [詳細を表示](../../installation/using/before-reading.md)

互換性マトリックスが更新され、Hadoop 3.0およびSnowflake FDAコネクタが追加されました。 [詳細を表示](https://helpx.adobe.com/campaign/kb/compatibility-matrix.html)

IP親和性のベストプラクティスがインストールガイドに追加されました。 [詳細を表示](../../installation/using/email-deliverability.md#list-of-ip-addresses-to-use)

データベースクリーンアップワークフローセクションが更新されました。 指定されたバッチ数値は、コード実装を反映しています。 [詳細を表示](../../production/using/database-cleanup-workflow.md)

HTTPを使用したFDAに関する制限が、トランザクションメッセージングガイドに追加されました。 [詳細を表示](../../production/using/database-cleanup-workflow.md)

新しいオプションに情報が追加され、およびワークフローアクティビティのタイムアウト期間を定義で **[!UICONTROL JavaScript code]** きるよう **[!UICONTROL Advanced JavaScript code]** になりました。 [詳細を表示](../../workflow/using/sql-code-and-javascript-code.md)

ノードにある新しいビュ **[!UICONTROL Start Pending]** ーに情報が追加さ **[!UICONTROL Administration]** れま **[!UICONTROL Audit]** した **[!UICONTROL Workflows Status]** 。 [詳細を表示](../../workflow/using/monitoring-workflow-execution.md#filtering-workflows-status)

プッシュ [通知の送信ガイドは](../../delivery/using/about-mobile-app-channel.md) 、移動され、整理および改善され、明確な情報が提供されました。

URLレポート設定の新しいパラメーターは、[こちら](../../reporting/using/properties-of-the-report.md#defining-additional-settings)で説明されています。

**Campaign Classic On-premise &amp; Hosted機能マトリックス**ページが新しいFDAコネクターで更新されました。 [詳細を表示](https://helpx.adobe.com/campaign/kb/acc-on-prem-vs-hosted.html)

**Campaign Classic機能マ トリックス**ページが更新されました。 [詳細を表示](https://helpx.adobe.com/campaign/kb/compatibility-matrix.html)

新しいワークフ **[!UICONTROL Cleanup of Nmsaddress]** ローは[ここ](../../production/using/database-cleanup-workflow.md#cleanup-of-nmsaddress)に記載されています。

ワークフローでクエリアクティビティを使用する場合に、制限が追加されました。 [詳細を表示](../../workflow/using/query.md).

ソフトエラーの場合に検疫にアドレスを送信するための、拡張された電子メールアドレス検証ルールの詳細を説明する新しいセクションが追加されました。 [詳細を表示](../../delivery/using/understanding-quarantine-management.md#soft-error-management)

設定ファイルのパラメーターは、インスタンスが拡張MTAを使用しているかどうかを示しています。 [詳細を表示](../../installation/using/the-server-configuration-file.md#mta)

## February 2020 {#february-2020}

3つの電子メールプロバイダー(Gmail、Outlook、Mail.ru)によって電子メール用のAMPがサポートされるようになりました。AMPを使用してインタラクティブコンテンツを定義する方法を説明する節が更新されました。 [詳細を表示](../../delivery/using/defining-interactive-content.md)

「電子メールのアーカイブ」セクションが明確になりました。 [詳細を表示](../../installation/using/email-archiving.md#recommendations-and-limitations)

## 2020 年 1 月{#january-2020}

「配信品質」セクションは、移動、再構成、および更新されたコンテンツによる拡張が行われました。 [詳細を表示](../../delivery/using/about-deliverability.md)

Adobe Campaign Classicデータモデルの基本と各表の説明にアクセスする方法について説明する新しい節が利用できるようになりました。 [詳細を表示](../../configuration/using/about-data-model.md)

「Adobe Campaign拡張MTA」の記事が更新され、すべてのメッセージに拡張MTAヘッダーを追加しないインスタンスに特定のタイポロジパッケージをインストールする方法に関する詳細が追加されました。 [詳細を表示](https://helpx.adobe.com/campaign/kb/campaign-enhanced-mta.html#impacts)

クエリデザインに関連する使用事例は、別々のセクションに再編成されました。 [詳細を表示](../../workflow/using/querying-recipient-table.md)

Adobe Campaign Classicのオファーの管理とインタラクションモジュールの使用に関するヒントとテクニックに関する新しい節が利用できるようになりました。 [詳細を表示](../../interaction/using/interaction-best-practices.md#tips-managing-offers)

インタラクションドキュメントは、オファーの管理方法をより良く理解するのに役立つ複数のビデオへのリンクで強化されました。 [詳細を表示](../../interaction/using/interaction-and-offer-management.md)

インスタンスで実行するクエリーを最適化する方法に関するベストプラクティスの記事がドキュメントに統合されました。 [詳細を表示](../../workflow/using/query.md#optimizing-queries)

レポートガイドが更新され、再構成されました。 [詳細を表示](../../reporting/using/about-adobe-campaign-reporting-tools.md)

ワークフローでのインスタンス変数の使用方法の例が追加されました。 [詳細を表示](../../workflow/using/javascript-scripts-and-templates.md)

## December 2019 {#december-2019}

「WdbcOptions_TempDbName」オプションがキャンペーンオプションのリストに追加されました。 [詳細を表示](../../installation/using/configuring-campaign-options.md)

FDAのマトリックスページは[ここ](/help/rn/using/assets/fda_rdbms_rights.pdf)に移動されました。

Access Rights Matrixページは[ここ](https://docs.adobe.com/content/help/en/campaign-classic/using/getting-started/administration-basics/assets/accessrights.pdf)に移動されました。

AMPを使用してインタラクティブコンテンツを定義する方法を説明する節が移動されました。 [詳細を表示](../../delivery/using/defining-interactive-content.md)

## 19.2 - 02/12/2019{#release-19-2}

**リリースに含まれる新機能**

カリフォルニア消費者プライバシー法(CCPA) — [詳細情報](https://helpx.adobe.com/campaign/kb/acc-privacy.html)

AMPを使用したインタラクティブコンテンツ — [詳細情報](../../delivery/using/defining-interactive-content.md)

ワークフローライブ監視 — [詳細情報](../../workflow/using/monitoring-workflow-execution.md#filtering-workflows-status)

セキュアSMSメッセージング(TLS) — [詳細情報](https://helpx.adobe.com/campaign/kb/sms-connector-protocol-and-settings.html)

**リリースに伴うその他のドキュメントの更新**

Adobe Campaign Enhanced MTAのドキュメントが利用できるようになりました。 [詳細を表示](https://helpx.adobe.com/campaign/kb/campaign-enhanced-mta.html)

キャンペーン内の「できるだけ早く開始」状態を維持するワークフローのトラブルシューティング方法に関する新しい節が追加されました。 [詳細を表示](../../production/using/workflow-execution.md#start-as-soon-as-possible-in-campaigns)

新しい「NmsOperation_DeliveryPreparationWindow」オプションと「WdbcKillSessionPolicy」オプションがキャンペーンオプションのリストに追加されました。 [詳細を表示](../../installation/using/configuring-campaign-options.md)

Adobe Campaign Classicデータモデルの基本を説明する新しいドキュメントが提供されました。 [詳細を表示](https://helpx.adobe.com/campaign/kb/acc-datamodel.html)

配信プロパティの **新しい最大パーソナライゼーション** 実行時間オプションについては、この[節](../../delivery/using/personalization-fields.md#timing-out-personalization)で説明します。

logon()およびquery()を使用した **HttpServletRequest** を使用したAPI呼び出しの例が更新されました。 [詳細を表示](../../configuration/using/web-service-calls.md).

スキーマ定義の **sqlDefault** 属性に対する推奨が追加されました。 [詳細を表示](../../configuration/using/elements-and-attributes.md#attribute-description).

Adobe CampaignとAdobe Real-time Customer Data Platformの統合については、Adobe Experience cloudとの統合ガイドを参 **照してください** 。 [詳細を表示](../../integrations/using/about-campaign-integrations.md).

## November 2019 {#november-2019}

[ミッドソーシングサーバーの多重化](../../installation/using/mid-sourcing-server.md#multiplexing-the-mid-sourcing-server)と[複数の制御インスタンスのサポート](../../message-center/using/transactional-messaging-architecture.md#supporting-several-control-instances)に、完全にホストされたクライアントおよびハイブリッドクライアントに対しては、これらのデプロイメントがサポートされていないことを示す警告が追加されました。

電子メールの送信時に使用する文字エンコーディングを強制する方法を説明する新しい節が追加されました。 [詳細を表示](../../delivery/using/sending-messages.md#character-encoding)

「アクセス管理」セクションが更新され、**「プライバシーデ ータ」権限**が追加されまし&#x200B;た。 [詳細を表示](../../platform/using/access-management.md#named-rights)

パーソナライゼーションフィールドのコンテンツは1024文字を超えないようにする情報が追加されました。 [詳細を表示](../../delivery/using/personalization-fields.md)

コントロールパネルのドキュメントは、新しいコラボレーションドキュメントセットに統合されました。 [詳細を表示](https://docs.adobe.com/content/help/en/control-panel/using/control-panel-home.html)

『配信のベストプラクティス集』ガイドが更新されました。 [詳細を表示](https://helpx.adobe.com/campaign/kb/delivery-best-practices.html)

## October 2019 {#october-2019}

Campaign StandardおよびCampaign Classicのエラーメッセージのリストが更新されました。 [詳細を表示](https://docs.campaign.adobe.com/doc/AC/en/technicalResources/error_messages/error_codes.html)

GDPR入門ガイドが改善され、強化されました。 GDPRやCCPAなどのプライバシー管理に関するドキュメントが提供されます。 [詳細を表示](https://helpx.adobe.com/content/help/en/campaign/kb/campaign-privacy.html)

Campaign Classicでの追跡用に、新しいトラブルシューティングページが追加されました。 [詳細を表示](https://helpx.adobe.com/campaign/kb/classic-tracking-troubleshooting.html).

Adobe Analytics Data Connectorの新しいベストプラクティスのページが追加されました。 [Adobe Analytics Data Connectorの詳細を読む](../../platform/using/adobe-analytics-data-connector.md)

『配信のベストプラクティス集』ガイドは移動および更新されました。 [詳細を表示](https://helpx.adobe.com/campaign/kb/delivery-best-practices.html)

同じプロバイダアカウントで拡張汎用SMPPコネクタを利用する複数の外部アカウントを使用する場合の問題を回避するため、SMSチャネルのドキュメントに推奨事項が追加されました。 [詳細を表示](../../delivery/using/sms-channel.md#automatic-reply)

ワークフローの同時実行を防ぐ方法に関する情報がスケジューラーアクティビティのドキュメントに追加されました。 [詳細を表示](../../workflow/using/scheduler.md)

オンプレミスインストールのインボックスレンダリングを設定する手順がドキュメントに追加されました。 [詳細を表示](../../delivery/using/inbox-rendering.md#activating-inbox-rendering)

## 2019 年 9 月 {#september-2019}

Campaign Classicの管理に関する一般的なガイドラインを提供する新しいページが追加されました。 [詳細を表示](https://helpx.adobe.com/campaign/kb/acc-maintenance.html)

ワークフロー監視に関する情報は、新しい専用セクションに一元化されました。 [詳細を表示](../../workflow/using/monitoring-workflow-execution.md).

Adobe Campaign Classicの追跡に関する一般的なガイドラインに関する新しいページが追加されました。 [詳細を表示](https://helpx.adobe.com/campaign/kb/acc-tracking.html).

ワークフローと配信のパフォーマンス改善のベストプラクティスが更新されました。 [ワークフローの詳細](../../workflow/using/workflow-best-practices.md)と[配信に関する詳細を参照](../../delivery/using/monitoring-a-delivery.md#best-practices-performance)。

## 19.1 - 30/05/2019{#release-19-1}

**リリースに含まれる新機能**

コントロールパネル — [詳細情報](https://docs.adobe.com/content/help/en/control-panel/using/control-panel-home.html)

監査証跡 — [詳細情報](https://docs.campaign.adobe.com/doc/AC/en/PRO_Production_procedures_Audit_trail.html)

**リリースに伴うその他のドキュメントの更新**

新しいビルドアップグレードFAQが作成されました。 [詳細を表示](https://helpx.adobe.com/campaign/kb/build-upgrade-faq.html)

The [Compatibility matrix](https://helpx.adobe.com/campaign/kb/compatibility-matrix.html) has been updated. サポートされるデータベースシステムのリスト、Android/iOSのバージョン、および関連するSDKが更新されました。 The [19.0 Compatibility matrix](https://helpx.adobe.com/campaign/kb/compatibility-matrix-19-0.html) has been archived.

「Campaign Classicの非推奨および削除された機能」ページが更新されました。 [詳細を表示](https://helpx.adobe.com/campaign/kb/deprecated-and-removed-features.html)

サーバー設定ファイルの説明が『インストールガイド』に追加されました。 [詳細を表示](https://docs.campaign.adobe.com/doc/AC/en/INS_Appendices_The_server_configuration_file.html)

ホストモデルとハイブリッドモデルのインストール手順と設定手順を説明する節が追加されました。 [詳細を表示](https://docs.campaign.adobe.com/doc/AC/en/INS_Hybrid_and_Hosted_models_Introduction.html)

Campaignサーバーのアンインストール手順を説明する節が追加されました。 [詳細を表示](https://docs.campaign.adobe.com/doc/AC/en/INS_Appendices_Uninstalling_Campaign.html)

[セキュリティ](https://docs.campaign.adobe.com/doc/AC/getting_started/EN/security.html)、[配信品質](https://docs.campaign.adobe.com/doc/AC/getting_started/EN/deliverability.html) 、[プライバシ](https://helpx.adobe.com/campaign/kb/acc-privacy.html) ー入門ガイドが更新されました。

製品の変更を反映して、前処理ワークフローオプションの説明が更新されました。 [詳細を表示](https://docs.campaign.adobe.com/doc/AC/en/WKF_Repository_of_activities_Action_activities.html#Data_loading__file_)

Marketing Cloud Triggersテクノートが更新されました。 [詳細を表示](https://helpx.adobe.com/campaign/kb/triggers-and-campaign.html)

エラーメッセージのリストが更新されました。 [詳細を表示](https://docs.campaign.adobe.com/doc/AC/en/technicalResources/error_messages/error_codes.html)

トランザクションメッセージングのSOAP認証方法に関する詳細を追加しました。 [詳細を表示](https://docs.campaign.adobe.com/doc/AC/en/MCE_Introduction_Event_description.html)

Apacheの設定手順が更新されました。 [詳細を表示](https://docs.campaign.adobe.com/doc/AC/en/INS_Installing_Campaign_in_Linux__Integration_into_a_Web_server.html#Configuring_Apache_web_server_in_RHEL)

Campaign StandardおよびClassicのエンドポイントのリストを含む新しいページが追加されました。 [詳細を表示](https://helpx.adobe.com/campaign/kb/campaign-endpoints.html)

データパッケージのベストプラクティスに関する記事が更新されました。 [詳細を表示](https://helpx.adobe.com/campaign/kb/data-package-best-practices.html)

オファーの管理に関するドキュメントが更新され、ベストプラクティスを一覧表示する新しいセクションが追加されました。 [詳細を表示](https://docs.campaign.adobe.com/doc/AC/en/ITA_Interaction_Overview_Interaction_best_practices.html)

Adobe Campaign Classicのオファーカタログの使用に関する新しいナレッジベース記事が作成されました。 [詳細を表示](https://helpx.adobe.com/campaign/kb/offer-best-practices.html)

「サブワークフロー」アクティビティセクションが、使用例で強化されました。 [詳細を表示](../../workflow/using/sub-workflow.md)

[Campaign Classic On-premise &amp; Hosted機能マトリックス](https://helpx.adobe.com/campaign/kb/acc-on-prem-vs-hosted.html)のナレッジベース記事が更新され、電子メールのアーカイブに関する情報が追加されました。

トランザクションメッセージのドキュメントが更新され、テンプレートの発行に関する注意事項が追加されました。 [詳細を表示](https://docs.campaign.adobe.com/doc/AC/en/MCE_Template_publication.html)

「未処理のバウンスメール」セクションが更新され、「エラーの転送先アドレス」フィールドと「エラーのアドレス」フィールドの詳細が追加されました。 [詳細を表示](https://docs.campaign.adobe.com/doc/AC/en/INS_Initial_configuration_Deploying_an_instance.html#Unprocessed_bounce_mails)

ワークフロー計画のベストプラクティスに関する新しい節が追加されました。 [詳細を表示](https://docs.campaign.adobe.com/doc/AC/en/WKF__General_operation_Workflow_best_practices.html#Execution_and_performance)

キャンペーンオプションのリストに、次の2つの新しいオプションが追加されました。XtkSecurity_Restrict_EditXMLとNmsOperation_OperationMgtDebug。
[詳細を表示](https://docs.campaign.adobe.com/doc/AC/en/INS_Appendices_Configuring_Campaign_options.html)

Campaign Classicで使用できる様々な外部アカウントと、その設定方法に関する情報を追加しました。
[詳細を表示](https://docs.campaign.adobe.com/doc/AC/en/PTF_Administration_basics_External_accounts.html)

インターフェイスの変更を反映するために、「Analytics Data Connector」セクションを更新しました。
[詳細を表示](https://docs.campaign.adobe.com/doc/AC/en/PTF_Connectors_Adobe_Analytics_Data_Connector.html)

請求レポートに関する情報を追加しました。
[詳細を表示](https://docs.campaign.adobe.com/doc/AC/en/PRO_Production_procedures_Monitoring_processes.html#Billing_report)

共有オーディエンス統合に関するドキュメントを更新しました。
[詳細を表示](https://docs.campaign.adobe.com/doc/AC/en/ITG_Audience_sharing_Configuring_shared_audiences_integration_in_Adobe_Campaign.html)

次のテクノロジが更新されました。 [SMSコネクタのプロトコルと設定](https://helpx.adobe.com/campaign/kb/sms-connector-protocol-and-settings.html) 、[シーケンスの自動生成](https://helpx.adobe.com/campaign/kb/sequence_auto_generation.html#Switchtoadedicatedsequence)。

「技術ワークフロー」セクションが更新されました。 [詳細を表示](https://docs.campaign.adobe.com/doc/AC/en/WKF_Technical_workflows_About_technical_workflows.html)

キャンペーンドメイン名の設定手順が改善され、更新されました。 [詳細を表示](https://helpx.adobe.com/campaign/kb/domain-name-delegation.html)

Google Cloud Messaging(GCM)からFirebase Cloud Messaging(FCM)へのAndroidアプリの移行手順が更新されました。 [詳細を表示](https://helpx.adobe.com/campaign/kb/migrate-to-fcm.html)

『キャンペーンハードウェアサイズガイド』が更新されました。 [詳細を表示](https://helpx.adobe.com/campaign/kb/hardware-sizing-guide.html)

Teradata外部アカウントのクエリバンディングに関する情報が追加されました。 [詳細を表示](https://docs.campaign.adobe.com/doc/AC/en/PTF_Administration_basics_External_accounts.html#External_database_external_account)

## 2019 年 1 月{#release-doc-16-01-2019}

Marketing Cloud Triggersテクノートが更新されました。 [詳細を表示](https://helpx.adobe.com/campaign/kb/triggers-and-campaign.html)

「コンテンツの承認」メンションが、すべてのオファーが有効/承認済みかどうかに関わらず、コンテンツの承認プロセスが達成されたことを示すことを示すメモを「オファーの承認」セクションに追加しました。 [詳細を表示](https://docs.campaign.adobe.com/doc/AC/en/ITA_Managing_an_offer_catalog_Approving_and_activating_an_offer.html#Approving_offer_content)

新しい節が『インストールガイド』に追加され、管理/プラットフォーム/オプションノードのオプションが一覧表示されました。 [詳細を表示](https://docs.campaign.adobe.com/doc/AC/en/INS_Appendices_Configuring_Campaign_options.html)

メーリングリストを保護するためのシードアドレスの使用に関する情報が追加されました。 [詳細を表示](https://docs.campaign.adobe.com/doc/AC/en/DLV_Using_seed_addresses_About_seed_addresses.html)

配信を作成して送信する際の主要な手順は、必要に応じて様々なチャネルを参照しながら、新しいセクションに再グループ化されました。 [詳細を表示](../../delivery/using/steps-about-delivery-creation-steps.md)

「[電子メールのアーカイブ](https://docs.campaign.adobe.com/doc/AC/en/INS_Additional_configurations_Email_archiving.html)」セクションが移動され、整理、改善され、情報が明確になりました。

* 接続ごとの電子メールおよびBCC送信IPパラメータに関するベストプラクティスが追加されました。 [詳細を表示](https://docs.campaign.adobe.com/doc/AC/en/INS_Additional_configurations_Email_archiving.html#Best_practices)

* 古いビルド（Adobe Campaign 17.2 - Build 8795より前）で電子メールアーカイブを既に使用している場合は、新しい電子メールアーカイブシステム(BCC)にアップグレードする手順を更新しました。 [詳細を表示](https://docs.campaign.adobe.com/doc/AC/en/INS_Additional_configurations_Email_archiving.html#Updated_email_archiving_system__BCC_)

「ワークフローによる自動化」ガイドに使用例が追加されました。オペレーターへのパーソナライズされたアラートの送信。 [詳細を表示](https://docs.campaign.adobe.com/doc/AC/en/WKF_Use_cases_Sending_personalized_alerts_to_operators.html)

「新しいバージョンへの移行」セクションが更新されました。 Adobe Campaign v6.11に移行できなくなったので、このドキュメントでは、Adobe Campaign Classic v7への移行手順のみを詳しく説明しています。詳 [細情報](https://docs.campaign.adobe.com/doc/AC/en/MIG_Migration_overview_About_migration.html)

「配信の一時的な失敗後に再試行する」の節が明確になりました。 [詳細を表示](https://docs.campaign.adobe.com/doc/AC/en/DLV_Monitoring_deliveries_Understanding_delivery_failures.html#Retries_after_a_delivery_temporary_failure)

「電子メールコンテンツの定義」セクションに「デジタルコンテンツエディター」セクションへのリンクが追加されました。 [詳細を表示](https://docs.campaign.adobe.com/doc/AC/en/DLV_Sending_emails_Defining_the_email_content.html#Message_content)

「トランザクションメッセージングアーキテクチャ」セクションが更新され、コントロールインスタンスと実行インスタンスを同じマシンにインストールできないことを示す警告が表示されました。 [詳細を表示](https://docs.campaign.adobe.com/doc/AC/en/MCE_Introduction_Transactional_messaging_architecture.html)

「ワークフローの監視」セクションは、8700 ～ 8977(18.10)のビルドに関するメモに更新されました。これらのビルドのWorkflow HeatMapパッケージのインストール方法に関するテクノテートへのリンクも含まれます。 [詳細を表示](https://docs.campaign.adobe.com/doc/AC/en/PRO_Production_procedures_Monitoring_processes.html#About_the_Workflow_HeatMap)

ワークフローの「エンリッチメント」アクティビティを使用して、カスタムデータフィールドを含む電子メールを送信する方法に関する使用例を追加しました。 [詳細を表示](https://docs.campaign.adobe.com/doc/AC/en/WKF_Use_cases_Email_enrichment_with_custom_date_fields.html)

特集ビデオは[ここ](https://docs.adobe.com/content/help/en/campaign-learn/campaign-classic-tutorials/overview.html)に移動されました。

[Teradata](https://helpx.adobe.com/campaign/kb/campaign_fda_teradata.html) と [MySQL 5.7](https://helpx.adobe.com/campaign/kb/campaign_fda_mysql.html) に2つのテクノートが追加されました。

## 18.10 - 05/11/2018{#release-18-10}

**リリースに含まれる新機能**

プッシュ通知の機能強化 — [詳細情報](https://docs.campaign.adobe.com/doc/AC/en/DLV_Sending_push_notifications_Setting_up_mobile_app_channel.html#Integrating_the_SDK_into_the_mobile_application)

SQL Data Managementアクティビティ — [詳細情報](https://docs.campaign.adobe.com/doc/AC/en/WKF_Repository_of_activities_Action_activities.html#SQL_Data_Management)

ワークフローの監視 — [詳細情報](https://docs.campaign.adobe.com/doc/AC/en/PRO_Production_procedures_Monitoring_processes.html#Workflow_monitoring)

**リリースに伴うその他のドキュメントの更新**

Campaign Classic API を[専用ページ](https://docs.campaign.adobe.com/doc/AC/en/jsapi/index.html)から入手できるようになりました。jsapi.chm ファイルを使用していた場合は、新しいオンラインバージョンを参照する必要があります。

互換性マトリックスが更新されました。[詳細を表示](https://helpx.adobe.com/campaign/kb/compatibility-matrix.html)

「Campaign Classicの非推奨および削除された機能」ページが更新されました。 [詳細を表示](https://helpx.adobe.com/campaign/kb/deprecated-and-removed-features.html)

[リリースノート](https://docs.campaign.adobe.com/doc/AC/en/RN.html)と[レガシーリリースノート](https://docs.campaign.adobe.com/doc/AC/en/RN_legacy.html)では、再呼び出しされたビルドに対して警告が追加されています。 17.9、18.4および18.6の累積ビルドも追加されました。

[セキュリティ](https://docs.campaign.adobe.com/doc/AC/getting_started/EN/security.html)、[配信品質](https://docs.campaign.adobe.com/doc/AC/getting_started/EN/deliverability.html)、[ビルドアップグレード](https://docs.campaign.adobe.com/doc/AC/getting_started/EN/buildUpgrade.html)入門ガイドが更新されました。

「[Privacy](https://helpx.adobe.com/campaign/kb/acc-privacy.html) Getting Started ガイド」は更新され、APIを外部から呼び出す方法と、queryDefを使用してステータスを照会し、GDPRファイルをダウンロードする方法に関する情報が追加されました。

送信ディスパッチに電子メールの添付ファイルをその場で追加するための、トランザクションメッセージングの使用例を追加しました。 [詳細を表示](https://docs.campaign.adobe.com/doc/AC/en/MCE_Use_case_Purpose.html)

接続しきい値のトラブルシューティングセクションを更新しました。 [詳細を表示](https://docs.campaign.adobe.com/doc/AC/en/PRO_Troubleshooting_Connection_thresholds.html)

プロキシ接続の設定方法に関する節が追加されました。 [詳細を表示](https://docs.campaign.adobe.com/doc/AC/en/INS_Additional_configurations_Configuring_Campaign_server.html#Proxy_connection_configuration)

許可された外部コマンドの制限に関する節を更新しました。 [詳細を表示](https://docs.campaign.adobe.com/doc/AC/en/INS_Additional_configurations_Configuring_Campaign_server.html#Restricting_authorized_external_commands)

SFTPの使用に関するトラブルシューティングの節を追加しました。 [詳細を表示](https://docs.campaign.adobe.com/doc/AC/en/PTF_Importing_and_exporting_data_SFTP_server_usage.html)

メッセージの送信ガイドの概要セクションが再編成されました。 配信作成のグローバルプロセスと様々な配信タイプに関する情報が追加されました。 [詳細を表示](https://docs.campaign.adobe.com/doc/AC/en/DLV_About_deliveries_and_channels_Communication_channels.html)

エラーメッセージのリストが更新されました。 [詳細を表示](https://docs.campaign.adobe.com/doc/AC/en/technicalResources/error_messages/error_codes.html)

シードアドレスの使い方に関する節を、メッセージの送信の概要の章に移動しました。 [詳細を表示](https://docs.campaign.adobe.com/doc/AC/en/DLV_Using_seed_addresses_About_seed_addresses.html)

新しいワークフローの使用例を追加しました。同時に実行するワークフローからの更新の管理。 [詳細を表示](https://docs.campaign.adobe.com/doc/AC/en/WKF_Use_cases_Coordinating_data_updates.html)

「インボックスレンダリング」セクションが更新され、Litmusに関する詳細な情報と、より詳細な手順が追加されました。 [詳細を表示](https://docs.campaign.adobe.com/doc/AC/en/DLV_Deliverability_management_Inbox_rendering.html#Multiplexing_the_mid-sourcing_server)

「スパムアサシン」セクションが改善されました。 [詳細を表示](https://docs.campaign.adobe.com/doc/AC/en/DLV_Deliverability_management_SpamAssassin.html)

「圧力ルールを使用したマーケティングの疲労の管理」の節に使用例が追加されました。 [詳細を表示](https://docs.campaign.adobe.com/doc/AC/en/CMP_Campaign_Optimization_Pressure_rules.html#Sending_only_the_highest-weighted_messages)

クロスチャネル配信ワークフローの作成方法を説明する新しい使用例が提供されました。 [詳細を表示](https://docs.campaign.adobe.com/doc/AC/en/WKF_Use_cases_Cross-channel_delivery_workflow.html)

「電子メールのアーカイブ」セクションに、いくつかのレコメンデーションが追加されました。 [詳細を表示](https://docs.campaign.adobe.com/doc/AC/en/INS_Additional_configurations_Email_deliverability.html#Activating_emails_BCC_archiving)

Adobe Campaignの最適な使用に向けた最小画面解像度に関する新しい推奨事項が追加されました。 [詳細を表示](https://docs.campaign.adobe.com/doc/AC/en/PTF_Starting_with_Adobe_Campaign_Adobe_Campaign_workspace.html#Screen_resolution)

Experience Manager統合ガイドが更新され、この統合の設定に説明が追加されました。 [詳細を表示](https://docs.campaign.adobe.com/doc/AC/en/ITG_Adobe_Experience_Manager_About_Adobe_Experience_Manager.html)

グループタイプリストとリストタイプリストの違いに関する情報を追加しました。 [詳細を表示](https://docs.campaign.adobe.com/doc/AC/en/PTF_Profile_management_Creating_and_managing_lists.html#About_lists_in_Adobe_Campaign)

レポート抽出を添付ファイルとして電子メールで送信するようにコードを更新。 [詳細を表示](https://docs.campaign.adobe.com/doc/AC/en/WKF_Use_cases_Sending_a_report_to_a_list.html#Step_3-_Creating_the_workflow)

過去7日間に電子メールを開いていない受信者をフィルターするクエリを作成する方法の例を追加しました。 [詳細を表示](https://docs.campaign.adobe.com/doc/AC/en/WKF_Use_cases_Designing_queries.html#Recipients_who_did_not_open_any_delivery)

Adobe Experience cloud統合ガイドでオーディエンスの共有を更新しました。 [詳細を表示](https://docs.campaign.adobe.com/doc/AC/en/ITG_Audience_sharing_Sharing_audiences_with_Adobe_Experience_Cloud.html)

一般的な質問のヘルプページに、利用可能なキャンペーン言語、Webフォームの翻訳、多言語電子メールに関する情報が含まれるようになりました。 [詳細を表示](../../platform/using/common-questions.md)

英語（米国）と英語（英国）のインスタンスの違いが、専用のセクションに表示されるようになりました。 [詳細を表示](https://docs.campaign.adobe.com/doc/AC/en/PTF_Starting_with_Adobe_Campaign_Adobe_Campaign_workspace.html#Formats_and_units)

よくある[質問](../../platform/using/common-questions.md)のヘルプページが、エラーメッセージページにリンクするようになりました。

「開く」トラッキングモードに関する情報が追加されました。 [詳細を表示](https://docs.campaign.adobe.com/doc/AC/en/DLV_Tracking_messages_Personalizing_URL_tracking.html)

WebアプリケーションおよびWebフォームの最小解像度に関する情報を追加します。 [詳細を表示](https://docs.campaign.adobe.com/doc/AC/en/WEB_Web_forms_About_web_forms.html)

キャンペーンとAdobe Experience cloudソリューション統合ガイドが更新され、再編成されました。 [詳細を表示](../../integrations/using/about-campaign-integrations.md)

Webフォームでのテキスト変数の使用に関する節を追加しました。 [詳細を表示](https://docs.campaign.adobe.com/doc/AC/en/WEB_Web_forms_Static_elements_in_a_web_form.html#Using_text_variables)

メッセージのURLトラッキングモードが詳細になりました。 [詳細を表示](https://docs.campaign.adobe.com/doc/AC/en/DLV_Tracking_messages_How_to_configure_tracked_links.html)

インスタンス作成セクションの構成が変更されました。 [詳細を表示](https://docs.campaign.adobe.com/doc/AC/en/INS_Initial_configuration_Creating_an_instance_and_logging_on.html)

日本の携帯電話での電子メールの送信に関する新しいセクションの説明が追加されました。 [詳細を表示](https://docs.campaign.adobe.com/doc/AC/en/DLV_Sending_emails_Defining_the_email_content.html#Sending_emails_on_Japanese_mobiles)

「最適化のパーソナライゼーション」セクションが更新され、詳細情報が追加されました。 [詳細を表示](https://docs.campaign.adobe.com/doc/AC/en/DLV_Personalizing_deliveries_Personalization_fields.html#Optimizing_personalization)

## 18.6 - 09/07/2018{#release-18-6}

**リリースに含まれる新機能**

互換性マトリックスが更新されました。[詳細を表示](https://helpx.adobe.com/campaign/kb/compatibility-matrix.html)

JSAPIのドキュメントが更新されました。 [詳細を表示](https://support.neolane.net/webApp/extranetLogin)

廃止および削除された機能ページが更新されました。 [詳細を表示](https://helpx.adobe.com/campaign/kb/deprecated-and-removed-features.html)

**リリースに伴うその他のドキュメントの更新**

Campaign Classicユーザーガイドの名前が変更され、ナビゲーションの簡素化、ユーザーエクスペリエンスの向上、情報へのアクセスおよびセルフヘルプが可能になりました。 [詳細を表示](https://docs.campaign.adobe.com/doc/AC/en/browseAC.html)

式エディターで使用できる関数のリストが更新されました。 [詳細を表示](https://docs.campaign.adobe.com/doc/AC/en/PTF_Creating_queries_Defining_filter_conditions.html#List_of_functions)

セキュリティ入門ガイドが更新され、PIを含むページの保護方法に関する情報が追加されました。 [詳細を表示](https://docs.campaign.adobe.com/doc/AC/getting_started/EN/security.html)

エラーメッセージのリストが更新されました。 [詳細を表示](https://docs.campaign.adobe.com/doc/AC/en/technicalResources/error_messages/error_codes.html)

IMS統合ドキュメントにトラブルシューティングの節が追加されました。 [詳細を表示](https://docs.campaign.adobe.com/doc/AC/en/ITG_Connecting_via_an_Adobe_ID_IMS_troubleshooting.html)

『Build Upgrade Getting Started』ガイドが更新されました。 [詳細を表示](https://docs.campaign.adobe.com/doc/AC/getting_started/EN/buildUpgrade.html)

「IP親和性の設定」セクションが更新されました。 [詳細を表示](https://docs.campaign.adobe.com/doc/AC/en/INS_Additional_configurations_Mid-sourcing_server.html#Multiplexing_the_mid-sourcing_server)

「パフォーマンスとスループット」のトラブルシューティングの節が追加されました。 [詳細を表示](https://docs.campaign.adobe.com/doc/AC/en/PRO_Troubleshooting_Performance_and_throughput_issues.html)

組み込みのパーソナライゼーションブロックのリストが、例で更新されました。 [詳細を表示](https://docs.campaign.adobe.com/doc/AC/en/DLV_Personalizing_deliveries_Personalization_blocks.html#Out-of-the-box_personalization_blocks)

配信失敗理由のリストが更新されました。 [詳細を表示](https://docs.campaign.adobe.com/doc/AC/en/DLV_Monitoring_deliveries_Understanding_delivery_failures.html#Delivery_failure_types_and_reasons)

パッケージ定義管理に関する新しいセクションが追加されました。 [詳細を表示](https://docs.campaign.adobe.com/doc/AC/en/PTF_Administration_basics_Working_with_data_packages.html#Managing_package_definitions)

Adobe AnalyticsとのCampaignの統合 — Data connectorsセクションが改善され、再編成されました。 [詳細を表示](https://docs.campaign.adobe.com/doc/AC/en/PTF_Connectors_Adobe_Analytics_Data_Connector.html)

新しいチュートリアルセクションが追加され、ステップバイステップガイドとハウツービデオへのリンクが追加されました。 [詳細を表示](https://docs.campaign.adobe.com/doc/AC/en/PTF_Starting_with_Adobe_Campaign_Tutorials.html)

SMSコネクタのプロトコルと設定に関する新しいテクノテーションが作成されました。 [詳細を表示](https://helpx.adobe.com/campaign/kb/sms-connector-protocol-and-settings.html)

『配信のベストプラクティスはじめに』ガイドが更新されました。 [詳細を表示](https://docs.campaign.adobe.com/doc/AC/getting_started/EN/deliveryBestPractices.html)

Web API展開を使用したMicrosoft Dynamics 365アカウント構成が更新されました。 [詳細を表示](https://docs.campaign.adobe.com/doc/AC/en/PTF_Connectors_CRM_Connectors.html#Example_for_Microsoft_Dynamics)

WindowsプラットフォームにAdobe Campaign Classicをインストールする手順が更新されました。 [詳細を表示](https://docs.campaign.adobe.com/doc/AC/en/INS_Installing_Campaign_in_Windows__Installing_the_server.html)

Adobe Experience cloudとCampaign Classicの間でのオーディエンス共有の時間枠について詳しく説明しました。 [詳細を表示](https://docs.campaign.adobe.com/doc/AC/en/ITG_Audience_sharing_Importing_and_exporting_audiences.html)

Campaign Classicリストの完全なナレッジベース記事が更新されました。 [詳細を表示](https://helpx.adobe.com/campaign/kb/article-list.html)

パフォーマンスの向上とベストプラクティスに関する新しいテクノテートが公開されました。 [詳細を表示](https://helpx.adobe.com/campaign/kb/best-practices-for-performance-improvement.html)

A/Bテストサンプルが更新されました。 [詳細を表示](https://docs.campaign.adobe.com/doc/AC/en/WKF_Use_cases_A-B_testing.html)

Campaign Classicの一般的な質問/FAQページが更新されました。 [詳細を表示](../../platform/using/common-questions.md)

## 18.4 - 24/04/2018{#release-18-4}

**リリースに含まれる新機能**

EU GDPR(General Data Protection Regulation) — [詳細を読む](https://helpx.adobe.com/campaign/kb/acc-privacy.html)

アクティブなプロファイル — [詳細情報](https://docs.campaign.adobe.com/doc/AC/en/PTF_Profile_management_About_profiles.html#Active_profiles)

Androidプッシュコネクタの機能強化 — [詳細情報](https://docs.campaign.adobe.com/doc/AC/en/DLV_Sending_push_notifications_Setting_up_mobile_app_channel.html#Android_connectors)

**リリースに伴うその他のドキュメントの更新**

リリースノートが改善され、ユーザーエクスペリエンスが向上し、お客様のリクエストに関連するすべてのパッチが含まれるようになりました。  [詳細を表示](https://docs.campaign.adobe.com/doc/AC/en/RN.html)

Campaign Classicに関する最も一般的な質問を含む新しいページが追加されました。 [詳細を表示](../../platform/using/common-questions.md)

エラーメッセージのリストが更新されました。 [詳細を表示](https://docs.campaign.adobe.com/doc/AC/en/technicalResources/error_messages/error_codes.html)

Marketing Cloud Triggersテクノートが更新されました。 [詳細を表示](https://helpx.adobe.com/campaign/kb/triggers-and-campaign.html)

レガシーバージョンのCampaign ClassicにGDPR（プライバシー）パッケージをインストールして展開する方法に関するテクノテートが追加されました。 [詳細を表示](https://helpx.adobe.com/campaign/kb/how-to-install-gdpr-package-on-legacy-versions.html)

新しいSequence自動生成メカニズムに関するテクノテートが追加されました。 [詳細を表示](https://helpx.adobe.com/campaign/kb/sequence_auto_generation.html)

JSAPIのドキュメントが更新されました。 [詳細を表示](https://support.neolane.net/webApp/extranetLogin)

互換性マトリックスが更新されました。[詳細を表示](https://helpx.adobe.com/campaign/kb/compatibility-matrix.html)

廃止された機能とバージョンを一覧表示する新しいページが提供されました。 [詳細を表示](https://helpx.adobe.com/campaign/kb/deprecated-and-removed-features.html)

RDBMSに関する既知の制限事項とベストプラクティスが追加されました。 [詳細を表示](https://docs.campaign.adobe.com/doc/AC/en/INS_Prerequisites_and_recommendations__Database.html)

SFTPの使用に関するベストプラクティスを説明します。 [詳細を表示](https://docs.campaign.adobe.com/doc/AC/en/PTF_Importing_and_exporting_data_SFTP_server_usage.html)

技術ワークフローのリストが更新されました。 [詳細を表示](https://docs.campaign.adobe.com/doc/AC/en/WKF_Technical_workflows_About_technical_workflows.html)

ナレッジベースの記事（旧称「テクノロジー」）のリストは、こちらから入手できます。 [詳細を表示](https://helpx.adobe.com/campaign/kb/article-list.html)

[ハウツービデ](https://docs.campaign.adobe.com/doc/AC/en/Videos/Videos.html)オが更新されました。

LINEドキュメントは、LINEパッケージの減価償却後に更新されました。 [詳細を表示](https://docs.campaign.adobe.com/doc/AC/en/DLV_Sending_messages_on_mobiles_LINE_channel.html)

レポートインジケーターの計算ドキュメントを更新しました。 [詳細を表示](../../reporting/using/indicator-calculation.md)

Oracleとのタイムゾーンファイルの配置に関する情報を追加しました。 [詳細を表示](https://docs.campaign.adobe.com/doc/AC/en/MIG_Configuration_General_configurations.html#Oracle)

新しい「配信の監視」節を追加し、配信の失敗と検疫の管理に関する情報を更新しました。 [詳細を表示](https://docs.campaign.adobe.com/doc/AC/en/DLV_Monitoring_deliveries_Monitoring_a_delivery.html)

「パーソナライゼーションブロック」セクションを再編成し、そのまま使用できるパーソナライゼーションブロックに関する新しい情報を追加しました。
[詳細を表示](https://docs.campaign.adobe.com/doc/AC/en/DLV_Personalizing_deliveries_Personalization_blocks.html)

「電子メールのアーカイブ」セクションを、ファイル構成に関する新しい情報で再編 ```config-<instance name>.xml``` 成しました。 [詳細を表示](https://docs.campaign.adobe.com/doc/AC/en/INS_Additional_configurations_Email_archiving.html#Activating_email_archiving__on_premise_)

Message Center（コントロール）の技術ワークフローに関する情報を更新しました。 [詳細を表示](https://docs.campaign.adobe.com/doc/AC/en/WKF_Technical_workflows_Message_Center__Control_.html)

SMTPリレーを設定する際のスループットの制限に関する情報を追加しました。 [詳細を表示](https://docs.campaign.adobe.com/doc/AC/en/INS_Additional_configurations_Configuring_Campaign_server.html#Personalizing_delivery_parameters)

## 17.12 - 14/12/2017{#release-doc-14-12-2017}

[Adobe Campaign Classicドキュメント](https://helpx.adobe.com/support/campaign/classic.html)セットは、使いやすさを改善するために再編成されました。

主要なキャンペーン機能のヘルプマテリアル、操作方法、サンプル、ビデオにアクセスしやすいように、新しい「チュートリアル」セクションが追加されました。 [詳細を表示](https://docs.campaign.adobe.com/doc/AC/en/PTF_Starting_with_Adobe_Campaign_Tutorials.html)

配信ステータスを監視する際に役立つが、発生の可能性があるエラーを監視し、その修正方法を学ぶための新しいセクションが追加されました。 [詳細を表示](https://docs.campaign.adobe.com/doc/AC/en/DLV_Monitoring_deliveries_Monitoring_a_delivery.html)

エラーメッセージのリストが更新されました。 [詳細を表示](https://docs.campaign.adobe.com/doc/AC/en/technicalResources/error_messages/error_codes.html)

Marketing Cloud Triggersテクノートが更新されました。 [詳細を表示](https://helpx.adobe.com/campaign/kb/triggers-and-campaign.html)

Campaign Classic移行ガイドがコレクションに追加されました。 [詳細を表示](https://docs.campaign.adobe.com/doc/AC/en/MIG_Migration_overview_About_migration.html)

キャンペーン互換表が更新されました。 [詳細を表示](https://helpx.adobe.com/campaign/kb/compatibility-matrix.html)

該当する場合、設定手順とインストール手順で、適用するホスティングモデルが示されるようになりました。 [詳細を表示](https://docs.campaign.adobe.com/doc/AC/en/INS_Additional_configurations_Configuring_Campaign_server.html)

ナレッジベースの新しい記事を使用して、オンプレミス、ハイブリッド、およびマネージドサービスのデプロイメントの設定と機能の違いを強調します。 [詳細を表示](https://helpx.adobe.com/campaign/kb/acc-on-prem-vs-hosted.html)

標準パッケージのインストール方法に関する手順を追加しました。 [詳細を表示](https://docs.campaign.adobe.com/doc/AC/en/INS_Initial_configuration_Installing_packages.html)

Audience ManagerまたはPeopleコアサービスとの統合を設定する方法に関する詳細を追加しました。 [詳細を表示](https://docs.campaign.adobe.com/doc/AC/en/ITG_Audience_sharing_Configuring_shared_audiences_integration_in_Adobe_Campaign.html)

PostreSQLを使用する場合は、Campaignのインストールにpgcryptoが必要になりました。 [詳細を表示](https://docs.campaign.adobe.com/doc/AC/en/INS_Installing_Campaign_in_Linux__Prerequisites.html#Database_access_layers)

## 17.9 - 25/09/2017{#release-17-9}

**リリースに含まれる新機能**

ACSコネクタの強化

SAP HANAコネクタ — [詳細情報](https://docs.campaign.adobe.com/doc/AC/en/PTF_Connectors_Accessing_an_external_database.html#SAP_HANA)

HiveSQL経由のHadoop Connector — [詳細情報](https://docs.campaign.adobe.com/doc/AC/en/PTF_Connectors_Accessing_an_external_database.html#Hadoop)

回線チャネル：メッセージングの強化 — [詳細情報](https://docs.campaign.adobe.com/doc/AC/en/DLV_Sending_messages_on_mobiles_LINE_channel.html)

**リリースに伴うその他のドキュメントの更新**

新しいクエリーサンプルが追加されました。 [詳細を表示](https://docs.campaign.adobe.com/doc/AC/en/WKF_Use_cases_Designing_queries.html#Filtering_duplicated_recipients)

配信のベストプラクティスガイドが更新されました。 [詳細を表示](https://docs.campaign.adobe.com/doc/AC/getting_started/EN/deliveryBestPractices.html)

A/Bテストサンプルが更新され、手順が見つかりません。 [詳細を表示](https://docs.campaign.adobe.com/doc/AC/en/WKF_Use_cases_A-B_testing.html)

ハウツービデオが更新されました。 [詳細を表示](https://docs.campaign.adobe.com/doc/AC/en/Videos/Videos.html)

電子メールのアーカイブセクションを更新します。 [詳細を表示](https://docs.campaign.adobe.com/doc/AC/en/INS_Additional_configurations_Email_archiving.html)

ワークフローでのスケジューラの使用を明確にする。 [詳細を表示](../../workflow/using/scheduler.md)

一時停止したワークフローのベストプラクティスの追加 [詳細を表示](https://docs.campaign.adobe.com/doc/AC/en/WKF__General_operation_Executing_a_workflow.html)

読み込み時の前処理ファイルと、ワークフロー内のデータを書き出す際の後処理に関する新しい手順が追加されました。 ここを [読みます](https://docs.campaign.adobe.com/doc/AC/en/WKF__General_operation_Importing_data.html)。

SMSメッセージドキュメントの検疫メカニズムが更新され、拡張汎用SMPPコネクタのエラー管理の特性が反映されました。 [詳細を表示](https://docs.campaign.adobe.com/doc/AC/en/DLV_Monitoring_deliveries_Understanding_quarantine_management.html#SMS_quarantines).

モバイルアプリチャネルのドキュメントが強化され、Androidでリッチ通知を送信する詳細な手順が追加されました。 [詳細を表示](https://docs.campaign.adobe.com/doc/AC/en/DLV_Sending_push_notifications_Setting_up_mobile_app_channel.html#Rich_notifications).

インボックスレンダリングのドキュメントが更新されました。 [詳細を表示](https://docs.campaign.adobe.com/doc/AC/en/DLV_Deliverability_management_Inbox_rendering.html).

Webトラッキングの設定に関するドキュメントが強化され、更新された例とメモが追加されました。 [詳細を表示](https://docs.campaign.adobe.com/doc/AC/en/CFG_Setting_up_web_tracking_Additional_parameters.html#Redirection_server_configuration).

SMSチャネルのドキュメントが更新され、拡張汎用SMPPコネクタに適用する「自動応答」セクションに説明が追加されました。 [詳細を表示](https://docs.campaign.adobe.com/doc/AC/en/DLV_Sending_messages_on_mobiles_SMS_channel.html#Creating_an_SMPP_external_account).

Social Marketingのドキュメントが更新されました。 [詳細を表示](../../social/using/about-social-marketing.md).

IPウォーミングに関する新しいテクノティーが追加されました。 [詳細を表示](https://docs.campaign.adobe.com/doc/AC/en/technicalResources/Technotes/AdobeCampaign_Deliverability_IP_Warming_overview.pdf).

ビルドアップグレードの新しい概要が追加されました。 [詳細を表示](https://docs.campaign.adobe.com/doc/AC/getting_started/EN/buildUpgrade.html).

## May 2017{#release-doc-30-05-2017}

はじめにガイドが新しく公開されました。配信の作成とターゲティングから送信や監視に至るまで、Adobe Campaign での配信に関するベストプラクティスを説明します。[詳細を表示](https://docs.campaign.adobe.com/doc/AC/getting_started/EN/deliveryBestPractices.html)

セキュリティに関するはじめにガイドが更新されました。[詳細を表示](https://docs.campaign.adobe.com/doc/AC/getting_started/EN/security.html)

The [&quot;Archiving emails&quot; documentation&quot;](https://docs.campaign.adobe.com/doc/AC/en/INS_Additional_configurations_Email_archiving.html) has been updated with the [&quot;Email BCC&quot;](https://docs.campaign.adobe.com/doc/AC/en/INS_Additional_configurations_Email_archiving.html#Configuring_the_BCC_email_address__on_premise_) section and the [detailed steps to activate the feature](https://docs.campaign.adobe.com/doc/AC/en/DLV_Sending_emails_Sending_messages.html#Archiving_emails).

いくつかのビデオが追加、更新されました。[詳細を表示](https://docs.campaign.adobe.com/doc/AC/en/Videos/Videos.html)

データベースを更新せずに、外部ファイルから読み込まれた受信者に配信を送信する方法について説明します。[詳細を表示](../../delivery/using/steps-defining-the-target-population.md#selecting-external-recipients)

二重のオプトインの例が更新されました。[詳細を表示](../../web/using/use-cases--web-forms.md)

## March 2017{#release-doc-31-03-2017}

配信品質：[はじめにガイド](https://docs.campaign.adobe.com/doc/AC/getting_started/EN/deliverability.html)が更新されました。配信品質ドキュメントに、より詳細な[概要](https://docs.campaign.adobe.com/doc/AC/en/DLV_Deliverability_management_About_deliverability.html)と[実装プロセスおよび主な手順](../../delivery/using/deliverability-key-points.md)の説明が含まれるようになりました。

「ウェーブを使用した送信」の節が移動され、詳細な例、推奨および使用例が追加されてより充実した内容となりました。[詳細を表示](https://docs.campaign.adobe.com/doc/AC/en/DLV_Sending_emails_Sending_messages.html#Sending_using_multiple_waves)

「強制隔離の管理」の節に SMS メッセージに特有のエラーを説明する表が追加されました。[詳細を表示](https://docs.campaign.adobe.com/doc/AC/en/DLV_Monitoring_deliveries_Understanding_quarantine_management.html#SMS_quarantines)

ワークフロー：新しいマルチチャネルワークフローの例が追加されました。[詳細を表示](https://docs.campaign.adobe.com/doc/AC/en/WKF_Repository_of_activities_Action_activities.html#Cross-channel_deliveries)

Marketing Cloud トリガー：Adobe Campaign を使用した設定方法および使用方法に関するテクニカルノートが追加されました。[詳細を表示](https://helpx.adobe.com/campaign/kb/triggers-and-campaign.html)

ワークフローガイドが再構成され、拡張されました。ワークフローの[作成](https://docs.campaign.adobe.com/doc/AC/en/WKF__General_operation_Building_a_workflow.html)および[実行](https://docs.campaign.adobe.com/doc/AC/en/WKF__General_operation_Executing_a_workflow.html)方法、データの[ターゲティング](https://docs.campaign.adobe.com/doc/AC/en/WKF__General_operation_Targeting_data.html)および[管理](https://docs.campaign.adobe.com/doc/AC/en/WKF__General_operation_Targeting_data.html#Data_Management)方法、データの[インポート](https://docs.campaign.adobe.com/doc/AC/en/WKF__General_operation_Importing_data.html)方法、および[データベースを更新](https://docs.campaign.adobe.com/doc/AC/en/WKF__General_operation_How_to_use_workflow_data.html#Updating_the_database)または[配信を送信](https://docs.campaign.adobe.com/doc/AC/en/WKF__General_operation_How_to_use_workflow_data.html#Delivering_via_a_workflow)するためのワークフローデータの使用方法が簡単に見つかります。

[インポートのベストプラクティス](https://docs.campaign.adobe.com/doc/AC/en/WKF__General_operation_Importing_data.html#Import_best_practices)に続いて[インポートワークフロー](https://docs.campaign.adobe.com/doc/AC/en/WKF__General_operation_How_to_use_workflow_data.html#Delivering_via_a_workflow)の例が提供されました。この新しいバージョン向けにインストールガイドが更新されました。[詳細を表示](https://docs.campaign.adobe.com/doc/AC/en/INS_Architecture_and_hosting_models_General_architecture.html)

互換性マトリックスが更新されました。[詳細を表示](https://helpx.adobe.com/campaign/kb/compatibility-matrix.html)

E メール配信にクーポンを含めると、受信者にとって付加価値となります。[詳細を表示](https://docs.campaign.adobe.com/doc/AC/en/DLV_Personalizing_deliveries_Personalized_coupons.html)

## Adobe Campaign v7 - 2017/03/16{#release-17-2}

**リリースに含まれる新機能**

ACS コネクタ

Microsoft Dynamics用Web API — [詳細情報](https://docs.campaign.adobe.com/doc/AC/en/PTF_Connectors_CRM_Connectors.html#Example_for_Microsoft_Dynamics)

電子メールアーカイブBCCメソッド — [詳細情報](https://docs.campaign.adobe.com/doc/AC/en/INS_Additional_configurations_Email_archiving.html#Updated_email_archiving_system__BCC_)

Amazon Simple Storage Service(S3)コネクタ — [詳細情報](https://docs.campaign.adobe.com/doc/AC/en/WKF_Repository_of_activities_Event_activities.html#File_transfer)

