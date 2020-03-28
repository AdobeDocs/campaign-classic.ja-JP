---
title: よくある質問
seo-title: よくある質問
description: Campaign Classic に関する FAQ
page-status-flag: never-activated
uuid: 3f719ac2-cc26-4fb0-adda-84666c8c38e1
contentOwner: sauviat
products: SG_CAMPAIGN/CLASSIC
audience: platform
content-type: reference
topic-tags: starting-with-adobe-campaign
discoiquuid: 16dbe423-018f-4666-9901-2120a8dc609a
index: y
internal: n
snippet: y
translation-type: ht
source-git-commit: 994ec35e37a1c26e83a8dd2ae31f6594cadd4c45

---


# 開発者向け FAQ {#dev-faq}

オープンなソリューションである Adobe Campaign は、カスタマイズと高度なアプリケーション開発ができるようになっています。

## Campaign データモデルとは何ですか？{#what-is-the-campaign-data-model}

Adobe Campaign データベースの概念データモデルは、一連の組み込みテーブルとそのインタラクションで構成されます。アプリケーションに格納されるデータの物理的および論理的構造は、XML で記述されます。スキーマと呼ばれる Adobe Campaign 特有の文法に従います。Adobe Campaign スキーマについて詳しくは、[この節](../../configuration/using/about-schema-edition.md)を参照してください。

Campaign データモデルについて詳しくは、[ここをクリック](https://helpx.adobe.com/jp/campaign/kb/acc-datamodel.html)してください。

ベストプラクティスについては、[この記事](https://helpx.adobe.com/jp/campaign/kb/acc-data-model-best-practices.html)を参照してください。

## Campaign スキーマの操作方法は？{#how-to-work-with-campaign-schemas-}

Adobe Campaign では、以下のためにデータスキーマが使用されます。

* アプリケーション内のデータオブジェクトが基盤となるデータベーステーブルにどのように関連付けられるかの定義
* Campaign アプリケーション内での異なるデータオブジェクト間リンクの定義
* 各オブジェクトに含まれている個々のフィールドの定義と記述

データスキーマの操作方法やニーズに対処するための Campaign の拡張およびカスタマイズの方法については、[テーブルとスキーマの概要](../../configuration/using/about-schema-edition.md)を参照してください。

## カスタム受信者テーブルの使用方法は？{#how-to-use-a-custom-recipient-table-}

メッセージを送信するために、Campaign で標準以外の受信者テーブルを作成および実装できます。

[詳しくはここをクリック](../../configuration/using/about-custom-recipient-table.md)

## Campaign でクエリを定義するためのベストプラクティスは？{#what-are-the-best-practices-to-define-queries-in-campaign-}

Adobe Campaign クエリエディターは、データの調査やセグメントの作成をおこなうための強力なツールです。

Adobe Campaign のクエリツールは、ターゲット母集団の作成、顧客のセグメント化、トラッキングログの抽出とフィルター、フィルターの作成などのために、ソフトウェアの複数のレベルで使用できます。

汎用クエリエディターを使用して Campaign データベースに対するクエリを実行できます。汎用クエリエディターにアクセスするには、**ツール／汎用クエリエディター...** メニューを使用します。汎用クエリエディターでは、データベースに格納されている情報を抽出し、構成、グループ化、並べ替えなどをおこなうことができます。例えば、ユーザーは、特定の期間にニュースレター内のリンクを「n」回以上クリックした受信者を収集することができます。このツールでは、ニーズに応じて結果を収集、並べ替えおよび表示できます。このツールは、Adobe Campaign のすべてのクエリ機能を組み合わせたものです。例えば、制限フィルターを作成して保存できます。つまり、汎用クエリエディターで作成したユーザーフィルターを、ターゲティングワークフローのクエリボックスなどで使用できます。

クエリは、選択したテーブルのフィールドを使用するか、数式を使用して作成します。Campaign データベースに対するクエリを作成する際の主な原則については、[このページ](../../platform/using/about-queries-in-campaign.md)を参照してください。

[ここをクリック](../../workflow/using/query.md)して、Campaign クエリエディターを開きます。

## データパッケージはどうすればインポートできますか？{#how-can-i-import-a-data-package-}

Adobe Campaign では、パッケージシステムを通じて、プラットフォーム設定とデータをエクスポートまたはインポートできます。データパッケージを使用すると、XML 形式のファイル経由で Adobe Campaign データベース内のエンティティを表示できます。パッケージに含まれる 1 つのエンティティは、それに該当するすべてのデータによって表現されます。

データパッケージの原則とは、データの設定をエクスポートして別の Adobe Campaign システム内に組み込むことです。

Campaign の設定をインポートおよびエクスポートするためにデータパッケージを使用する方法については、[ここをクリック](../../platform/using/working-with-data-packages.md)してください。

## Campaign Classic API のリストはどこにありますか？{#where-can-i-find-the-list-of-campaign-classic-apis}

詳細な説明を含むすべての Campaign API は、この[専用ドキュメント](https://docs.adobe.com/content/help/en/campaign-classic/technicalresources/api/index.html)で利用できます。
