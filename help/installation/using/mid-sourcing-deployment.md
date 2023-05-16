---
product: campaign
title: ミッドソーシングへのデプロイメント
description: ミッドソーシングへのデプロイメント
badge-v7-only: label="v7" type="Informative" tooltip="Applies to Campaign Classic v7 only"
audience: installation
content-type: reference
topic-tags: deployment-types-
exl-id: 8a4d7ef1-de5b-4aee-a527-1b74d987ba61
source-git-commit: 8debcd3d8fb883b3316cf75187a86bebf15a1d31
workflow-type: tm+mt
source-wordcount: '351'
ht-degree: 16%

---

# ミッドソーシングへのデプロイメント{#mid-sourcing-deployment}



この設定は、ホスト (ASP) 設定と内部化の間の最適な中間ソリューションです。 外向きの実行コンポーネントは、Adobe Campaignでホストされる「ミッドソーシング」サーバーで実行されます。

>[!NOTE]
>
>このタイプのデプロイメントを設定するには、適切なオプションを入手する必要があります。 ライセンス契約を確認してください。

サーバーとプロセス間の一般的な通信は、次のスキーマに従って実行されます。

![](assets/s_ncs_install_midsourcing.png)

* 実行とバウンスの管理モジュールがインスタンスで無効になっています。
* アプリケーションは、SOAP 呼び出し（HTTP または HTTPS 経由）を使用して駆動されるリモートの「ミッドソース」サーバーでメッセージを実行するように設定されています。

## 機能 {#features}

### メリット {#advantages}

* サーバー設定の簡略化：お客様が外向きモジュール（mta および inMail）を設定する必要はありません。
* 帯域幅の使用制限：実行はミッドソーシングサーバーによって実行されるので、パーソナライゼーションデータをミッドソーシングサーバーに送信するのに十分な帯域幅のみが必要です。
* 高可用性は、内部的な問題ではなくなりました。問題がミッドソーシングサーバー（リダイレクト、ミラーページ、実行サーバーなど）に移行します。
* データベースが会社を離れない場合：メッセージの組み立てに必要なデータのみがミッドソーシングサーバーに送信されます（HTTPS を使用できます）。
* このタイプのデプロイメントは、大量のアーキテクチャ（データベース内の多くの受信者）に対して、大幅な配信スループットを備えたソリューションになります。

### デメリット {#disadvantages}

* 中間ソーシングサーバーから情報を取り戻すのにかかる時間により、メッセージ実行情報の表示およびレポート機能の表示に若干の遅延が生じます。
* 調査および Web フォームは、クライアントプラットフォーム上に残ります。

### 推奨機器 {#recommended-equipment}

* アプリケーションサーバー：2 Ghz クアッドコア CPU、4 GB RAM、ソフトウェア RAID 1 80 GB SATA ハードドライブ。
* データベースサーバ：3 GHz バイクアッドコア CPU、最低 4 GB RAM、ハードウェア RAID 10 15000RPM SAS ハードドライブ、データベースのサイズと予想されるパフォーマンスに応じた数。

>[!NOTE]
>
>リダイレクトとミッドソーシングは別々の要素ですが、一般的に、トラッキングサーバーはミッドソーシングサーバーと共有されます。

## インストールおよび設定手順 {#installation-and-configuration-steps-}

### 前提条件 {#prerequisites}

* アプリケーションサーバーの JDK。
* アプリケーションサーバー上のデータベースサーバーにアクセスする。
* ミッドソーシングサーバーに対して HTTP(80) または HTTPS(443) ポートを開くように設定されたファイアウォール。

### インストールと設定（ミッドソーシングデプロイメント） {#installing-and-configuring--mid-sourcing-deployment-}

参照： [ミッドソーシングサーバー](../../installation/using/mid-sourcing-server.md).
