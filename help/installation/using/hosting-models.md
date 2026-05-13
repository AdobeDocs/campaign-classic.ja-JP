---
product: campaign
title: ホスティングモデル
description: Campaign ホスティングモデルの詳細
feature: Installation, Architecture, Deployment
role: Developer
level: Beginner
exl-id: a06b1365-d487-4df1-8f4a-7268b871a427
TQID: https://experienceleague.adobe.com/9pZQYt2gLVR94ZWsw21JCv7CL55KDRyiqocvuS54SbM
product_v2:
  - id: dfc56824-e8b9-499e-85d4-21aedb507314
feature_v2:
  - id: a7760dfc-5c44-4d77-bb68-c50b1e265c93
subfeature_v2:
  - id: ac9c0a9c-8a76-4419-bd64-9c34c5782666
  - id: fb2a841f-c522-491f-9901-a1b939d252df
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
level_v2:
  - id: e8ccd51f-da0d-4e3b-939b-e30d5ebb1ea5
topic_v2:
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
  - id: cdd65e7e-8839-44a2-bc21-0e03623b5dd1
  - id: d095671a-1355-40aa-8b5f-06c33c68080b
  - id: f4e6943a-c91a-4134-a2c7-f4f20cfff2f0
source-git-commit: 4c295c0dabae8aba298390a3da2422a3fa1219f9
workflow-type: tm+mt
source-wordcount: 637
ht-degree: 3%

---

# ホスティングモデル{#hosting-models}



Adobe Campaignでは、3つのホスティングモデルから選択でき、ビジネスニーズに合わせて最適なモデルやモデルを柔軟に選択できます。

