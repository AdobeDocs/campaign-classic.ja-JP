---
title: Campaign 統合について
description: アドビの各ソリューションが提供する様々な機能を Campaign と組み合わせることができます。
page-status-flag: never-activated
uuid: 087abdf0-b4b2-45e6-be21-b03bf85ddf83
contentOwner: sauviat
products: SG_CAMPAIGN/CLASSIC
audience: integrations
content-type: reference
topic-tags: campaign-integrations
discoiquuid: 0af1fd96-48ef-43c9-a03b-0f9a6e0e02fe
translation-type: tm+mt
source-git-commit: 4b98c23f4120cbea6dd54cd68b61202e74bee3e1
workflow-type: tm+mt
source-wordcount: '788'
ht-degree: 74%

---


# Get started with Adobe Campaign integrations {#about-campaign-integrations}

Adobe Experience Cloud は、共通データプラットフォーム上に構築され、強力なコアサービスの共通セットと統合されたクラス最高のソリューションの包括的なセットです。

Adobe Campaign と [Adobe Experience Cloud ソリューション](https://docs.adobe.com/content/help/ja-JP/core-services/interface/marketing-cloud-integrations.html)および[コアサービス](https://docs.adobe.com/content/help/ja-JP/core-services/interface/about-core-services/core-services.html)との間で使用可能な機能の統合について説明します。その後、ソリューションの実装を最新化し、Experience Cloud を実装して、顧客属性やオーディエンスなどの機能を使用できるようにします。

![](assets/ExCloud-solutions.png)

Adobe Campaign と統合できるアドビのソリューションとコアサービスの完全なリスト、および関連ドキュメントについては、[このページ](#experience-cloud-integrations)で参照できます。

>[!CAUTION]
>
>これらの統合のほとんどは、Adobe ID経由でログインするために、AdobeIdentity Managementシステム(IMS)を実装する必要があります。 [詳しくは、このページを参照してください](../../integrations/using/about-adobe-id.md)。


## ソリューションのリンク {#working-with-experience-cloud-solutions}

複数のソリューションをAdobe Experience Cloudにリンクできます。 The **organization** is the customer entity that enables an administrator to configure groups and users, and to control single sign-on (SSO) in Adobe Experience Cloud. 組織は、すべてのExperience Cloud製品とソリューションにわたるログイン会社のように機能します。 ほとんどの場合、組織は勤務先の会社名です。ただし、1 つの会社が多くの組織を持つことができます。

組織管理と Adobe Experience Cloud アカウントのリンク付けについて詳しくは、[Adobe Experience Cloud ヘルプポータル](https://docs.adobe.com/content/help/ja-JP/core-services/interface/manage-users-and-products/organizations.html)で説明しています。

## IDとcookieの管理 {#id-and-cookies}

When installing Adobe Campaign or integrating an existing installation with Adobe Experience Cloud, the [Adobe Experience Cloud Identity Service](https://docs.adobe.com/content/help/ja-JP/id-service/using/home.translate.html) is enabled. このサービスは、Adobe Campaign がトラッキング機能のために最初に使用した永続 Cookie を置き換えます。

Adobe Experience Cloudアイデンティティサービス（IDサービス）は、Experience Cloud内のすべてのソリューションにわたって訪問者を識別する、汎用の永続的なIDを提供します。

一意の訪問者IDが、トラッキングログを生成する受信者に割り当てられます。 この ID は **[!UICONTROL nms:trackingLogRcp]** テーブルの「**[!UICONTROL リクエスター UUID (@sourceID)]**」フィールドに保存されます。**したがって、訪問者IDサービスが実装される前に存在した受信者の追跡データは使用できなくなります**。

この ID は、他の Adobe Experience Cloud ソリューションに同じ [CNAME](https://docs.adobe.com/content/help/ja-JP/id-service/using/reference/analytics-reference/cname.html) で認識されます。

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
   <td> <strong>AdobeRTCDP(Real-time Customer Data Platform)</strong><br /> </td> 
   <td> The integration between Adobe Campaign and Adobe Real-time Customer Data Platform (RTCDP) allows you to share segments data and import audiences to Adobe Campaign.<br /> <p>Campaign とアドビのリアルタイムカスタマーデータプラットフォーム（CDP）の統合について詳しくは、<a href="https://docs.adobe.com/content/help/ja-JP/experience-platform/rtcdp/destinations/destinations-cat/adobe-destinations/adobe-campaign-destination.html">こちら</a>を参照してください。</p><br /> </td> 
  </tr> 
  <tr> 
   <td> <strong>AdobeIdentity Managementシステム(IMS) -Adobe ID</strong><br /> </td> 
   <td> 他の Adobe Experience Cloud ソリューションと同じ Adobe ID を使用して Adobe Campaign に接続することができます。<br />Adobe Experience Cloud の統合、特にコアサービスにリンクした特定の機能を使用するには、Adobe ID を使用してログインする必要があります。<br /> <p>Adobe Campaign での Adobe ID の実装について詳しくは、<a href="../../integrations/using/about-adobe-id.md">こちら</a>を参照してください。</p><br /> </td> 
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
   <td> <strong>People コアサービス</strong><br /> <strong>Adobe Audience Manager</strong><br /> </td> 
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
   <td> <strong>Triggers コアサービス</strong>と Adobe Campaign を統合すると、Web サイト上で Adobe Analytics によってトラッキングされている特定の動作に対する反応としてパーソナライズされた E メールを送信できます。<br /> <p>Adobe Campaign と Experience Cloud Triggers の統合について詳しくは、<a href="https://helpx.adobe.com/jp/campaign/kb/triggers-and-campaign.html">こちら</a>を参照してください。</p><br /> </td> 
  </tr> 
  <tr> 
   <td> <strong>Adobe Analytics - Data コネクタ</strong><br /> </td> 
   <td> <strong>Data コネクタ</strong>（旧 Adobe Genesis）を使用すると、Adobe Campaign と Adobe Analytics の間で、E メールキャンペーン後のユーザー行動に関するセグメントを介したインタラクションが可能になります。反対に、Adobe Campaign から配信された E メールキャンペーンの指標と属性を Adobe Analytics - Data コネクタに送信します。<br /> <p>Campaign と Data コネクタの統合について詳しくは、<a href="../../platform/using/adobe-analytics-data-connector.md">こちら</a>を参照してください。</p><br /> </td> 
  </tr> 
 </tbody> 
</table>

