---
product: campaign
title: IMSを使用してAdobe Campaignに接続するための環境の更新
description: Campaign - IMSの更新
hide: true
hidefromtoc: true
source-git-commit: 883ac681e0bf0e4ccf916c745924b7340a4d22f9
workflow-type: tm+mt
source-wordcount: '588'
ht-degree: 21%

---

# IMSを使用してAdobe Campaignに接続するための環境の更新方法 {#acc-ims-faq}

2021年6月30日に、Adobe Campaignの引き続き使用に影響を与える可能性のある[AdobeIdentity Managementシステム](https://helpx.adobe.com/jp/enterprise/using/identity.html)(IMS)のログイン機能が変更されます。 中断せずにAdobe Campaign Classic v7を引き続き使用する方法を説明します。

## 何が変わった？

AdobeIdentity Managementサービス(IMS)は、2021年6月30日(PT)以降の古いInternet Explorerバージョンのサポートを停止します。 ****[詳細情報](https://helpx.adobe.com/jp/x-productkb/global/update-operating-system-and-browser.html)。

Adobeは、2021年6月31日を過ぎるすべてのお客様のIMS機能を保持したいと考えています。 IMSは、ユーザーがクライアントコンソール(Adobe Campaign)にログインできるセキュリティフレームワークの一部です。

この機能を維持するには、各ユーザーのマシン上でクライアントコンソールを更新し、**Internet Explorer 11**&#x200B;の組み込みを使用して[Windows版](../rn/using/compatibility-matrix.md#ClientConsoleoperatingsystems)の最新の更新を各ユーザーのマシンにインストールする必要があります。

## 影響の有無

Adobe ID](../integrations/using/about-adobe-id.md)を介してCampaign [にAdobeし、Identity Managementサービス(IMS)を通じて接続し、以下に示すバージョンより古いバージョンのCampaignを実行している場合は、影響を受けます。

既に更新済みで、古いバージョンのMicrosoft Internet Explorerを使用している場合は、Internet Explorer 11にアップグレードする必要があります。

## 更新方法

* ホスト型のお客様は、Adobeで既にインスタンスを新しいバージョンにアップグレードしています。

* オンプレミス/ハイブリッドのお客様は、新しいクライアントコンソールを活用し、2021年6月30日より前にシームレスな移行を確実に&#x200B;**おこなうには、上記の新しいバージョンの1つにアップグレードする必要があります。**

   以下に示す新しいバージョンの 1 つにアップグレードする必要があります。

   * Gold Standard 11。 [詳細情報](../rn/using/gold-standard.md)
   * Campaign 21.1.3 リリース。 [詳細情報](../rn/using/latest-release.md)
   * Campaign 20.2.4 リリース。 [詳細情報](../rn/using/release--20-2.md)
   * Campaign 20.1.4 リリース。 [詳細情報](../rn/using/release--20-1.md)
   * Campaign 19.2.4 リリース。 [詳細情報](../rn/using/release--19-2.md)
   * Campaign 19.1.8 リリース。 [詳細情報](../rn/using/release--19-1.md)

   これらのリリースには、新しい接続プロトコルが付属しています。 アップグレードは、Campaignサーバーとクライアントコンソールの両方に必須です。すべてのインスタンスをアップグレードしたら、**2021年6月30日**&#x200B;以降にCampaignに接続できるように、クライアントコンソールをこのバージョンにアップグレードする必要があります。

さらに、[Windows版](../rn/using/compatibility-matrix.md#ClientConsoleoperatingsystems)の最新の更新（**Internet Explorer 11**&#x200B;組み込み）が各ユーザーのマシンにインストールされていることを確認します。

## よくある質問

**Campaignのバージョンはどうすれば確認できますか？**

バージョンを確認する方法については、](../platform/using/launching-adobe-campaign.md#getting-your-campaign-version)こちらの節[を参照してください。


**IMSを使用しているかどうかを確認するには、どうすればよいですか？**

接続モードを確認するには、次の操作を行います。

* Campaignクライアントコンソールを起動し、インスタンス接続設定にアクセスします。 「**Adobe IDで接続**」オプションが選択されている場合は、AdobeIMSを使用しています。

   ![](../integrations/using/assets/ims_1.png)

または

* Campaignクライアントコンソールを起動し、接続ウィンドウを確認します。 Adobe IDと接続する場合は、次の画面に示すように、IMSを使用しています。

   ![](../integrations/using/assets/adobeID.png)

**接続警告メッセージ**

クライアントコンソールを更新する必要がある場合や、古いバージョンのMicrosoft Internet Explorerを使用する必要がある場合は、次の警告メッセージが表示されます。**WindowsやAdobeアプリに対応した最新のアップデートをインストールする必要があります。**

![](../integrations/using/assets/do-not-localize/errorMsg.png)

このような警告が表示された場合は、使用しているオペレーティングシステムの最新の更新プログラムをインストールしてください。 [詳細情報](https://helpx.adobe.com/x-productkb/global/update-operating-system-and-browser.html)

**2021年6月31日以降**、次のメッセージが表示され、Adobe Campaignに接続できなくなります。

![](../integrations/using/assets/do-not-localize/errorUpdateReq.png)

>[!NOTE]
>
>これらの変更点に関するご質問は、[アドビのサポート](https://helpx.adobe.com/jp/enterprise/admin-guide.html/enterprise/using/support-for-experience-cloud.ug.html?lang=ja)にお問い合わせください。


## 役立つリンク

* [環境のアップグレード](../production/using/build-upgrade.md)
* [ビルドのアップグレードに関する FAQ](../platform/using/faq-build-upgrade.md)
* [ユーザーへの新しいクライアントコンソールの公開](../installation/using/client-console-availability-for-windows.md)
* [Campaign クライアントコンソールのインストール](../installation/using/installing-the-client-console.md)
* [アクセスAdobeソフトウェア配布](https://experienceleague.adobe.com/docs/experience-cloud/software-distribution/home.html?lang=ja)
* [Campaign Classic ビルドのダウンロード](https://experience.adobe.com/#/downloads/content/software-distribution/jp/campaign.html)