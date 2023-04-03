---
product: campaign
title: テクニカルノート — Campaign 環境でのMicrosoft Edge Chromium の有効化
description: キャンペーン — Edge Chromium
hide: true
hidefromtoc: true
source-git-commit: d883db444ef7cc243241833b86e8b946454e5d2a
workflow-type: tm+mt
source-wordcount: '228'
ht-degree: 16%

---


# お使いの環境でMicrosoft Edge Chromium を有効にする方法 {#edge-conf}

![](../../assets/v7-only.svg)


## 変更点

Microsoft Internet Explorer 11 の提供終了後、クライアントコンソールのHTMLのダッシュボードレンダリングエンジンは、Campaign Classicv7.3 以降の Edge Chromium を使用します。

Microsoft Edge Webview 2 ランタイムのインストールに加えて、次の URL が [クライアントコンソールのインストールに必要](../../installation/using/installing-the-client-console.md#webview)の場合、Microsoft Edge Chromium をインスタンスで有効にする必要があります。

## 影響の有無

環境がCampaign Classicv7.3（またはそれ以降）にアップグレードされている場合は、影響を受けます。

## 更新方法

* As a **ホスト** のお客様。Adobeは、インスタンスで既にMicrosoft Edge Chromium を有効にしています。 追加のアクションは必要ありません。

* As a **オンプレミス/ハイブリッド** をご使用の場合は、インスタンスでMicrosoft Edge Chromium を有効にする必要があります。

   Campaign Classicv7.3（以降）にアップグレードする場合、 `webView2Mode` 属性は、Campaign サーバーの設定ファイルで使用できます。 `serverConf.xml`. この属性を有効にする必要があります。

   これを実行するには、すべての環境 (MKT、MID、RT) に次の手順を適用します。

   1. Campaign サーバー設定ファイル (`serverConf.xml`)
   1. 内 `<web>` モジュール、設定 `webView2Mode = "1"`
   1. サーバー設定を再読み込みします

      ```
      nlserver config -reload
      ```

   1. Web サーバーの再起動

      ```
      nlserver restart web
      ```

   1. 環境が Apache 上で動作している場合は、Apache を再起動します。

      ```
      /etc/init.d/apache2 restart
      ```


>[!NOTE]
>
>これらの変更点に関するご質問については、[アドビカスタマーケア](https://helpx.adobe.com/jp/enterprise/admin-guide.html/enterprise/using/support-for-experience-cloud.ug.html)にお問い合わせください。

## 関連トピック

* [環境のアップグレード](../../production/using/build-upgrade.md)
* [ビルドのアップグレードに関する FAQ](../../platform/using/faq-build-upgrade.md)
* [Campaign クライアントコンソールのインストール](../../installation/using/installing-the-client-console.md)

