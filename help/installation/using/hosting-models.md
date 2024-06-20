---
product: campaign
title: ホスティングモデル
description: Campaign ホスティングモデルの確認
feature: Installation, Architecture, Deployment
role: Architect
level: Beginner
exl-id: a06b1365-d487-4df1-8f4a-7268b871a427
source-git-commit: a38d53f4b37aadbc53446b5e399af2eae56c12af
workflow-type: tm+mt
source-wordcount: '615'
ht-degree: 0%

---

# ホスティングモデル{#hosting-models}



Adobe Campaignでは、3 つのホスティングモデルから選択でき、ビジネスニーズに合わせて最適なモデルやモデルを柔軟かつ自由に選択できます。

>[!NOTE]
>
>Adobeホスト環境の場合、サーバーの設定やインスタンス設定ファイルのカスタマイズなど、メインのインストールおよび設定手順はAdobeによってのみ実行できます。 デプロイメントモードの主な違いについて詳しくは、次を参照してください。 [このページ](../../installation/using/capability-matrix.md).

## Managed Services / ホスト

Adobe Campaignはas a Managed Serviceでデプロイできます。ユーザーインターフェイス、Execution Management Engine、顧客の Campaign データベースなど、Adobe Campaignのすべてのコンポーネントは、メール実行、ミラーページ、トラッキングサーバー、登録解除ページ/環境設定センター、ランディングページなどの外部向け web コンポーネントなど、Adobeで完全にホストされます。

![](assets/deployment_hosted.png)

ホステッド環境のお客様の場合、インストールと設定の手順のほとんどはAdobeが行います。 以下のセクションにアクセスして、実装をカスタマイズできます。

* ブランドごとにトラッキングとミラーページの URL を設定します。 トランザクションメッセージについては、を参照してください [このセクションに](../../message-center/using/additional-configurations.md#configuring-multibranding).
* クライアントコンソールをインストールします。詳しくは、 [このセクションに](../../installation/using/installing-the-client-console.md).
* 配信品質ツールとベストプラクティスについて詳しくは、を参照してください。 [詳細ドキュメント](../../delivery/using/about-deliverability.md).
* Campaign オプションの設定：を参照してください [このセクションに](../../installation/using/configuring-campaign-options.md).
* CRM コネクタの設定：を参照してください。 [このセクションに](../../platform/using/crm-connectors.md).

## オンプレミス

Adobe Campaignはオンプレミスでデプロイできます。ユーザーインターフェイス、Execution Management Engine、データベースなど、Adobe Campaignのすべてのコンポーネントは、お客様のデータセンターにオンサイトで配置されます。 このデプロイメントモデルでは、お客様はソフトウェアおよびハードウェアの更新やアップグレードをすべて管理します。また、専任のデータベース管理者がメンテナンスや最適化のタスクを実行して、Campaign インスタンスを確実に管理する必要があります。

![](assets/deployment_onpremise.png)

オンプレミス環境のお客様は、Campaign Classicのデプロイを開始する前に、次の前提条件と推奨事項に注意してください。

* を読み上げます。 [互換性マトリックス](../../rn/using/compatibility-matrix.md) に、Adobe Campaignでサポートされているシステムとコンポーネントのすべてのバージョンを示します。
* 環境に応じて、を読み上げます。 [windows の前提条件](../../installation/using/prerequisites-of-campaign-installation-in-windows.md) および [linux の前提条件](../../installation/using/prerequisites-of-campaign-installation-in-linux.md).
* データベースエンジンに関する推奨事項を説明します [この節](../../installation/using/database.md).
* 必要なデータベースアクセスレイヤーがサーバーにインストールされ、Adobe Campaign アカウントからアクセスできることを確認します。 [詳細情報](../../installation/using/application-server.md)。
* 一部のプロセスが他のプロセスと通信したり、LAN やインターネットにアクセスしたりする必要があるので、ネットワークを構成します。 つまり、これらのプロセスでは、一部の TCP ポートを開く必要があります。 [詳細情報](../../installation/using/network-configuration.md) ネットワーク構成要件について。
* 読み上げる [Campaign のセキュリティとプライバシーのチェックリスト](https://helpx.adobe.com/jp/campaign/kb/acc-security.html).
* オンプレミスデプロイメントのハードウェア要件を見積もるための一般的なガイドラインを確認します [この記事の](https://helpx.adobe.com/jp/campaign/kb/hardware-sizing-guide.html).

## ハイブリッド

Adobe Campaign ソリューションソフトウェアをハイブリッドモデルとしてデプロイする場合、お客様のサイトにオンプレミスで導入し、Adobeが Cloud Service として提供します。 Adobe Campaign マーケティングインスタンスは、顧客のファイアウォール内にインストールされているので、個人を特定できる情報（PII）は社内に残り、メールのパーソナライズに必要なデータのみがメール処理用にクラウドに送信されます。 実行インスタンスはクラウドでホストされ、メールを配信するためのリクエストをオンプレミスインスタンスから受け取ります。 このインスタンスは、すべてのメールをパーソナライズして配信します。 どのような種類のデータも、クラウドに永続的に保存されることはありません。

![](assets/deployment_hybrid.png)

ハイブリッド環境のお客様の場合、インストール手順と設定手順のほとんどはAdobeが実行します。 以下のセクションにアクセスして、実装をカスタマイズできます。

* トランザクションメッセージを設定する：を参照してください [このセクションに](../../message-center/using/transactional-messaging-architecture.md).
* ブランドごとにトラッキングとミラーページの URL を設定します。 トランザクションメッセージについては、を参照してください [このセクションに](../../message-center/using/additional-configurations.md#configuring-multibranding).
* クライアントコンソールをインストールします。詳しくは、 [このセクションに](../../installation/using/installing-the-client-console.md).
* ビルトインパッケージのインストール：を参照 [このセクションに](../../installation/using/installing-campaign-standard-packages.md).
* 配信品質：の設定 [MX ルール](../../installation/using/email-deliverability.md#mx-configuration) および [e メール形式](../../installation/using/email-deliverability.md#managing-email-formats). 配信品質ツールとベストプラクティスについて詳しくは、を参照してください。 [詳細ドキュメント](../../delivery/using/about-deliverability.md).
* Campaign オプションの設定：を参照してください [このセクションに](../../installation/using/configuring-campaign-options.md).
* 外部データベース（Federated Data Access）を設定します。詳しくは、 [このセクションに](../../installation/using/about-fda.md).
* CRM コネクタの設定：を参照してください [このセクションに](../../platform/using/crm-connectors.md).
* ミッドソーシングデプロイメントの原則について詳しくは、以下を参照してください。 [このセクションに](../../installation/using/mid-sourcing-deployment.md).
