---
product: campaign
title: テクニカルノート - Campaign 環境での Microsoft Edge Chromium の有効化
description: Campaign - Edge Chromium
feature: Technote, Upgrade
exl-id: 22f4cbaf-ca37-47b9-b7dd-1ee73d5b348d
source-git-commit: 8734e6ef26a7342042a5242d54854b7d3a5e6244
workflow-type: ht
source-wordcount: '263'
ht-degree: 100%

---

# お使いの環境で Microsoft Edge Chromium を有効にする方法 {#edge-conf}

## 変更点

Microsoft Internet Explorer 11 のサポート終了に伴い、クライアントコンソールのダッシュボードの HTML レンダリングエンジンは、Campaign Classic v7.3 から Edge Chromium を使用しています。

[あらゆるクライアントコンソールのインストールに必要](../../installation/using/installing-the-client-console.md#webview)になった Microsoft Edge Webview 2 ランタイムのインストールに加えて、インスタンスで Microsoft Edge Chromium を有効にする必要があります。

>[!NOTE]
>
>Microsoft Edge Chromium を有効にすると、ブラウザーの検索ダイアログボックスを開くための `Ctrl+F`（Windows）または `Command+F`（Mac）のショートカットが機能しなくなります。

## 影響の有無

お使いの環境が Campaign Classic v7.3（以降）にアップグレードされている場合、影響を受けます。

## 更新方法

* **ホステッド**&#x200B;環境のお客様には、アドビはお使いのインスタンスで Microsoft Edge Chromium を既に有効にしています。追加のアクションは不要です。

* **オンプレミス／ハイブリッド**&#x200B;環境のお客様は、お使いのインスタンスで Microsoft Edge Chromium を有効にする必要があります。

  Campaign Classic v7.3（以降）にアップグレードすると、新しい `webView2Mode` 属性が Campaign サーバー設定ファイル `serverConf.xml` で使用可能になります。この属性を有効にする必要があります。

  これを実行するには、すべての環境（MKT、MID、RT）で次の手順を適用します。

   1. Campaign サーバー設定ファイル（`serverConf.xml`）を編集します
   1. `<web>` モジュールで、`webView2Mode = "1"` を設定します
   1. 次のコマンドを実行して、サーバー設定をリロードします。

      ```
      nlserver config -reload
      ```

   1. 次のコマンドを実行して、web サーバーを再起動します。

      ```
      nlserver restart web
      ```

   1. お使いの環境で Apache を web サーバーとして使用している場合は、次のコマンドを実行して Apache を再起動します。

      ```
      /etc/init.d/apache2 restart
      ```


>[!NOTE]
>
>これらの変更点に関するご質問については、[アドビカスタマーケア](https://helpx.adobe.com/jp/enterprise/admin-guide.html/enterprise/using/support-for-experience-cloud.ug.html)にお問い合わせください。
>

## 関連トピック

* [環境のアップグレード](../../production/using/build-upgrade.md)
* [ビルドのアップグレードに関する FAQ](../../platform/using/faq-build-upgrade.md)
* [Campaign クライアントコンソールのインストール](../../installation/using/installing-the-client-console.md)
