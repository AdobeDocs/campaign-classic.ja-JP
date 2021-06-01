---
product: campaign
title: URLへのアクセス権限の設定
description: URLへのアクセス権限の設定方法を説明します
audience: installation
content-type: reference
topic-tags: additional-configurations
exl-id: 67dda58f-97d1-4df5-9648-5f8a1453b814,6fe8da3b-57b9-4a69-8602-a03993630b27
source-git-commit: 98d646919fedc66ee9145522ad0c5f15b25dbf2e
workflow-type: tm+mt
source-wordcount: '338'
ht-degree: 36%

---

# URLへのアクセス権限の設定（オンプレミス）{#url-permissions}

Campaign Classic インスタンスの JavaScript コード（ワークフローなど）で呼び出すことができる URL のデフォルトリストは、制限されています。リストに記載されている URL を使用すれば、インスタンスは正常に機能します。

デフォルトでは、インスタンスは外部の URL にアクセスできないようになっています。ただし、外部のURLを承認済みURLリストに追加して、インスタンスからアクセスできるようにすることもできます。 これにより、Campaign インスタンスを SFTP サーバーや Web サイトなどの外部システムと接続して、ファイルやデータの転送が可能になります。

>[!NOTE]
>
>この手順は、**オンプレミス**&#x200B;デプロイメントに制限されます。
>
>**ホスト**&#x200B;のお客様は、[CampaignCampaign コントロールパネル](https://experienceleague.adobe.com/docs/control-panel/using/control-panel-home.html?lang=ja)にアクセスできる場合、URL権限セルフサービスインターフェイスを使用できます。 [詳細情報](https://experienceleague.adobe.com/docs/control-panel/using/instances-settings/url-permissions.html?lang=ja)
>
>その他の&#x200B;**ハイブリッド/ホスト型**&#x200B;のお客様は、Adobeサポートチームに連絡して、許可リストにIPを追加する必要があります。


**ハイブリッド**&#x200B;と&#x200B;**オンプレミス**&#x200B;のデプロイメントの場合、管理者は、**serverConf.xml**&#x200B;ファイルで新しい&#x200B;**urlPermission**&#x200B;を参照する必要があります。


次の3つの接続保護モードを使用できます。

* **ブロック**:そのユーザーに属さないURLはすべて許可リストブロックされ、エラーメッセージが表示されます。これは、ポストアップグレード後のデフォルトのモードです。
* **許可**:そのユーザーに属さないURLをす許可リストべて許可します。
* **警告**:このに属さないURLはすべて許可されます許可リストが、JSインタープリターが警告を表示するので、管理者はこの警告を収集できます。このモードでは JST-310027 警告メッセージが追加されます。

```
<urlPermission action="warn" debugTrace="true">
  <url dnsSuffix="abc.company1.com" urlRegEx=".*" />
  <url dnsSuffix="def.partnerA_company1.com" urlRegEx=".*" />
  <url dnsSuffix="xyz.partnerB_company1.com" urlRegEx=".*" />
</urlPermission>
```

>[!IMPORTANT]
>
>デフォルトでは、新しい実装では&#x200B;**ブロック**&#x200B;モードが使用されます。
>
>移行を行う既存のお客様は、一時的に&#x200B;**警告**&#x200B;モードを使用できます。 URLを許可する前にアウトバウンドトラフィックを分析します。 許可されたURLのリストを定義したら、URLをに追加許可リストし、**ブロック**&#x200B;モードを有効にします。

詳しくは、次の節を参照してください。

* [コントロールパネルのドキュメント](https://experienceleague.adobe.com/docs/control-panel/using/control-panel-home.html)
* [ホスティングモデル](hosting-models.md)
* [Campaign サーバーの設定](configuring-campaign-server.md)
* [Campaignサーバー設定ファイルのパラメーター](the-server-configuration-file.md)
* [セキュリティ／プライバシーチェックリスト](get-started-security-privacy.md)
