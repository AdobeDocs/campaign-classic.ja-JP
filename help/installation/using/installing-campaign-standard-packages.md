---
product: campaign
title: Campaign Classicのビルトインパッケージのインストール
description: Campaign ビルトインパッケージのインストール方法を学ぶ
feature: Installation, Application Settings
badge-v7-prem: label="オンプレミス／ハイブリッドのみ" type="Caution" url="https://experienceleague.adobe.com/docs/campaign-classic/using/installing-campaign-classic/architecture-and-hosting-models/hosting-models-lp/hosting-models.html?lang=ja" tooltip="オンプレミスデプロイメントとハイブリッドデプロイメントにのみ適用されます"
exl-id: 2bc077c4-ed65-4157-bfc9-df5d0442f476
source-git-commit: 0ed70b3c57714ad6c3926181334f57ed3b409d98
workflow-type: tm+mt
source-wordcount: '1299'
ht-degree: 11%

---

# Campaign Classicのビルトインパッケージのインストール{#installing-campaign-standard-packages}



## ビルトインパッケージについて {#campaign-standard-packages}

ビルトインパッケージには、必要に応じて、契約に応じてインストールできる一連の機能が含まれています。 Campaign ビルトインパッケージの完全なリストは、以下で入手できます。

>[!CAUTION]
>
>ライセンス契約に記載されているオプションに対応するパッケージのみをインストールできます。
>
>新しいパッケージをインストールすると、すべてのプラットフォームに影響を与える可能性があります。最終的なデプロイメントの前にテストおよび検証する必要があります。
>
>パッケージは、インストール後はアンインストールできません。
>
>ホステッド環境またはハイブリッド環境のお客様は、Adobeに連絡して新しいビルトインパッケージをデプロイしてもらってください。

ビルトインパッケージをインストールするには：

1. Adobe Campaign クライアントコンソールの&#x200B;**[!UICONTROL ツール／高度なツール／パッケージをインポート]**&#x200B;から、パッケージインポートアシスタントにアクセスします。
1. 「**[!UICONTROL 標準パッケージをインストール]**」を選択します。
1. パッケージリストで、インストールするパッケージを確認します。
   >[!NOTE]
   >
   >パッケージがグレー表示されている場合は、が既にインストールされているか、インスタンスと互換性がないことを意味します。 互換性について詳しくは、次の表を参照してください。
1. 「**[!UICONTROL 次へ]**」、「**[!UICONTROL 開始]**」の順にクリックして、パッケージのインストールを開始します。

   パッケージがインストールされると、進行状況バーに **100%** と表示され、インストールログに、「**[!UICONTROL パッケージが正常にインストールされました]**」と表示されます。

1. インストールウィンドウを&#x200B;**[!UICONTROL 閉じます]**。

これで、パッケージがインストールされました。

### 標準提供のパッケージのリスト {#list-of-standard-packages}

次の表に、Campaign のすべてのビルトインパッケージを示します。

