---
product: campaign
title: Campaign Classic 組み込みパッケージのインストール
description: Campaign の組み込みパッケージのインストール方法を説明します
audience: installation
content-type: reference
topic-tags: initial-configuration
exl-id: 2bc077c4-ed65-4157-bfc9-df5d0442f476
source-git-commit: 6c23dadb5b6523e17e242de43a908ca86ed7cc23
workflow-type: tm+mt
source-wordcount: '1223'
ht-degree: 27%

---

# Campaign Classic 組み込みパッケージのインストール{#installing-campaign-standard-packages}

![](../../assets/v7-only.svg)

## 組み込みパッケージについて {#campaign-standard-packages}

組み込みパッケージには、必要に応じて、および契約に応じてインストールできる一連の機能が含まれています。 Campaign の組み込みパッケージの完全なリストは、以下で確認できます。

>[!CAUTION]
>
>使用許諾契約に記載されているオプションに対応するパッケージのみをインストールできます。
>
>新しいパッケージをインストールすると、すべてのプラットフォームに影響を与える可能性があります。最終的なデプロイメントの前に、テストと検証をおこなう必要があります。
>
>インストールしたパッケージはアンインストールできません。
>
>ホスト型またはハイブリッド型のお客様は、Adobeに連絡して、新しい組み込みパッケージをデプロイしてもらいます。

組み込みパッケージをインストールするには：

1. Adobe Campaign クライアントコンソールの&#x200B;**[!UICONTROL ツール／高度なツール／パッケージをインポート]**&#x200B;から、パッケージインポートウィザードにアクセスします。
1. 「**[!UICONTROL 標準パッケージをインストール]**」を選択します。
1. パッケージリストで、インストールするパッケージを確認します。
   >[!NOTE]
   >
   >パッケージがグレー表示になっている場合は、既にインストールされているか、お使いのインスタンスと互換性がありません。 互換性について詳しくは、次の表を参照してください。
1. 「**[!UICONTROL 次へ]**」、「**[!UICONTROL 開始]**」の順にクリックして、パッケージのインストールを開始します。

   パッケージがインストールされると、進行状況バーに **100%** と表示され、インストールログに、「**[!UICONTROL パッケージが正常にインストールされました]**」と表示されます。

1. インストールウィンドウを&#x200B;**[!UICONTROL 閉じます]**。

これで、パッケージがインストールされました。

### 標準パッケージのリスト {#list-of-standard-packages}

