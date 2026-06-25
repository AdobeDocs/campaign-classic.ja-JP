---
product: campaign
title: Campaign Classic に関する FAQ
description: Adobe Campaign Classic v7 のアーキテクチャ、デプロイメント、機能に固有の質問
feature: Overview, Troubleshooting
audience: platform
content-type: reference
topic-tags: starting-with-adobe-campaign
exl-id: 89356b5a-d99c-43d1-892b-5a1d003e76cc
TQID: https://experienceleague.adobe.com/FL-v5m07U-OzscVIiQONAa-RMu323ZpTuBrL29ukMc4
product_v2:
  - id: dfc56824-e8b9-499e-85d4-21aedb507314
feature_v2:
  - id: d5ef99fa-df0c-4153-bf94-105ad0724167
  - id: afa4204e-6d08-4e29-bc35-26aafb656d48
subfeature_v2:
  - id: f529d0bd-1401-4c88-9833-43228cc1d40f
  - id: d6330382-c886-4f7a-a4f7-74e3f36c0d9c
  - id: f5293531-9312-4099-bfa3-9e67df6a8750
  - id: efa38731-2723-4334-8d8b-a778af834835
topic_v2:
  - id: aa2f3246-cb95-4b30-8899-fdf7d73550cc
  - id: c1579802-ddd4-4214-8a91-97b2066abe11
  - id: d095671a-1355-40aa-8b5f-06c33c68080b
  - id: e0eb8757-182f-49f3-94a4-1587d16f5094
  - id: f4e6943a-c91a-4134-a2c7-f4f20cfff2f0
source-git-commit: 38eab6b8da73163e4476e91c0ef73f25c3f57546
workflow-type: ht
source-wordcount: 1522
ht-degree: 100%

---

# Campaign Classic v7 に関する FAQ {#campaign-classic-v7-faq}

