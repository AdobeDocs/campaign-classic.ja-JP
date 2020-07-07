---
title: Campaign Classic 標準パッケージのインストール
seo-title: Campaign Classic 標準パッケージのインストール
description: Campaign Classic 標準パッケージのインストール
seo-description: null
page-status-flag: never-activated
uuid: 1cba9487-52fc-442f-ae99-f8a2c157f25e
contentOwner: sauviat
products: SG_CAMPAIGN/CLASSIC
audience: installation
content-type: reference
topic-tags: initial-configuration
discoiquuid: dd8f9adf-208c-42d9-b1a7-bfc8a690687e
index: y
internal: n
snippet: y
translation-type: tm+mt
source-git-commit: 788866c4f11d3875f713a61f7560d6d5255f3019
workflow-type: tm+mt
source-wordcount: '1176'
ht-degree: 27%

---


# Installing Campaign Classic built-in packages{#installing-campaign-standard-packages}

## 組み込みパッケージについて {#campaign-standard-packages}

組み込みのパッケージには、ニーズに応じて、また契約に応じてインストールできる一連の機能が含まれています。 キャンペーン組み込みパッケージの完全なリストは以下のとおりです。

>[!CAUTION]
>
>使用許諾契約に記載されているオプションに対応するパッケージのみをインストールできます。
>
>新しいパッケージをインストールすると、すべてのプラットフォームに影響を与える可能性があります。 最終的な導入の前に、テストと検証を行う必要があります。
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

### List of out-of-the-box Packages {#list-of-standard-packages}

