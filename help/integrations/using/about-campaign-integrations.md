---
product: campaign
title: Campaign 統合について
description: アドビの各ソリューションが提供する様々な機能を Campaign と組み合わせることができます
feature: Overview
badge-v7: label="v7" type="Informative" tooltip="Campaign Classic v7 に適用されます"
badge-v8: label="v8" type="Positive" tooltip="Campaign v8 にも適用されます"
audience: integrations
content-type: reference
topic-tags: campaign-integrations
exl-id: ceb584da-bc97-4b71-9499-59df5e6d10c3
source-git-commit: 3a9b21d626b60754789c3f594ba798309f62a553
workflow-type: tm+mt
source-wordcount: '774'
ht-degree: 100%

---

# Adobe Campaign 統合の基本を学ぶ {#about-campaign-integrations}



Adobe Experience Cloud は、共通データプラットフォーム上に構築され、強力なコアサービスの共通セットと統合されたクラス最高のソリューションの包括的なセットです。

Adobe Campaign と [Adobe Experience Cloud ソリューション](https://experienceleague.adobe.com/docs/core-services/interface/marketing-cloud-integrations.html?lang=ja)および[コアサービス](https://experienceleague.adobe.com/docs/core-services/interface/about-core-services/core-services.html?lang=ja)との間で使用可能な機能の統合について説明します。その後、ソリューションの実装を最新化し、Experience Cloud を実装して、顧客属性やオーディエンスなどの機能を使用できるようにします。

![](assets/ExCloud-solutions.png)

Adobe Campaign と統合できるアドビのソリューションとコアサービスの完全なリスト、および関連ドキュメントについては、[このページ](#experience-cloud-integrations)で参照できます。

>[!CAUTION]
>
>これらの統合のほとんどでは、Adobe ID 経由でログインするために、Adobe Identity Management システム（IMS）を実装する必要があります。詳しくは、[このページ](../../integrations/using/about-adobe-id.md)を参照してください。
>

## ソリューションのリンク {#working-with-experience-cloud-solutions}

複数のソリューションを Adobe Experience Cloud にリンクできます。**組織**&#x200B;とは、管理者がグループとユーザーを設定し、Adobe Experience Cloud でのシングルサインオン（SSO）を制御できる顧客エンティティのことです。組織は、すべての Experience Cloud 製品およびソリューションにまたがるログイン会社のように動作します。ほとんどの場合、組織は勤務先の会社名です。ただし、1 つの会社が多くの組織を持つことができます。

組織管理と Adobe Experience Cloud アカウントのリンク付けについて詳しくは、[Adobe Experience Cloud ヘルプポータル](https://experienceleague.adobe.com/docs/core-services/interface/manage-users-and-products/organizations.html?lang=ja)で説明しています。

## ID と Cookie の管理 {#id-and-cookies}

Adobe Campaign をインストールする場合、または既存のインストールを Adobe Experience Cloud に統合する場合、[Adobe Experience Cloud ID サービス](https://experienceleague.adobe.com/docs/id-service/using/home.html?lang=ja)は有効になっています。このサービスは、Adobe Campaign がトラッキング機能のために最初に使用した永続 Cookie を置き換えます。

Adobe Experience Cloud ID サービス（ID サービス）は、Experience Cloud 内のすべてのソリューションをまたいで訪問者を識別する、永続的な汎用 ID を提供します。

固有の訪問者 ID が受信者に割り当てられ、トラッキングログが生成されます。この ID は **[!UICONTROL nms:trackingLogRcp]** テーブルの「**[!UICONTROL リクエスター UUID (@sourceID)]**」フィールドに保存されます。**そのため、訪問者 ID サービスが実装される前に存在していた受信者のトラッキングデータは、これ以降使用することはできません。**

この ID は、他の Adobe Experience Cloud ソリューションにより、同じ CNAME で認識されます。[詳細情報](https://experienceleague.adobe.com/docs/id-service/using/reference/analytics-reference/cname.html?lang=ja)

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
   <td> <strong>アドビのリアルタイムカスタマーデータプラットフォーム（RTCDP）</strong><br /> </td> 
   <td> Adobe Campaign とアドビのリアルタイムカスタマーデータプラットフォーム（RTCDP）の統合により、セグメントデータを共有し、オーディエンスを Adobe Campaign にインポートできます。<br /> <p>Campaign とアドビのリアルタイム顧客データプラットフォーム（CDP）の統合について詳しくは、<a href="../../integrations/using/get-started-sources-destinations.md">こちら</a>を参照してください。</p><br /> </td> 
  </tr> 
  <tr> 
   <td> <strong>Adobe Identity Management システム（IMS）- Adobe ID</strong><br /> </td> 
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
   <td> <strong>Adobe Analytics Connector</strong><br /> </td> 
   <td> <strong>Adobe Analytics コネクタ</strong>を使用すると、メールキャンペーン後のユーザー行動に関するセグメントについて、Adobe Campaign と Adobe Analytics を連携させることができます。このコネクタは、Adobe Campaign から配信された メールキャンペーンの指標と属性を Adobe Analytics に送信します。<br /> <p>Campaign と Analytics のコネクタでの統合に関する<a href="../../platform/using/adobe-analytics-connector.md">詳細情報</a>。</p><br /> </td> 
  </tr> 
 </tbody> 
</table>
