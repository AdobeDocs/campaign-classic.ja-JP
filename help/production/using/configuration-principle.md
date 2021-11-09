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

Adobe Campaignプラットフォームは、Apache が使用する仮想ホストと同様に、インスタンスの概念に基づいています。 この操作モードでは、複数のインスタンスを割り当ててサーバーを共有できます。 インスタンスは完全に別々で、独自のデータベースと設定ファイルを使用して動作します。

特定のサーバーに対して、すべてのAdobe Campaignインスタンスに共通する 2 つの要素があります。

* この **内部** パスワード：これは、一般的な管理者パスワードです。 特定のアプリケーションサーバーのすべてのインスタンスに共通です。

   >[!IMPORTANT]
   >
   >を使用してログオンするには、以下を実行します。 **内部** 識別子の場合は、事前にパスワードを定義しておく必要があります。 詳しくは、[この節](../../installation/using/configuring-campaign-server.md#internal-identifier)を参照してください。

* 複数のテクニカルサーバー設定：これらの設定は、すべて、インスタンスの特定の設定でオーバーロードできます。

設定ファイルは、 **conf** インストールディレクトリのディレクトリ。 設定は、次の 3 つのファイルに分類されます。

* **serverConf.xml**:すべてのインスタンスの全体的な設定。
* **config-**`<instance>`**.xml** ( **`<instance>`** はインスタンス名です )。インスタンスの特定の設定。
* **serverConf.xml.diff**:初期設定と現在の設定の差分。 このファイルは、アプリケーションによって自動的に生成され、手動で変更しないでください。 ビルドバージョンの更新時に、ユーザーの変更を自動的に反映するために使用されます。

インスタンスの設定は、次のように読み込まれます。

* モジュールは、 **serverConf.xml** ファイルを参照して、すべてのインスタンスで共有されるパラメーターを取得します。
* その後、 **config-**`<instance>`**.xml** ファイル。 このファイルで見つかった値は、 **serverConf.xml**.

   これら 2 つのファイルは同じ形式です。 の任意の値 **serverConf.xml** は、 **config-`<instance>`.xml** ファイル。

この動作モードは、設定を柔軟に行うことができます。
