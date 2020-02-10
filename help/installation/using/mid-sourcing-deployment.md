---
title: 中間調査の導入
seo-title: 中間調査の導入
description: 中間調査の導入
seo-description: null
page-status-flag: never-activated
uuid: e359c486-7ee6-4295-80fc-4c371a0ef068
contentOwner: sauviat
products: SG_CAMPAIGN/CLASSIC
audience: installation
content-type: reference
topic-tags: deployment-types-
discoiquuid: 19220d8e-9494-46b4-9aa0-4c4a729aea96
index: y
internal: n
snippet: y
translation-type: tm+mt
source-git-commit: be590c6d993eecacf51736e3c3e415addae5c6bd

---


# 中間調査の導入{#mid-sourcing-deployment}

この設定は、ホスト型(ASP)設定と内部化の最適な中間ソリューションです。 外向きの実行コンポーネントは、Adobe Campaignでホストされる「ミッドソーシング」サーバーで実行されます。

>[!NOTE]
>
>このタイプの展開を設定するには、適切なオプションを取得する必要があります。 ライセンス契約を確認してください。

サーバーとプロセス間の一般的な通信は、次のスキーマに従って実行されます。

![](assets/s_ncs_install_midsourcing.png)

* インスタンス上で、実行とバウンスの管理モジュールが無効になっています。
* アプリケーションは、SOAP呼び出し（HTTPまたはHTTPS経由）を使用して駆動されるリモートの「ミッドソース」サーバー上でメッセージ実行を実行するように設定されます。

## 機能 {#features}

### メリット {#advantages}

* シンプル化されたサーバー設定：顧客が外向きのモジュール（mtaおよびinMail）を設定する必要はありません。
* 帯域幅の使用制限：実行はミッドソーシングサーバーによって実行されるので、パーソナライゼーションデータをミッドソーシングサーバーに送信するのに十分な帯域幅のみが必要です。
* 高可用性が内部の問題ではなくなりました。問題は、ミッドソーシングサーバー（リダイレクト、ミラーページ、実行サーバーなど）に移行します。
* データベースが会社を離れません：メッセージのアセンブリに必要なデータのみがミッドソーシングサーバーに送信されます（HTTPSを使用できます）。
* このタイプの導入は、大量のアーキテクチャ（データベース内の多くの受信者）に適した、大量の配信スループットを備えたソリューションとなります。

### 欠点 {#disadvantages}

* 中間ソーシングサーバーから情報を取得するのにかかる時間により、メッセージ実行情報およびレポート機能の表示に若干の遅延が生じました。
* 調査とWebフォームはクライアントプラットフォームに残ります。

### 推奨機器 {#recommended-equipment}

* アプリケーションサーバー：2 GhzクアッドコアCPU、4 GB RAM、ソフトウェアRAID 1 80 GB SATAハードドライブ。
* データベースサーバー：3 GHzバイクアッドコアCPU、最低4 GB RAM、ハードウェアRAID 10 15000 RPM SASハードドライブ、データベースのサイズと予想されるパフォーマンスに応じた数。

>[!NOTE]
>
>リダイレクトとミッドソーシングは別々の要素ですが、一般的に、トラッキングサーバーはミッドソーシングサーバーと共有されます。

## インストールと設定の手順 {#installation-and-configuration-steps-}

### 前提条件 {#prerequisites}

* アプリケーションサーバー上のJDK。
* アプリケーションサーバー上のデータベースサーバーへのアクセス。
* ファイアウォールは、ミッドソーシングサーバーに対してHTTP(80)またはHTTPS(443)ポートを開くように設定されています。

### インストールと設定（中間ソーシング配置） {#installing-and-configuring--mid-sourcing-deployment-}

ミッドソーシ [ングサーバーを参照](../../installation/using/mid-sourcing-server.md)。
