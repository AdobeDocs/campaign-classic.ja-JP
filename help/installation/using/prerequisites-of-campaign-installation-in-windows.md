---
product: campaign
title: WindowsでのCampaign インストールの前提条件
description: WindowsでのCampaign インストールの前提条件
feature: Installation, Instance Settings
badge-v7-prem: label="オンプレミス／ハイブリッドのみ" type="Caution" url="https://experienceleague.adobe.com/docs/campaign-classic/using/installing-campaign-classic/architecture-and-hosting-models/hosting-models-lp/hosting-models.html?lang=ja" tooltip="オンプレミスデプロイメントとハイブリッドデプロイメントにのみ適用されます"
audience: installation
content-type: reference
topic-tags: installing-campaign-in-windows-
exl-id: a7cf59cc-9260-4109-af4c-b2e2a9c999da
TQID: https://experienceleague.adobe.com/vECxz7-bt6DMteRM-N4BtD6Uo5qonHrkgQQeEOkTSt0
product_v2: id: dfc56824-e8b9-499e-85d4-21aedb507314
feature_v2: []
subfeature_v2: []
source-git-commit: bb41e9407ab5853b0194bb325bbf3f17bc3ea232
workflow-type: tm+mt
source-wordcount: 173
ht-degree: 17%

---

# WindowsでのCampaignのインストールの基本を学ぶ {#prerequisites-of-campaign-installation-in-windows}



Adobe Campaignのインストールに必要な技術的な設定とソフトウェアは、[互換性マトリックス ](../../rn/using/compatibility-matrix.md)に記載されています。

マルチインスタンス使用のAdobe Campaign サーバーのインストールプロセスについては、[ サーバーのインストール ](../../installation/using/installing-the-server.md)を参照してください。

主な手順は次のとおりです。

1. アプリケーションサーバーをインストールします。[ インストールプログラムの実行](../../installation/using/installing-the-server.md#executing-the-installation-program)を参照してください。
1. Web サーバーとの統合（デプロイされたコンポーネントに応じてオプション）については、[IIS Web サーバーの設定](../../installation/using/integration-into-a-web-server-for-windows.md#configuring-the-iis-web-server)を参照してください。

インストール手順が完了したら、インスタンス、データベース、サーバーを設定する必要があります。 詳しくは、[初期設定について](../../installation/using/about-initial-configuration.md)を参照してください。

>[!NOTE]
>
>Adobe CampaignをWindows環境にデプロイする場合、必要なアクセス権を持つユーザーは、ネットワーク上のファイル操作中のアクセスパスにUNC構文（Universal.Uniform Naming Convention）を使用できます。
