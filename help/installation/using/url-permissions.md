---
product: campaign
title: URL へのアクセス権限の設定
description: URL へのアクセス権限の設定方法を説明します
badge-v7-only: label="v7" type="Informative" tooltip="Applies to Campaign Classic v7 only"
badge-v7-prem: label="on-premise & hybrid" type="Caution" url="https://experienceleague.adobe.com/docs/campaign-classic/using/installing-campaign-classic/architecture-and-hosting-models/hosting-models-lp/hosting-models.html" tooltip="Applies to on-premise and hybrid deployments only"
audience: installation
content-type: reference
topic-tags: additional-configurations
exl-id: 6fe8da3b-57b9-4a69-8602-a03993630b27
source-git-commit: 4661688a22bd1a82eaf9c72a739b5a5ecee168b1
workflow-type: tm+mt
source-wordcount: '337'
ht-degree: 36%

---

# URL へのアクセス権限の設定（オンプレミス）{#url-permissions}



Campaign Classic インスタンスの JavaScript コード（ワークフローなど）で呼び出すことができる URL のデフォルトリストは、制限されています。リストに記載されている URL を使用すれば、インスタンスは正常に機能します。

デフォルトでは、インスタンスは外部の URL にアクセスできないようになっています。ただし、外部の URL を承認済み URL リストに追加して、インスタンスがアクセスできるようにすることは可能です。 これにより、Campaign インスタンスを SFTP サーバーや web サイトなどの外部システムと接続して、ファイルやデータの転送が可能になります。

>[!NOTE]
>
>この手順は次に制限されています： **オンプレミス** デプロイメント。
>
>As a **ホスト** 顧客、 [キャンペーンCampaign コントロールパネル](https://experienceleague.adobe.com/docs/control-panel/using/control-panel-home.html?lang=ja)に設定されている場合は、URL 権限セルフサービスインターフェイスを使用できます。 [詳細情報](https://experienceleague.adobe.com/docs/control-panel/using/instances-settings/url-permissions.html?lang=ja)
>
>その他 **ハイブリッド/ホスト** のお客様は、Adobeサポートチームに連絡して、IP をチームに追加する必要があり許可リストます。

の場合 **ハイブリッド** および **オンプレミス** デプロイメントを使用する場合、管理者は新しい **urlPermission** 内 **serverConf.xml** ファイル。


次の 3 つの接続保護モードを使用できます。

* **ブロック**:そのページに属さないすべての URL がブ許可リストロックされ、エラーメッセージが表示されます。 これは、ポストアップグレード後のデフォルトのモードです。
* **許容**:このタブに属さないすべての URL が許許可リスト可されます。
* **警告**:このに属さない URL はすべて許可されま許可リストすが、JS インタープリタが警告を表示するので、管理者が収集できます。 このモードでは JST-310027 警告メッセージが追加されます。

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
>移行による既存のお客様は、 **警告** モード。 URL を許可する前にアウトバウンドトラフィックを分析します。 許可された URL のリストを定義したら、URL をリストに追加して、次の URL をアク許可リストティブ化できます。 **ブロック** モード。

詳しくは、次の節を参照してください。

* [コントロールパネルに関するドキュメント](https://experienceleague.adobe.com/docs/control-panel/using/control-panel-home.html?lang=ja)
* [ホスティングモデル](hosting-models.md)
* [Campaign サーバーの設定](configuring-campaign-server.md)
* [Campaign サーバー設定ファイルのパラメーター](the-server-configuration-file.md)
* [セキュリティとプライバシーのチェックリスト](get-started-security-privacy.md)
