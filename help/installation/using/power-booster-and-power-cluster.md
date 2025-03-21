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
source-wordcount: '413'
ht-degree: 6%

---

# パワーブースターとパワークラスター{#power-booster-and-power-cluster}



## 概要 {#overview}

Adobe Campaignには、デプロイメントの寸法を記入するための、パッケージ済みのアーキテクチャオプションが 2 つ用意されています。

* **パワーブースター**

  このオプションは、プライマリ Adobe Campaign アプリケーションインスタンスから切り離された 1 つの追加の実行インスタンスに対するサポートを提供します。 専用実行インスタンスは、リモートまたはサードパーティでホストできます。 実装する場合、メールの実行、トラッキング、ミラーページおよびバウンスメッセージは、中央のアプリケーション機能とは独立して処理されます。

* **電源クラスター**

  このオプションは、特定のアプリケーションに関して、プライマリ Adobe Campaign アプリケーションインスタンスから切り離された 2～N のクラスター実行インスタンスをサポートします。 クラスターは、リモートで、分散デプロイメントで、およびサードパーティによってホストできます。 プロセスの分離によるメリットに加えて、Adobe Campaignのパワークラスターオプションは、市販のハードウェアを使用して冗長性とスケールアウト戦略を実現し、SLAやパフォーマンスの進化をシンプルにします。

![](assets/architectural_options_diagram.png)

## 適格な申請 {#eligible-applications}

パワーブースターとパワークラスターオプションは、次のアプリケーションで使用できます。

* キャンペーン
* 配信
* Message Center

## アーキテクチャ推奨事項のマトリックス {#matrix-of-architectural-recommendations}

<table> 
 <tbody> 
  <tr> 
   <td> </td> 
   <td> <strong> 標準アーキテクチャ </strong><br /> </td> 
   <td> <strong> パワーブースター </strong><br /> </td> 
   <td> <strong> 電源クラスター </strong><br /> </td> 
  </tr> 
  <tr> 
   <td> メールキャンペーンとアウトバウンドインタラクション <br /> </td> 
   <td> 1 か月あたり最大約 3,000 万通のメール <br /> </td> 
   <td> 1 か月あたり 3,000 万～1 億のメール <br /> </td> 
   <td> 月に 1 億通を超えるメール <br /> </td> 
  </tr> 
  <tr> 
   <td> トランザクションメッセージ <br /> </td> 
   <td> 実行サーバーあたり 1 時間あたり 50,000<br /> </td> 
   <td> 実行サーバーあたり 1 時間あたり 50,000<br /> </td> 
   <td> 実行サーバーあたり 1 時間あたり 50,000<br /> </td> 
  </tr> 
  <tr> 
   <td> 対象 <br /> </td> 
   <td> プライマリ・データベースの <br /> </td> 
   <td> 24 時間年中無休（実行インスタンスのメンテナンスウィンドウとダウンタイムを除く） <br /> </td> 
   <td> 24/7/365 のサービスが可能 <br /> </td> 
  </tr> 
  <tr> 
   <td> セキュリティ <br /> </td> 
   <td> データマートは、パブリックインターネットから潜在的にアクセスでき <br /> す。 </td> 
   <td> データマートは、インターネットに接続された正面のコンポーネントから分離されている <br /> </td> 
   <td> データマートは、インターネットに接続された正面のコンポーネントから分離されている <br /> </td> 
  </tr> 
  <tr> 
   <td> 配置テンプレート <br /> </td> 
   <td> すべてを 1 つのサイトに（オンプレミスでもクラウドでも） <br /> </td> 
   <td> クラウドでの実行を可能にするオンプレミスマーケティング <br /> </td> 
   <td> クラウドで実行するオンプレミスマーケティング。異なる地域での実行が可能 <br /> </td> 
  </tr> 
 </tbody> 
</table>

## 推奨事項 {#recommendations}

* 実行インスタンスは、サービス専用である必要があります。 購読していないサービスのパッケージはインストールできません。 例えば、**Message Center** サービスの **パワーブースター** オプションをサブスクライブしている場合、**[!UICONTROL トランザクションメッセージの実行]** パッケージを専用の実行インスタンスにのみインストールできます。 使用許諾契約書を確認してください。
* 専用インスタンス（またはクラスター）はAdobe Campaign インスタンスなので、推奨事項はメインインスタンスの場合と同じです。 詳しくは、[ このドキュメント ](../../production/using/foreword.md) を参照してください。
* データベース/ハードウェアコンポーネントの観点からインスタンスを適切に設定するには、Adobe Campaign プロフェッショナルサービスにお問い合わせください。
