---
product: campaign
title: デプロイメントタイプについて
description: デプロイメントタイプについて
badge-v7-only: label="v7" type="Informative" tooltip="Applies to Campaign Classic v7 only"
audience: installation
content-type: reference
topic-tags: deployment-types-
exl-id: 08628efb-9186-4b67-9431-310d4bc276b4
source-git-commit: 8debcd3d8fb883b3316cf75187a86bebf15a1d31
workflow-type: tm+mt
source-wordcount: '136'
ht-degree: 6%

---

# デプロイメントタイプについて{#about-deployment-types}



Adobe Campaignのモジュラー設計により、スタンドアロンセットアップ（1 台のマシン上のすべてのコンポーネント）から、複数のサーバーを使用した完全に冗長化され分散アーキテクチャを備えた大規模なデプロイメント構成まで、幅広いデプロイメント構成が可能です。 すべては、必要なパフォーマンスとセキュリティのレベルに応じて異なります。

複数のコンピューターで構成する場合は、以下の全体で同じオペレーティングシステムを使用する必要はありません。例えば、Linux 上でリダイレクションサーバーを使用し、Windows 上で配信サーバーと Apache 上でリダイレクションサーバーを使用できます。

>[!NOTE]
>
>主なインストール設定手順は、Adobeがホストするデプロイメントの場合、例えばAdobeとインスタンスの設定ファイルを設定する場合に、サーバーが実行する必要があります。
>
>デプロイメント間の主な違いについて詳しくは、 [ホスティングのモデル](../../installation/using/hosting-models.md) セクションまたは [ホスト型デプロイメントとオンプレミスデプロイメントの機能の違い](../../installation/using/capability-matrix.md).
