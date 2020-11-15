---
title: ホスティングのモデル
description: Discoverキャンペーンのホスティングモデル
page-status-flag: never-activated
uuid: a9e035d9-326b-4e14-8f05-a22fe38d172b
contentOwner: sauviat
products: SG_CAMPAIGN/CLASSIC
audience: installation
content-type: reference
topic-tags: architecture-and-hosting-models
discoiquuid: 3175b9ab-e305-4f19-8267-d6172fa07a2a
translation-type: tm+mt
source-git-commit: 24521f77d6d13f8469869fdd8445b46a8d215dad
workflow-type: tm+mt
source-wordcount: '334'
ht-degree: 1%

---


# ホスティングのモデル{#hosting-models}

Adobe Campaignオファーは、3つのホスティングモデルから選択でき、最適なモデル、またはビジネスニーズに合ったモデルを柔軟に選択できます。

>[!NOTE]
>
>Adobeがホストする環境の場合、メインのインストールと設定の手順は、Adobe（サーバーの設定、インスタンス設定ファイルのカスタマイズなど）によってのみ実行できます。 デプロイメントモード間の主な違いについて詳しくは、 [このページを参照してください](../../installation/using/capability-matrix.md)。

* **Managed Services（ホスト）**

   Adobe Campaignは、次の管理対象サービスとして展開できます。adobe campaignインターフェイス、実行管理エンジン、および顧客のキャンペーンデータベースを含むすべてのコンポーネントは、電子メールの実行、ミラーページ、トラッキングサーバー、および登録解除ページ/環境設定センターやランディングページなどの外部対応のWebコンポーネントを含め、Adobeによって完全にホストされます。 Adobeは、クラウド内で最大3つのインスタンス（開発、テスト/ステージ、実稼動）を割り当てます。 このホスティングモデルのインストールと設定の手順は、こ [の節で説明します](../../installation/using/hosted-model.md)。

   ![](assets/deployment_hosted.png)

* **オンプレミス**

   Adobe Campaignはオンプレミスでデプロイできます。ユーザー・インターフェース、実行管理エンジン、データベースを含むAdobe Campaignのすべてのコンポーネントは、お客様のデータ・センター内のオンサイトに存在します。 この導入モデルでは、お客様はすべてのソフトウェアおよびハードウェアの更新とアップグレードを管理し、キャンペーンインスタンスの管理を確実に行うために、保守と最適化のタスクを専任のデータベース管理者が実行する必要があります。 オンプレミスのお客様向けの導入ガイドラインは、この節 [で説明します](../../installation/using/before-starting.md)。

   ![](assets/deployment_onpremise.png)

* **ハイブリッド**

   ハイブリッドモデルとして展開する場合、Adobe Campaignソリューションソフトウェアはお客様のサイトにオンプレミスで常駐し、実行管理はクラウドサービスとしてAdobeによって提供されます。 Adobe Campaignマーケティングインスタンスは、顧客のファイアウォール内にインストールされるので、個人情報(PII)は社内に残り、電子メールのパーソナライズに必要なデータのみがCloudに送信され、電子メールを実行します。 クラウドでホストされる実行インスタンスは、電子メールを配信するためのオンプレミスインスタンスからの要求を受け取ります。 このインスタンスは、すべての電子メールをパーソナライズし、配信します。 どのような種類のデータも、クラウドに永久的に保存されません。 このホスティングモデルのインストールと設定の手順は、こ [の節で説明します](../../installation/using/hybrid-model.md)。

   ![](assets/deployment_hybrid.png)

