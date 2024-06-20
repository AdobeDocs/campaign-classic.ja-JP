---
product: campaign
title: Campaign 統合について
description: アドビの各ソリューションが提供する様々な機能を Campaign と組み合わせることができます
feature: Overview
badge-v8: label="v8 にも適用されます" type="Positive" tooltip="Campaign v8 にも適用されます"
audience: integrations
content-type: reference
topic-tags: campaign-integrations
exl-id: ceb584da-bc97-4b71-9499-59df5e6d10c3
source-git-commit: 597d24fa780a324507c56c55a5309b6ee1cf46eb
workflow-type: tm+mt
source-wordcount: '709'
ht-degree: 46%

---

# Adobe Campaign 統合の基本を学ぶ {#about-campaign-integrations}

Adobe Experience Cloudは、共通の強力なソリューションやアプリのセットを備え、共通のデータプラットフォーム上に構築された、クラス最高の統合ソリューションの包括的なセットです。

Adobe CampaignとAdobe Experience Cloud ソリューション間で利用できる機能統合について詳しくは、を参照してください。 [このページ](https://experienceleague.adobe.com/en/docs/core-services/interface/administration/integrations){_blank}.

Adobe Campaignと統合できるAdobeソリューションおよびアプリケーションサービスの完全なリストと関連ドキュメントについては、を参照してください [この節](#experience-cloud-integrations).

>[!CAUTION]
>
>これらの統合機能を使用するには、AdobeのIdentity Management System （IMS）を実装し、Adobe ID経由でログインする必要があります。 詳しくは、[このページ](../../integrations/using/about-adobe-id.md)を参照してください。
>

## ソリューションのリンク {#working-with-experience-cloud-solutions}

複数のソリューションを Adobe Experience Cloud にリンクできます。**組織**&#x200B;とは、管理者がグループとユーザーを設定し、Adobe Experience Cloud でのシングルサインオン（SSO）を制御できる顧客エンティティのことです。組織は、すべての Experience Cloud 製品およびソリューションにまたがるログイン会社のように動作します。ほとんどの場合、組織は勤務先の会社名です。ただし、1 つの会社が多くの組織を持つことができます。

組織の管理とAdobe Experience Cloud アカウントのリンクについて詳しくは、以下を参照してください [Adobe Experience Cloud ヘルプポータル](https://experienceleague.adobe.com/en/docs/core-services/interface/administration/organizations){_blank}.

## ID と Cookie の管理 {#id-and-cookies}

Adobe Campaignのインストール時、または既存のインストールとAdobe Experience Cloudの統合時に、 [Adobe Experience Cloud ID サービス](https://experienceleague.adobe.com/en/docs/id-service/using/home){_blank} が有効になっています。 このサービスは、Adobe Campaign がトラッキング機能のために最初に使用した永続 Cookie を置き換えます。

Adobe Experience Cloud ID サービス（ID サービス）は、Experience Cloud 内のすべてのソリューションをまたいで訪問者を識別する、永続的な汎用 ID を提供します。

固有の訪問者 ID が受信者に割り当てられ、トラッキングログが生成されます。この ID は **[!UICONTROL nms:trackingLogRcp]** テーブルの「**[!UICONTROL リクエスター UUID (@sourceID)]**」フィールドに保存されます。**そのため、訪問者 ID サービスが実装される前に存在していた受信者のトラッキングデータは、これ以降使用することはできません。**

この ID は、他の Adobe Experience Cloud ソリューションにより、同じ CNAME で認識されます。[詳細情報](https://experienceleague.adobe.com/en/docs/id-service/using/reference/analytics-reference/cname){_blank}.

## Experience Cloud との統合 {#experience-cloud-integrations}

次の表から、使用可能な Experience Cloud 統合ドキュメントにアクセスできます。

<table> 
 <thead> 
  <tr> 
   <th> ソリューションとアプリ<br /> </th> 
   <th> ユースケース<br /> </th> 
  </tr> 
 </thead> 
 <tbody> 
  <tr> 
   <td> <strong>アドビのリアルタイムカスタマーデータプラットフォーム（RTCDP）</strong><br /> </td> 
   <td> Adobe CampaignとAdobe Real-time Customer Data Platform（RTCDP）の統合を設定して、セグメントデータを共有し、オーディエンスをAdobe Campaignに読み込みます。<br /> <p>Campaign とアドビのリアルタイム顧客データプラットフォーム（CDP）の統合について詳しくは、<a href="../../integrations/using/get-started-sources-destinations.md">こちら</a>を参照してください。</p><br /> </td> 
  </tr> 
  <tr> 
   <td> <strong>Adobe Identity Management システム（IMS）- Adobe ID</strong><br /> </td> 
   <td> Adobe IMSを設定し、他のAdobe Experience Cloud ソリューションと同じAdobe IDでAdobe Campaignに接続します。<br /> Adobe Experience Cloud統合にリンクされた特定の機能を使用するには、Adobe IDを使用してログインする必要があります。<br /> <p>Adobe Campaign での Adobe ID の実装について詳しくは、<a href="../../integrations/using/about-adobe-id.md">こちら</a>を参照してください。</p><br /> </td> 
  </tr> 
  <tr> 
   <td> <strong>Adobe Experience Manager</strong><br /> </td> 
   <td> この統合を設定すると、Adobe Campaign データベースに直接マッピングされたメールコンテンツまたはフォームをで作成できます。 <strong>Adobe Experience Manager</strong>.<br /> <p>Adobe Campaign と Adobe Experience Manager の統合について詳しくは、<a href="../../integrations/using/about-adobe-experience-manager.md">こちら</a>を参照してください。</p><br /> </td> 
  </tr> 
  <tr> 
   <td> <strong>Adobe Target</strong><br /> </td> 
   <td> によって動的に計算される画像を挿入する場合は、この統合を設定します。 <strong>Adobe Target</strong> Adobe Campaignが作成および送信した電子メールが開封された時点。<br /> <p>Adobe Campaign と Adobe Target の統合について詳しくは、<a href="../../integrations/using/integrating-with-adobe-target.md">こちら</a>を参照してください。</p><br /> </td> 
  </tr> 
  <tr> 
   <td><strong>Adobe Audience Manager</strong><br /> </td> 
   <td> この統合を設定すると、Adobe Experience Cloud ソリューションと使用するアプリ間でオーディエンスを共有できます。<br /> <p><a href="../../integrations/using/sharing-audiences-with-adobe-experience-cloud.md">詳細情報</a> Adobe CampaignとAdobe Audience Managerの統合について</p><br /> </td> 
  </tr> 
  <tr> 
   <td> <strong>アセット</strong><br /> </td> 
   <td> この統合を設定すると、Adobe Campaign ライブラリからAdobe Experience Cloudで作成されたメールとランディングページにアセットを挿入できます。<br /> <p><a href="../../integrations/using/configuring-access-to-assets.md#integrating-with-experience-cloud-assets">詳細情報</a> Adobe Campaignについて – Assets の統合</p><br /> </td> 
  </tr> 
  <tr> 
   <td> <strong>AEM Assets</strong><br /> </td> 
   <td> からアセットを挿入するには、この統合を設定 <strong>AEM Assets</strong> Adobe Campaignで作成されたメールおよびランディングページへのライブラリ。<br /> <p>Adobe Campaign と AEM Assets の統合について詳しくは、<a href="../../integrations/using/configuring-access-to-assets.md#integrating-with-aem-assets">こちら</a>を参照してください。</p><br /> </td> 
  </tr> 
  <tr> 
   <td> <strong>Experience Cloud Triggers</strong><br /> </td> 
   <td> 間の統合の設定 <strong>Adobe Experience Cloud Triggers</strong> さらに、Adobe Analyticsによって web サイト上でトラッキングされる特定の行動に対する反応として、パーソナライズされたメールを顧客に送信するAdobe Campaignも用意されています。<br /> <p>Adobe Campaign と Experience Cloud Triggers の統合について詳しくは、<a href="about-triggers.md">こちら</a>を参照してください。</p><br /> </td> 
  </tr> 
  <tr> 
   <td> <strong>Adobe Analytics Connector</strong><br /> </td> 
   <td> この統合を設定すると、メールキャンペーン後のユーザー行動に関するセグメントについて、Adobe CampaignとAdobe Analyticsがやり取りできるようになります。 このコネクタは、Adobe Campaign から配信された メールキャンペーンの指標と属性を Adobe Analytics に送信します。<br /> <p>Campaign と Analytics のコネクタでの統合に関する<a href="../../integrations/using/gs-aa.md">詳細情報</a>。</p><br /> </td> 
  </tr> 
 </tbody> 
</table>
