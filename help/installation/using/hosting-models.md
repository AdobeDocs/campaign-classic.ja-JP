---
solution: Campaign Classic
product: campaign
title: ホスティングのモデル
description: Discoverキャンペーンのホスティングモデル
audience: installation
content-type: reference
topic-tags: architecture-and-hosting-models
translation-type: tm+mt
source-git-commit: 972885c3a38bcd3a260574bacbb3f507e11ae05b
workflow-type: tm+mt
source-wordcount: '334'
ht-degree: 1%

---


# ホスティングのモデル{#hosting-models}

Adobe Campaignオファーは、3つのホスティングモデルから選択でき、最適なモデル、またはビジネスニーズに合ったモデルを柔軟に選択できます。

>[!NOTE]
>
>Adobeがホストする環境の場合、メインのインストールと設定の手順は、Adobe（サーバーの設定、インスタンス設定ファイルのカスタマイズなど）によってのみ実行できます。 展開モードの主な違いについて詳しくは、[このページ](../../installation/using/capability-matrix.md)を参照してください。

* **Managed Services（ホスト）**

   Adobe Campaignは、次の管理対象サービスとして展開できます。adobe campaignインターフェイス、実行管理エンジン、および顧客のキャンペーンデータベースを含むすべてのコンポーネントは、電子メールの実行、ミラーページ、トラッキングサーバー、および登録解除ページ/環境設定センターやランディングページなどの外部対応のWebコンポーネントを含め、Adobeによって完全にホストされます。 Adobeは、クラウド内で最大3つのインスタンス（開発、テスト/ステージ、実稼動）を割り当てます。 このホスティングモデルのインストールと設定の手順は、このセクション](../../installation/using/hosted-model.md)に[示されます。

   ![](assets/deployment_hosted.png)

* **オンプレミス**

   Adobe Campaignはオンプレミスでデプロイできます。ユーザー・インターフェース、実行管理エンジン、データベースを含むAdobe Campaignのすべてのコンポーネントは、お客様のデータ・センター内のオンサイトに存在します。 この導入モデルでは、お客様はすべてのソフトウェアおよびハードウェアの更新とアップグレードを管理し、キャンペーンインスタンスの管理を確実に行うために、保守と最適化のタスクを専任のデータベース管理者が実行する必要があります。 オンプレミスのお客様向けの導入ガイドラインは、このセクション](../../installation/using/before-starting.md)に[示します。

   ![](assets/deployment_onpremise.png)

* **ハイブリッド**

   ハイブリッドモデルとして展開する場合、Adobe Campaignソリューションソフトウェアはお客様のサイトにオンプレミスで常駐し、実行管理はクラウドサービスとしてAdobeによって提供されます。 Adobe Campaignマーケティングインスタンスは、顧客のファイアウォール内にインストールされるので、個人情報(PII)は社内に残り、電子メールのパーソナライズに必要なデータのみがCloudに送信され、電子メールを実行します。 クラウドでホストされる実行インスタンスは、電子メールを配信するためのオンプレミスインスタンスからの要求を受け取ります。 このインスタンスは、すべての電子メールをパーソナライズし、配信します。 どのような種類のデータも、クラウドに永久的に保存されません。 このホスティングモデルのインストールと設定の手順は、このセクション](../../installation/using/hybrid-model.md)に[示されます。

   ![](assets/deployment_hybrid.png)

