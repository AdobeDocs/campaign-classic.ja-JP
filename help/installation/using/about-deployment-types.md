---
product: campaign
title: デプロイメントタイプについて
description: デプロイメントタイプについて
feature: Installation, Architecture
audience: installation
content-type: reference
topic-tags: deployment-types-
exl-id: 08628efb-9186-4b67-9431-310d4bc276b4
TQID: 'https://experienceleague.adobe.com/Xf-z3lKtUNbgrNAh0-3vRasteUegsRDW2cYQ7L9-rok'
product_v2:
  - id: dfc56824-e8b9-499e-85d4-21aedb507314
    internal-label: Campaign
  - id: fd6e6e36-54e4-4f1a-96fc-1a750e400d50
    internal-label: Campaign Classic v7
feature_v2:
  - id: bae31391-3416-5fbd-bc4b-2cdcae2922db
    internal-label: Architecture
  - id: c5474392-5419-4296-9e41-f6f4ce4f6e9b
    internal-label: Administration
subfeature_v2:
  - id: e656c701-3899-4db3-989c-de0980ddfffa
    internal-label: Installation
topic_v2:
  - id: d095671a-1355-40aa-8b5f-06c33c68080b
    internal-label: Security
source-git-commit: a43e591a565a18d79f583d975e3e812c5435b0c0
workflow-type: tm+mt
source-wordcount: '137'
ht-degree: 6%
---
# デプロイメントタイプについて{#about-deployment-types}



Adobe Campaignのモジュラー設計により、スタンドアロンのセットアップ（1台のマシン上のすべてのコンポーネント）から、複数のサーバーを使用する完全冗長かつ分散型のアーキテクチャを備えたエンタープライズ版まで、幅広いデプロイメント構成が可能になります。 これらはすべて、必要なレベルのパフォーマンスとセキュリティによって異なります。

複数のコンピューターで構成する場合、同じオペレーティングシステムを使用する必要はありません。例えば、Linux + Apacheでリダイレクトサーバーを使用し、Windowsで配信サーバーを使用できます。

>[!NOTE]
>
>主なインストール設定手順は、例えばサーバーとインスタンスの設定ファイルを設定するために、Adobeがホストするデプロイメントに対してのみAdobeで実行できます。
>
>デプロイメント間の主な違いについて詳しくは、「[ ホスティングモデル ](../../installation/using/hosting-models.md)」セクションまたは「[ ホスト型とオンプレミス型のデプロイメントの機能の違い](../../installation/using/capability-matrix.md)」を参照してください。
