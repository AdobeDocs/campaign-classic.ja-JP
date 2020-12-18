---
solution: Campaign Classic
product: campaign
title: Campaign Classic組み込みパッケージのインストール
description: キャンペーンの組み込みパッケージをインストールする方法を説明します。
audience: installation
content-type: reference
topic-tags: initial-configuration
translation-type: tm+mt
source-git-commit: 6d5dbc16ed6c6e5a2e62ceb522e2ccd64b142825
workflow-type: tm+mt
source-wordcount: '1189'
ht-degree: 26%

---


# Campaign Classicの組み込みパッケージのインストール{#installing-campaign-standard-packages}

## 組み込みパッケージについて{#campaign-standard-packages}

組み込みのパッケージには、ニーズに応じて、また契約に応じてインストールできる一連の機能が含まれています。 キャンペーン組み込みパッケージの完全なリストは以下のとおりです。

>[!CAUTION]
>
>使用許諾契約に記載されているオプションに対応するパッケージのみをインストールできます。
>
>新しいパッケージをインストールすると、すべてのプラットフォームに影響を与える可能性があります。最終的な導入の前に、テストと検証を行う必要があります。
>
>パッケージをインストールした後は、アンインストールできません。

組み込みパッケージをインストールするには：

1. Adobe Campaign クライアントコンソールの&#x200B;**[!UICONTROL ツール／高度なツール／パッケージをインポート...]**&#x200B;からパッケージ読み込みウィザードにアクセスします。
1. 「**[!UICONTROL 標準パッケージをインストール]**」を選択します。
1. パッケージリストで、インストールするパッケージを確認します。
   >[!NOTE]
   >
   >パッケージがグレー表示の場合は、既にインストールされているか、お使いのインスタンスと互換性がないことを意味します。 互換性については、次の表を参照してください。
1. 「**[!UICONTROL 次へ]**」、「**[!UICONTROL 開始]**」の順にクリックして、パッケージのインストールを開始します。

   パッケージがインストールされると、進行状況バーに **100%** と表示され、インストールログに、「**[!UICONTROL パッケージが正常にインストールされました]**」と表示されます。

1. インストールウィンドウを&#x200B;**[!UICONTROL 閉じます]**。

これでパッケージがインストールされます。

### パッケージのリスト{#list-of-standard-packages}

