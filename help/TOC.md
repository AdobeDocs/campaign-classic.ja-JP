---
audience: end-user
breadcrumb-title: Campaign Classic v7 ドキュメント
product: campaign
title: Campaign Classic v7 ガイド
user-guide-title: Campaign Classic v7 ガイド
user-guide-description: Adobe Campaign Classic v7 に関する製品ドキュメント。
sub-product: adobe campaign classic
type: Documentation
nudge: false
source-git-commit: 59d78c785d8984861fd537c2f64f82a7d2d77fbf
workflow-type: ht
source-wordcount: '1657'
ht-degree: 100%
---

# Adobe Campaign Classic v7 ドキュメント {#using}

+ [Campaign v7 ドキュメント](campaign-classic-home.md)
+ リリースノート {#release-notes}
  + [アップグレードの概要](rn/using/rn-overview.md)
  + [最新リリース](rn/using/latest-release.md)
  + 以前のリリース {#previous-releases}
    + [2025](rn/using/release-2025.md)
    + [2024](rn/using/release-2024.md)
    + {hide-from-toc}[2023 - 非表示](rn/using/release-2023.md)
    + {hide-from-toc}[2022 - 非表示](rn/using/release-2022.md)
    + {hide-from-toc}[2021 - 非表示](rn/using/release-2021.md)
    + {hide-from-toc}[[!DNL Gold Standard - HIDDEN]](rn/using/gold-standard.md)
  + [非推奨（廃止予定）の機能](rn/using/deprecated-features.md)
  + [互換性マトリックス](rn/using/compatibility-matrix.md)
+ はじめに {#getting-started}
  + [Adobe Campaign Classic の概要](platform/using/about-adobe-campaign-classic.md)
  + [Adobe Campaign のローンチ](platform/using/launching-adobe-campaign.md)
  + [Campaign コネクタ](platform/using/about-connectors.md)
  + よくある質問 {#faq}
    + [Campaign Classic に関する FAQ](platform/using/faq-campaign-classic-v7.md)
    + [ビルドのアップグレード](platform/using/faq-build-upgrade.md)
  + プライバシー {#privacy}
    + [プライバシーと同意](platform/using/privacy-and-recommendations.md)
    + [プライバシー管理](platform/using/privacy-management.md)
    + プライバシーリクエスト {#privacy-requests}
      + [プライバシーリクエストの作成と管理](platform/using/privacy-requests-ui.md)
      + [自動プライバシーリクエストプロセス](platform/using/privacy-requests-api.md)
    + [個人情報の販売に対するオプトアウト](platform/using/privacy-requests-ccpa.md)
  + プロファイル管理 {#profile-management}
    + [プロファイルについて](platform/using/about-profiles.md)
    + [データの更新](platform/using/updating-data.md)
  + データのインポートとエクスポート {#importing-and-exporting-data}
    + 一般的なインポートおよびエクスポートの作成 {#generic-imports-exports}
      + [ジョブの実行の監視](platform/using/monitoring-jobs-execution.md)
      + [一般的なインポートのサンプル](platform/using/import-operations-samples.md)
    + データの暗号化と圧縮の管理 {#managing-data-encryption-compression}
      + [処理前のファイルの解凍と復号化](platform/using/unzip-decrypt.md)
      + [処理前のファイルの圧縮または暗号化](platform/using/zip-encrypt.md)
    + ベストプラクティスとトラブルシューティング {#best-practices}
      + [インポートとエクスポートのベストプラクティス](platform/using/import-export-best-practices.md)
      + [SFTP サーバーのベストプラクティスとトラブルシューティング](platform/using/sftp-server-usage.md)
  + 権限 {#permissions}
    + [権限の基本を学ぶ](platform/using/access-management.md)
    + ネイティブ認証（レガシー） {#native}
      + [オペレーターの作成と管理](platform/using/access-management-operators.md)
      + [グループの作成と管理](platform/using/access-management-groups.md)
  + CRM コネクタ {#connectors}
    + [CRM コネクタの基本を学ぶ](platform/using/crm-connectors.md)
+ メッセージの作成と送信 {#sending-messages}
  + [メッセージの基本を学ぶ](delivery/using/communication-channels.md)
  + {hide-from-toc}[配信設定 - 非表示](delivery/using/delivery-settings.md)
  + クイックスタート {#key-steps-when-creating-a-delivery}
    + {hide-from-toc}[配信の送信 - 非表示](delivery/using/steps-sending-the-delivery.md)
  + [メールを送信](delivery/using/about-email-channel.md)
  + SMS を送信 {#sending-messages-on-mobiles}
    + SMS チャネルの設定 {#sms-set-up}
      + [スタンドアロンインスタンスでの SMS の設定](delivery/using/sms-set-up.md)
      + [ミッドソーシングインフラストラクチャでの SMS の設定](delivery/using/sms-set-up-mid.md)
      + [SMS コネクタのプロトコルと設定](delivery/using/sms-protocol.md)
      + [その他の設定](delivery/using/sms-send.md)
      + [SMS のトラブルシューティング](delivery/using/troubleshooting-sms.md)
    + {hide-from-toc}[拡張された汎用 SMPP コネクタへの移行](delivery/using/unsupported-connector-migration.md)
  + [プッシュ通知の送信](delivery/using/about-mobile-app-channel.md)
  + プッシュ通知の送信 {#sending-push-notifications}
    + モバイルアプリケーションの設定{#configure-the-mobile-app}
      + {hide-from-toc}[アプリ設定の基本を学ぶ - 非表示](delivery/using/get-started-app-config.md)
      + {hide-from-toc}[iOS の設定手順 - 非表示](delivery/using/configuring-the-mobile-application.md)
      + {hide-from-toc}[Android の設定手順 - 非表示](delivery/using/configuring-the-mobile-application-android.md)
    + {hide-from-toc}[トラブルシューティング - 非表示](delivery/using/troubleshooting.md)
  + [ダイレクトメールの送信](delivery/using/about-direct-mail-channel.md)
  + 配信のパーソナライズ {#personalizing-deliveries}
    + [パーソナライゼーションについて](delivery/using/about-personalization.md)
  + シードアドレスを使用 {#using-seed-addresses}
    + [ユースケース：基準に基づいたシードアドレスの選択](delivery/using/use-case-selecting-seed-addresses-on-criteria.md)
    + [ユースケース：フィールド置換の設定](delivery/using/use-case-configuring-the-field-substitution.md)
  + A/B テスト {#a-b-testing}
    + [A/B テストの基本を学ぶ](delivery/using/get-started-a-b-testing.md)
    + [A/B テストの設定](delivery/using/configuring-a-b-testing.md)
    + ユースケース {#use-case}
      + [このユースケースについて](delivery/using/a-b-testing-use-case.md)
      + [ターゲティングワークフローの作成](delivery/using/a-b-testing-uc-targeting-workflow.md)
      + [母集団サンプルの設定](delivery/using/a-b-testing-uc-population-samples.md)
      + [配信テンプレートの作成](delivery/using/a-b-testing-uc-delivery-templates.md)
      + [配信の設定](delivery/using/a-b-testing-uc-configuring-deliveries.md)
      + [スクリプトの作成](delivery/using/a-b-testing-uc-script.md)
      + [最終配信の定義](delivery/using/a-b-testing-uc-final-delivery.md)
      + [ワークフローの開始](delivery/using/a-b-testing-uc-start-workflow.md)
      + [結果の分析](delivery/using/a-b-testing-uc-analyzing.md)
  + サービスと購読 {#subscriptions-and-referrals}
    + [サービスと購読について](delivery/using/about-services-and-subscriptions.md)
    + [購読の管理](delivery/using/managing-subscriptions.md)
    + [バイラルおよびソーシャルマーケティング](delivery/using/viral-and-social-marketing.md)
  + 配信の監視 {#monitoring-deliveries}
    + [配信パフォーマンスの監視](delivery/using/about-delivery-monitoring.md)
    + [メッセージのトラッキング](delivery/using/about-message-tracking.md)
    + [配信のパフォーマンスとトラブルシューティング](delivery/using/delivery-performance-troubleshooting.md)
    + [配信エラーと強制隔離の管理](delivery/using/delivery-failures-quarantine.md)
    + [詳細設定：配信ログのカスタマイズ](delivery/using/customize-delivery-logs.md)
  + 配信品質の管理 {#deliverability-management}
    + [配信品質とは](delivery/using/about-deliverability.md)
    + [インボックスレンダリング](delivery/using/inbox-rendering.md)
    + [トラブルシューティング](delivery/using/deliverability-faq.md)
  + コンテンツ管理モジュール {#content-management}
    + [コンテンツ管理について](delivery/using/about-content-management.md)
    + [コンテンツマネージャーのリソースと原則](delivery/using/content-manager-resources-and-principles.md)
    + [ユースケース：コンテンツ管理の作成](delivery/using/use-case-creating-content-management.md)
    + [データスキーマ](delivery/using/data-schemas.md)
    + [入力フォーム](delivery/using/input-forms.md)
    + [フォーマット設定](delivery/using/formatting.md)
    + [公開テンプレート](delivery/using/publication-templates.md)
    + [コンテンツテンプレートの使用](delivery/using/using-a-content-template.md)
    + [コンテンツのエンリッチメント](delivery/using/enriching-content.md)
    + [ワークフローによる自動化](delivery/using/automating-via-workflows.md)
+ [マーケティングキャンペーンのオーケストレーション](campaign/using/about-marketing-campaigns.md)
+ Response Manager {#response-manager}
  + [Response Manager の基本を学ぶ](response/using/about-response-manager.md)
  + [設定](response/using/configuration.md)
  + [仮説テンプレート](response/using/hypothesis-templates.md)
  + [仮説の作成](response/using/creating-hypotheses.md)
  + [仮説のトラッキング](response/using/hypothesis-tracking.md)
+ レポートの設計と共有 {#reporting}
  + レポートの基本を学ぶ {#reporting-in-adobe-campaign}
    + [レポートのベストプラクティス](reporting/using/best-practices.md)
  + ビルトインレポートへのアクセス {#accessing-built-in-reports}
    + [ビルトインレポートについて](reporting/using/about-campaign-built-in-reports.md)
    + [レポートのリスト](reporting/using/list-of-reports.md)
  + 配信に関するレポート{#reports-on-deliveries}
    + [指標の計算](reporting/using/indicator-calculation.md)
  + 母集団の分析 {#analyzing-populations}
    + [記述的分析とは](reporting/using/about-descriptive-analysis.md)
    + [最初の記述的分析レポートの作成](reporting/using/using-the-descriptive-analysis-wizard.md)
    + [分析レポートの管理と設定](reporting/using/processing-a-report.md)
    + [分析レポートのユースケース](reporting/using/use-cases.md)
  + レポートの新規作成 {#creating-new-reports}
    + [レポートを設計するための主な手順](reporting/using/about-reports-creation-in-campaign.md)
    + [レポートの新規作成](reporting/using/creating-a-new-report.md)
    + [分析するデータの収集](reporting/using/collecting-data-to-analyze.md)
    + [コンテキストの使用](reporting/using/using-the-context.md)
    + [テーブルの作成](reporting/using/creating-a-table.md)
    + [グラフの作成](reporting/using/creating-a-chart.md)
    + [要素のレイアウト](reporting/using/element-layout.md)
    + [条件付きコンテンツの定義](reporting/using/defining-a-conditional-content.md)
    + [高度な機能](reporting/using/advanced-functionalities.md)
    + [レポートのプロパティ](reporting/using/properties-of-the-report.md)
    + [レポートへのアクセスの設定](reporting/using/configuring-access-to-the-report.md)
    + [レポートに対するアクション](reporting/using/actions-on-reports.md)
  + [キューブを使用したレポートの設計](reporting/using/ac-cubes.md)
+ Web コンテンツの設計 {#designing-content}
  + web アプリケーション {#web-applications}
    + [web アプリケーションの基本を学ぶ](web/using/about-web-applications.md)
    + [web アプリケーションの新規作成](web/using/creating-a-new-web-application.md)
    + [web アプリケーションの設計](web/using/designing-a-web-application.md)
    + [ユースケース：概要の作成](web/using/use-cases-creating-overviews.md)
    + [web アプリケーションの翻訳](web/using/translating-a-web-application.md)
    + [web アプリケーションへの訪問のトラッキング](web/using/tracking-a-web-application.md)
    + [web アプリケーショントラッキングのオプトアウト](web/using/web-application-tracking-opt-out.md)
  + HTML コンテンツの編集 {#editing-html-content}
    + [HTML エディターの基本を学ぶ](web/using/about-campaign-html-editor.md)
    + [テンプレート管理](web/using/template-management.md)
    + [コンテンツエディターのインターフェイス](web/using/content-editor-interface.md)
    + [コンテンツの編集](web/using/editing-content.md)
    + [コンテンツ編集のベストプラクティス](web/using/content-editing-best-practices.md)
    + [ランディングページの作成](web/using/creating-a-landing-page.md)
    + [ユースケース：メール配信の作成](web/using/use-case-creating-an-email-delivery.md)
  + Web フォーム {#web-forms}
    + [web フォームの基本を学ぶ](web/using/about-web-forms.md)
    + [web フォームテンプレートの使用](web/using/using-a-web-form-template.md)
    + [web フォームへのフィールドの追加](web/using/adding-fields-to-a-web-form.md)
    + [web フォームの静的要素](web/using/static-elements-in-a-web-form.md)
    + [web フォームレイアウトの定義](web/using/defining-web-forms-layout.md)
    + [フォームレンダリング](web/using/form-rendering.md)
    + [ページの順序付けの定義](web/using/defining-web-forms-page-sequencing.md)
    + [web フォームの回答の保存](web/using/web-forms-answers.md)
    + [web フォームの公開](web/using/publishing-a-web-form.md)
    + [web フォームプロパティの定義](web/using/defining-web-forms-properties.md)
    + [web フォームの翻訳](web/using/translating-a-web-form.md)
    + [ユースケース：web フォーム](web/using/use-cases-web-forms.md)
+ オンライン調査の作成 {#online-surveys}
  + [調査の基本を学ぶ](surveys/using/about-surveys.md)
  + [調査を作成するための主な手順](surveys/using/getting-started-with-surveys.md)
  + [調査の設計](surveys/using/building-a-survey.md)
  + [回答の管理](surveys/using/managing-answers.md)
  + [収集したデータの公開、トラッキングおよび使用](surveys/using/publish-track-and-use-collected-data.md)
  + [調査の設定](surveys/using/configuring-surveys.md)
  + [ユースケース：リファラルフォームの作成](surveys/using/use-case-creating-a-refer-a-friend-form.md)
  + [ユースケース：オンライン調査への回答に関するレポートの表示](surveys/using/use-case-displaying-report-on-answers-to-an-online-survey.md)
+ Adobe Experience Cloud との統合 {#integrating-with-adobe-experience-cloud}
  + [Campaign 統合の基本を学ぶ](integrations/using/about-campaign-integrations.md)
  + [Adobe テクニカルアカウントの作成](integrations/using/oauth-technical-account.md)
  + Adobe Experience Cloud Triggers {#experience-triggers}
    + [ [!DNL Experience Cloud Triggers] の操作](integrations/using/about-triggers.md)
    + [パイプラインの設定](integrations/using/configuring-pipeline.md)
    + [カスタム実装用のイベントの設定](integrations/using/events.md)
    + [パイプラインの監視](integrations/using/pipeline-monitoring.md)
    + [パイプラインのトラブルシューティング](integrations/using/pipeline-troubleshooting.md)
  + Adobe Experience Platform のソースと宛先 {#aep-sources-destinations}
    + [ソースと宛先の操作](integrations/using/get-started-sources-destinations.md)
    + [Campaign への Adobe Experience Platform オーディエンスの取り込み](integrations/using/ingest-aep-data.md)
    + [Campaign から Adobe Experience Platform へのデータのエクスポート](integrations/using/export-campaign-data.md)
  + Adobe Analytics Connector{#analytics-connector}
    + [Adobe Analytics Connector の基本を学ぶ](integrations/using/gs-aa.md)
    + [Adobe Analytics コネクタのプロビジョニング](integrations/using/adobe-analytics-provisioning.md)
  + オーディエンスの共有 {#audience-sharing}
    + [ [!DNL Adobe Experience Cloud] とのオーディエンスの共有](integrations/using/sharing-audiences-with-adobe-experience-cloud.md)
    + [アドビへのリクエストの送信](integrations/using/submitting-request-to-adobe.md)
    + [ [!DNL Adobe Campaign] での共有オーディエンス統合の設定](integrations/using/configuring-shared-audiences-integration-in-adobe-campaign.md)
    + {hide-from-toc}[トラブルシューティング](integrations/using/troubleshooting.md)
    + [オーディエンスのインポートとエクスポート](integrations/using/importing-and-exporting-audiences.md)
  + アセットの共有 {#asset-sharing}
    + [ [!DNL Adobe Experience Cloud] とのアセットの共有](integrations/using/sharing-assets-with-adobe-experience-cloud.md)
    + [ [!DNL Assets] へのアクセスの設定](integrations/using/configuring-access-to-assets.md)
    + [共有アセットの挿入](integrations/using/inserting-a-shared-asset.md)
  + Adobe Experience Manager {#adobe-experience-manager}
    + [ [!DNL Adobe Experience Manager] の操作](integrations/using/about-adobe-experience-manager.md)
    + [統合の設定](integrations/using/configuring-the-integration.md)
    + [ [!DNL Experience Manager]  ニュースレターの作成](integrations/using/creating-an-experience-manager-newsletter.md)
  + Adobe Target {#adobe-target}
    + [ [!DNL Adobe Target] の操作](integrations/using/integrating-with-adobe-target.md)
    + [ [!DNL Adobe Target] との統合の設定](integrations/using/configuring-the-integration-with-adobe-target.md)
    + [動的画像の挿入](integrations/using/inserting-a-dynamic-image.md)
  + ACS コネクタ {#acs-connector}
    + {hide-from-toc}[ [!DNL ACS Connector]  の基本を学ぶ - 非表示](integrations/using/acs-connector-principles-and-data-cycle.md)
    + {hide-from-toc}[プロファイルの同期 - 非表示](integrations/using/synchronizing-profiles.md)
    + {hide-from-toc}[オーディエンスの同期 - 非表示](integrations/using/synchronizing-audiences.md)
    + {hide-from-toc}[Web アプリケーションの同期 - 非表示](integrations/using/synchronizing-web-applications.md)
    + {hide-from-toc}[ [!DNL ACS Connector]  のトラブルシューティング - 非表示](integrations/using/troubleshooting-the-acs-connector.md)
+ [ワークフローを使用した自動化](workflow/using/about-workflows.md)
+ オファーの管理 {#managing-offers}
  + インタラクションの基本を学ぶ {#interaction-overview}
    + [インタラクションとオファー管理](interaction/using/interaction-and-offer-management.md)
  + オファーカタログの管理 {#managing-an-offer-catalog}
    + [オファーの承認と有効化](interaction/using/approving-and-activating-an-offer.md)
    + [オファーテンプレートの管理](interaction/using/managing-offer-templates.md)
    + [オファープレゼンテーションの管理](interaction/using/managing-offer-presentation.md)
  + オファーのシミュレーション{#simulating-offers}
    + [オファーのシミュレーションについて](interaction/using/about-offers-simulation.md)
    + [実行設定](interaction/using/execution-settings.md)
    + [シミュレーションのスコープ](interaction/using/simulation-scope.md)
    + [シミュレーションのトラッキング](interaction/using/simulation-tracking.md)
  + 詳細設定パラメーター {#advanced-parameters}
    + [詳細設定パラメーターの使用](interaction/using/using-advanced-parameters.md)
    + [追加データ](interaction/using/additional-data.md)
    + [拡張の例](interaction/using/extension-example.md)
    + [テスト環境の作成](interaction/using/creating-a-test-environment.md)
    + [エンジンの標準動作の変更](interaction/using/hooks.md)
    + [分散アーキテクチャ](interaction/using/distributed-architectures.md)
    + [データバッファーの設定](installation/using/interaction-data-buffer.md)
  + ユースケース {#case-study}
    + [プレゼンテーションルール](interaction/using/presentation-rules.md)
    + [インバウンドチャネルのオファー](interaction/using/offers-on-an-inbound-channel.md)
    + [アウトバウンドチャネルのオファー](interaction/using/offers-on-an-outbound-channel.md)
+ トランザクションメッセージ {#transactional-messaging}
  + [トランザクションメッセージの基本を学ぶ](message-center/using/about-transactional-messaging.md)
  + トランザクションメッセージの設定 {#configure-transactional-messaging}
    + [トランザクションメッセージのアーキテクチャ](message-center/using/transactional-messaging-architecture.md)
    + [インスタンスの設定](message-center/using/configuring-instances.md)
    + [その他の設定](message-center/using/additional-configurations.md)
  + メッセージテンプレート {#message-templates}
    + [メッセージテンプレートをテスト](message-center/using/testing-message-templates.md)
  + [ユースケース](message-center/using/transactional-email-with-attachments.md)
+ ソーシャルメディアとの統合 {#integrating-with-social-media}
  + [ソーシャルマーケティングについて](social/using/about-social-marketing.md)
+ インストールおよび設定ガイド {#installing-campaign-classic}
  + アーキテクチャの原則 {#architecture-and-hosting-models}
    + [一般的なアーキテクチャ](installation/using/general-architecture.md)
    + ホスティングモデル{#hosting-models-lp}
      + [Campaign ホスティングモデル](installation/using/hosting-models.md)
      + [機能マトリックス](installation/using/capability-matrix.md)
  + デプロイメントタイプ {#deployment-types}
    + [デプロイメントタイプについて](installation/using/about-deployment-types.md)
    + [スタンドアロンデプロイメント](installation/using/standalone-deployment.md)
    + [標準デプロイメント](installation/using/standard-deployment.md)
    + [企業へのデプロイメント](installation/using/enterprise-deployment.md)
    + [ミッドソーシングへのデプロイメント](installation/using/mid-sourcing-deployment.md)
    + [パワーブースターとパワークラスター](installation/using/power-booster-and-power-cluster.md)
  + セキュリティとプライバシーの設定 {#security-privacy}
    + [セキュリティとプライバシーのチェックリスト](installation/using/get-started-security-privacy.md)
    + [パーソナライゼーションとプライバシー](installation/using/privacy.md)
    + [安全なアクセス管理](installation/using/access-management.md)
    + [スクリプトとコーディングのガイドライン](installation/using/scripting-coding-guidelines.md)
    + [ネットワーク、データベース、SSL/TLS](installation/using/network-database.md)
    + [サーバーのセキュリティ設定](installation/using/server-configuration.md)
    + [Web サーバーのセキュリティ設定](installation/using/web-server-configuration.md)
  + Campaign のインストール（オンプレミス）{#install-campaign-on-prem}
    + デプロイメントのガイドライン {#deployment-guidelines}
      + [データベースサーバー](installation/using/database.md)
      + [アプリケーションサーバー](installation/using/application-server.md)
      + [メッセージサーバー](installation/using/messaging-server.md)
      + [ネットワーク設定](installation/using/network-configuration.md)
    + Campaign Windows 版 {#installing-campaign-in-windows}
      + [はじめに](installation/using/prerequisites-of-campaign-installation-in-windows.md)
      + [サーバーのインストール](installation/using/installing-the-server.md)
      + [Web サーバーへの統合（Windows）](installation/using/integration-into-a-web-server-for-windows.md)
      + [Windows でのクライアントコンソールの可用性](installation/using/client-console-availability-for-windows.md)
    + Campaign Linux 版 {#installing-campaign-in-linux}
      + [前提条件](installation/using/prerequisites-of-campaign-installation-in-linux.md)
      + [パッケージのインストール](installation/using/installing-packages-with-linux.md)
      + [Web サーバーへの統合](installation/using/integration-into-a-web-server-for-linux.md)
    + [タイムゾーン管理](installation/using/time-zone-management.md)
    + [ミッドソーシングサーバーのインストール](installation/using/mid-sourcing-server.md)
    + Campaign のデプロイ（オンプレミス） {#initial-configuration}
      + [主な手順](installation/using/about-initial-configuration.md)
      + [インスタンスの作成とログオン](installation/using/creating-an-instance-and-logging-on.md)
      + [データベースの作成と設定](installation/using/creating-and-configuring-the-database.md)
      + [インスタンスのデプロイ](installation/using/deploying-an-instance.md)
      + [ビルトインパッケージのインストール](installation/using/installing-campaign-standard-packages.md)
  + Campaign の設定 {#additional-configurations}
    + [Campaign サーバーの設定](installation/using/configuring-campaign-server.md)
    + [セキュリティゾーンの定義](installation/using/security-zones.md)
    + [URL 権限の設定](installation/using/url-permissions.md)
    + [ファイルとリソース](installation/using/file-res-management.md)
    + [Tomcat の設定](installation/using/configure-tomcat.md)
    + [配信設定の指定](installation/using/configure-delivery-settings.md)
    + [技術的なメール設定](installation/using/email-deliverability.md)
    + {hide-from-toc}[Campaign での MX サーバーの使用](installation/using/using-mx-servers.md)
    + [メール BCC の設定](installation/using/email-archiving.md)
    + [SpamAssassin の設定](installation/using/configuring-spamassassin.md)
  + Campaign への接続{#connect-to-campaign}
    + [クライアントコンソールのインストール](installation/using/installing-the-client-console.md)
    + Adobe ID を使用した接続 {#connecting-via-an-adobe-id}
      + [ [!DNL Adobe ID] について](integrations/using/about-adobe-id.md)
      + [Adobe [!DNL IMS] の設定](integrations/using/configuring-ims.md)
      + [Adobe [!DNL IMS] の実装](integrations/using/implementing-ims.md)
      + [IMS のトラブルシューティング](integrations/using/ims-troubleshooting.md)
    + [LDAP 経由の接続](installation/using/connecting-through-ldap.md)
  + Campaign を外部システムに接続 {#accessing-external-database}
    + [外部アカウントの設定](installation/using/external-accounts.md)
    + Federated Data Access の設定{#configure-fda}
      + [Federated Data Access の概要](installation/using/about-fda.md)
      + [ベストプラクティスと制限事項](installation/using/fda-best-practices.md)
      + 設定のガイドライン {#config-databases}
        + [設定の手順](installation/using/configure-fda.md)
        + [Amazon Redshift の設定](installation/using/configure-fda-redshift.md)
        + [Azure Synapse の設定](installation/using/configure-fda-synapse.md)
        + [Google BigQuery の設定](installation/using/configure-fda-google-big-query.md)
        + [Hadoop の設定](installation/using/configure-fda-hadoop.md)
        + [Microsoft SQL Server の設定](installation/using/configure-fda-sql.md)
        + [Netezza の設定](installation/using/configure-fda-netezza.md)
        + [Oracle の設定](installation/using/configure-fda-oracle.md)
        + [PostgreSQL の設定](installation/using/configure-fda-postgresql.md)
        + [SAP HANA の設定](installation/using/configure-fda-sap-hana.md)
        + [Snowflake の設定](installation/using/configure-fda-snowflake.md)
        + [Sybase IQ の設定](installation/using/configure-fda-sybase.md)
        + [Teradata の設定](installation/using/configure-fda-teradata.md)
        + [Vertica Analytics の設定](installation/using/configure-fda-vertica.md)
    + [リモートアクセス権](installation/using/remote-database-access-rights.md)
    + [データベースへの接続](installation/using/connecting-to-database.md)
    + [データスキーマの作成](installation/using/creating-data-schema.md)
    + [データマッピングの定義](installation/using/defining-data-mapping.md)
  + 付録 {#appendices}
    + [サーバー設定ファイル](installation/using/the-server-configuration-file.md)
    + [Campaign ネットワークエンドポイント](installation/using/campaign-network-endpoints.md)
    + [コマンドライン](installation/using/command-lines.md)
    + [インスタンスの新規作成](installation/using/creating-new-instances.md)
    + [Campaign オプションの一覧](installation/using/configuring-campaign-options.md)
    + {hide-from-toc}[Campaign のアンインストール](installation/using/uninstalling-campaign.md)
    + [新しいフォントのインストール](installation/using/install-fonts.md)
+ 監視ガイド {#monitoring-campaign-classic}
  + はじめに {#introduction}
    + [前書き](production/using/foreword.md)
    + [一般的なアーキテクチャ](production/using/general-architecture.md)
    + [監視のガイドライン](production/using/monitoring-guidelines.md)
  + 本番の手順 {#production-procedures}
    + [設定の原則](production/using/configuration-principle.md)
    + [動作の原則](production/using/operating-principle.md)
    + [管理](production/using/administration.md)
    + [設定](production/using/configuration.md)
    + [ログファイル](production/using/log-files.md)
    + [プロセスの監視](production/using/monitoring-processes.md)
    + [通常のコマンド](production/using/usual-commands.md)
    + [監査記録](production/using/audit-trail.md)
  + データ処理 {#data-processing}
    + [バックアップ](production/using/backup.md)
    + [復元](production/using/restoration.md)
    + [環境の複製](production/using/duplicating-environments.md)
    + [データベースクリーンアップのワークフロー](production/using/database-cleanup-workflow.md)
  + Adobe Campaign の更新 {#updating-adobe-campaign}
    + [はじめに](production/using/introduction.md)
    + [ビルドアップグレードの実行](production/using/build-upgrade.md)
    + [アップグレード手順（オンプレミス）](production/using/upgrading.md)
    + [Unicode への切り替え](production/using/switching-to-unicode.md)
    + {hide-from-toc}[移行手順](production/using/migration-procedures.md)
  + データベースのメンテナンス {#database-maintenance}
    + [レコメンデーション](production/using/recommendations.md)
    + [維持するテーブル](production/using/tables-to-maintain.md)
    + [メンテナンスのタイプ](production/using/types-of-maintenance.md)
    + [RDBMS 固有のレコメンデーション](production/using/rdbms-specific-recommendations.md)
    + [アプリケーションオブジェクト](production/using/application-objects.md)
  + トラブルシューティング {#troubleshooting-toc}
    + [本番のトラブルシューティングの概要](production/using/troubleshooting.md)
    + よくある問題と一般的な問題 {#common-general-issues-toc}
      + [モジュールおよびよくある問題](production/using/modules-and-frequent-issues.md)
      + [ワークフローの実行](production/using/workflow-execution.md)
      + [パスワードを忘れた場合](production/using/lost-password.md)
      + [コンソールの更新](production/using/console-update.md)
    + 配信のトラブルシューティング {#delivery-troubleshooting-toc}
      + [パフォーマンスとスループットの問題](production/using/performance-and-throughput-issues.md)
      + [画像の表示の問題](production/using/image-display-issues.md)
      + [画像が見つからない](production/using/images-missing.md)
      + [一時ファイル](production/using/temporary-files.md)
    + ログの操作 {#working-with-log-toc}
      + [ログの精度](production/using/log-precision.md)
      + [トラッキングログの問題](production/using/tracking-logs-issues.md)
    + データベースの問題 {#database-issues-toc}
      + [データベースのパフォーマンス](production/using/database-performances.md)
      + [Oracle データベースのエンコード](production/using/encoding-of-the-oracle-database.md)
    + 接続の向上 {#connection-improvements-toc}
      + [接続の失敗](production/using/failure-to-connect.md)
      + [接続のしきい値](production/using/connection-thresholds.md)
    + 技術的なトラブルシューティング {#technical-troubleshooting-toc}
      + [Linux でのスタックトレース](production/using/stack-trace-in-linux.md)
      + [JSP の動作](production/using/jsp-behavior.md)
      + [Tomcat バージョンの検索](production/using/locate-tomcat-version.md)
+ 開発者ガイド {#configuring-campaign-classic}
  + [データパッケージ](platform/using/working-with-data-packages.md)
  + データモデル {#data-model}
    + [データモデルの説明](configuration/using/data-model-description.md)
    + [ベストプラクティス](configuration/using/data-model-best-practices.md)
  + スキーマの操作 {#schema-reference}
    + [スキーマの基本を学ぶ](configuration/using/about-schema-reference.md)
    + [スキーマの構造](configuration/using/schema-structure.md)
    + [データベースマッピング](configuration/using/database-mapping.md)
    + [鍵の管理](configuration/using/database-keys.md)
    + 要素と属性 {#elements-attributes}
      + [はじめに](configuration/using/schema-introduction.md)
      + [属性](configuration/using/schema/attribute.md)
      + [文字列を計算](configuration/using/schema/compute-string.md)
      + [条件](configuration/using/schema/condition.md)
      + [DB インデックス](configuration/using/schema/db-index.md)
      + [要素](configuration/using/schema/element.md)
      + [定義済みリスト](configuration/using/schema/enumeration.md)
      + [ヘルプ](configuration/using/schema/help.md)
      + [結合](configuration/using/schema/join.md)
      + [キー](configuration/using/schema/key.md)
      + [キーフィールド](configuration/using/schema/keyfield.md)
      + [メソッド](configuration/using/schema/method.md)
      + [メソッド](configuration/using/schema/methods.md)
      + [Param](configuration/using/schema/param.md)
      + [パラメーター](configuration/using/schema/parameters.md)
      + [SrcSchema](configuration/using/schema/srcschema.md)
      + [Sysfilter](configuration/using/schema/sysfilter.md)
      + [値](configuration/using/schema/value.md)
  + スキーマの編集 {#editing-schemas}
    + [既存のテーブルのスキーマ](configuration/using/schema-of-an-existing-table.md)
    + [スキーマの拡張](configuration/using/extending-a-schema.md)
    + [データベース構造の更新](configuration/using/updating-the-database-structure.md)
    + [新しいフィールドアシスタント](configuration/using/new-field-wizard.md)
    + [データスキーマの構造](configuration/using/structure-of-a-data-schema.md)
    + [スキーマの再生成](configuration/using/regenerating-schemas.md)
    + [スキーマエディションの例](configuration/using/examples-of-schemas-edition.md)
  + 入力フォーム {#input-forms}
    + [フォームを編集](configuration/using/editing-forms.md)
  + API {#api}
    + [Web サービスについて](configuration/using/about-web-services.md)
    + [Web サービスの呼び出し](configuration/using/web-service-calls.md)
    + [データ指向の API](configuration/using/data-oriented-apis.md)
    + [ビジネス指向の API](configuration/using/business-oriented-apis.md)
    + [SOAP メソッドの実装](configuration/using/implementing-soap-methods.md)
    + [JavaScript での SOAP メソッド](configuration/using/soap-methods-in-javascript.md)
    + [SQL 関数の追加](configuration/using/adding-additional-sql-functions.md)
  + ナビゲーション階層 {#navigation-hierarchy}
    + [エクスプローラー階層の設定](configuration/using/configuration.md)
    + [エクスプローラー階層の編集](configuration/using/edition.md)
  + カスタム受信者テーブルの使用 {#use-a-custom-recipient-table}
    + [カスタム受信者テーブルについて](configuration/using/about-custom-recipient-table.md)
    + [スキーマの特性](configuration/using/schema-characteristics.md)
    + [ターゲットマッピング](configuration/using/target-mapping.md)
    + [インターフェイスの設定](configuration/using/configuring-the-interface.md)
    + [シードアドレス](configuration/using/seed-addresses.md)
    + [フィルターの作成](configuration/using/creating-filters.md)
    + [ワークフローを使用したプロファイルリストの作成](configuration/using/creating-a-profile-list-with-a-workflow.md)
    + [ワークフローの管理](configuration/using/managing-workflows.md)
    + [レポートの管理](configuration/using/managing-reports.md)
  + Web トラッキングの設定 {#setting-up-web-tracking}
    + [Web トラッキングについて](configuration/using/about-web-tracking.md)
    + [Web トラッキングモード](configuration/using/web-tracking-mode.md)
    + [Web トラッキングタグ：定義](configuration/using/web-tracking-tag-definition.md)
    + [ステージの設定](configuration/using/setup-stages.md)
    + [追加パラメーター](configuration/using/additional-parameters.md)
    + [Web トラッキングタグの作成](configuration/using/creating-web-tracking-tags.md)
    + [サイトへのタグの挿入](configuration/using/inserting-tags-in-your-site.md)
    + [すべての訪問の収集](configuration/using/collecting-all-visits.md)
    + [匿名トラッキング](configuration/using/anonymous-tracking.md)
+ 移行ガイド {#migrating-to-a-new-version}
  + {hide-from-toc}[Adobe Campaign v7 に移行](migration/using/about-migration.md)
  + 移行手順 {#migration-procedure}
    + {hide-from-toc}[前提条件](migration/using/before-starting-migration.md)
    + {hide-from-toc}[移行テストについて](migration/using/testing-the-migration.md)
    + {hide-from-toc}[設定の適応](migration/using/configuring-your-platform.md)
  + 移行の開始 {#migrating-to-adobe-campaign-7}
    + {hide-from-toc}[Microsoft Windows プラットフォームの移行](migration/using/migrating-in-windows-for-adobe-campaign-7.md)
    + {hide-from-toc}[Linux プラットフォームの移行](migration/using/migrating-in-linux-for-adobe-campaign-v7.md)
  + {hide-from-toc}[ロールバック手順](migration/using/about-rollback.md)
+ テクニカルノート {#technotes}
  + [ハードウェアサイズについてのレコメンデーション](technotes/using/hardware-sizing.md)
  + [Enhanced MTA を使用した送信](delivery/using/sending-with-enhanced-mta.md)
  + [ミッドソーシングインフラストラクチャに対する「インバウンド SMS」ワークフローアクティビティ](technotes/using/inbound-sms-wf.md)
  + IMS へのアップグレード{#ims}
    + [Adobe IMS への移行](technotes/using/ac-ims.md)
    + [ユーザーを IMS へ移行](technotes/using/migrate-users-to-ims.md)
    + [テクニカルオペレーターを Developer Console へ移行](technotes/using/ims-migration.md)
    + [IMS 移行後のインターフェイスへの影響](technotes/using/impact-ims-migration.md)
  + アップグレードと互換性{#technote-migration}
    + [Microsoft Edge Chromium の有効化](technotes/using/edge-chromium.md)
    + {hide-from-toc}[新しい配信サーバー](technotes/using/deliverability-server.md)
    + {hide-from-toc}[Apache セキュリティアップグレード](technotes/using/acc-apache-upgrade.md)
    + {hide-from-toc}[2023 年のシステムアップグレード](technotes/using/tech-stack-upgrade.md)
    + {hide-from-toc}[IMS の更新](technotes/using/ims-updates.md)
    + {hide-from-toc}[Adobe Analytics 2.0 API への移行](technotes/using/analytics-2-migration.md)
  + メールとプッシュ通知{#technotes-email}
    + [Apple iOS のメールプライバシー保護](technotes/using/apple-mail-app-privacy-protection.md)
    + [iOS 証明書の更新](technotes/using/ios-certificate-update.md)
    + {hide-from-toc}[トラッキング対象 URL の更新](technotes/using/tracked-urls.md)
  + Adobe Managed Services への移行{#dc-migration}
    + [パブリッククラウドへの移行](technotes/using/dc-migration.md)
    + [FAQ](technotes/using/dc-migration-faq.md)
  + [GCM ベースの関数](technotes/using/gcm-functions.md)
+ [Campaign コントロールパネル](https://experienceleague.adobe.com/docs/control-panel/using/control-panel-home.html?lang=ja)
