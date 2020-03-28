---
title: テーブルの作成
seo-title: テーブルの作成
description: テーブルの作成
seo-description: null
page-status-flag: never-activated
uuid: c5bca799-a5d6-4d98-8fc5-25d7f71be5f7
contentOwner: sauviat
products: SG_CAMPAIGN/CLASSIC
audience: reporting
content-type: reference
topic-tags: creating-new-reports
discoiquuid: 74084618-2b35-42c5-8a86-87ce137abb71
index: y
internal: n
snippet: y
translation-type: ht
source-git-commit: 209ac4d81d2d27c264ee6b288bcb7fcb1900ffc5

---


# テーブルの作成{#creating-a-table}

レポートにテーブルを追加して、データを表示できます。追加できるテーブルには、キューブの測定に基づいて作成されたピボットテーブル、グループ化されたリスト、値の分類を含むテーブルがあります。

![](assets/s_advuser_report_page_activity_05.png)

## グループ化されたリストの作成 {#creating-a-list-with-group}

**[!UICONTROL グループ化されたリスト]**&#x200B;タイプのテーブルでは、テーブルのデータをグループ化し、それに関する統計を生成できます。例えば、データの合計と小計を作成できます。グループごとに、専用のヘッダー行、詳細行、フッター行があります。

>[!CAUTION]
>
>テーブルを含む&#x200B;**[!UICONTROL ページ]**&#x200B;アクティビティの前に、レポートで分析するデータを収集するための&#x200B;**[!UICONTROL クエリ]**&#x200B;または&#x200B;**[!UICONTROL スクリプト]**&#x200B;アクティビティが必要です。これらのアクティビティについて詳しくは、[分析するデータの収集](../../reporting/using/collecting-data-to-analyze.md)および[スクリプトアクティビティ](../../reporting/using/advanced-functionalities.md#script-activity)を参照してください。

### 動作の仕組み {#operating-principle}

複数のデータカテゴリを一度に分析しなければならないことがあります。グループ化されたリストでは、データを組み合わせて、同じテーブル内のデータの様々なグループに関する統計を作成できます。それには、テーブルにグループを作成します。

次の例では、グループは、データベース内のすべてのキャンペーン、配信、および配信ごと／キャンペーンごとに送信されたメッセージ数を表示します。

キャンペーン（**[!UICONTROL ラベル (キャンペーン)]**）、キャンペーンにリンクされた配信（**[!UICONTROL ラベル]**）のリスト、配信ごとに送信されたメッセージの数（**[!UICONTROL 処理済み]**）、それらをキャンペーンごとに合計した総数（**[!UICONTROL Sum(@processed)]**）を一覧表示できます。

![](assets/s_advuser_ergo_listgroup_005.png)

### 実装の手順 {#implementation-steps}