次の表に、すべての Campaign 組み込みパッケージの一覧を示します。

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
   <td> 配信と、メッセージの送信時に結果として起こる問題を監視します。 <a href="../../delivery/using/about-delivery-monitoring.md">詳細情報</a><br /> </td> 
   <td> すべて</td> 
  </tr> 
  <tr> 
   <td> マーケティングキャンペーン（キャンペーン）<br /> </td> 
   <td> 通信およびマーケティングキャンペーンを定義、最適化、実行および分析します。 <a href="../../campaign/using/designing-marketing-campaigns.md">詳細</a><br /> </td> 
   <td> マーケティング</td>
  </tr> 
  <tr> 
   <td> マーケティングリソース（MRM）<br /> </td> 
   <td> タスク、予算およびマーケティングリソースの管理とトラッキングを提供し、マーケティングアクションを協調モードで制御します。 <a href="../../mrm/using/about-marketing-resource-management.md">詳細</a> <br /> </td> 
   <td> マーケティング</td> 
  </tr> 
  <tr> 
   <td> オファーエンジン（インタラクション）<br /> </td> 
   <td> 特定の連絡先（顧客またはターゲット）とのインタラクション中に、1 つまたは複数の適応したオファーを作成して、リアルタイムで応答します。  （オプション）<a href="../../interaction/using/interaction-and-offer-management.md#packages-configuration">詳細</a> <br /> </td> 
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
   <td> 高い可用性と優れた負荷管理を確保します。 （オプション）<a href="../../message-center/using/about-transactional-messaging.md">詳細</a><br /> </td> 
   <td> 実行<br /> </td>
  </tr> 
  <tr> 
   <td> LINE チャネル<br /> </td> 
   <td> Adobe Campaignで LINE チャネルを使用して配信を送信します。 （オプション）トランザクションメッセージ（Message Center パッケージ）が必須です。 <a href="../../delivery/using/line-channel.md">詳細</a> <br /> </td> 
   <td> すべて<br /> </td> 
  </tr> 
  <tr> 
   <td> ダイレクトメールチャネル<br /> </td> 
   <td> Adobe Campaignでダイレクトメールチャネルを使用して配信を送信します。 （オプション）<a href="../../delivery/using/about-direct-mail-channel.md">詳細</a><br /> </td> 
   <td> すべて<br /> </td>
  </tr> 
  <tr> 
   <td> モバイルチャネル (SMS) <br /> </td> 
   <td> Adobe Campaignでモバイル/SMS チャネルを使用して配信を送信します。 （オプション）<a href="../../delivery/using/sms-channel.md">詳細</a> <br /> </td> 
   <td> すべて<br /> </td> 
  </tr> 
   <tr> 
   <td> 電話チャネル<br /> </td> 
   <td> Adobe Campaignで電話チャネルを使用して配信を送信します。 コールセンターに使用されます。 （オプション）<a href="../../delivery/using/communication-channels.md">詳細</a> <br /> </td> 
   <td> すべて<br /> </td> 
  </tr> 
  <tr> 
   <td> モバイルアプリチャネル<br /> </td> 
   <td> Adobe Campaignプラットフォームを使用して、アプリを介してiOSおよび Android の端末にパーソナライズされた通知を送信します。 （オプション）<a href="../../delivery/using/about-mobile-app-channel.md">詳細</a> <br /> </td> 
   <td> すべて<br /> </td> 
  </tr> 
  <tr> 
   <td> コンテンツマネージャー<br /> </td> 
   <td> 定期的なニュースレターや Web サイトを作成し、メッセージを検証して公開します。 <a href="../../delivery/using/about-content-management.md">詳細</a> <br /> </td> 
   <td> </td>
  </tr> 
  <tr> 
   <td> オンライン調査 (調査マネージャー)<br /> </td> 
   <td> プロファイル情報の追加や変更、購読、購読解除、競合他社の入力フォームを行うオンラインフォームを作成および管理します。 （オプション）<a href="../../surveys/using/about-surveys.md">詳細</a> <br /> </td> 
   <td> マーケティング<br /> </td> 
  </tr> 
  <tr> 
   <td> マーケティング分析<br /> </td> 
   <td> データの分析と測定、統計の計算、レポートの作成と計算のシンプル化および最適化が可能です。 また、レポートを作成し、ターゲット母集団を作成することもできます。 （オプション）<a href="../../reporting/using/about-cubes.md">詳細</a><br /> </td> 
   <td> マーケティング<br /> </td> 
  </tr> 
  <tr> 
   <td> Response Manager<br /> </td> 
   <td> すべての通信チャネルに対するマーケティングキャンペーンまたはオファーの提案の成功と収益性を測定します。  （オプション）<a href="../../response/using/about-response-manager.md">詳細</a> <br /> </td> 
   <td> マーケティング<br /> </td> 
  </tr> 
  <tr> 
   <td> 外部データへのアクセス (Federated Data Access)<br /> </td> 
   <td> 1 つ以上の外部データベースに保存されている情報を処理するために、 Federated Data Access(FDA) オプションが用意されており、Adobe Campaignデータの構造を変更せずに外部データにアクセスできます。  （オプション）<a href="../../workflow/using/accessing-an-external-database--fda-.md">詳細</a> <br /> </td> 
   <td> すべて<br /> </td> 
  </tr> 
  <tr> 
   <td> キャンペーンの最適化<br /> </td> 
   <td> 配信の送信を制御、フィルタリングおよび監視し、会社の通信ポリシーに従って、送信されたメッセージが顧客のニーズと期待に最も合うようにします。 （オプション）<a href="../../campaign-opt/using/about-campaign-typologies.md">詳細</a> <br /> </td> 
   <td> マーケティング<br /> </td> 
  </tr> 
  <tr> 
   <td> 配信品質の監視 (E メールの配信品質)<br /> </td> 
   <td> バウンスしたりスパムとしてマークされたりせずに受信者の受信ボックスに到達したかに基づいて、キャンペーンの成功を測定します。 （オプション）<a href="../../delivery/using/about-deliverability.md">詳細</a> <br /> </td> 
   <td> すべて </td> 
  </tr> 
  <tr> 
   <td> クーポン管理<br /> </td> 
   <td> 次回のマーケティングオファーに追加するクーポンのセットを作成します。 （オプション）<a href="../../delivery/using/personalized-coupons.md">詳細</a> <br /> </td> 
   <td> マーケティング<br /> </td> 
  </tr> 
  <tr> 
   <td> 受信ボックスレンダリング（IR）<br /> </td> 
   <td> 異なるコンテキストで受信される可能性のある、送信されたメッセージをプレビューし、メジャーなデスクトップおよびアプリケーションの互換性を確認できます。 （オプション）<a href="../../delivery/using/inbox-rendering.md">詳細</a><br /> </td> 
   <td> マーケティング<br /> </td> 
  </tr> 
  <tr> 
   <td> セントラル／ローカルマーケティング（分散型マーケティング）<br /> </td> 
   <td> セントラルエンティティ（本社、マーケティング部門など）間の協調キャンペーンの実装 ローカルエンティティ（セールスポイント、地域機関など） （オプション）<a href="../../distributed/using/about-distributed-marketing.md">詳細</a><br /> </td> 
   <td> マーケティング </td> 
  </tr> 
  <tr> 
   <td> CRM コネクタ<br /> </td> 
   <td> Adobe Campaignプラットフォームをサードパーティのシステムにリンクするための様々な CRM コネクタを提供します。  <a href="../../platform/using/crm-connectors.md">詳細</a> <br /> </td> 
   <td> マーケティング</td> 
  </tr> 
  <tr> 
   <td> Web 分析コネクタ<br /> </td> 
   <td> Adobe CampaignとAdobe Analyticsが Web 分析コネクタパッケージを介してやり取りできるようにします。 トランザクションメッセージ（Message Center パッケージ）とは互換性がありません。 <a href="../../platform/using/adobe-analytics-connector.md">詳細</a><br /> </td> 
   <td> マーケティング </td> 
  </tr> 
  <tr> 
   <td> AEM 統合<br /> </td> 
   <td> E メール配信とフォームのコンテンツをAdobe Experience Managerで直接管理し、AEMのコンテンツ編集機能やAdobe Campaignの配信能力を活用することができます。 <a href="../../integrations/using/about-adobe-experience-manager.md">詳細</a> <br /> </td> 
   <td> マーケティング</td> 
  </tr> 
  <tr> 
   <td> Adobe Experience Cloud 共有オーディエンス統合<br /> </td> 
   <td> Adobe Experience Cloudソリューションやコアサービスとオーディエンスやセグメントを交換し、共有できます。 IMS が必要です。 <a href="../../integrations/using/sharing-audiences-with-adobe-experience-cloud.md">詳細</a> <br /> </td> 
   <td> マーケティング<br /> </td> 
  </tr> 
  <tr> 
   <td> Adobe Experience Cloud との統合<br /> </td> 
   <td> 別のAdobe Experience Cloudソリューションのオーディエンス/セグメントをAdobe Campaignにインポートおよびエクスポートできます。 （オプション）<a href="../../integrations/using/configuring-ims.md#installing-the-package">詳細</a> </td> 
   <td> マーケティング</td> 
  </tr> 
  <tr> 
   <td> プライバシーデータ保護規則<br /> </td> 
   <td> プライバシーのコンプライアンスに役立つ追加機能がCampaign Classicに含まれています。 <a href="https://helpx.adobe.com/jp/campaign/kb/acc-privacy.html">詳細</a> <br /> </td> 
   <td> すべて</td> 
  </tr> 
  <tr> 
   <td> ミッドソーシング転送 <br /> </td> 
   <td> ミッドソーシングサーバーのインストールと設定の詳細、およびサードパーティがミッドソーシングモードでメッセージを送信できるようにするインスタンスのデプロイメントについて説明します。 （オプション）<a href="../../installation/using/mid-sourcing-server.md">詳細</a> <br /> </td> 
   <td> マーケティング </td> 
  </tr> 
  <tr> 
   <td> ミッドソーシングプラットフォーム<br /> </td> 
   <td> この設定は、ホスト (ASP) 設定と内部化の間の最適な中間ソリューションです。 外向きの実行コンポーネントは、Adobe Campaignでホストされる「ミッドソーシング」サーバーで実行されます。 （オプション）<a href="../../installation/using/mid-sourcing-server.md">詳細</a> <br /> </td> 
   <td> ミッドソーシング </td> 
  </tr> 
  <tr> 
   <td> AMP サポート<br /> </td> 
   <td> 新しいインタラクティブ AMP for e メールフォーマットを使用して、動的な E メールを送信できます。 （オプション）<a href="../../delivery/using/defining-interactive-content.md">詳細</a> <br /> </td> 
   <td> すべて </td> 
  </tr> 
  <tr> 
   <td> ACS コネクタ<br /> </td> 
   <td> Adobe Campaign v7 とAdobe Campaign Standardをブリッジします。 Campaign v7 の統合機能で、Campaign Standard にデータを自動的にレプリケートして、両方のアプリケーションの優れた機能を連携させます。（オプション）<a href="../../integrations/using/acs-connector-principles-and-data-cycle.md">詳細</a> <br /> </td> 
   <td> マーケティング </td> 
  </tr> 
 </tbody> 
