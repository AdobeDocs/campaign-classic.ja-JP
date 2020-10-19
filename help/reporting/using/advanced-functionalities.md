---
title: 高度な機能
description: 高度な機能
page-status-flag: never-activated
uuid: 4dbf4750-0226-4f96-98d8-ec49b20374ac
contentOwner: sauviat
products: SG_CAMPAIGN/CLASSIC
audience: reporting
content-type: reference
topic-tags: creating-new-reports
discoiquuid: 0c264783-2775-4ec6-8d49-cd9a45a18d60
translation-type: tm+mt
source-git-commit: 2a82493deada11cb22ef37d215b6eae8274ce890
workflow-type: tm+mt
source-wordcount: '647'
ht-degree: 54%

---


# 高度な機能{#advanced-functionalities}

技術ユーザーは、 [一般的なプロパティに加えて](../../reporting/using/properties-of-the-report.md)、次のような高度な機能を利用してレポートを設定できます。

* 複雑なクエリを作成して、 **スクリプト** アクティビティのデータを処理します。 [詳細情報](#script-activity)

* サーバー側追加またはクライアント側で実行する外部スクリプト。 [詳細情報](#external-script)

* ジャンプ **アクティビティを使用してレポートを呼び出します** 。 [詳細情報](#calling-up-another-report)

* アクセスしやすくす追加るためのURLパラメーター。 [詳細情報](#calling-up-another-report)

* レポートのコンテキストで追加使用される変数。 [詳細情報](#adding-variables)

## スクリプトの操作 {#adding-a-script}

### 外部スクリプトの参照 {#external-script}

レポートページが呼び出されたときにクライアント側やサーバー側で実行されるJavaScriptコードを参照できます。

手順は次のとおりです。

1. Edit the [report properties](../../reporting/using/properties-of-the-report.md) and click the **[!UICONTROL Scripts]**.
1. 「**[!UICONTROL 追加]**」をクリックし、参照するスクリプトを選択します。
1. 次に、実行モードを選択します。

   複数のスクリプトを追加する場合は、ツールバーの矢印を使用して、実行順序を定義します。

   ![](assets/reporting_custom_js.png)

クライアント側で通常の実行を行うには、参照先のスクリプトをJavaScriptで記述し、一般的なブラウザーとの互換性を持たせる必要があります。 詳しくは、[この節](../../web/using/web-forms-answers.md)を参照してください。

### Adding a Script activity {#script-activity}

レポートを [デザインする際に](../../reporting/using/creating-a-new-report.md#modelizing-the-chart)、 **** スクリプトアクティビティを使用してデータを処理し、SQL言語を有効にしない複雑なクエリを簡単に作成できます。 スクリプトウィンドウでクエリを直接入力できます。

「**[!UICONTROL テキスト]**」タブでは、テキスト文字列を定義できます。それらを使用するときの構文は、**$(Identifier)** のようになります。テキストの使用について詳しくは、[ヘッダーやフッターの追加](../../reporting/using/element-layout.md#adding-a-header-and-a-footer)を参照してください。

>[!CAUTION]
>
>JavaScript コードを使用して集計を作成することはお勧めしません。

レポートの履歴を作成するには、アーカイブしたデータを保存するために、JavaScript クエリに次の行を追加します。

```
if( ctx.@_historyId.toString().length == 0 )
```

そうしないと、現在のデータのみが表示されます。

## URLパラメーターの追加 {#defining-additional-settings}

The **[!UICONTROL Parameters]** tab of the [report properties](../../reporting/using/properties-of-the-report.md) lets you define additional settings for the report: these settings will be passed into the URL during the call up.

>[!CAUTION]
>
>セキュリティ上の理由から、これらのパラメーターは慎重に使用する必要があります。

新しい設定を作成するには

1. 「**[!UICONTROL 追加]**」ボタンをクリックし、設定の名前を入力します。

   ![](assets/s_ncs_advuser_report_properties_09a.png)

1. 必要に応じて、設定が必須かどうかを指定します。

1. 作成する設定の種類を選択します。選択できるのは、**[!UICONTROL フィルター]**&#x200B;または&#x200B;**[!UICONTROL 変数]**&#x200B;です。

   「**[!UICONTROL エンティティをフィルター]**」オプションでは、データベースのフィールドをパラメーターとして使用できます。

   ![](assets/s_ncs_advuser_report_properties_09b.png)

   データの復元は、エンティティレベル **ctx/recipient/@account** で直接おこなわれます。

   「**[!UICONTROL 変数]**」オプションでは、変数を作成または選択できます。変数は、URL のパラメーターとして渡されるほか、フィルターで使用することもできます。

**[!UICONTROL 応答 HTTP ヘッダー]**&#x200B;を使用すると、iframe を使用してレポートのページを HTML ページに含める際のクリックジャックを防ぐことができます。クリックジャックを避けるために、**[!UICONTROL X-Frame-options ヘッダー]**&#x200B;の動作を選択できます。

* **[!UICONTROL なし]**：レポートには **[!UICONTROL X-Frame-options ヘッダー]**&#x200B;は含まれません。
* **[!UICONTROL 同じ生成源]**：新しいレポートおよび再パブリッシュされたレポートに対してデフォルトで設定されます。ホスト名は、レポートの URL と同じになります。
* **[!UICONTROL 拒否]**：iframe を使用して HTML ページにレポートを含めることはできません。

![](assets/s_ncs_advuser_report_properties_09c.png)

## 変数の追加 {#adding-variables}

「**[!UICONTROL 変数]**」タブには、レポートに設定されている変数のリストが表示されます。これらの変数は、レポートのコンテキストで公開されており、計算で使用できます。

「**[!UICONTROL 追加]**」ボタンをクリックして、新しい変数を作成します。

変数の定義を表示するには、変数を選択し、「**[!UICONTROL 詳細]**」ボタンをクリックします。

![](assets/s_ncs_advuser_report_properties_10.png)

## 使用例：レポート内での変数とパラメーターの使用

次のビデオの例では、「_type」パラメーターを追加して、この属性の値に基づいて異なる表示のレポートを作成する方法を学びます。

![](assets/do-not-localize/how-to-video.png) [ビデオでこの機能を確認する](https://helpx.adobe.com/campaign/classic/how-to/add-url-parameter-in-acv6.html?playlist=/ccx/v1/collection/product/campaign/classic/segment/business-practitioners/explevel/intermediate/applaunch/how-to-4/collection.ccx.js&amp;ref=helpx.adobe.com)


## 別のレポートの呼び出し {#calling-up-another-report}

A **Jump** activity is like a transition without an arrow: it lets you go from one activity to another or access another report.
