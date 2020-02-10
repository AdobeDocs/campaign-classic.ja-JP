---
title: データのインポート
description: Adobe Campaign Classicでデータをインポートする方法を説明します。
page-status-flag: never-activated
uuid: c8cf2bf1-f7a5-4de4-9e53-a961c9e5beca
contentOwner: sauviat
products: SG_CAMPAIGN/CLASSIC
audience: workflow
content-type: reference
topic-tags: -general-operation
discoiquuid: e53af1c2-b50c-4a8c-b5b8-f23a85bd3211
index: y
internal: n
snippet: y
translation-type: tm+mt
source-git-commit: 2e16d4de068f8cb1e61069aa53626f7bf7021466

---


# データのインポート{#importing-data}

## データの収集方法 {#how-to-collect-data}

### リストのデータの使用：読み取りリスト {#using-data-from-a-list--read-list}

ワークフローに送られるデータを、事前にデータが準備され、構造化されているリストから取り出すこともできます。

This list may have been directly created in Adobe Campaign or imported by the **[!UICONTROL Import a list]** option. このオプションについて詳しくは、この[ページ](../../platform/using/generic-imports-and-exports.md)を参照してください。

For more on using the read list activity in a workflow, refer to [Read list](../../workflow/using/read-list.md).

### ファイルからのデータの読み込み {#loading-data-from-a-file}

ワークフロー内で処理されるデータは、Adobe Campaign にインポートできるように、構造化ファイルから抽出することができます。

A description of the loading data activity can be found in the [Data loading (file)](../../workflow/using/data-loading--file-.md) section.

インポートする構造化ファイルの例：

```
lastname;firstname;birthdate;email;crmID
Smith;Hayden;23/05/1989;hayden.smith@example.com;124365
Mars;Daniel;17/11/1987;dannymars@example.com;123545
Smith;Clara;08/02/1989;hayden.smith@example.com;124567
Durance;Allison;15/12/1978;allison.durance@example.com;120987
```

### 処理前のファイルの解凍または復号化 {#unzipping-or-decrypting-a-file-before-processing}

Adobe Campaign では、圧縮されたファイルや暗号化されたファイルをインポートできます。Before they can be read in a **[!UICONTROL Data loading (file)]** activity, you can define a pre-processing to unzip or to decrypt the file.

手順は以下のとおりです。

