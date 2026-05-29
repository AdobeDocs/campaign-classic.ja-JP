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
TQID: https://experienceleague.adobe.com/qh8T4QUwIzRfwYj0j0ZUOJp0V78fiw4ADrSzzMfAsZg
product_v2:
  - id: dfc56824-e8b9-499e-85d4-21aedb507314
feature_v2: []
subfeature_v2:
  - id: c03a11ff-bdf9-4e5b-b279-f468b4293464
  - id: e519a22f-a06a-42fc-9d09-d78a3ab2c434
source-git-commit: 38eab6b8da73163e4476e91c0ef73f25c3f57546
workflow-type: tm+mt
source-wordcount: 311
ht-degree: 14%

---

# 設定の原則{#configuration-principle}



Adobe Campaign プラットフォームは、Apacheで使用されるバーチャルホストと同様に、インスタンスの概念に基づいています。 この操作モードでは、サーバーに複数のインスタンスを割り当てることで、サーバーを共有できます。 インスタンスは互いに完全に分離され、独自のデータベースと設定ファイルで動作します。

特定のサーバーの場合、すべてのAdobe Campaign インスタンスに共通する2つの要素があります。

* **internal** パスワード：これは一般管理者のパスワードです。 特定のアプリケーションサーバーのすべてのインスタンスに共通です。

  >[!IMPORTANT]
  >
  >**Internal**&#x200B;識別子でログオンするには、事前にパスワードを定義しておく必要があります。 詳しくは、[この節](../../installation/using/configuring-campaign-server.md#internal-identifier)を参照してください。

* 複数のテクニカルサーバー設定：これらの設定はすべて、インスタンスの特定の設定でオーバーロードできます。

設定ファイルは、インストールディレクトリの&#x200B;**conf** ディレクトリに保存されます。 設定は、次の3つのファイルに分かれています。

* **serverConf.xml**：すべてのインスタンスの全体的な設定。
* **config-**`<instance>`**.xml** （**`<instance>`**&#x200B;はインスタンス名）: インスタンスの特定の設定。
* **serverConf.xml.diff**：初期設定と現在の設定の差分。 このファイルはアプリケーションによって自動的に生成されるので、手動で変更することはできません。 ビルドバージョンを更新する際に、ユーザーの変更を自動的に反映するために使用されます。

インスタンス設定は次のように読み込まれます。

* モジュールは&#x200B;**serverConf.xml** ファイルを読み込み、すべてのインスタンスで共有されているパラメーターを取得します。
* 次に、**config-**`<instance>`**.xml** ファイルが読み込まれます。 このファイルに見つかった値は、**serverConf.xml**&#x200B;に含まれる値よりも優先されます。

  これらの2つのファイルの形式は同じです。 **serverConf.xml**&#x200B;の値はすべて、**config-`<instance>`.xml** ファイル内の特定のインスタンスに対してオーバーロードできます。

この動作モードは、設定に優れた柔軟性を提供します。
