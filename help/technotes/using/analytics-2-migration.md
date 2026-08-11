---
product: campaign
title: Adobe Analytics 2.0 APIへの移行
description: Campaign Classic - Adobe Analytics 2.0 API移行ガイド
feature: Technote, Analytics Integration
hide: true
source-git-commit: 64460d51b002a7821bba9c2998d9ccccab3046ad
workflow-type: tm+mt
source-wordcount: '910'
ht-degree: 2%

---

# Adobe Analytics 2.0 APIへの移行 {#analytics-2-migration}

Adobe Analytics 1.4 APIは[提供終了に達しています](https://developer.adobe.com/analytics-apis/docs/1.4/guides/eol){target="_blank"}。 Campaign インスタンスをAdobe Analyticsにリンクする[Web Analytics コネクタ &#x200B;](../../integrations/using/gs-aa.md)は、これらのAPIに依存しているため、新しいAnalytics 2.0 APIを使用するビルドにアップグレードして統合を実行する必要があります。

>[!CAUTION]
>
>アップグレードすると、コネクタを強化する2つの組み込み技術ワークフロー（[!UICONTROL webAnalyticsSendMetrics]および[!UICONTROL webAnalyticsGetWebEvents]）が再インポートされます（それぞれのワークフローの機能については、[Web分析ワークフローのリファレンス &#x200B;](../../workflow/using/web-analytics.md)を参照）。 これらのワークフロー上で行ったカスタマイズは、再インポートによって上書きされます。 組み込みのワークフローを直接変更することは避けましょう。カスタマイズしたワークフローは別のカスタムワークフローで作成するため、今後のアップグレードで上書きされることはありません。 また、組み込みのAnalytics JavaScript ファイルも更新されます。カスタムワークフローがこれらのファイルを参照している場合、ファイルが壊れて、新しいコードに適応する必要があります。

## 影響の有無 {#are-you-impacted}

インスタンスが次のいずれかに[!UICONTROL Web Analytics]外部アカウントを使用している場合、影響を受けます。

* Adobe Analyticsに指標としてメールキャンペーンの指標と属性を送信する。
* Adobe Analyticsへの分類データの送信。
* リマーケティングフロー（キャンペーン後にコンバージョンしたコンタクトの特定）。
* 初めて設定する予定の[!UICONTROL Web Analytics]外部アカウント。

お客様に最適なツールをご提案します？ 上記のテクニカルワークフローのうち、インスタンスでアクティブなものはどれかを確認し、[!UICONTROL 管理/プラットフォーム/外部アカウント &#x200B;]で[!UICONTROL Web Analytics]外部アカウント設定を確認します（[Web Analytics外部アカウント &#x200B;](../../installation/using/external-accounts.md#web-analytics-external-account)を参照）。

## 移行方法 {#how-to-migrate}

**Adobeでホストされている** インスタンスを使用している場合、Adobeは、アップグレードの一環としてSFTP プロビジョニング、IP許可リスト、キー設定を処理します。新しいビルドが公開されたら、ユースケースを検証する必要があります。

**オンプレミスまたはハイブリッド**&#x200B;のデプロイメントを利用している場合は、次の手順を実行します。

1. [Campaign環境](../../production/using/build-upgrade.md)を、Adobe Analytics 2.0の変更点を含むビルドにアップグレードします。 実行しているビルドは、[!UICONTROL &#x200B; ヘルプ/バージョン情報…]から確認できます（[Campaign バージョンの確認方法](../../platform/using/launching-adobe-campaign.md#getting-your-campaign-version)を参照）。
1. 次のステップはインスタンスによって異なるため、上記のユースケースのうち、どのユースケースがインスタンスに適用されるかを確認します。
1. リマーケティングフローを使用する場合、[!UICONTROL webAnalyticsFindConverted] ワークフローには、Adobe Analytics 2.0とデータを交換するための専用のSFTP チャネルが必要です。 これを次のように設定します。設定しない場合は、次の手順に進みます。
   1. 他の外部SFTP統合に適用するのと同じ[SFTP サーバーのベストプラクティス &#x200B;](../../platform/using/sftp-server-usage.md)に従って、キーベースの認証を使用してインスタンスのSFTP サーバーをプロビジョニングします。 Adobeには、開始に役立つ[&#x200B; サンプル SFTP セットアップ スクリプト &#x200B;](https://experience.adobe.com/#/downloads/content/software-distribution/en/campaign.html?package=/content/software-distribution/en/details.html/content/dam/campaign/public/setup_sftp.zip){target="_blank"}が用意されています。
   1. 新しいビルドで配信されたスクリプトを実行して、そのサーバーの接続の詳細をAdobe Analyticsに登録します。

      ```
      nlserver javascript -instance:<instance_name> -arg:host=<sftp_host_url>#user=<sftp_user> -file <path_to_the_file>/aaremarketingLocation.js
      ```

      例：

      ```
      nlserver javascript -instance:test_mkt_stage2 -arg:host=test-mkt-stage1.campaign.adobe.com#user=test -file ./nl6/datakit/nms/eng/js/aaremarketingLocation.js
      ```

   1. リマーケティングの書き出しは、固定セットのAdobe Analytics IP範囲からのみ開始されるため、SFTP サーバーでAdobeを許可リストに登録します。
      * [現在のAdobe Analytics Data Collection IP アドレス &#x200B;](https://experienceleague.adobe.com/ja/docs/core-services/interface/data-collection/ip-addresses){target="_blank"}を検索し、SFTP サーバーの許可リストに追加します。 FTP ベースのAnalyticsの書き出し（データフィードを含む）は、ロンドン、オレゴン、シンガポールの各地域のIPv4 アドレスからのみ送信されます。
      * [Adobe Analyticsの公開鍵](https://experienceleague.adobe.com/ja/docs/experience-cloud-kcs/kbarticles/ka-18141){target="_blank"}を取得し、SFTP サーバー上の`authorized_keys` ファイルに追加して、Analyticsが認証できるようにします。
1. Campaign エクスプローラーツリーの&#x200B;**[!UICONTROL 管理] > [!UICONTROL &#x200B; プラットフォーム &#x200B;] > [!UICONTROL &#x200B; オプション]**&#x200B;の下の[!UICONTROL xtkOption]でオプションの`longvalue`を`1`に作成または設定して、インスタンスで`FEATUREFLAG_USE_ANALYTICS_20_API`機能フラグを有効にします。 この手順は、上記のどのユースケースが該当するかに関係なく必要です。
1. 古い接続を廃止する前に、インスタンスに適用される各ユースケースを実行して移行を検証します（テストキャンペーンを送信し、指標がAnalyticsに表示されることを確認し、必要に応じてリマーケティングデータを確認します）。

## 新しいWeb Analytics外部アカウントの設定 {#setting-up-a-new-web-analytics-external-account}

インスタンスがAdobe ホスト型かオンプレミス/ハイブリッド型かを問わず、次の条件が適用されます。

既存のアカウントを移行せずに、初めて[!UICONTROL Web Analytics]外部アカウントを設定する場合は、[外部アカウントの設定手順](../../installation/using/external-accounts.md#web-analytics-external-account)と[&#x200B; コネクタの開始ガイド &#x200B;](../../integrations/using/gs-aa.md)に従ってください。

Analytics 2.0では新しい分類処理が導入されるので、外部アカウントがレポートスイートの分類データを取得する前に、Adobe Analyticsで分類セットを作成する必要もあります。 これは新しい手順です。コンバージョン変数と成功イベントを設定した後、Campaignで外部アカウントを設定する前に作成します。

分類セットを作成するには：

1. [!DNL Adobe Analytics]上部のメニューバーから、**[!UICONTROL コンポーネント]** > **[!UICONTROL 分類セット]**&#x200B;を選択し、**[!UICONTROL 新規]**&#x200B;をクリックします。

   ![](assets/analytics-classification-set-menu.png)

1. **[!UICONTROL 新しい分類セットを追加]** ダイアログで、次の操作を行います。

   ![](assets/analytics-classification-set-dialog.png)

   * 分類セットの&#x200B;**[!UICONTROL 名前]**&#x200B;を入力します。
   * **[!UICONTROL Type]**&#x200B;を&#x200B;**[!UICONTROL プライマリ]**&#x200B;に設定します。
   * **[!UICONTROL ジョブ通知]**&#x200B;で、分類セットジョブの成功または失敗に関する通知を受け取るユーザーを選択し、対応する電子メールアドレスを指定します。
   * **[!UICONTROL サブスクリプション]**&#x200B;で、前の手順で内部キャンペーン名として作成したレポートスイートとコンバージョン変数を選択します。

1. 「**[!UICONTROL 保存]**」をクリックします。

この分類セットは、次の手順で外部アカウントを設定すると、Campaignによって自動的に検出されます。 分類セットについて詳しくは、[Adobe Analytics ドキュメント &#x200B;](https://experienceleague.adobe.com/ja/docs/analytics/components/classifications/sets/create-set){target="_blank"}を参照してください。

## お困りですか？ {#need-help}

移行中に問題が発生した場合は、[Adobe カスタマーケア &#x200B;](https://helpx.adobe.com/jp/enterprise/admin-guide.html/enterprise/using/support-for-experience-cloud.ug.html){target="_blank"}にお問い合わせください。