</table>

### Message Center パッケージ {#message-center-package}

配信チャネル（E メール、モバイルチャネル、モバイルアプリチャネルなど）を トランザクションメッセージ（Message Center パッケージ）をインストールする前に、 E メールのみの Message Center プロジェクトを開始し、その後新しいチャネルを追加する必要がある場合は、次の手順に従う必要があります。

1. 新しいチャネル（例： ）をインストールします。 **モバイルチャネル**、パッケージインポートウィザード ( **[!UICONTROL ツール/詳細設定/パッケージをインポート/Adobe Campaignパッケージ]**) をクリックします。
1. ファイル ( **[!UICONTROL ツール/詳細設定/パッケージをインポート/ファイル]**) をクリックし、次を選択します。

   ```
   \datakit\nms\[Your language]\package\messageCenter.xml
   ```

1. 内 **[!UICONTROL インポートする XML データコンテンツ]**&#x200B;関連するチャネルに対応する Message Center の配信テンプレートのみを残します。 例えば、 **モバイルチャネル**、 **エンティティ** 次に対応する要素 **[!UICONTROL モバイルトランザクションメッセージ]** (smsTriggerMessage) テンプレート。 次の **モバイルアプリチャネル**、 **iOSトランザクションメッセージ** テンプレート (iosTriggerMessage) および **Android トランザクションメッセージ** (androidTriggerMessage)。

   ![](assets/messagecenter_install_channel.png)

>[!CAUTION]
>
>LINE より前に Message Center パッケージがインストールされている場合、LINE 用の Message Center 配信テンプレートは使用できません
