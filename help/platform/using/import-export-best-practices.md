---
product: campaign
title: インポートとエクスポートのベストプラクティス
description: データのインポートまたはエクスポート時に従うべきベストプラクティスについて詳しく学ぶ
feature: Data Management
badge-v8: label="v8 にも適用されます" type="Positive" tooltip="Campaign v8 にも適用されます"
audience: automating
content-type: reference
topic-tags: workflow-general-operation
exl-id: 03d35202-d221-4136-aad4-00704aabb356
source-git-commit: e34718caefdf5db4ddd61db601420274be77054e
workflow-type: tm+mt
source-wordcount: '527'
ht-degree: 100%

---

# インポートとエクスポートのベストプラクティス {#import-export-best-practices}



次に説明するいくつかのシンプルなルールに注意して従うと、データベース内のデータの一貫性を確保し、データベースの更新時またはデータのエクスポート時の一般的なエラーを避けるのに非常に有効です。

## ワークフローテンプレートの使用 {#using-import-templates}

データのインポートを目的としたワークフローのほとんどには、**[!UICONTROL ファイルの読み込み]**、**[!UICONTROL 紐付け]**、**[!UICONTROL セグメント化]**、**[!UICONTROL 重複の除外]**、**[!UICONTROL データの更新]**&#x200B;の各アクティビティが含まれている必要があります。

ワークフローテンプレートを使用すると、同様のインポートを準備したり、データベース内のデータの一貫性を確保したりするのに非常に便利です。

プロジェクトで使用されるファイルには重複はないので、多くのプロジェクトでは、インポートは「**[!UICONTROL 重複排除]**」アクティビティなしで作成されます。複数のファイルをインポートすると、重複が発生する場合があります。そうなると、重複排除は困難になります。そのため、すべてのインポートワークフローで重複排除ステップを設けることは、優れた予防措置となります。

受信データは一貫性があり正しいとか、IT 部門や Adobe Campaign スーパーバイザーが対処するとは思わないでください。プロジェクトの間、データクレンジングに留意してください。データをインポートする際には、重複排除し、紐付けし、一貫性を維持します。

データのインポート用に設計された汎用ワークフローテンプレートの例は、「[例：データインポート用ワークフローテンプレート](../../platform/using/creating-import-export-templates.md)」節で紹介されています。

## フラットファイルフォーマットの使用 {#using-flat-file-formats}

インポートで最も効率的なフォーマットは、フラットファイルです。フラットファイルは、データベースレベルで、一括モードでインポートできます。

次に例を示します。

* 区切り記号：タブまたはセミコロン
* 最初の行は見出し
* 文字列の区切り記号なし
* 日付形式：`YYYY/MM/DD HH:mm:SS`

インポートするファイルの例：

```
lastname;firstname;birthdate;email;crmID
Smith;Hayden;23/05/1989;hayden.smith@example.com;124365
Mars;Daniel;17/11/1987;dannymars@example.com;123545
Smith;Clara;08/02/1989;hayden.smith@example.com;124567
Durance;Allison;15/12/1978;allison.durance@example.com;120987
```

## 圧縮の使用 {#using-compression}

可能な限り、圧縮されたファイルをインポートおよびエクスポートに使用します。GZIP がデフォルトでサポートされています。 **[!UICONTROL ファイルの読み込み]**&#x200B;および&#x200B;**[!UICONTROL ファイルの抽出]**&#x200B;ワークフローアクティビティでは、それぞれ、ファイルのインポート時に前処理を追加したり、データ抽出時に後処理を追加したりできます。

**関連トピック：**

* [データ読み込み（ファイル）アクティビティ](../../workflow/using/data-loading-file.md)
* [データ抽出（ファイル）アクティビティ](../../workflow/using/extraction-file.md)

## 差分モードでのインポート {#importing-in-delta-mode}

定期的インポートは、差分モードでおこなう必要があります。つまり、毎回、テーブル全体ではなく、新規または変更されたデータのみが Adobe Campaign に送信されるようにします。

完全インポートは、最初の読み込みにのみ使用する必要があります。

## 一貫性の維持 {#maintaining-consistency}

Adobe Campaign データベースのデータの一貫性を維持するには、次の原則に従います。

* インポートされたデータが Adobe Campaign の参照テーブルに一致する場合、ワークフローでそのテーブルと紐付けされる必要があります。一致しないレコードは、却下される必要があります。
* インポートされたデータが常に&#x200B;**「正規化」**&#x200B;されている（メール、電話番号、ダイレクトメールアドレス）ことと、この正規化が信頼でき、何年にもわたって変更されないことを確認します。該当しない場合、データベースに何らかの重複が現れる可能性が高く、Adobe Campaign には「あいまい」一致をおこなうツールがないので、重複を管理および削除することが非常に難しくなります。
* 重複の作成を避けるために、トランザクションデータは、紐付けキーを持ち、既存のデータと紐付けされている必要があります。
* **関連ファイルを順番どおりにインポートします**。お互いに依存する複数のファイルでインポートが構成されている場合、ワークフローでファイルが正しい順番でインポートされていることを確認する必要があります。あるファイルが失敗すると、他のファイルはインポートされません。
* データをインポートする際には、**重複排除**&#x200B;し、紐付けし、一貫性を維持します。
