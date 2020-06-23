---
title: Campaign 統合について
description: 現行バージョンの Adobe Campaign と Adobe Experience Cloud ソリューションとの間で使用可能な機能の統合について説明します。
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
source-git-commit: 0c3737b22c7bf4e614c5a2fbe8e8fd954d3ece8a
workflow-type: tm+mt
source-wordcount: '783'
ht-degree: 96%

---


# Campaign 統合について {#about-campaign-integrations}

Adobe Experience Cloud は、共通データプラットフォーム上に構築され、強力なコアサービスの共通セットと統合されたクラス最高のソリューションの包括的なセットです。

Adobe Campaign と [Adobe Experience Cloud ソリューション](https://docs.adobe.com/content/help/ja-JP/core-services/interface/marketing-cloud-integrations.html)および[コアサービス](https://docs.adobe.com/content/help/ja-JP/core-services/interface/about-core-services/core-services.html)との間で使用可能な機能の統合について説明します。その後、ソリューションの実装を最新化し、Experience Cloud を実装して、顧客属性やオーディエンスなどの機能を使用できるようにします。

Adobe Campaign と統合できるアドビのソリューションとコアサービスの完全なリスト、および関連ドキュメントについては、[このページ](#experience-cloud-integrations)で参照できます。

![](assets/ExCloud-solutions.png)


>[!CAUTION]
>
>ほとんどの場合、これらの統合作業をおこなうには Adobe ID（IMS）を使用してログインする必要があります。この実装について詳しくは、[このページ](../../integrations/using/about-adobe-id.md)を参照してください。
>
>IMS の実装は複雑なプロセスで、長くなる場合があります。この作業をおこなうのはアドビの技術管理者に限られます。

## ソリューションのリンク {#working-with-experience-cloud-solutions}

環境によっては、Adobe Experience Cloud に複数のソリューションをリンクすることができます。これらは組織としてリンクされます。**組織**&#x200B;とは、管理者がグループとユーザーを設定し、Experience Cloud でのシングルサインオンを制御できるエンティティのことです。組織は、すべての Experience Cloud 製品およびソリューションにまたがるログイン会社のように機能します。ほとんどの場合、組織は勤務先の会社名です。ただし、1 つの会社が多くの組織を持つことができます。

組織管理と Adobe Experience Cloud アカウントのリンク付けについて詳しくは、[Adobe Experience Cloud ヘルプポータル](https://docs.adobe.com/content/help/en/core-services/interface/manage-users-and-products/organizations.html)で説明しています。

>[!CAUTION]
>
>Adobe Campaign を新規にインストールする場合、または既存のインストールを Adobe Experience Cloud に統合する場合、[Experience Cloud ID サービス](https://docs.adobe.com/content/help/en/id-service/using/home.html)は有効になっています。このサービスは、Adobe Campaign がトラッキング機能のために最初に使用した永続 Cookie を置き換えます。
>
>次に、固有の訪問者 ID が受信者に割り当てられ、トラッキングログが生成されます。この ID は **[!UICONTROL nms:trackingLogRcp]** テーブルの「**[!UICONTROL リクエスター UUID (@sourceID)]**」フィールドに保存されます。そのため、訪問者 ID サービスが実装される前に存在していた受信者のトラッキングデータは、これ以降使用することはできません。
>
>この ID は、他の Adobe Experience Cloud ソリューションに同じ [CNAME](https://docs.adobe.com/content/help/en/id-service/using/reference/analytics-reference/cname.html) で認識されます。

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
   <td> <strong>アドビのリアルタイムカスタマーデータプラットフォーム（CDP）</strong><br /> </td> 
   <td> Adobe Campaign とアドビのリアルタイムカスタマーデータプラットフォーム（CDP）の統合により、セグメントデータを共有し、オーディエンスを Adobe Campaign にインポートできます。<br /> <p>Campaign とアドビのリアルタイムカスタマーデータプラットフォーム（CDP）の統合について詳しくは、<a href="https://docs.adobe.com/content/help/ja-JP/experience-platform/rtcdp/destinations/destinations-cat/adobe-destinations/adobe-campaign-destination.html">こちら</a>を参照してください。</p><br /> </td> 
  </tr> 
  <tr> 
   <td> <strong>IMS - Adobe ID</strong><br /> </td> 
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