>[!NOTE]
>
>Adobeでホストされている環境の場合、メインインストールと設定の手順は、サーバーの設定やインスタンス設定ファイルのカスタマイズなど、Adobeでのみ実行できます。 デプロイメントモードの主な違いについて詳しくは、[このページ &#x200B;](../../installation/using/capability-matrix.md)を参照してください。

## Managed Services / ホスト型

Adobe Campaignをデプロイできます。as a Managed Service: ユーザーインターフェイス、実行管理エンジン、お客様のCampaign データベースなど、Adobe Campaignのすべてのコンポーネントは、メール実行、ミラーページ、トラッキングサーバー、配信停止ページ/プリファレンスセンターやランディングページなどの外部に向かうweb コンポーネントなど、Adobeによって完全にホストされます。

![](assets/deployment_hosted.png)

ホストされているお客様は、インストールと設定の手順のほとんどをAdobeで実行できます。 以下のセクションにアクセスして、実装をカスタマイズできます。

* ブランドごとにトラッキングページとミラーページのURLを設定します。 トランザクションメッセージについては、[この節](../../message-center/using/additional-configurations.md#configuring-multibranding)を参照してください。
* クライアントコンソールをインストールします。[この節](../../installation/using/installing-the-client-console.md)を参照してください。
* 配信品質ツールとベストプラクティスについて詳しくは、[詳細ドキュメント &#x200B;](../../delivery/using/about-deliverability.md)を参照してください。
* Campaign オプションの設定：この節の[を参照してください](../../installation/using/configuring-campaign-options.md)。
* CRM コネクタの設定：このセクションについては[を参照してください](../../platform/using/crm-connectors.md)。

## オンプレミス

Adobe Campaignはオンプレミスでデプロイできます。ユーザーインターフェイス、実行管理エンジン、データベースなど、Adobe Campaignのすべてのコンポーネントは、お客様のデータセンターにオンサイトで保管されます。 このデプロイメントモデルでは、お客様がすべてのソフトウェアとハードウェアのアップデートとアップグレードを管理します。Campaign インスタンス管理を確実に行うには、専用のデータベース管理者がメンテナンスと最適化タスクを実行する必要があります。

![](assets/deployment_onpremise.png)

オンプレミス環境のお客様は、Campaign Classicの導入を開始する前に、次の前提条件と推奨事項に注意してください。

* Adobe Campaignでサポートされているシステムとコンポーネントのすべてのバージョンを一覧表示する[互換性マトリックス &#x200B;](../../rn/using/compatibility-matrix.md)を読んでください。
* お使いの環境に応じて、「[Windowsの前提条件](../../installation/using/prerequisites-of-campaign-installation-in-windows.md)」と「[Linuxの前提条件](../../installation/using/prerequisites-of-campaign-installation-in-linux.md)」をお読みください。
* データベース エンジン [に関する推奨事項については、この節](../../installation/using/database.md)を参照してください。
* 必要なデータベースアクセスレイヤーがサーバーにインストールされ、Adobe Campaign アカウントからアクセスできることを確認します。 [詳細情報](../../installation/using/application-server.md)。
* 一部のプロセスが他のプロセスと通信したり、LANやインターネットにアクセスしたりする必要があるため、ネットワークを設定します。 つまり、一部のTCP ポートは、これらのプロセスに対してオープンにする必要があります。 ネットワーク構成の要件について[詳細](../../installation/using/network-configuration.md)を確認します。
* [Campaign セキュリティとプライバシーのチェックリスト &#x200B;](https://helpx.adobe.com/jp/campaign/kb/acc-security.html)をお読みください。
* オンプレミス展開[のハードウェア要件の見積もりに関する一般的なガイドラインについては、この記事](https://helpx.adobe.com/jp/campaign/kb/hardware-sizing-guide.html)を参照してください。

## ハイブリッド

ハイブリッドモデルとして導入した場合、Adobe Campaignソリューションソフトウェアは顧客サイトのオンプレミスで使用され、実行管理はAdobeによってクラウドサービスとして提供されます。 Adobe Campaignのマーケティングインスタンスは、顧客のファイアウォール内にインストールされるため、PII （個人を特定できる情報）は社内に保持され、電子メールをパーソナライズするために必要なデータのみがクラウドに送信され、電子メールを実行できます。 実行インスタンスは、クラウドでホストされ、オンプレミスインスタンスからリクエストを受信してメールを配信します。 このインスタンスでは、すべてのメールをパーソナライズして配信します。 いかなる種類のデータも、クラウドに永続的に保存されることはありません。

![](assets/deployment_hybrid.png)

ハイブリッド版のお客様は、ほとんどのインストールおよび設定手順をAdobeで実行できます。 以下のセクションにアクセスして、実装をカスタマイズできます。

* トランザクションメッセージの設定：このセクションについては[を参照してください](../../message-center/using/transactional-messaging-architecture.md)。
* ブランドごとにトラッキングページとミラーページのURLを設定します。 トランザクションメッセージについては、[この節](../../message-center/using/additional-configurations.md#configuring-multibranding)を参照してください。
* クライアントコンソールをインストールします。[この節](../../installation/using/installing-the-client-console.md)を参照してください。
* 組み込みパッケージをインストールします。このセクションについては[を参照してください](../../installation/using/installing-campaign-standard-packages.md)。
* 配信品質：[MX ルール &#x200B;](../../installation/using/email-deliverability.md#mx-configuration)と[&#x200B; メール形式](../../installation/using/email-deliverability.md#managing-email-formats)を設定します。 配信品質ツールとベストプラクティスについて詳しくは、[詳細ドキュメント &#x200B;](../../delivery/using/about-deliverability.md)を参照してください。
* Campaign オプションの設定：この節の[を参照してください](../../installation/using/configuring-campaign-options.md)。
* 外部データベース （Federated Data Access）を設定します。この節は[を参照してください](../../installation/using/about-fda.md)。
* CRM コネクタの設定：このセクションについては[を参照してください](../../platform/using/crm-connectors.md)。
* ミッドソーシングのデプロイメント原則について詳しくは、この節[を参照してください](../../installation/using/mid-sourcing-deployment.md)。
