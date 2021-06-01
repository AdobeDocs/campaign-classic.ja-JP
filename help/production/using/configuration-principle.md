---
product: campaign
title: 設定の原則
description: 設定の原則
audience: production
content-type: reference
topic-tags: production-procedures
exl-id: 03d7e579-8678-44b8-bbe7-cf4204bffb25
source-git-commit: 98d646919fedc66ee9145522ad0c5f15b25dbf2e
workflow-type: tm+mt
source-wordcount: '281'
ht-degree: 4%

---

# 設定の原則{#configuration-principle}

Adobe Campaignプラットフォームは、Apacheが使用する仮想ホストと同様に、インスタンスの概念に基づいています。 この操作モードでは、複数のインスタンスを割り当てて1つのサーバーを共有できます。 インスタンスは完全に分離され、独自のデータベースと設定ファイルで動作します。

特定のサーバーには、すべてのAdobe Campaignインスタンスに共通の2つの要素があります。

* **内部**&#x200B;パスワード：これは一般的な管理者パスワードです。 特定のアプリケーションサーバーのすべてのインスタンスに共通です。

   >[!IMPORTANT]
   >
   >**内部**&#x200B;識別子を使用してログオンするには、事前にパスワードを定義しておく必要があります。 詳細については、[このセクション](../../installation/using/configuring-campaign-server.md#internal-identifier)を参照してください。

* 複数のテクニカルサーバ設定：これらの設定は、すべて、インスタンスの特定の設定でオーバーロードできます。

設定ファイルは、インストールディレクトリの&#x200B;**conf**&#x200B;ディレクトリに保存されます。 設定は、次の3つのファイルに分類されます。

* **serverConf.xml**:すべてのインスタンスの全体的な設定。
* **config-**`<instance>`**.xml** ( **`<instance>`** はインスタンス名):インスタンスの特定の設定。
* **serverConf.xml.diff**:初期設定と現在の設定の差。このファイルは、アプリケーションによって自動的に生成され、手動で変更することはできません。 ビルドバージョンの更新時に、ユーザーの変更を自動的に反映するために使用されます。

インスタンス設定は次のように読み込まれます。

* このモジュールは、**serverConf.xml**&#x200B;ファイルを読み込んで、すべてのインスタンスで共有されるパラメーターを取得します。
* 次に、**config-**`<instance>`**.xml**&#x200B;ファイルを読み込みます。 このファイルに含まれる値は、**serverConf.xml**&#x200B;に含まれる値よりも優先されます。

   これら2つのファイルは同じ形式です。 **serverConf.xml**&#x200B;の値は、**config-`<instance>`.xml**&#x200B;ファイルの特定のインスタンスに対してオーバーロードできます。

この動作モードは、設定に対して非常に柔軟性があります。
