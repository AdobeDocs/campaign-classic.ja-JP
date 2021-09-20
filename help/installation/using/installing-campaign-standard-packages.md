---
product: campaign
title: Campaign Classic 組み込みパッケージのインストール
description: Campaignの組み込みパッケージのインストール方法を説明します
audience: installation
content-type: reference
topic-tags: initial-configuration
exl-id: 2bc077c4-ed65-4157-bfc9-df5d0442f476
source-git-commit: 00b8a9b4a693920aa6b4be9e7c41f08c2e53a0c6
workflow-type: tm+mt
source-wordcount: '1208'
ht-degree: 26%

---

# Campaign Classic 組み込みパッケージのインストール{#installing-campaign-standard-packages}

![](../../assets/v7-only.svg)

## 組み込みパッケージについて {#campaign-standard-packages}

組み込みパッケージには、ニーズや契約に応じてインストールできる一連の機能が含まれています。 Campaignの組み込みパッケージの完全なリストは、以下で確認できます。

>[!CAUTION]
>
>使用許諾契約に記載されているオプションに対応するパッケージのみをインストールできます。
>
>新しいパッケージをインストールすると、すべてのプラットフォームに影響を与える可能性があります。最終的なデプロイメントの前に、テストおよび検証をおこなう必要があります。
>
>インストールしたパッケージはアンインストールできません。

組み込みパッケージをインストールするには：

1. Adobe Campaignクライアントコンソールで、**[!UICONTROL ツール/詳細設定/パッケージをインポート]**&#x200B;からパッケージインポートウィザードにアクセスします。
1. 「**[!UICONTROL 標準パッケージをインストール]**」を選択します。
1. パッケージリストで、インストールするパッケージを確認します。
   >[!NOTE]
   >
   >パッケージがグレー表示になっている場合は、既にインストールされているか、お使いのインスタンスと互換性がないことを意味します。 互換性について詳しくは、次の表を参照してください。
1. 「**[!UICONTROL 次へ]**」、「**[!UICONTROL 開始]**」の順にクリックして、パッケージのインストールを開始します。

   パッケージがインストールされると、進行状況バーに **100%** と表示され、インストールログに、「**[!UICONTROL パッケージが正常にインストールされました]**」と表示されます。

1. インストールウィンドウを&#x200B;**[!UICONTROL 閉じます]**。

これで、パッケージがインストールされました。

### 標準パッケージのリスト {#list-of-standard-packages}

