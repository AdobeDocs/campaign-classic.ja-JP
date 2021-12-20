---
product: campaign
title: テクニカルノート
description: テクニカルノート
hide: true
hidefromtoc: true
exl-id: e7d4331b-7149-4768-8e46-2e2911319074
source-git-commit: 70240d5f62fd3d7b755389b5ad8c4b499c94657d
workflow-type: tm+mt
source-wordcount: '355'
ht-degree: 100%

---

# トラッキング対象 URL の署名に関する問題 {#tracked-urls}

![](../../assets/v7-only.svg)

最近の変更に伴い、Campaign で URL 署名がアクティブになっている場合、トラッキングされる URL が失敗することがあります。 一部の会社が使用している特定のセキュリティツールでは、リンクに影響を与え、URL 署名のメカニズムを変更する可能性があるため、一部のメールボックスは他のメールボックスよりも影響を受ける可能性が高くなります。

そのため、リンクのトラッキングに使用する署名のメカニズムを無効にすることをお勧めします。 この手順により、古いトラッキングリンク（重複エスケープで受信したものを除く）が修正されます。

購読解除リンクは他のリンクと同様に失敗する可能性があります。その頻度はホストにより異なりますが、1％未満です。

**影響の有無**

セキュリティを強化するため、電子メールのリンクをトラッキングするための署名メカニズムが [Campaign Gold Standard 8](../../rn/using/gold-standard.md#gs8) - 2020 年 4 月 - に導入され、Build 19.1.4（9032@3a9dc9c）および Campaign 20.2 以降のすべてのお客様に対してデフォルトで有効になっています。

環境が次のいずれかのバージョンで実行されている場合は、影響を受ける可能性があります。

* Gold Standard 8～11。[詳細情報](../../rn/using/gold-standard.md#gs-8)
* Campaign 21.1.1（ビルド 9277）～21.1.2（ビルド 9282）リリース。[詳細情報](../../rn/using/latest-release.md)
* Campaign 20.3.1（ビルド 9228）～20.3.3（ビルド 9234）リリース。[詳細情報](../../rn/using/release--2020.md#release-20-3)
* Campaign 20.2.1（ビルド 9178）～20.2.4（ビルド 9187）リリース。[詳細情報](../../rn/using/release--2020.md#release-20-2)
* Campaign 20.1.1（ビルド 9122）～21.1.3（ビルド 9124）リリース。[詳細情報](../../rn/using/release--2020.md#release-20-1)
* Campaign 19.2.2（ビルド 9080）～19.2.3（ビルド 9081）リリース。[詳細情報](../../rn/using/release--2019.md#release-19-2)
* Campaign 19.1.5（ビルド 9033）～19.1.7（ビルド 9036）リリース。[詳細情報](../../rn/using/release--2019.md#release-19-1)


バージョンを確認する方法については、](../../platform/using/launching-adobe-campaign.md#getting-your-campaign-version)こちらの節[を参照してください。

**更新方法**

**ホステッド環境のお客様**&#x200B;には、近日中に設定の更新にご協力いたします。

**オンプレミス／ハイブリッド環境のお客様**&#x200B;は、設定を更新する必要があります。 

以下の手順に従います。

1. [サーバー設定ファイル](../../installation/using/the-server-configuration-file.md) （serverConf.xml）で、**signEmailLinks** を **false** に変更します。
1. **nlserver** サービスを再起動します。
1. トラッキングサーバーで、Web サーバー（Debian では apache2、CentOS/RedHat では httpd、Windows では IIS）を再起動します。

   ```
   nlserver restart web
   ```

>[!NOTE]
>
>**config-`<instance>`.xml** ファイルは、**serverConf.xml** の設定よりも優先されます。 **signEmailLinks** が **config-`<instance>`.xml** に存在する場合（**instance** はインスタンスの名前）、**false** にする必要があります。

**どのような影響がありますか？**

メンテナンスには最大 25 分のダウンタイムが必要で、この間はすべての配信、トラッキングリンクおよび API 呼び出しが機能しません。

更新が完了すると、すべてのリンクが想定通りに動作します。

>[!NOTE]
>
>これらの変更点に関するご質問は、[アドビのサポート](https://helpx.adobe.com/jp/enterprise/admin-guide.html/enterprise/using/support-for-experience-cloud.ug.html)にお問い合わせください。