次の表に、すべての標準パッケージの説明と、それらのパッケージをインストールできるインスタンスタイプ（マーケティング、中間など）を示します。 および追加情報。

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
   <td> メッセージの送信時に発生する配信と最終的な問題を監視します。 <a href="../../delivery/using/monitoring-a-delivery.md">詳細情報</a><br />。 </td> 
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
   <td> Offer engine (interaction)<br /> </td> 
   <td> 1つまたは複数の適合オファーを作成することで、特定の接触(顧客またはターゲット)との対話中にリアルタイムで応答します。  （オプション）<a href="../../interaction/using/interaction-and-offer-management.md">詳細情報</a> <br /> </td> 
   <td> すべて<br /> </td> 
  </tr> 
  <tr> 
   <td> 実行インスタンスによるオファーエンジンのコントロール. （オプション）<br /> </td> 
   <td> </td> 
   <td> マーケティング<br /> </td>  
  </tr> 
  <tr> 
   <td> 実行インスタンス用のオファーエンジン. （オプション）<br /> </td> 
   <td> </td> 
   <td> 中間、実行 <br /> </td>  
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
   <td> 電話チャネル<br /> </td> 
   <td> 電話チャネルを使用してAdobe Campaignを送信します。<br /> </td> 
   <td> すべて<br /> </td> 
   <td> オプション</td> 
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
   <td> Coupon Management<br /> </td> 
   <td> クーポンのセットを作成して、今後のマーケティングオファーに追加します。 （オプション）<a href="../../delivery/using/personalized-coupons.md">詳細情報</a> <br /> </td> 
   <td> マーケティング<br /> </td> 
  </tr> 
  <tr> 
   <td> 受信ボックスレンダリング (IR)<br /> </td> 
   <td> メッセージを受信する様々なコンテキストで送信するプレビューを有効にし、メジャーなデスクトップおよびアプリケーションでの互換性を確認します。 （オプション）<a href="../../delivery/using/inbox-rendering.md">詳細情報</a><br /> </td> 
   <td> マーケティング<br /> </td> 
  </tr> 
  <tr> 
   <td> セントラル / ローカルマーケティング (分散型マーケティング)<br /> </td> 
   <td> セントラルエンティティ（本部、販売部など）間の協調キャンペーンを実現 ローカルエンティティ（販売地点、地域機関等） （オプション）<a href="../../campaign/using/about-distributed-marketing.md">詳細情報</a><br /> </td> 
   <td> マーケティング </td> 
  </tr> 
  <tr> 
   <td> CRM コネクタ<br /> </td> 
   <td> Adobe Campaignプラットフォームをサードパーティ製システムにリンクするための様々なCRMコネクターを提供します。  <a href="../../platform/using/crm-connectors.md">詳細情報</a> <br /> </td> 
   <td> マーケティング</td> 
  </tr> 
  <tr> 
   <td> Web 分析コネクタ<br /> </td> 
   <td> Adobe CampaignとアドビのAnalyticsがWebAnalyticsコネクターパッケージを使用してやり取りを行うことを許可します。 トランザクションメッセージング（Message Centerパッケージ）との互換性がありません。 <a href="../../platform/using/adobe-analytics-data-connector.md">詳細情報</a><br /> </td> 
   <td> マーケティング </td> 
  </tr> 
  <tr> 
   <td> AEM 統合<br /> </td> 
   <td> 電子メール配信のコンテンツとフォームをAdobe Experience Managerで直接管理でき、AEMのコンテンツ編集機能とAdobe Campaignの配信容量を活用できます。 <a href="../../integrations/using/about-adobe-experience-manager.md">詳細情報</a> <br /> </td> 
   <td> マーケティング</td> 
  </tr> 
  <tr> 
   <td> Adobe Marketing Cloud との共有オーディエンスの統合<br /> </td> 
   <td> オーディエンス/セグメントをAdobe Experience Cloudソリューションおよびコアサービスと交換および共有できます。 IMSが必要です。 <a href="../../integrations/using/sharing-audiences-with-adobe-experience-cloud.md">詳細情報</a> <br /> </td> 
   <td> マーケティング<br /> </td> 
  </tr> 
  <tr> 
   <td> Integration with Adobe Marketing Cloud<br /> </td> 
   <td> 様々なAdobe Marketing Cloudソリューションからオーディエンス/セグメントをAdobe Campaignにインポートおよびエクスポートできます。 （オプション）<a href="../../integrations/using/configuring-ims.md#installing-the-package">詳細情報</a> </td> 
   <td> マーケティング</td> 
  </tr> 
  <tr> 
   <td> プライバシーデータ保護規則<br /> </td> 
   <td> Campaign Classicのプライバシーコンプライアンスに役立つ追加機能が含まれています。 <a href="https://helpx.adobe.com/jp/campaign/kb/acc-privacy.html">詳細情報</a> <br /> </td> 
   <td> すべて</td> 
  </tr> 
  <tr> 
   <td> ミッドソーシング転送 <br /> </td> 
   <td> ミッドソーシングサーバーのインストールと設定、およびサードパーティがミッドソーシングモードでメッセージを送信できるようにするインスタンスのデプロイメントについて詳しく説明します。 （オプション）<a href="../../installation/using/mid-sourcing-server.md">詳細情報</a> <br /> </td> 
   <td> マーケティング </td> 
  </tr> 
  <tr> 
   <td> ミッドソーシングプラットフォーム<br /> </td> 
   <td> この設定は、ホスト(ASP)設定と内部化の間の最適な中間ソリューションです。 外向きの実行コンポーネントは、Adobe Campaignでホストされる「ミッドソーシング」サーバーで実行されます。 （オプション）<a href="../../installation/using/mid-sourcing-server.md">詳細情報</a> <br /> </td> 
   <td> ミッドソーシング </td> 
  </tr> 
  <tr> 
   <td> ACS コネクタ<br /> </td> 
   <td> BridgesAdobe Campaignv7およびAdobe Campaign Standard。 Campaign v7 の統合機能で、Campaign Standard にデータを自動的にレプリケートして、両方のアプリケーションの優れた機能を連携させます。（オプション）<a href="../../integrations/using/acs-connector-principles-and-data-cycle.md">詳細情報</a> <br /> </td> 
   <td> マーケティング </td> 
  </tr> 
 </tbody> 
</table>

### Message Centerパッケージ {#message-center-package}

配信チャネル(電子メール、モバイルチャネル、モバイルアプリチャネルなど)を トランザクションメッセージをインストールする前に（Message Centerパッケージ） 電子メールのみのMessage Centerプロジェクトを開始し、その後新しいチャネルを追加する必要がある場合は、次の手順に従う必要があります。

1. Install the new channel, for example the **Mobile channel**, using the package import wizard ( **[!UICONTROL Tools > Advanced > Import package > Adobe Campaign package]**).
1. ファイルを読み込み( **[!UICONTROL ツール/アドバンスト/パッケージの読み込み/ファイル]**)、次を選択します。

   ```
   \datakit\nms\[Your language]\package\messageCenter.xml
   ```

1. 読み込む **[!UICONTROL XMLデータコンテンツで]**、関連するチャネルに対応するMessage Center配信テンプレートのみを保持します。 For example, if you have added the **Mobile channel**, keep only the **entities** element corresponding to the **[!UICONTROL Mobile transactional message]** (smsTriggerMessage) template. If you have added the **Mobile App Channel**, keep only the **iOS transactional message** templates (iosTriggerMessage) and **Android transactional message** (androidTriggerMessage).

   ![](assets/messagecenter_install_channel.png)

>[!CAUTION]
>
>Message CenterパッケージがLINEの前にインストールされている場合、LINEのMessage Center配信テンプレートは使用できません

