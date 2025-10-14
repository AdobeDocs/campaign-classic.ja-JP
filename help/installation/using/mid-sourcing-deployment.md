---
product: campaign
title: ミッドソーシングへのデプロイメント
description: ミッドソーシングへのデプロイメント
feature: Installation, Architecture, Deployment
audience: installation
content-type: reference
topic-tags: deployment-types-
exl-id: 8a4d7ef1-de5b-4aee-a527-1b74d987ba61
source-git-commit: b666535f7f82d1b8c2da4fbce1bc25cf8d39d187
workflow-type: tm+mt
source-wordcount: '356'
ht-degree: 16%

---

# ミッドソーシングへのデプロイメント{#mid-sourcing-deployment}



この設定は、ホスト型（ASP）設定と内部化の間の最適な中間ソリューションです。 外部向きの実行コンポーネントは、Adobe Campaignでホストされる「ミッドソーシング」サーバーで実行されます。

>[!NOTE]
>
>このタイプのデプロイメントを設定するには、適切なオプションを取得する必要があります。 ライセンス契約をご確認ください。

サーバーとプロセス間の一般的な通信は、次のスキーマに従って実行されます。

![](assets/s_ncs_install_midsourcing.png)

* 実行とバウンスの管理モジュールがインスタンスで無効になっています。
* アプリケーションは、SOAP 呼び出し（HTTP または HTTPS 経由）を使用して駆動されるリモートの「ミッドソース」サーバーでメッセージを実行するように設定されています。

## 機能 {#features}

### メリット {#advantages}

* サーバー設定の簡素化：お客様は、外部モジュール（mta および inMail）を設定する必要はありません。
* 帯域幅の使用制限：ミッドソーシングサーバーが実行するので、ミッドソーシングサーバーにパーソナライゼーションデータを送信するのに十分な帯域幅のみが必要になります。
* 高可用性はもはや内部的な問題ではありません。問題は、ミッドソーシングサーバー（リダイレクト、ミラーページ、実行サーバーなど）に移行します。
* データベースは会社を離れません。メッセージの組み合わせに必要なデータのみがミッドソーシングサーバーに送信されます（このために HTTPS を使用できます）。
* このタイプのデプロイメントは、大量のアーキテクチャ（データベース内の多くの受信者）を処理し、配信スループットが高いソリューションになります。

### デメリット {#disadvantages}

* ミッドソーシングサーバーから情報を取得するのに時間がかかるので、メッセージ実行情報の表示やレポート機能にわずかな遅延が生じます。
* 調査と web フォームは、クライアントプラットフォーム上に残ります。

### 推奨機器 {#recommended-equipment}

* アプリケーションサーバ：2 Ghz クアッドコアCPU、4 GB RAM、ソフトウェア RAID 1 80 GB SATA ハードドライブ。
* データベースサーバー：3 GHz の両クアッドコア CPU、最小 4 GB の RAM、ハードウェア RAID 10 15000RPM SAS ハードドライブ、データベースのサイズと予想パフォーマンスに応じた数。

>[!NOTE]
>
>リダイレクトとミッドソーシングは別々の要素ですが、トラッキングサーバーは通常、ミッドソーシングサーバーと共有されます。

## インストールと設定の手順 {#installation-and-configuration-steps-}

### 前提条件 {#prerequisites}

* アプリケーションサーバー上の JDK
* アプリケーションサーバー上のデータベースサーバーにアクセスします。
* ミッドソーシングサーバーへの HTTP （80）または HTTPS （443）ポートを開くように設定されたファイアウォール。

### インストールと設定（ミッドソーシングデプロイメント） {#installing-and-configuring--mid-sourcing-deployment-}

[&#x200B; ミッドソーシングサーバー &#x200B;](../../installation/using/mid-sourcing-server.md) を参照してください。
