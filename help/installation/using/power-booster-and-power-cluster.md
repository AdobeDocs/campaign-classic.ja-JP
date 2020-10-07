---
title: パワーブースターとパワークラスター
seo-title: パワーブースターとパワークラスター
description: パワーブースターとパワークラスター
seo-description: null
page-status-flag: never-activated
uuid: 4d23ed42-a368-4bd6-afaf-48452e253d19
contentOwner: sauviat
products: SG_CAMPAIGN/CLASSIC
audience: installation
content-type: reference
topic-tags: deployment-types-
discoiquuid: 715d2b69-5b47-4890-8b7d-1dc0a0d4ead8
translation-type: tm+mt
source-git-commit: 70b143445b2e77128b9404e35d96b39694d55335
workflow-type: tm+mt
source-wordcount: '405'
ht-degree: 8%

---


# パワーブースターとパワークラスター{#power-booster-and-power-cluster}

## 概要 {#overview}

Adobe Campaignには、配置の寸法を記入するための、パッケージ済みの2つのアーキテクチャオプションが用意されています。

* **パワー・ブースタ**

   このオプションは、プライマリAdobe Campaignアプリケーションインスタンスから切り離された単一の追加実行インスタンスをサポートします。 専用実行インスタンスは、リモートでホストすることも、サードパーティでホストすることもできます。 実装する場合、電子メールの実行、追跡、ミラーページおよびバウンスのメッセージは、中央のアプリケーションの機能とは独立して処理されます。

* **電源クラスタ**

   このオプションは、2 ～ Nのクラスター化された実行インスタンスを、所定のアプリケーションに関連してプライマリAdobe Campaignアプリケーションインスタンスから切り離すことをサポートします。 クラスターは、リモートで、分散デプロイメントで、およびサードパーティによってホストできます。 プロセス分離のメリットに加えて、Adobe Campaign電源クラスタオプションでは、SLAやパフォーマンスのシンプルな進化を実現するために、ハードウェアを使用した冗長性とスケールアウト戦略を実現します。

![](assets/architectural_options_diagram.png)

## 適格な申し込み {#eligible-applications}

パワー・ブースタとパワー・クラスタのオプションは、次のアプリケーションで使用できます。

* キャンペーン
* 配信
* Message Center

## 建築推奨のマトリックス {#matrix-of-architectural-recommendations}

<table> 
 <tbody> 
  <tr> 
   <td> </td> 
   <td> <strong>標準アーキテクチャ</strong><br /> </td> 
   <td> <strong>パワー・ブースタ</strong><br /> </td> 
   <td> <strong>電源クラスタ</strong><br /> </td> 
  </tr> 
  <tr> 
   <td> 電子メールキャンペーンと送信のインタラクション<br /> </td> 
   <td> 1か月あたり最大3,000万件の電子メール<br /> </td> 
   <td> 月に3000万～1億件の電子メール<br /> </td> 
   <td> 1か月に1億件を超える電子メール<br /> </td> 
  </tr> 
  <tr> 
   <td> トランザクションメッセージ<br /> </td> 
   <td> 実行サーバ1時間あたり50,000<br /> </td> 
   <td> 実行サーバ1時間あたり50,000<br /> </td> 
   <td> 実行サーバ1時間あたり50,000<br /> </td> 
  </tr> 
  <tr> 
   <td> 使用有無<br /> </td> 
   <td> プライマリ・データベースのデータベース<br /> </td> 
   <td> 24時間365日対応(実行インスタンスのメンテナンス期間とダウンタイムを除く)<br /> </td> 
   <td> 24/7/365サービス可能<br /> </td> 
  </tr> 
  <tr> 
   <td> セキュリティ<br /> </td> 
   <td> データマートは、潜在的に公共のインターネットからアクセスできる<br /> </td> 
   <td> データマートは、正面、インターネットに接続するコンポーネントから切り離されています。<br /> </td> 
   <td> データマートは、正面、インターネットに接続するコンポーネントから切り離されています。<br /> </td> 
  </tr> 
  <tr> 
   <td> 導入テンプレート<br /> </td> 
   <td> すべて1つのサイト（オンプレミスまたはクラウド内）<br /> </td> 
   <td> クラウドでの実行を可能にするオンプレミスマーケティング<br /> </td> 
   <td> クラウドでの実行を伴うオンプレミスマーケティング可能な異なるgeoの実行<br /> </td> 
  </tr> 
 </tbody> 
</table>

## 推奨事項 {#recommendations}

* 実行インスタンスは、サービス専用にする必要があります。 登録していないサービス用のパッケージをインストールすることはできません。 例えば、 **Message Centerサービスの** 電源ブースタ **・オプションを購読している場合は、専用実行インスタンスにトランザクションメッセージ** ・パッケージの **** 実行のみをインストールできます。 使用許諾契約書を確認してください。
* 専用のインスタンス（またはクラスター）はAdobe Campaignインスタンスなので、レコメンデーションはメインインスタンスと同じです。 For more on this, refer to [this document](../../production/using/foreword.md).
* データベース/ハードウェアコンポーネントの表示点からインスタンスを適切に構成するには、Adobe Campaignプロフェッショナルサービスにお問い合わせください。

