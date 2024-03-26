---
product: campaign
title: URL へのアクセス権限の設定
description: URL へのアクセス権限の設定方法を説明します
feature: Installation, Instance Settings, Permissions
badge-v7-only: label="v7" type="Informative" tooltip="Campaign Classic v7 にのみ適用されます"
badge-v7-prem: label="オンプレミスおよびハイブリッド" type="Caution" url="https://experienceleague.adobe.com/docs/campaign-classic/using/installing-campaign-classic/architecture-and-hosting-models/hosting-models-lp/hosting-models.html?lang=ja" tooltip="オンプレミスデプロイメントとハイブリッドデプロイメントにのみ適用されます"
audience: installation
content-type: reference
topic-tags: additional-configurations
exl-id: 6fe8da3b-57b9-4a69-8602-a03993630b27
source-git-commit: 3a9b21d626b60754789c3f594ba798309f62a553
workflow-type: tm+mt
source-wordcount: '339'
ht-degree: 35%

---

# URL へのアクセス権限の設定（オンプレミス）{#url-permissions}



Campaign Classic インスタンスの JavaScript コード（ワークフローなど）で呼び出すことができる URL のデフォルトリストは、制限されています。リストに記載されている URL を使用すれば、インスタンスは正常に機能します。

デフォルトでは、インスタンスは外部の URL にアクセスできないようになっています。ただし、外部の URL を承認済み URL リストに追加して、インスタンスがアクセスできるようにすることは可能です。 これにより、Campaign インスタンスを SFTP サーバーや web サイトなどの外部システムと接続して、ファイルやデータの転送が可能になります。

>[!NOTE]
>
>この手順は次に制限されています： **オンプレミス** デプロイメント。
>
>As a **ホスト** 顧客、アクセス可能な場合 [キャンペーンCampaign コントロールパネル](https://experienceleague.adobe.com/docs/control-panel/using/control-panel-home.html?lang=ja)に設定されている場合は、URL 権限セルフサービスインターフェイスを使用できます。 [詳細情報](https://experienceleague.adobe.com/docs/control-panel/using/instances-settings/url-permissions.html?lang=ja)
>
>その他 **ハイブリッド/ホスト** のお客様は、Adobeサポートチームに連絡して、IP をチームに追加する必要があり許可リストに加えるます。
>

の場合 **ハイブリッド** および **オンプレミス** デプロイメントを使用する場合、管理者は新しい **urlPermission** （内） **serverConf.xml** ファイル。


次の 3 つの接続保護モードを使用できます。

* **ブロック**：特定のに属さないすべての URL がブ許可リストに加えるロックされ、エラーメッセージが表示されます。 これは、ポストアップグレード後のデフォルトのモードです。
* **許容**：特定の URL に属さないすべての URL を許許可リストに加える可します。
* **警告**：このに属さない URL をすべて許可しま許可リストに加えるすが、JS インタープリターが警告を表示するので、管理者がそれらを収集できます。 このモードでは JST-310027 警告メッセージが追加されます。

```
<urlPermission action="warn" debugTrace="true">
  <url dnsSuffix="abc.company1.com" urlRegEx=".*" />
  <url dnsSuffix="def.partnerA_company1.com" urlRegEx=".*" />
  <url dnsSuffix="xyz.partnerB_company1.com" urlRegEx=".*" />
</urlPermission>
```

>[!IMPORTANT]
>
>デフォルトでは、新しい実装では、 **ブロック** モード。
>
>移行による既存のお客様は、一時的に **警告** モード。 URL を許可する前にアウトバウンドトラフィックを分析します。 許可された URL のリストを定義したら、URL をリストに追加して、次の URL をアク許可リストに加えるティブ化できます。 **ブロック** モード。

詳しくは、次の節を参照してください。

* [コントロールパネルに関するドキュメント](https://experienceleague.adobe.com/docs/control-panel/using/control-panel-home.html?lang=ja)
* [ホスティングのモデル](hosting-models.md)
* [Campaign サーバーの設定](configuring-campaign-server.md)
* [Campaign サーバー設定ファイルのパラメーター](the-server-configuration-file.md)
* [セキュリティおよびプライバシーチェックリスト](get-started-security-privacy.md)
