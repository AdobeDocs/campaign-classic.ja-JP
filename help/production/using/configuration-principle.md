---
product: campaign
title: 設定の原則
description: 設定の原則
audience: production
content-type: reference
topic-tags: production-procedures
exl-id: 03d7e579-8678-44b8-bbe7-cf4204bffb25
source-git-commit: 20509f44c5b8e0827a09f44dffdf2ec9d11652a1
workflow-type: tm+mt
source-wordcount: '281'
ht-degree: 4%

---

# 設定の原則{#configuration-principle}

![](../../assets/v7-only.svg)

Adobe Campaignプラットフォームは、Apache が使用する仮想ホストと同様に、インスタンスの概念に基づいています。 この操作モードでは、複数のインスタンスを割り当ててサーバーを共有できます。 インスタンスは完全に分離され、独自のデータベースと設定ファイルで動作します。

特定のサーバーには、すべてのAdobe Campaignインスタンスに共通する 2 つの要素があります。

* **内部** パスワード：これは、一般的な管理者パスワードです。 特定のアプリケーションサーバーのすべてのインスタンスに共通です。

   >[!IMPORTANT]
   >
   >**内部** 識別子を使用してログオンするには、事前にパスワードを定義しておく必要があります。 詳しくは、[この節](../../installation/using/configuring-campaign-server.md#internal-identifier)を参照してください。

* 複数のテクニカルサーバー設定：これらの設定は、すべて、インスタンスの特定の設定でオーバーロードできます。

設定ファイルは、インストールディレクトリの **conf** ディレクトリに保存されます。 設定は次の 3 つのファイルに分類されます。

* **serverConf.xml**:すべてのインスタンスの全体的な設定。
* **config-**`<instance>`**.xml** ( **`<instance>`** はインスタンス名 ):インスタンスの特定の設定。
* **serverConf.xml.diff**:初期設定と現在の設定の差。このファイルは、アプリケーションによって自動的に生成され、手動で変更しないでください。 ビルドバージョンの更新時に、ユーザーの変更を自動的に反映するために使用されます。

インスタンス設定は次のように読み込まれます。

* このモジュールは、**serverConf.xml** ファイルを読み込んで、すべてのインスタンスで共有されるパラメータを取得します。
* 次に、**config-**`<instance>`**.xml** ファイルを読み込みます。 このファイルに含まれる値は、**serverConf.xml** に含まれる値よりも優先されます。

   これら 2 つのファイルは同じ形式です。 **serverConf.xml** の値は、**config-`<instance>`.xml** ファイルの特定のインスタンスに対してオーバーロードできます。

この動作モードは、設定に対して非常に柔軟性があります。
