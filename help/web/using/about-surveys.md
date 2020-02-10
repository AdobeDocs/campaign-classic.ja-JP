---
title: 調査について
seo-title: 調査について
description: 調査について
seo-description: null
page-status-flag: never-activated
uuid: 31a07a48-2ebb-4b51-ae24-382f3ce3f04a
contentOwner: sauviat
products: SG_CAMPAIGN/CLASSIC
audience: web
content-type: reference
topic-tags: online-surveys
discoiquuid: ef7d9b16-506a-409c-a578-000b88cd17a2
index: y
internal: n
snippet: y
translation-type: tm+mt
source-git-commit: c9c9d5f96856ce9e19571bad032d2bf04eaa60bd

---


# 調査について{#about-surveys}

Adobe Campaign には、Web アプリケーションを定義およびパブリッシュするためのグラフィカルなモジュールが含まれています。これは、エクストラネット上の編集フォームや、データベースからのデータを含み、テーブル、グラフ、入力フォームなどを備えた通知フォームなどの、ページの作成に使用されます。この機能を使用すると、ユーザーが情報を調べたり入力したりできる Web ページをデザインおよび投稿できます。

オプションの&#x200B;**調査**&#x200B;モジュールを使用すると、プロファイル情報を追加または修正するフォーム、情報サービスを購読または購読解除するフォーム、競合他社入力フォームなど、オンラインアンケートを作成および管理するための、新しいタイプの Web アプリケーションを作成できます。回答が収集されると、データベースまたはローカル変数に格納されます。データモデルは、アンケートの回答を使用して動的に拡張できます。結果をリアルタイムに表示したり、回答をフィルターしたり、専用のグラフを使用してそれらを分析したりできます。

この章では、**調査**&#x200B;の作成および管理方法、フィールドとページの管理、ストレージモードとレコードについて詳しく説明します。

標準 Web フォームの作成手順について詳しくは、[この節](../../web/using/about-web-forms.md)を参照してください。

Web アプリケーション管理について詳しくは、[この節](../../web/using/about-web-applications.md)を参照してください。その他について詳しくは、この章を参照してください。

>[!CAUTION]
>
>プライバシー保護のために、すべての外部リソースに対して HTTPS を使用することをお勧めします。

## キャンペーン調査の範囲 {#campaign-surveys-scope}

Adobe Campaign では、一般に、Web アプリケーションを使用すると、次の機能を利用できます。

* 複数ページのフォームの作成
* 統合された翻訳ツールによる多言語の調査の管理
* グラフィカルなページ管理インターフェイス、複数列のページレイアウト
* パーソナライゼーションとフィールドの位置のレンダリング
* 回答に応じた調査フィールドの条件付き表示
* 条件付きページ表示
* 期待されるデータのタイプ（数値、E メールアドレス、日付など）および必須フィールドに応じて、承認前に情報をチェック
* E メールの招待状／通知
* エラーおよび終了メッセージのパーソナライゼーション
* 画像、ビデオ、ハイパーテキストリンク、Captcha などの使用

>[!NOTE]
>
>Web フォームに関連するすべての設定について詳しくは、[この節](../../web/using/about-web-forms.md)を参照してください。概念および Adobe Campaign を使用した Web フォームの機能について詳しくは、このドキュメントを参照してください。

オプションの調査作成モジュール（**調査**）は、次の追加機能を提供します。

* データベースの動的な拡張（最初のデータモデルに含まれない回答の作成）：詳しくは、「収集した回答の保存」を [参照してください](../../web/using/managing-answers.md#storing-collected-answers)。
* スコア管理. For more on this, refer to [Score management](../../web/using/managing-answers.md#score-management).
* 質問のランダム表示：For more on this, refer to [Adding questions](../../web/using/building-a-survey.md#adding-questions).
* 回答のリアルタイムトラッキング：For more on this, refer to [Response tracking](../../web/using/publish--track-and-use-collected-data.md#response-tracking).
* 専用レポートの生成For more on this, refer to [Reports on surveys](../../web/using/publish--track-and-use-collected-data.md#reports-on-surveys).

Web アプリケーションと比較すると、調査は、シンプルなグラフィカルインターフェイスを備え、編集コントロールが少なくなっています。

## 調査の実装手順 {#surveys-implementation-steps}

次の手順に従って、調査を作成および配信し、その結果を処理します。

1. 調査のページおよびそのコンテンツ（入力フィールド、ドロップダウンリスト、質問など）を作成します。
1. 回答の保存方法を定義します。

   既にデータベースにあるデータをフォームにプリロードするために、データのプリロード手順を挿入できます。テストボックスを追加することもできます。

1. 調査を投稿し、受信者に配信します（例：配信またはWebサイトにリンクを含める）。
1. 回答を監視し、レポートを表示します。

これらの手順の設定と順番については、[この節](../../web/using/about-web-forms.md)を参照してください。この章では、調査に固有の設定のみについて説明します。

## 調査の設定 {#surveys-configuration}

調査は、Adobe Campaignツリーの **[!UICONTROL Resources > Online > Web Applications]** ノードに保存されます。 設定は、次のフォルダーにあります。

* **[!UICONTROL Administration > Configuration > Form rendering]**:には、Webフォームプレゼンテーション（アプリケーションおよび調査）用のレンダリングテンプレートが含まれています。
* **[!UICONTROL Resources > Templates > Web application templates]**:フォームテンプレートが含まれます。 フォームを作成するには、テンプレートから開始する必要があります。

>[!NOTE]
>
>設定について詳しくは、[この節](../../web/using/about-web-forms.md)を参照してください。

