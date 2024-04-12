---
product: campaign
title: URL 権限の設定
description: URL 権限の設定方法を学ぶ
feature: Installation, Instance Settings, Permissions
badge-v7-prem: label="オンプレミス/ハイブリッドのみ" type="Caution" url="https://experienceleague.adobe.com/docs/campaign-classic/using/installing-campaign-classic/architecture-and-hosting-models/hosting-models-lp/hosting-models.html?lang=ja" tooltip="オンプレミスデプロイメントとハイブリッドデプロイメントにのみ適用されます"
audience: installation
content-type: reference
topic-tags: additional-configurations
exl-id: 6fe8da3b-57b9-4a69-8602-a03993630b27
source-git-commit: 14ba450ebff9bba6a36c0df07d715b7279604222
workflow-type: tm+mt
source-wordcount: '333'
ht-degree: 33%

---

# URL 権限の設定（オンプレミス）{#url-permissions}



Campaign Classic インスタンスの JavaScript コード（ワークフローなど）で呼び出すことができる URL のデフォルトリストは、制限されています。リストに記載されている URL を使用すれば、インスタンスは正常に機能します。

デフォルトでは、インスタンスは外部の URL にアクセスできないようになっています。ただし、一部の外部 URL を承認済み URL のリストに追加して、インスタンスから接続できるようにすることは可能です。 これにより、Campaign インスタンスを SFTP サーバーや web サイトなどの外部システムと接続して、ファイルやデータの転送が可能になります。

>[!NOTE]
>
>この手順は、次の場合に制限されます **オンプレミス** のデプロイメント。
>
>As a **hosted** 顧客（アクセス可能な場合） [キャンペーンCampaign コントロールパネル](https://experienceleague.adobe.com/docs/control-panel/using/control-panel-home.html?lang=ja)URL 権限のセルフサービスインターフェイスを使用できます。 [詳細情報](https://experienceleague.adobe.com/docs/control-panel/using/instances-settings/url-permissions.html?lang=ja)
>
>その他 **ハイブリッド/ホスト** お客様は、Adobe許可リストに加える サポートチームに連絡して、IP をチームに追加する必要があります。
>

の場合 **ハイブリッド** および **オンプレミス** デプロイメントの場合、管理者は新しいを参照する必要があります **urlPermission** が含まれる **serverConf.xml** ファイル。


次の 3 つの接続保護モードを使用できます。

* **ブロック**:許可リストに属さないすべての URL はブロックされ、エラーメッセージが表示されます。 これは、ポストアップグレード後のデフォルトのモードです。
* **許容値**:許可リストに属さないすべての URL が許可されます。
* **警告**&#x200B;許可リストに加える：に属さない URL はすべて許可されますが、JS インタープリターは管理者が収集できるように警告を表示します。 このモードでは JST-310027 警告メッセージが追加されます。

```
<urlPermission action="warn" debugTrace="true">
  <url dnsSuffix="abc.company1.com" urlRegEx=".*" />
  <url dnsSuffix="def.partnerA_company1.com" urlRegEx=".*" />
  <url dnsSuffix="xyz.partnerB_company1.com" urlRegEx=".*" />
</urlPermission>
```

>[!IMPORTANT]
>
>デフォルトでは、新しい実装ではを使用します **ブロック** モード。
>
>既存の移行顧客として、を一時的に使用できます。 **警告** モード。 URL を許可する前に送信トラフィックを分析します。 許可されている URL のリストを定義したら、その URL を許可リストに追加して、 **ブロック** モード。

詳しくは、次の節を参照してください。

* [コントロールパネルに関するドキュメント](https://experienceleague.adobe.com/docs/control-panel/using/control-panel-home.html?lang=ja)
* [ホスティングモデル](hosting-models.md)
* [Campaign サーバーの設定](configuring-campaign-server.md)
* [Campaign サーバー設定ファイルパラメーター](the-server-configuration-file.md)
* [セキュリティとプライバシーのチェックリスト](get-started-security-privacy.md)
