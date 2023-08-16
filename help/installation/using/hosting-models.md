---
product: campaign
title: ホスティングモデル
description: Campaign のホスティングモデルを確認する
feature: Installation, Architecture, Deployment
badge-v7-only: label="v7" type="Informative" tooltip="Campaign Classic v7 にのみ適用されます"
role: Architect
level: Beginner
exl-id: a06b1365-d487-4df1-8f4a-7268b871a427
source-git-commit: 3a9b21d626b60754789c3f594ba798309f62a553
workflow-type: tm+mt
source-wordcount: '630'
ht-degree: 3%

---

# ホスティングモデル{#hosting-models}



Adobe Campaignは、3 つのホスティングモデルから選択でき、ビジネスニーズに合わせて最適なモデル（モデル）を柔軟に選択でき、自由に選択できます。

>[!NOTE]
>
>Adobeがホストする環境では、サーバーの設定やインスタンス設定ファイルのカスタマイズなど、Adobeのみが主なインストールおよび設定手順を実行できます。 デプロイメントモード間の主な違いについて詳しくは、 [このページ](../../installation/using/capability-matrix.md).

## Managed Services/ホスト

Adobe Campaignはas a Managed Service的にデプロイできます。Adobe Campaignのすべてのコンポーネント（ユーザーインターフェイス、実行管理エンジン、顧客の Campaign データベースを含む）は、E メールの実行、ミラーページ、トラッキングサーバー、配信停止ページ/環境設定センター、ランディングページなど、Adobeで完全にホストします。

![](assets/deployment_hosted.png)

ホスト版のお客様は、インストールおよび設定手順のほとんどをAdobeが実行します。 以下のセクションにアクセスして、実装をカスタマイズできます。

* ブランドごとにトラッキングとミラーページの URL を設定します。 トランザクションメッセージについては、 [このセクションに](../../message-center/using/additional-configurations.md#configuring-multibranding).
* クライアントコンソールをインストールします。を参照してください。 [このセクションに](../../installation/using/installing-the-client-console.md).
* 配信品質ツールとベストプラクティスの詳細については、 [詳細なドキュメント](../../delivery/using/about-deliverability.md).
* キャンペーンオプションの設定：を参照してください。 [このセクションに](../../installation/using/configuring-campaign-options.md).
* CRM コネクタを設定します。を参照してください。 [このセクションに](../../platform/using/crm-connectors.md).

## オンプレミス

Adobe Campaignはオンプレミスでデプロイできます。ユーザーインターフェイス、実行管理エンジン、データベースを含む、Adobe Campaignのすべてのコンポーネントは、お客様のデータセンターのオンサイトに配置されます。 このデプロイメントモデルでは、お客様はすべてのソフトウェアとハードウェアの更新とアップグレードを管理し、専用のデータベース管理者は、Campaign インスタンスの管理を確実におこなうためのメンテナンスと最適化のタスクを実行する必要があります。

![](assets/deployment_onpremise.png)

オンプレミス型のお客様は、Campaign Classicのデプロイを開始する前に、次の前提条件と推奨事項に従ってください。

* 詳しくは、 [互換性マトリックス](../../rn/using/compatibility-matrix.md) Adobe Campaignでサポートされているシステムとコンポーネントのすべてのバージョンを示しています。
* ご使用の環境に応じて、 [Windows の前提条件](../../installation/using/prerequisites-of-campaign-installation-in-windows.md) および [Linux の前提条件](../../installation/using/prerequisites-of-campaign-installation-in-linux.md).
* データベースエンジンに関する推奨事項について説明します。 [この節](../../installation/using/database.md).
* 必要なデータベースアクセスレイヤーがサーバーにインストールされ、Adobe Campaignアカウントからアクセスできることを確認します。 [詳細情報](../../installation/using/application-server.md)
* 一部のプロセスは、他のプロセスと通信したり、LAN やインターネットにアクセスしたりする必要があるので、ネットワークを設定します。 つまり、これらのプロセスでは、一部の TCP ポートを開く必要があります。 [詳細情報](../../installation/using/network-configuration.md) ネットワーク構成の要件について
* 読み取り [Campaign のセキュリティおよびプライバシーチェックリスト](https://helpx.adobe.com/jp/campaign/kb/acc-security.html).
* オンプレミスデプロイメント用のハードウェア要件の見積もりに関する一般的なガイドラインを確認します。 [この記事では、](https://helpx.adobe.com/jp/campaign/kb/hardware-sizing-guide.html).

## ハイブリッド

ハイブリッドモデルとしてデプロイする場合、Adobe Campaignソリューションソフトウェアはお客様のサイトにオンプレミスで配置され、実行管理はAdobeによってクラウドサービスとして提供されます。 Adobe Campaign Marketing インスタンスは、顧客のファイアウォール内にインストールされるので、個人を特定できる情報 (PII) は社内に残り、E メールのパーソナライズに必要なデータのみが E メールの実行のために Cloud に送信されます。 クラウドでホストされる実行インスタンスは、On-Premise インスタンスから E メールを配信する要求を受け取ります。 このインスタンスは、すべての E メールをパーソナライズして配信します。 どのような種類のデータも、クラウドに永続的に保存されません。

![](assets/deployment_hybrid.png)

ハイブリッドのお客様は、インストールおよび設定手順のほとんどをAdobeで実行します。 以下のセクションにアクセスして、実装をカスタマイズできます。

* トランザクションメッセージの設定：を参照してください。 [このセクションに](../../message-center/using/transactional-messaging-architecture.md).
* ブランドごとにトラッキングとミラーページの URL を設定します。 トランザクションメッセージについては、 [このセクションに](../../message-center/using/additional-configurations.md#configuring-multibranding).
* クライアントコンソールをインストールします。を参照してください。 [このセクションに](../../installation/using/installing-the-client-console.md).
* 組み込みパッケージのインストール：を参照してください。 [このセクションに](../../installation/using/installing-campaign-standard-packages.md).
* 配信品質：設定 [MX ルール](../../installation/using/email-deliverability.md#mx-configuration) および [電子メールの形式](../../installation/using/email-deliverability.md#managing-email-formats). 配信品質ツールとベストプラクティスの詳細については、 [詳細なドキュメント](../../delivery/using/about-deliverability.md).
* キャンペーンオプションの設定：を参照してください。 [このセクションに](../../installation/using/configuring-campaign-options.md).
* 外部データベース (Federated Data Access) の設定：を参照してください。 [このセクションに](../../installation/using/about-fda.md).
* CRM コネクタの設定：を参照してください。 [このセクションに](../../platform/using/crm-connectors.md).
* ミッドソーシングデプロイメントの原則について詳しくは、 [このセクションに](../../installation/using/mid-sourcing-deployment.md).