次の表に、すべてのキャンペーン組み込みパッケージのリストを示します。

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
   <td> マーケティングキャンペーン (キャンペーン)<br /> </td> 
   <td> 通信とマーケティングキャンペーンを定義、最適化、実行、分析します。 <a href="../../campaign/using/designing-marketing-campaigns.md">詳細情報</a><br /> </td> 
   <td> マーケティング</td>
  </tr> 
  <tr> 
   <td> マーケティングリソース (MRM)<br /> </td> 
   <td> タスク、予算、マーケティングリソースの管理と追跡を提供することで、共同作業モードでのマーケティングアクションを制御します。 <a href="../../campaign/using/about-marketing-resource-management.md">詳細情報</a> <br /> </td> 
   <td> マーケティング</td> 
  </tr> 
  <tr> 
   <td> オファーエンジン（相互作用）<br /> </td> 
   <td> 1つまたは複数の適合オファーを作成することで、特定の接触(顧客またはターゲット)との対話中にリアルタイムで応答します。  （オプション）<a href="../../interaction/using/interaction-and-offer-management.md#packages-configuration">詳細情報</a> <br /> </td> 
   <td> すべて<br /> </td> 
  </tr> 
  <tr> 
   <td> 実行インスタンスによるオファーエンジンのコントロール. （オプション）<br /> </td> 
   <td> オファーエンジン（操作）のコントロールインスタンスにインストールするパッケージです。 <a href="../../interaction/using/distributed-architectures.md#packages-configuration">詳細情報</a> </td> 
   <td> マーケティング<br /> </td>  
  </tr> 
  <tr> 
   <td> 実行インスタンス用のオファーエンジン. （オプション）<br /> </td> 
   <td> オファーエンジン（操作）の実行インスタンスにインストールするパッケージです。 <a href="../../interaction/using/distributed-architectures.md">詳細情報</a> </td> 
   <td> 中間、実行<br /> </td>  
  </tr> 
  <!--tr> 
   <td> Lead Management (Leads) (deprecated)<br /> </td> 
   <td> Simplifies the process of building and maintaining the entire leads management life cycle. <br /> </td> 
   <td> Yes<br /> </td> 
   <td> Optional, <a href="https://helpx.adobe.com/campaign/kb/deprecated-and-removed-features.html">Learn More</a> </td> 
  </tr--> 
  <tr> 
   <td> ソーシャルネットワーク (ソーシャルマーケティング) <br /> </td> 
   <td> TwitterおよびFacebookとAdobe Campaignを同期します。 <a href="../../social/using/about-social-marketing.md">詳細情報</a> <br /> </td> 
   <td> すべて</td> 
  </tr> 
  <tr> 
   <td> トランザクションメッセージコントロール (Message Center - コントロール)<br /> </td> 
   <td> 情報システムからトリガーされたイベントから生成されるトリガーメッセージを管理します。 （オプション）<a href="../../message-center/using/about-transactional-messaging.md">詳細情報</a> <br /> </td> 
   <td> マーケティング<br /> </td> 
  </tr> 
  <tr> 
   <td> トランザクションメッセージ実行 (Message Center - 実行) <br /> </td> 
   <td> 高い可用性と優れたロード管理を実現 （オプション）<a href="../../message-center/using/about-transactional-messaging.md">詳細情報</a><br /> </td> 
   <td> 実行<br /> </td>
  </tr> 
  <tr> 
   <td> LINE チャネル<br /> </td> 
   <td> LINEチャネルを使用してAdobe Campaignを配信に送信します。 （オプション）トランザクションメッセージング（Message Centerパッケージ）は必須です。 <a href="../../delivery/using/line-channel.md">詳細情報</a> <br /> </td> 
   <td> すべて<br /> </td> 
  </tr> 
  <tr> 
   <td> ダイレクトメールチャネル<br /> </td> 
   <td> ダイレクトメールチャネルとAdobe Campaignを使用して配信を送信します。 （オプション）<a href="../../delivery/using/about-direct-mail-channel.md">詳細情報</a><br /> </td> 
   <td> すべて<br /> </td>
  </tr> 
  <tr> 
   <td> モバイルチャネル (SMS) <br /> </td> 
   <td> モバイル/SMSチャネルを使用してAdobe Campaignと配信を送信します。 （オプション）<a href="../../delivery/using/sms-channel.md">詳細情報</a> <br /> </td> 
   <td> すべて<br /> </td> 
  </tr> 
  <tr> 
   <td> モバイルアプリチャネル<br /> </td> 
   <td> Adobe Campaignプラットフォームを使用して、アプリを介してiOSおよびAndroid端末にパーソナライズされた通知を送信します。 （オプション）<a href="../../delivery/using/about-mobile-app-channel.md">詳細情報</a> <br /> </td> 
   <td> すべて<br /> </td> 
  </tr> 
  <tr> 
   <td> コンテンツマネージャー<br /> </td> 
   <td> 定期的なニュースレターまたはWebサイトを作成し、メッセージを検証して発行します。 <a href="../../delivery/using/about-content-management.md">詳細情報</a> <br /> </td> 
   <td> </td>
  </tr> 
  <tr> 
   <td> オンライン調査 (調査マネージャー)<br /> </td> 
   <td> プロファイル情報の追加や変更、購読、登録解除、または競合相手の入力フォームを行うオンラインフォームを作成および管理します。 （オプション）<a href="../../web/using/about-surveys.md">詳細情報</a> <br /> </td> 
   <td> マーケティング<br /> </td> 
  </tr> 
  <tr> 
   <td> マーケティング分析<br /> </td> 
   <td> データの分析と測定、統計の計算、レポートの作成と計算の単純化と最適化を行えます。 また、レポートを作成し、ターゲット数を作成できます。 （オプション）<a href="../../reporting/using/about-cubes.md">詳細情報</a><br /> </td> 
   <td> マーケティング<br /> </td> 
  </tr> 
  <tr> 
   <td> Response Manager<br /> </td> 
   <td> すべてのコミュニケーションチャネルに対するマーケティングキャンペーンまたはオファーの提案の成功と収益性を測定します。  （オプション）<a href="../../campaign/using/about-response-manager.md">詳細情報</a> <br /> </td> 
   <td> マーケティング<br /> </td> 
  </tr> 
  <tr> 
   <td> 外部データへのアクセス (Federated Data Access)<br /> </td> 
   <td> 1つ以上の外部データベースに保存されたFederated Data Accessを処理するために、Adobe Campaign(FDA)オプションを提供します。これにより、情報データの構造を変更せずに外部データにアクセスできます。  （オプション）<a href="../../workflow/using/accessing-an-external-database--fda-.md">詳細情報</a> <br /> </td> 
   <td> すべて<br /> </td> 
  </tr> 
  <tr> 
   <td> キャンペーンの最適化<br /> </td> 
   <td> 配信の送信を制御、フィルター、および監視し、会社の通信ポリシーに従って、送信されるメッセージが顧客のニーズと期待に最も合うようにします。 （オプション）<a href="../../campaign/using/about-campaign-typologies.md">詳細情報</a> <br /> </td> 
   <td> マーケティング<br /> </td> 
  </tr> 
  <tr> 
   <td> 配信品質の監視 (E メールの配信品質)<br /> </td> 
   <td> バウンスを発生させたり、スパムとしてマークされたりすることなく、受信者の受信トレイに届いたキャンペーンの成功を測定します。 （オプション）<a href="../../delivery/using/about-deliverability.md">詳細情報</a> <br /> </td> 
   <td> すべて </td> 
  </tr> 
  <tr> 
   <td> クーポン管理<br /> </td> 
   <td> 今後のマーケティング特典に追加するクーポンのセットを作成します。 （オプション）<a href="../../delivery/using/personalized-coupons.md">詳細情報</a> <br /> </td> 
   <td> マーケティング<br /> </td> 
  </tr> 
  <tr> 
   <td> 受信ボックスレンダリング (IR)<br /> </td> 
   <td> メッセージを受信する様々なコンテキストで送信するプレビューを有効にし、メジャーなデスクトップおよびアプリケーションでの互換性を確認します。 （オプション）<a href="../../delivery/using/inbox-rendering.md">詳細情報</a><br /> </td> 
   <td> マーケティング<br /> </td> 
  </tr> 
  <tr> 
   <td> セントラル / ローカルマーケティング (分散型マーケティング)<br /> </td> 
   <td> 中央機関（本社、マーケティング部など）間の共同キャンペーンを実施 地元の事業体（販売拠点、地域機関等） （オプション）<a href="../../campaign/using/about-distributed-marketing.md">詳細情報</a><br /> </td> 
   <td> マーケティング </td> 
  </tr> 
  <tr> 
   <td> CRM コネクタ<br /> </td> 
   <td> Adobe Campaignプラットフォームをサードパーティ製システムにリンクするための様々なCRMコネクターを提供します。  <a href="../../platform/using/crm-connectors.md">詳細情報</a> <br /> </td> 
   <td> マーケティング</td> 
  </tr> 
  <tr> 
   <td> Web 分析コネクタ<br /> </td> 
   <td> Adobe CampaignとAdobe AnalyticsがWeb Analyticsコネクタパッケージを介して対話できるようにします。 トランザクションメッセージング（メッセージセンターパッケージ）と互換性がありません。 <a href="../../platform/using/adobe-analytics-data-connector.md">詳細情報</a><br /> </td> 
   <td> マーケティング </td> 
  </tr> 
  <tr> 
   <td> AEM 統合<br /> </td> 
   <td> AEMのコンテンツ編集機能とAdobe Campaignの配信機能を利用するために、電子メール配信のコンテンツとフォームをAdobe Experience Managerで直接管理できます。 <a href="../../integrations/using/about-adobe-experience-manager.md">詳細情報</a> <br /> </td> 
   <td> マーケティング</td> 
  </tr> 
  <tr> 
   <td> Adobe Experience Cloud 共有オーディエンス統合<br /> </td> 
   <td> オーディエンス/セグメントをAdobe Experience Cloudのソリューションおよびコアサービスと交換および共有できます。 IMSが必要 <a href="../../integrations/using/sharing-audiences-with-adobe-experience-cloud.md">詳細情報</a> <br /> </td> 
   <td> マーケティング<br /> </td> 
  </tr> 
  <tr> 
   <td> Adobe Experience Cloud<br />との統合 </td> 
   <td> さまざまなAdobe Experience CloudソリューションからAdobe Campaignに対して、対象ユーザー/セグメントを読み込み、書き出すことができます。 （オプション）<a href="../../integrations/using/configuring-ims.md#installing-the-package">詳細情報</a> </td> 
   <td> マーケティング</td> 
  </tr> 
  <tr> 
   <td> プライバシーデータ保護規則<br /> </td> 
   <td> Campaign Classicのプライバシーコンプライアンスに役立つ追加機能が含まれています。 <a href="https://helpx.adobe.com/jp/campaign/kb/acc-privacy.html">詳細情報</a> <br /> </td> 
   <td> すべて</td> 
  </tr> 
  <tr> 
   <td> ミッドソーシング転送 <br /> </td> 
   <td> ミッドソーシングサーバーのインストールと構成、およびサードパーティが中間ソーシングモードでメッセージを送信できるインスタンスのデプロイの詳細。 （オプション）<a href="../../installation/using/mid-sourcing-server.md">詳細情報</a> <br /> </td> 
   <td> マーケティング </td> 
  </tr> 
  <tr> 
   <td> ミッドソーシングプラットフォーム<br /> </td> 
   <td> この構成は、ホスト(ASP)構成と内部化の間の最適な中間ソリューションです。 外向きの実行コンポーネントは、Adobe Campaignでホストされる「ミッドソーシング」サーバで実行されます。 （オプション）<a href="../../installation/using/mid-sourcing-server.md">詳細情報</a> <br /> </td> 
   <td> ミッドソーシング </td> 
  </tr> 
  <tr> 
   <td> AMP サポート<br /> </td> 
   <td> 新しい対話型AMPを電子メール形式に使用し、動的な電子メールを送信できます。 （オプション）<a href="../../delivery/using/defining-interactive-content.md">詳細情報</a> <br /> </td> 
   <td> すべて </td> 
  </tr> 
  <tr> 
   <td> ACS コネクタ<br /> </td> 
   <td> BridgesAdobe Campaignv7とAdobe Campaign Standard。 Campaign v7 の統合機能で、Campaign Standard にデータを自動的にレプリケートして、両方のアプリケーションの優れた機能を連携させます。（オプション）<a href="../../integrations/using/acs-connector-principles-and-data-cycle.md">詳細情報</a> <br /> </td> 
   <td> マーケティング </td> 
  </tr> 
 </tbody> 