完全な実装例は、[使用例：グループリストを含むレポートの作成](#use-case--create-a-report-with-a-group-list)で説明しています。

「グループ化されたリスト」タイプのテーブルを作成するには、次の手順に従ってください。

1. レポートのチャートに移動し、**[!UICONTROL クエリ]**&#x200B;アクティビティを追加します。[分析するデータの収集](../../reporting/using/collecting-data-to-analyze.md)を参照してください。
1. ソーステーブルを入力し、そのテーブルのフィールドのうち、統計に関係するものを選択します。
1. フローチャートに&#x200B;**[!UICONTROL ページ]**&#x200B;アクティビティを追加します。詳しくは、[静的要素](../../reporting/using/creating-a-new-report.md#static-elements)を参照してください。
1. ページに&#x200B;**[!UICONTROL グループ化されたリスト]**&#x200B;タイプのテーブルを挿入します。
1. データパス、またはクエリでデータソースとして選択されたテーブルを指定します。

   後でソーステーブルのフィールドを復元し、それらをテーブルのセルに挿入する場合、この手順は必須です。

1. テーブルとその内容を作成します。
1. 最終決定したレポートを「**[!UICONTROL プレビュー]**」タブに表示します。その後は、レポートをパブリッシュしたり、必要に応じてレポートを別のフォーマットにエクスポートしたりできます。詳しくは、[レポートのエクスポート](../../reporting/using/actions-on-reports.md#exporting-a-report)を参照してください。

### 行や列の追加 {#adding-lines-and-columns}

デフォルトでは、**[!UICONTROL グループ化されたリスト]**&#x200B;タイプのテーブルには、ヘッダー行、詳細行、フッター行が含まれています。

グループ自体に、ヘッダー行、詳細行、フッター行が含まれています。

* **ヘッダー行**：この行にはテーブルの列のタイトルを入力できます。

   ![](assets/s_advuser_ergo_listgroup_003a.png)

* **詳細行**：この行には統計値が含まれます。

   ![](assets/s_advuser_ergo_listgroup_004.png)

* **フッター行**：この行には合計値を表示できます。

   ![](assets/s_advuser_ergo_listgroup_003.png)

必要に応じて、行や列を追加できます。

グループは、テーブルの任意の行に配置でき、独自のヘッダー行、詳細行、フッター行を含みます。

![](assets/s_advuser_ergo_listgroup_019.png)

**行や列**：行や列を追加または削除するには、既存の行や列に移動し、右クリックメニューを使用します。

![](assets/s_advuser_ergo_listgroup_006.png)

追加する行の特性は、カーソルの位置によって決まります。例えば、ヘッダー行を追加するには、ヘッダーにカーソルを置き、**[!UICONTROL 追加／上に 1 行（または下に 1 行）]**&#x200B;を選択します。

![](assets/s_advuser_ergo_listgroup_006a.png)

列の幅は&#x200B;**[!UICONTROL 列のフォーマット]**&#x200B;項目で変更できます。

**グループ**：グループを追加するには、対象となる行に移動し、ドロップダウンメニューから該当する項目を選択します。

![](assets/s_advuser_ergo_listgroup_007.png)

### セルの内容の定義 {#defining-cell-content}

テーブルのセルを編集してセルの内容とフォーマットを定義するには、対象となるセルに移動し、右クリックメニューを使用します。

**[!UICONTROL 式]**&#x200B;メニューエントリを使用すると、表示する値を選択できます。

![](assets/s_advuser_ergo_listgroup_010.png)

* 分析する値をテーブルに直接挿入する場合は、使用可能なフィールドの中から該当するものを選択します。

   使用可能なフィールドのリストは、レポート作成チャートでテーブル作成の前に定義するクエリの内容に一致します。

   ![](assets/s_advuser_ergo_listgroup_011.png)

* セル（例えばヘッダーセル）のラベルを入力します。

   それには、データベースにフィールドを挿入する場合と同様の手順に従いますが、式は選択しません。「**[!UICONTROL ラベル]**」フィールドにラベルを入力します。それがそのまま表示されます。

* 集計（平均や合計など）を計算し、それをセルに表示します。

   それには、**[!UICONTROL 集計]**&#x200B;メニューエントリを使用し、目的とするキャンペーンを選択します。

   ![](assets/s_advuser_ergo_listgroup_008.png)

### セルのフォーマットの定義 {#defining-cell-format}

![](assets/s_advuser_ergo_listgroup_017.png)

セルのフォーマットを定義する場合は、**[!UICONTROL セルのフォーマット...]** メニューを使用して、選択したセルに使用できるすべての書式設定オプションにアクセスできます。

これらのオプションを使用すると、レポートの最終的なレンダリングをパーソナライズし、情報を読み取りやすくすることができます。

データを Excel にエクスポートする場合は、「**[!UICONTROL CR]**」フィールドを使用します。「**[!UICONTROL はい]**」の値を選択すると、強制的に復帰改行されます。この値はエクスポート時に保持されます。詳しくは、[レポートのエクスポート](../../reporting/using/actions-on-reports.md#exporting-a-report)を参照してください。

**[!UICONTROL セルのフォーマット]**&#x200B;ウィンドウでは、次のタブにアクセスできます。

* 「**[!UICONTROL 値]**」タブ
* 「**[!UICONTROL 境界線]**」タブ
* 「**[!UICONTROL クリック]**」タブ
* 「**[!UICONTROL 追加]**」タブ

「**[!UICONTROL 値]**」タブでは、フォントおよび様々な値属性を変更したり、値の性質に基づいてフォーマットを定義したりできます。

![](assets/s_advuser_ergo_listgroup_009.png)

フォーマットによってデータの表示が変わります。例えば、「**[!UICONTROL 数]**」、「**[!UICONTROL 通貨]**」、「**[!UICONTROL 割合]**」の各フォーマットを使用すると、数字を右詰めにして小数点を表示できます。

通貨フォーマットの設定方法の例：値の表示に使用される通貨を指定し、3 桁区切り記号を使用するかどうかを選択し、負の値を赤で表示できます。通貨記号の位置は、オペレーターのプロファイルに定義されている言語に依存します。

![](assets/s_advuser_ergo_listgroup_012.png)

日付の設定例：時刻を表示するかどうかを選択できます。

![](assets/s_advuser_ergo_listgroup_013.png)

「**境界線**」タブでは、テーブルの行や列に境界線を追加できます。セルに境界線を追加すると、サイズの大きいレポートを Excel にエクスポートする際に、パフォーマンス上の問題が発生する可能性があります。

![](assets/s_advuser_ergo_listgroup_014.png)

必要に応じて、テーブルテンプレート（**[!UICONTROL 管理／設定／フォームのレンダリング]**）で境界線を定義できます。

その場合、使用する構文は次のようになります。

「Web」タブで使用する構文

```
 .tabular td {
 border: solid 1px #000000;
 }
```

「Excel」タブで使用する構文

```
 <style name="odd" fillColor="#fdfdfd">
  <border>
   <borderTop value="solid 0.05pt #000000" />
   <borderBottom value="solid 0.05pt #000000" />
   <borderLeft value="solid 0.05pt #000000" />
   <borderRight value="solid 0.05pt #000000" />
  </border>
 </style> 
 
 <style name="even" fillColor="#f7f8fa">
  <border>
   <borderTop value="solid 0.05pt #000000" />
   <borderBottom value="solid 0.05pt #000000" />
   <borderLeft value="solid 0.05pt #000000" />
   <borderRight value="solid 0.05pt #000000" />
  </border>
 </style> 
```

「**[!UICONTROL クリック]**」タブでは、ユーザーがセルやテーブルの内容をクリックしたときに実行されるアクションを定義できます。

次の例では、セルの値をクリックするとレポートの 2 番目のページが表示されるようになります。配信時の情報がセルに格納されます。

![](assets/s_advuser_ergo_listgroup_015.png)

「**追加**」タブでは、色付きマークや棒グラフなどのビジュアルをデータにリンクできます。色付きのマークは、テーブルが凡例としてグラフに表示される場合に使用されます。詳しくは、[手順 5 - 2 番目のページの作成](#step-5---create-the-second-page)の実装例を参照してください。

![](assets/s_advuser_ergo_listgroup_016.png)

## 使用例：グループリストを含むレポートの作成 {#use-case--create-a-report-with-a-group-list}

この例では、2 ページから成るレポートを作成します。最初のページには、キャンペーンのリストとキャンペーンごとの合計配信数のほか、送信されたメッセージの数が表示されます。配信名はクリック可能なリンクになっており、それをクリックすると、レポートの 2 番目のページに移動し、テーブルやグラフで選択した配信の E メールドメインごとの配信の分類が表示されます。2 番目のページでは、テーブルはグラフの凡例になります。

![](assets/reporting_quick_start_report-final.png)

### 手順 1 - レポートの作成 {#step-1---create-a-report}

キャンペーンスキーマに関する新しいレポート、「**[!UICONTROL キャンペーン (nms)]**」を作成します。

![](assets/s_advuser_report_listgroup_001.png)

「**[!UICONTROL 保存]**」ボタンをクリックして、レポートを作成します。

チャートに移動し、レポートのコンテンツを設計するための最初のコンポーネント、つまり、最初のクエリと最初のページを追加します。

![](assets/reporting_quick_start_diagram.png)

### 手順 2 - 最初のクエリの作成 {#step-2---create-the-first-query}

最初のクエリでは、各キャンペーンにリンクされている配信を収集します。目標は、Adobe Campaign データベースの様々な配信のうち、各キャンペーンにリンクされている配信に関するレポートを表示することです。

最初のクエリをダブルクリックして編集してから、次の手順に従ってクエリを設定します。

1. 最初に、クエリのソースのスキーマを変更します。「**[!UICONTROL 配信 (nms)]**」スキーマを選択します。
1. 「**[!UICONTROL クエリを編集]**」リンクをクリックして、詳細フィールドを表示します。

   ![](assets/reporting_quick_start_query-1.png)

1. 次のフィールドを選択します。

   * 配信ラベル
   * 配信のプライマリキー
   * キャンペーンラベル
   * 処理された配信の指標
   * 「キャンペーン」リンクの外部キー
   * エラー率指標
   ![](assets/s_advuser_report_listgroup_002.png)

   各フィールドにエイリアスをリンクします。これにより、レポートの最初のページに追加されるテーブルからデータを選択しやすくなるので、お勧めします。

   この例の場合は、次のエイリアスを使用します。

   * ラベル：**@label**
   * プライマリキー：**@deliveryId**
   * ラベル（キャンペーン）：**@label1**
   * 処理済み：**@processed**
   * 「キャンペーン」リンク (&#39;id&#39; フィールド) の外部キー：**@operationId**
   * エラー率：**@errorRatio**


1. 「**[!UICONTROL 次へ]**」ボタンを 2 回クリックして、**[!UICONTROL データのフィルター]**&#x200B;手順に移動します。

   キャンペーンにリンクされた配信のみを収集するためのフィルター条件を追加します。

   このフィルターの構文は「&quot;キャンペーン&quot; リンクの外部キーが 0 より大きい」です。

   ![](assets/reporting_quick_start_query_filter.png)

1. 「**[!UICONTROL 完了]**」をクリックしてこれらの条件を保存した後、「**[!UICONTROL OK]**」をクリックしてクエリエディターを閉じます。

### 手順 3：最初のページの作成 {#step-3--create-the-first-page}

この手順では、レポートの最初のページを設定します。設定するには、次の手順に従います。

1. **[!UICONTROL ページ]**&#x200B;アクティビティを開き、そのタイトルを、例えばこの場合は &quot;**Deliveries**&quot; と入力します。

   ![](assets/s_advuser_report_listgroup_003.png)

1. ツールバーからグループ化されたリストを挿入し、そのラベルを入力します。例：キャンペーンごとの配信のリスト。

   ![](assets/s_advuser_report_listgroup_004.png)

1. 「**[!UICONTROL テーブルデータ Xpath...]**」リンクをクリックし、`[query/delivery]` のような配信リンクを選択します。

   ![](assets/s_advuser_report_listgroup_005.png)

1. 「**[!UICONTROL データ]**」タブをクリックし、テーブルのレイアウトを変更します。右側に 3 列を追加します。

   ![](assets/s_advuser_report_listgroup_006.png)

1. グループを追加します。

   ![](assets/s_advuser_report_listgroup_008.png)

   このグループによって、キャンペーンとそのキャンペーンにリンクされている配信をグループ化できるようになります。

1. グループウィンドウで&#x200B;**「キャンペーン」リンク (「id」フィールド) の外部キー**&#x200B;を参照し、ウィンドウを閉じます。

   ![](assets/s_advuser_report_listgroup_007.png)

1. グループヘッダーの最初のセルを編集し、式としてキャンペーンの&#x200B;**[!UICONTROL ラベル]**&#x200B;フィールドを挿入します。

   ![](assets/s_advuser_report_listgroup_009.png)

1. 詳細行の 2 番目のセルを編集し、配信の&#x200B;**[!UICONTROL ラベル]**&#x200B;を選択します。

   ![](assets/s_advuser_report_listgroup_011.png)

1. このセルのフォーマットを編集し、「**[!UICONTROL クリック]**」タブを開きます。ユーザーが配信の名前をクリックしたときにその配信が同じウィンドウに開くように、適切なオプションを設定します。

   ![](assets/s_advuser_report_listgroup_0111.png)

   それには、**[!UICONTROL 次のページ]**&#x200B;タイプのアクションを選択し、「**[!UICONTROL 同じウィンドウで]**」をウィンドウオプションとして選択します。

   ![](assets/s_advuser_report_listgroup_0112.png)

1. ウィンドウ下部の「**[!UICONTROL 追加]**」をクリックし、先に作成したクエリで定義したとおり、**`/vars/selectedDelivery`**&#x200B;パスおよび配信のプライマリキーのエイリアスに一致する **[!UICONTROL @deliveryId]** の式を指定します。この式を使用すると、選択した配信にアクセスできます。

   ![](assets/s_advuser_report_listgroup_010.png)

1. グループのフッター行の 2 番目のセルを編集し、ラベルとして &quot;**[!UICONTROL Total per Campaign]**&quot; を入力します。

   ![](assets/s_advuser_report_listgroup_012.png)

1. グループのヘッダー行の 3 番目のセルを編集し、ラベルとして &quot;**[!UICONTROL Number of messages sent]**&quot; を入力します。

   ![](assets/s_advuser_report_listgroup_013.png)

   この情報は列タイトルと一致します。

1. 詳細行の 3 番目のセルを編集し、処理されたメッセージの指標を式として選択します。

   ![](assets/s_advuser_report_listgroup_014.png)

1. グループのフッター行の 3 番目のセルを編集して、処理された配信の指標を選択し、それに対して&#x200B;**[!UICONTROL 合計]**&#x200B;の集計を適用します。

   ![](assets/s_advuser_report_listgroup_015.png)

1. 詳細行の 4 番目のセルを編集し、式として「**配信のエラー率 (@errorRatio)**」を選択します。

   ![](assets/s_advuser_report_listgroup_016.png)

1. このセルを選択して、配信のエラー率を表す棒グラフを表示するように設定します。

   それには、セルのフォーマットにアクセスし、「**[!UICONTROL 追加]**」タブを開きます。ドロップダウンリストの&#x200B;**[!UICONTROL 棒グラフ]**&#x200B;を選択し、「**[!UICONTROL セル値を非表示]**」オプションを選択します。

   ![](assets/s_advuser_report_listgroup_023.png)

   これでレポートのレンダリングを表示できます。「**[!UICONTROL プレビュー]**」タブをクリックし、「**[!UICONTROL グローバル]**」オプションを選択します。これで、キャンペーンにリンクされている Adobe Campaign データベースのすべての配信のリストが表示されます。

   ![](assets/s_advuser_report_listgroup_025.png)

   「**[!UICONTROL プレビュー]**」タブを使用して、テーブル内のデータが正しく選択および設定されていることを確認することをお勧めします。それが済めば、テーブルの書式設定に進むことができます。

1. キャンペーンごとの合計配信数と処理されたメッセージの総数を表示するセルに&#x200B;**[!UICONTROL 太字]**&#x200B;スタイルを適用します。

   ![](assets/s_advuser_report_listgroup_024.png)

1. グループのヘッダー行の最初のセル（キャンペーン名を表示するセル）をクリックし、**[!UICONTROL 編集／右に結合]**&#x200B;を選択します。

   ![](assets/s_advuser_report_listgroup_026.png)

   グループのヘッダー行の最初の 2 つのセルを結合すると、キャンペーンのタイトルと、キャンペーンにリンクされている配信のリストが整列し直されます。

   ![](assets/s_advuser_report_listgroup_027.png)

   >[!CAUTION]
   >
   >セルを結合するのはレポートが作成されてからにすることをお勧めします。結合は元に戻せないからです。

### 手順 4 - 2 番目のクエリの作成 {#step-4---create-the-second-query}

レポートのユーザーが配信をクリックしたきにその配信の詳細が表示されるように、2 番目のクエリと 2 番目のページを追加します。クエリを追加する前に、作成したページを編集し、クエリにリンクできるように出力トランジションを有効にします。

1. **[!UICONTROL ページ]**&#x200B;アクティビティの後に新しいクエリを追加し、そのクエリのスキーマを編集して&#x200B;**[!UICONTROL 受信者配信ログ]**&#x200B;スキーマを選択します。

   ![](assets/reporting_quick_start_query-2.png)

1. クエリを編集し、出力列を定義します。E メールドメインごとの配信数を表示するには、次の作業が必要です。

   * プライマリキーの合計を計算して、配信ログの数をカウントします。

      ![](assets/reporting_quick_start_query-2_count.png)

   * 受信者の E メールドメインを収集し、このフィールドに関する情報をグループ化します。それには、出力列で「**[!UICONTROL グループ]**」オプションを選択します。
   ![](assets/reporting_quick_start_query-2_filter.png)

   フィールドに次のエイリアスをリンクします。

   * カウント（プライマリキー）：**@count**
   * E メールドメイン（受信者）：**@domain**

      ![](assets/reporting_quick_start_query-2_alias.png)


1. 「**[!UICONTROL 次へ]**」ボタンを 2 回クリックします。これで、**[!UICONTROL データのフィルター]**&#x200B;の手順に移動します。

   選択した配信にリンクされている情報のみを収集するフィルター条件を追加します。

   構文は「&quot;配信&quot; リンクの外部キーが設定の値と等しい」です。 `$([vars/selectedDelivery])`

   ![](assets/s_advuser_report_listgroup_017.png)

1. クエリ設定ウィンドウを閉じ、チャートに（2 番目のクエリの直後に）ページアクティビティを追加します。

### 手順 5 - 2 番目のページの作成 {#step-5---create-the-second-page}

1. ページを編集し、そのラベルを「**E メールドメイン**」と入力します。
1. 「**[!UICONTROL アウトバウンドトランジションを有効にする]**」オプションのチェックをオフにします。これがレポートの最後のページであり、この後に別のアクティビティが続くことはありません。

   ![](assets/s_advuser_report_listgroup_028.png)

1. 右クリックメニューを使用して、グループ化されたリストを新しく追加し、名前を &quot;**Email domain per recipient**&quot; とします。
1. 「**[!UICONTROL テーブルデータ Xpath]**」をクリックし、「**[!UICONTROL 受信者配信ログ]**」リンクを選択します。

   ![](assets/s_advuser_report_listgroup_029.png)

1. 「**[!UICONTROL データ]**」タブで、テーブルを次のように調整します。

   * 右側に 2 列を追加します。
   * 詳細行の最初のセルに、行数をカウントする式 **[!UICONTROL rowNum()-1]** を追加します。その次に、セルのフォーマットを変更します。「**[!UICONTROL 追加]**」タブで、「**[!UICONTROL 「カラー」タブ]**」を選択し、「**[!UICONTROL OK]**」をクリックします。

      ![](assets/s_advuser_report_listgroup_018.png)

      この設定によって、テーブルをグラフのキャプションとして使用できるようになります。

   * 詳細行の 2 番目のセルに、式 **[!UICONTROL Email domain(Recipient)]** を追加します。
   * 詳細行の 3 番目のセルに、式 **[!UICONTROL count(primary key)]** を追加します。
   ![](assets/s_advuser_report_listgroup_019.png)

1. 右クリックメニューを使用してページに円グラフを追加し、そのラベルを &quot;**Email domains**&quot; にします。詳しくは、[グラフのタイプとバリエーション](../../reporting/using/creating-a-chart.md#chart-types-and-variants)を参照してください。
1. 「**[!UICONTROL バリエーション]**」リンクをクリックし、「**[!UICONTROL ラベルを表示]**」オプションと「**[!UICONTROL キャプションを表示]**」オプションの選択を解除します。
1. 値の並べ替えが設定されていないことを確認します。詳しくは、[この節](../../reporting/using/processing-a-report.md#configuring-the-layout-of-a-descriptive-analysis-report)を参照してください。

   ![](assets/s_advuser_report_listgroup_0191.png)

1. 「**[!UICONTROL データ]**」タブで、データソースを変更します。それには、ドロップダウンリストから「**[!UICONTROL コンテキストデータ]**」を選択します。

   ![](assets/s_advuser_report_listgroup_020.png)

1. 次に、「**[!UICONTROL 詳細設定パラメーター]**」をクリックし、受信者配信ログへのリンクを選択します。

   ![](assets/s_advuser_report_listgroup_0201.png)

1. 「**[!UICONTROL グラフタイプ]**」セクションで、**[!UICONTROL E メールドメイン]**&#x200B;変数を選択します。
1. 次に、実行する計算を追加します。合計を演算子として選択します。

   ![](assets/s_advuser_report_listgroup_0202.png)

1. 「**[!UICONTROL 詳細]**」ボタンをクリックして、カウントに関係するフィールドを選択した後、設定ウィンドウを閉じます。

   ![](assets/s_advuser_report_listgroup_030.png)

1. レポートを保存します。

   これで、ページが設定されました。

### 手順 6 - レポートの表示 {#step-6---viewing-the-report}

この設定の結果を表示するには、「**[!UICONTROL プレビュー]**」タブをクリックし、「**[!UICONTROL グローバル]**」オプションを選択します。

レポートの最初のページに、データベースに含まれるすべての配信のリストが詳しく表示されます。

![](assets/s_advuser_report_listgroup_021.png)

これらの配信のいずれかを選択し、そのリンクをクリックすると、その配信の E メールドメインの分類を示すグラフが表示されます。それがレポートの 2 番目のページで、適切なボタンをクリックすることで前のページに戻ることができます。

![](assets/s_advuser_report_listgroup_022.png)

## 分類またはピボットテーブルの作成 {#creating-a-breakdown-or-pivot-table}

このタイプのテーブルでは、データベース内のデータに関して計算した統計を表示できます。

これらのタイプのレポートの設定は、記述的分析ウィザードの場合と似ています。詳しくは、[このページ](../../reporting/using/using-the-descriptive-analysis-wizard.md#configuring-the-quantitative-distribution-template)を参照してください。

ピボットテーブルの作成について詳しくは、[この節](../../reporting/using/using-cubes-to-explore-data.md)を参照してください。
