---
product: campaign
title: Windows での Campaign のインストールの前提条件
description: Windows での Campaign のインストールの前提条件
feature: Installation, Instance Settings
badge-v7-only: label="v7" type="Informative" tooltip="Campaign Classic v7 にのみ適用されます"
badge-v7-prem: label="オンプレミスおよびハイブリッド" type="Caution" url="https://experienceleague.adobe.com/docs/campaign-classic/using/installing-campaign-classic/architecture-and-hosting-models/hosting-models-lp/hosting-models.html?lang=ja" tooltip="オンプレミスデプロイメントとハイブリッドデプロイメントにのみ適用されます"
audience: installation
content-type: reference
topic-tags: installing-campaign-in-windows-
exl-id: a7cf59cc-9260-4109-af4c-b2e2a9c999da
source-git-commit: 3a9b21d626b60754789c3f594ba798309f62a553
workflow-type: tm+mt
source-wordcount: '167'
ht-degree: 20%

---

# Windows への Campaign のインストールの基本を学ぶ {#prerequisites-of-campaign-installation-in-windows}



Adobe Campaignのインストールに必要な技術的な設定とソフトウェアについては、 [互換性マトリックス](../../rn/using/compatibility-matrix.md).

マルチインスタンスを使用するためのAdobe Campaignサーバーのインストールプロセスについては、以下で説明します。 [サーバーのインストール](../../installation/using/installing-the-server.md).

主な手順は次のとおりです。

1. アプリケーションサーバーをインストールします。を参照してください。 [インストールプログラムの実行](../../installation/using/installing-the-server.md#executing-the-installation-program).
1. Web サーバーとの統合（デプロイされたコンポーネントに応じてオプション）。を参照してください。 [IIS Web サーバーの設定](../../installation/using/integration-into-a-web-server-for-windows.md#configuring-the-iis-web-server).

インストール手順が完了したら、インスタンス、データベース、サーバーを設定する必要があります。 詳しくは、 [初期設定について](../../installation/using/about-initial-configuration.md).

>[!NOTE]
>
>Adobe Campaignを Windows 環境に展開すると、必要なアクセス権を持つユーザーは、ネットワーク上でのファイル操作中に UNC 構文 (Universal.Uniform Naming Convention) を使用してアクセスパスを指定できます。
