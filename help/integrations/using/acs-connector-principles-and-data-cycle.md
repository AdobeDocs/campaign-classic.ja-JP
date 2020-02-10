---
title: ACS コネクタの原則とデータサイクル
seo-title: ACS コネクタの原則とデータサイクル
description: ACS コネクタの原則とデータサイクル
seo-description: null
page-status-flag: never-activated
uuid: ea62ee69-042e-4c18-aaea-d65872d07dd9
contentOwner: sauviat
products: SG_CAMPAIGN/CLASSIC
audience: integrations
content-type: reference
topic-tags: acs-connector
discoiquuid: 64d87bea-2376-4684-ac93-6ca56fe0f262
index: y
internal: n
snippet: y
translation-type: tm+mt
source-git-commit: 209ac4d81d2d27c264ee6b288bcb7fcb1900ffc5

---


# ACS コネクタの原則とデータサイクル{#acs-connector-principles-and-data-cycle}

## はじめに {#introduction}

ACS コネクタは、Adobe Campaign v7 と Adobe Campaign Standard を橋渡しします。Campaign v7 の統合機能で、Campaign Standard にデータを自動的にレプリケートして、両方のアプリケーションの優れた機能を連携させます。Campaign v7 には、プライマリマーケティングデータベースを管理する高度なツールがあります。Campaign v7 からのデータレプリケーションにより、Campaign Standard の使いやすい環境でリッチデータを活用できます。

![](assets/acs_connect_puzzle_link_01.png)

ACS コネクタを使用すると、デジタルマーケターが Campaign Standard を引き続き使用して、キャンペーンを設計、ターゲティングおよび実行したり、データベースマーケターなどのデータ指向のユーザーが Campaign v7 をカスタマイズしたりできます。

>[!CAUTION]
>
>ACS コネクタは、Adobe Campaign Prime の一部としてのみ使用できます。Adobe Campaign Prime のライセンス付与の方法について詳しくは、担当のアカウントマネージャーにお問い合わせください。
>
>ACS コネクタは、ホストアーキテクチャおよびハイブリッドアーキテクチャでのみ使用できます。完全なオンプレミスインストールには使用できません。
>
>この機能を使用するには、Adobe ID（IMS）で Campaign に接続する必要があります。[Adobe ID を使用した接続](../../integrations/using/about-adobe-id.md)を参照してください。

このドキュメントでは、ACS コネクタの機能について説明します。以下の節では、この機能を使用したデータのレプリケート方法に関する情報と、レプリケートされたプロファイルの操作方法を説明します。