次の表に、すべてのCampaign組み込みパッケージを示します。

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
   <td> 配信と、メッセージの送信時に結果として発生する問題を監視します。 <a href="../../delivery/using/about-delivery-monitoring.md">詳細情報</a><br /> </td> 
   <td> すべて</td> 
  </tr> 
  <tr> 
   <td> マーケティングキャンペーン（キャンペーン）<br /> </td> 
   <td> コミュニケーションおよびマーケティングキャンペーンを定義、最適化、実行、分析します。 <a href="../../campaign/using/designing-marketing-campaigns.md">詳細</a><br /> </td> 
   <td> マーケティング</td>
  </tr> 
  <tr> 
   <td> マーケティングリソース（MRM）<br /> </td> 
   <td> タスク、予算およびマーケティングリソースの管理とトラッキングを提供し、マーケティングアクションを協調モードで制御します。 <a href="../../mrm/using/about-marketing-resource-management.md">詳細</a> <br /> </td> 
   <td> マーケティング</td> 
  </tr> 
  <tr> 
   <td> オファーエンジン（インタラクション）<br /> </td> 
   <td> 特定のコンタクト先（顧客またはターゲット）とのインタラクション中に、1つまたは複数の適合したオファーを提示して、リアルタイムで応答します。  （オプション）<a href="../../interaction/using/interaction-and-offer-management.md#packages-configuration">詳細</a> <br /> </td> 
   <td> すべて<br /> </td> 
  </tr> 
  <tr> 
   <td> 実行インスタンスによるオファーエンジンのコントロール. （オプション）<br /> </td> 
   <td> オファーエンジン（インタラクション）のコントロールインスタンスにインストールするパッケージ。 <a href="../../interaction/using/distributed-architectures.md#packages-configuration">詳細</a> </td> 
   <td> マーケティング<br /> </td>  
  </tr> 
  <tr> 
   <td> 実行インスタンス用のオファーエンジン. （オプション）<br /> </td> 
   <td> オファーエンジン（インタラクション）の実行インスタンスにインストールするパッケージ。 <a href="../../interaction/using/distributed-architectures.md">詳細</a> </td> 
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
   <td> Adobe CampaignをTwitterおよびFacebookと同期します。 <a href="../../social/using/about-social-marketing.md">詳細</a> <br /> </td> 
   <td> すべて</td> 
  </tr> 
  <tr> 
   <td> トランザクションメッセージコントロール（Message Center - コントロール）<br /> </td> 
   <td> 情報システムからトリガーされたトリガーから生成されたイベントメッセージを管理します。 （オプション）<a href="../../message-center/using/about-transactional-messaging.md">詳細</a> <br /> </td> 
   <td> マーケティング<br /> </td> 
  </tr> 
  <tr> 
   <td> トランザクションメッセージ実行 (Message Center - 実行) <br /> </td> 
   <td> 高い可用性と優れた負荷管理を実現 （オプション）<a href="../../message-center/using/about-transactional-messaging.md">詳細</a><br /> </td> 
   <td> 実行<br /> </td>
  </tr> 
  <tr> 
   <td> LINE チャネル<br /> </td> 
   <td> Adobe CampaignでLINEチャネルを使用して配信を送信します。 （オプション）トランザクションメッセージ（Message Centerパッケージ）が必須です。 <a href="../../delivery/using/line-channel.md">詳細</a> <br /> </td> 
   <td> すべて<br /> </td> 
  </tr> 
  <tr> 
   <td> ダイレクトメールチャネル<br /> </td> 
   <td> Adobe Campaignでダイレクトメールチャネルを使用して配信を送信します。 （オプション）<a href="../../delivery/using/about-direct-mail-channel.md">詳細</a><br /> </td> 
   <td> すべて<br /> </td>
  </tr> 
  <tr> 
   <td> モバイルチャネル (SMS) <br /> </td> 
   <td> Adobe Campaignでモバイル/SMSチャネルを使用して配信を送信します。 （オプション）<a href="../../delivery/using/sms-channel.md">詳細</a> <br /> </td> 
   <td> すべて<br /> </td> 
  </tr> 
   <tr> 
   <td> 電話チャネル<br /> </td> 
   <td> Adobe Campaignで電話チャネルを使用して配信を送信します。 コールセンターに使用します。 （オプション）<a href="../../delivery/using/communication-channels.md">詳細</a> <br /> </td> 
   <td> すべて<br /> </td> 
  </tr> 
  <tr> 
   <td> モバイルアプリチャネル<br /> </td> 
   <td> Adobe Campaignプラットフォームを使用して、アプリを介してiOSおよびAndroidの端末にパーソナライズされた通知を送信します。 （オプション）<a href="../../delivery/using/about-mobile-app-channel.md">詳細</a> <br /> </td> 
   <td> すべて<br /> </td> 
  </tr> 
  <tr> 
   <td> コンテンツマネージャー<br /> </td> 
   <td> 定期的なニュースレターまたはWebサイトを作成し、メッセージを検証して発行します。 <a href="../../delivery/using/about-content-management.md">詳細</a> <br /> </td> 
   <td> </td>
  </tr> 
  <tr> 
   <td> オンライン調査 (調査マネージャー)<br /> </td> 
   <td> オンラインフォームを作成および管理して、プロファイル情報の追加または変更、購読、購読解除、競合参加フォームを作成および管理します。 （オプション）<a href="../../surveys/using/about-surveys.md">詳細</a> <br /> </td> 
   <td> マーケティング<br /> </td> 
  </tr> 
  <tr> 
   <td> マーケティング分析<br /> </td> 
   <td> データの分析と測定、統計の計算、レポートの作成と計算のシンプル化および最適化が可能です。 また、レポートを作成し、ターゲット母集団を作成することもできます。 （オプション）<a href="../../reporting/using/about-cubes.md">詳細</a><br /> </td> 
   <td> マーケティング<br /> </td> 
  </tr> 
  <tr> 
   <td> Response Manager<br /> </td> 
   <td> マーケティングキャンペーンの成功と収益性、またはすべてのコミュニケーションチャネルのオファーの提案を測定します。  （オプション）<a href="../../response/using/about-response-manager.md">詳細</a> <br /> </td> 
   <td> マーケティング<br /> </td> 
  </tr> 
  <tr> 
   <td> 外部データへのアクセス (Federated Data Access)<br /> </td> 
   <td> 1つ以上の外部データベースに保存された情報を処理してAdobe Campaignデータの構造を変更せずに外部データにアクセスできるようにするためのFederated Data Access(FDA)オプションが用意されています。  （オプション）<a href="../../workflow/using/accessing-an-external-database--fda-.md">詳細</a> <br /> </td> 
   <td> すべて<br /> </td> 
  </tr> 
  <tr> 
   <td> キャンペーンの最適化<br /> </td> 
   <td> 配信の送信を制御、フィルタリングおよび監視し、会社のコミュニケーションポリシーに従って、顧客のニーズと期待に応える最適なメッセージを送信します。 （オプション）<a href="../../campaign-opt/using/about-campaign-typologies.md">詳細</a> <br /> </td> 
   <td> マーケティング<br /> </td> 
  </tr> 
  <tr> 
   <td> 配信品質の監視 (E メールの配信品質)<br /> </td> 
   <td> バウンスしたりスパムとしてマークされたりせずに受信者の受信ボックスに到達したかに基づいて、キャンペーンの成功を測定します。 （オプション）<a href="../../delivery/using/about-deliverability.md">詳細</a> <br /> </td> 
   <td> すべて </td> 
  </tr> 
  <tr> 
   <td> クーポン管理<br /> </td> 
   <td> クーポンのセットを作成し、今後のマーケティングオファーに追加します。 （オプション）<a href="../../delivery/using/personalized-coupons.md">詳細</a> <br /> </td> 
   <td> マーケティング<br /> </td> 
  </tr> 
  <tr> 
   <td> 受信ボックスレンダリング（IR）<br /> </td> 
   <td> 異なるコンテキストで受信される可能性のある、送信されたメッセージをプレビューし、メジャーなデスクトップおよびアプリケーションの互換性を確認できます。 （オプション）<a href="../../delivery/using/inbox-rendering.md">詳細</a><br /> </td> 
   <td> マーケティング<br /> </td> 
  </tr> 
  <tr> 
   <td> セントラル／ローカルマーケティング（分散型マーケティング）<br /> </td> 
   <td> セントラルエンティティ間（本社、マーケティング部門など）の協調キャンペーンを実装 およびローカルエンティティ（販売ポイント、地域機関など） （オプション）<a href="../../distributed/using/about-distributed-marketing.md">詳細</a><br /> </td> 
   <td> マーケティング </td> 
  </tr> 
  <tr> 
   <td> CRM コネクタ<br /> </td> 
   <td> Adobe Campaignプラットフォームをサードパーティシステムにリンクするための様々なCRMコネクタを提供します。  <a href="../../platform/using/crm-connectors.md">詳細</a> <br /> </td> 
   <td> マーケティング</td> 
  </tr> 
  <tr> 
   <td> Web 分析コネクタ<br /> </td> 
   <td> Adobe CampaignとAdobe AnalyticsがWeb分析コネクタパッケージを介してやり取りできるようにします。 トランザクションメッセージ（Message Centerパッケージ）との互換性がない。 <a href="../../platform/using/adobe-analytics-connector.md">詳細</a><br /> </td> 
   <td> マーケティング </td> 
  </tr> 
  <tr> 
   <td> AEM 統合<br /> </td> 
   <td> Eメール配信とフォームのコンテンツをAdobe Experience Managerで直接管理でき、AEMのコンテンツ編集機能やAdobe Campaignの配信能力を活用できます。 <a href="../../integrations/using/about-adobe-experience-manager.md">詳細</a> <br /> </td> 
   <td> マーケティング</td> 
  </tr> 
  <tr> 
   <td> Adobe Experience Cloud 共有オーディエンス統合<br /> </td> 
   <td> Adobe Experience Cloudソリューションおよびコアサービスとオーディエンス/セグメントを交換および共有できます。 IMSが必要です。 <a href="../../integrations/using/sharing-audiences-with-adobe-experience-cloud.md">詳細</a> <br /> </td> 
   <td> マーケティング<br /> </td> 
  </tr> 
  <tr> 
   <td> Adobe Experience Cloud との統合<br /> </td> 
   <td> 別のAdobe Experience Cloudソリューションのオーディエンス/セグメントをAdobe Campaignにインポートおよびエクスポートできます。 （オプション）<a href="../../integrations/using/configuring-ims.md#installing-the-package">詳細</a> </td> 
   <td> マーケティング</td> 
  </tr> 
  <tr> 
   <td> プライバシーデータ保護規則<br /> </td> 
   <td> プライバシーのコンプライアンスに役立つ追加機能が含まれています。Campaign Classic <a href="https://helpx.adobe.com/jp/campaign/kb/acc-privacy.html">詳細</a> <br /> </td> 
   <td> すべて</td> 
  </tr> 
  <tr> 
   <td> ミッドソーシング転送 <br /> </td> 
   <td> ミッドソーシングサーバーのインストールと設定の詳細、およびサードパーティによるミッドソーシングモードでのメッセージの送信を可能にするインスタンスのデプロイメントについて説明します。 （オプション）<a href="../../installation/using/mid-sourcing-server.md">詳細</a> <br /> </td> 
   <td> マーケティング </td> 
  </tr> 
  <tr> 
   <td> ミッドソーシングプラットフォーム<br /> </td> 
   <td> この設定は、ホスト型(ASP)設定と内部化の間の最適な中間ソリューションです。 外向きの実行コンポーネントは、Adobe Campaignでホストされる「ミッドソーシング」サーバーで実行されます。 （オプション）<a href="../../installation/using/mid-sourcing-server.md">詳細</a> <br /> </td> 
   <td> ミッドソーシング </td> 
  </tr> 
  <tr> 
   <td> AMP サポート<br /> </td> 
   <td> 新しいインタラクティブAMP for Eメールフォーマットを使用し、動的なEメールを送信できます。 （オプション）<a href="../../delivery/using/defining-interactive-content.md">詳細</a> <br /> </td> 
   <td> すべて </td> 
  </tr> 
  <tr> 
   <td> ACS コネクタ<br /> </td> 
   <td> Adobe Campaign v7とAdobe Campaign Standardをブリッジします。 Campaign v7 の統合機能で、Campaign Standard にデータを自動的にレプリケートして、両方のアプリケーションの優れた機能を連携させます。（オプション）<a href="../../integrations/using/acs-connector-principles-and-data-cycle.md">詳細</a> <br /> </td> 
   <td> マーケティング </td> 
  </tr> 
 </tbody> 
