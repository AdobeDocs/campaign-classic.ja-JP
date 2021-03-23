---
solution: Campaign Classic
product: campaign
title: ホスティングのモデル
description: Discoverキャンペーンのホスティングモデル
feature: 概要
role: 建築家
level: 初心者
translation-type: tm+mt
source-git-commit: 09bd634142f643206c38ac5f881302a5d489ecaf
workflow-type: tm+mt
source-wordcount: '626'
ht-degree: 3%

---


# ホスティングのモデル{#hosting-models}

Adobe Campaignオファーは、3つのホスティングモデルから選択でき、最適なモデル、またはビジネスニーズに合ったモデルを柔軟に選択できます。

>[!NOTE]
>
>Adobeがホストする環境の場合、メインのインストールと設定の手順は、Adobe（サーバーの設定、インスタンス設定ファイルのカスタマイズなど）によってのみ実行できます。 展開モードの主な違いについて詳しくは、[このページ](../../installation/using/capability-matrix.md)を参照してください。

## Managed Services/ホスト

Adobe Campaignは、次の管理対象サービスとして展開できます。Adobe Campaignインターフェイス、実行管理エンジン、および顧客のキャンペーンデータベースを含むすべてのコンポーネントは、電子メールの実行、ミラーページ、トラッキングサーバー、および登録解除ページ/環境設定センターやランディングページなどの外部対応のWebコンポーネントを含め、Adobeによって完全にホストされます。

![](assets/deployment_hosted.png)

ホストのお客様は、インストールと設定のほとんどの手順をAdobeが実行します。 以下のセクションにアクセスして、実装をカスタマイズできます。

* ブランドごとのトラッキングURLとミラーページURLを設定します。 トランザクションメッセージについては、[このセクション](../../message-center/using/configuring-multibranding.md)を参照してください。
* クライアントコンソールをインストールします。[を参照して、](../../installation/using/installing-the-client-console.md)を参照してください。
* 配信品質のツールとベストプラクティスについて詳しくは、[詳細なドキュメント](../../delivery/using/about-deliverability.md)を参照してください。
* キャンペーンオプションの設定：[を参照して、](../../installation/using/configuring-campaign-options.md)を参照してください。
* CRMコネクタの設定：[を参照して、](../../platform/using/crm-connectors.md)を参照してください。

## オンプレミス

Adobe Campaignはオンプレミスでデプロイできます。ユーザー・インターフェース、実行管理エンジン、データベースを含むAdobe Campaignのすべてのコンポーネントは、お客様のデータ・センター内のオンサイトに存在します。 この導入モデルでは、お客様はすべてのソフトウェアおよびハードウェアの更新とアップグレードを管理し、キャンペーンインスタンスの管理を確実に行うために、保守と最適化のタスクを専任のデータベース管理者が実行する必要があります。

![](assets/deployment_onpremise.png)

オンプレミスのお客様は、Campaign Classicのデプロイを開始する前に、次の前提条件および推奨事項に注意してください。

* [互換表](../../rn/using/compatibility-matrix.md)を読み取り、Adobe Campaignに対してサポートされるシステムとコンポーネントの全バージョンをリストします。
* 環境に応じて、Windows](../../installation/using/prerequisites-of-campaign-installation-in-windows.md)の[前提条件とLinux](../../installation/using/prerequisites-of-campaign-installation-in-linux.md)の[前提条件を読み上げます。
* この節](../../installation/using/database.md)では、データベースエンジン[に関する推奨事項を説明します。
* 必要なデータベースアクセスレイヤーがサーバーにインストールされ、Adobe Campaignアカウントからアクセスできることを確認します。 [詳細情報](../../installation/using/application-server.md)。
* 一部のプロセスが他のプロセスと通信したり、LANやインターネットにアクセスしたりする必要があるので、ネットワークを設定します。 これは、一部のTCPポートをこれらのプロセスで開く必要があることを意味します。 [ネットワーク構成の要件](../../installation/using/network-configuration.md) について詳しく説明します。
* [キャンペーンセキュリティとプライバシーのチェックリスト](https://helpx.adobe.com/jp/campaign/kb/acc-security.html)を読み上げます。
* この記事](https://helpx.adobe.com/jp/campaign/kb/hardware-sizing-guide.html)で、オンプレミスデプロイメント[のハードウェア要件を見積もる際の一般的なガイドラインを確認してください。

## ハイブリッド

ハイブリッドモデルとして展開する場合、Adobe Campaignソリューションソフトウェアはお客様のサイトにオンプレミスで常駐し、実行管理はクラウドサービスとしてAdobeによって提供されます。 Adobe Campaignマーケティングインスタンスは、顧客のファイアウォール内にインストールされるので、個人情報(PII)は社内に残り、電子メールのパーソナライズに必要なデータのみがCloudに送信され、電子メールを実行します。 クラウドでホストされる実行インスタンスは、電子メールを配信するためのオンプレミスインスタンスからの要求を受け取ります。 このインスタンスは、すべての電子メールをパーソナライズし、配信します。 どのような種類のデータも、クラウドに永久的に保存されません。

![](assets/deployment_hybrid.png)

ハイブリッドなお客様の場合、インストールと設定のほとんどの手順はAdobeが実行します。 以下のセクションにアクセスして、実装をカスタマイズできます。

* トランザクションメッセージの設定：[を参照して、](../../message-center/using/transactional-messaging-architecture.md)を参照してください。
* ブランドごとのトラッキングURLとミラーページURLを設定します。 トランザクションメッセージについては、[このセクション](../../message-center/using/configuring-multibranding.md)を参照してください。
* クライアントコンソールをインストールします。[を参照して、](../../installation/using/installing-the-client-console.md)を参照してください。
* 組み込みパッケージのインストール：[を参照して、](../../installation/using/installing-campaign-standard-packages.md)を参照してください。
* 配信品質：[MXルール](../../installation/using/email-deliverability.md#mx-configuration)と[E メールフォーマット](../../installation/using/email-deliverability.md#managing-email-formats)を構成します。 配信品質のツールとベストプラクティスについて詳しくは、[詳細なドキュメント](../../delivery/using/about-deliverability.md)を参照してください。
* キャンペーンオプションの設定：[を参照して、](../../installation/using/configuring-campaign-options.md)を参照してください。
* 外部データベース(Federated Data Access)の設定：[を参照して、](../../installation/using/about-fda.md)を参照してください。
* CRMコネクタの設定：[を参照して、](../../platform/using/crm-connectors.md)を参照してください。
* ミッドソーシング導入の原則についての詳細は、[このセクション](../../installation/using/mid-sourcing-deployment.md)を参照してください。
