---
product: campaign
title: Campaign 統合について
description: アドビの各ソリューションが提供する様々な機能を Campaign と組み合わせることができます
feature: Overview
badge-v8: label="v8 にも適用されます" type="Positive" tooltip="Campaign v8 にも適用されます"
audience: integrations
content-type: reference
level: Intermediate, Experienced
topic-tags: campaign-integrations
exl-id: ceb584da-bc97-4b71-9499-59df5e6d10c3
TQID: https://experienceleague.adobe.com/PUFoWjnwax8oHM3dH-FJDH7b26p4qNBMaJfm2qWGNz0
product_v2: id: dfc56824-e8b9-499e-85d4-21aedb507314
feature_v2: id: a075b2c1-7748-4328-b7f6-343aa314616aid: d5ef99fa-df0c-4153-bf94-105ad0724167
subfeature_v2: id: b1fd1501-3105-4d6b-b4d4-9af53126df75id: c3bf7e1e-1db5-4c72-9293-e2f0b1ab73d0id: df0d6518-6f49-46e2-b46e-3bcc513f553f
level_v2: id: b5a62a22-46f7-4f0d-b151-3fc640bef588
topic_v2: id: eddd9b14-83bd-4ff4-9072-54a4a484abb7
source-git-commit: 4c295c0dabae8aba298390a3da2422a3fa1219f9
workflow-type: tm+mt
source-wordcount: 744
ht-degree: 92%

---

# Adobe Campaign 統合の基本を学ぶ {#about-campaign-integrations}

Adobe Experience Cloud は、強力なソリューションとアプリの共通セットを使用して、共通データプラットフォーム上に構築された、クラス最高の統合ソリューションの包括的なセットです。

