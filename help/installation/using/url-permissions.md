---
product: campaign
title: URL へのアクセス権限の設定
description: URL へのアクセス権限の設定方法を説明します
audience: installation
content-type: reference
topic-tags: additional-configurations
source-git-commit: dab18d24f5471034a2169dd674e6f7000de30cac
workflow-type: tm+mt
source-wordcount: '338'
ht-degree: 36%

---

# URL へのアクセス権限の設定（オンプレミス）{#url-permissions}

![](../../assets/v7-only.svg)

Campaign Classic インスタンスの JavaScript コード（ワークフローなど）で呼び出すことができる URL のデフォルトリストは、制限されています。リストに記載されている URL を使用すれば、インスタンスは正常に機能します。

デフォルトでは、インスタンスは外部の URL にアクセスできないようになっています。ただし、外部の URL を承認済み URL リストに追加して、インスタンスからアクセスできるようにすることもできます。 これにより、Campaign インスタンスを SFTP サーバーや web サイトなどの外部システムと接続して、ファイルやデータの転送が可能になります。

>[!NOTE]
>
>この手順は、**オンプレミス** のデプロイメントに制限されます。
>
>**ホスト** のお客様は、[CampaignCampaign コントロールパネル](https://experienceleague.adobe.com/docs/control-panel/using/control-panel-home.html?lang=ja) にアクセスできる場合、URL 権限セルフサービスインターフェイスを使用できます。 [詳細情報](https://experienceleague.adobe.com/docs/control-panel/using/instances-settings/url-permissions.html?lang=ja)
>
>その他の **ハイブリッド/ホスト型** のお客様は、Adobeサポートチームに連絡して、許可リストに IP を追加する必要があります。

**ハイブリッド** および **オンプレミス** のデプロイメントの場合、管理者は、新しい **urlPermission** を **serverConf.xml** ファイルで参照する必要があります。


次の 3 つの接続保護モードを使用できます。

* **ブロック**:該当する URL に属さない URL はすべて許可リストブロックされ、エラーメッセージが表示されます。これは、ポストアップグレード後のデフォルトのモードです。
* **許可**:そのユーザーに属さない URL はす許可リストべて許可されます。
* **警告**:このに属さない URL はすべて許可されます許可リストが、JS インタープリタが警告を表示するので、管理者はこの URL を収集できます。このモードでは JST-310027 警告メッセージが追加されます。

```
<urlPermission action="warn" debugTrace="true">
  <url dnsSuffix="abc.company1.com" urlRegEx=".*" />
  <url dnsSuffix="def.partnerA_company1.com" urlRegEx=".*" />
  <url dnsSuffix="xyz.partnerB_company1.com" urlRegEx=".*" />
</urlPermission>
```

>[!IMPORTANT]
>
>デフォルトでは、新しい実装では **ブロック** モードが使用されます。
>
>移行を行った既存のお客様は、一時的に **警告** モードを使用できます。 URL を許可する前にアウトバウンドトラフィックを分析します。 許可された URL のリストを定義したら、その URL をに追加し許可リストて、**ブロック** モードを有効にします。

詳しくは、次の節を参照してください。

* [コントロールパネルに関するドキュメント](https://experienceleague.adobe.com/docs/control-panel/using/control-panel-home.html)
* [ホスティングモデル](hosting-models.md)
* [Campaign サーバーの設定](configuring-campaign-server.md)
* [Campaign サーバー設定ファイルのパラメーター](the-server-configuration-file.md)
* [セキュリティとプライバシーのチェックリスト](get-started-security-privacy.md)
