---
product: campaign
title: ホスティングモデル
description: Campaign ホスティングモデルの確認
feature: Installation, Architecture, Deployment
role: Developer
level: Beginner
exl-id: a06b1365-d487-4df1-8f4a-7268b871a427
source-git-commit: 9f5205ced6b8d81639d4d0cb6a76905a753cddac
workflow-type: tm+mt
source-wordcount: '615'
ht-degree: 1%

---

# ホスティングモデル{#hosting-models}



Adobe Campaignでは、3 つのホスティングモデルから選択でき、ビジネスニーズに合わせて最適なモデルやモデルを柔軟かつ自由に選択できます。

>[!NOTE]
>
>Adobeがホストする環境の場合、サーバーの設定やインスタンス設定ファイルのカスタマイズなど、主なインストール手順と設定手順は、Adobeによってのみ実行できます。 デプロイメントモードの主な違いについて詳しくは、[&#x200B; このページ &#x200B;](../../installation/using/capability-matrix.md) を参照してください。

## Managed Services / ホスト

Adobe Campaignは、as a Managed Serviceにデプロイできます。ユーザーインターフェイス、Execution Management Engine、顧客の Campaign データベースなど、Adobe Campaignのすべてのコンポーネントは、Adobeで完全にホストされます。これには、メール実行、ミラーページ、トラッキングサーバー、登録解除ページ/環境設定センターやランディングページなどの外部向け web コンポーネントが含まれます。

![](assets/deployment_hosted.png)

ホステッド環境のお客様の場合、インストールと設定の手順のほとんどはAdobeによって実行されます。 以下のセクションにアクセスして、実装をカスタマイズできます。

* ブランドごとにトラッキングとミラーページの URL を設定します。 トランザクションメッセージについては、[&#x200B; この節 &#x200B;](../../message-center/using/additional-configurations.md#configuring-multibranding) を参照してください。
* クライアントコンソールをインストールします。[&#x200B; この節 &#x200B;](../../installation/using/installing-the-client-console.md) を参照してください。
* 配信品質ツールとベストプラクティスについて詳しくは、[&#x200B; 詳細ドキュメント &#x200B;](../../delivery/using/about-deliverability.md) を参照してください。
* Campaign オプションを設定します。[&#x200B; この節 &#x200B;](../../installation/using/configuring-campaign-options.md) を参照してください。
* CRM コネクタを設定します。[&#x200B; この節 &#x200B;](../../platform/using/crm-connectors.md) を参照してください。

## オンプレミス

Adobe Campaignはオンプレミスでデプロイできます。ユーザーインターフェイス、Execution Management Engine、データベースなど、Adobe Campaignのすべてのコンポーネントは、お客様のデータセンターにオンサイトで配置されます。 このデプロイメントモデルでは、お客様はソフトウェアおよびハードウェアの更新やアップグレードをすべて管理します。また、専任のデータベース管理者がメンテナンスや最適化のタスクを実行して、Campaign インスタンスを確実に管理する必要があります。

![](assets/deployment_onpremise.png)

オンプレミス環境のお客様は、Campaign Classicのデプロイを開始する前に、次の前提条件と推奨事項に注意してください。

* Adobe Campaignでサポートされているシステムおよびコンポーネントのすべてのバージョンが記載されている [&#x200B; 互換性マトリックス &#x200B;](../../rn/using/compatibility-matrix.md) を参照してください。
* 環境に応じて、[Windows の前提条件 &#x200B;](../../installation/using/prerequisites-of-campaign-installation-in-windows.md) および [Linux の前提条件 &#x200B;](../../installation/using/prerequisites-of-campaign-installation-in-linux.md) を参照してください。
* データベースエンジンに関する推奨事項について説明します [&#x200B; この節 &#x200B;](../../installation/using/database.md)。
* 必要なデータベースアクセスレイヤーがサーバーにインストールされ、Adobe Campaign アカウントからアクセスできることを確認します。 [詳細情報](../../installation/using/application-server.md)。
* 一部のプロセスが他のプロセスと通信したり、LAN やインターネットにアクセスしたりする必要があるので、ネットワークを構成します。 つまり、これらのプロセスでは、一部の TCP ポートを開く必要があります。 ネットワーク構成の要件について [&#x200B; 詳細情報 &#x200B;](../../installation/using/network-configuration.md) します。
* [Campaign のセキュリティとプライバシーのチェックリスト &#x200B;](https://helpx.adobe.com/jp/campaign/kb/acc-security.html) を参照してください。
* オンプレミスデプロイメントのハードウェア要件を見積もるための一般的なガイドラインを確認してください [&#x200B; この記事を参照してください &#x200B;](https://helpx.adobe.com/jp/campaign/kb/hardware-sizing-guide.html)。

## ハイブリッド

Adobe Campaign ソリューションソフトウェアをハイブリッドモデルとしてデプロイする場合は、お客様のサイトにオンプレミスで配置され、Adobeによって Cloud Service として Execution Management が提供されます。 Adobe Campaign マーケティングインスタンスは、顧客のファイアウォール内にインストールされているので、個人を特定できる情報（PII）は社内に残り、メールのパーソナライズに必要なデータのみがメール処理用にクラウドに送信されます。 実行インスタンスはクラウドでホストされ、メールを配信するためのリクエストをオンプレミスインスタンスから受け取ります。 このインスタンスは、すべてのメールをパーソナライズして配信します。 どのような種類のデータも、クラウドに永続的に保存されることはありません。

![](assets/deployment_hybrid.png)

ハイブリッド環境のお客様の場合、インストール手順と設定手順のほとんどはAdobeによって実行されます。 以下のセクションにアクセスして、実装をカスタマイズできます。

* トランザクションメッセージを設定します。[&#x200B; この節 &#x200B;](../../message-center/using/transactional-messaging-architecture.md) を参照してください。
* ブランドごとにトラッキングとミラーページの URL を設定します。 トランザクションメッセージについては、[&#x200B; この節 &#x200B;](../../message-center/using/additional-configurations.md#configuring-multibranding) を参照してください。
* クライアントコンソールをインストールします。[&#x200B; この節 &#x200B;](../../installation/using/installing-the-client-console.md) を参照してください。
* ビルトインパッケージをインストールします。[&#x200B; この節を参照 &#x200B;](../../installation/using/installing-campaign-standard-packages.md)。
* 配信品質：[MX ルール &#x200B;](../../installation/using/email-deliverability.md#mx-configuration) および [&#x200B; メール形式 &#x200B;](../../installation/using/email-deliverability.md#managing-email-formats) を設定します。 配信品質ツールとベストプラクティスについて詳しくは、[&#x200B; 詳細ドキュメント &#x200B;](../../delivery/using/about-deliverability.md) を参照してください。
* Campaign オプションを設定します。[&#x200B; この節 &#x200B;](../../installation/using/configuring-campaign-options.md) を参照してください。
* 外部データベース（Federated Data Access）を設定します。[&#x200B; この節 &#x200B;](../../installation/using/about-fda.md) を参照してください。
* CRM コネクタの設定：[&#x200B; この節 &#x200B;](../../platform/using/crm-connectors.md) を参照してください。
* ミッドソーシングデプロイメントの原則について詳しくは、[&#x200B; この節 &#x200B;](../../installation/using/mid-sourcing-deployment.md) を参照してください。
