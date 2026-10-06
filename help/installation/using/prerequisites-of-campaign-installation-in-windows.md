---
product: campaign
title: WindowsでのCampaign インストールの前提条件
description: WindowsでのCampaign インストールの前提条件
feature: Installation, Instance Settings
badge-v7-prem: label="On-premise/hybrid only" type="Caution" url="https://experienceleague.adobe.com/docs/campaign-classic/using/installing-campaign-classic/architecture-and-hosting-models/hosting-models-lp/hosting-models.html?lang=ja" tooltip="Applies to on-premise and hybrid deployments only"
audience: installation
content-type: reference
topic-tags: installing-campaign-in-windows-
exl-id: a7cf59cc-9260-4109-af4c-b2e2a9c999da
TQID: 'https://experienceleague.adobe.com/vECxz7-bt6DMteRM-N4BtD6Uo5qonHrkgQQeEOkTSt0'
product_v2:
  - id: dfc56824-e8b9-499e-85d4-21aedb507314
    internal-label: Campaign
  - id: fd6e6e36-54e4-4f1a-96fc-1a750e400d50
    internal-label: Campaign Classic v7
feature_v2:
  - id: 7f0a1ee5-eeb8-5478-a9cd-b1896f033118
    internal-label: Instance Settings
  - id: c5474392-5419-4296-9e41-f6f4ce4f6e9b
    internal-label: Administration
subfeature_v2:
  - id: e656c701-3899-4db3-989c-de0980ddfffa
    internal-label: Installation
source-git-commit: a43e591a565a18d79f583d975e3e812c5435b0c0
workflow-type: tm+mt
source-wordcount: '161'
ht-degree: 11%
---
# WindowsでのCampaignのインストールの基本を学ぶ {#prerequisites-of-campaign-installation-in-windows}



Adobe Campaignのインストールに必要な技術的な設定とソフトウェアは、[互換性マトリックス &#x200B;](../../rn/using/compatibility-matrix.md)に記載されています。

マルチインスタンス使用のAdobe Campaign サーバーのインストールプロセスについては、[&#x200B; サーバーのインストール &#x200B;](../../installation/using/installing-the-server.md)を参照してください。

主な手順は次のとおりです。

1. アプリケーションサーバーをインストールします。[&#x200B; インストールプログラムの実行](../../installation/using/installing-the-server.md#executing-the-installation-program)を参照してください。
1. Web サーバーとの統合（デプロイされたコンポーネントに応じてオプション）については、[IIS Web サーバーの設定](../../installation/using/integration-into-a-web-server-for-windows.md#configuring-the-iis-web-server)を参照してください。

インストール手順が完了したら、インスタンス、データベース、サーバーを設定する必要があります。 詳しくは、[初期設定について](../../installation/using/about-initial-configuration.md)を参照してください。

>[!NOTE]
>
>Adobe CampaignをWindows環境にデプロイする場合、必要なアクセス権を持つユーザーは、ネットワーク上のファイル操作中のアクセスパスにUNC構文（Universal.Uniform Naming Convention）を使用できます。
