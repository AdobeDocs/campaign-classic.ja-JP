---
product: campaign
title: 設定の原則
description: 設定の原則
feature: Monitoring, Configuration
badge-v7-prem: label="オンプレミスおよびハイブリッド" type="Caution" url="https://experienceleague.adobe.com/docs/campaign-classic/using/installing-campaign-classic/architecture-and-hosting-models/hosting-models-lp/hosting-models.html?lang=ja" tooltip="オンプレミスデプロイメントとハイブリッドデプロイメントにのみ適用されます"
audience: production
content-type: reference
topic-tags: production-procedures
exl-id: 03d7e579-8678-44b8-bbe7-cf4204bffb25
source-git-commit: b666535f7f82d1b8c2da4fbce1bc25cf8d39d187
workflow-type: tm+mt
source-wordcount: '291'
ht-degree: 8%

---

# 設定の原則{#configuration-principle}



Adobe Campaign プラットフォームは、インスタンスの概念に基づいています。これは、Apache が使用するバーチャルホストと同様です。 この操作モードでは、複数のインスタンスをサーバーに割り当てることで、サーバーを共有できます。 インスタンスは互いに完全に独立しており、独自のデータベースおよび設定ファイルで動作します。

特定のサーバーには、すべてのAdobe Campaign インスタンスに共通の要素が 2 つあります。

* この **内部** パスワード：これは一般管理者のパスワードです。 これは、特定のアプリケーションサーバーのすべてのインスタンスに共通です。

  >[!IMPORTANT]
  >
  >を使用してログオンするには **内部** 識別子。事前にパスワードを定義しておく必要があります。 詳しくは、[この節](../../installation/using/configuring-campaign-server.md#internal-identifier)を参照してください。

* 複数のテクニカルサーバー設定：これらの設定はすべて、インスタンスの特定の設定でオーバーロードできます。

設定ファイルはに保存されます。 **conf** インストールディレクトリのディレクトリ。 設定は次の 3 つのファイルに分類されます。

* **serverConf.xml**：すべてのインスタンスの全体的な設定。
* **config-**`<instance>`**.xml** （ここで、 **`<instance>`** はインスタンス名）：インスタンス固有の設定です。
* **serverConf.xml.diff**：初期設定と現在の設定の差分。 このファイルはアプリケーションによって自動的に生成されるので、手動で変更しないでください。 ビルドバージョンの更新時にユーザーの変更を自動的に反映するために使用されます。

インスタンス設定は、次のように読み込まれます。

* モジュールは、 **serverConf.xml** すべてのインスタンスで共有されるパラメーターを取得するファイルです。
* その後、が読み込まれます。 **config-**`<instance>`**.xml** ファイル。 このファイルにある値は、に含まれる値よりも優先されます。 **serverConf.xml**.

  これら 2 つのファイルの形式は同じです。 内の任意の値 **serverConf.xml** は、特定のインスタンスの場合にオーバーロードできます。 **config-`<instance>`.xml** ファイル。

この動作モードは、設定に優れた柔軟性を提供します。
