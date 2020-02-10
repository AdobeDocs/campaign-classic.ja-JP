---
title: コンテンツマネージャーのリソースと原則
seo-title: コンテンツマネージャーのリソースと原則
description: コンテンツマネージャーのリソースと原則
seo-description: null
page-status-flag: never-activated
uuid: 3560e392-129a-471d-a211-05481cdda224
contentOwner: sauviat
products: SG_CAMPAIGN/CLASSIC
audience: delivery
content-type: reference
topic-tags: content-management
discoiquuid: b22b3abb-6fe5-4f4d-93fc-0d00d426edb6
index: y
internal: n
snippet: y
translation-type: tm+mt
source-git-commit: 7dbc876fae0bde78e3088ee1ab986cd09e9bcc38

---


# コンテンツマネージャーのリソースと原則{#content-manager-resources-and-principles}

パブリッシュテンプレートを定義する必要があります。このテンプレートには、コンテンツごとの変換テンプレートが含まれます。

コンテンツブロックは、データストレージ用の XML ドキュメント内で構造化します。編集インターフェイスを使用して、Adobe Campaign のクライアントコンソールまたは Web ブラウザーからコンテンツを入力します。コンテンツは、XML フローのキャプチャまたはデータベースに集計されたデータから自動的に入力することもできます。

XML ドキュメントと XSL スタイルシートまたは JavaScript テンプレートのスタイルシートを組み合わせると、様々なフォーマット（HTML、テキスト）のパブリッシュテンプレートモデルが自動的に生成されます。

![](assets/d_ncs_content_process.png)

コンテンツの設定には次のリソースが必要です。

* データスキーマ：XML コンテンツ構造を記述したもの。For more on this, refer to [Data schemas](../../delivery/using/data-schemas.md).
* データ入力フォーム：データ入力画面の構造。For more on this, refer to [Input forms](../../delivery/using/input-forms.md).
* 画像：データ入力フォームで使用する画像。For more on this, refer to [Image management](../../delivery/using/formatting.md#image-management).
* スタイルシート：XSLT 言語を使用した出力ドキュメントの書式設定。For more on this, refer to [Formatting](../../delivery/using/formatting.md).
* JavaScript テンプレート：JavaScript 言語を使用した出力ドキュメントの書式設定。For more on this, refer to [Publication templates](../../delivery/using/publication-templates.md).
* JavaScriptコード：データ集計用のJavaScriptコード。 For more on this, refer to [Aggregator](../../delivery/using/publication-templates.md#aggregator).
* パブリッシュテンプレート：パブリッシュテンプレートの定義。For more on this, refer to [Publication templates](../../delivery/using/publication-templates.md).
* コンテンツ：作成してパブリッシュするコンテンツインスタンス。For more on this, refer to [Using a content template](../../delivery/using/using-a-content-template.md).
