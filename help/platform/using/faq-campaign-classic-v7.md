---
product: campaign
title: Campaign Classic に関する FAQ
description: Adobe Campaign Classic v7 のアーキテクチャ、デプロイメント、機能に固有の質問
feature: Overview, Troubleshooting
audience: platform
content-type: reference
topic-tags: starting-with-adobe-campaign
source-git-commit: 295e3596d9291cbcc55e2d264309141526c3806b
workflow-type: ht
source-wordcount: '1535'
ht-degree: 100%

---

# Campaign Classic v7 に関する FAQ {#campaign-classic-v7-faq}

この FAQ では、Adobe Campaign Classic v7 のアーキテクチャ、デプロイメントモデル、v7 固有の機能に関する質問について説明します。

**Campaign のよくある質問**（ワークフロー、配信、オーディエンス、レポート、パーソナライゼーションなど）への包括的な回答については、トピック別に詳細な回答が記載されている [**Campaign v8 に関する包括的な FAQ**](https://experienceleague.adobe.com/docs/campaign/campaign-v8/start/campaign-faq-comprehensive.html?lang=ja){target="_blank"} を参照してください。

## Campaign Classic v7 のアーキテクチャとデプロイメント {#v7-architecture}

### Campaign Classic v7 で使用できるホスティングモデルは何ですか？ {#what-are-the-hosting-models-available-in-campaign-classic-v7}

Adobe Campaign Classic v7 には、次の 3 つのデプロイメントモデルがあります。

* **ホスト（Managed Services）** - Adobe インフラストラクチャ上でアドビで完全に管理されます
* **オンプレミス** - 独自のインフラストラクチャ上でインストールおよび管理されます
* **ハイブリッド** - クラウドとオンプレミスのコンポーネントを組み合わせたミッドソーシングアーキテクチャ

各デプロイメントモデルには、異なる機能と管理責任があります。モジュール、オプション、設定の可用性は、デプロイメントタイプによって異なります。

ホスティングモデルとその違いについて[詳しくは、こちらをクリックしてください](../../installation/using/hosting-models.md)。

**メモ：** Campaign v8 は、Managed Cloud Services としてのみ利用可能です。[Campaign v8 の詳細情報](https://experienceleague.adobe.com/docs/campaign/campaign-v8/new/whats-new.html?lang=ja){target="_blank"}。

### オンプレミス環境とホスト環境では作業する際にどのような違いがありますか？ {#what-are-the-differences-when-working-on-premise-vs-in-a-hosted-environment}

Adobe Campaign Classic v7 には一連のモジュールとオプションが付属しています。これらのモジュールの可用性とその設定は、インストールの[デプロイメントタイプ](../../installation/using/hosting-models.md)（ホスト（Managed Services）、ハイブリッド、オンプレミス）によって異なります。

主な違い：

* **オンプレミス** - インストール、インフラストラクチャ、設定を完全に制御します。メンテナンス、アップグレード、セキュリティには、内部 IT リソースが必要です。
* **ホスト／Managed Services** - インフラストラクチャとメンテナンスはアドビで管理されます。自動アップグレードが実行され、セキュリティが強化されています。サーバーへの直接アクセスは制限されています。
* **ハイブリッド** - 両方のモデルのメリットを組み合わせます。マーケティングインスタンスはアドビでホストされ、実行／ミッドソーシングは個別に管理されます。

[完全な機能マトリックスについて詳しくは、こちらをクリックしてください](../../installation/using/capability-matrix.md)。

### オンプレミス／ハイブリッドから Adobe Managed Services に移行するにはどうすればよいですか？ {#how-do-i-migrate-from-on-premise-hybrid-to-adobe-managed-services}

Adobe Managed Services への移行により、スケーラビリティとセキュリティが向上し、IT オーバーヘッドが削減されます。多くの場合、これは Campaign v8 に移行する前の足がかりとなります。

**主なポイント：**

* 自動移行ツールは使用できません。手動での計画と実行が必要です
* Adobe Professional Services サポートを強くお勧めします
* メリットには、クラウドインフラストラクチャー、自動セキュリティパッチ、エキスパートによるサポート、v8 への簡単なパスが含まれます
* 移行には、デューデリジェンス、環境監査、データクリーンアップ、ステージ移行、実稼動環境へのカットオーバーが含まれます

**はじめに：**&#x200B;アドビ担当者に連絡して環境を評価し、Adobe Professional Services で詳細な移行プランを作成してください。

詳しくは、[Managed Services への移行](https://experienceleaguecommunities.adobe.com/t5/adobe-campaign-classic-blogs/migrate-your-adobe-campaign-v7-onprem-hybrid-environment-to/ba-p/681605){target="_blank"}を参照してください。

## ビルドのアップグレード（Campaign Classic v7） {#build-upgrades-v7}

### Campaign Classic v7 のビルドのアップグレードとは何ですか？ {#what-is-a-build-upgrade-v7}

ビルドのアップグレードとは、Adobe Campaign Classic v7 ソフトウェアが、メジャー／マイナーのビルドレベルは変わらないまま、最新の安全なビルド番号に更新されることを指します。例：Campaign Classic v7 ビルド 9026 から Campaign v7 ビルド 9032。

Adobe Campaign は定期的にアップデートされています。マイナーバージョンは、新機能、改善および修正が加えられ、リリースされています。さらに、累積的な修正のみを含むビルドが定期的にリリースされています。

詳しくは、[この節](../../rn/using/rn-overview.md)を参照してください。

### Campaign Classic v7 を最新バージョンにアップグレードするにはどうすればよいですか？ {#how-can-i-upgrade-campaign-classic-v7}

Adobe Campaign Classic では、優れた価値提供のため、様々なテクノロジーを使用しています。こうしたテクノロジーによる優れたセキュリティ、安定性、パフォーマンスを実現するには、Campaign Classic v7 インスタンスを定期的にアップグレードして、常に最新バージョンを使用する必要があります。

**ホスト環境のお客様の場合：** Campaign の年次アップグレードで、最新の安定したバージョンを自動的に利用できます。アドビがアップグレードプロセスを管理し、お客様とタイミングを調整します。

**オンプレミス／ハイブリッド環境のお客様の場合：**&#x200B;アップグレードを実行するのはお客様の責任となります。アドビでは、1 年に 1 回以上はアップグレードすることを強くお勧めします。

環境の更新方法について詳しくは、[この節](../../production/using/build-upgrade.md)を参照してください。また、このトピックに関する質問について詳しくは、[ビルドのアップグレードに関する FAQ](../../platform/using/faq-build-upgrade.md) を参照してください。

### Adobe Campaign Classic v7 の最新バージョンは何ですか？ {#what-is-the-latest-version-v7}

Campaign Classic v7 の最新バージョン（新機能およびドキュメントを含む）については、最新の[リリースノート](../../rn/using/latest-release.md)に詳細が記載されています。

### 実行している Campaign Classic v7 のバージョンを確認するにはどうすればよいですか？ {#how-do-i-know-which-version-v7}

Adobe Campaign クライアントコンソールの&#x200B;**[!UICONTROL ヘルプ／バージョン情報...]** メニューで、お使いのバージョンおよびビルド番号を確認できます。「**[!UICONTROL バージョン情報]**」ボックスには、コンソールとサーバーの両方で実行しているバージョンとビルドに関する詳細情報が含まれています。

詳しくは、[この節](../../platform/using/launching-adobe-campaign.md#getting-your-campaign-version)を参照してください。

### ビルドのアップグレードは、バージョンのアップグレードと同じですか？ {#is-build-upgrade-same-as-version-upgrade}

いいえ。ビルドのアップグレードは、特定のメジャーバージョン内での増分アップデートです。バージョンのアップグレードは、あるメジャーバージョンから別のメジャーバージョンへの変更です。ビルドのアップグレードは簡単で、通常はアーキテクチャ、技術、データモデルの大きな変更は含まれません。

バージョンのアップグレード（例：v7 から v8）には通常、大幅な技術的変更が伴い、カスタマイズに応じて設定の変更や部分的な再実装が必要になる場合があります。

## Campaign Classic v7 の設定 {#v7-configuration}

### Campaign Classic v7 インターフェイスの言語を変更できますか？ {#can-i-change-language-v7}

Campaign Classic v7 の言語はインスタンスを作成する際に選択します。**後から変更することはできません。**

Adobe Campaign v7 のユーザーインターフェイスは、英語、フランス語、ドイツ語、日本語の 4 つの言語で利用できます。クライアントコンソールとサーバーは同一言語で設定する必要があります。Campaign Classic v7 インスタンスはそれぞれ、1 つの言語でしか実行できません。

英語であれば、Campaign v7 をインストールする際に米国英語か英国英語を選べます（それぞれ日時の書式設定が異なります）。

[詳しくは、この節を参照してください](../../installation/using/creating-an-instance-and-logging-on.md)。

**メモ：** Campaign v8 web UI では、ユーザーがインターフェイス言語を独自に変更できます。[詳細情報](https://experienceleague.adobe.com/docs/campaign/campaign-v8/start/connect.html?lang=ja#language-pref){target="_blank"}。

### Campaign Classic v7 でセキュリティゾーンを設定するにはどうすればよいですか？ {#how-can-i-configure-security-zones-v7}

セキュリティゾーンのセルフサービスインターフェイスを使用すると、Adobe Campaign Classic v7 デプロイメントの VPN セキュリティゾーン設定にあるエントリを管理できます。これは、主にオンプレミスおよびハイブリッドのデプロイメントに関連します。

Campaign v7 のセキュリティゾーンについて詳しくは、[この節](../../installation/using/security-zones.md)を参照してください。

セキュリティゾーンのセルフサービス UI について[詳しくは、こちらをクリックしてください](https://helpx.adobe.com/jp/campaign/kb/configuring-security-zones-self-service.html){target="_blank"}。

**メモ：**&#x200B;ホスト環境／Managed Services のお客様がセキュリティゾーンを設定するには、アドビに連絡する必要があります。

### Adobe Campaign Classic v7 は LDAP と統合できますか？ {#can-campaign-classic-integrate-with-ldap}

はい。**オンプレミス／ハイブリッド環境のお客様**&#x200B;は、Campaign Classic v7 を LDAP ディレクトリと統合して、認証とユーザー管理を一元化できます。

この統合により、以下が可能になります。

* 企業の LDAP ディレクトリに対する認証
* ユーザーと権限の一元管理
* ユーザーグループと権限の自動同期
* シングルサインオン機能

Campaign Classic v7 で LDAP 統合を設定する[方法について詳しくは、こちらをクリックしてください](../../installation/using/connecting-through-ldap.md)。

**メモ：** LDAP 統合は、オンプレミスおよびハイブリッドのデプロイメントで使用できます。ホスト環境のお客様は、認証に Adobe IMS を使用します。

### オンプレミスデプロイメントでのセキュリティのベストプラクティスは何ですか？ {#security-best-practices-on-premise}

オンプレミスおよびハイブリッドのデプロイメントでは、ホスト環境と比較して、追加のセキュリティ設定と堅牢化が必要です。

**主なセキュリティ領域：**

* ネットワークセキュリティとファイアウォールの設定
* データベースアクセスとセキュリティ
* オペレーティングシステムの堅牢化
* ファイル権限とアクセス制御
* セキュリティゾーンの設定
* 暗号化（保存時および転送中のデータ）
* ユーザーアクセス管理
* 定期的なセキュリティパッチ適用
* 監査ログと監視

オンプレミスデプロイメントのセキュリティ設定と堅牢化に関して確認する主な要素について詳しくは、[セキュリティ設定チェックリスト](https://helpx.adobe.com/jp/campaign/kb/acc-security.html){target="_blank"}を参照してください。

### クライアントコンソールのキャッシュをクリアするにはどうすればよいですか？ {#how-do-i-clear-console-cache}

Campaign クライアントコンソールのキャッシュをクリアすると、多くの一般的な表示および機能の問題が解決されます。キャッシュには、破損したり古くなったりする場合があるローカル設定ファイルが格納されます。

**キャッシュをクリアするタイミング：**

* 新しいブランディング要素が正しく表示されない
* エクスポート／インポート機能に予期せずエラーが発生する
* 設定の変更後にインターフェイス要素が更新されない
* パフォーマンスの問題またはコンソールの応答が遅い
* 新しいクライアントコンソールバージョンにアップグレードした後

**キャッシュをクリアする方法：**

1. **ソフトキャッシュクリア（最初はこちらを試してください）：**
   * Campaign クライアントコンソールを開きます
   * **[!UICONTROL ファイル]**&#x200B;メニューに移動します
   * 「**[!UICONTROL ローカルキャッシュをクリア…]**」を選択します
   * プロンプトが表示されたら、アクションを確認します
   * クライアントコンソールを再起動します

2. **ハードキャッシュクリア（ソフトクリアで問題が解決しない場合）：**
   * 最初にソフトキャッシュクリアを実行します
   * ログアウトして、クライアントコンソールを完全に閉じます
   * 次の場所に移動します。
      * Windows 7／10：`C:\Users\<Username>\AppData\Roaming\Neolane\NL_5\`
      * Windows XP：`C:\Documents and Settings\<Username>\Application Data\Neolane\NL_5\`
   * `nlclient-config-<alphanumerical value>.xml` という名前の XML ファイルと関連フォルダーをすべて削除します
   * **重要：**`nlclient_cnx.xml` ファイルは削除しないでください
   * クライアントコンソールを再起動します

詳しくは、[Campaign クライアントコンソールドキュメント](../../platform/using/launching-adobe-campaign.md)を参照してください。

## ヘルプの取得 {#getting-help}

### Campaign Classic v7 の詳細情報はどこで参照できますか？ {#where-to-find-more-info-v7}

**ドキュメントとリソース：**

* [Campaign Classic v7 ドキュメント](https://experienceleague.adobe.com/docs/campaign-classic/using/campaign-classic-home.html?lang=ja){target="_blank"} - 完全なドキュメント
* [Campaign Classic v7 リリースノート](../../rn/using/latest-release.md) - 最新リリース情報
* [Campaign Classic 互換性マトリックス](../../rn/using/compatibility-matrix.md) - サポートされているシステムとバージョン
* [Campaign Classic チュートリアル](https://experienceleague.adobe.com/docs/campaign-classic-learn/tutorials/overview.html?lang=ja){target="_blank"} - ビデオチュートリアル

**Campaign に関するよくある質問の場合：**

次の項目に関する回答について詳しくは、[**Campaign v8 に関する包括的な FAQ**](https://experienceleague.adobe.com/docs/campaign/campaign-v8/start/campaign-faq-comprehensive.html?lang=ja){target="_blank"} を参照してください。

* Campaign の基本を学ぶ
* プロファイルとオーディエンス
* メッセージのデザインと配信
* ワークフローと自動化
* レポートと分析
* Campaign の設定と指定
* 開発者向けリソース
* プライバシーとコンプライアンス

**コミュニティとサポート：**

* [Campaign コミュニティフォーラム](https://experienceleaguecommunities.adobe.com/t5/adobe-campaign-classic/ct-p/adobe-campaign-classic-community){target="_blank"}
* [アドビサポート](https://helpx.adobe.com/jp/enterprise/admin-guide.html/enterprise/using/support-for-experience-cloud.ug.html){target="_blank"}
* [コントロールパネル（ホスト環境のお客様）](https://experienceleague.adobe.com/docs/control-panel/using/control-panel-home.html?lang=ja){target="_blank"}

### Campaign Classic v7 から Campaign v8 に移行する必要がありますか？ {#should-i-migrate-to-v8}

Campaign v8 は、大規模なキャンペーン、最新の web UI、クラウドネイティブのメリット、長期的なサポートを必要とする組織に最適なアドビの戦略的プラットフォームです。Campaign Classic v7 は、今後数年以内にサポートを終了する予定です。

**次の場合は、Campaign v8 への移行を検討してください。**

* 大量のデータを処理しているか、パフォーマンスに問題が発生している
* IT オーバーヘッドとインフラストラクチャ管理を削減する（v8 は Managed Cloud Services のみ）
* 最新の UI と Adobe Experience Platform の統合が必要
* 自動更新機能を備えた今後の配達確認テクノロジーが必要
* 現在、ホスト環境／Managed Services 上にある（簡単な移行パス）

**重要な考慮事項：**

* Campaign v8 は、Managed Cloud Services としてのみ使用できます（オンプレミス／ハイブリッドオプションなし）
* カスタマイズと統合の移行計画が必要です
* FFDA アーキテクチャはパフォーマンスを向上させますが、ワークフロー／API の調整が必要です

**次の手順：**&#x200B;アドビ担当者に連絡して移行の準備状況を評価し、移行ツールにアクセスしてください。

詳細情報：

* [Campaign v8 の概要](https://experienceleague.adobe.com/docs/campaign/campaign-v8/new/whats-new.html?lang=ja){target="_blank"}
* [Campaign Classic v7 から v8 への移行](https://experienceleague.adobe.com/docs/campaign/campaign-v8/start/v7-to-v8.html?lang=ja){target="_blank"}
* [Campaign v8 に関する包括的な FAQ](https://experienceleague.adobe.com/docs/campaign/campaign-v8/start/campaign-faq-comprehensive.html?lang=ja){target="_blank"}

**ワークフロー、配信、オーディエンス、レポート、パーソナライゼーションなどに関する Campaign のよくある質問への回答について詳しくは**、[Campaign v8 に関する包括的な FAQ](https://experienceleague.adobe.com/docs/campaign/campaign-v8/start/campaign-faq-comprehensive.html?lang=ja){target="_blank"} を参照してください。
