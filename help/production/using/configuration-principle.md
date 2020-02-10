---
title: 設定原則
seo-title: 設定原則
description: 設定原則
seo-description: null
page-status-flag: never-activated
uuid: 6315d526-b820-46ab-96c7-e64e101c6a7d
contentOwner: sauviat
products: SG_CAMPAIGN/CLASSIC
audience: production
content-type: reference
topic-tags: production-procedures
discoiquuid: d08ff769-da93-4f86-8802-f0fb5b051ece
index: y
internal: n
snippet: y
translation-type: tm+mt
source-git-commit: 34cd6e6cf5652c9e2163848c2b1ef32f53ee6ca4

---


# 設定原則{#configuration-principle}

Adobe Campaignプラットフォームは、Apacheが使用する仮想ホストと同様に、インスタンスの概念に基づいています。 この操作モードでは、1つのサーバーに複数のインスタンスを割り当てることで、1つのサーバーを共有できます。 インスタンスは互いに完全に分離され、独自のデータベースと設定ファイルを使用して動作します。

特定のサーバーには、すべてのAdobe Campaignインスタンスに共通の2つの要素があります。

* 内部パ **スワード** :一般管理者のパスワードです。 特定のアプリケーションサーバーのすべてのインスタンスに共通です。

   >[!CAUTION]
   >
   >内部識別子を使用してログオ **ンするには** 、事前にパスワードを定義しておく必要があります。 詳しくは、[この節](../../installation/using/campaign-server-configuration.md#internal-identifier)を参照してください。

* 複数のテクニカルサーバ構成：これらの設定はすべて、インスタンスの特定の設定でオーバーロードできます。

設定ファイルは、インストールディレクトリの **conf** ディレクトリに保存されます。 設定は3つのファイルに分類されます。

* **serverConf.xml**:すべてのインスタンスの全体的な設定。
* **config-**`<instance>`**.xml** (はイン **`<instance>`** スタンス名です):インスタンスの特定の設定。
* **serverConf.xml.diff**:初期設定と現在の設定の差。 このファイルはアプリケーションによって自動的に生成され、手動で変更しないでください。 これは、ビルドバージョンの更新時にユーザーの変更を自動的に反映するために使用されます。

インスタンス設定は、次のように読み込まれます。

* モジュールは、 **serverConf.xmlファイルを読み込み** 、すべてのインスタンスで共有されるパラメーターを取得します。
* 次に、 **config-**`<instance>`**.xmlファイルを読み込みます** 。 このファイルで見つかった値は、 **serverConf.xmlに含まれる値よりも優先されます**。

   これら2つのファイルは同じ形式です。 config- **.xmlファイル内の特定のインスタンスに対して、** serverConf.xml内の任意の値をオーバーロードできます **`<instance>`** 。

このオペレーティングモードは、設定に非常に柔軟性があります。
