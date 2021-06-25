---
product: campaign
title: ホスティングモデル
description: Campaignのホスティングモデルの理解
feature: 概要
role: Architect
level: Beginner
exl-id: a06b1365-d487-4df1-8f4a-7268b871a427
source-git-commit: 515587695115c23d9b248ecb87a7ae89ea7c62a0
workflow-type: tm+mt
source-wordcount: '624'
ht-degree: 2%

---

# ホスティングモデル{#hosting-models}

Adobe Campaignは、3種類のホスティングモデルから選択でき、ビジネスニーズに合った最適なモデル（モデル）を柔軟かつ自由に選択できます。

>[!NOTE]
>
>Adobeがホストする環境では、サーバーの設定やインスタンス設定ファイルのカスタマイズなど、主なインストールおよび設定手順はAdobeのみ実行できます。 デプロイメントモード間の主な違いについて詳しくは、[このページ](../../installation/using/capability-matrix.md)を参照してください。

## Managed Services/ホスト

Adobe Campaignは、次のようにManaged Serviceとしてデプロイできます。ユーザーインターフェイス、実行管理エンジン、お客様のCampaignデータベースを含むAdobe Campaignのすべてのコンポーネントは、電子メールの実行、ミラーページ、トラッキングサーバー、購読解除ページ/環境設定センターやランディングページなど、外部に接続するWebコンポーネントで完全にホストされます。

![](assets/deployment_hosted.png)

ホスト版のお客様は、ほとんどのインストールおよび設定手順をAdobeで実行します。 以下のセクションにアクセスして実装をカスタマイズできます。

* ブランドごとのトラッキングおよびミラーページURLの設定 トランザクションメッセージについては、[をこの節](../../message-center/using/additional-configurations.md#configuring-multibranding)で参照してください。
* クライアントコンソールをインストールします。この節](../../installation/using/installing-the-client-console.md)を[で参照してください。
* 配信品質ツールとベストプラクティスの詳細については、[詳細なドキュメント](../../delivery/using/about-deliverability.md)を参照してください。
* キャンペーンオプションの設定：この節](../../installation/using/configuring-campaign-options.md)を[で参照してください。
* CRMコネクタを設定します。この節](../../platform/using/crm-connectors.md)を[で参照してください。

## オンプレミス

Adobe Campaignはオンプレミスでデプロイできます。ユーザーインターフェイス、実行管理エンジン、データベースを含むAdobe Campaignのすべてのコンポーネントは、お客様のデータセンターのオンサイトに存在します。 このデプロイメントモデルでは、お客様はすべてのソフトウェアとハードウェアの更新とアップグレードを管理し、専用のデータベース管理者がメンテナンスと最適化のタスクを実行してCampaignインスタンスを確実に管理する必要があります。

![](assets/deployment_onpremise.png)

オンプレミス型のお客様は、Campaign Classicのデプロイを開始する前に、次の前提条件と推奨事項に注意してください。

* [互換性マトリックス](../../rn/using/compatibility-matrix.md)を読み、Adobe Campaignでサポートされているすべてのバージョンのシステムとコンポーネントを示します。
* 環境に応じて、Windows](../../installation/using/prerequisites-of-campaign-installation-in-windows.md)の[前提条件とLinux](../../installation/using/prerequisites-of-campaign-installation-in-linux.md)の[前提条件を確認します。
* データベースエンジン[に関する推奨事項については、この節](../../installation/using/database.md)を参照してください。
* 必要なデータベースアクセスレイヤーがサーバーにインストールされ、Adobe Campaignアカウントからアクセスできることを確認します。 [詳細情報](../../installation/using/application-server.md)。
* 一部のプロセスは他のプロセスと通信したり、LANやインターネットにアクセスしたりする必要があるので、ネットワークを設定します。 これは、これらのプロセスに対して一部のTCPポートを開く必要があることを意味します。 [ネットワーク](../../installation/using/network-configuration.md) 構成要件の詳細を説明します。
* [Campaignのセキュリティとプライバシーのチェックリスト](https://helpx.adobe.com/jp/campaign/kb/acc-security.html)を参照してください。
* オンプレミスデプロイメントのハードウェア要件の推定に関する一般的なガイドラインを確認します。[](https://helpx.adobe.com/jp/campaign/kb/hardware-sizing-guide.html)

## ハイブリッド

ハイブリッドモデルとしてデプロイする場合、Adobe Campaignソリューションソフトウェアはオンプレミスで顧客サイトに存在し、実行管理はAdobeによってクラウドサービスとして提供されます。 Adobe Campaign Marketingインスタンスは顧客のファイアウォール内にインストールされるので、個人情報(PII)は社内に残り、Eメールのパーソナライズに必要なデータのみがEメールの実行のためにCloudに送信されます。 クラウドでホストされる実行インスタンスは、オンプレミスインスタンスからEメールを配信する要求を受け取ります。 このインスタンスは、すべてのEメールをパーソナライズして配信します。 どのような種類のデータも、クラウドに永続的に保存されません。

![](assets/deployment_hybrid.png)

ハイブリッドのお客様は、インストールおよび設定手順のほとんどをAdobeで実行します。 以下のセクションにアクセスして実装をカスタマイズできます。

* トランザクションメッセージの設定：この節](../../message-center/using/transactional-messaging-architecture.md)を[で参照してください。
* ブランドごとのトラッキングおよびミラーページURLの設定 トランザクションメッセージについては、[をこの節](../../message-center/using/additional-configurations.md#configuring-multibranding)で参照してください。
* クライアントコンソールをインストールします。この節](../../installation/using/installing-the-client-console.md)を[で参照してください。
* 組み込みパッケージのインストール：この節](../../installation/using/installing-campaign-standard-packages.md)を[で参照してください。
* 配信品質：[MXルール](../../installation/using/email-deliverability.md#mx-configuration)と[eメールフォーマット](../../installation/using/email-deliverability.md#managing-email-formats)を設定します。 配信品質ツールとベストプラクティスの詳細については、[詳細なドキュメント](../../delivery/using/about-deliverability.md)を参照してください。
* キャンペーンオプションの設定：この節](../../installation/using/configuring-campaign-options.md)を[で参照してください。
* 外部データベース(Federated Data Access)の設定：この節](../../installation/using/about-fda.md)を[で参照してください。
* CRMコネクタの設定：この節](../../platform/using/crm-connectors.md)を[で参照してください。
* ミッドソーシングデプロイメントの原則について詳しくは、[この節](../../installation/using/mid-sourcing-deployment.md)を参照してください。
