---
product: campaign
title: テクニカルノート — IMS を使用してAdobe Campaignに接続する環境の更新
description: Campaign - IMS の更新
exl-id: ecb5a258-a150-46a3-8b83-2b2c06d873ee
source-git-commit: 0c97efef21bfd3b8671847c3e1c27bb76cf167e4
workflow-type: tm+mt
source-wordcount: '591'
ht-degree: 84%

---

# IMS を使用して Adobe Campaign に接続するように環境を更新する方法 {#acc-ims-faq}

![](../../assets/v7-only.svg)

2021 年 6 月 30 日に、[AdobeIdentity Managementシステム ](https://helpx.adobe.com/jp/enterprise/using/identity.html)(IMS) のログイン機能が変更され、Adobe Campaignの引き続き使用する際に影響を及ぼす可能性がありました。 Adobe Campaign Classic v7 を中断することなく引き続き使用できるようにする方法を説明します。

## 変更点

AdobeIdentity Managementサービス (IMS) は、2021 年 6 月 30 日に、古いバージョンの Internet Explorer のサポートを停止しました。****[詳細情報](https://helpx.adobe.com/jp/x-productkb/global/update-operating-system-and-browser.html)。

アドビは、2021 年 6 月 30 日（PT）以降も、すべてのお客様に対して引き続き IMS 機能を提供したいと考えています。IMS はセキュリティフレームワークの一部で、ユーザーがクライアントコンソール、したがって Adobe Campaign にログインできるようにするものです。

この機能を維持するには、各ユーザーのマシン上でクライアントコンソールを更新し、**Internet Explorer 11** が組み込まれた最新の [Windows バージョン](../../rn/using/compatibility-matrix.md#ClientConsoleoperatingsystems)を各ユーザーのマシンに確実にインストールする必要があります。

## 影響の有無

Adobe Identity Management Service（IMS）を通じて [Adobe ID で](../../integrations/using/about-adobe-id.md) Campaign に接続しており、下記に示すバージョンより古いバージョンの Campaign を使用している場合は、影響を受けます。

既にアップグレード済みで、古いバージョンの Microsoft Internet Explorer を使用している場合は、Internet Explorer 11 にアップグレードする必要があります。

## 更新方法

* ホステッド環境のお客様の場合は、インスタンスが既に新しいバージョンにアップグレードされています。

* オンプレミス／ハイブリッド環境のお客様の場合は、新しいクライアントコンソールを活用し、シームレスな移行を確実に実施するには、**2021 年 6 月 30 日（PT）までに**&#x200B;上記の新しいバージョンのいずれかにアップグレードする必要があります。

   以下に示す新しいバージョンの 1 つにアップグレードする必要があります。

   * Gold Standard 11。 [詳細情報](../../rn/using/gold-standard.md)
   * Campaign 21.1.3 リリース。 [詳細情報](../../rn/using/latest-release.md)
   * Campaign 20.2.5 リリース。 [詳細情報](../../rn/using/release--20-2.md)
   * Campaign 20.1.4 リリース。 [詳細情報](../../rn/using/release--20-1.md)
   * Campaign 19.2.4 リリース。 [詳細情報](../../rn/using/release--19-2.md)
   * Campaign 19.1.8 リリース。 [詳細情報](../../rn/using/release--19-1.md)

   これらのリリースには、新しい接続プロトコルが付属しています。 Campaign サーバーとクライアントコンソールの両方をアップグレードする必要があります。すべてのインスタンスをアップグレードしたら、**2021 年 6 月 30 日（PT）**&#x200B;以降も Campaign に接続できるようにするには、クライアントコンソールもこのバージョンにアップグレードする必要があります。

さらに、**Internet Explorer 11** が組み込まれた最新の [Windows バージョン](../../rn/using/compatibility-matrix.md#ClientConsoleoperatingsystems)が各ユーザーのマシンにインストールされていることを確認してください。

## FAQ

**Campaign のバージョンを確認するにはどうすればよいですか？**

バージョンを確認する方法については、](../../platform/using/launching-adobe-campaign.md#getting-your-campaign-version)この節[を参照してください。


**IMS を使用しているかどうかを確認するにはどうすればよいですか？**

接続モードを確認するには、次の操作を行います。

* Campaign クライアントコンソールを起動し、インスタンス接続設定にアクセスします。「**Adobe ID で接続**」オプションが選択されている場合は、Adobe IMS を使用しています。

   ![](../../integrations/using/assets/ims_1.png)

または

* Campaign クライアントコンソールを起動し、接続ウィンドウを確認します。Adobe ID と接続している場合は、下の画面に示すように、IMS を使用しています。

   ![](../../integrations/using/assets/adobeID.png)

**接続警告メッセージ**

クライアントコンソールを更新する必要がある場合や、古いバージョンの Microsoft Internet Explorer を使用している場合は、次のような警告メッセージが表示されます。**Windows や Adobe アプリの最新アップデートをインストールする必要があります。**

![](../../integrations/using/assets/do-not-localize/errorMsg.png)

このような警告が表示された場合は、使用しているオペレーティングシステムの最新のアップデートをインストールしてください。 [詳細情報](https://helpx.adobe.com/x-productkb/global/update-operating-system-and-browser.html)

Internet Explorer のバージョンを更新しなかった場合は、次のメッセージが表示され、Adobe Campaignに接続できなくなります。

![](../../integrations/using/assets/do-not-localize/errorUpdateReq.png)

>[!NOTE]
>
>これらの変更点に関するご質問については、[アドビカスタマーケア](https://helpx.adobe.com/jp/enterprise/admin-guide.html/enterprise/using/support-for-experience-cloud.ug.html)にお問い合わせください。

## 参考になるリンク

* [環境のアップグレード](../../production/using/build-upgrade.md)
* [ビルドのアップグレードに関する FAQ](../../platform/using/faq-build-upgrade.md)
* [ユーザーへの新しいクライアントコンソールの公開](../../installation/using/client-console-availability-for-windows.md)
* [Campaign クライアントコンソールのインストール](../../installation/using/installing-the-client-console.md)
* [Adobe ソフトウェア配布へのアクセス](https://experienceleague.adobe.com/docs/experience-cloud/software-distribution/home.html?lang=ja)
* [Campaign Classic ビルドのダウンロード](https://experience.adobe.com/#/downloads/content/software-distribution/ja/campaign.html)
