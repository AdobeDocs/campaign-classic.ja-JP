---
title: WindowsでのCampaignのインストールの前提条件
seo-title: WindowsでのCampaignのインストールの前提条件
description: WindowsでのCampaignのインストールの前提条件
seo-description: null
page-status-flag: never-activated
uuid: 3c030186-d2ab-4845-b5c6-2ed49da00756
contentOwner: sauviat
products: SG_CAMPAIGN/CLASSIC
audience: installation
content-type: reference
topic-tags: installing-campaign-in-windows-
discoiquuid: faaecbd6-f707-4307-8921-04d8993c2c47
index: y
internal: n
snippet: y
translation-type: tm+mt
source-git-commit: 46f5bfb41bfe9c938ac0ffa767ead3e47a32047d

---


# WindowsでのCampaignのインストールの前提条件{#prerequisites-of-campaign-installation-in-windows}

Adobe Campaignのインストールに必要な技術的な設定とソフトウェアは、互換性マトリックスに記載さ [れています](https://helpx.adobe.com/campaign/kb/compatibility-matrix.html)。

マルチインスタンス用のAdobe Campaignサーバーのインストールプロセスについては、「サーバーのインスト [ール」で説明しま](../../installation/using/installing-the-server.md)す。

主な手順は次のとおりです。

1. アプリケーションサーバーをインストールします。詳しくは、イン [ストールプログラムの実行を参照してくださ](../../installation/using/installing-the-server.md#executing-the-installation-program)い。
1. Webサーバーとの統合（デプロイされたコンポーネントに応じてオプション）については、「IIS webサー [バーの設定」を参照してください](../../installation/using/integration-into-a-web-server-for-windows.md#configuring-the-iis-web-server)。

インストール手順が完了したら、インスタンス、データベース、およびサーバーを設定する必要があります。 For more on this, refer to [About initial configuration](../../installation/using/about-initial-configuration.md).

>[!NOTE]
>
>Adobe CampaignをWindows環境に展開すると、必要なアクセス権を持つユーザーは、ネットワーク上でのファイル操作中にアクセスパスにUNC構文(Universal.Uniform Naming Convention)を使用できます。

