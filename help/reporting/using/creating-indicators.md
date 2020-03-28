---
title: 指標の作成
seo-title: 指標の作成
description: 指標の作成
seo-description: null
page-status-flag: never-activated
uuid: 3caaba6b-b6c8-4b64-b123-d7098e9ddc7a
contentOwner: sauviat
products: SG_CAMPAIGN/CLASSIC
audience: reporting
content-type: reference
topic-tags: designing-reports-with-cubes
discoiquuid: a5fc6c78-b4fb-41fd-a072-7be4ece3c554
index: y
internal: n
snippet: y
translation-type: ht
source-git-commit: 209ac4d81d2d27c264ee6b288bcb7fcb1900ffc5

---


# 指標の作成{#creating-indicators}

キューブを機能させるには、関係のあるディメンションと測定を特定し、キューブにそれらを作成する必要があります。

キューブを作成するには、次の手順に従います。

1. 作業用テーブルを選択します。[作業用テーブルの選択](#selecting-the-work-table)を参照してください。
1. ディメンションを定義します。[ディメンションの定義](#defining-dimensions)を参照してください。
1. 測定を定義します。[指標の構築](#building-indicators)を参照してください。
1. 集計を作成します（オプション）。[集計の計算と使用](../../reporting/using/concepts-and-methodology.md#calculating-and-using-aggregates)を参照してください。

この例では、レポートにシンプルなキューブをすばやく作成して、そのキューブの測定をエクスポートする方法を示します。

次に、実装手順を示します。すべてのオプションとその説明については、この章の他の節を参照してください。

## 作業用テーブルの選択 {#selecting-the-work-table}

キューブを作成するには、キューブのリストの上にある「**[!UICONTROL 新規]**」ボタンをクリックします。

![](assets/s_advuser_cube_create.png)

ファクトスキーマ（調査の対象となる要素が含まれているスキーマ）を選択します。この例では、**受信者**&#x200B;テーブルを選択します。

![](assets/s_advuser_cube_wz_02.png)

「**[!UICONTROL 保存]**」をクリックして、キューブを作成します。そのキューブはキューブのリストに表示され、その後、適切なタブを使用して設定できます。

「**[!UICONTROL ソースデータをフィルター]**」リンクをクリックして、データベースから選択した一部のデータに、このキューブの計算を適用します。

![](assets/s_advuser_cube_wz_03.png)

## ディメンションの定義 {#defining-dimensions}

ディメンションは、関連するファクトスキーマに基づいたキューブごとに定義された分析軸と一致します。これらが、分析で調査されるディメンションです。例えば、時間（年、月、日など）、製品や契約の分類（ファミリー、参照など）、母集団のセグメント（市区町村別、年齢別、グループ別、ステータス別など）といったものです。

これらの分析軸は、キューブの「**[!UICONTROL ディメンション]**」タブで定義します。

「**[!UICONTROL 追加]**」ボタンをクリックして新しいディメンションを作成した後、「**[!UICONTROL 式]**」フィールドで「**[!UICONTROL 式を編集]**」アイコンをクリックして、該当するデータを格納したフィールドを選択します。

![](assets/s_advuser_cube_wz_04.png)

* まず最初に、受信者の&#x200B;**年齢**&#x200B;を選択します。このフィールドに対して、ビニングを定義して年齢をグループ化し、情報を読み取りやすくすることができます。いくつかの独立した値を扱う可能性がある場合は、ビニングを使用することをお勧めします。

   それには、「**[!UICONTROL ビニングを有効にする]**」オプションにチェックを入れます。ビニングモードについて詳しくは、[データビニング](../../reporting/using/concepts-and-methodology.md#data-binning)を参照してください。

   ![](assets/s_advuser_cube_wz_05.png)

* **日付**&#x200B;タイプのディメンションを追加します。ここでは、受信者プロファイルの作成日を表示します。

   それには、「**[!UICONTROL 追加]**」をクリックし、受信者テーブルの&#x200B;**[!UICONTROL 作成日]**&#x200B;フィールドを選択します。

   ![](assets/s_advuser_cube_wz_06.png)

   日付表示モードを選択できます。それには、使用する階層と生成するレベルを選択します。

   ![](assets/s_advuser_cube_wz_07.png)

   この例では、年、月および日のみを表示します。これは、週と学期／月を同時に扱うことができないためです。これらのレベルの間には互換性がありません。

* 別のディメンションを作成して、受信者の市区町村に関連するデータを分析します。

   それには、新しいディメンションを追加し、受信者スキーマの&#x200B;**[!UICONTROL 場所]**&#x200B;ノードに属している「市区町村」を選択します。

   ![](assets/s_advuser_cube_wz_08.png)

   ビニングを有効にして情報を読み取りやすくし、値を列挙にリンクします。

   ![](assets/s_advuser_cube_wz_09.png)

   ドロップダウンリストから列挙を選択します。

   ![](assets/s_advuser_cube_wz_10.png)

   その列挙の値のみ表示されます。それ以外は、「**[!UICONTROL 他の値のラベル]**」フィールドで定義したラベルの下にグループ化されます。

   詳しくは、[bin の動的管理](../../reporting/using/concepts-and-methodology.md#dynamically-managing-bins)を参照してください。

## 指標の構築 {#building-indicators}

ディメンションを定義したら、セルに表示する値の計算モードを指定する必要があります。それには、対応する指標を「**[!UICONTROL 測定]**」タブで作成します。キューブを使用するレポートに表示する列と同じ数の測定を作成します。

それには、次の手順に従います。

1. 「**[!UICONTROL 追加]**」ボタンをクリックします。
1. 測定のタイプと適用する式を選択します。ここでは、女性の受信者の数をカウントします。

   この場合の測定はファクトスキーマに基づいたもので、使用する演算子は&#x200B;**[!UICONTROL カウント]**&#x200B;です。

   ![](assets/s_advuser_cube_wz_11.png)

   「**[!UICONTROL 測定データをフィルター]**」リンクをたどって、女性だけを選択できます。測定と使用可能なオプションの定義について詳しくは、[測定の定義](../../reporting/using/concepts-and-methodology.md#defining-measures)を参照してください。

   ![](assets/s_advuser_cube_wz_12.png)

1. 測定のラベルを入力し、測定を保存します。

   ![](assets/s_advuser_cube_wz_13.png)

1. キューブを保存します。

## キューブに基づくレポートの作成 {#creating-a-report-based-on-a-cube}

キューブを設定したら、新しいレポートを作成するためのテンプレートとして使用できます。

手順は次のとおりです。

1. **[!UICONTROL レポート]**&#x200B;ウィンドウの「**[!UICONTROL 作成]**」ボタンをクリックし、先ほど作成したキューブを選択します。

   ![](assets/s_advuser_cube_wz_14.png)

1. 「**[!UICONTROL 作成]**」ボタンをクリックして確定します。これにより、レポート設定および表示ページが開きます。

   デフォルトでは、使用可能な最初の 2 つのディメンションは行と列で提供されますが、値はテーブルには表示されません。テーブルを生成するには、メインアイコンをクリックします。

   ![](assets/s_advuser_cube_wz_15.png)

1. ディメンションの軸を切り替えたり、軸を削除したり、新しい測定を追加したりできます。可能な操作について詳しくは、[キューブを使用したデータ調査](../../reporting/using/using-cubes-to-explore-data.md)を参照してください。

   それには、該当するアイコンを使用します。

   ![](assets/s_advuser_cube_wz_16.png)

