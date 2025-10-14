---
product: campaign
title: Windows での Campaign インストールの前提条件
description: Windows での Campaign インストールの前提条件
feature: Installation, Instance Settings
badge-v7-prem: label="オンプレミス／ハイブリッドのみ" type="Caution" url="https://experienceleague.adobe.com/docs/campaign-classic/using/installing-campaign-classic/architecture-and-hosting-models/hosting-models-lp/hosting-models.html?lang=ja" tooltip="オンプレミスデプロイメントとハイブリッドデプロイメントにのみ適用されます"
audience: installation
content-type: reference
topic-tags: installing-campaign-in-windows-
exl-id: a7cf59cc-9260-4109-af4c-b2e2a9c999da
source-git-commit: 14ba450ebff9bba6a36c0df07d715b7279604222
workflow-type: tm+mt
source-wordcount: '153'
ht-degree: 7%

---

# Windows への Campaign のインストールの基本を学ぶ {#prerequisites-of-campaign-installation-in-windows}



Adobe Campaignのインストールに必要な技術的な設定とソフトウェアについては、[&#x200B; 互換性マトリックス &#x200B;](../../rn/using/compatibility-matrix.md) を参照してください。

マルチインスタンス使用のためのAdobe Campaign サーバーのインストールプロセスについては、以下の [&#x200B; サーバーのインストール &#x200B;](../../installation/using/installing-the-server.md) を参照してください。

主な手順は次のとおりです。

1. アプリケーションサーバーのインストールについては、[&#x200B; インストールプログラムの実行 &#x200B;](../../installation/using/installing-the-server.md#executing-the-installation-program) を参照してください。
1. Web サーバーとの統合（オプション。デプロイされているコンポーネントによって異なります）については、[IIS Web サーバーの設定 &#x200B;](../../installation/using/integration-into-a-web-server-for-windows.md#configuring-the-iis-web-server) を参照してください。

インストール手順が完了したら、インスタンス、データベース、サーバーを設定する必要があります。 詳しくは、[&#x200B; 初期設定について &#x200B;](../../installation/using/about-initial-configuration.md) を参照してください。

>[!NOTE]
>
>Adobe Campaignを Windows 環境にデプロイする場合、必要なアクセス権を持つユーザーは、ネットワーク上でファイルを操作する際にアクセスパスに UNC 構文（Universal.Uniform Naming Convention）を使用できます。
