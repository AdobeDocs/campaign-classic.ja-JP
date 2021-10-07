---
product: campaign
title: ホスティングモデル
description: Campaign のホスティングモデルの理解
feature: Overview
role: Architect
level: Beginner
exl-id: a06b1365-d487-4df1-8f4a-7268b871a427
source-git-commit: 20509f44c5b8e0827a09f44dffdf2ec9d11652a1
workflow-type: tm+mt
source-wordcount: '623'
ht-degree: 2%

---

# ホスティングモデル{#hosting-models}

![](../../assets/v7-only.svg)

Adobe Campaignは、3 つのホスティングモデルから選択でき、ビジネスニーズに合った最適なモデルを柔軟かつ自由に選択できます。

>[!NOTE]
>
>Adobeがホストする環境では、サーバーの設定やインスタンス設定ファイルのカスタマイズなど、主なインストールおよび設定手順は、Adobeが実行する必要があります。 デプロイメントモード間の主な違いについて詳しくは、[ このページ ](../../installation/using/capability-matrix.md) を参照してください。

## Managed Services/ホスト

Adobe Campaignは、次のas a Managed Service的にデプロイできます。Adobe Campaignのすべてのコンポーネント（ユーザーインターフェイス、実行管理エンジン、お客様の Campaign データベースを含む）は、電子メールの実行、ミラーページ、トラッキングサーバー、購読解除ページ/環境設定センター、ランディングページなど、Adobeで完全にホストされます。

![](assets/deployment_hosted.png)

ホスト型のお客様は、ほとんどのインストール手順と設定手順をAdobeで実行します。 以下のセクションにアクセスして、実装をカスタマイズできます。

* ブランドごとのトラッキングおよびミラーページ URL の設定 トランザクションメッセージについては、[ この節 ](../../message-center/using/additional-configurations.md#configuring-multibranding) を参照してください。
* クライアントコンソールをインストールします。[ を参照してください。](../../installation/using/installing-the-client-console.md)
* 配信品質ツールとベストプラクティスの詳細については、[ 詳細なドキュメント ](../../delivery/using/about-deliverability.md) を参照してください。
* キャンペーンオプションの設定：[ を参照してください。](../../installation/using/configuring-campaign-options.md)
* CRM コネクタを設定します。[ を参照してください。](../../platform/using/crm-connectors.md)

## オンプレミス

Adobe Campaignはオンプレミスでデプロイできます。ユーザーインターフェイス、実行管理エンジン、データベースを含む、Adobe Campaignのすべてのコンポーネントは、お客様のデータセンターのオンサイトに存在します。 このデプロイメントモデルでは、お客様はすべてのソフトウェアとハードウェアの更新とアップグレードを管理し、専用のデータベース管理者はメンテナンスと最適化のタスクを実行して Campaign インスタンスの管理を確実に行う必要があります。

![](assets/deployment_onpremise.png)

オンプレミス版のお客様は、Campaign Classicのデプロイを開始する前に、次の前提条件と推奨事項に注意してください。

* [ 互換性マトリックス ](../../rn/using/compatibility-matrix.md) に、Adobe Campaignでサポートされているすべてのバージョンのシステムとコンポーネントを記載しています。
* お使いの環境に応じて、Windows の [ 前提条件と、Linux の ](../../installation/using/prerequisites-of-campaign-installation-in-linux.md) の [ 前提条件をお読みください。](../../installation/using/prerequisites-of-campaign-installation-in-windows.md)
* データベースエンジンに関する推奨事項については、この節 [ を参照してください。](../../installation/using/database.md)
* 必要なデータベースアクセスレイヤーがサーバーにインストールされ、Adobe Campaignアカウントからアクセスできることを確認します。 [詳細情報](../../installation/using/application-server.md)。
* 一部のプロセスは他のプロセスと通信したり、LAN やインターネットにアクセスしたりする必要があるので、ネットワークを設定します。 これは、これらのプロセスで一部の TCP ポートを開く必要があることを意味します。 [ネットワ](../../installation/using/network-configuration.md) ーク構成要件の詳細を説明します。
* [Campaign のセキュリティおよびプライバシーチェックリスト ](https://helpx.adobe.com/jp/campaign/kb/acc-security.html) を参照してください。
* オンプレミスデプロイメントのハードウェア要件の見積もりに関する一般的なガイドラインを確認してください。 [](https://helpx.adobe.com/jp/campaign/kb/hardware-sizing-guide.html)

## ハイブリッド

ハイブリッドモデルとしてデプロイする場合、Adobe Campaignソリューションソフトウェアはオンプレミスで顧客サイトに存在し、実行管理はAdobeによってクラウドサービスとして提供されます。 Adobe Campaign Marketing インスタンスは顧客のファイアウォール内にインストールされるので、個人情報 (PII) は社内に残り、E メールのパーソナライズに必要なデータのみが E メールの実行のために Cloud に送信されます。 クラウドでホストされる実行インスタンスは、オンプレミスインスタンスから E メールの配信要求を受け取ります。 このインスタンスは、すべての E メールをパーソナライズし、配信します。 どのような種類のデータも、クラウドに永続的に保存されません。

![](assets/deployment_hybrid.png)

ハイブリッドのお客様は、インストールおよび設定手順のほとんどをAdobeで実行します。 以下のセクションにアクセスして、実装をカスタマイズできます。

* トランザクションメッセージの設定：[ を参照してください。](../../message-center/using/transactional-messaging-architecture.md)
* ブランドごとのトラッキングおよびミラーページ URL の設定 トランザクションメッセージについては、[ この節 ](../../message-center/using/additional-configurations.md#configuring-multibranding) を参照してください。
* クライアントコンソールをインストールします。[ を参照してください。](../../installation/using/installing-the-client-console.md)
* 組み込みパッケージのインストール：[ を参照してください。](../../installation/using/installing-campaign-standard-packages.md)
* 配信品質：[MX ルール ](../../installation/using/email-deliverability.md#mx-configuration) と [ 電子メールフォーマット ](../../installation/using/email-deliverability.md#managing-email-formats) を設定します。 配信品質ツールとベストプラクティスの詳細については、[ 詳細なドキュメント ](../../delivery/using/about-deliverability.md) を参照してください。
* キャンペーンオプションの設定：[ を参照してください。](../../installation/using/configuring-campaign-options.md)
* 外部データベースの設定 (Federated Data Access):[ を参照してください。](../../installation/using/about-fda.md)
* CRM コネクタの設定：[ を参照してください。](../../platform/using/crm-connectors.md)
* ミッドソーシングデプロイメントの原則について詳しくは、[ この節 ](../../installation/using/mid-sourcing-deployment.md) を参照してください。
