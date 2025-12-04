---
product: campaign
title: Campaign Classic に関する FAQ
description: Adobe Campaign Classic v7 のアーキテクチャ、デプロイメント、機能に関する質問
feature: Overview, Troubleshooting
audience: platform
content-type: reference
topic-tags: starting-with-adobe-campaign
source-git-commit: 295e3596d9291cbcc55e2d264309141526c3806b
workflow-type: tm+mt
source-wordcount: '1535'
ht-degree: 5%

---

# Campaign Classic v7 に関するよくある質問 {#campaign-classic-v7-faq}

この FAQ は、Adobe Campaign Classic v7 アーキテクチャ、デプロイメントモデル、v7 固有の機能に関する質問に対応しています。

**Campaign に関するよくある質問** ワークフロー、配信、オーディエンス、レポート、パーソナライゼーションなど）に対する包括的な回答については、[**Campaign v8 の包括的な FAQ**](https://experienceleague.adobe.com/docs/campaign/campaign-v8/start/campaign-faq-comprehensive.html){target="_blank"} を参照してください。この FAQ では、トピック別に整理された詳細な回答を提供しています。

## Campaign Classic v7 のアーキテクチャとデプロイメント {#v7-architecture}

### Campaign Classic v7 で使用できるホスティングモデルは何ですか？ {#what-are-the-hosting-models-available-in-campaign-classic-v7}

Adobe Campaign Classic v7 には、次の 3 つのデプロイメントモデルがあります。

* **ホスト（Managed Services）** - Adobe インフラストラクチャ上のAdobeによって完全に管理されます。
* **オンプレミス** – 独自のインフラストラクチャにインストールして管理
* **ハイブリッド** - クラウドコンポーネントとオンプレミスコンポーネントを混在させたミッドソーシングアーキテクチャ

デプロイメントモデルごとに、異なる機能と管理責任があります。 使用できるモジュール、オプション、設定は、デプロイメントのタイプによって異なります。

モデルのホスティングとその違いについて詳しくは [&#x200B; ここをクリック &#x200B;](../../installation/using/hosting-models.md) してください。

**メモ：** Campaign v8 は、Managed Cloud Services としてのみ使用できます。 [Campaign v8 の詳細 &#x200B;](https://experienceleague.adobe.com/docs/campaign/campaign-v8/new/whats-new.html){target="_blank"}。

### オンプレミス環境とホスト環境では作業する際にどのような違いがありますか？ {#what-are-the-differences-when-working-on-premise-vs-in-a-hosted-environment}

Adobe Campaign Classic v7 には、一連のモジュールとオプションが付属しています。 これらのモジュールの可用性と設定は、インストールの [&#x200B; デプロイメントのタイプ &#x200B;](../../installation/using/hosting-models.md) ホスト型（Managed Services）、ハイブリッドまたはオンプレミス）によって異なります。

主な違い：

* **オンプレミス** - インストール、インフラストラクチャ、設定を完全に制御します。 メンテナンス、アップグレード、およびセキュリティに社内の IT リソースが必要です。
* **ホスト型/Managed Services** - Adobeが管理するインフラストラクチャとメンテナンス。 自動アップグレードとセキュリティの強化。 サーバーアクセスの制限。
* **ハイブリッド** – 両方のモデルの利点を組み合わせます。 Adobeでホストされるマーケティングインスタンス。実行/ミッドソーシングは個別に管理されます。

[&#x200B; 機能マトリックス全体については、ここをクリックしてください &#x200B;](../../installation/using/capability-matrix.md)。

### オンプレミス/ハイブリッドからAdobe Managed Servicesに移行するにはどうすればよいですか？ {#how-do-i-migrate-from-on-premise-hybrid-to-adobe-managed-services}

Adobe Managed Servicesへの移行により、スケーラビリティとセキュリティが向上し、IT オーバーヘッドが削減されます。 Campaign v8 への移行は、多くの場合、その第一歩を踏み出すものです。

**ポイント：**

* 自動移行ツールは利用できません。手動の計画と実行が必要です。
* Adobe Professional Services サポートを強くお勧めします
* メリットとしては、クラウドインフラストラクチャ、自動セキュリティパッチ、エキスパートのサポート、v8 への容易な移行などがあります
* 移行には、デューデリジェンス、環境監査、データクリーンアップ、ステージ移行、実稼動のカットオーバーが含まれます

**はじめに：** Adobeの担当者に連絡して環境を評価し、Adobe Professional Servicesで詳細な移行プランを作成してください。

詳しくは、[Managed Servicesへの移行 &#x200B;](https://experienceleaguecommunities.adobe.com/t5/adobe-campaign-classic-blogs/migrate-your-adobe-campaign-v7-onprem-hybrid-environment-to/ba-p/681605){target="_blank"} を参照してください。

## ビルドアップグレード（Campaign Classic v7） {#build-upgrades-v7}

### Campaign Classic v7 のビルドアップグレードとは {#what-is-a-build-upgrade-v7}

ビルドアップグレードとは、Adobe Campaign Classic v7 ソフトウェアを最新のセキュアなビルド番号に更新しても、メジャー/マイナービルドレベルは変わらない場合です。 例：Campaign Classic v7 ビルド 9026 -> Campaign v7 ビルド 9032。

Adobe Campaign は定期的にアップデートされています。マイナーバージョンは、新機能、改善および修正が加えられた状態でリリースされています。 さらに、累積的な修正のみを含むビルドは、定期的にリリースされます。

詳しくは、[この節](../../rn/using/rn-overview.md)を参照してください。

### Campaign Classic v7 を最新版にアップグレードするにはどうすればよいですか？ {#how-can-i-upgrade-campaign-classic-v7}

Adobe Campaign Classicでは、様々なテクノロジーを活用して価値を提供しています。 こうしたテクノロジーによる優れたセキュリティ、安定性、パフォーマンスを実現するには、Campaign Classic v7 インスタンスを定期的にアップグレードして、常に最新版を使用する必要があります。

**ホステッド環境のお客様の場合：** Campaign の年次アップグレードのメリットは自動的に得られ、最新の安定したバージョンが利用できます。 Adobeがアップグレードプロセスを管理し、タイミングを調整します。

**オンプレミス/ハイブリッド環境のお客様の場合：** アップグレードの実行は、お客様が担当します。 Adobeでは、少なくとも年に 1 回はアップグレードすることを強くお勧めします。

[&#x200B; この節 &#x200B;](../../production/using/build-upgrade.md) では、環境の更新方法を説明します。また、この特定のトピックに関する詳細な質問については、[&#x200B; ビルドアップグレードに関する FAQ](../../platform/using/faq-build-upgrade.md) を参照してください。

### Adobe Campaign Classic v7 の最新バージョンとは {#what-is-the-latest-version-v7}

新機能やドキュメントを含む最新のCampaign Classic v7 バージョンについては、最新の [&#x200B; リリースノート &#x200B;](../../rn/using/latest-release.md) を参照してください。

### 実行中のCampaign Classic v7 のバージョンを確認するにはどうすればよいですか？ {#how-do-i-know-which-version-v7}

Adobe Campaign クライアントコンソールの **[!UICONTROL ヘルプ/バージョン情報]** メニューで、お使いのバージョンおよびビルド番号を確認できます。 **[!UICONTROL バージョン情報]** ボックスには、コンソールとサーバーの両方で実行しているバージョンとビルドに関する詳細情報が表示されます。

詳しくは、[この節](../../platform/using/launching-adobe-campaign.md#getting-your-campaign-version)を参照してください。

### ビルドアップグレードとバージョンアップグレードは同じですか？ {#is-build-upgrade-same-as-version-upgrade}

いいえ。ビルドのアップグレードは、特定のメジャーバージョン内での増分アップデートです。バージョンのアップグレードは、あるメジャーバージョンから別のメジャーバージョンへの変更です。ビルドアップグレードは簡単で、通常は、アーキテクチャ、技術、データモデルに大きな変更を加える必要はありません。

バージョンのアップグレード（v7 から v8 など）には通常、重大な技術的変更が伴い、カスタマイズによっては設定の変更または部分的な再実装が必要になる場合があります。

## Campaign Classic v7 の設定 {#v7-configuration}

### Campaign Classic v7 インターフェイスの言語を変更できますか？ {#can-i-change-language-v7}

インスタンスの作成時にはCampaign Classic v7 言語が選択されています。 **後で変更することはできません。**

Adobe Campaign v7 ユーザーインターフェイスは、英語、フランス語、ドイツ語、日本語の 4 つの言語で使用できます。 クライアントコンソールとサーバーには同じ言語を設定する必要があります。 各Campaign Classic v7 インスタンスは、1 つの言語でのみ実行できます。

英語の場合、Campaign v7 をインストールする際は、アメリカ英語またはイギリス英語のいずれかを選択できます。これらは日付と時間の形式が異なります。

[詳しくは、この節を参照してください](../../installation/using/creating-an-instance-and-logging-on.md)。

**メモ：** Campaign v8 web UI では、ユーザーが独自にインターフェイス言語を変更できます。 [詳細情報](https://experienceleague.adobe.com/docs/campaign/campaign-v8/start/connect.html#language-pref){target="_blank"}。

### Campaign Classic v7 でセキュリティゾーンを設定するにはどうすればよいですか？ {#how-can-i-configure-security-zones-v7}

セキュリティゾーンセルフサービスインターフェイスを使用すると、Adobe Campaign Classic v7 デプロイメントの VPN セキュリティゾーン設定のエントリを管理できます。 これは、主にオンプレミスデプロイメントとハイブリッドデプロイメントに関連しています。

Campaign v7 のセキュリティゾーンについては、[&#x200B; この節 &#x200B;](../../installation/using/security-zones.md) を参照してください。

セキュリティゾーンセルフサービス UI について [&#x200B; 詳しくは、](https://helpx.adobe.com/jp/campaign/kb/configuring-security-zones-self-service.html){target="_blank"} ここをクリックしてください。

**メモ：** ホスト環境またはManaged Servicesのお客様がセキュリティゾーンを設定するには、Adobeにお問い合わせください。

### Adobe Campaign Classic v7 を LDAP と統合できますか？ {#can-campaign-classic-integrate-with-ldap}

はい。**オンプレミス/ハイブリッド環境のお客様** は、Campaign Classic v7 を LDAP ディレクトリと統合して、認証とユーザーの一元管理を行うことができます。

この統合により、次のことが可能になります。

* 企業の LDAP ディレクトリに対して認証するユーザー
* ユーザーと権限の一元的な管理
* ユーザーグループと権限の自動同期
* シングルサインオン機能

Campaign Classic v7 で LDAP 統合を設定する方法については [&#x200B; ここをクリック &#x200B;](../../installation/using/connecting-through-ldap.md) してください。

**メモ：** LDAP 統合は、オンプレミスデプロイメントとハイブリッドデプロイメントで使用できます。 ホスト環境のお客様は、認証にAdobe IMSを使用されます。

### オンプレミスデプロイメントのセキュリティのベストプラクティスは何ですか？ {#security-best-practices-on-premise}

オンプレミスデプロイメントとハイブリッドデプロイメントでは、ホスト環境と比較して、追加のセキュリティ設定と堅牢化が必要です。

**重要なセキュリティ領域：**

* ネットワークセキュリティとファイアウォール設定
* データベースへのアクセスとセキュリティ
* オペレーティングシステムの堅牢化
* ファイルの権限とアクセス制御
* セキュリティゾーンの設定
* 暗号化（保存中および転送中のデータ）
* ユーザーアクセス管理
* 定期的なセキュリティパッチ適用
* 監査ログと監視

オンプレミスデプロイメントのセキュリティ設定と強化に関して確認すべき重要な要素については、[&#x200B; セキュリティ設定チェックリスト &#x200B;](https://helpx.adobe.com/jp/campaign/kb/acc-security.html){target="_blank"} を参照してください。

### クライアントコンソールのキャッシュをクリアするにはどうすればよいですか？ {#how-do-i-clear-console-cache}

Campaign クライアントコンソールのキャッシュをクリアすると、表示や機能に関するよくある多くの問題が解決します。 キャッシュには、破損したり古くなったりする可能性のあるローカル設定ファイルが格納されます。

**キャッシュをクリアするタイミング：**

* 新しいブランディング要素が正しく表示されない
* 書き出し/読み込み関数が予期せず失敗する
* 設定の変更後にインターフェイス要素が更新されない
* パフォーマンスの問題またはコンソールの応答が遅い
* 新しいクライアントコンソールバージョンにアップグレードした後

**キャッシュのクリア方法：**

1. **ソフト キャッシュ クリア （最初に試す）:**
   * Campaign クライアントコンソールを開きます
   * **[!UICONTROL ファイル]** メニューに移動
   * 「**[!UICONTROL ローカルキャッシュをクリア…]**」を選択します
   * プロンプトが表示されたらアクションを確認します
   * クライアントコンソールを再起動します

2. **ハードキャッシュの消去（ソフトクリアしても問題が解決しない場合）:**
   * 最初にソフトキャッシュの消去を実行します
   * ログアウトして、クライアントコンソールを完全に閉じます
   * 次の場所に移動します。
      * Windows 7/10: `C:\Users\<Username>\AppData\Roaming\Neolane\NL_5\`
      * Windows XP: `C:\Documents and Settings\<Username>\Application Data\Neolane\NL_5\`
   * `nlclient-config-<alphanumerical value>.xml` という名前の XML ファイルおよび関連するフォルダーをすべて削除
   * **重要：** ファイルを削除 `nlclient_cnx.xml` ない
   * クライアントコンソールの再起動

詳しくは、[Campaign クライアントコンソールのドキュメント &#x200B;](../../platform/using/launching-adobe-campaign.md) を参照してください。

## ヘルプ {#getting-help}

### Campaign Classic v7 の詳細はどこで確認できますか？ {#where-to-find-more-info-v7}

**ドキュメントとリソース：**

* [Campaign Classic v7 ドキュメント &#x200B;](https://experienceleague.adobe.com/docs/campaign-classic/using/campaign-classic-home.html?lang=ja){target="_blank"} – 完全なドキュメント
* [Campaign Classic v7 リリースノート &#x200B;](../../rn/using/latest-release.md) – 最新のリリース情報
* [Campaign Classic互換性マトリックス &#x200B;](../../rn/using/compatibility-matrix.md) - サポートされているシステムおよびバージョン
* [Campaign Classic チュートリアル &#x200B;](https://experienceleague.adobe.com/docs/campaign-classic-learn/tutorials/overview.html?lang=ja){target="_blank"} - ビデオチュートリアル

**Campaign に関するよくある質問の場合：**

詳しい回答については、[**Campaign v8 の包括的な FAQ**](https://experienceleague.adobe.com/docs/campaign/campaign-v8/start/campaign-faq-comprehensive.html){target="_blank"} を参照してください。

* Campaign 使用の手引き
* プロファイルとオーディエンス
* メッセージデザインと配信
* ワークフローと自動処理
* レポートと分析
* キャンペーンの設定と指定
* 開発者向けリソース
* プライバシーとコンプライアンス

**コミュニティとサポート：**

* [Campaign コミュニティフォーラム &#x200B;](https://experienceleaguecommunities.adobe.com/t5/adobe-campaign-classic/ct-p/adobe-campaign-classic-community){target="_blank"}
* [Adobe サポート &#x200B;](https://helpx.adobe.com/jp/enterprise/admin-guide.html/enterprise/using/support-for-experience-cloud.ug.html){target="_blank"}
* [Campaign コントロールパネル（ホストされているお客様） &#x200B;](https://experienceleague.adobe.com/docs/control-panel/using/control-panel-home.html?lang=ja){target="_blank"}

### Campaign Classic v7 から Campaign v8 に移行する必要はありますか？ {#should-i-migrate-to-v8}

Campaign v8 は、Adobeの戦略的プラットフォームで、大量のキャンペーン、最新の web UI、クラウドネイティブのメリット、長期的なサポートを必要とする組織に最適です。 Campaign Classic v7 は、今後数年以内にサポートを終了する予定です。

**次の場合は、Campaign v8 への移行を検討してください。**

* 大量のデータを処理したり、パフォーマンス上の問題に対処したりします
* IT オーバーヘッドとインフラストラクチャ管理を削減したい（v8 は Managed Cloud Services のみ）
* 最新の UI とAdobe Experience Platformの統合が必要
* 自動更新機能を備えた将来性の高いテクノロジーが必要
* 現在ホスト型/Managed Services 上にある（移行パスが容易）

**重要な考慮事項：**

* Campaign v8 は、Managed Cloud Services としてのみ使用できます（オンプレミス/ハイブリッドオプションなし）
* カスタマイズと統合の移行の計画が必要
* FFDA アーキテクチャはパフォーマンスをもたらしますが、いくつかのワークフロー/API 適応が必要です

**次の手順：** Adobe担当者に問い合わせて、移行に対する準備状況を評価し、移行ツールにアクセスします。

詳細情報：

* [Campaign v8 の概要 &#x200B;](https://experienceleague.adobe.com/docs/campaign/campaign-v8/new/whats-new.html){target="_blank"}
* [Campaign Classic v7 から v8 への移行 &#x200B;](https://experienceleague.adobe.com/docs/campaign/campaign-v8/start/v7-to-v8.html){target="_blank"}
* [Campaign v8 の包括的な FAQ](https://experienceleague.adobe.com/docs/campaign/campaign-v8/start/campaign-faq-comprehensive.html){target="_blank"}

**ワークフロー、配信、オーディエンス、レポート、パーソナライゼーションなどに関する Campaign のよくある質問への詳細な回答については** Campaign v8 の包括的な FAQ[&#x200B; を参照してください &#x200B;](https://experienceleague.adobe.com/docs/campaign/campaign-v8/start/campaign-faq-comprehensive.html){target="_blank"}。