</table>

### メッセージセンターパッケージ{#message-center-package}

配信チャネル（Eメール、モバイルチャネル、モバイルアプリチャネルなど）をインストールする必要があります トランザクションメッセージング（メッセージセンターパッケージ）をインストールする前に、 電子メール専用のメッセージセンタープロジェクトを開始し、その後に新しいチャネルを追加する必要がある場合は、次の手順に従ってください。

1. パッケージインポートウィザード(**[!UICONTROL ツール/詳細/パッケージの読み込み/Adobe Campaignパッケージ]**)を使用して、新しいチャネル(**モバイルチャネル**&#x200B;など)をインストールします。
1. ファイルをインポートし（ **[!UICONTROL [ツール] > [詳細設定] > [パッケージのインポート] > [ファイル]]**）、次の項目を選択します。

   ```
   \datakit\nms\[Your language]\package\messageCenter.xml
   ```

1. **[!UICONTROL インポートするXMLデータコンテンツ]**&#x200B;では、関連するチャネルに対応するメッセージセンター配信テンプレートのみを保持します。 例えば、**モバイルチャネル**&#x200B;を追加した場合、**[!UICONTROL モバイルトランザクションメッセージ]** (smsTriggerMessage)テンプレートに対応する&#x200B;**entities**&#x200B;要素のみを保持します。 **モバイルアプリチャネル**&#x200B;を追加した場合は、**iOSトランザクションメッセージ**&#x200B;テンプレート(iosTriggerMessage)と&#x200B;**Androidトランザクションメッセージ**(androidTriggerMessage)のみを残してください。

   ![](assets/messagecenter_install_channel.png)

>[!CAUTION]
>
>LINEの前にメッセージセンターパッケージがインストールされている場合、LINEのメッセージセンター配信テンプレートは使用できません