>[!NOTE]
>
>この FAQ では、Adobe Campaign Classic v7 のアーキテクチャ、デプロイメントモデル、v7 固有の機能に関する質問について説明します。
>
>**Campaign のよくある質問**（ワークフロー、配信、オーディエンス、レポート、パーソナライゼーションなど）への包括的な回答については、トピック別に詳細な回答が記載されている [**Campaign v8 に関する包括的な FAQ**](https://experienceleague.adobe.com/ja/docs/campaign/campaign-v8/new/campaign-faq-comprehensive){target="_blank"} を参照してください。

## Campaign Classic v7 のアーキテクチャとデプロイメント {#v7-architecture}

Campaign Classic v7 のホスティングモデル、デプロイメントの違い、移行パスに関する回答をご覧ください。これらの質問では、インフラの選択と関連する責任に焦点を当てています。

+++ Campaign Classic v7 で使用できるホスティングモデルは何ですか？{#what-are-the-hosting-models-available-in-campaign-classic-v7}

Adobe Campaign Classic v7 には、次の 3 つのデプロイメントモデルがあります。

* **ホスト（Managed Services）** - Adobe インフラストラクチャ上でアドビで完全に管理されます
* **オンプレミス** - 独自のインフラストラクチャ上でインストールおよび管理されます
* **ハイブリッド** - クラウドとオンプレミスのコンポーネントを組み合わせたミッドソーシングアーキテクチャ

各デプロイメントモデルには、異なる機能と管理責任があります。 モジュール、オプション、設定の可用性は、デプロイメントタイプによって異なります。

ホスティングモデルとその違いについて[詳しくは、こちらをクリックしてください](../../installation/using/hosting-models.md)。

**メモ：** Campaign v8 は、Managed Cloud Services としてのみ利用可能です。 [Campaign v8 の詳細情報](https://experienceleague.adobe.com/docs/campaign/campaign-v8/new/whats-new.html?lang=ja){target="_blank"}。

+++

+++ オンプレミス環境とホスト環境では作業する際にどのような違いがありますか？{#what-are-the-differences-when-working-on-premise-vs-in-a-hosted-environment}

Adobe Campaign Classic v7 には一連のモジュールとオプションが付属しています。 これらのモジュールの可用性とその設定は、インストールの[デプロイメントタイプ](../../installation/using/hosting-models.md)（ホスト（Managed Services）、ハイブリッド、オンプレミス）によって異なります。

主な違い：

* **オンプレミス** - インストール、インフラストラクチャ、設定を完全に制御します。 メンテナンス、アップグレード、セキュリティには、内部 IT リソースが必要です。
* **ホスト／Managed Services** - インフラストラクチャとメンテナンスはアドビで管理されます。 自動アップグレードが実行され、セキュリティが強化されています。 サーバーへの直接アクセスは制限されています。
* **ハイブリッド** - 両方のモデルのメリットを組み合わせます。 マーケティングインスタンスはアドビでホストされ、実行／ミッドソーシングは個別に管理されます。

[完全な機能マトリックスについて詳しくは、こちらをクリックしてください](../../installation/using/capability-matrix.md)。

+++

+++ オンプレミス／ハイブリッドから Adobe Managed Services に移行するにはどうすればよいですか？{#how-do-i-migrate-from-on-premise-hybrid-to-adobe-managed-services}

Adobe Managed Services への移行により、スケーラビリティとセキュリティが向上し、IT オーバーヘッドが削減されます。 多くの場合、これは Campaign v8 に移行する前の足がかりとなります。

**主なポイント：**

* 自動移行ツールは使用できません。手動での計画と実行が必要です
* Adobe Professional Services サポートを強くお勧めします
* メリットには、クラウドインフラストラクチャー、自動セキュリティパッチ、エキスパートによるサポート、v8 への簡単なパスが含まれます
* 移行には、デューデリジェンス、環境監査、データクリーンアップ、ステージ移行、実稼動環境へのカットオーバーが含まれます

**はじめに：**&#x200B;アドビ担当者に連絡して環境を評価し、Adobe Professional Services で詳細な移行プランを作成してください。

詳しくは、[Managed Services への移行](https://experienceleaguecommunities.adobe.com/t5/adobe-campaign-classic-blogs/migrate-your-adobe-campaign-v7-onprem-hybrid-environment-to/ba-p/681605){target="_blank"}を参照してください。

+++

+++ Campaign Classic v7 から Campaign v8 に移行する必要がありますか？{#should-i-migrate-to-v8}

Campaign v8 は、大規模なキャンペーン、最新の web UI、クラウドネイティブのメリット、長期的なサポートを必要とする組織に最適なアドビの戦略的プラットフォームです。 Campaign Classic v7 は、今後数年以内にサポートを終了する予定です。

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

+++

## ビルドのアップグレード（Campaign Classic v7） {#build-upgrades-v7}

ビルドアップグレードのガイダンスと関連する FAQ について詳しくは、[ビルドアップグレードに関する FAQ](faq-build-upgrade.md) および[ビルドアップグレードに関するドキュメント](../../production/using/build-upgrade.md)を参照してください。

## Campaign Classic v7 の設定 {#v7-configuration}

これらの質問では、言語設定からセキュリティの強化に至るまで、Campaign Classic v7 の一般的な設定タスクとポリシーについて説明します。これらを使用して、設定の選択肢と運用手法を検証します。

+++ Campaign Classic v7 インターフェイスの言語を変更できますか？{#can-i-change-language-v7}

Campaign Classic v7 の言語はインスタンスを作成する際に選択します。 **後から変更することはできません。**

Adobe Campaign v7 のユーザーインターフェイスは、英語、フランス語、ドイツ語、日本語の 4 つの言語で利用できます。 クライアントコンソールとサーバーは同一言語で設定する必要があります。 Campaign Classic v7 インスタンスはそれぞれ、1 つの言語でしか実行できません。

英語であれば、Campaign v7 をインストールする際に米国英語か英国英語を選べます（それぞれ日時の書式設定が異なります）。

[詳しくは、この節を参照してください](../../installation/using/creating-an-instance-and-logging-on.md)。

**メモ：** Campaign v8 web UI では、ユーザーがインターフェイス言語を独自に変更できます。 [詳細情報](https://experienceleague.adobe.com/docs/campaign/campaign-v8/start/connect.html?lang=ja#language-pref){target="_blank"}。

+++

+++ Campaign Classic v7 でセキュリティゾーンを設定するにはどうすればよいですか？{#how-can-i-configure-security-zones-v7}

セキュリティゾーンのセルフサービスインターフェイスを使用すると、Adobe Campaign Classic v7 デプロイメントの VPN セキュリティゾーン設定にあるエントリを管理できます。 これは、主にオンプレミスおよびハイブリッドのデプロイメントに関連します。

Campaign v7 のセキュリティゾーンについて詳しくは、[この節](../../installation/using/security-zones.md)を参照してください。

セキュリティゾーンのセルフサービス UI について[詳しくは、こちらをクリックしてください](https://helpx.adobe.com/jp/campaign/kb/configuring-security-zones-self-service.html){target="_blank"}。

**メモ：**&#x200B;ホスト環境／Managed Services のお客様がセキュリティゾーンを設定するには、アドビに連絡する必要があります。

+++

+++ Adobe Campaign Classic v7 は LDAP と統合できますか？{#can-campaign-classic-integrate-with-ldap}

はい。 **オンプレミス／ハイブリッド環境のお客様**&#x200B;は、Campaign Classic v7 を LDAP ディレクトリと統合して、認証とユーザー管理を一元化できます。

この統合により、以下が可能になります。

* 企業の LDAP ディレクトリに対する認証
* ユーザーと権限の一元管理
* ユーザーグループと権限の自動同期
* シングルサインオン機能

Campaign Classic v7 で LDAP 統合を設定する[方法について詳しくは、こちらをクリックしてください](../../installation/using/connecting-through-ldap.md)。

**メモ：** LDAP 統合は、オンプレミスおよびハイブリッドのデプロイメントで使用できます。 ホスト環境のお客様は、認証に Adobe IMS を使用します。

+++

+++ オンプレミスデプロイメントでのセキュリティのベストプラクティスは何ですか？{#security-best-practices-on-premise}

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

+++

+++ クライアントコンソールのキャッシュをクリアするにはどうすればよいですか？{#how-do-i-clear-console-cache}

Campaign クライアントコンソールのキャッシュをクリアすると、多くの一般的な表示および機能の問題が解決されます。 キャッシュには、破損したり古くなったりする場合があるローカル設定ファイルが格納されます。

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

+++

+++ ホスト環境のお客様はどこでインスタンス設定を管理できますか？{#where-to-manage-instance-settings}

[コントロールパネル](https://experienceleague.adobe.com/docs/control-panel/using/control-panel-home.html?lang=ja){target="_blank"}は、Adobe Campaign の製品管理者が各インスタンスの設定を管理し、使用状況を追跡するのに役立ちます。直感的なインターフェイスにより、主要なアセットを監視し、IP 許可リストの更新、SFTP ストレージのモニタリング、鍵の管理などの管理タスクを実行できます。

**主なメリット：**

* カスタマーケアに問い合わせることなく、設定をすばやく変更します。
* 様々なタイミングで様々なビジネスニーズに基づいて設定を行うことができます。
* ニーズごとにアクセス設定を制御することでセキュリティを強化できます。

+++

## ヘルプの取得 {#getting-help}

コミュニティフォーラムやアドビサポートへのリンクなど、Campaign Classic v7 の主要なドキュメント、FAQ およびサポートチャネルについて説明しています。

+++ Campaign Classic v7 のドキュメントはどこで参照できますか？{#where-to-find-more-info-v7}

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

+++

+++ Campaign Classic v7 のコミュニティを探したり、アドビサポートを受けるにはどうすればよいですか？{#where-to-get-support-v7}

**コミュニティとサポート：**

* [Campaign コミュニティフォーラム](https://experienceleaguecommunities.adobe.com/t5/adobe-campaign-classic/ct-p/adobe-campaign-classic-community){target="_blank"}
* [アドビサポート](https://helpx.adobe.com/jp/enterprise/admin-guide.html/enterprise/using/support-for-experience-cloud.ug.html){target="_blank"}

+++
