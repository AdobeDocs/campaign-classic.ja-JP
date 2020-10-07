---
title: 設定の原則
seo-title: 設定の原則
description: 設定の原則
seo-description: null
page-status-flag: never-activated
uuid: 6315d526-b820-46ab-96c7-e64e101c6a7d
contentOwner: sauviat
products: SG_CAMPAIGN/CLASSIC
audience: production
content-type: reference
topic-tags: production-procedures
discoiquuid: d08ff769-da93-4f86-8802-f0fb5b051ece
translation-type: tm+mt
source-git-commit: 70b143445b2e77128b9404e35d96b39694d55335
workflow-type: tm+mt
source-wordcount: '283'
ht-degree: 5%

---


# 設定の原則{#configuration-principle}

Adobe Campaignプラットフォームは、Apacheが使用する仮想ホストと同様、インスタンスの概念に基づいています。 この操作モードでは、1つのサーバーに複数のインスタンスを割り当てて1つのサーバーを共有できます。 インスタンスは互いに完全に分離され、独自のデータベースと設定ファイルを使用して動作します。

特定のサーバーには、すべてのAdobe Campaignインスタンスに共通の2つの要素があります。

* 内部 **パスワード** :これは、一般管理者のパスワードです。 特定のアプリケーションサーバーのすべてのインスタンスに共通です。

   >[!CAUTION]
   >
   >**Internal** identifierを使用してログオンするには、事前にパスワードを定義しておく必要があります。 詳しくは、[この節](../../installation/using/campaign-server-configuration.md#internal-identifier)を参照してください。

* 複数のテクニカルサーバ構成：これらの設定はすべて、インスタンスの特定の設定で過負荷になる可能性があります。

設定ファイルは、インストールディレクトリの **conf** ディレクトリに保存されます。 設定は3つのファイルに分類されます。

* **serverConf.xml**:すべてのインスタンスの全体的な設定。
* **config-**`<instance>`**.xml** ( **`<instance>`** はインスタンス名):インスタンスの特定の設定。
* **serverConf.xml.diff**:初期設定と現在の設定の差。 このファイルはアプリケーションによって自動的に生成され、手動で変更することはできません。 これは、ビルドバージョンの更新時に、ユーザーによる変更を自動的に反映するために使用されます。

インスタンス設定は、次のようにロードされます。

* モジュールは、 **serverConf.xml** ファイルを読み込み、すべてのインスタンスで共有されるパラメーターを取得します。
* 次に、 **config-**`<instance>`**.xml** ファイルを読み込みます。 このファイルで見つかる値は、 **serverConf.xmlに含まれる値よりも優先されます**。

   これら2つのファイルは同じ形式です。 serverConf.xml **内の任意の値を、** config- **.xml`<instance>`** ファイル内の特定のインスタンスに対してオーバーロードできます。

このオペレーティングモードは、設定を柔軟に行うことができます。
