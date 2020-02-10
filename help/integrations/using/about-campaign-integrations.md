---
title: Campaign 統合について
description: 現在のバージョンのAdobe Campaignと[Adobe Experience cloudソリューション間で使用できる機能統合について説明します。
page-status-flag: never-activated
uuid: 087abdf0-b4b2-45e6-be21-b03bf85ddf83
contentOwner: sauviat
products: SG_CAMPAIGN/CLASSIC
audience: integrations
content-type: reference
topic-tags: campaign-integrations
discoiquuid: 0af1fd96-48ef-43c9-a03b-0f9a6e0e02fe
index: y
internal: n
snippet: y
translation-type: tm+mt
source-git-commit: 2e16d4de068f8cb1e61069aa53626f7bf7021466

---


# Campaign 統合について{#about-campaign-integrations}

現行バージョンの Adobe Campaign と [Adobe Experience Cloud ソリューション](https://marketing.adobe.com/resources/help/en_US/mcloud/marketing-cloud-integrations.html)および[コアサービス](https://marketing.adobe.com/resources/help/en_US/mcloud/core-services-landing.html)との間で使用可能な機能の統合について説明します。

Adobe Experience Cloud は、共通データプラットフォーム上に構築され、強力なコアサービスの共通セットと統合されたクラス最高のソリューションの包括的なセットです。

Adobe Campaign と統合できるアドビのソリューションおよびコアサービスの完全なリスト、および関連ドキュメントについては、[このページ](#experience-cloud-integrations)を参照してください。

>[!CAUTION]
>
>ほとんどの場合、これらの統合作業をおこなうには Adobe ID（IMS）を使用してログインする必要があります。この実装について詳しくは、[このページ](../../integrations/using/about-adobe-id.md)を参照してください。
>
>IMS の実装は複雑な作業であり、時間がかかるので、事前の計画が必要になります。この作業をおこなうのはアドビの技術管理者に限られます。

## Experience Cloud ソリューションの操作 {#working-with-experience-cloud-solutions}

環境によっては、Adobe Experience Cloud に複数のソリューションをリンクすることができます。これらは組織としてリンクされます。**組織**&#x200B;とは、管理者がグループとユーザーを設定し、Experience Cloud でのシングルサインオンを制御できるエンティティのことです。組織は、すべての Experience Cloud 製品およびソリューションにまたがるログイン会社のように機能します。ほとんどの場合、組織は勤務先の会社名です。ただし、1 つの会社が多くの組織を持つことができます。

組織管理と Adobe Experience Cloud アカウントのリンク付けについて詳しくは、[Adobe Experience Cloud ヘルプポータル](https://marketing.adobe.com/resources/help/en_US/mcloud/organizations.html)で説明しています。

>[!CAUTION]
>
>Adobe Campaign を新規にインストールする場合、または既存のインストールを Adobe Experience Cloud に統合する場合、[Experience Cloud ID サービス](https://marketing.adobe.com/resources/help/en_US/mcvid/)は有効になっています。このサービスは、Adobe Campaign がトラッキング機能のために最初に使用した永続 Cookie を置き換えます。
>
>次に、固有の訪問者 ID が受信者に割り当てられ、トラッキングログが生成されます。このIDは、テーブルのフィール **[!UICONTROL Requester UUID (@sourceID)]** ドに保存され **[!UICONTROL nms:trackingLogRcp]** ます。 そのため、訪問者 ID サービスが実装される前に存在していた受信者のトラッキングデータは、これ以降使用することはできません。
>
>この ID は、他の Adobe Experience Cloud ソリューションに同じ [CNAME](https://marketing.adobe.com/resources/help/en_US/mcvid/mcvid_cname.html) で認識されます。

## Experience Cloud との統合 {#experience-cloud-integrations}

次の表から、使用可能な Experience Cloud 統合ドキュメントにアクセスできます。

<table> 
 <thead> 
  <tr> 
   <th> ソリューションおよびコアサービス<br /> </th> 
   <th> 使用例<br /> </th> 
  </tr> 
 </thead> 
 <tbody> 
  <tr> 
   <td> <strong>Adobe Campaign Standard</strong>（Prime）<br /> </td> 
   <td> <strong>Campaign Standard</strong> にデータをレプリケートして、両方のアプリケーションの優れた機能を連携させることができます。Campaign Classic v7 には、プライマリマーケティングデータベースを管理するための高度なツールがあります。Campaign Classic v7 からのデータレプリケーションにより、Campaign Standard の使いやすい環境でリッチデータを活用できます。<br /><p> Adobe Campaign Classic と Adobe Campaign Standard の統合について詳しくは、<a href="../../integrations/using/acs-connector-principles-and-data-cycle.md">こちら</a>を参照してください。</p><br /></td> 
  </tr> 
  <tr> 
   <td> <strong>IMS - Adobe ID</strong><br /> </td> 
   <td> 他の Adobe Experience Cloud ソリューションと同じ Adobe ID を使用して Adobe Campaign に接続することができます。<br /> Adobe Experience cloud統合（特にコアサービス）にリンクされた特定の機能を使用するには、Adobe IDを使用してログインする必要があります。<br /> <p>Adobe Campaign での Adobe ID の実装について詳しくは、<a href="../../integrations/using/about-adobe-id.md">こちら</a>を参照してください。</p><br /> </td> 
  </tr> 
  <tr> 
   <td> <strong>Adobe Experience Manager</strong><br /> </td> 
   <td> E メールコンテンツや Adobe Campaign データベースにマッピングされたフォームを <strong>Adobe Experience Manager</strong> で直接作成することができます。<br /> <p>Adobe Campaign と Adobe Experience Manager の統合について詳しくは、<a href="../../integrations/using/about-adobe-experience-manager.md">こちら</a>を参照してください。</p><br /> </td> 
  </tr> 
  <tr> 
   <td> <strong>Adobe Target</strong><br /> </td> 
   <td> Adobe Campaign で作成、送信された E メールが開封されたときに <strong>Adobe Target</strong> が動的に自動生成した画像を挿入することができます。<br /> <p>Adobe Campaign と Adobe Target の統合について詳しくは、<a href="../../integrations/using/integrating-with-adobe-target.md">こちら</a>を参照してください。</p><br /> </td> 
  </tr> 
  <tr> 
   <td> <strong>Peopleコアサービス</strong><br /><strong>Adobe Audience Manager</strong><br /> </td> 
   <td> Adobe Experience Cloud ソリューションと使用しているコアとの間でオーディエンスを共有できます。<br /> <p>Adobe Campaign と People コアサービスおよび Adobe Audience Manager の統合について詳しくは、<a href="../../integrations/using/sharing-audiences-with-adobe-experience-cloud.md">こちら</a>を参照してください。</p><br /> </td> 
  </tr> 
  <tr> 
   <td> <strong>Assets コアサービス</strong><br /> </td> 
   <td> Adobe Campaign で作成した E メールとランディングページに Adobe Experience Cloud ライブラリからアセットを挿入することができます。<br /> <p>Adobe Campaign と Assets コアサービスの統合について詳しくは、<a href="../../integrations/using/configuring-access-to-assets.md#integrating-with-experience-cloud-assets">こちら</a>を参照してください。</p><br /> </td> 
  </tr> 
  <tr> 
   <td> <strong>AEM Assets</strong><br /> </td> 
   <td> Adobe Campaign で作成した E メールとランディングページに <strong>AEM Assets</strong> ライブラリからアセットを挿入することができます。<br /> <p>Adobe Campaign と AEM Assets の統合について詳しくは、<a href="../../integrations/using/configuring-access-to-assets.md#integrating-with-aem-assets">こちら</a>を参照してください。</p><br /> </td> 
  </tr> 
  <tr> 
   <td> <strong>Experience Cloud Triggers</strong><br /> </td> 
   <td> <strong>Triggers コアサービス</strong>と Adobe Campaign を統合すると、Web サイト上で Adobe Analytics によってトラッキングされている特定の動作に対する反応としてパーソナライズされた E メールを送信できます。詳しくは、この<a href="https://helpx.adobe.com/campaign/kb/triggers-and-campaign.html">記事</a>を参照してください。<br /> <p>Adobe Campaign と Experience Cloud Triggers の統合について詳しくは、<a href="https://helpx.adobe.com/campaign/kb/triggers-and-campaign.html">こちら</a>を参照してください。</p><br /> </td> 
  </tr> 
  <tr> 
   <td> <strong>Adobe Analytics - Data コネクタ</strong><br /> </td> 
   <td> <strong>Data コネクタ</strong>（旧 Adobe Genesis）を使用すると、Adobe Campaign と Adobe Analytics の間で、E メールキャンペーン後のユーザー行動に関するセグメントを介したインタラクションが可能になります。反対に、Adobe Campaign から配信された E メールキャンペーンの指標と属性を Adobe Analytics - Data コネクタに送信します。<br /> <p>Campaign と Data コネクタの統合について詳しくは、<a href="../../platform/using/adobe-analytics-data-connector.md">こちら</a>を参照してください。</p><br /> </td> 
  </tr> 
  <tr> 
   <td> <strong>Adobe Real-time Customer Data Platform</strong><br /> </td> 
   <td> Adobe CampaignとAdobe Real-time Customer Data Platformの統合により、セグメントデータを共有し、オーディエンスをAdobe Campaignにインポートできます。<br /> <p><a href="https://docs.adobe.com/content/help/en/experience-platform/rtcdp/destinations/destinations-cat/adobe-destinations/adobe-campaign-destination.html">キャンペーン</a> - Adobe Real-time Customer Data Platform統合について詳しく説明します。</p><br /> </td> 
  </tr> 
 </tbody> 
</table>

