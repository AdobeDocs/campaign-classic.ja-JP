---
solution: Campaign Classic
product: campaign
title: 設定の原則
description: 設定の原則
audience: production
content-type: reference
topic-tags: production-procedures
translation-type: tm+mt
source-git-commit: 972885c3a38bcd3a260574bacbb3f507e11ae05b
workflow-type: tm+mt
source-wordcount: '281'
ht-degree: 4%

---


# 設定の原則{#configuration-principle}

Adobe Campaignプラットフォームは、Apacheが使用する仮想ホストと同様、インスタンスの概念に基づいています。 この操作モードでは、1つのサーバーに複数のインスタンスを割り当てて1つのサーバーを共有できます。 インスタンスは互いに完全に分離され、独自のデータベースと設定ファイルを使用して動作します。

特定のサーバーには、すべてのAdobe Campaignインスタンスに共通の2つの要素があります。

* **internal**&#x200B;パスワード：これは、一般管理者のパスワードです。 特定のアプリケーションサーバーのすべてのインスタンスに共通です。

   >[!IMPORTANT]
   >
   >**内部**&#x200B;識別子を使用してログオンするには、事前にパスワードを定義しておく必要があります。 詳しくは、[こちらの節](../../installation/using/campaign-server-configuration.md#internal-identifier)を参照してください。

* 複数のテクニカルサーバ構成：これらの設定はすべて、インスタンスの特定の設定で過負荷になる可能性があります。

設定ファイルは、インストールディレクトリの&#x200B;**conf**&#x200B;ディレクトリに保存されます。 設定は3つのファイルに分類されます。

* **serverConf.xml**:すべてのインスタンスの全体的な設定。
* **config-**`<instance>`**.xml** ( **`<instance>`** はインスタンス名):インスタンスの特定の設定。
* **serverConf.xml.diff**:初期設定と現在の設定の差。このファイルはアプリケーションによって自動的に生成され、手動で変更することはできません。 これは、ビルドバージョンの更新時に、ユーザーによる変更を自動的に反映するために使用されます。

インスタンス設定は、次のようにロードされます。

* モジュールは、**serverConf.xml**&#x200B;ファイルを読み込み、すべてのインスタンスで共有されるパラメーターを取得します。
* 次に、**config-**`<instance>`**.xml**&#x200B;ファイルを読み込みます。 このファイル内の値は、**serverConf.xml**&#x200B;に含まれる値よりも優先されます。

   これら2つのファイルは同じ形式です。 **serverConf.xml**&#x200B;内の値は、**config-`<instance>`.xml**&#x200B;ファイル内の特定のインスタンスに対してオーバーロードできます。

このオペレーティングモードは、設定を柔軟に行うことができます。