<table> 
 <thead> 
  <tr> 
   <th> パッケージ </th> 
   <th> 説明 </th> 
   <th> インスタンスタイプ </th>
  </tr> 
 </thead> 
 <tbody> 
  <tr> 
   <td> 配信<br /> </td> 
   <td> メッセージの送信時に発生する配信と最終的な問題を監視します。 <a href="../../delivery/using/about-delivery-monitoring.md">詳細情報</a><br /> </td> 
   <td> すべて</td> 
  </tr> 
  <tr> 
   <td> マーケティングキャンペーン（Campaign） <br /> </td> 
   <td> コミュニケーションおよびマーケティングキャンペーンを定義、最適化、実行、分析します。 <a href="../../campaign/using/designing-marketing-campaigns.md"> 詳細情報 </a><br /> </td> 
   <td> マーケティング</td>
  </tr> 
  <tr> 
   <td> マーケティングリソース（MRM） <br /> </td> 
   <td> タスク、予算およびマーケティングリソースの管理とトラッキングを提供することにより、協調モードでマーケティングアクションを制御します。 <a href="../../mrm/using/about-marketing-resource-management.md"> 詳細情報 </a> <br /> </td> 
   <td> マーケティング</td> 
  </tr> 
  <tr> 
   <td> オファーエンジン（インタラクション） <br /> </td> 
   <td> 特定の連絡先（顧客またはターゲット）とのインタラクション中に、1 つまたは複数の適合するオファーを提供することで、リアルタイムで応答します。  オプション。 <a href="../../interaction/using/interaction-and-offer-management.md#packages-configuration"> 詳細情報 </a> <br /> </td> 
   <td> すべて<br /> </td> 
  </tr> 
  <tr> 
   <td> 実行インスタンスによるオファーエンジンの制御。 Optional.<br /> </td> 
   <td> オファーエンジン （インタラクション）のコントロールインスタンスにインストールするパッケージ。 <a href="../../interaction/using/distributed-architectures.md#packages-configuration"> 詳細情報 </a> </td> 
   <td> マーケティング <br /> </td>  
  </tr> 
  <tr> 
   <td> 実行インスタンスのオファーエンジン。 Optional.<br /> </td> 
   <td> オファーエンジン （インタラクション）の実行インスタンスにインストールするパッケージ。 <a href="../../interaction/using/distributed-architectures.md"> 詳細情報 </a> </td> 
   <td> Mid、実行 <br /> </td>  
  </tr> 
  <!--tr> 
   <td> Lead Management (Leads) (deprecated)<br /> </td> 
   <td> Simplifies the process of building and maintaining the entire leads management life cycle. <br /> </td> 
   <td> Yes<br /> </td> 
   <td> Optional, <a href="https://helpx.adobe.com/campaign/kb/deprecated-and-removed-features.html">Learn More</a> </td> 
  </tr--> 
  <tr> 
   <td> ソーシャルネットワーク（ソーシャルマーケティング） <br /> </td> 
   <td> Adobe Campaignを X （旧称：Twitter）およびFacebookと同期します。 <a href="../../social/using/about-social-marketing.md"> 詳細情報 </a> <br /> </td> 
   <td> すべて</td> 
  </tr> 
  <tr> 
   <td> トランザクションメッセージコントロール（Message Center - コントロール） <br /> </td> 
   <td> 情報システムからトリガーされたイベントから生成されたトリガーメッセージを管理します。 オプション。 <a href="../../message-center/using/about-transactional-messaging.md"> 詳細情報 </a> <br /> </td> 
   <td> マーケティング <br /> </td> 
  </tr> 
  <tr> 
   <td> トランザクションメッセージの実行（Message Center – 実行） <br /> </td> 
   <td> 高可用性と優れた負荷管理を実現します。 オプション。 <a href="../../message-center/using/about-transactional-messaging.md"> 詳細情報 </a><br /> </td> 
   <td> 実行<br /> </td>
  </tr> 
  <tr> 
   <td> LINE チャネル<br /> </td> 
   <td> Adobe Campaignで LINE チャネルを使用して配信を送信します。 オプション。 トランザクションメッセージ （Message Center パッケージ）は必須です。 <a href="../../delivery/using/line-channel.md"> 詳細情報 </a> <br /> </td> 
   <td> すべて<br /> </td> 
  </tr> 
  <tr> 
   <td> ダイレクトメールチャネル <br /> </td> 
   <td> Adobe Campaignのダイレクトメールチャネルを使用して配信を送信します。 オプション。 <a href="../../delivery/using/about-direct-mail-channel.md"> 詳細情報 </a><br /> </td> 
   <td> すべて<br /> </td>
  </tr> 
  <tr> 
   <td> モバイルチャネル （SMS） <br /> </td> 
   <td> Adobe Campaignでモバイル/SMS チャネルを使用して配信を送信します。 オプション。 <a href="../../delivery/using/sms-channel.md"> 詳細情報 </a> <br /> </td> 
   <td> すべて<br /> </td> 
  </tr> 
   <tr> 
   <td> 電話チャネル <br /> </td> 
   <td> Adobe Campaignで電話チャネルを使用して配信を送信します。 コールセンターに使用されます。 オプション。 <a href="../../delivery/using/communication-channels.md"> 詳細情報 </a> <br /> </td> 
   <td> すべて<br /> </td> 
  </tr> 
  <tr> 
   <td> モバイルアプリチャネル<br /> </td> 
   <td> は、Adobe Campaign プラットフォームを使用して、パーソナライズされた通知をアプリ経由でiOSおよびAndroid端末に送信します。 オプション。 <a href="../../delivery/using/about-mobile-app-channel.md"> 詳細情報 </a> <br /> </td> 
   <td> すべて<br /> </td> 
  </tr> 
  <tr> 
   <td> コンテンツマネージャー <br /> </td> 
   <td> 定期的なニュースレターまたは web サイトを作成し、メッセージを検証して公開します。 <a href="../../delivery/using/about-content-management.md"> 詳細情報 </a> <br /> </td> 
   <td> </td>
  </tr> 
  <tr> 
   <td> オンライン調査（調査マネージャ） <br /> </td> 
   <td> プロファイル情報の追加または変更、購読、購読解除、コンテストにエントリーするためのオンラインフォームを作成および管理します。 オプション。 <a href="../../surveys/using/about-surveys.md"> 詳細情報 </a> <br /> </td> 
   <td> マーケティング <br /> </td> 
  </tr> 
  <tr> 
   <td> マーケティング分析 <br /> </td> 
   <td> を使用すると、データの分析と測定、統計の計算、レポートの作成と計算の簡素化および最適化を行うことができます。 また、レポートを作成して、ターゲット母集団を作成できます。 オプション。 <a href="../../reporting/using/ac-cubes.md"> 詳細情報 </a><br /> </td> 
   <td> マーケティング <br /> </td> 
  </tr> 
  <tr> 
   <td> Response Manager<br /> </td> 
   <td> マーケティングキャンペーンの成功と収益性を測定したり、すべての通信チャネルのオファーの提案を測定したりします。  オプション。 <a href="../../response/using/about-response-manager.md"> 詳細情報 </a> <br /> </td> 
   <td> マーケティング <br /> </td> 
  </tr> 
  <tr> 
   <td> 外部データへのアクセス （Federated Data Access） <br /> </td> 
   <td> Adobe Campaign データの構造を変更せずに外部データにアクセスできるように、1 つ以上の外部データベースに保存されている情報を処理するための Federated Data Access （FDA） オプションが用意されています。  オプション。 <a href="../../workflow/using/accessing-an-external-database-fda.md"> 詳細情報 </a> <br /> </td> 
   <td> すべて<br /> </td> 
  </tr> 
  <tr> 
   <td> キャンペーンの最適化<br /> </td> 
   <td> 会社の通信ポリシーに従って、送信するメッセージが顧客のニーズと期待に最もよく合うように、配信の送信を制御、フィルターおよび監視します。 オプション。 <a href="../../campaign-opt/using/about-campaign-typologies.md"> 詳細情報 </a> <br /> </td> 
   <td> マーケティング <br /> </td> 
  </tr> 
  <tr> 
   <td> 配信品質の監視 (メールの配信品質)<br /> </td> 
   <td> バウンスしたりスパムと見なされたりすることなく、受信者のインボックスに到達するキャンペーンの成否を測定します。 オプション。 <a href="../../delivery/using/about-deliverability.md"> 詳細情報 </a> <br /> </td> 
   <td> すべて </td> 
  </tr> 
  <tr> 
   <td> クーポン管理 <br /> </td> 
   <td> 今後のマーケティングオファーに追加するクーポンのセットを作成します。 オプション。 <a href="../../delivery/using/personalized-coupons.md"> 詳細情報 </a> <br /> </td> 
   <td> マーケティング <br /> </td> 
  </tr> 
  <tr> 
   <td> 受信ボックスレンダリング（IR） <br /> </td> 
   <td> 様々なコンテキストで送信され、受信されるメッセージをプレビューし、主要なデスクトップやアプリケーションの互換性を確認できます。 オプション。 <a href="../../delivery/using/inbox-rendering.md"> 詳細情報 </a><br /> </td> 
   <td> マーケティング <br /> </td> 
  </tr> 
  <tr> 
   <td> セントラルマーケティング/ローカルマーケティング（分散型マーケティング） <br /> </td> 
   <td> セントラルエンティティ（本社、マーケティング部門など）とローカルエンティティ（販売店、地域代理店など）の間で協調キャンペーンを実装します。 オプション。 <a href="../../distributed/using/about-distributed-marketing.md"> 詳細情報 </a><br /> </td> 
   <td> マーケティング </td> 
  </tr> 
  <tr> 
   <td> CRM コネクタ<br /> </td> 
   <td> は、Adobe Campaign プラットフォームをサードパーティシステムにリンクするための様々な CRM コネクタを提供します。  <a href="../../platform/using/crm-connectors.md"> 詳細情報 </a> <br /> </td> 
   <td> マーケティング</td> 
  </tr> 
  <tr> 
   <td> Web 分析コネクタ <br /> </td> 
   <td> Adobe CampaignとAdobe Analyticsが、Web 分析コネクタ パッケージを介してやり取りできるようにします。 トランザクションメッセージ（Message Center パッケージ）との互換性がありません。 <a href="../../integrations/using/gs-aa.md"> 詳細情報 </a><br /> </td> 
   <td> マーケティング </td> 
  </tr> 
  <tr> 
   <td> AEM統合 <br /> </td> 
   <td> では、AEMのコンテンツ編集機能とAdobe Campaignの配信機能を活用するために、メール配信とフォームのコンテンツをAdobe Experience Managerで直接管理できます。 <a href="../../integrations/using/about-adobe-experience-manager.md"> 詳細情報 </a> <br /> </td> 
   <td> マーケティング</td> 
  </tr> 
  <tr> 
   <td> Adobe Experience Cloud共有オーディエンスの統合 <br /> </td> 
   <td> Adobe Experience Cloudのソリューションやアプリとオーディエンス/セグメントを交換および共有できます。 IMS が必要です。 <a href="../../integrations/using/sharing-audiences-with-adobe-experience-cloud.md"> 詳細情報 </a> <br /> </td> 
   <td> マーケティング <br /> </td> 
  </tr> 
  <tr> 
   <td> Adobe Experience Cloudとの統合 <br /> </td> 
   <td> 様々なAdobe Experience Cloud ソリューションからAdobe Campaignへのオーディエンス/セグメントの読み込みおよび書き出しが可能です。 オプション。 <a href="../../integrations/using/configuring-ims.md#installing-the-package"> 詳細情報 </a> </td> 
   <td> マーケティング</td> 
  </tr> 
  <tr> 
   <td> プライバシーデータ保護規則<br /> </td> 
   <td> Campaign Classicのプライバシーコンプライアンスに役立つ追加機能が含まれます。 <a href="https://helpx.adobe.com/jp/campaign/kb/acc-privacy.html"> 詳細情報 </a> <br /> </td> 
   <td> すべて</td> 
  </tr> 
  <tr> 
   <td> ミッドソーシングサー <br /> スに転送 </td> 
   <td> ミッドソーシングサーバーのインストールと設定、およびサードパーティがミッドソーシングモードでメッセージを送信できるインスタンスのデプロイメントについて詳しく説明します。 オプション。 <a href="../../installation/using/mid-sourcing-server.md"> 詳細情報 </a> <br /> </td> 
   <td> マーケティング </td> 
  </tr> 
  <tr> 
   <td> ミッドソーシングプラットフォーム<br /> </td> 
   <td> この設定は、ホスト型（ASP）設定と内部化の間の最適な中間ソリューションです。 外部向きの実行コンポーネントは、Adobe Campaignでホストされる「ミッドソーシング」サーバーで実行されます。 オプション。 <a href="../../installation/using/mid-sourcing-server.md"> 詳細情報 </a> <br /> </td> 
   <td> ミッドソーシング </td> 
  </tr> 
  <tr> 
   <td> AMP のサポート <br /> </td> 
   <td> を使用すると、新しいインタラクティブ AMP for E メールフォーマットを使用し、動的なメールを送信できます。 オプション。 <a href="../../delivery/using/defining-interactive-content.md"> 詳細情報 </a> <br /> </td> 
   <td> すべて </td> 
  </tr> 
  <tr> 
   <td> ACS コネクタ（非推奨） <br /> </td> 
   <td> Adobe Campaign v7 とAdobe Campaign Standardをブリッジします。 Campaign v7 の統合機能で、Campaign Standard にデータを自動的にレプリケートして、両方のアプリケーションの優れた機能を連携させます。Optional.<br /> </td> 
   <td> マーケティング </td> 
  </tr> 
 </tbody> 
