---
title: モデルのホスティング
seo-title: モデルのホスティング
description: モデルのホスティング
seo-description: null
page-status-flag: never-activated
uuid: a9e035d9-326b-4e14-8f05-a22fe38d172b
contentOwner: sauviat
products: SG_CAMPAIGN/CLASSIC
audience: installation
content-type: reference
topic-tags: architecture-and-hosting-models
discoiquuid: 3175b9ab-e305-4f19-8267-d6172fa07a2a
translation-type: tm+mt
source-git-commit: 70b143445b2e77128b9404e35d96b39694d55335
workflow-type: tm+mt
source-wordcount: '343'
ht-degree: 4%

---


# モデルのホスティング{#hosting-models}

Adobe Campaignオファーは、3つのホスティングモデルから選択でき、最適なモデル、またはビジネスニーズに合ったモデルを柔軟に選択できます。

>[!NOTE]
>
>メインのインストールおよび設定手順は、Adobeがホストする配置に対してのみAdobeが実行できます。 例えば、サーバー設定ファイルとインスタンス設定ファイルを設定する場合です。 デプロイメントモード間の主な違いについて詳しくは、 [この記事を参照してください](https://helpx.adobe.com/jp/campaign/kb/acc-on-prem-vs-hosted.html)。 ホストモデルまたはハイブリッドモデルがある場合は、この [節を参照してください](../../installation/using/about-hybrid-and-hosted-models.md)。

* **Managed Services（ホスト）**

   Adobe Campaignは、次の管理対象サービスとして展開できます。adobe campaignインターフェイス、実行管理エンジン、および顧客のキャンペーンデータベースを含むすべてのコンポーネントは、電子メールの実行、ミラーページ、トラッキングサーバー、および登録解除ページ/環境設定センターやランディングページなどの外部対応のWebコンポーネントを含め、Adobeによって完全にホストされます。 Adobeは、クラウド内で最大3つのインスタンス（開発、テスト/ステージ、実稼動）を割り当てます。 この [節では、このホスティングモデルのインストールと設定の手順を示します](../../installation/using/hosted-model.md)。

   ![](assets/deployment_hosted.png)

* **オンプレミス**

   Adobe Campaignはオンプレミスでデプロイできます。ユーザー・インターフェース、実行管理エンジン、データベースを含むAdobe Campaignのすべてのコンポーネントは、お客様のデータ・センター内のオンサイトに存在します。 この導入モデルでは、お客様はすべてのソフトウェアおよびハードウェアの更新とアップグレードを管理し、キャンペーンインスタンスの管理を確実に行うために、保守と最適化のタスクを専任のデータベース管理者が実行する必要があります。

   ![](assets/deployment_onpremise.png)

* **ハイブリッド**

   ハイブリッドモデルとして展開する場合、Adobe Campaignソリューションソフトウェアはお客様のサイトにオンプレミスで常駐し、実行管理はクラウドサービスとしてAdobeによって提供されます。 Adobe Campaignマーケティングインスタンスは、顧客のファイアウォール内にインストールされるので、個人情報(PII)は社内に残り、電子メールのパーソナライズに必要なデータのみがCloudに送信され、電子メールを実行します。 クラウドでホストされる実行インスタンスは、電子メールを配信するためのオンプレミスインスタンスからの要求を受け取ります。 このインスタンスは、すべての電子メールをパーソナライズし、配信します。 どのような種類のデータも、クラウドに永久的に保存されません。 この [節では、このホスティングモデルのインストールと設定の手順を示します](../../installation/using/hybrid-model.md)。

   ![](assets/deployment_hybrid.png)

