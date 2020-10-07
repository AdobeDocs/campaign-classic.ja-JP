---
title: ミッドソーシングへのデプロイメント
seo-title: ミッドソーシングへのデプロイメント
description: ミッドソーシングへのデプロイメント
seo-description: null
page-status-flag: never-activated
uuid: e359c486-7ee6-4295-80fc-4c371a0ef068
contentOwner: sauviat
products: SG_CAMPAIGN/CLASSIC
audience: installation
content-type: reference
topic-tags: deployment-types-
discoiquuid: 19220d8e-9494-46b4-9aa0-4c4a729aea96
translation-type: tm+mt
source-git-commit: 70b143445b2e77128b9404e35d96b39694d55335
workflow-type: tm+mt
source-wordcount: '353'
ht-degree: 3%

---


# ミッドソーシングへのデプロイメント{#mid-sourcing-deployment}

この設定は、ホスト(ASP)設定と内部化の間の最適な中間ソリューションです。 外向きの実行コンポーネントは、Adobe Campaignでホストされる「ミッドソーシング」サーバーで実行されます。

>[!NOTE]
>
>このタイプのデプロイメントを設定するには、適切なオプションを取得する必要があります。 ライセンス契約を確認してください。

サーバとプロセス間の一般的な通信は、次のスキーマに従って行われます。

![](assets/s_ncs_install_midsourcing.png)

* 実行とバウンスの管理モジュールがインスタンスで無効になっています。
* アプリケーションは、SOAP呼び出し（HTTPまたはHTTPS経由）を使用して駆動されるリモートの「ミッドソース」サーバーでメッセージ実行を実行するように設定されます。

## 機能 {#features}

### メリット {#advantages}

* サーバー設定の簡素化：お客様が外向きモジュール（mtaおよびinMail）を設定する必要はありません。
* 帯域幅の使用制限：ミッドソーシングサーバが実行するので、パーソナライゼーションデータをミッドソーシングサーバに送信するのに十分な帯域幅しか必要ありません。
* 高可用性は、内部の問題ではなくなりました。問題は、ミッドソーシングサーバ(リダイレクト、ミラーページ、実行サーバなど)に移行します。
* データベースが会社を離れません：メッセージをアセンブルするために必要なデータのみがミッドソーシングサーバーに送信されます（HTTPSを使用できます）。
* このタイプの導入は、大量のアーキテクチャ(データベース内の多くの受信者)に対するソリューションとなり、配信のスループットが大幅に向上します。

### デメリット {#disadvantages}

* ミッドソーシングサーバーから情報を取得するのに要する時間が原因で、レポートの実行情報およびメッセージ機能の表示に若干の遅延が生じる。
* 調査とWebフォームは、クライアントプラットフォームに残ります。

### 推奨される機器 {#recommended-equipment}

* アプリケーションサーバー：2 GHZクアッドコアCPU、4 GB RAM、ソフトウェアRAID 1 80 GB SATAハードドライブ。
* データベースサーバー：3 GHzバイクアッドコアCPU、最小4 GB RAM、ハードウェアRAID 10 15000 RPM SASハードドライブ、データベースのサイズと予想されるパフォーマンスに応じた数。

>[!NOTE]
>
>リダイレクトとミッドソーシングは別々の要素ですが、一般的に、トラッキングサーバーはミッドソーシングサーバーと共有します。

## インストールと設定の手順 {#installation-and-configuration-steps-}

### 前提条件 {#prerequisites}

* アプリケーションサーバーのJDK。
* アプリケーションサーバー上のデータベースサーバーにアクセスします。
* ミッドソーシングサーバーへのHTTP(80)またはHTTPS(443)ポートを開くように構成されたファイアウォール。

### インストールと設定(ミッドソーシング導入) {#installing-and-configuring--mid-sourcing-deployment-}

「 [ミッドソーシングサーバ](../../installation/using/mid-sourcing-server.md)」を参照してください。