</table>

### Message Center パッケージ {#message-center-package}

トランザクションメッセージ（Message Center パッケージ）をインストールする前に、配信チャネル（メール、モバイルチャネル、モバイルアプリチャネル、LINE など）をインストールする必要があります。 メールのみの Message Center プロジェクトを開始し、後で新しいチャネルを追加する必要がある場合は、次の手順に従う必要があります。

1. パッケージインポートアシスタント（**[!UICONTROL ツール/詳細設定/パッケージをインポート/Adobe Campaign パッケージ]**）を使用して、新しいチャネル（**モバイルチャネル** など）をインストールします。
1. ファイルをインポートし（**[!UICONTROL ツール/詳細/パッケージをインポート/ファイル]**）、次を選択します。

   ```
   \datakit\nms\[Your language]\package\messageCenter.xml
   ```

1. **[!UICONTROL インポートする XML データコンテンツ]** には、関連チャネルに対応する Message Center 配信テンプレートのみを保存します。 例えば、**モバイルチャネル** を追加した場合は、**[!UICONTROL モバイルトランザクションメッセージ** （smsTriggerMessage）テンプレートに対応する **entities]** 要素のみを残します。 **モバイルアプリチャネル** を追加した場合は、**iOS トランザクションメッセージ** テンプレート（iosTriggerMessage）と **Android トランザクションメッセージ** （androidTriggerMessage）のみを保持します。

   ![](assets/messagecenter_install_channel.png)


### [!DNL LINE] チャネル設定{#line-package}

[!DNL LINE] チャネルを設定するには、まず [!DNL LINE] パッケージをインストールする必要があります。

ミッドソーシング設定のコンテキストでは、次の操作が必要です。

* マーケティングインスタンスと MID インスタンスの両方に [!DNL LINE] パッケージをインストールします

* 配信モードを変更して、ミッドインスタンスを指すように mkt インスタンスで [!DNL LINE] 外部アカウントを設定します。 [詳細情報](../../delivery/using/line-channel.md#configure-line-external)

* MID インスタンスの外部アカウントに [!DNL LINE] 資格情報をセットアップします。

>[!CAUTION]
>
>リク [!DNL LINE] スト前に Message Center パッケージがインストールされている場合、[!DNL LINE] チャネルの Message Center 配信テンプレートは使用できません。