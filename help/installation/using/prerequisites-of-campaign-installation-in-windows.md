---
product: campaign
title: Windows での Campaign のインストールの前提条件
description: Windows での Campaign のインストールの前提条件
audience: installation
content-type: reference
topic-tags: installing-campaign-in-windows-
exl-id: a7cf59cc-9260-4109-af4c-b2e2a9c999da
source-git-commit: 20509f44c5b8e0827a09f44dffdf2ec9d11652a1
workflow-type: tm+mt
source-wordcount: '142'
ht-degree: 8%

---

# Windows への Campaign のインストールの概要 {#prerequisites-of-campaign-installation-in-windows}

![](../../assets/v7-only.svg)

Adobe Campaignのインストールに必要な技術的な設定とソフトウェアは、[ 互換性マトリックス ](../../rn/using/compatibility-matrix.md) に記載されています。

複数インスタンスを使用するためのAdobe Campaignサーバーのインストールプロセスについては、[ サーバーのインストール ](../../installation/using/installing-the-server.md) で説明します。

主な手順は次のとおりです。

1. アプリケーションサーバーをインストールします。[ インストールプログラムの実行 ](../../installation/using/installing-the-server.md#executing-the-installation-program) を参照してください。
1. Web サーバーとの統合（デプロイされたコンポーネントに応じてオプション）。[IIS Web サーバーの設定 ](../../installation/using/integration-into-a-web-server-for-windows.md#configuring-the-iis-web-server) を参照してください。

インストール手順が完了したら、インスタンス、データベース、サーバーを設定する必要があります。 詳しくは、[ 初期設定について ](../../installation/using/about-initial-configuration.md) を参照してください。

>[!NOTE]
>
>Adobe Campaignを Windows 環境にデプロイすると、必要なアクセス権を持つユーザーは、ネットワーク上でのファイル操作中に UNC 構文 (Universal.Uniform Naming Convention) を使用してアクセスパスを指定できます。