* インストールした Adobe Campaign がアドビによってホストされている場合：必要なユーティリティをサーバーにインストールするよう[サポート](https://support.neolane.net)に依頼します。
* Adobe Campaignのインストールがオンプレミスの場合：使用するユーティリティをインストールします(例：GPG、GZIP)と、アプリケーションサーバー上の必要なキー（暗号化キー）。

1. Add and configure a **[!UICONTROL File transfer]** activity in your workflow.
1. アクティビティ **[!UICONTROL Data loading (file)]** を追加し、ファイル形式を定義します。
1. オプションをオン **[!UICONTROL Pre-process the file]** にします。
1. 適用する前処理コマンドを指定します。以下に PGP でファイルを復号化する場合の例を示します。

   ```
   <path-to_pgp_if-not_global_or_server/>pgp.exe --decrypt --input nl6/var/vp/import/filename.pgp --passphrase "your password" --recipient recipient @email.com --verbose --output nl6/var/vp/import/filename
   ```

1. ファイルから取得したデータを管理するために必要なその他のアクティビティを追加します。
1. 保存して、ワークフローを実行します。

ファイルのエクスポート時には、ファイルを圧縮または暗号化することもできます。See [Zipping or encrypting a file](../../workflow/using/how-to-use-workflow-data.md#zipping-or-encrypting-a-file).

## データをインポートする際のベストプラクティス {#best-practices-when-importing-data}

次に説明するいくつかのシンプルなルールに注意して従うと、データベース内のデータの一貫性を確保し、データベースの更新中またはデータを読み込む際の一般的なエラーを避けるのに非常に役立ちます。

### インポートテンプレートの使用 {#using-import-templates}

Most import workflows should contain the following activities: **[!UICONTROL Data loading (file)]**, **[!UICONTROL Enrichment]**, **[!UICONTROL Split]**, **[!UICONTROL Deduplication]**, **[!UICONTROL Update data]**.

インポートテンプレートを使用すると、同様のインポートを準備したり、データベース内のデータの一貫性を確保したりするのに非常に便利です。Learn how to build workflow templates in the [Workflow templates](../../workflow/using/building-a-workflow.md#workflow-templates) section.

In many projects, imports are built without **[!UICONTROL Deduplication]** activity because the files used in the project do not have duplicates. 複数のファイルをインポートすると、重複が発生する場合があります。そうなると、重複排除は困難になります。そのため、すべてのインポートワークフローで重複排除ステップを設けることは、優れた予防措置となります。

受信データは一貫性があり正しいとか、IT 部門や Adobe Campaign スーパーバイザーが対処するとは思わないでください。プロジェクトの間、データクレンジングに留意してください。データをインポートする際には、重複排除し、紐付けし、一貫性を維持します。

インポートテンプレートの例は、「定期インポート [の設定」セクションにあります](#setting-up-a-recurring-import) 。

### フラットファイルフォーマットの使用 {#using-flat-file-formats}

インポートで最も効率的なフォーマットは、フラットファイルです。フラットファイルは、データベースレベルで、一括モードでインポートできます。

次に例を示します。

* 区切り記号：タブまたはセミコロン
* 最初の行は見出し
* 文字列の区切り記号なし
* 日付形式：YYYY/MM/DD HH:mm:SS

Adobe Campaign では、標準ファイルインポートアクティビティを使用して XML ファイルをインポートすることはできません。JavaScript を使用して XML ファイルをインポートできますが、ファイルあたり 10,000 レコード未満の少量の場合に限られます。

### 圧縮と暗号化の使用 {#using-compression-and-encryption}

可能であれば、インポートおよびエクスポートに zip 形式のファイルを使用します。

Linux では、コマンドラインを使用して、ファイルを解凍すると同時にインポートできます。次に例を示します。

```
zcat nl6/var/vp/import/filename.gz
```

また、安全でないネットワークを通じて送信するファイルは暗号化することをお勧めします。これには、GPG を使用できます。

### ファイルからのバッチでのデータ読み込み {#loading-data-in-batch-from-files}

ファイルからバッチでデータを読み込むことは、（Web サービスを使用するなどして）一度に 1 行ずつ読み込むよりも効率的です。

Web サービスを使用したインポートは効率的ではありません。可能であれば、ファイルを使用することをお勧めします。

また、リアルタイムでプロファイルをエンリッチメントするための外部 Web サービスの呼び出しは、行レベルで機能するので、パフォーマンスの問題およびメモリリークの原因となることが知られています。

データをインポートする必要がある場合、リアルタイムで Web アプリケーションまたは Web サービスを使用するよりも、ワークフローを使用してバッチでおこなうことをお勧めします。

### データ管理の使用 {#using-data-management}

JavaScript を使用した、繰り返しモード（行ごと）の読み込みは、少量に限定する必要があります。

For better efficiency, always use the **[!UICONTROL Data Loading (File)]** activity in data management workflows.

### 差分モードでのインポート {#importing-in-delta-mode}

標準のインポートは、差分モードでおこなう必要があります。つまり、毎回、テーブル全体ではなく、新規または変更されたデータのみが Adobe Campaign に送信されるようにします。

完全インポートは、最初の読み込みにのみ使用する必要があります。

JavaScript ではなくデータ管理を使用してデータをインポートします。

### 一貫性の維持 {#maintaining-consistency}

Adobe Campaign データベースのデータの一貫性を維持するには、次の原則に従います。

* インポートされたデータが Adobe Campaign の参照テーブルに一致する場合、ワークフローでそのテーブルと紐付けされる必要があります。一致しないレコードは、却下される必要があります。
* インポートされたデータが常に&#x200B;**「正規化」**&#x200B;されている（E メール、電話番号、ダイレクトメールアドレス）ことと、この正規化が信頼でき、何年にもわたって変更されないことを確認します。該当しない場合、データベースに何らかの重複が現れる可能性が高く、Adobe Campaign には「あいまい」一致をおこなうツールがないので、重複を管理および削除することが非常に難しくなります。
* 重複の作成を避けるために、トランザクションデータは、紐付けキーを持ち、既存のデータと紐付けされている必要があります。
* **関連ファイルを順番どおりにインポートします**。

   お互いに依存する複数のファイルでインポートが構成されている場合、ワークフローでファイルが正しい順番でインポートされていることを確認する必要があります。あるファイルが失敗すると、他のファイルはインポートされません。

* データをインポートする際には、**重複排除**&#x200B;し、紐付けし、一貫性を維持します。

## 繰り返し発生するインポートの設定 {#setting-up-a-recurring-import}

同じ構造のファイルを頻繁にインポートする必要がある場合、インポートテンプレートを使用することをお勧めします。

この例では、Adobe Campaign データベースの CRM からのプロファイルのインポートに再利用できるワークフローを事前設定する方法を示します。各アクティビティで使用できるすべての設定について詳しくは、この[節](../../workflow/using/about-activities.md)を参照してください。

1. Create a new workflow template from **[!UICONTROL Resources > Templates > Workflow templates]**.
1. 次のアクティビティを追加します。

   * **[!UICONTROL Data loading (file)]**:インポートするデータを含むファイルの予期される構造を定義します。
   * **[!UICONTROL Enrichment]**:インポートしたデータをデータベースデータと調整します。
   * **[!UICONTROL Split]**:レコードを調整できるかどうかに応じて、レコードを処理するフィルターを作成します。
   * **[!UICONTROL Deduplication]**:データベースに挿入する前に、受信ファイルのデータの重複を除外します。
   * **[!UICONTROL Update data]**:インポートしたプロファイルでデータベースを更新します。
   ![](assets/import_template_example0.png)

1. アクティビティの **[!UICONTROL Data Loading (file)]** 設定：

   * サンプルファイルをアップロードすることで、求められる構造を定義します。サンプルファイルには、インポートに必要なすべての列と、いくつかの行のみが含まれている必要があります。ファイルフォーマットをチェックおよび編集して、各列のタイプが正しく設定されていることを確認します（テキスト、日付、整数など）。次に例を示します。

      ```
      lastname;firstname;birthdate;email;crmID
      Smith;Hayden;23/05/1989;hayden.smith@mailtest.com;123456
      ```

   * セクション **[!UICONTROL Name of the file to load]** で、フィールド **[!UICONTROL Upload a file from the local machine]** を選択し、空白のままにします。 このテンプレートから新しいワークフローを作成するたびに、ここで、定義された構造に対応するファイルを指定できます。

      任意のオプションを使用できますが、それに応じてテンプレートを修正する必要があります。For example, if you select **[!UICONTROL Specified in the transition]**, you can add a **[!UICONTROL File Transfer]** activity before to retrieve the file to import from a FTP/SFTP server. S3またはSFTP接続を使用すると、Adobe Real-time Customer Data Platformを使用して、セグメントデータをAdobe Campaignにインポートすることもできます。 For more on this, refer to this [documentation](https://docs.adobe.com/content/help/en/experience-platform/rtcdp/destinations/destinations-cat/adobe-destinations/adobe-campaign-destination.html).

      ![](assets/import_template_example1.png)

1. アクティビティを設 **[!UICONTROL Enrichment]** 定します。 ここでのこのアクティビティの目的は、受信データを識別することです。

   * In the **[!UICONTROL Enrichment]** tab, select **[!UICONTROL Add data]** and define a link between the imported data and the recipients targeting dimension. この例では、結合条件の作成に **CRM ID** カスタムフィールドが使用されています。一意のレコードを識別できる限り、必要なフィールドまたはフィールドの組み合わせを使用します。
   * タブで、こ **[!UICONTROL Reconciliation]** のオプションはオフのまま **[!UICONTROL Identify the document from the working data]** にします。
   ![](assets/import_template_example2.png)

1. Configure the **[!UICONTROL Split]** activity to retrieve reconciled recipients in one transition and recipients that could not be reconciled but who have enough data in a second transition.

   紐付けされた受信者を含むトランジションは、データベースを更新するために使用できます。不明な受信者を含むトランジションは、ファイルで最小限の情報が利用できる場合、データベースに新しい受信者エントリを作成するために使用できます。

   紐付けできず、十分なデータを持たない受信者は、補集合アウトバウンドトランジションで選択され、別のファイルにエクスポートしたり、単純に無視したりできます。

   * アクティビティ **[!UICONTROL General]** のタブで、「フィルター設定」 **[!UICONTROL Use the additional data only]** を選択し、が自動的に「」に設定され **[!UICONTROL Targeting dimension]** ていることを確認しま **[!UICONTROL Enrichment]**&#x200B;す。

      Check the **[!UICONTROL Generate complement]** option to be able to see if any record cannot be inserted in the database. 必要に応じて、補完データのさらなる処理（ファイルエクスポート、リスト更新など）を適用できます。

   * In the first subset of the **[!UICONTROL Subsets]** tab, add a filtering condition on the inbound population to select only records for which the recipient primary key is not equal to 0. この方法では、データベースの受信者に紐付けされたファイルのデータがそのサブセットで選択されます。

      ![](assets/import_template_example3.png)

   * データベースに挿入される十分なデータを持つ紐付けられていないレコードを選択する 2 番目のサブセットを追加します（例：E メールアドレス、姓名）。

      サブセットは、作成順に処理されます。つまり、2 番目のサブセットが処理されるときに、データベースに既に存在するすべてのレコードは最初のサブセットで既に選択されています。

      ![](assets/import_template_example3_2.png)

   * All records that are not selected in the first two subsets are selected in the **[!UICONTROL Complement]**.

1. Configure the **[!UICONTROL Update data]** activity located after the first outbound transition of the **[!UICONTROL Split]** activity configured previously.

   * Select **[!UICONTROL Update]** as **[!UICONTROL Operation type]** since the inbound transition only contains recipients already present in the database.
   * セクション **[!UICONTROL Record identification]** で、ターゲットデ **[!UICONTROL Using reconciliation keys]** ィメンションと、で作成したリンクとの間のキーを選択して定義しま **[!UICONTROL Enrichment]**&#x200B;す。 この例では、**CRM ID** カスタムフィールドが使用されています。
   * In the **[!UICONTROL Fields to update]** section, indicate the fields from the recipients dimension to update with the value of the corresponding column from the file. ファイル列の名前が受信者ディメンションフィールドの名前と同一またはほとんど同じ場合、自動選択ボタンを使用して、異なるフィールドを自動的に一致させることができます。

      ![](assets/import_template_example6.png)

1. Configure the **[!UICONTROL Deduplication]** activity located after the transition containing unreconciled recipients:

   * Select **[!UICONTROL Edit configuration]** and set the targeting dimension to the temporary schema generated from the **[!UICONTROL Enrichment]** activity of the workflow.

      ![](assets/import_template_example4.png)

   * この例では、一意のプロファイルを見つけるために、E メールフィールドが使用されています。入力されていることがわかっており、一意の組み合わせを構成する任意のフィールドを使用できます。
   * 画面で、オ **[!UICONTROL Deduplication method]** プションを選 **[!UICONTROL Advanced parameters]** 択し、 **[!UICONTROL Disable automatic filtering of 0 ID records]** 0に等しい主キーを持つレコード（この移行のすべてのレコード）が除外されないことを確認します。
   ![](assets/import_template_example7.png)

1. 前に設定したア **[!UICONTROL Update data]** クティビティの後に配置さ **[!UICONTROL Deduplication]** れるアクティビティを設定します。

   * Select **[!UICONTROL Insert]** as **[!UICONTROL Operation type]** since the inbound transition only contains recipients not present in the database.
   * セクション **[!UICONTROL Record identification]** で、を選択し、 **[!UICONTROL Directly using the targeting dimension]** ディメンションを選択 **[!UICONTROL Recipients]** します。
   * In the **[!UICONTROL Fields to update]** section, indicate the fields from the recipients dimension to update with the value of the corresponding column from the file. ファイル列の名前が受信者ディメンションフィールドの名前と同一またはほとんど同じ場合、自動選択ボタンを使用して、異なるフィールドを自動的に一致させることができます。

      ![](assets/import_template_example8.png)

1. After the third transition of the **[!UICONTROL Split]** activity, add a **[!UICONTROL Data extraction (file)]** activity and a **[!UICONTROL File transfer]** activity if you want to keep track of data not inserted in the database. これらのアクティビティを設定して、必要な列をエクスポートし、ファイルを取得可能な FTP または SFTP サーバーにファイルを転送します。
1. Add an **[!UICONTROL End]** activity and save the workflow template.

これで、テンプレートが使用できるようになり、すべての新規ワークフローに利用できます。All is needed is then to specify the file containing the data to import in the **[!UICONTROL Data loading (file)]** activity.

![](assets/import_template_example9.png)