</table>

### Message Centerパッケージ {#message-center-package}

配信チャネル（Eメール、モバイルチャネル、モバイルアプリチャネルなど）を トランザクションメッセージ（Message Centerパッケージ）をインストールする前に EメールのみのMessage Centerプロジェクトを開始し、その後新しいチャネルを追加する必要がある場合は、次の手順に従います。

1. パッケージインポートウィザードを使用して、新しいチャネル（例：**モバイルチャネル**）をインストールします(**[!UICONTROL ツール/詳細設定/パッケージをインポート/Adobe Campaignパッケージ]**)。
1. ファイルを読み込み（**[!UICONTROL ツール/詳細設定/パッケージを読み込み/ファイル]**）、次を選択します。

   ```
   \datakit\nms\[Your language]\package\messageCenter.xml
   ```

1. **[!UICONTROL インポートするXMLデータコンテンツ]**&#x200B;には、関連するチャネルに対応するMessage Center配信テンプレートのみを残します。 例えば、**モバイルチャネル**&#x200B;を追加した場合は、**[!UICONTROL モバイルトランザクションメッセージ]**(smsTriggerMessage)テンプレートに対応する&#x200B;**entities**&#x200B;要素のみを残します。 **モバイルアプリチャネル**&#x200B;を追加した場合は、**iOSトランザクションメッセージ**&#x200B;テンプレート(iosTriggerMessage)と&#x200B;**Androidトランザクションメッセージ**(androidTriggerMessage)のみを残します。

   ![](assets/messagecenter_install_channel.png)

>[!CAUTION]
>
>LINEより前にMessage Centerパッケージがインストールされている場合、LINE用のMessage Center配信テンプレートは使用できません
