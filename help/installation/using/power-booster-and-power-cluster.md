---
product: campaign
title: パワーブースターとパワークラスター
description: パワーブースターとパワークラスター
feature: Installation, Instance Settings
audience: installation
content-type: reference
topic-tags: deployment-types-
exl-id: 59364cfc-9917-4057-ad5f-fbca7e261b07
source-git-commit: 0ed70b3c57714ad6c3926181334f57ed3b409d98
workflow-type: tm+mt
source-wordcount: '416'
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
* 専用インスタンス（またはクラスター）はAdobe Campaign インスタンスであるため、推奨事項はメインインスタンスと同じです。 詳しくは、[このドキュメント &#x200B;](../../production/using/foreword.md)を参照してください。
* データベース/ハードウェアコンポーネントの観点からインスタンスを適切に設定するには、Adobe Campaign プロフェッショナルサービスにお問い合わせください。
