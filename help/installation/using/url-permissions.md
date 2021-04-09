---
solution: Campaign Classic
product: campaign
title: URL権限の設定
description: URL権限の設定方法を説明します。
audience: installation
content-type: reference
topic-tags: additional-configurations
exl-id: 67dda58f-97d1-4df5-9648-5f8a1453b814,6fe8da3b-57b9-4a69-8602-a03993630b27
translation-type: tm+mt
source-git-commit: 5d8d9e6ba41f94179bbf5f6d41f86267381b9b93
workflow-type: tm+mt
source-wordcount: '338'
ht-degree: 34%

---

# URL権限の設定（オンプレミス）{#url-permissions}

Campaign Classic インスタンスの JavaScript コード（ワークフローなど）で呼び出すことができる URL のデフォルトリストは、制限されています。リストに記載されている URL を使用すれば、インスタンスは正常に機能します。

デフォルトでは、インスタンスは外部の URL にアクセスできないようになっています。ただし、許可されたURLのリストに外部URLを追加して、それらのURLにインスタンスを接続することは可能です。 これにより、Campaign インスタンスを SFTP サーバーや Web サイトなどの外部システムと接続して、ファイルやデータの転送が可能になります。

>[!NOTE]
>
>この手順は、**オンプレミス**&#x200B;のデプロイメントに制限されます。
>
>**ホスト**&#x200B;のお客様は、[キャンペーンCampaign コントロールパネル](https://experienceleague.adobe.com/docs/control-panel/using/control-panel-home.html?lang=ja)にアクセスできる場合、URL権限セルフサービスインターフェイスを使用できます。 [詳細情報](https://experienceleague.adobe.com/docs/control-panel/using/instances-settings/url-permissions.html)
>
>他の&#x200B;**ハイブリッド/ホスト型**&#x200B;お客様は、IPを許可リストに追加するために、Adobeサポートチームに連絡する必要があります。


**ハイブリッド**&#x200B;および&#x200B;**オンプレミス**&#x200B;のデプロイメントの場合、管理者は、新しい&#x200B;**urlPermission**&#x200B;を&#x200B;**serverConf.xml**&#x200B;ファイルで参照する必要があります。


次の3つの接続保護モードを使用できます。

* **ブロック**:許可リストに属していないURLはすべてブロックされ、エラーメッセージが表示されます。これは、ポストアップグレード後のデフォルトのモードです。
* **権限設定**:許可リストに属していないURLはすべて許可されます。
* **警告**:許可リストに属さないURLはすべて許可されますが、JSインタプリタは警告を出すので、管理者がそれらを収集できます。このモードでは JST-310027 警告メッセージが追加されます。

```
<urlPermission action="warn" debugTrace="true">
  <url dnsSuffix="abc.company1.com" urlRegEx=".*" />
  <url dnsSuffix="def.partnerA_company1.com" urlRegEx=".*" />
  <url dnsSuffix="xyz.partnerB_company1.com" urlRegEx=".*" />
</urlPermission>
```

>[!IMPORTANT]
>
>デフォルトでは、新しい実装では&#x200B;**Blocking**&#x200B;モードが使用されます。
>
>移行を行う既存のお客様は、**警告**&#x200B;モードを一時的に使用できます。 URLを許可する前に、アウトバウンドトラフィックを分析します。 許可されたURLのリストを定義したら、URLを許可リストに追加し、**ブロック**&#x200B;モードをアクティブにします。

詳しくは、次の節を参照してください。

* [コントロールパネルのドキュメント](https://experienceleague.adobe.com/docs/control-panel/using/control-panel-home.html)
* [モデルのホスティング](hosting-models.md)
* [Campaign サーバーの設定](configuring-campaign-server.md)
* [キャンペーンサーバー設定ファイルのパラメーター](the-server-configuration-file.md)
* [セキュリティ／プライバシーチェックリスト](get-started-security-privacy.md)
