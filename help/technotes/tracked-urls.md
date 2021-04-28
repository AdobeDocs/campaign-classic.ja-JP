---
solution: Campaign Classic
product: campaign
title: テクニカルノート
description: テクニカルノート
hide: true
hidefromtoc: true
translation-type: tm+mt
source-git-commit: e1b09767a8eed3a7dc90e4db0429238d86d39570
workflow-type: tm+mt
source-wordcount: '355'
ht-degree: 14%

---

# 追跡されたURLの署名の問題{#tracked-urls}

最近の変更に従って、キャンペーンでURL署名がアクティブな場合、追跡されるURLが失敗する場合があります。 一部の会社は、リンクに影響を与え、URL署名のメカニズムを変更する可能性がある特定のセキュリティツールを備えているので、一部のメールボックスは他のメールボックスよりも影響を受ける可能性があります。

そのため、Adobeでは、リンクの追跡に使用する署名のメカニズムを無効にすることをお勧めします。 この手順では、重複エスケープで受信したもの以外の古いトラッキングリンクを修正します。

購読解除リンクは他のリンクと同様に失敗する可能性があるので、頻度はホスト間で変化しますが、1%未満です。

**影響の有無**

セキュリティを強化するため、電子メールのリンクを追跡するための署名メカニズムは、[キャンペーンゴールド標準8](../rn/using/gold-standard.md#gs8) - 2020年4月に導入され、Build 19.1.4(9032@3a9dc9c)およびキャンペーン20.2を開始するすべてのお客様に対してデフォルトで有効になっています。

環境が次のいずれかのバージョンで実行されている場合は、次の影響を受ける可能性があります。

* ゴールド標準8 ～ 11。 [詳細情報](../rn/using/gold-standard.md#gs-8)
* キャンペーン21.1.1 （ビルド9277）から21.1.2 （ビルド9282）リリースまで [詳細情報](../rn/using/latest-release.md)
* キャンペーン20.3.1 （ビルド9228） ～ 20.3.3 （ビルド9234）リリース。 [詳細情報](../rn/using/release--20-3.md)
* キャンペーン20.2.1 （ビルド9178）から20.2.3 （ビルド9182）リリースまで [詳細情報](../rn/using/release--20-2.md)
* キャンペーン20.1.1 （ビルド9122）から21.1.3 （ビルド9124）リリースまで [詳細情報](../rn/using/release--20-1.md)
* キャンペーン19.2.2 （ビルド9080）から19.2.3 （ビルド9081）リリースまで [詳細情報](../rn/using/release--19-2.md)
* キャンペーン19.1.5 （ビルド9033）から19.1.7 （ビルド9036）リリースまで [詳細情報](../rn/using/release--19-1.md)

バージョンを確認する方法については、](../platform/using/launching-adobe-campaign.md#getting-your-campaign-version)こちらの節[を参照してください。

**更新方法**

**ホストするお客様**&#x200B;として、Adobeは近日中に設定を更新する際にご協力いたします。

**オンプレミス/ハイブリッド顧客**&#x200B;として、設定を更新する必要があります。

次の手順に従います。

1. [サーバー設定ファイル](../installation/using/the-server-configuration-file.md) (serverConf.xml)で、**signEmailLinks**&#x200B;を&#x200B;**false**&#x200B;に変更します。
1. **nlserver** サービスを再起動します。
1. トラッキングサーバーで、Webサーバー（Debianではapache2、CentOS/RedHatではhttpd、WindowsではIIS）を再起動します。

   ```
   nlserver restart web
   ```

>[!NOTE]
>
>**config-`<instance>`.xml**&#x200B;ファイルは、**serverConf.xml**&#x200B;の設定よりも優先されます。 **signEmailLinks**&#x200B;が&#x200B;**config-`<instance>`.xml**&#x200B;に存在する場合（**instance**&#x200B;はインスタンスの名前）、**false**&#x200B;にも変換する必要があります。


**影響は？**

メンテナンスには最大25分のダウンタイムが必要で、この間はすべての配信、トラッキングリンクおよびAPI呼び出しが機能しません。

更新が完了すると、すべてのリンクが期待どおりに動作します。

>[!NOTE]
>
>これらの変更点に関するご質問は、[アドビカスタマーケア](https://helpx.adobe.com/jp/enterprise/admin-guide.html/enterprise/using/support-for-experience-cloud.ug.html)にお問い合わせください。

