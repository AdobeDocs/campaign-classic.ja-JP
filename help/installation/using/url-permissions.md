---
product: campaign
title: URL権限の設定
description: URL権限の設定方法について説明します
feature: Installation, Instance Settings, Permissions
badge-v7-prem: label="オンプレミス／ハイブリッドのみ" type="Caution" url="https://experienceleague.adobe.com/docs/campaign-classic/using/installing-campaign-classic/architecture-and-hosting-models/hosting-models-lp/hosting-models.html?lang=ja" tooltip="オンプレミスデプロイメントとハイブリッドデプロイメントにのみ適用されます"
audience: installation
content-type: reference
topic-tags: additional-configurations
exl-id: 6fe8da3b-57b9-4a69-8602-a03993630b27
source-git-commit: 14ba450ebff9bba6a36c0df07d715b7279604222
workflow-type: tm+mt
source-wordcount: '380'
ht-degree: 35%

---

# URL権限の設定（オンプレミス）{#url-permissions}



JavaScript コードで呼び出すことができるURLのデフォルトリスト（ワークフローなど） Campaign Classicインスタンス数は限られています。 リストに記載されている URL を使用すれば、インスタンスは正常に機能します。

デフォルトでは、インスタンスは外部の URL にアクセスできないようになっています。 ただし、一部の外部URLを承認済みURLのリストに追加して、インスタンスがそれらのURLに接続できるようにすることは可能です。 これにより、Campaign インスタンスを SFTP サーバーや web サイトなどの外部システムと接続して、ファイルやデータの転送が可能になります。

>[!NOTE]
>
>この手順は、**オンプレミス**&#x200B;のデプロイメントに制限されています。
>
>**ホスト**&#x200B;のお客様は、[Campaign Campaign コントロールパネル](https://experienceleague.adobe.com/docs/control-panel/using/control-panel-home.html?lang=ja)にアクセスできる場合、URL権限のセルフサービスインターフェイスを使用できます。 [詳細情報](https://experienceleague.adobe.com/docs/control-panel/using/instances-settings/url-permissions.html?lang=ja)
>
>その他の&#x200B;**ハイブリッド/ホスト**&#x200B;のお客様は、Adobe サポートチームに連絡してIPを契約許可リストに追加する必要があります。
>

**ハイブリッド**&#x200B;および&#x200B;**オンプレミス**&#x200B;のデプロイメントの場合、管理者は&#x200B;**serverConf.xml** ファイルで新しい&#x200B;**urlPermission**&#x200B;を参照する必要があります。


3つの接続保護モードを使用できます。

* **ブロッキング**:「」許可リストに属しないすべてのURLがブロックされ、エラーメッセージが表示されます。 これは、ポストアップグレード後のデフォルトのモードです。
* **Permissive**: 許可リストに属しないすべてのURLが許可されます。
* **Warning**: 許可リストに属しないすべてのURLは許可されますが、JS インタプリタは警告を発するため、管理者は警告を収集できます。 このモードでは JST-310027 警告メッセージが追加されます。

```
<urlPermission action="warn" debugTrace="true">
  <url dnsSuffix="abc.company1.com" urlRegEx=".*" />
  <url dnsSuffix="def.partnerA_company1.com" urlRegEx=".*" />
  <url dnsSuffix="xyz.partnerB_company1.com" urlRegEx=".*" />
</urlPermission>
```

>[!IMPORTANT]
>
>デフォルトでは、新しい実装では&#x200B;**ブロッキング** モードが使用されます。
>
>移行からの既存のお客様は、**警告** モードを一時的に使用できます。 URLを許可する前に、アウトバウンドトラフィックを分析します。 許可されたURLのリストを定義したら、URLを許可リストに追加し、**ブロッキング** モードを有効にできます。

詳しくは、次の節を参照してください。

* [Campaign コントロールパネルドキュメント](https://experienceleague.adobe.com/docs/control-panel/using/control-panel-home.html?lang=ja)
* [ホスティングモデル](hosting-models.md)
* [Campaign サーバーの設定](configuring-campaign-server.md)
* [Campaign サーバー設定ファイルのパラメーター](the-server-configuration-file.md)
* [セキュリティとプライバシーの評価](get-started-security-privacy.md)
