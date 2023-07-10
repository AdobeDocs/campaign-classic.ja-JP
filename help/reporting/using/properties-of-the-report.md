---
product: campaign
title: レポートのプロパティ
description: レポートプロパティ設定の詳細
badge-v7: label="v7" type="Informative" tooltip="Applies to Campaign Classic v7"
badge-v8: label="v8" type="Positive" tooltip="Also applies to Campaign v8"
feature: Reporting
exl-id: dfa9d329-1086-4f6d-9d03-df159cad5495
source-git-commit: 6dc6aeb5adeb82d527b39a05ee70a9926205ea0b
workflow-type: tm+mt
source-wordcount: '451'
ht-degree: 100%

---

# レポートのプロパティ{#properties-of-the-report}



必要に応じて、レポートを完全にパーソナライズしたり、設定したりできます。それには、レポートのプロパティを編集します。レポートのプロパティには、アクティビティ順序チャートの上にある「**[!UICONTROL プロパティ]**」ボタンをクリックしてアクセスします。

![](assets/s_ncs_advuser_report_properties_01.png)

一般的なプロパティについては、以下に説明します。「**[!UICONTROL パラメーター]**」、「**[!UICONTROL 変数]**」、「**[!UICONTROL スクリプト]**」の各タブで設定される高度な機能については、[この節](../../reporting/using/advanced-functionalities.md)で説明します。

## 一般的なプロパティ {#overall-properties}

レポートプロパティの「**[!UICONTROL 一般]**」タブで、次に示す設定を編集できます。

* レポートのラベルと内部名。「**[!UICONTROL 内部名]**」は、レポートの最終 URL に使用されます。レポートの作成後は変更しないでください。

* レポート&#x200B;**フォルダー**&#x200B;はレポートの作成時に選択されます。ベストプラクティスは、[ビルトインレポート](../../reporting/using/about-campaign-built-in-reports.md)と混在しないように、カスタムレポート専用のフォルダーを作成することです。

* **ストレージ**&#x200B;はレポートの作成時に選択されます。レポートのデータテーブルを変更するには、「**[!UICONTROL ドキュメントタイプ]**」フィールドの右にある「**[!UICONTROL リンクを選択]**」アイコンをクリックします。

  ![](assets/s_ncs_advuser_report_properties_02.png)

* **アクセス制御**&#x200B;パラメーター。これらの設定については、以下で説明します。

## レポートへのアクセスの制御 {#report-accessibility}

レポートは、Adobe Campaign コンソールまたは Web ブラウザーからアクセスできます。その場合は、次に示すように、レポートへのアクセス制御の設定が必要になることがあります。

![](assets/s_ncs_advuser_report_properties_02b.png)

選択できるオプションは次のとおりです。

* **[!UICONTROL 匿名アクセス]**：このオプションでは、レポートへの無制限アクセスが可能になります。ただし、操作はできません。

  「Web アプリ」テクニカルオペレーターの権限は、レポート要素を表示するために使用されます。 詳しくは、[この節](../../platform/using/access-management-operators.md)を参照してください。

* **[!UICONTROL アクセス制御]**：このオプションでは、Adobe Campaign オペレーターがログオン後にレポートにアクセスできるようになります。
* **[!UICONTROL 特定のアカウントを使用]**：このオプションでは、「**[!UICONTROL オペレーター]**」フィールドで選択したオペレーターの権限でレポートを実行できるようになります。

## レポートを翻訳 {#report-localization}

レポートの翻訳先の言語を設定できます。それには、「**[!UICONTROL ローカライゼーション]**」タブをクリックします。

![](assets/s_ncs_advuser_report_properties_06.png)

編集言語は、書き込む際に使用する言語です。言語を追加すると、レポート編集ページにサブタブが表示されます。

![](assets/s_ncs_advuser_report_properties_05a.png)

>[!NOTE]
>
>Campaign での Web ページのローカライゼーションについて詳しくは、[この節](../../web/using/translating-a-web-form.md)を参照してください。

## HTML レンダリングのパーソナライズ {#personalizing-html-rendering}

「**[!UICONTROL レンダリング]**」タブでは、ページのデータ表示モードをパーソナライズできます。次の項目を選択できます。

* レポートでのナビゲーションタイプ（ボタンによるか、リンクによるか）。
* レポート要素のラベルのデフォルト位置。この位置は、要素ごとにオーバーロードできます。
* レポートページの生成に使用されるテンプレートまたはテーマ。

![](assets/s_ncs_advuser_report_properties_08.png)

## エラーページのパーソナライズ {#personalizing-the-error-page}

「**[!UICONTROL エラーページ]**」タブでは、レポートの表示でエラーが発生した場合に出力されるメッセージを設定できます。

テキストを定義し、レポートのローカライゼーションを管理する特定の識別子にそれらのテキストをリンクできます。詳しくは、[ヘッダーやフッターの追加](../../reporting/using/element-layout.md#adding-a-header-and-a-footer)を参照してください。

![](assets/s_ncs_advuser_report_properties_11.png)
