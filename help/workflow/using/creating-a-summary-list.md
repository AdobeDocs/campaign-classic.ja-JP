---
title: サマリーリストの作成
seo-title: サマリーリストの作成
description: サマリーリストの作成
seo-description: null
page-status-flag: never-activated
uuid: ea9d097d-d474-47e6-b0d7-08d587666a55
contentOwner: sauviat
products: SG_CAMPAIGN/CLASSIC
audience: workflow
content-type: reference
topic-tags: use-cases
discoiquuid: 6b0acb6b-0808-4972-b2a2-15fab29b3861
index: y
internal: n
snippet: y
translation-type: tm+mt
source-git-commit: c10a0a11c6e9952aa47da1f7a15188c79c62508d

---


# サマリーリストの作成{#creating-a-summary-list}

この使用例では、ファイルや以下に示すいくつかのエンリッチメントの収集後にサマリーリストを作成できるワークフローについて、作成の手順を詳しく説明します。この例では、店舗で購入をおこなった顧客の連絡先のリストをベースにします。

![](assets/uc2_enrich_overview.png)

次のデータ構造が使用されます。

![](assets/uc2_enrich_data.png)

目的は次のとおりです。

* 「エンリッチメント」アクティビティの様々なオプションを使用する
* 紐付けの後にデータベースのデータを更新する
* エンリッチメントされたデータのグローバル「表示」をおこなう

概要リストを作成するには、次の手順に従う必要があります。

1. 「購入品」ファイルを収集して、ワークフローの作業用テーブルに読み込む
1. 参照テーブルへのリンクを作成して、インポート済みのデータをエンリッチメントする
1. エンリッチメントしたデータで、「購入品」テーブルを更新する
1. 「購入品」テーブルから集計したデータを使用して、「連絡先」データをエンリッチメントする
1. サマリーリストの作成

## Step 1: Loading the file and reconciling the imported data {#step-1--loading-the-file-and-reconciling-the-imported-data}

読み込むデータは、「購入品」に関係する、以下の形式のデータです。

```
Product Name;Product price;Store
Computer;2000;London 3
Tablet;600;Cambridge
Computer;2000;London 5
Comptuer;2000;London 8
Tablet;600;Cambridge
Phone;500;London 5
```

このデータは、「Purchases.txt」ファイルに含まれています。

