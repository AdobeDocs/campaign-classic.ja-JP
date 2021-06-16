---
product: campaign
title: コンテンツ管理について
description: コンテンツ管理について
audience: delivery
content-type: reference
topic-tags: content-management
exl-id: 87434cc2-1636-4558-ab60-255b7f873c0c
source-git-commit: 895aa2fd4fa9c7c71c0073e9be33c12d4e92c9fa
workflow-type: tm+mt
source-wordcount: '245'
ht-degree: 91%

---

# コンテンツ管理について{#about-content-management}

Adobe Campaign Content Managerモジュールは、定期的ニュースレターやWebサイトを作成するためにインストールできる、特定のCampaign Classic[組み込みパッケージ](../../installation/using/installing-campaign-standard-packages.md)です。 このモジュールを使用して、メッセージを作成、検証、パブリッシュできます。

>[!NOTE]
>
>この節では、コンテンツ管理モジュールについて説明します。E メール配信コンテンツのデザイン方法について詳しくは、[この節](../../delivery/using/defining-the-email-content.md)を参照してください。

コンテンツ管理モジュールには、作業グループ、ワークフローおよびコンテンツ集計機能が含まれます。そのため、メッセージを自動的に書式設定できます（E メール、郵便、SMS、Web など）。

配信でコンテンツ管理を利用すると、コンテンツの作成を担当するオペレーターに入力フィールドまたは選択フィールドを提供できます。このコンテンツのレイアウトと表示、変更は、スタイルシートを使用して自動的に管理されます。

![](assets/s_ncs_content_create_content_sample.png)

>[!CAUTION]
>
>スタイルシートに対する変更はすべて、使用するコンテンツテンプレートに基づいて、配信レベルで実施されます。

コンテンツ管理には次のメリットがあります。

* 入力インターフェイスを通じて構造化されたメッセージ編集ができる
* データコンテンツとその表示方法を分離できる（XML フォーマットで生成）
* グラフィックガイドラインに則ったスタイルシートに基づき、複数フォーマット（html、txt、XML など）のドキュメントを生成できる
* 外部コンテンツフローを復元し、自動集計できる
* データの検証や確認をおこなうワークフローと連携できる

ただし、このコンテンツ作成モードには、次のように、いくつかの制約があります。

* ドキュメントの最終デザインに関する制限
* 機能の不足によってエンドユーザーが不便を感じることのないように、要件は厳密に分析する必要があります。
