---
product: campaign
title: 設定の原則
description: 設定の原則
feature: Monitoring, Configuration
badge-v7-prem: label="オンプレミス／ハイブリッドのみ" type="Caution" url="https://experienceleague.adobe.com/docs/campaign-classic/using/installing-campaign-classic/architecture-and-hosting-models/hosting-models-lp/hosting-models.html?lang=ja" tooltip="オンプレミスデプロイメントとハイブリッドデプロイメントにのみ適用されます"
audience: production
content-type: reference
topic-tags: production-procedures
exl-id: 03d7e579-8678-44b8-bbe7-cf4204bffb25
source-git-commit: 14ba450ebff9bba6a36c0df07d715b7279604222
workflow-type: tm+mt
source-wordcount: '292'
ht-degree: 8%

---

# 設定の原則{#configuration-principle}



Adobe Campaign プラットフォームは、インスタンスの概念に基づいています。これは、Apache が使用するバーチャルホストと同様です。 この操作モードでは、複数のインスタンスをサーバーに割り当てることで、サーバーを共有できます。 インスタンスは互いに完全に独立しており、独自のデータベースおよび設定ファイルで動作します。

特定のサーバーには、すべてのAdobe Campaign インスタンスに共通の要素が 2 つあります。

* **internal** パスワード：これは一般管理者のパスワードです。 これは、特定のアプリケーションサーバーのすべてのインスタンスに共通です。

  >[!IMPORTANT]
  >
  >**内部** 識別子でログオンするには、事前にパスワードを定義しておく必要があります。 詳しくは、[この節](../../installation/using/configuring-campaign-server.md#internal-identifier)を参照してください。

* 複数のテクニカルサーバー設定：これらの設定はすべて、インスタンスの特定の設定でオーバーロードできます。

設定ファイルは、インストールディレクトリの **conf** ディレクトリに保存されます。 設定は次の 3 つのファイルに分類されます。

* **serverConf.xml**：すべてのインスタンスの全体的な設定。
* **config-**`<instance>`**.xml** （**`<instance>`** はインスタンス名）：インスタンスの特定の設定。
* **serverConf.xml.diff**：初期設定と現在の設定の差分。 このファイルはアプリケーションによって自動的に生成されるので、手動で変更しないでください。 ビルドバージョンの更新時にユーザーの変更を自動的に反映するために使用されます。

インスタンス設定は、次のように読み込まれます。

* このモジュールは、**serverConf.xml** ファイルを読み込んで、すべてのインスタンスで共有されるパラメーターを取得します。
* その後、**config-**`<instance>`**.xml** ファイルを読み込みます。 このファイルにある値は、**serverConf.xml** に含まれる値よりも優先されます。

  これら 2 つのファイルの形式は同じです。 **serverConf.xml** 内の任意の値は、**config-`<instance>`.xml** ファイル内の特定のインスタンスに対してオーバーロードできます。

この動作モードは、設定に優れた柔軟性を提供します。
