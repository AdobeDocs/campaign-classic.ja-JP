---
title: 要素のレイアウト
seo-title: 要素のレイアウト
description: 要素のレイアウト
seo-description: null
page-status-flag: never-activated
uuid: 60dc80d9-f81b-48ce-9341-f975daaf5ebc
contentOwner: sauviat
products: SG_CAMPAIGN/CLASSIC
audience: reporting
content-type: reference
topic-tags: creating-new-reports
discoiquuid: 8fdda764-3e42-4972-a9c9-63567588931e
index: y
internal: n
snippet: y
translation-type: ht
source-git-commit: 209ac4d81d2d27c264ee6b288bcb7fcb1900ffc5

---


# 要素のレイアウト{#element-layout}

[グラフのタイプとバリエーション](../../reporting/using/creating-a-chart.md#chart-types-and-variants)で説明する様々なグラフに加えて、表示を適応させたり、レポートページに要素を追加したりできます。

コンテナを使用すると、ページの複数の要素をリンクし、それらのレイアウトを列やセルで設定できます。それらの使用方法について詳しくは、[この節](../../web/using/defining-web-forms-layout.md#creating-containers)を参照してください。

ツリーのルートでレポートのレイアウトを設定し、コンテナごとにそれをオーバーロードできます。ページは列に並べ替えられます。コンテナも列に並べ替えられます。静的要素およびグラフィカル要素のみ、セルに並べ替えられます。

## 各ページのオプションの定義 {#defining-the-options-for-each-page}

レポートの各ページでオプションを使用できます。

「**[!UICONTROL 一般]**」タブでは、ページのタイトルを変更できるほか、凡例の位置やレポートページ間のナビゲーションを設定できます。

![](assets/s_ncs_advuser_report_wizard_022.png)

「**[!UICONTROL タイトル]**」フィールドでは、レポートページのヘッダーのレベルをパーソナライズできます。ウィンドウのタイトルは、レポートの&#x200B;**[!UICONTROL プロパティ]**&#x200B;ウィンドウで設定できます。詳しくは、[ヘッダーやフッターの追加](#adding-a-header-and-a-footer)を参照してください。

「**[!UICONTROL 表示設定]**」オプションでは、レポートページ内のコントロールキャプションの位置を選択したり、ページの列数を定義したりできます。ページレイアウトについて詳しくは、[この節](../../web/using/defining-web-forms-layout.md#positioning-the-fields-on-the-page)の&#x200B;**項目のレイアウト**&#x200B;に関する節を参照してください。

「**[!UICONTROL ナビゲーション]**」セクションで様々オプションを選択すると、レポートページ間の移動を許可することができます。「**[!UICONTROL 次のページを無効にする]**」オプションまたは「**[!UICONTROL 前のページに戻ることを許可しない]**」オプションを選択すると、「**[!UICONTROL 次のページ]**」ボタンまたは「**[!UICONTROL 前のページ]**」ボタンがレポートページに表示されなくなります。

## ヘッダーやフッターの追加 {#adding-a-header-and-a-footer}

レポートのプロパティウィンドウでは、レイアウト要素（ウィンドウのタイトルやヘッダーおよびフッターの HTML コンテンツなど）も定義できます。

プロパティウィンドウにアクセスするには、レポートの「**[!UICONTROL プロパティ]**」ボタンをクリックします。

![](assets/reporting_properties.png)

「**[!UICONTROL ページ]**」タブでは、表示をパーソナライズできます。

![](assets/s_ncs_advuser_report_properties_04.png)

このタブで設定したコンテンツは、すべてのレポートページに表示されます。

「**[!UICONTROL テキスト]**」サブタブでは、変数コンテンツを定義できます。レポートが複数の言語で使用されるように設計されている場合は、翻訳サイクルでこの変数コンテンツが考慮されます。

このサブタブでは、テキスト断片のリストを作成し、それらを識別子に関連付けることができます。

![](assets/s_ncs_advuser_report_properties_04a.png)

その後で、これらの識別子をレポートの HTML コンテンツに挿入します。

![](assets/s_ncs_advuser_report_properties_04b.png)

これらの識別子は、レポートが表示される際に、適切なコンテンツに自動的に置き換わります。

HTML テキストの場合と同様に、この動作モードによって、レポートで使用するテキストとその翻訳を一元管理できます。このタブで作成したテキストは、Adobe Campaign の統合翻訳ツールで自動的に収集されます。
