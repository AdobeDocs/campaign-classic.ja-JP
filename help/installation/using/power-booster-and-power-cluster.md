---
title: パワーブースタとパワークラスタ
seo-title: パワーブースタとパワークラスタ
description: パワーブースタとパワークラスタ
seo-description: null
page-status-flag: never-activated
uuid: 4d23ed42-a368-4bd6-afaf-48452e253d19
contentOwner: sauviat
products: SG_CAMPAIGN/CLASSIC
audience: installation
content-type: reference
topic-tags: deployment-types-
discoiquuid: 715d2b69-5b47-4890-8b7d-1dc0a0d4ead8
index: y
internal: n
snippet: y
translation-type: tm+mt
source-git-commit: a5072ba55690d4d88c12ac7ff647f163deddbf32

---


# パワーブースタとパワークラスタ{#power-booster-and-power-cluster}

## 概要 {#overview}

Adobe Campaignには、展開の寸法を記入するための2つのセットのプリパッケージアーキテクチャオプションが用意されています。

* **パワーブースタ**

   このオプションは、プライマリAdobe Campaignアプリケーションインスタンスから切り離された1つの追加実行インスタンスをサポートします。 専用の実行インスタンスは、リモートでホストすることも、サードパーティによってホストすることもできます。 実装する場合、電子メールの実行、追跡、ミラーページおよびバウンスメッセージは、中央のアプリケーション機能とは独立して処理されます。

* **電源クラスタ**

   このオプションは、特定のアプリケーションに関連して、Adobe Campaignのプライマリアプリケーションインスタンスから切り離された2 ～ n個のクラスター化された実行インスタンスをサポートします。 クラスターは、リモートで、分散デプロイメント、およびサードパーティによってホストできます。 Adobe Campaignのパワークラスターオプションを使用すると、プロセスの分離のメリットに加えて、SLAやパフォーマンスの進化をシンプルにするために、冗長性とスケールアウト戦略を実現できます。

![](assets/architectural_options_diagram.png)

## 申し込み対象 {#eligible-applications}

パワーブースターとパワークラスタのオプションは、次のアプリケーションで使用できます。

* キャンペーン
* リード
* 配信
* Message Center

## アーキテクチャ推奨のマトリックス {#matrix-of-architectural-recommendations}

<table> 
 <tbody> 
  <tr> 
   <td> </td> 
   <td> <strong>標準アーキテクチャ</strong><br /> </td> 
   <td> <strong>パワーブースタ</strong><br /> </td> 
   <td> <strong>電源クラスタ</strong><br /> </td> 
  </tr> 
  <tr> 
   <td> 電子メールキャンペーンとアウトバウンドインタラクション<br /> </td> 
   <td> 1か月あたり最大3,000万通の電子メール<br /> </td> 
   <td> 月に3000万～1億通のメール<br /> </td> 
   <td> 1か月に1億通以上のメール<br /> </td> 
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
   <td> 24時間365日（実行インスタンスのメンテナンス期間とダウンタイムを除く）<br /> </td> 
   <td> 24/7/365サービス可能<br /> </td> 
  </tr> 
  <tr> 
   <td> セキュリティ<br /> </td> 
   <td> データマートは、潜在的にパブリックインターネットからアクセス可能<br /> </td> 
   <td> データマートは正面向けのインターネット対応コンポーネントから切り離されています。<br /> </td> 
   <td> データマートは正面向けのインターネット対応コンポーネントから切り離されています。<br /> </td> 
  </tr> 
  <tr> 
   <td> 導入テンプレート<br /> </td> 
   <td> すべて1つのサイト（オンプレミスまたはクラウド内）<br /> </td> 
   <td> クラウドで実行可能なオンプレミスマーケティング<br /> </td> 
   <td> クラウドで実行するオンプレミスマーケティング可能な異なる地域での実行<br /> </td> 
  </tr> 
 </tbody> 
</table>

## 推奨事項 {#recommendations}

* 実行インスタンスは、サービス専用である必要があります。 登録していないサービス用のパッケージをインストールすることはできません。 例えば、 **Message Centerサービスの** Power Booster **（パワーブースター）オプションをサブスクライブしている場合は** 、専用の実行インスタンスにの **[!UICONTROL Execution of transactional messages]** みパッケージをインストールできます。 使用許諾契約書を確認してください。
* 専用インスタンス（またはクラスター）はAdobe Campaignインスタンスなので、レコメンデーションはメインインスタンスと同じです。 For more on this, refer to [this document](../../production/using/foreword.md).
* データベース/ハードウェアコンポーネントの観点からインスタンスを適切に設定するには、Adobe Campaignプロフェッショナルサービスにお問い合わせください。