* [プロセス](#process):ACSコネクタの概要とデータ複製の管理方法。
* [実装](#implementation):ACSコネクタの使い始め方の概要と、基本データと詳細データの複製方法の説明。
* [プロファイルの同期](../../integrations/using/synchronizing-profiles.md):プロファイルの複製方法とプロファイルを使用した配信の作成方法に関する説明。
* [オーディエンスの同期](../../integrations/using/synchronizing-audiences.md):Campaign v7で受信者のリストをターゲットにし、オーディエンスとしてCampaign Standardにリストを複製する方法について説明します。
* [Webアプリケーションの同期](../../integrations/using/synchronizing-web-applications.md):Campaign v7 webアプリケーションをCampaign Standardにリンクする方法について説明します。
* [ACSコネクタのトラブルシューティング](../../integrations/using/troubleshooting-the-acs-connector.md):一般的な問題に対する回答を確認します。

>[!NOTE]
>
>ACS コネクタは、ライセンス契約下の Campaign v7 に含まれます。ACS コネクタを使用するには、Campaign v7 と Campaign Standard との間で切り替えられることを確認します。バージョンおよび含まれる機能について不明な場合は、管理者にお問い合わせください。

## プロセス {#process}

### データレプリケーション {#data-replication}

![](assets/acs_connect_flows_01.png)

ACS コネクタは、Campaign v7 から Campaign Standard に以下の項目を定期的にレプリケートします。

* **受信者**
* **購読**
* **サービス**
* **ランディングページ**

デフォルトでは、ACS コネクタの定期的なレプリケーションは、15 分ごとに 1 回です。定期的なレプリケーションの長さは、ニーズに合わせて調整できます。変更が必要な場合は、コンサルタントにお問い合わせください。

受信者、購読、サービス、ランディングページのデータレプリケーションは、増分です。つまり、新しい受信者と既存の受信者に対する変更が、Campaign v7 から Campaign Standard にレプリケートされます。ただし、オーディエンスのレプリケーションが単一のインスタンスで発生します。Campaign v7 でオーディエンスを作成したら、Campaign Standard に 1 回レプリケートできます。レプリケーションはただちにおこなわれ、定期的な更新は設定できません。手順については、オーディエンスの同 [期を参照してくださ](../../integrations/using/synchronizing-audiences.md)い。

>[!NOTE]
>
>大規模なデータベースの最初のレプリケーションは、数時間かかる場合がありますのでご注意ください。ただし、以降のレプリケーションは増分でおこなわれ、かかる時間も大幅に短縮されます。

ACS コネクタは、Campaign Standard から Campaign v7 に以下の項目を定期的にレプリケートします。

* **[!UICONTROL Delivery IDs]**
* **[!UICONTROL Email broad logs]**
* **[!UICONTROL Email tracking logs]**

配信 ID および E メールログをレプリケートすることで、Campaign v7 から v7 受信者の配信の履歴およびトラッキングデータにアクセスできます。

>[!CAUTION]
>
>Campaign Standard から Campaign v7 にレプリケートされるのは、E メール配信ログとトラッキングログのみです。

### データの同期 {#data-synchronization}

![](assets/acs_connect_flows_02.png)

ACS コネクタは、Campaign v7 と Campaign Standard の間で強制隔離を同期します。

例えば、Campaign v7 から Campaign Standard にレプリケートされたプロファイルには、E メールアドレスが含まれます。E メールアドレスが Campaign Standard によって強制隔離されると、次の同期時にデータが Campaign v7 に渡されます。強制隔離について詳しくは、[強制隔離の管理](../../delivery/using/understanding-quarantine-management.md)および [Campaign Standard の強制隔離](https://docs.adobe.com/content/help/en/campaign-standard/using/testing-and-sending/monitoring-messages/understanding-quarantine-management.html)を参照してください。

### レプリケートされたプロファイルの使用 {#using-replicated-profiles}

レプリケートされたプロファイルは、Campaign Standard および Campaign v7 でマーケティングキャンペーンのワークフローをターゲティングするために使用できます。

For instruction on how to send a delivery in Campaign Standard using replicated profiles, see [Synchronizing profiles](../../integrations/using/synchronizing-profiles.md). Campaign v7 と Campaign Standard の間の購読解除データを共有する手順が追加されています。

### 制限事項 {#limitations}

レプリケートされたプロファイルは、すぐに配信に使用できますが、Campaign Standard でいくつかの制限があります。以下の項目を参照して、最善の管理方法を確認してください。

* **Campaign Standardの読み取り専用プロファイル**:レプリケートされたプロファイルは、Campaign Standardでは読み取り専用です。 ただし、Campaign v7 で受信者を編集できます。その変更は ACS コネクタによって Campaign Standard で自動的に更新されます。
* **Campaign Standardで作成されたプロファイル**:ACSコネクタは、Campaign v7からCampaign Standardへ、受信者データを一方向に複製します。 そのため、Campaign Standard に由来するプロファイルは、Campaign v7 にレプリケートされません。
* **Campaign Standardの基本受信者データ**:ACSコネクタは、キャンペーン標準に適した受信者データを複製します。 このデータには、受信者の名前、住所、E メールアドレス、携帯電話番号、自宅電話番号、その他関連のある連絡先情報が含まれます。Campaign v7 で使用できる追加の受信者フィールドおよびカスタムターゲティングテーブルがワークフローで重要な場合、コンサルタントにお問い合わせください。
* **検疫済みプロファイルのインポート**:連絡を受けたくないプロファイルのリストは、隔離されたプロファイルとしてCampaign v7またはCampaign Standardにインポートできます。 プロファイルのステータスは、アプリケーション間の強制隔離の同期に含まれ、配信には使用されません。
* **Campaign Standardでのサービスの購読解除**:配信の購読を解除する選択がCampaign StandardからCampaign v7に同期されません。 ただし、Campaign Standard の配信の購読解除リンクを Campaign v7 宛てにするように設定できます。購読解除リンクをクリックする受信者のプロファイルは、Campaign v7 で更新され、そのデータは Campaign Standard にレプリケートされます。See [Changing the unsubscription link](../../integrations/using/synchronizing-profiles.md#changing-the-unsubscription-link).
* Campaign Standard から Campaign v7 にレプリケートされるのは、E メール配信ログとトラッキングログのみです。

### 請求 {#billing}

配信を送信するアプリケーションとして Campaign v7 と Campaign Standard のどちらを選択しても、請求に影響はありません。請求情報は、Campaign v7 と Campaign Standard の間で紐付けされています。そのため、両方のアプリケーションを使用して同じ受信者に配信を送信する場合でも、1 つのアクティブなプロファイルとみなされます。

## 実装 {#implementation}

ACS コネクタには、2 つのタイプの実装があります。どちらも、常に Adobe Campaign コンサルティングチームによって実行されます。

>[!CAUTION]
>
>この節では、エキスパートユーザーのみに向けて、実装プロセスの全体像と主な手順について説明します。
>
>どのような手段であれ、これらの実装を自分自身で実行しようとしないでください。これらの実装は厳密に Adobe Campaign コンサルタントによっておこなわれる操作です。

**基本的な実装**&#x200B;により、受信者（標準のフィールド）、サービスと購読、Web アプリケーションおよびオーディエンスをレプリケートできます。これは、Campaign v7 から Campaign Standard の一方向のレプリケーションです。

**高度な実装**&#x200B;により、例えば、追加の受信者フィールドまたはカスタム受信者テーブル（トランザクションテーブルなど）がある場合など、より複雑な使用例を実行できます。詳しくは、 [高度な実装を参照してくださ](#advanced-implementation)い。

### パッケージのインストール {#installing-the-package}

To use the feature, the **[!UICONTROL ACS Connector]** package needs to be installed. これは、常にアドビの技術管理者またはコンサルタントによって実行されます。

All the technical elements related to ACS Connector are available in the **[!UICONTROL Administration > ACS Connector]** node of the explorer.

### テクニカルワークフローおよびレプリケーションワークフロー {#technical-and-replication-workflows}

After the installation of the package, two technical workflows are available under **[!UICONTROL Administration > ACS Connector > Process]**.

>[!CAUTION]
>
>これらのワークフローは決して変更しないでください。エラーや一時停止が発生しないようにしてください。このような状況が発生した場合は、Adobe Campaign コンサルタントにお問い合わせください。

![](assets/acs_connect_implementation_3.png)

* **[!UICONTROL `[ACS] Quarantine synchronization`]** （検疫同期）:このワークフローは、すべての検疫情報を同期します。 Campaign v7 のすべての新しい強制隔離は、Campaign Standard にレプリケートされます。Campaign Standard からのすべての新しい強制隔離は、Campaign v7 にレプリケートされます。これにより、すべての除外ルールが Campaign v7 と Campaign Standard との間で必ず同期されます。
* **[!UICONTROL `[ACS] Security group synchronization`]** (securityGroupSync):このワークフローは、権限の変換に使用されます。 詳しくは、権 [利変換を参照してください](#rights-conversion)。

以下のレプリケーションワークフローが「使用準備完了」テンプレートとして使用できます。Adobe Campaign コンサルタントによって実装される必要があります。

![](assets/acs_connect_implementation_2.png)

* **[!UICONTROL `[ACS] Profile replication`]** (newProfileReplication):この増分ワークフローは、受信者をCampaign Standardに複製します。 デフォルトでは、すべての標準の受信者フィールドをレプリケートします。デフォルトの受 [信者フィールドを参照してくださ](#default-recipient-fields)い。
* **[!UICONTROL `[ACS] Service replication`]** (newServiceReplication):この増分ワークフローは、選択したサービスをCampaign Standardに複製します。 「Webアプリケーションの同期」の使 [用例を参照してくださ](../../integrations/using/synchronizing-web-applications.md)い。
* **[!UICONTROL `[ACS] Landing pages replication`]** (newLandingPageReplication):この増分ワークフローは、選択したWebアプリケーションをCampaign Standardに複製します。 Campaign v7 Web アプリケーションは、Campaign Standard でランディングページとして表示されます。「Webアプリケーションの同期」の使 [用例を参照してくださ](../../integrations/using/synchronizing-web-applications.md)い。
* **[!UICONTROL `[ACS] New replication`]** (newReplication):この増分ワークフローは、カスタムテーブルの複製に使用できる例です。 詳しくは、 [高度な実装を参照してくださ](#advanced-implementation)い。
* **[!UICONTROL `[ACS] Delivery-mesage replication`]** (newDlvMsgQualification):この増分ワークフローは、配信メッセージをCampaign StandardからCampaign v7に複製します。
* **[!UICONTROL `[ACS] Profile delivery log replication`]** (newRcpDeliveryLogReplication):この増分ワークフローは、配信ID、電子メールの部分的なログ、電子メールの追跡ログをCampaign StandardからCampaign v7に複製します。 ここでは、Campaign Standard から Campaign v7 の nms:recipients テーブルの一部であるプロファイルに送信された配信のみが考慮されます。
* **[!UICONTROL `[ACS] New delivery log replication`]** (newRcpDeliveryLogReplication):この増分ワークフローは、配信ID、電子メールの部分的なログ、電子メールの追跡ログをCampaign StandardからCampaign v7に複製します。 ここでは、Campaign Standard から Campaign v7 の（nms:recipient 以外の定義する）特定のテーブルの一部であるプロファイルに送信された配信のみが考慮されます。

### デフォルトの受信者フィールド {#default-recipient-fields}

追加のフィールドまたはカスタムテーブル（トランザクションテーブルなど）がある場合、デフォルトではレプリケートされません。実行するには、高度な設定が必要です。詳しくは、 [高度な実装を参照してくださ](#advanced-implementation)い。

次に、基本的な実装でレプリケートされた受信者フィールドのリストを示します。これらは標準のフィールドです。

<table> 
 <tbody> 
  <tr> 
   <td> <strong>ラベル</strong><br /> </td> 
   <td> <strong>内部名</strong><br /> </td> 
  </tr> 
  <tr> 
   <td> ソース ID<br /> </td> 
   <td> @sourceId<br /> </td> 
  </tr> 
  <tr> 
   <td> 作成日<br /> </td> 
   <td> @created<br /> </td> 
  </tr> 
  <tr> 
   <td> 変更日<br /> </td> 
   <td> @lastModified<br /> </td> 
  </tr> 
  <tr> 
   <td> E メール<br /> </td> 
   <td> @email<br /> </td> 
  </tr> 
  <tr> 
   <td> 姓<br /> </td> 
   <td> @lastName<br /> </td> 
  </tr> 
  <tr> 
   <td> 名<br /> </td> 
   <td> @firstName<br /> </td> 
  </tr> 
  <tr> 
   <td> ミドルネーム<br /> </td> 
   <td> @middleName<br /> </td> 
  </tr> 
  <tr> 
   <td> モバイル<br /> </td> 
   <td> @mobilePhone<br /> </td> 
  </tr> 
  <tr> 
   <td> 生年月日<br /> </td> 
   <td> @birthDate<br /> </td> 
  </tr> 
  <tr> 
   <td> 性別<br /> </td> 
   <td> @gender<br /> </td> 
  </tr> 
  <tr> 
   <td> 敬称<br /> </td> 
   <td> @salutation<br /> </td> 
  </tr> 
  <tr> 
   <td> 今後の連絡は不要 (すべてのチャネル)<br /> </td> 
   <td> @blackList<br /> </td> 
  </tr> 
  <tr> 
   <td> 今後の E メールによる連絡は不要<br /> </td> 
   <td> @blackListEmail<br /> </td> 
  </tr> 
  <tr> 
   <td> 今後の SMS による連絡は不要<br /> </td> 
   <td> @blackListMobile<br /> </td> 
  </tr> 
  <tr> 
   <td> 電話<br /> </td> 
   <td> @phone<br /> </td> 
  </tr> 
  <tr> 
   <td> FAX<br /> </td> 
   <td> @fax<br /> </td> 
  </tr> 
  <tr> 
   <td> 住所 1 (建物名)<br /> </td> 
   <td> [location/@address1]<br /> </td> 
  </tr> 
  <tr> 
   <td> 住所 2<br /> </td> 
   <td> [location/@address2]<br /> </td> 
  </tr> 
  <tr> 
   <td> 住所 3 (番地)<br /> </td> 
   <td> [location/@address3]<br /> </td> 
  </tr> 
  <tr> 
   <td> 住所 4 (郡)<br /> </td> 
   <td> [location/@address4]<br /> </td> 
  </tr> 
  <tr> 
   <td> 郵便番号<br /> </td> 
   <td> [location/@zipCode]<br /> </td> 
  </tr> 
  <tr> 
   <td> 市区町村<br /> </td> 
   <td> [location/@city]<br /> </td> 
  </tr> 
  <tr> 
   <td> 都道府県コード<br /> </td> 
   <td> [location/@stateCode]<br /> </td> 
  </tr> 
  <tr> 
   <td> 国コード<br /> </td> 
   <td> [location/@countryCode]<br /> </td> 
  </tr> 
 </tbody> 
</table>

### 権限の変換 {#rights-conversion}

権限は、Campaign v7 と Campaign Standard で扱いが異なります。Campaign v7 では、権限管理は、フォルダーベースであるのに対して、Campaign Standard では、単位アクセス（組織／地理的単位）に基づいています。Campaign Standard ユーザーは、制限コンテキストのセキュリティグループに属します。そのため、Campaign v7 権限システムは、Campaign Standard のシステムに合わせて変換される必要があります。権限の変換を実行するには、いくつかの方法があります。次に実装の例を示します。

1. で、こ **[!UICONTROL Administration > ACS Connector > Rights management > Security groups]**&#x200B;のボタンを使 **[!UICONTROL Synchronize]** 用して、Campaign Standardのすべてのセキュリティグループを取得します。 標準の Campaign Standard グループは除外されます。

   ![](assets/acs_connect_implementation_4.png)

1. 権限管理がフォルダーベースの場合は、に進み、必要な各フォ **[!UICONTROL Administration > ACS Connector > Rights management > Folder mapping]** ルダーをセキュリティグループにマッピングします。

   ![](assets/acs_connect_implementation_5.png)

1. レプリケーションワークフローは、次にこの情報を使用して対応する組織／地理的単位を各オブジェクトに追加し、レプリケートします。

### 高度な実装 {#advanced-implementation}

ここでは、高度な実装の観点からいくつかの可能性を説明します。

>[!CAUTION]
>
>この情報は、一般的なガイドラインとしてのみ使用できます。実装については、Adobe Campaign コンサルタントにお問い合わせください。

高度な実装では、お客様のニーズに応じて、カスタムレプリケーションワークフローが追加されます。以下に、いくつかの例を示します。

* 配信レプリケーション
* キャンペーンレプリケーション
* プログラムレプリケーション
* シードメンバーレプリケーション
* トランザクションレプリケーション
* その他

**受信者の拡張フィールドのレプリケート**

基本的な実装では、標準の受信者フィールドがレプリケートされます。受信者スキーマに追加したカスタムフィールドをレプリケートする場合は、それらを識別する必要があります。

1. の下で、 **[!UICONTROL Administration > ACS Connector > Data mapping]**&#x200B;テーブルにターゲットマッピングを作成 **[!UICONTROL nms:recipient]** します。

   ![](assets/acs_connect_implementation_6.png)

1. レプリケートする追加のフィールドとその他の必要な情報（インデックス、リンク、識別キー）を選択します。

   ![](assets/acs_connect_implementation_7.png)

1. 専用のプロファイルレプリケーションワークフロー（テンプレートではなく、ワークフローインスタンス自体）を開きます。これらのフィールド **[!UICONTROL Query]** を含めるに **[!UICONTROL Update data]** は、アクティビティとを変更します。 See [Technical and replication workflows](#technical-and-replication-workflows).

   ![](assets/acs_connect_implementation_8.png)

   ![](assets/acs_connect_implementation_9.png)

**カスタムプロファイルテーブルのレプリケート**

基本的な実装では、標準の受信者テーブルがレプリケートされます。カスタム受信者テーブルを追加した場合、ここに、それらを識別する方法を示します。

1. の下で、カ **[!UICONTROL Administration > ACS Connector > Data mapping]**&#x200B;スタムプロファイルテーブルにターゲットマッピングを作成します。

   ![](assets/acs_connect_implementation_10.png)

1. レプリケートする識別データ、インデックス、リンクおよびフィールドを定義します。

   ![](assets/acs_connect_implementation_10.png)

1. 権限管理がフォルダベースの場合は、に進み、カスタムテ **[!UICONTROL Administration > ACS Connector > Rights management > Folder mapping]**&#x200B;ーブルにリンクされたフォルダのセキュリティグループを定義します。 詳しくは、権 [利変換を参照してください](#rights-conversion)。
1. Use the **[!UICONTROL New replication]** workflow (not the template, but the workflow instance itself) to include the custom table and the fields to replicate. See [Technical and replication workflows](#technical-and-replication-workflows).

