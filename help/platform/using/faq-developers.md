---
product: campaign
title: 開発者向け FAQ
description: 開発者向け FAQ
feature: Troubleshooting, Configuration
audience: platform
content-type: reference
level: Intermediate, Experienced
topic-tags: starting-with-adobe-campaign
exl-id: 20552812-5c58-4d48-9636-d5135197685d
source-git-commit: 2bfcec5eaa1145cfb88adfa9c8b2f72ee3cd9469
workflow-type: ht
source-wordcount: '509'
ht-degree: 100%

---

# 開発者向け FAQ {#dev-faq}



オープンなソリューションである Adobe Campaign は、カスタマイズと高度なアプリケーション開発に対応しています。

## Campaign データモデルとは何ですか？ {#what-is-the-campaign-data-model}

Adobe Campaign データベースの概念データモデルは、一連のビルトインテーブルとそのインタラクションで構成されます。アプリケーションに格納されるデータの物理的および論理的構造は、XML で記述されます。スキーマと呼ばれる Adobe Campaign 特有の文法に従います。Adobe Campaign スキーマについて詳しくは、[この節](../../configuration/using/about-schema-edition.md)を参照してください。

[Campaign データモデルについて詳しくは、こちらをクリックしてください](https://helpx.adobe.com/jp/campaign/kb/acc-datamodel.html)。

ベストプラクティスについて詳しくは、[この記事](../../configuration/using/data-model-best-practices.md)を参照してください。

## Campaign スキーマの操作方法は？ {#how-to-work-with-campaign-schemas-}

Adobe Campaign では、以下のためにデータスキーマが使用されます。

* アプリケーション内のデータオブジェクトが基盤となるデータベーステーブルにどのように関連付けられるかの定義
* Campaign アプリケーション内での異なるデータオブジェクト間リンクの定義
* 各オブジェクトに含まれている個々のフィールドの定義と記述

データスキーマの操作方法やニーズに対処するための Campaign の拡張およびカスタマイズの方法については、[テーブルとスキーマの概要](../../configuration/using/about-schema-edition.md)を参照してください。

## カスタム受信者テーブルの使用方法は？ {#how-to-use-a-custom-recipient-table-}

Campaign でビルトイン以外の受信者テーブルを作成および実装してメッセージを送信することができます。

[詳しくはこちらをクリックしてください。](../../configuration/using/about-custom-recipient-table.md)

## Campaign でクエリを定義するためのベストプラクティスは？ {#what-are-the-best-practices-to-define-queries-in-campaign-}

Adobe Campaign クエリエディターは、データの調査やセグメントの作成をおこなうための強力なツールです。

Adobe Campaign のクエリツールは、ターゲット母集団の作成、顧客のセグメント化、トラッキングログの抽出とフィルター、フィルターの作成などのために、ソフトウェアの複数のレベルで使用できます。

汎用クエリエディターを使用して Campaign データベースに対するクエリを実行できます。汎用クエリエディターにアクセスするには、**ツール／汎用クエリエディター...** メニューを使用します。汎用クエリエディターでは、データベースに格納されている情報を抽出し、構成、グループ化、並べ替えなどをおこなうことができます。例えば、ユーザーは、特定の期間にニュースレター内のリンクを「n」回以上クリックした受信者を収集することができます。このツールでは、ニーズに応じて結果を収集、並べ替えおよび表示できます。このツールは、Adobe Campaign のすべてのクエリ機能を組み合わせたものです。例えば、制限フィルターを作成して保存できます。つまり、汎用クエリエディターで作成したユーザーフィルターを、ターゲティングワークフローのクエリボックスなどで使用できます。

クエリは、選択したテーブルのフィールドを使用するか、数式を使用して作成します。Campaign データベースに対するクエリを作成する際の主な原則については、[このページ](../../platform/using/about-queries-in-campaign.md)を参照してください。

[ここをクリック](../../workflow/using/query.md)して、Campaign クエリエディターを開きます。

## データパッケージをインポートするにはどうすればよいですか？ {#how-can-i-import-a-data-package-}

Adobe Campaign では、パッケージシステムを通じて、プラットフォーム設定とデータをエクスポートまたはインポートできます。データパッケージを使用すると、XML 形式のファイル経由で Adobe Campaign データベース内のエンティティを表示できます。パッケージに含まれる 1 つのエンティティは、それに該当するすべてのデータによって表現されます。

データパッケージの原則とは、データの設定をエクスポートして別の Adobe Campaign システム内に組み込むことです。

Campaign の設定をインポートおよびエクスポートするためにデータパッケージを使用する方法については、[ここをクリック](../../platform/using/working-with-data-packages.md)してください。

## Campaign Classic API のリストはどこで参照できますか？ {#where-can-i-find-the-list-of-campaign-classic-apis}

すべての Campaign API とその詳細な説明については、この[専用ドキュメント](https://experienceleague.adobe.com/developer/campaign-api/api/index.html?lang=ja)を参照してください。
