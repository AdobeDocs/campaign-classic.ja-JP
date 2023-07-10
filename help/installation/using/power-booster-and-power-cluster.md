---
product: campaign
title: パワーブースターとパワークラスター
description: パワーブースターとパワークラスター
badge-v7-only: label="v7" type="Informative" tooltip="Applies to Campaign Classic v7 only"
audience: installation
content-type: reference
topic-tags: deployment-types-
exl-id: 59364cfc-9917-4057-ad5f-fbca7e261b07
source-git-commit: 8debcd3d8fb883b3316cf75187a86bebf15a1d31
workflow-type: tm+mt
source-wordcount: '400'
ht-degree: 7%

---

# パワーブースターとパワークラスター{#power-booster-and-power-cluster}



## 概要 {#overview}

Adobe Campaignには、配置の寸法を記入するための、パッケージ化された 2 つのアーキテクチャオプションが用意されています。

* **パワーブースター**

  このオプションは、プライマリAdobe Campaignアプリケーションインスタンスから切り離された単一の追加の実行インスタンスをサポートします。 専用の実行インスタンスは、リモートで、またはサードパーティでホストできます。 実装すると、E メールの実行、トラッキング、ミラーページおよびバウンスメッセージは、中央のアプリケーションの機能とは独立して処理されます。

* **電源クラスタ**

  このオプションは、特定のアプリケーションに関連して、プライマリAdobe Campaignアプリケーションインスタンスから切り離された 2 ～ n のクラスター化実行インスタンスをサポートします。 クラスターは、リモート、分散デプロイメント、およびサードパーティによってホストできます。 Adobe Campaign Power Cluster オプションは、プロセス分離のメリットに加え、SLA やパフォーマンスの変化をシンプルにするために、商品ハードウェアを使用した冗長性とスケールアウト戦略を可能にします。

![](assets/architectural_options_diagram.png)

## 適格なアプリ {#eligible-applications}

パワーブースターとパワークラスターのオプションは、次のアプリケーションで使用できます。

* キャンペーン
* 配信
* Message Center

## アーキテクチャの推奨事項のマトリックス {#matrix-of-architectural-recommendations}

<table> 
 <tbody> 
  <tr> 
   <td> </td> 
   <td> <strong>標準アーキテクチャ</strong><br /> </td> 
   <td> <strong>パワーブースター</strong><br /> </td> 
   <td> <strong>電源クラスタ</strong><br /> </td> 
  </tr> 
  <tr> 
   <td> 電子メールキャンペーンとアウトバウンドインタラクション<br /> </td> 
   <td> 1 ヶ月あたり最大 3,000 万通の E メール<br /> </td> 
   <td> 月に 3,000 万～ 1 億通のメール<br /> </td> 
   <td> 1 ヶ月に 1 億通以上のメール<br /> </td> 
  </tr> 
  <tr> 
   <td> トランザクションメッセージ<br /> </td> 
   <td> 実行サーバーあたり 50,000 時間<br /> </td> 
   <td> 実行サーバーあたり 50,000 時間<br /> </td> 
   <td> 実行サーバーあたり 50,000 時間<br /> </td> 
  </tr> 
  <tr> 
   <td> アベイラビリティ<br /> </td> 
   <td> プライマリデータベースのデータベース<br /> </td> 
   <td> 24/7（メンテナンスウィンドウを除く）、および実行インスタンスのダウンタイム<br /> </td> 
   <td> 24/7/365サービスが可能<br /> </td> 
  </tr> 
  <tr> 
   <td> セキュリティ<br /> </td> 
   <td> データマートは、潜在的にパブリックインターネットからアクセス可能です<br /> </td> 
   <td> データマートは、正面の、インターネットに接続するコンポーネントから切り離されています<br /> </td> 
   <td> データマートは、正面の、インターネットに接続するコンポーネントから切り離されています<br /> </td> 
  </tr> 
  <tr> 
   <td> デプロイメントテンプレート<br /> </td> 
   <td> すべて 1 つのサイト（オンプレミスまたはクラウド内）で実行<br /> </td> 
   <td> クラウドでの実行が可能なオンプレミスマーケティング<br /> </td> 
   <td> クラウドでの実行を含むオンプレミスマーケティング可能な異なる地域での実行<br /> </td> 
  </tr> 
 </tbody> 
</table>

## 推奨事項 {#recommendations}

* 実行インスタンスは、サービス専用である必要があります。 購読していないサービス用のパッケージはインストールできません。 例えば、 **パワーブースター** オプション **Message Center** サービス、インストールできるのは **[!UICONTROL トランザクションメッセージの実行]** パッケージを専用の実行インスタンス上に配置します。 使用許諾契約書を確認してください。
* 専用インスタンス（またはクラスター）はAdobe Campaignインスタンスなので、レコメンデーションはメインインスタンスの場合と同じです。 詳しくは、 [このドキュメント](../../production/using/foreword.md).
* データベース/ハードウェアコンポーネントの観点からインスタンスを適切に設定するには、Adobe Campaign Professional Services にお問い合わせください。
