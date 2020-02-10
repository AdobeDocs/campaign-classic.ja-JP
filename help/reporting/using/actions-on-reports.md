---
title: レポートに対するアクション
seo-title: レポートに対するアクション
description: レポートに対するアクション
seo-description: null
page-status-flag: never-activated
uuid: 7f9d99ab-ce19-46dd-bbf0-79de348d38fb
contentOwner: sauviat
products: SG_CAMPAIGN/CLASSIC
audience: reporting
content-type: reference
topic-tags: creating-new-reports
discoiquuid: 3b9c138e-8f7f-4ee1-9baa-328848d01d3a
index: y
internal: n
snippet: y
translation-type: tm+mt
source-git-commit: af768da6ee8cc0ca2ea1f24f297239b974c113a5

---


# レポートに対するアクション{#actions-on-reports}

レポートを表示している際に、ツールバーを使用すると、一定数のアクションを実行できます。次に、それらについて説明します。

![](assets/s_ncs_advuser_report_wizard_2.png)

ツールバーでは、レポートのエクスポート、印刷、アーカイブ、Web ブラウザーでの表示などをおこなうことができます。

![](assets/s_ncs_advuser_report_wizard_04.png)

## レポートのエクスポート {#exporting-a-report}

レポートのエクスポートフォーマットをドロップダウンリストから選択します。.xls、.pdf、.ods のいずれかです。

![](assets/s_ncs_advuser_report_wizard_06.png)

レポートが複数のページで構成されている場合は、ページごとに操作を繰り返す必要があります。

レポートを PDF、Excel、OpenOffice のいずれかのフォーマットにエクスポートすることを考慮して、レポートを設定できます。Adobe Campaign エクスプローラーを開き、該当するレポートを選択します。

Export options are accessed via the **[!UICONTROL Page]** activities of the report, in the **[!UICONTROL Advanced]** tab.

Change the settings of **[!UICONTROL Paper]** and **[!UICONTROL Margins]** to suit your needs. PDF フォーマットでのページのエクスポートのみ許可することもできます。To do this, uncheck the **[!UICONTROL Activate OpenOffice/Microsoft Excel export]** option.

![](assets/s_ncs_advuser_report_wizard_021.png)

### Microsoft Excel へのエクスポート {#exporting-into-microsoft-excel}

For **[!UICONTROL List with group]** type reports destined to be exported into Excel, the following recommendations and limitations apply:

* これらのレポートには空行を含めないでください。

   ![](assets/export_limitations_remove_empty_line.png)

* リストの凡例は非表示にしてください。

   ![](assets/export_limitations_hide_label.png)

* レポートでは、セルレベルで定義した特定の書式設定を使用する必要はありません。It is preferable to use **[!UICONTROL Form rendering]** to define the format of the cells in the table. は、を **[!UICONTROL Form rendering]** 使用してアクセスできま **[!UICONTROL Administration > Configuration > Form rendering]**&#x200B;す。
* HTML コンテンツの挿入はお勧めしません。
* レポートに、テーブルやグラフなどのタイプの要素が複数含まれている場合、それらは 1 つずつ順にエクスポートされます。
* セル内で強制的に復帰改行させることができます。この設定は Excel でも保たれます。詳しくは、この「セル・フォーマットの定義」を [参照してください](../../reporting/using/creating-a-table.md#defining-cell-format)。

### エクスポートの先送り {#postpone-the-export}

レポートのエクスポートを先送りして、例えば、非同期呼び出しを待つことができます。それには、ページの初期化スクリプトに次のように入力します。

```
document.nl_waitBeforeRender = true;
```

エクスポートを有効にし、PDF への変換を開始するには、パラメーターのない **document.nl_renderToPdf()** 関数を使用します。

### メモリ割り当て {#memory-allocation}

ある種の大規模なレポートをエクスポートする際には、メモリ割り当てエラーが発生する可能性があります。

あるインスタンスでは、設定ファイル **serverConf.xml** で指定されている JavaScript の **maxMB**（ホストされたインスタンスの場合は **SKMS**）のデフォルト値は 64 MB に設定されています。レポートのエクスポート中にメモリ不足エラーが発生した場合は、次のように、この数値を 512 MB に増やしてみることをお勧めします。

```
<javaScript maxMB="512" stackSizeKB="8"/>
```

変更内容を設定に適用するには、**nlserver** サービスを再起動する必要があります。

**serverConf.xml** ファイルについて詳しくは、[この節](../../production/using/configuration-principle.md)を参照してください。

**nlserver** サービスについて詳しくは、[この節](../../production/using/administration.md)を参照してください。

## レポートの印刷 {#printing-a-report}

レポートを印刷できます。それには、プリンターアイコンをクリックします。すると、ダイアログボックスが開きます。

より良い結果を得るには、Internet Explorerの印刷オプションを編集し、を選択しま **[!UICONTROL Print background colors and images]**&#x200B;す。

![](assets/s_ncs_advuser_report_print_options.png)

## レポートアーカイブの作成 {#creating-report-archives}

レポートをアーカイブすることで、様々な期間でレポートの表示を作成して、例えば、一定期間にわたる統計を表示できます。

アーカイブを作成するには、該当するレポートを開き、適切なアイコンをクリックします。

![](assets/s_ncs_advuser_report_wizard_07.png)

既存のアーカイブを表示または非表示にするには、表示／非表示アイコンをクリックします。

![](assets/s_ncs_advuser_report_history_06.png)

アーカイブの日付が表示／非表示アイコンの下に表示されます。目的のアーカイブをクリックすると、それが表示されます。

![](assets/s_ncs_advuser_report_history_04.png)

レポートアーカイブを削除できます。それには、レポートが格納されている Adobe Campaign ノードに移動します。Click the **[!UICONTROL Archives]** tab, select the one you want to delete and click **[!UICONTROL Delete]**.

![](assets/s_ncs_advuser_report_history_01.png)

