---
product: campaign
title: 設定の原則
description: 設定の原則
feature: Monitoring, Configuration
badge-v7-only: label="v7" type="Informative" tooltip="Campaign Classicv7 にのみ適用"
badge-v7-prem: label="オンプレミスおよびハイブリッド" type="Caution" url="https://experienceleague.adobe.com/docs/campaign-classic/using/installing-campaign-classic/architecture-and-hosting-models/hosting-models-lp/hosting-models.html?lang=ja" tooltip="オンプレミスデプロイメントとハイブリッドデプロイメントにのみ適用されます"
audience: production
content-type: reference
topic-tags: production-procedures
exl-id: 03d7e579-8678-44b8-bbe7-cf4204bffb25
source-git-commit: 3a9b21d626b60754789c3f594ba798309f62a553
workflow-type: tm+mt
source-wordcount: '306'
ht-degree: 10%

---

# 設定の原則{#configuration-principle}



Adobe Campaignプラットフォームは、Apache が使用する仮想ホストと同様に、インスタンスの概念に基づいています。 この操作モードでは、複数のインスタンスを割り当ててサーバーを共有できます。 インスタンスは完全に別々で、独自のデータベースと設定ファイルを使用して動作します。

特定のサーバーに対して、すべてのAdobe Campaignインスタンスに共通する 2 つの要素があります。

* The **内部** password：一般的な管理者パスワードです。 特定のアプリケーションサーバーのすべてのインスタンスに共通です。

  >[!IMPORTANT]
  >
  >を使用してログオンするには、以下を実行します。 **内部** 識別子の場合は、事前にパスワードを定義しておく必要があります。 詳しくは、[この節](../../installation/using/configuring-campaign-server.md#internal-identifier)を参照してください。

* 複数の技術的なサーバー設定：インスタンスの特定の設定では、すべてオーバーロードできます。

設定ファイルは、 **conf** インストールディレクトリのディレクトリ。 設定は、次の 3 つのファイルに分類されます。

* **serverConf.xml**：すべてのインスタンスの全体的な設定。
* **config-**`<instance>`**.xml** ( ここで **`<instance>`** はインスタンス名です )：インスタンスの特定の設定。
* **serverConf.xml.diff**：初期設定と現在の設定の差分。 このファイルは、アプリケーションによって自動的に生成され、手動で変更しないでください。 ビルドバージョンの更新時に、ユーザーの変更を自動的に反映するために使用されます。

インスタンスの設定は、次のように読み込まれます。

* モジュールは、 **serverConf.xml** ファイルを参照して、すべてのインスタンスで共有されるパラメーターを取得します。
* その後、 **config-**`<instance>`**.xml** ファイル。 このファイルで見つかった値は、 **serverConf.xml**.

  これら 2 つのファイルは同じ形式です。 の任意の値 **serverConf.xml** は、 **config-`<instance>`.xml** ファイル。

この動作モードは、設定を柔軟に行うことができます。