1. 「**ファイルコレクター**」アクティビティと「**データの読み込み（ファイル）**」アクティビティをワークフローに追加します。

   「**ファイルコレクター**」アクティビティを使用することで、Adobe Campaign サーバーの間で、ファイルの収集、送信をおこなうことができます。

   一方、「**データの読み込み（ファイル）**」アクティビティでは、収集したデータでワークフローの作業用テーブルをエンリッチメントすることが可能です。

   このアクティビティについて詳しくは、「ファイルからのデ [ータの読み込み」を参照してくださ](../../workflow/using/importing-data.md#loading-data-from-a-file)い。

1. 「**ファイルコレクター**」アクティビティを設定し、任意のディレクトリからテキスト（*.txt）タイプのファイルを収集します。

   ![](assets/uc2_enrich_collecteur.png)

   「**ファイルコレクター**」アクティビティを使用すると、ソースディレクトリにファイルの不足がないかを管理することができます。これを行うには、オプションをオンに **[!UICONTROL Process file nonexistence]** します。 このワークフローでは、収集の際にデータがディレクトリから失われている場合に別のファイルを収集するよう、「**待機**」アクティビティを追加しています。

1. インポートするデータと同じ形式のサンプルファイルを利用して、「**データの読み込み（ファイル）**」アクティビティを設定します。

   ![](assets/uc2_enrich_chargement1.png)

   「購入」テ **[!UICONTROL Click here to change the file format...]** ーブルの内部名とラベルを使用して列の名前を変更するには、このリンクをクリックします。

   ![](assets/uc2_enrich_chargement2.png)

データがインポートされたら、「店舗」のスキーマと一致する参照テーブルへのリンクを作成して、エンリッチメントをおこないます。

「エンリッチメント」アクティビティを追加し、次のように設定します。

1. 「**データの読み込み（ファイル）**」アクティビティのデータから構成されるメインセットを選択します。

   ![](assets/uc2_enrich_enrich1.png)

1. をクリック **[!UICONTROL Add data]**&#x200B;し、オプションを選択 **[!UICONTROL A link]** します。

   ![](assets/uc2_enrich_enrich2.png)

1. オプションを選 **[!UICONTROL Define a collection]** 択します。
1. ターゲットとして「店舗」スキーマを選択します。

   ![](assets/uc2_enrich_enrich3.png)

各種リンクの詳細については、『データの強化と変 [更』を参照してください](../../workflow/using/targeting-data.md#enriching-and-modifying-data)。

以下のウィンドウで、（メインセットにある）ソースフィールドと、ターゲットフィールド（「店舗」スキーマに属する）を選択して結合条件を作成し、データの紐付けを設定する必要があります。

![](assets/uc2_enrich_enrich4.png)

リンクが作成できたら、「店舗」スキーマのワークフローの作業用テーブルに「郵便番号の参照」フィールドの列を追加します。

1. 「エンリッチメント」アクティビティを開きます。
1. クリック **[!UICONTROL Edit additional data]**.
1. Add the &quot;ZipCode Reference&quot; field to the **[!UICONTROL Output columns]**.

![](assets/uc2_enrich_enrich5.png)

このエンリッチメントが完了すると、ワークフローの作業用テーブルのデータは次のようになります。

![](assets/uc2_enrich_population1.png)

## Step 2: Writing enriched data to the &#39;Purchases&#39; table {#step-2--writing-enriched-data-to-the--purchases--table}

このステップでは、インポートされエンリッチメントされたデータを「購入品」テーブルに書き込む方法を詳しく説明します。これをおこなうには、「**データを更新**」アクティビティを使用する必要があります。

「**購入品**」テーブルのデータを更新する前に、ワークフローの作業用テーブルのデータと、「**購入品**」のターゲティングディメンションとの間で紐付けをおこなう必要があります。

1. Click the **[!UICONTROL Reconciliation]** tab of the enrichment activity.
1. ターゲティングディメンション、この場合は「購入品」のスキーマを選択します。
1. ワークフローテーブルのデータについて、「ソース式」を選択します。このケースでは、「storeName」フィールドを選択します。
1. 「購入品」テーブルのデータについて、「宛先の式」を選択します。このケースでは、「storename」フィールドを選択します。
1. オプションをオン **[!UICONTROL Keep unreconciled data coming from the work table]** にします。

![](assets/uc2_enrich_reconciliation.png)

「**データを更新**」アクティビティで、以下の設定作業をおこなう必要があります。

1. Select the **[!UICONTROL Insert or update]** option in the **[!UICONTROL Operation type]** field to avoid creating new records each time the file is collected.
1. オプション **[!UICONTROL By directly using the targeting dimension]** の値を選択 **[!UICONTROL Record identification]** します。
1. Select the &quot;Purchases&quot; schema as a **[!UICONTROL Document type]**.
1. 更新するフィールドのリストを指定します。The **[!UICONTROL Destination]** column lets you define the fields of the &quot;Purchases&quot; schema. The **[!UICONTROL Expression]** column lets you select the fields in the work table to carry out a mapping.
1. オプションをクリ **[!UICONTROL Generate an outbound transition]** ックします。

![](assets/uc2_enrich_miseajour.png)

## 手順3:「連絡先」データの強化 {#step-3--enriching--contact--data-}

「連絡先」スキーマは「購入品」スキーマと物理的にリンクします。これは、フィルタリングディメンションにリンクしたデータを追加するという、「エンリッチメント」オプションの別のオプションが利用できることを意味します。

この 2 つ目のエンリッチメントの目的は、「購入品」スキーマの集計をおこない、特定した個々の連絡先について、購入品の総数を計算することにあります。

1. 保存されているすべての&#x200B;**連絡先**&#x200B;を復元する「**クエリ**」タイプアクティビティを追加します。
1. 「**エンリッチメント**」アクティビティを追加し、前のクエリから生成されたメインセットを選択します。
1. Click add **[!UICONTROL Data]**.
1. オプションをクリ **[!UICONTROL Data linked to the targeting dimension]** ックします。
1. ウィンドウのオ **[!UICONTROL Data linked to the filtering dimension]** プションをクリック **[!UICONTROL Select fields to add]** します。
1. ノードを選択し **[!UICONTROL Purchases]** て、をクリックしま **[!UICONTROL Next]**&#x200B;す。

   ![](assets/uc2_enrich_enrich9.png)

1. オプションを選 **[!UICONTROL Collected data]** 択してフィールドを変更 **[!UICONTROL Aggregates]** します。

   ![](assets/uc2_enrich_enrich10.png)

1. クリック **[!UICONTROL Next]**.
1. 次の式を追加して、各連絡先の購入合計を計算します。&quot;Sum(@prodprice)&quot;.

   ![](assets/uc2_enrich_enrich6.png)

サマリーリストを準備するには、「購入品」フィールドのフィールドと、1 番目のエンリッチメントのフィールドである「郵便番号の参照」フィールドを追加する必要があります。

1. 強化アクティビティ **[!UICONTROL Edit additional data...]** のリンクをクリックします。
1. 「店舗名」、「購入品／郵便番号の参照」フィールドを追加します。

   ![](assets/uc2_enrich_enrich7.png)

1. タブをクリック **[!UICONTROL Properties]** します。
1. 1 つの行だけを作成するよう、2 つ目のリンクを変更します。

   ![](assets/uc2_enrich_enrich8.png)

## Step 4: Creating and adding to a summary list {#step-4--creating-and-adding-to-a-summary-list}

最後のステップでは、エンリッチメントしたデータをすべてリストに書き込みます。

1. 「**リスト更新**」アクティビティをワークフローに追加します。このアクティビティは、2 つ目の「エンリッチメント」アクティビティのアウトバウンドトランジションとリンクさせる必要があります。
1. オプションを選 **[!UICONTROL Create the list if necessary (Calculated name)]** 択します。
1. 計算済みの名前の値を選択します。リストに対して選択されたラベルは現在の日付です。&lt;%= formatDate(new Date(), &quot;%2D/%2M/%2Y&quot;) %>。

ワークフローを実行すると、リストには次の情報が含まれるようになります。

* 連絡先のリスト
* 購入品の総数の列
* 「店舗名」の列
* 店舗参照スキーマに含まれるすべての店舗について入力する「郵便番号の参照」列

![](assets/uc2_enrich_listfinal.png)

