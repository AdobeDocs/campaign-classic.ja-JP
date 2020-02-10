---
title: モデルのホスト
seo-title: モデルのホスト
description: モデルのホスト
seo-description: null
page-status-flag: never-activated
uuid: a9e035d9-326b-4e14-8f05-a22fe38d172b
contentOwner: sauviat
products: SG_CAMPAIGN/CLASSIC
audience: installation
content-type: reference
topic-tags: architecture-and-hosting-models
discoiquuid: 3175b9ab-e305-4f19-8267-d6172fa07a2a
index: y
internal: n
snippet: y
translation-type: tm+mt
source-git-commit: 46f5bfb41bfe9c938ac0ffa767ead3e47a32047d

---


# モデルのホスト{#hosting-models}

Adobe Campaignは、3つのホスティングモデルから選択でき、ビジネスニーズに合った最適なモデルやモデルを柔軟に選択できるようにします。

>[!NOTE]
>
>メインのインストールおよび設定手順は、アドビがホストするデプロイメントに対してのみ実行できます。 例えば、サーバーおよびインスタンスの設定ファイルを設定する場合です。 展開モードの主な違いについて詳しくは、この記事を参照し [てください](https://helpx.adobe.com/campaign/kb/acc-on-prem-vs-hosted.html)。 ホストモデルまたはハイブリッドモデルがある場合は、この節を参照してく [ださい](../../installation/using/about-hybrid-and-hosted-models.md)。

* **マネージドサービス（ホスト）**

   Adobe Campaignは、管理サービスとして展開できます。ユーザーインターフェイス、実行管理エンジン、顧客のCampaignデータベースを含むAdobe Campaignのすべてのコンポーネントは、電子メールの実行、ミラーページ、トラッキングサーバー、登録解除ページ/環境設定センター、ランディングページなど、外部に接続するWebコンポーネントを含め、アドビによって完全にホストされます。 アドビは、開発、テスト/ステージ、実稼動の3つまでのインスタンスをクラウドに割り当てます。 このホスティングモデルのインストールと設定の手順をこの節で説明 [します](../../installation/using/hosted-model.md)。

   ![](assets/deployment_hosted.png)

* **オンプレミス**

   Adobe Campaignはオンプレミスでデプロイできます。ユーザーインターフェイス、実行管理エンジン、データベースを含む、Adobe Campaignのすべてのコンポーネントは、お客様のデータセンターのオンサイトに存在します。 この導入モデルでは、お客様がすべてのソフトウェアおよびハードウェアの更新とアップグレードを管理し、専用のデータベース管理者がCampaignインスタンス管理を確実に行うための保守と最適化のタスクを実行する必要があります。

   ![](assets/deployment_onpremise.png)

* **ハイブリッド**

   ハイブリッドモデルとして展開する場合、Adobe Campaignソリューションソフトウェアはお客様のサイトにオンプレミスで常駐し、実行管理はクラウドサービスとしてアドビから提供されます。 Adobe Campaignマーケティングインスタンスは、顧客のファイアウォール内にインストールされるので、個人情報(PII)は社内に残り、電子メールのパーソナライズに必要なデータのみがCloudに送信され、電子メールを実行します。 クラウドでホストされる実行インスタンスは、電子メールを配信するためのOn-Premiseインスタンスからの要求を受け取ります。 このインスタンスは、すべての電子メールをパーソナライズし、配信します。 どの種類のデータもクラウドに永続的に保存されません。 このホスティングモデルのインストールと設定の手順をこの節で説明 [します](../../installation/using/hybrid-model.md)。

   ![](assets/deployment_hybrid.png)

