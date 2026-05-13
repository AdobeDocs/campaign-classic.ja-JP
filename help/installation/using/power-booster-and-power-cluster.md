---
product: campaign
title: パワーブースターとパワークラスター
description: パワーブースターとパワークラスター
feature: Installation, Instance Settings
audience: installation
content-type: reference
topic-tags: deployment-types-
exl-id: 59364cfc-9917-4057-ad5f-fbca7e261b07
TQID: https://experienceleague.adobe.com/lcr5Xfipd9cDuglWBqBsiVXJUUZqQxLEmzzZPrAEhHU
product_v2: id: dfc56824-e8b9-499e-85d4-21aedb507314
feature_v2: id: a075b2c1-7748-4328-b7f6-343aa314616aid: a7760dfc-5c44-4d77-bb68-c50b1e265c93
subfeature_v2: id: ac9c0a9c-8a76-4419-bd64-9c34c5782666id: fb2a841f-c522-491f-9901-a1b939d252df
topic_v2: id: d095671a-1355-40aa-8b5f-06c33c68080bid: f4e6943a-c91a-4134-a2c7-f4f20cfff2f0
source-git-commit: 4c295c0dabae8aba298390a3da2422a3fa1219f9
workflow-type: tm+mt
source-wordcount: 416
ht-degree: 6%

---

# パワーブースターとパワークラスター{#power-booster-and-power-cluster}



## 概要 {#overview}

Adobe Campaignには、デプロイメントの寸法を決定するための2つのパッケージ化されたアーキテクチャオプションが用意されています。

* **パワーブースター**

  このオプションは、プライマリ Adobe Campaign アプリケーションインスタンスから切り離された1つの追加の実行インスタンスのサポートを提供します。 専用の実行インスタンスは、リモートまたはサードパーティによってホストできます。 実装すると、電子メールの実行、トラッキング、ミラーページ、バウンスメッセージは、中央のアプリケーション機能とは独立して処理されます。

* **パワークラスター**

  このオプションは、特定のアプリケーションに関して、プライマリ Adobe Campaign アプリケーションインスタンスから切り離された2 ～ Nのクラスター化された実行インスタンスをサポートします。 クラスターは、リモート、分散型デプロイメント、およびサードパーティによってホストできます。 プロセス分離の利点に加えて、Adobe Campaign Power Cluster オプションは、SLAやパフォーマンスの進化を簡素化するために、汎用ハードウェアを使用した冗長性とスケールアウト戦略を可能にします。

![](assets/architectural_options_diagram.png)

## 対象アプリケーション {#eligible-applications}

Power Booster オプションとPower Cluster オプションは、次のアプリケーションで使用できます。

* キャンペーン
* 配信
* Message Center

## アーキテクチャに関する推奨事項のマトリックス {#matrix-of-architectural-recommendations}

<table> 
 <tbody> 
  <tr> 
   <td> </td> 
   <td> <strong>標準アーキテクチャ </strong><br /> </td> 
   <td> <strong> パワーブースター</strong><br /> </td> 
   <td> <strong> パワークラスター</strong><br /> </td> 
  </tr> 
  <tr> 
   <td> メールキャンペーンとアウトバウンドインタラクション <br /> </td> 
   <td> 1か月あたり最大約3,000万通のメール <br /> </td> 
   <td> 毎月3,000万通から1億通のメール <br /> </td> 
   <td> 1か月あたり1億件以上のメール <br /> </td> 
  </tr> 
  <tr> 
   <td> トランザクションメッセージ <br /> </td> 
   <td> 実行サーバーごとに1時間あたり50,000 <br /></td> 
   <td> 実行サーバーごとに1時間あたり50,000 <br /></td> 
   <td> 実行サーバーごとに1時間あたり50,000 <br /></td> 
  </tr> 
  <tr> 
   <td> 可用性<br /> </td> 
   <td> プライマリデータベース <br />の </td> 
   <td> 実行インスタンスのメンテナンスウィンドウとダウンタイムを除く、24時間年中無休<br /> </td> 
   <td> 24/7/365 サービスが可能です<br /> </td> 
  </tr> 
  <tr> 
   <td> セキュリティ <br /> </td> 
   <td> データマートは、パブリック インターネットからアクセスできる可能性があります<br /> </td> 
   <td> データマートは、フロントエンドのインターネット向けコンポーネントから分離されています<br /> </td> 
   <td> データマートは、フロントエンドのインターネット向けコンポーネントから分離されています<br /> </td> 
  </tr> 
  <tr> 
   <td> デプロイメントテンプレート <br /> </td> 
   <td> すべて1つのサイト （オンプレミスまたはクラウド内にできます） <br /> </td> 
   <td> クラウドでの実行が可能なオンプレミスでのマーケティング <br /> </td> 
   <td> オンプレミスでのマーケティングとクラウドでの実行。異なる地域での実行が可能<br /> </td> 
  </tr> 
 </tbody> 
</table>

## 推奨事項 {#recommendations}

* 実行インスタンスはサービス専用である必要があります。 購読していないサービスのパッケージをインストールすることはできません。 例えば、**Message Center** サービスの&#x200B;**Power Booster** オプションを購読している場合、専用の実行インスタンスに&#x200B;**[!UICONTROL トランザクションメッセージの実行]** パッケージのみをインストールできます。 使用許諾契約書を確認してください。
* 専用インスタンス（またはクラスター）はAdobe Campaign インスタンスであるため、推奨事項はメインインスタンスと同じです。 詳しくは、[このドキュメント ](../../production/using/foreword.md)を参照してください。
* データベース/ハードウェアコンポーネントの観点からインスタンスを適切に設定するには、Adobe Campaign プロフェッショナルサービスにお問い合わせください。