Adobe Campaign と Adobe Experience Cloud ソリューション間で使用できる機能統合について詳しくは、[このページ](https://experienceleague.adobe.com/ja/docs/core-services/interface/administration/integrations){_blank}を参照してください。

Adobe Campaign と統合できるアドビのソリューションとアプリサービスの完全なリスト、および関連ドキュメントについては、[この節](#experience-cloud-integrations)を参照してください。

>[!CAUTION]
>
>これらの統合では、Adobe ID 経由でログインするために、Adobe Identity Management System（IMS）を実装する必要があります。 詳しくは、[このページ](../../integrations/using/about-adobe-id.md)を参照してください。
>

## ソリューションのリンク {#working-with-experience-cloud-solutions}

複数のソリューションを Adobe Experience Cloud にリンクできます。 **組織**&#x200B;とは、管理者がグループとユーザーを設定し、Adobe Experience Cloud でのシングルサインオン（SSO）を制御できる顧客エンティティのことです。 組織は、すべての Experience Cloud 製品およびソリューションにまたがるログイン会社のように動作します。 ほとんどの場合、組織は勤務先の会社名です。 ただし、1 つの会社が多くの組織を持つことができます。

組織管理と Adobe Experience Cloud アカウントのリンク付けについて詳しくは、[Adobe Experience Cloud ヘルプポータル](https://experienceleague.adobe.com/ja/docs/core-services/interface/administration/organizations){_blank}で説明しています。

## ID と Cookie の管理 {#id-and-cookies}

Adobe Campaign をインストールする場合、または既存のインストールを Adobe Experience Cloud に統合する場合、[Adobe Experience Cloud ID サービス](https://experienceleague.adobe.com/ja/docs/id-service/using/home){_blank}は有効になっています。 このサービスは、Adobe Campaign がトラッキング機能のために最初に使用した永続 Cookie を置き換えます。

Adobe Experience Cloud ID サービス（ID サービス）は、Experience Cloud 内のすべてのソリューションをまたいで訪問者を識別する、永続的な汎用 ID を提供します。

ユニーク訪問者 ID が受信者に割り当てられ、トラッキングログが生成されます。 このIDは、**[!UICONTROL nms:trackingLogRcp]** テーブルの&#x200B;**[!UICONTROL 依頼者UUID （@sourceID）]** フィールドに保存されます。 **そのため、訪問者 ID サービスが実装される前に存在していた受信者のトラッキングデータは、これ以降使用することはできません。**

この ID は、他の Adobe Experience Cloud ソリューションにより、同じ CNAME で認識されます。 [詳細情報](https://experienceleague.adobe.com/ja/docs/id-service/using/reference/analytics-reference/cname){_blank}。

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
   <td> Adobe Campaign と Adobe Real-time Customer Data Platform（RTCDP）間の統合を設定すると、セグメントデータを共有して、オーディエンスを Adobe Campaign にインポートできます。<br /> <p>Campaign とアドビのリアルタイム顧客データプラットフォーム（CDP）の統合について詳しくは、<a href="../../integrations/using/get-started-sources-destinations.md">こちら</a>を参照してください。</p><br /> </td> 
  </tr> 
  <tr> 
   <td> <strong>Adobe Identity Management システム（IMS）- Adobe ID</strong><br /> </td> 
   <td> 他のAdobe Experience Cloud ソリューションと同じAdobe IDを使用してAdobe Campaignに接続するようにAdobe IMSを構成します。<br /> Adobe Experience Cloud統合に関連する特定の機能を使用するには、Adobe IDを使用してログインする必要があります。<br /> <p>Adobe Campaign での Adobe ID の実装について詳しくは、<a href="../../integrations/using/about-adobe-id.md">こちら</a>を参照してください。</p><br /> </td> 
  </tr> 
  <tr> 
   <td> <strong>Adobe Experience Manager</strong><br /> </td> 
   <td> Adobe Campaign データベースにマッピングされたメールコンテンツやフォームを <strong>Adobe Experience Manager</strong> で直接作成するには、この統合を設定します。<br /> <p>Adobe Campaign と Adobe Experience Manager の統合について詳しくは、<a href="../../integrations/using/about-adobe-experience-manager.md">こちら</a>を参照してください。</p><br /> </td> 
  </tr> 
  <tr> 
   <td> <strong>Adobe Target</strong><br /> </td> 
   <td> Adobe Campaign で作成、送信されたメールが開封されたときに <strong>Adobe Target</strong> が動的に自動生成した画像を挿入するには、この統合を設定します。<br /> <p>Adobe Campaign と Adobe Target の統合について詳しくは、<a href="../../integrations/using/integrating-with-adobe-target.md">こちら</a>を参照してください。</p><br /> </td> 
  </tr> 
  <tr> 
   <td><strong>Adobe Audience Manager</strong><br /> </td> 
   <td> Adobe Experience Cloud ソリューションと使用するアプリとの間でオーディエンスを共有するには、この統合を設定します。<br /> <p>Adobe Campaign と Adobe Audience Manager の統合について詳しくは、<a href="../../integrations/using/sharing-audiences-with-adobe-experience-cloud.md">こちら</a>を参照してください。</p><br /> </td> 
  </tr> 
  <tr> 
   <td> <strong>Assets</strong><br /> </td> 
   <td> Adobe Campaign で作成したメールとランディングページに Adobe Experience Cloud ライブラリからアセットを挿入するには、この統合を設定します。<br /> <p>Adobe Campaign と Assets の統合について詳しくは、<a href="../../integrations/using/configuring-access-to-assets.md#integrating-with-experience-cloud-assets">こちら</a>を参照してください。</p><br /> </td> 
  </tr> 
  <tr> 
   <td> <strong>AEM Assets</strong><br /> </td> 
   <td> Adobe Campaign で作成したメールとランディングページに <strong>AEM Assets</strong> ライブラリからアセットを挿入するには、この統合を設定します。<br /> <p>Adobe Campaign と AEM Assets の統合について詳しくは、<a href="../../integrations/using/configuring-access-to-assets.md#integrating-with-aem-assets">こちら</a>を参照してください。</p><br /> </td> 
  </tr> 
  <tr> 
   <td> <strong>Experience Cloud Triggers</strong><br /> </td> 
   <td> <strong>Adobe Experience Cloud Triggers</strong>と Adobe Campaign の統合を設定すると、web サイト上で Adobe Analytics によってトラッキングされている特定の動作に対する反応としてパーソナライズされたメールを送信できます。<br /> <p>Adobe Campaign と Experience Cloud Triggers の統合について詳しくは、<a href="about-triggers.md">こちら</a>を参照してください。</p><br /> </td> 
  </tr> 
  <tr> 
   <td> <strong>Adobe Analytics Connector</strong><br /> </td> 
   <td> メールキャンペーン後のユーザー行動に関するセグメントについて、Adobe Campaign と Adobe Analytics を連携させるには、この統合を設定します。 このコネクタは、Adobe Campaign から配信された メールキャンペーンの指標と属性を Adobe Analytics に送信します。<br /> <p>Campaign と Analytics のコネクタでの統合に関する<a href="../../integrations/using/gs-aa.md">詳細情報</a>。</p><br /> </td> 
  </tr> 
 </tbody> 
</table>
