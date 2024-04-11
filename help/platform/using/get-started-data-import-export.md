---
product: campaign
title: データのインポートとエクスポートの基本を学ぶ
description: Campaign でのデータのインポートとエクスポートについて詳しく学ぶ
feature: Data Management, Encryption
badge-v8: label="v8 にも適用されます" type="Positive" tooltip="Campaign v8 にも適用されます"
audience: platform
content-type: reference
topic-tags: importing-and-exporting-data
exl-id: d6055d97-75fc-4ed7-89bd-8336157454eb
source-git-commit: e34718caefdf5db4ddd61db601420274be77054e
workflow-type: tm+mt
source-wordcount: '334'
ht-degree: 98%

---

# データのインポートとエクスポートの基本を学ぶ {#get-started-data-import-export}



Adobe Campaign Classic は、データのインポートとエクスポートを可能にするデータ管理機能を備えています。 これらの操作は、ワークフローまたは一般的なインポートおよびエクスポートのいずれかを使用して実行できます。

>[!IMPORTANT]
>
>この機能を使用する際は、Adobe Campaign の契約条件が定める SFTP ストレージ、データベースストレージ、アクティブプロファイルの制限に注意してください。

## ワークフロー {#workflows}

<img src="assets/do-not-localize/icon_workflows.svg" width="60px">

**ワークフロー**&#x200B;は、インポートプロセスを自動化する便利な方法です。データをローカルファイルからインポートするか、SFTP からインポートするかに関係なく、データ管理手順を標準化することができます。

ワークフローを使用すると、例えば複数の情報システム間のデータ交換を自動化するために、インポートとエクスポートの操作をスケジュールに従って自動的に繰り返すことができます。

詳しくは、[この節](../../platform/using/import-export-workflows.md)を参照してください。

## 一般的なインポートおよびエクスポート {#generic-import-export}

<img src="assets/do-not-localize/icon_templates.svg" width="60px">

また、Campaign Classic には、不定期のインポート／エクスポートジョブを作成できる&#x200B;**一般的なインポートおよびエクスポート**&#x200B;が用意されています。

インポートとエクスポートは、インポートおよびエクスポートジョブを起動および監視するように設定および使用できる専用のテンプレートで設定されます。

一般的なインポートおよびエクスポートの詳細については、[こちらの節](../../platform/using/about-generic-imports-exports.md)を参照してください。

>[!IMPORTANT]
>一般的なインポートおよびエクスポートは、不定期の操作にのみ使用します。データの一貫性を確保し効率を向上させるには、ワークフローを使用してインポートおよびエクスポート操作を実行することをお勧めします。

## データの暗号化と圧縮 {#data-encryption-compression}

<img src="assets/do-not-localize/icon_encrypt.svg" width="60px">

Campaign Classic では、圧縮ファイルまたは暗号化ファイルのインポートやエクスポートが可能です。

これらの操作は、活用するデータに前処理段階を適用することで、ワークフロー内で実行されます。

詳しくは、以下の節を参照してください。

* [ファイルの解凍または復号化](../../platform/using/unzip-decrypt.md)
* [ファイルの圧縮または暗号化](../../platform/using/zip-encrypt.md)

## ベストプラクティスとトラブルシューティング {#best-practices-troubleshooting}

<img src="assets/do-not-localize/icon_bestpractices.svg" width="60px">

データベース内のデータの一貫性を確保し、更新操作時やエクスポート操作時によく発生するエラーを避けるために、インポート操作とエクスポート操作を実行する際は、いくつかの[ベストプラクティス](../../platform/using/import-export-best-practices.md)に従ってください。

また、SFTP サーバーの使用に関するレコメンデーションとよくある問題については、[この節](../../platform/using/sftp-server-usage.md)を参照してください。
