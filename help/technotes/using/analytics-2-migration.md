---
product: campaign
title: Adobe Analytics 2.0 API への移行
description: Campaign Classic - Adobe Analytics 2.0 API 移行ガイド
feature: Technote, Analytics Integration
hide: true
source-git-commit: 64460d51b002a7821bba9c2998d9ccccab3046ad
workflow-type: ht
source-wordcount: '910'
ht-degree: 100%

---

# Adobe Analytics 2.0 API への移行 {#analytics-2-migration}

Adobe Analytics 1.4 API は[提供が終了](https://developer.adobe.com/analytics-apis/docs/1.4/guides/eol){target="_blank"}する予定です。Campaign インスタンスを Adobe Analytics にリンクする [web 分析コネクタ](../../integrations/using/gs-aa.md)は、これらの API に依存しているので、引き続き統合を実行するには、新しい Analytics 2.0 API を使用するビルドにアップグレードする必要があります。

>[!CAUTION]
>
>アップグレードすると、コネクタを活用する 2 つのビルトインテクニカルワークフロー（[!UICONTROL webAnalyticsSendMetrics] および [!UICONTROL webAnalyticsGetWebEvents]）が再インポートされます（各ワークフローの機能について詳しくは、[Web 分析ワークフローのリファレンス](../../workflow/using/web-analytics.md)を参照してください）。これらのワークフローに対して行ったカスタマイズは、再度インポートすることで上書きされます。これらのビルトインワークフローを直接変更することは回避し、代わりに、カスタマイズは別のカスタムワークフローで作成してください。これにより、今後のアップグレードで上書きされることはありません。また、このアップグレードでは、ビルトイン Analytics JavaScript ファイルも更新されます。カスタムワークフローでこれらのファイルを参照している場合は機能しなくなるので、新しいコードに合わせて適応させる必要があります。

## 影響の有無 {#are-you-impacted}

お使いのインスタンスで [!UICONTROL web 分析]外部アカウントを次のいずれかの目的で使用している場合は、影響を受けます。

* 指標としての Adobe Analytics へのメールキャンペーンの指標と属性の送信。
* Adobe Analytics への分類データの送信。
* リマーケティングフロー（キャンペーン後の変換済み連絡先の特定）。
* 初めて設定する予定の [!UICONTROL web 分析]外部アカウント。

これらが適用されるかどうかが不明な場合上記のテクニカルワークフローのうち、インスタンスでどれがアクティブになっているかを確認し、[!UICONTROL 管理／プラットフォーム／外部アカウント]で [!UICONTROL web 分析]外部アカウントの設定を確認します（[Web 分析外部アカウント](../../installation/using/external-accounts.md#web-analytics-external-account)を参照）。

## 移行方法 {#how-to-migrate}

**アドビがホスト**&#x200B;するインスタンスを使用している場合、アドビでは、アップグレードの一部として SFTP プロビジョニング、IP 許可リストへの登録、キー設定を処理します。ユーザーは、新しいビルドが公開された後にユースケースを検証するだけで済みます。

**オンプレミスまたはハイブリッド**&#x200B;デプロイメントで運用している場合は、次の手順を実行します。

1. Adobe Analytics 2.0 の変更点を含むビルドに [Campaign 環境をアップグレード](../../production/using/build-upgrade.md)します。実行しているビルドは、[!UICONTROL ヘルプ／バージョン情報...] から確認できます（[Campaign バージョンの確認方法](../../platform/using/launching-adobe-campaign.md#getting-your-campaign-version)を参照）。
1. 次の手順はインスタンスによって異なるので、上記のユースケースのうち、どれがお使いのインスタンスに適用されるかを確認します。
1. リマーケティングフローを使用する場合、[!UICONTROL webAnalyticsFindConverted] ワークフローには、Adobe Analytics 2.0 とデータを交換するための専用の SFTP チャネルが必要です。これを次のように設定します。設定しない場合は、次の手順にスキップします。
   1. 他の外部 SFTP 統合に適用するのと同じ [SFTP サーバーベストプラクティス](../../platform/using/sftp-server-usage.md)に従って、キーベースの認証を使用する SFTP サーバーをインスタンス用にプロビジョニングします。アドビには、開始に役立つ[サンプル SFTP 設定スクリプト](https://experience.adobe.com/#/downloads/content/software-distribution/en/campaign.html?package=/content/software-distribution/en/details.html/content/dam/campaign/public/setup_sftp.zip){target="_blank"}が用意されています。
   1. 新しいビルドで配信されたスクリプトを実行して、そのサーバーの接続の詳細を Adobe Analytics に登録します。

      ```
      nlserver javascript -instance:<instance_name> -arg:host=<sftp_host_url>#user=<sftp_user> -file <path_to_the_file>/aaremarketingLocation.js
      ```

      例：

      ```
      nlserver javascript -instance:test_mkt_stage2 -arg:host=test-mkt-stage1.campaign.adobe.com#user=test -file ./nl6/datakit/nms/eng/js/aaremarketingLocation.js
      ```

   1. リマーケティングのエクスポートは固定セットの Adobe IP 範囲からのみ開始されるので、SFTP サーバーで Adobe Analytics を許可リストに登録します。
      * [現在の Adobe Analytics のデータ収集 IP アドレスを検索](https://experienceleague.adobe.com/ja/docs/core-services/interface/data-collection/ip-addresses){target="_blank"}して、SFTP サーバーの許可リストに追加します。FTP ベースの Analytics エクスポート（データフィードを含む）は、ロンドン、オレゴン、シンガポールの各地域の IPv4 アドレスからのみ送信されます。
      * [Adobe Analytics の公開鍵を取得](https://experienceleague.adobe.com/ja/docs/experience-cloud-kcs/kbarticles/ka-18141){target="_blank"}し、Analytics が認証できるように、SFTPサーバー上の `authorized_keys` ファイルに追加します。
1. Campaign エクスプローラーツリーの&#x200B;**[!UICONTROL 管理]／[!UICONTROL プラットフォーム]／[!UICONTROL オプション]**&#x200B;にある [!UICONTROL xtkOption] で、オプションの `longvalue` を `1` に作成または設定して、インスタンスで `FEATUREFLAG_USE_ANALYTICS_20_API` 機能フラグを有効にします。この手順は、上記のどのユースケースが適用されるかに関係なく必要です。
1. 古い接続を廃止する前に、お使いのインスタンスに適用される各ユースケースを実行して、移行を検証します（テストキャンペーンの送信、Analytics への指標の表示の確認および該当する場合はリマーケティングデータを確認します）。

## 新しい web 分析外部アカウントの設定 {#setting-up-a-new-web-analytics-external-account}

インスタンスがアドビによってホストされている場合でも、オンプレミス／ハイブリッドである場合でも、次の条件が適用されます。

既存のアカウントを移行するのではなく、初めて [!UICONTROL web 分析]外部アカウントを設定する場合は、[外部アカウントの設定手順](../../installation/using/external-accounts.md#web-analytics-external-account)および[コネクタの入門ガイド](../../integrations/using/gs-aa.md)に従ってください。

Analytics 2.0 では新しい分類の処理が導入されるので、外部アカウントでレポートスイートの分類データを取得できるようにする前に、Adobe Analytics で分類セットを作成する必要もあります。これは新しい手順です。コンバージョン変数と成功イベントを設定した後、Campaign で外部アカウントを設定する前に作成します。

分類セットを作成するには：

1. [!DNL Adobe Analytics] の上部のメニューバーから、**[!UICONTROL コンポーネント]**／**[!UICONTROL 分類セット]**&#x200B;を選択して、「**[!UICONTROL 新規]**」をクリックします。

   ![](assets/analytics-classification-set-menu.png)

1. **[!UICONTROL 新しい分類セットを追加]**&#x200B;ダイアログで、次の操作を実行します。

   ![](assets/analytics-classification-set-dialog.png)

   * 分類セットの&#x200B;**[!UICONTROL 名前]**&#x200B;を入力します。
   * **[!UICONTROL タイプ]**&#x200B;を&#x200B;**[!UICONTROL プライマリ]**&#x200B;に設定します。
   * **[!UICONTROL ジョブ通知]**&#x200B;で、分類セットジョブの成功または失敗に関する通知を受け取るユーザーを選択し、対応するメールアドレスを指定します。
   * **[!UICONTROL 購読]**&#x200B;で、レポートスイートと、前の手順で内部キャンペーン名用に作成したコンバージョン変数を選択します。

1. 「**[!UICONTROL 保存]**」をクリックします。

この分類セットは、次の手順で外部アカウントを設定すると、Campaign によって自動的に検出されます。分類セットについて詳しくは、[Adobe Analytics ドキュメント](https://experienceleague.adobe.com/ja/docs/analytics/components/classifications/sets/create-set){target="_blank"}を参照してください。

## お困りですか？ {#need-help}

移行中に問題が発生した場合は、[アドビカスタマーケア](https://helpx.adobe.com/jp/enterprise/admin-guide.html/enterprise/using/support-for-experience-cloud.ug.html){target="_blank"}にお問い合わせください。
